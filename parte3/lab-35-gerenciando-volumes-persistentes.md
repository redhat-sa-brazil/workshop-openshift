# Persistent Storage Using NFS

* [Overview](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#overview)
* [Provisioning](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-provisioning)
* [Enforcing Disk Quotas](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-enforcing-disk-quotas)
* [NFS Volume Security](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-volume-security)
  * [Group IDs](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-supplemental-groups)
  * [User IDs](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-user-ids)
  * [SELinux](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-selinux)
  * [Export Settings](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-export-settings)
* [Reclaiming Resources](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-reclaiming-resources)
* [Automation](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-automation)
* [Additional Configuration and Troubleshooting](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-additional-config-and-troubleshooting)

## Overview {#overview}

OpenShift Origin clusters can be provisioned with[persistent storage](https://docs.openshift.org/latest/architecture/additional_concepts/storage.html#architecture-additional-concepts-storage)using NFS. Persistent volumes \(PVs\) and persistent volume claims \(PVCs\) provide a convenient method for sharing a volume across a project. While the NFS-specific information contained in a PV definition could also be defined directly in a pod definition, doing so does not create the volume as a distinct cluster resource, making the volume more susceptible to conflicts.

This topic covers the specifics of using the NFS persistent storage type. Some familiarity with OpenShift Origin and[NFS](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/ch-nfs.html)is beneficial. See the[Persistent Storage](https://docs.openshift.org/latest/architecture/additional_concepts/storage.html#architecture-additional-concepts-storage)concept topic for details on the OpenShift Origin persistent volume \(PV\) framework in general.

## Provisioning {#nfs-provisioning}

Storage must exist in the underlying infrastructure before it can be mounted as a volume in OpenShift Origin. To provision NFS volumes, a list of NFS servers and export paths are all that is required.

You must first create an object definition for the PV:

Example 1. PV Object Definition Using NFS

```
apiVersion
: 
v1
kind
: 
PersistentVolume
metadata
:
  
name
: 
pv0001 
spec
:
  
capacity
:
    
storage
: 
5Gi 
accessModes
:
  - 
ReadWriteOnce 
nfs
: 
path
: 
/tmp 
server
: 
172.17.0.2 
persistentVolumeReclaimPolicy
: 
Recycle 
```

|  | The name of the volume. This is the PV identity in various`oc <command> pod`commands. |
| :--- | :--- |
|  | The amount of storage allocated to this volume. |
|  | Though this appears to be related to controlling access to the volume, it is actually used similarly to labels and used to match a PVC to a PV. Currently, no access rules are enforced based on the**`accessModes`**. |
|  | The volume type being used, in this case the**nfs**plug-in. |
|  | The path that is exported by the NFS server. |
|  | The host name or IP address of the NFS server. |
|  | The reclaim policy for the PV. This defines what happens to a volume when released from its claim. Valid options are**Retain**\(default\) and**Recycle**. See[Reclaiming Resources](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-reclaiming-resources). |

|  | Each NFS volume must be mountable by all schedulable nodes in the cluster. |
| :--- | :--- |


Save the definition to a file, for example_**nfs-pv.yaml**_, and create the PV:

```
$ oc create -f nfs-pv.yaml
persistentvolume "pv0001" created
```

Verify that the PV was created:

```
# oc get pv
NAME                     LABELS    CAPACITY     ACCESSMODES   STATUS      CLAIM     REASON    AGE
pv0001                   
<
none
>
    5368709120   RWO           Available                       31s
```

The next step can be to create a persistent volume claim \(PVC\) which will bind to the new PV:

Example 2. PVC Object Definition

```
apiVersion
: 
v1
kind
: 
PersistentVolumeClaim
metadata
:
  
name
: 
nfs-claim1
spec
:
  
accessModes
:
    - 
ReadWriteOnce 
resources
:
    
requests
:
      
storage
: 
1Gi 
```

|  | As mentioned above for PVs, the**`accessModes`**do not enforce security, but rather act as labels to match a PV to a PVC. |
| :--- | :--- |
|  | This claim will look for PVs offering**1Gi**or greater capacity. |

Save the definition to a file, for example_**nfs-claim.yaml**_, and create the PVC:

```
# oc create -f nfs-claim.yaml
```

## Enforcing Disk Quotas {#nfs-enforcing-disk-quotas}

You can use disk partitions to enforce disk quotas and size constraints. Each partition can be its own export. Each export is one PV. OpenShift Origin enforces unique names for PVs, but the uniqueness of the NFS volume’s server and path is up to the administrator.

Enforcing quotas in this way allows the developer to request persistent storage by a specific amount \(for example, 10Gi\) and be matched with a corresponding volume of equal or greater capacity.

## NFS Volume Security {#nfs-volume-security}

This section covers NFS volume security, including matching permissions and SELinux considerations. The reader is expected to understand the basics of POSIX permissions, process UIDs, supplemental groups, and SELinux.

|  | See the full[Volume Security](https://docs.openshift.org/latest/install_config/persistent_storage/pod_security_context.html#install-config-persistent-storage-pod-security-context)topic before implementing NFS volumes. |
| :--- | :--- |


Developers request NFS storage by referencing, in the**`volumes`**section of their pod definition, either a PVC by name or the NFS volume plug-in directly.

The_**/etc/exports**_file on the NFS server contains the accessible NFS directories. The target NFS directory has POSIX owner and group IDs. The OpenShift Origin NFS plug-in mounts the container’s NFS directory with the same POSIX ownership and permissions found on the exported NFS directory. However, the container is not run with its effective UID equal to the owner of the NFS mount, which is the desired behavior.

As an example, if the target NFS directory appears on the NFS server as:

```
# ls -lZ /opt/nfs -d
drwxrws---. nfsnobody 5555 unconfined_u:object_r:usr_t:s0   /opt/nfs

# id nfsnobody
uid=65534(nfsnobody) gid=65534(nfsnobody) groups=65534(nfsnobody)
```

Then the container must match SELinux labels, and either run with a UID of**65534**\(**nfsnobody**owner\) or with**5555**in its supplemental groups in order to access the directory.

|  | The owner ID of 65534 is used as an example. Even though NFS’s**root\_squash**maps**root**\(0\) to**nfsnobody**\(65534\), NFS exports can have arbitrary owner IDs. Owner 65534 is not required for NFS exports. |
| :--- | :--- |


### Group IDs {#nfs-supplemental-groups}

The recommended way to handle NFS access \(assuming it is not an option to change permissions on the NFS export\) is to use supplemental groups. Supplemental groups in OpenShift Origin are used for shared storage, of which NFS is an example. In contrast, block storage, such as Ceph RBD or iSCSI, use the**fsGroup**SCC strategy and the**fsGroup**value in the pod’s**`securityContext`**.

|  | It is generally preferable to use supplemental group IDs to gain access to persistent storage versus using[user IDs](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-user-ids). Supplemental groups are covered further in the full[Volume Security](https://docs.openshift.org/latest/install_config/persistent_storage/pod_security_context.html#supplemental-groups)topic. |
| :--- | :--- |


Because the group ID on the[example target NFS directory](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-export)shown above is 5555, the pod can define that group ID using**`supplementalGroups`**under the pod-level**`securityContext`**definition. For example:

```
spec:
  containers:
    - name:
    ...
  securityContext: 

    supplementalGroups: [5555] 
```

|  | **`securityContext`**must be defined at the pod level, not under a specific container. |
| :--- | :--- |
|  | An array of GIDs defined for the pod. In this case, there is one element in the array; additional GIDs would be comma-separated. |

Assuming there are no custom SCCs that might satisfy the pod’s requirements, the pod will likely match the**restricted**SCC. This SCC has the**`supplementalGroups`**strategy set to**RunAsAny**, meaning that any supplied group ID will be accepted without range checking.

As a result, the above pod will pass admissions and will be launched. However, if group ID range checking is desired, a custom SCC, as described in[pod security and custom SCCs](https://docs.openshift.org/latest/install_config/persistent_storage/pod_security_context.html#scc-supplemental-groups), is the preferred solution. A custom SCC can be created such that minimum and maximum group IDs are defined, group ID range checking is enforced, and a group ID of 5555 is allowed.

|  | In order to use a custom SCC, you must first add it to the appropriate service account. For example, use the`default`service account in the given project unless another has been specified on the pod specification. See[Add an SCC to a User, Group, or Project](https://docs.openshift.org/latest/admin_guide/manage_scc.html#add-scc-to-user-group-project)for details. |
| :--- | :--- |


### User IDs {#nfs-user-ids}

User IDs can be defined in the container image or in the pod definition. The full[Volume Security](https://docs.openshift.org/latest/install_config/persistent_storage/pod_security_context.html#user-id)topic covers controlling storage access based on user IDs, and should be read prior to setting up NFS persistent storage.

|  | It is generally preferable to use[supplemental group IDs](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-supplemental-groups)to gain access to persistent storage versus using user IDs. |
| :--- | :--- |


In the[example target NFS directory](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-export)shown above, the container needs its UID set to 65534 \(ignoring group IDs for the moment\), so the following can be added to the pod definition:

```
spec
:
  
containers
: 

  - 
name:
...
securityContext
:
      
runAsUser
: 
65534 
```

|  | Pods contain a**`securtityContext`**specific to each container \(shown here\) and a pod-level**`securityContext`**which applies to all containers defined in the pod. |
| :--- | :--- |
|  | 65534 is the**nfsnobody**user. |

Assuming the**default**project and the**restricted**SCC, the pod’s requested user ID of 65534 will, unfortunately, not be allowed, and therefore the pod will fail. The pod fails because of the following:

* It requests 65534 as its user ID.

* All SCCs available to the pod are examined to see which SCC will allow a user ID of 65534 \(actually, all policies of the SCCs are checked but the focus here is on user ID\).

* Because all available SCCs use**MustRunAsRange**for their**`runAsUser`**strategy, UID range checking is required.

* 65534 is not included in the SCC or project’s user ID range.

It is generally considered a good practice not to modify the predefined SCCs. The preferred way to fix this situation is to create a custom SCC, as described in the full[Volume Security](https://docs.openshift.org/latest/install_config/persistent_storage/pod_security_context.html#scc-runasuser)topic. A custom SCC can be created such that minimum and maximum user IDs are defined, UID range checking is still enforced, and the UID of 65534 will be allowed.

|  | In order to use a custom SCC, you must first add it to the appropriate service account. For example, use the`default`service account in the given project unless another has been specified on the pod specification. See[Add an SCC to a User, Group, or Project](https://docs.openshift.org/latest/admin_guide/manage_scc.html#add-scc-to-user-group-project)for details. |
| :--- | :--- |


### SELinux {#nfs-selinux}

|  | See the full[Volume Security](https://docs.openshift.org/latest/install_config/persistent_storage/pod_security_context.html#selinuxoptions)topic for information on controlling storage access in conjunction with using SELinux. |
| :--- | :--- |


By default, SELinux does not allow writing from a pod to a remote NFS server. The NFS volume mounts correctly, but is read-only.

To enable writing to NFS volumes with SELinux enforcing on each node, run:

```
# setsebool -P virt_use_nfs 1
```

The`-P`option above makes the bool persistent between reboots.

The**virt\_use\_nfs**boolean is defined by the_**docker-selinux**_package. If an error is seen indicating that this bool is not defined, ensure this package has been installed.

### Export Settings {#nfs-export-settings}

In order to enable arbitrary container users to read and write the volume, each exported volume on the NFS server should conform to the following conditions:

* Each export must be:

  ```
  /
  <
  example_fs
  >
   *(rw,root_squash)
  ```

* The firewall must be configured to allow traffic to the mount point.

  * For NFSv4, configure the default port`2049`\(**nfs**\) and port`111`\(**portmapper**\).

    NFSv4
    ```
    # iptables -I INPUT 1 -p tcp --dport 2049 -j ACCEPT
    # iptables -I INPUT 1 -p tcp --dport 111 -j ACCEPT
    ```

  * For NFSv3, there are three ports to configure:`2049`\(**nfs**\),`20048`\(**mountd**\), and`111`\(**portmapper**\).

    NFSv3
    ```
    # iptables -I INPUT 1 -p tcp --dport 2049 -j ACCEPT
    # iptables -I INPUT 1 -p tcp --dport 20048 -j ACCEPT
    # iptables -I INPUT 1 -p tcp --dport 111 -j ACCEPT
    ```

* The NFS export and directory must be set up so that it is accessible by the target pods. Either set the export to be owned by the container’s primary UID, or supply the pod group access using**`supplementalGroups`**, as shown in[Group IDs](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-supplemental-groups)above. See the full[Volume Security](https://docs.openshift.org/latest/install_config/persistent_storage/pod_security_context.html#install-config-persistent-storage-pod-security-context)topic for additional pod security information as well.

## Reclaiming Resources {#nfs-reclaiming-resources}

NFS implements the OpenShift Origin**Recyclable**plug-in interface. Automatic processes handle reclamation tasks based on policies set on each persistent volume.

By default, persistent volumes are set to**Retain**. NFS volumes which are set to**Recycle**are scrubbed \(i.e.,`rm -rf`is run on the volume\) after being released from their claim \(i.e, after the user’s**`PersistentVolumeClaim`**bound to the volume is deleted\). Once recycled, the NFS volume can be bound to a new claim.

## Automation {#nfs-automation}

Clusters can be provisioned with persistent storage using NFS in the following ways:

* [Enforce storage quotas](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-enforcing-disk-quotas)using disk partitions.

* Enforce security by[restricting volumes](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-volume-security)to the project that has a claim to them.

* Configure[reclamation of discarded resources](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#nfs-reclaiming-resources)for each PV.

They are many ways that you can use scripts to automate the above tasks. You can use an[example Ansible playbook](https://github.com/openshift/openshift-ansible/tree/master/roles/openshift_node_certificates)to help you get started.

## Additional Configuration and Troubleshooting {#nfs-additional-config-and-troubleshooting}

Depending on what version of NFS is being used and how it is configured, there may be additional configuration steps needed for proper export and security mapping. The following are some that may apply:

| NFSv4 mount incorrectly shows all files with ownership of**nobody:nobody** | Could be attributed to the ID mapping settings \(/etc/idmapd.conf\) on your NFSSee[this Red Hat Solution](https://access.redhat.com/solutions/33455). |
| :--- | :--- |
| Disabling ID mapping on NFSv4 | On both the NFS client and server, run:\# echo 'Y' &gt; /sys/modulefsd/parametersfs4\_disable\_idmapping |



