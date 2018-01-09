## System Requirements {#system-requirements}

The following sections identify the hardware specifications and system-level requirements of all hosts within your OpenShift Origin environment.

### Minimum Hardware Requirements {#hardware}

The system requirements vary per host type:

| [Masters](https://docs.openshift.org/latest/architecture/infrastructure_components/kubernetes_infrastructure.html#master) | Physical or virtual system, or an instance running on a public or private IaaS.Base OS: Fedora 21, CentOS 7.3, RHEL 7.3, or RHEL 7.4 with the "Minimal" installation option and the latest packages from the Extras channel, or RHEL Atomic Host 7.4.2 or later.2 vCPU.Minimum 16 GB RAM.Minimum 40 GB hard disk space for the file system containing_**/var/**_.![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABcAAAAWCAYAAAArdgcFAAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAB3RJTUUH4QcFDi0d3YBVmQAAAeFJREFUOMu91b9LG2Ecx/H3XWx+XCJEShexQsyQtkEu2EmHI1s7FncjTo27Q/+Dkq1ORhAXCehk8S8IBwZzU0QIVtAcpZuCQu6xpq13HUpSmtwl1zT24Kbnntd9+D58n6/kOI7DAz1jfVfv77k5OEBUq9zWatzWaiBJKJnMr3dujonFRQgEXLdLXslbFxc0lpYQlUrf/0cXFkjs7BCamelZk902XG1tUVfVgTCAqFSoqypX29uDk18Wi3xeXR2qxtMbGzzJ593x1vk5dVXFFmIoXI5GeXF8TCiZ7CqLbdPI5TzhsVfvSV07vLzeZyLkjttC0FheBtv+ExeG4VHjEJG3+zz7+I5YfHB6cXiIMIwu/OjI/etUnukPr6Fc5Mb0V5621cEtL/xTETOb5fTNLt991t7qxj2T06JVrfLjLw62J7l9dzeytm9bHVzJZEaGt63/g0dGiLetTofaQnA6P8/Xk5N/gsPpNM8NA1lRfieXo1ESpRJSMDg0LAWDJPf2kBWl91aMzM4yVSgMjU8VCoTT6f73+eXmJl/W1rAtyxcaiMd5ur7O41zO37D4ZpqYKys0y+W+8Hg2S6JU4tHkpP9J1OnPszOauk5T17F0HRyHmKYxrmnENI1wKuV9Bg85oH8CT8DJrJGjGicAAAAASUVORK5CYII= "redcircle 1")Minimum 1 GB hard disk space for the file system containing_**/usr/local/bin/**_.Minimum 1 GB hard disk space for the file system containing the system’s temporary directory.![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABcAAAAWCAYAAAArdgcFAAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAB3RJTUUH4QcFDi4QiBx65wAAAmhJREFUOMu11T9IG1EcwPFvoiYxF6nSWor4L8YSbZA77FIdQsZ2qrjUxaibTrUgdHU0U+ukgohFAmYyddGtGjBophOpiFVj/0BbtKCY00s1lw5tUqp3iaT44Kb33ud+7/d4v58pnU6nuaFRnHM2leJofh5lbY1TWeZUlsFkwi5Jv7/WVio6O6GoSHe7ySjy5N4e8e5ulGg05/+F9nacMzNYGxquzJn1NhxOTrIpinlhACUaZVMUOZyayh/5wfg4nwYGCspx7dgYlf39+nhyd5dNUURTlIJwsyDwYH0dq8t1KS2aRtzvvwpb3VS8mqP56xkP02eI8XfUPq3TxTVFId7TA5r2L67EYro5Lu4YoWawA4sqc7wok7rno3J2mjt1BnewsoISi13CV1d1F1+Eetnt8PHe2cbOEx+fw0dga0Kotxpf8h8riycMcDhGebvMBYC1CYdUDuoWylbSEE9cxhVDPDNu4RiZ5m6Tijo+zI/v5I08+0I1Vc0JCy8XcQ1KnId72XmxTK6akbGykdslyWCpldLnYRpHJFLhXj50vSGZ54wZKy9u6Znl/msfxeo3zm1d1IQXaFyYo/ZZXV48m5ZSXdyK5ZFECYCtHsfj+uyMKg9D6KMunrGyL1RTFLba2jjb2PivMmvzeGiOxTDb7X/TYhYEnMEgJoulYNhkseAKhTDb7VerYmlLC9WBQMF4dSCAzePJXc8PJib4MjSElkhcCy0qL6dmdJTbfv/1msXP/X32+/o4WVrKCZf5fDiDQUqqqq7fibJleHubk0iEk0iERCQC6TQOr5cyrxeH14vN7Ta+g5ts0L8Ax+z488wl6EkAAAAASUVORK5CYII= "redcircle 2") |
| :--- | :--- |
| [Nodes](https://docs.openshift.org/latest/architecture/infrastructure_components/kubernetes_infrastructure.html#node) | Physical or virtual system, or an instance running on a public or private IaaS.Base OS: Fedora 21, CentOS 7.3 or 7.4, RHEL 7.3 or 7.4 with "Minimal" installation option, or RHEL Atomic Host 7.4.2 or later.NetworkManager 1.0 or later.1 vCPU.Minimum 8 GB RAM.Minimum 15 GB hard disk space for the file system containing_**/var/**_.![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABcAAAAWCAYAAAArdgcFAAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAB3RJTUUH4QcFDi0d3YBVmQAAAeFJREFUOMu91b9LG2Ecx/H3XWx+XCJEShexQsyQtkEu2EmHI1s7FncjTo27Q/+Dkq1ORhAXCehk8S8IBwZzU0QIVtAcpZuCQu6xpq13HUpSmtwl1zT24Kbnntd9+D58n6/kOI7DAz1jfVfv77k5OEBUq9zWatzWaiBJKJnMr3dujonFRQgEXLdLXslbFxc0lpYQlUrf/0cXFkjs7BCamelZk902XG1tUVfVgTCAqFSoqypX29uDk18Wi3xeXR2qxtMbGzzJ593x1vk5dVXFFmIoXI5GeXF8TCiZ7CqLbdPI5TzhsVfvSV07vLzeZyLkjttC0FheBtv+ExeG4VHjEJG3+zz7+I5YfHB6cXiIMIwu/OjI/etUnukPr6Fc5Mb0V5621cEtL/xTETOb5fTNLt991t7qxj2T06JVrfLjLw62J7l9dzeytm9bHVzJZEaGt63/g0dGiLetTofaQnA6P8/Xk5N/gsPpNM8NA1lRfieXo1ESpRJSMDg0LAWDJPf2kBWl91aMzM4yVSgMjU8VCoTT6f73+eXmJl/W1rAtyxcaiMd5ur7O41zO37D4ZpqYKys0y+W+8Hg2S6JU4tHkpP9J1OnPszOauk5T17F0HRyHmKYxrmnENI1wKuV9Bg85oH8CT8DJrJGjGicAAAAASUVORK5CYII= "redcircle 1")Minimum 1 GB hard disk space for the file system containing_**/usr/local/bin/**_.Minimum 1 GB hard disk space for the file system containing the system’s temporary directory.![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABcAAAAWCAYAAAArdgcFAAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAB3RJTUUH4QcFDi4QiBx65wAAAmhJREFUOMu11T9IG1EcwPFvoiYxF6nSWor4L8YSbZA77FIdQsZ2qrjUxaibTrUgdHU0U+ukgohFAmYyddGtGjBophOpiFVj/0BbtKCY00s1lw5tUqp3iaT44Kb33ud+7/d4v58pnU6nuaFRnHM2leJofh5lbY1TWeZUlsFkwi5Jv7/WVio6O6GoSHe7ySjy5N4e8e5ulGg05/+F9nacMzNYGxquzJn1NhxOTrIpinlhACUaZVMUOZyayh/5wfg4nwYGCspx7dgYlf39+nhyd5dNUURTlIJwsyDwYH0dq8t1KS2aRtzvvwpb3VS8mqP56xkP02eI8XfUPq3TxTVFId7TA5r2L67EYro5Lu4YoWawA4sqc7wok7rno3J2mjt1BnewsoISi13CV1d1F1+Eetnt8PHe2cbOEx+fw0dga0Kotxpf8h8riycMcDhGebvMBYC1CYdUDuoWylbSEE9cxhVDPDNu4RiZ5m6Tijo+zI/v5I08+0I1Vc0JCy8XcQ1KnId72XmxTK6akbGykdslyWCpldLnYRpHJFLhXj50vSGZ54wZKy9u6Znl/msfxeo3zm1d1IQXaFyYo/ZZXV48m5ZSXdyK5ZFECYCtHsfj+uyMKg9D6KMunrGyL1RTFLba2jjb2PivMmvzeGiOxTDb7X/TYhYEnMEgJoulYNhkseAKhTDb7VerYmlLC9WBQMF4dSCAzePJXc8PJib4MjSElkhcCy0qL6dmdJTbfv/1msXP/X32+/o4WVrKCZf5fDiDQUqqqq7fibJleHubk0iEk0iERCQC6TQOr5cyrxeH14vN7Ta+g5ts0L8Ax+z488wl6EkAAAAASUVORK5CYII= "redcircle 2")An additional minimum 15 GB unallocated space to be used for Docker’s storage back end; see[Configuring Docker Storage](https://docs.openshift.org/latest/install_config/install/host_preparation.html#configuring-docker-storage). |
| External etcd Nodes | Minimum 20 GB hard disk space for etcd data.Consult[Hardware Recommendations](https://github.com/coreos/etcd/blob/master/Documentation/op-guide/hardware.md#hardware-recommendations)to properly size your etcd nodes.Currently, OpenShift Origin stores image, build, and deployment metadata in etcd. You must periodically[prune old resources](https://docs.openshift.org/latest/admin_guide/pruning_resources.html#admin-guide-pruning-resources). If you are planning to leverage a large number of these resources, place etcd on machines with large amounts of memory and fast SSD drives. |

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABcAAAAWCAYAAAArdgcFAAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAB3RJTUUH4QcFDi0d3YBVmQAAAeFJREFUOMu91b9LG2Ecx/H3XWx+XCJEShexQsyQtkEu2EmHI1s7FncjTo27Q/+Dkq1ORhAXCehk8S8IBwZzU0QIVtAcpZuCQu6xpq13HUpSmtwl1zT24Kbnntd9+D58n6/kOI7DAz1jfVfv77k5OEBUq9zWatzWaiBJKJnMr3dujonFRQgEXLdLXslbFxc0lpYQlUrf/0cXFkjs7BCamelZk902XG1tUVfVgTCAqFSoqypX29uDk18Wi3xeXR2qxtMbGzzJ593x1vk5dVXFFmIoXI5GeXF8TCiZ7CqLbdPI5TzhsVfvSV07vLzeZyLkjttC0FheBtv+ExeG4VHjEJG3+zz7+I5YfHB6cXiIMIwu/OjI/etUnukPr6Fc5Mb0V5621cEtL/xTETOb5fTNLt991t7qxj2T06JVrfLjLw62J7l9dzeytm9bHVzJZEaGt63/g0dGiLetTofaQnA6P8/Xk5N/gsPpNM8NA1lRfieXo1ESpRJSMDg0LAWDJPf2kBWl91aMzM4yVSgMjU8VCoTT6f73+eXmJl/W1rAtyxcaiMd5ur7O41zO37D4ZpqYKys0y+W+8Hg2S6JU4tHkpP9J1OnPszOauk5T17F0HRyHmKYxrmnENI1wKuV9Bg85oH8CT8DJrJGjGicAAAAASUVORK5CYII= "redcircle 1")Meeting the_**/var/**_file system sizing requirements in RHEL Atomic Host requires making changes to the default configuration. See[Managing Storage in Red Hat Enterprise Linux Atomic Host](https://access.redhat.com/documentation/en/red-hat-enterprise-linux-atomic-host/version-7/getting-started-with-containers/#managing_storage_in_red_hat_enterprise_linux_atomic_host)for instructions on configuring this during or after installation.

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABcAAAAWCAYAAAArdgcFAAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAB3RJTUUH4QcFDi4QiBx65wAAAmhJREFUOMu11T9IG1EcwPFvoiYxF6nSWor4L8YSbZA77FIdQsZ2qrjUxaibTrUgdHU0U+ukgohFAmYyddGtGjBophOpiFVj/0BbtKCY00s1lw5tUqp3iaT44Kb33ud+7/d4v58pnU6nuaFRnHM2leJofh5lbY1TWeZUlsFkwi5Jv7/WVio6O6GoSHe7ySjy5N4e8e5ulGg05/+F9nacMzNYGxquzJn1NhxOTrIpinlhACUaZVMUOZyayh/5wfg4nwYGCspx7dgYlf39+nhyd5dNUURTlIJwsyDwYH0dq8t1KS2aRtzvvwpb3VS8mqP56xkP02eI8XfUPq3TxTVFId7TA5r2L67EYro5Lu4YoWawA4sqc7wok7rno3J2mjt1BnewsoISi13CV1d1F1+Eetnt8PHe2cbOEx+fw0dga0Kotxpf8h8riycMcDhGebvMBYC1CYdUDuoWylbSEE9cxhVDPDNu4RiZ5m6Tijo+zI/v5I08+0I1Vc0JCy8XcQ1KnId72XmxTK6akbGykdslyWCpldLnYRpHJFLhXj50vSGZ54wZKy9u6Znl/msfxeo3zm1d1IQXaFyYo/ZZXV48m5ZSXdyK5ZFECYCtHsfj+uyMKg9D6KMunrGyL1RTFLba2jjb2PivMmvzeGiOxTDb7X/TYhYEnMEgJoulYNhkseAKhTDb7VerYmlLC9WBQMF4dSCAzePJXc8PJib4MjSElkhcCy0qL6dmdJTbfv/1msXP/X32+/o4WVrKCZf5fDiDQUqqqq7fibJleHubk0iEk0iERCQC6TQOr5cyrxeH14vN7Ta+g5ts0L8Ax+z488wl6EkAAAAASUVORK5CYII= "redcircle 2")The system’s temporary directory is determined according to the rules defined in the[**`tempfile`**](https://docs.python.org/2/library/tempfile.html#tempfile.tempdir)module in Python’s standard library.

|  | OpenShift Origin only supports servers with the x86\_64 architecture. |
| :--- | :--- |


### Production Level Hardware Requirements {#production-level-hardware-requirements}

Test or sample environments function with the minimum requirements. For production environments, the following recommendations apply:

Master Hosts

In a highly available OpenShift Origin cluster with external etcd, a master host should have, in addition to the minimum requirements in the table above, 1 CPU core and 1.5 GB of memory for each 1000 pods. Therefore, the recommended size of a master host in an OpenShift Origin cluster of 2000 pods would be the minimum requirements of 2 CPU cores and 16 GB of RAM, plus 2 CPU cores and 3 GB of RAM, totaling 4 CPU cores and 19 GB of RAM.

When planning an environment with multiple masters, a minimum of three etcd hosts and a load-balancer between the master hosts are required.

The OpenShift Origin master caches deserialized versions of resources aggressively to ease CPU load. However, in smaller clusters of less than 1000 pods, this cache can waste a lot of memory for negligible CPU load reduction. The default cache size is 50,000 entries, which, depending on the size of your resources, can grow to occupy 1 to 2 GB of memory. This cache size can be reduced using the following setting the in_**/etc/origin/master/master-config.yaml**_:

```
kubernetesMasterConfig:
  apiServerArguments:
    deserialization-cache-size:
    - "1000"
```

Node Hosts

The size of a node host depends on the expected size of its workload. As an OpenShift Origin cluster administrator, you will need to calculate the expected workload, then add about 10 percent for overhead. For production environments, allocate enough resources so that a node host failure does not affect your maximum capacity.

|  | Oversubscribing the physical resources on a node affects resource guarantees the Kubernetes scheduler makes during pod placement. Learn what measures you can take to[avoid memory swapping](https://docs.openshift.org/latest/admin_guide/overcommit.html#disabling-swap-memory). |
| :--- | :--- |


### Configuring Core Usage {#configuring-core-usage}

By default, OpenShift Origin masters and nodes use all available cores in the system they run on. You can choose the number of cores you want OpenShift Origin to use by setting the[**`GOMAXPROCS`**environment variable](https://golang.org/pkg/runtime/).

For example, run the following before starting the server to make OpenShift Origin only run on one core:

```
# export GOMAXPROCS=1
```

Alternatively, if you plan to[run OpenShift in a container](https://docs.openshift.org/latest/getting_started/administrators.html#running-in-a-docker-container), add`-e GOMAXPROCS=1`to the`docker run`command when launching the server.

### SELinux {#prereq-selinux}

Security-Enhanced Linux \(SELinux\) must be enabled on all of the servers before installing OpenShift Origin or the installer will fail. Also, configure**`SELINUXTYPE=targeted`**in the_**/etc/selinux/config**_file:

```
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=enforcing
# SELINUXTYPE= can take one of these three values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted
```

### Using OverlayFS {#install-prerequisites-overlayfs}

OverlayFS is a union file system that allows you to overlay one file system on top of another.

As of Red Hat Enterprise Linux 7.4, you have the option to configure your OpenShift Origin environment to use OverlayFS. The`overlay2`graph driver is fully supported in addition to the older`overlay`driver. However, Red Hat recommends using`overlay2`instead of`overlay`, because of its speed and simple implementation.

See the[Overlay Graph Driver](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux_atomic_host/7/html-single/managing_containers/#overlay_graph_driver)section of the Atomic Host documentation for instructions on how to to enable the`overlay2`graph driver for the Docker service.

### NTP {#prereq-NTP}

You must enable Network Time Protocol \(NTP\) to prevent masters and nodes in the cluster from going out of sync. Set`openshift_clock_enabled`to`true`in the Ansible playbook to enable NTP on masters and nodes in the cluster during Ansible installation.

```
# openshift_clock_enabled=true
```

### Security Warning {#security-warning}

OpenShift Origin runs[containers](https://docs.openshift.org/latest/architecture/core_concepts/containers_and_images.html#containers)on your hosts, and in some cases, such as build operations and the registry service, it does so using privileged containers. Furthermore, those containers access your host’s Docker daemon and perform`docker build`and`docker push`operations. As such, you should be aware of the inherent security risks associated with performing`docker run`operations on arbitrary images as they effectively have root access.

For more information, see these articles:

* [http://opensource.com/business/14/7/docker-security-selinux](http://opensource.com/business/14/7/docker-security-selinux)

* [https://docs.docker.com/engine/security/security/](https://docs.docker.com/engine/security/security/)

To address these risks, OpenShift Origin uses[security context constraints](https://docs.openshift.org/latest/architecture/additional_concepts/authorization.html#security-context-constraints)that control the actions that pods can perform and what it has the ability to access.

## Environment Requirements {#envirornment-requirements}

The following section defines the requirements of the environment containing your OpenShift Origin configuration. This includes networking considerations and access to external services, such as Git repository access, storage, and cloud infrastructure providers.

### DNS {#prereq-dns}

OpenShift Origin requires a fully functional DNS server in the environment. This is ideally a separate host running DNS software and can provide name resolution to hosts and containers running on the platform.

|  | Adding entries into the_**/etc/hosts**_file on each host is not enough. This file is not copied into containers running on the platform. |
| :--- | :--- |


Key components of OpenShift Origin run themselves inside of containers and use the following process for name resolution:

1. By default, containers receive their DNS configuration file \(_**/etc/resolv.conf**_\) from their host.

2. OpenShift Origin then inserts one DNS value into the pods \(above the node’s nameserver values\). That value is defined in the_**/etc/origin/node/node-config.yaml**_file by the[**`dnsIP`**](https://docs.openshift.org/latest/admin_solutions/master_node_config.html#node-config-options)parameter, which by default is set to the address of the host node because the host is using**dnsmasq**.

3. If the[**`dnsIP`**](https://docs.openshift.org/latest/admin_solutions/master_node_config.html#node-config-options)parameter is omitted from the_**node-config.yaml**_file, then the value defaults to the kubernetes service IP, which is the first nameserver in the pod’s_**/etc/resolv.conf**_file.

As of OpenShift Origin 1.2,**dnsmasq**is automatically configured on all masters and nodes. The pods use the nodes as their DNS, and the nodes forward the requests. By default,**dnsmasq**is configured on the nodes to listen on port 53, therefore the nodes cannot run any other type of DNS application.

|  | **NetworkManager**is required on the nodes in order to populate**dnsmasq**with the DNS IP addresses.DNSMSQ must be enabled \(`openshift_use_dnsmasq=true`\) or the installation will fail and critical features will not function. |
| :--- | :--- |


The following is an example set of DNS records for the[Single Master and Multiple Nodes](https://docs.openshift.org/latest/install_config/install/planning.html#single-master-multi-node)scenario:

```
master    A   10.64.33.100
node1     A   10.64.33.101
node2     A   10.64.33.102
```

If you do not have a properly functioning DNS environment, you could experience failure with:

* Product installation via the reference Ansible-based scripts

* Deployment of the infrastructure containers \(registry, routers\)

* Access to the OpenShift Origin web console, because it is not accessible via IP address alone

#### CONFIGURING HOSTS TO USE DNS {#dns-config-prereq}

Make sure each host in your environment is configured to resolve hostnames from your DNS server. The configuration for hosts' DNS resolution depend on whether DHCP is enabled. If DHCP is:

* Disabled, then configure your network interface to be static, and add DNS nameservers to NetworkManager.

* Enabled, then the NetworkManager dispatch script automatically configures DNS based on the DHCP configuration. Optionally, you can add a value to[**`dnsIP`**](https://docs.openshift.org/latest/admin_solutions/master_node_config.html#node-config-options)in the_**node-config.yaml**_file to prepend the pod’s_**resolv.conf**_file. The second nameserver is then defined by the host’s first nameserver. By default, this will be the IP address of the node host.

  |  | For most configurations, do not set the**`openshift_dns_ip`**option during the advanced installation of OpenShift Origin \(using Ansible\), because this option overrides the default IP address set by[**`dnsIP`**](https://docs.openshift.org/latest/admin_solutions/master_node_config.html#node-config-options).Instead, allow the installer to configure each node to use**dnsmasq**and forward requests to SkyDNS or the external DNS provider. If you do set the**`openshift_dns_ip`**option, then it should be set either with a DNS IP that queries SkyDNS first, or to the SkyDNS service or endpoint IP \(the Kubernetes service IP\). |
  | :--- | :--- |

To verify that hosts can be resolved by your DNS server:

1. Check the contents of_**/etc/resolv.conf**_:

   ```
   $ cat /etc/resolv.conf
   # Generated by NetworkManager
   search example.com
   nameserver 10.64.33.1
   # nameserver updated by /etc/NetworkManager/dispatcher.d/99-origin-dns.sh
   ```

   In this example, 10.64.33.1 is the address of our DNS server.

2. Test that the DNS servers listed in_**/etc/resolv.conf**_are able to resolve host names to the IP addresses of all masters and nodes in your OpenShift Origin environment:

   ```
   $ dig 
   <
   node_hostname
   >
    @
   <
   IP_address
   >
    +short
   ```

   For example:

   ```
   $ dig master.example.com @10.64.33.1 +short
   10.64.33.100
   $ dig node1.example.com @10.64.33.1 +short
   10.64.33.101
   ```

#### CONFIGURING A DNS WILDCARD {#wildcard-dns-prereq}

Optionally, configure a wildcard for the router to use, so that you do not need to update your DNS configuration when new routes are added.

A wildcard for a DNS zone must ultimately resolve to the IP address of the OpenShift Origin[router](https://docs.openshift.org/latest/architecture/networking/routes.html#routers).

For example, create a wildcard DNS entry for**cloudapps**that has a low time-to-live value \(TTL\) and points to the public IP address of the host where the router will be deployed:

```
*.cloudapps.example.com. 300 IN  A 192.168.133.2
```

In almost all cases, when referencing VMs you must use host names, and the host names that you use must match the output of the`hostname -f`command on each node.

|  | In your_**/etc/resolv.conf**_file on each node host, ensure that the DNS server that has the wildcard entry is not listed as a nameserver or that the wildcard domain is not listed in the search list. Otherwise, containers managed by OpenShift Origin may fail to resolve host names properly. |
| :--- | :--- |


### Network Access {#prereq-network-access}

A shared network must exist between the master and node hosts. If you plan to configure[multiple masters for high-availability](https://docs.openshift.org/latest/architecture/infrastructure_components/kubernetes_infrastructure.html#high-availability-masters)using the[advanced installation method](https://docs.openshift.org/latest/install_config/install/advanced_install.html#install-config-install-advanced-install), you must also select an IP to be configured as your[virtual IP](https://docs.openshift.org/latest/architecture/infrastructure_components/kubernetes_infrastructure.html#master-components)\(VIP\) during the installation process. The IP that you select must be routable between all of your nodes, and if you configure using a FQDN it should resolve on all nodes.

#### NETWORKMANAGER {#prereq-networkmanager}

NetworkManager, a program for providing detection and configuration for systems to automatically connect to the network, is required.

#### REQUIRED PORTS {#required-ports}

The OpenShift Origin installation automatically creates a set of internal firewall rules on each host using`iptables`. However, if your network configuration uses an external firewall, such as a hardware-based firewall, you must ensure infrastructure components can communicate with each other through specific ports that act as communication endpoints for certain processes or services.

Ensure the following ports required by OpenShift Origin are open on your network and configured to allow access between hosts. Some ports are optional depending on your configuration and usage.

|  |  |  |
| :--- | :--- | :--- |
| **4789** | UDP | Required for SDN communication between pods on separate hosts. |

|  |  |  |
| :--- | :--- | :--- |
| **53**or**8053** | TCP/UDP | Required for DNS resolution of cluster services \(SkyDNS\). Installations prior to 1.2 or environments upgraded to 1.2 use port 53. New installations will use 8053 by default so that**dnsmasq**may be configured. |
| **4789** | UDP | Required for SDN communication between pods on separate hosts. |
| **443**or**8443** | TCP | Required for node hosts to communicate to the master API, for the node hosts to post back status, to receive tasks, and so on. |

|  |  |  |
| :--- | :--- | :--- |
| **4789** | UDP | Required for SDN communication between pods on separate hosts. |
| **10250** | TCP | The master proxies to node hosts via the Kubelet for`oc`commands. |

|  | In the following table,**\(L\)**indicates the marked port is also used in_loopback mode_, enabling the master to communicate with itself.In a single-master cluster:Ports marked with**\(L\)**must be open.Ports not marked with**\(L\)**need not be open.In a multiple-master cluster, all the listed ports must be open. |
| :--- | :--- |


|  |  |  |
| :--- | :--- | :--- |
| **53 \(L\)**or**8053 \(L\)** | TCP/UDP | Required for DNS resolution of cluster services \(SkyDNS\). Installations prior to 1.2 or environments upgraded to 1.2 use port 53. New installations will use 8053 by default so that**dnsmasq**may be configured. |
| **2049 \(L\)** | TCP/UDP | Required when provisioning an NFS host as part of the installer. |
| **2379** | TCP | Used for standalone etcd \(clustered\) to accept changes in state. |
| **2380** | TCP | etcd requires this port be open between masters for leader election and peering connections when using standalone etcd \(clustered\). |
| **4001 \(L\)** | TCP | Used for embedded etcd \(non-clustered\) to accept changes in state. |
| **4789 \(L\)** | UDP | Required for SDN communication between pods on separate hosts. |

|  |  |  |
| :--- | :--- | :--- |
| **9000** | TCP | If you choose the**`native`**HA method, optional to allow access to the HAProxy statistics page. |

|  |  |  |
| :--- | :--- | :--- |
| **443**or**8443** | TCP | Required for node hosts to communicate to the master API, for node hosts to post back status, to receive tasks, and so on. |

|  |  |  |
| :--- | :--- | :--- |
| **22** | TCP | Required for SSH by the installer or system administrator. |
| **53**or**8053** | TCP/UDP | Required for DNS resolution of cluster services \(SkyDNS\). Installations prior to 1.2 or environments upgraded to 1.2 use port 53. New installations will use 8053 by default so that**dnsmasq**may be configured. Only required to be internally open on master hosts. |
| **80**or**443** | TCP | For HTTP/HTTPS use for the router. Required to be externally open on node hosts, especially on nodes running the router. |
| **1936** | TCP | \(**Optional**\) Required to be open when running the template router to access statistics. Can be open externally or internally to connections depending on if you want the statistics to be expressed publicly. Can require extra configuration to open. See the Notes section below for more information. |
| **4001** | TCP | For embedded etcd \(non-clustered\) use. Only required to be internally open on the master host.**4001**is for server-client connections. |
| **2379**and**2380** | TCP | For standalone etcd use. Only required to be internally open on the master host.**2379**is for server-client connections.**2380**is for server-server connections, and is only required if you have clustered etcd. |
| **4789** | UDP | For VxLAN use \(OpenShift SDN\). Required only internally on node hosts. |
| **8443** | TCP | For use by the OpenShift Origin web console, shared with the API server. |
| **10250** | TCP | For use by the Kubelet. Required to be externally open on nodes. |

**Notes**

* In the above examples, port**4789**is used for User Datagram Protocol \(UDP\).

* When deployments are using the SDN, the pod network is accessed via a service proxy, unless it is accessing the registry from the same node the registry is deployed on.

* OpenShift Origin internal DNS cannot be received over SDN. Depending on the detected values of**`openshift_facts`**, or if the**`openshift_ip`**and**`openshift_public_ip`**values are overridden, it will be the computed value of**`openshift_ip`**. For non-cloud deployments, this will default to the IP address associated with the default route on the master host. For cloud deployments, it will default to the IP address associated with the first internal interface as defined by the cloud metadata.

* The master host uses port**10250**to reach the nodes and does not go over SDN. It depends on the target host of the deployment and uses the computed values of**`openshift_hostname`**and**`openshift_public_hostname`**.

* Port**1936**can still be inaccessible due to your iptables rules. Use the following to configure iptables to open port**1936**:

  ```
  # iptables OS_FIREWALL_ALLOW -p tcp -m state --state NEW -m tcp \
      --dport 1936 -j ACCEPT
  ```

|  |  |  |
| :--- | :--- | :--- |
| **9200** | TCP | For Elasticsearch API use. Required to be internally open on any infrastructure nodes so Kibana is able to retrieve logs for display. It can be externally opened for direct access to Elasticsearch by means of a route. The route can be created using`oc expose`. |
| **9300** | TCP | For Elasticsearch inter-cluster use. Required to be internally open on any infrastructure node so the members of the Elasticsearch cluster may communicate with each other. |

### Persistent Storage {#prereq-persistent-storage}

The Kubernetes[persistent volume](https://docs.openshift.org/latest/architecture/additional_concepts/storage.html#architecture-additional-concepts-storage)framework allows you to provision an OpenShift Origin cluster with persistent storage using networked storage available in your environment. This can be done after completing the initial OpenShift Origin installation depending on your application needs, giving users a way to request those resources without having any knowledge of the underlying infrastructure.

The[Installation and Configuration Guide](https://docs.openshift.org/latest/install_config/index.html#install-config-index)provides instructions for cluster administrators on provisioning an OpenShift Origin cluster with persistent storage using[NFS](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_nfs.html#install-config-persistent-storage-persistent-storage-nfs),[GlusterFS](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_glusterfs.html#install-config-persistent-storage-persistent-storage-glusterfs),[Ceph RBD](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_ceph_rbd.html#install-config-persistent-storage-persistent-storage-ceph-rbd),[OpenStack Cinder](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_cinder.html#install-config-persistent-storage-persistent-storage-cinder),[AWS Elastic Block Store \(EBS\)](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_aws.html#install-config-persistent-storage-persistent-storage-aws),[GCE Persistent Disks](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_gce.html#install-config-persistent-storage-persistent-storage-gce), and[iSCSI](https://docs.openshift.org/latest/install_config/persistent_storage/persistent_storage_iscsi.html#install-config-persistent-storage-persistent-storage-iscsi).

### Cloud Provider Considerations {#prereq-cloud-provider-considerations}

There are certain aspects to take into consideration if installing OpenShift Origin on a cloud provider.

#### CONFIGURING A SECURITY GROUP {#configuring-a-security-group}

When installing on AWS or OpenStack, ensure that you set up the appropriate security groups. These are some ports that you should have in your security groups, without which the installation will fail. You may need more depending on the cluster configuration you want to install. For more information and to adjust your security groups accordingly, see[Required Ports](https://docs.openshift.org/latest/install_config/install/prerequisites.html#required-ports)for more information.

| **All OpenShift Origin Hosts** | tcp/22 from host running the installer/Ansible |
| :--- | :--- |
| **etcd Security Group** | tcp/2379 from masterstcp/2380 from etcd hosts |
| **Master Security Group** | tcp/8443 from 0.0.0.0/0tcp/53 from all OpenShift Origin hosts for environments installed prior to or upgraded to 1.2udp/53 from all OpenShift Origin hosts for environments installed prior to or upgraded to 1.2tcp/8053 from all OpenShift Origin hosts for new environments installed with 1.2udp/8053 from all OpenShift Origin hosts for new environments installed with 1.2 |
| **Node Security Group** | tcp/10250 from mastersudp/4789 from nodes |
| **Infrastructure Nodes**\(ones that can host the OpenShift Origin router\) | tcp/443 from 0.0.0.0/0tcp/80 from 0.0.0.0/0 |

If configuring ELBs for load balancing the masters and/or routers, you also need to configure Ingress and Egress security groups for the ELBs appropriately.

#### OVERRIDING DETECTED IP ADDRESSES AND HOST NAMES {#overriding-detected-ip-addresses-host-names}

Some deployments require that the user override the detected host names and IP addresses for the hosts. To see the default values, run the**`openshift_facts`**playbook:

```
# ansible-playbook  [-i /path/to/inventory] \
    ~/openshift-ansible/roles/openshift_facts/library/openshift_facts.py
```

Now, verify the detected common settings. If they are not what you expect them to be, you can override them.

The[Advanced Installation](https://docs.openshift.org/latest/install_config/install/advanced_install.html#configuring-ansible)topic discusses the available Ansible variables in greater detail.

| Variable | Usage |
| :--- | :--- |
| **`hostname`** | Should resolve to the internal IP from the instances themselves.**`openshift_hostname`**overrides. |
| **`ip`** | Should be the internal IP of the instance.**`openshift_ip`**will overrides. |
| **`public_hostname`** | Should resolve to the external IP from hosts outside of the cloud.Provider**`openshift_public_hostname`**overrides. |
| **`public_ip`** | Should be the externally accessible IP associated with the instance.**`openshift_public_ip`**overrides. |
| **`use_openshift_sdn`** | Should be true unless the cloud is GCE.**`openshift_use_openshift_sdn`**overrides. |

|  | If**`openshift_hostname`**is set to a value other than the metadata-provided**`private-dns-name`**value, the native cloud integration for those providers will no longer work. |
| :--- | :--- |


In AWS, situations that require overriding the variables include:

| Variable | Usage |
| :--- | :--- |
| **`hostname`** | The user is installing in a VPC that is not configured for both**`DNS hostnames`**and**`DNS resolution`**. |
| **`ip`** | Possibly if they have multiple network interfaces configured and they want to use one other than the default. You must first set**`openshift_set_node_ip`**to`True`. Otherwise, the SDN would attempt to use the**`hostname`**setting or try to resolve the host name for the IP. |
| **`public_hostname`** | A master instance where the VPC subnet is not configured for**`Auto-assign Public IP`**. For external access to this master, you need to have an ELB or other load balancer configured that would provide the external access needed, or you need to connect over a VPN connection to the internal name of the host.A master instance where metadata is disabled.This value is not actually used by the nodes. |
| **`public_ip`** | A master instance where the VPC subnet is not configured for**`Auto-assign Public IP`**.A master instance where metadata is disabled.This value is not actually used by the nodes. |

If setting**`openshift_hostname`**to something other than the metadata-provided**`private-dns-name`**value, the native cloud integration for those providers will no longer work.

For EC2 hosts in particular, they must be deployed in a VPC that has both**`DNS host names`**and**`DNS resolution`**enabled, and**`openshift_hostname`**should not be overridden.

#### POST-INSTALLATION CONFIGURATION FOR CLOUD PROVIDERS {#post-installation-configuration-for-cloud-providers}

Following the installation process, you can configure OpenShift Origin for[AWS](https://docs.openshift.org/latest/install_config/configuring_aws.html#install-config-configuring-aws),[OpenStack](https://docs.openshift.org/latest/install_config/configuring_openstack.html#install-config-configuring-openstack), or[GCE](https://docs.openshift.org/latest/install_config/configuring_gce.html#install-config-configuring-gce).

### Containerized GlusterFS Considerations {#prereq-containerized-glusterfs-considerations}

If you choose to configure[containerized GlusterFS persistent storage](https://docs.openshift.org/latest/install_config/install/advanced_install.html#advanced-install-containerized-glusterfs-persistent-storage)for your cluster, or if you choose to configure a[containerized GlusterFS-backed OpenShift Container Registry](https://docs.openshift.org/latest/install_config/install/advanced_install.html#advanced-install-containerized-glusterfs-backed-registry), you must consider the following prerequisites.

#### STORAGE NODES {#prereq-glusterfs-storage-nodes}

To use containerized GlusterFS persistent storage:

* A minimum of 3 storage nodes is required.

* Each storage node must have at least 1 raw block device with least 100 GB available.

To run a containerized GlusterFS-backed OpenShift Container Registry:

* A minimum of 3 storage nodes is required.

* Each storage node must have at least 1 raw block device with at least 10 GB of free storage.

|  | While containerized GlusterFS persistent storage can be configured and deployed on the same OpenShift Origin cluster as a containerized GlusterFS-backed registry, their storage should be kept separate from each other and also requires additional storage nodes. For example, if both are configured, a total of 6 storage nodes would be needed: 3 for the registry and 3 for persistent storage. This limitation is imposed to avoid potential impacts on performance in I/O and volume creation. |
| :--- | :--- |


#### REQUIRED SOFTWARE COMPONENTS {#prereq-glusterfs-software-components}

The`mount.glusterfs`command must be available on all nodes that will host pods that will use GlusterFS volumes. For RPM-based systems, the**glusterfs-fuse**package must be installed:

```
# yum install glusterfs-fuse
```

If GlusterFS is already installed on the nodes, ensure the latest version is installed:

```
# yum update glusterfs-fuse
```



