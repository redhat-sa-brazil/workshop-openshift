# Host Preparation

* [Installing Base Packages](https://docs.openshift.org/latest/install_config/install/host_preparation.html#installing-base-packages)
* [Preparing for Advanced Installations](https://docs.openshift.org/latest/install_config/install/host_preparation.html#preparing-for-advanced-installations-origin)
* [Installing Docker](https://docs.openshift.org/latest/install_config/install/host_preparation.html#installing-docker)
* [Configuring Docker Storage](https://docs.openshift.org/latest/install_config/install/host_preparation.html#configuring-docker-storage)
  * [Reconfiguring Docker Storage](https://docs.openshift.org/latest/install_config/install/host_preparation.html#reconfiguring-docker-storage)
  * [Enabling Image Signature Support](https://docs.openshift.org/latest/install_config/install/host_preparation.html#enabling-image-signature-support)
  * [Managing Container Logs](https://docs.openshift.org/latest/install_config/install/host_preparation.html#managing-docker-container-logs)
  * [Viewing Available Container Logs](https://docs.openshift.org/latest/install_config/install/host_preparation.html#viewing-available-container-logs)
* [Ensuring Host Access](https://docs.openshift.org/latest/install_config/install/host_preparation.html#ensuring-host-access)
* [What’s Next?](https://docs.openshift.org/latest/install_config/install/host_preparation.html#what-s-next)

## Installing Base Packages {#installing-base-packages}

For RHEL 7 systems:

1. Install the following base packages:

   ```
   # yum install wget git net-tools bind-utils iptables-services bridge-utils bash-completion kexec-tools sos psacct
   ```

2. Update the system to the latest packages:

   ```
   # yum update
   ```

For RHEL Atomic Host 7 systems:

1. Ensure the host is up to date by upgrading to the latest Atomic tree if one is available:

   ```
   # atomic host upgrade
   ```

2. After the upgrade is completed and prepared for the next boot, reboot the host:

   ```
   # systemctl reboot
   ```

## Preparing for Advanced Installations {#preparing-for-advanced-installations-origin}

If you plan to use the[containerized installer](https://docs.openshift.org/latest/install_config/install/advanced_install.html#running-the-advanced-installation-system-container)to run an advanced installation \(currently a Technology Preview feature\):

1. Install the**atomic**package:

   ```
   # yum install atomic
   ```

2. Skip to[Installing Docker](https://docs.openshift.org/latest/install_config/install/host_preparation.html#installing-docker).

If you plan to use the[RPM-based installer](https://docs.openshift.org/latest/install_config/install/advanced_install.html#running-the-advanced-installation-rpm)to run an advanced installation:

1. Install Ansible. For convenience, the following steps are provided if you want to use EPEL as a package source for Ansible:

   1. Install the EPEL repository:

      ```
      # yum -y install \
          https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
      ```

   2. Disable the EPEL repository globally so that it is not accidentally used during later steps of the installation:

      ```
      # sed -i -e "s/^enabled=1/enabled=0/" /etc/yum.repos.d/epel.repo
      ```

   3. Install the packages for Ansible:

      ```
      # yum -y --enablerepo=epel install ansible pyOpenSSL
      ```

2. Clone the**openshift/openshift-ansible**repository from GitHub, which provides the required playbooks and configuration files:

   ```
   # cd ~
   # git clone https://github.com/openshift/openshift-ansible
   # cd openshift-ansible
   ```

   |  | Be sure to stay on the**master**branch of the**openshift-ansible**repository when running an advanced installation. |
   | :--- | :--- |

## Installing Docker {#installing-docker}

At this point, you should install Docker on all master and node hosts. This allows you to configure your[Docker storage options](https://docs.openshift.org/latest/install_config/install/host_preparation.html#configuring-docker-storage)before installing OpenShift Origin.

For RHEL 7 systems, install Docker 1.12:

|  | On RHEL Atomic Host 7 systems, Docker should already be installed, configured, and running by default. |
| :--- | :--- |


```
# yum install docker-1.12.6
```

After the package installation is complete, verify that version 1.12 was installed:

```
# rpm -V docker-1.12.6
# docker version
```

|  | The[Advanced Installation](https://docs.openshift.org/latest/install_config/install/advanced_install.html#install-config-install-advanced-install)method automatically changes_**/etc/sysconfig/docker**_. |
| :--- | :--- |


The`--insecure-registry`option instructs the Docker daemon to trust any Docker registry on the indicated subnet, rather than[requiring a certificate](https://docs.openshift.org/latest/install_config/registry/securing_and_exposing_registry.html#securing-the-registry).

|  | 172.30.0.0/16 is the default value of the**`servicesSubnet`**variable in the_**master-config.yaml**_file. If this has changed, then the`--insecure-registry`value in the above step should be adjusted to match, as it is indicating the subnet for the registry to use. Note that the**`openshift_master_portal_net`**variable can be set in the Ansible inventory file and used during the[advanced installation](https://docs.openshift.org/latest/install_config/install/advanced_install.html#configuring-ansible)method to modify the**`servicesSubnet`**variable. |
| :--- | :--- |


|  | After the initial OpenShift Origin installation is complete, you can choose to[secure the integrated Docker registry](https://docs.openshift.org/latest/install_config/registry/securing_and_exposing_registry.html#securing-the-registry), which involves adjusting the`--insecure-registry`option accordingly. |
| :--- | :--- |


## Configuring Docker Storage {#configuring-docker-storage}

Containers and the images they are created from are stored in Docker’s storage back end. This storage is ephemeral and separate from any[persistent storage](https://docs.openshift.org/latest/dev_guide/persistent_volumes.html#dev-guide-persistent-volumes)allocated to meet the needs of your applications.

For RHEL Atomic Host

The default storage back end for Docker on RHEL Atomic Host is a thin pool logical volume, which is supported for production environments. You must ensure that enough space is allocated for this volume per the Docker storage requirements mentioned in[System Requirements](https://docs.openshift.org/latest/install_config/install/prerequisites.html#system-requirements).

If you do not have enough allocated, see[Managing Storage with Docker Formatted Containers](https://access.redhat.com/documentation/en/red-hat-enterprise-linux-atomic-host/version-7/getting-started-with-containers/#managing_storage_with_docker_formatted_containers)for details on using**docker-storage-setup**and basic instructions on storage management in RHEL Atomic Host.

For RHEL

The default storage back end for Docker on RHEL 7 is a thin pool on loopback devices, which is not supported for production use and only appropriate for proof of concept environments. For production environments, you must create a thin pool logical volume and re-configure Docker to use that volume.

You can use the**docker-storage-setup**script included with Docker to create a thin pool device and configure Docker’s storage driver. This can be done after installing Docker and should be done before creating images or containers. The script reads configuration options from the_**/etc/sysconfig/docker-storage-setup**_file and supports three options for creating the logical volume:

* **Option A\)**Use an additional block device.

* **Option B\)**Use an existing, specified volume group.

* **Option C\)**Use the remaining free space from the volume group where your root file system is located.

Option A is the most robust option, however it requires adding an additional block device to your host before configuring Docker storage. Options B and C both require leaving free space available when provisioning your host. Option C is known to cause issues with some applications, for example Red Hat Mobile Application Platform \(RHMAP\).

1. Create the**docker-pool**volume using one of the following three options:

   * **Option A\)**Use an additional block device.

     In_**/etc/sysconfig/docker-storage-setup**_, set**DEVS**to the path of the block device you wish to use. Set**VG**to the volume group name you wish to create;**docker-vg**is a reasonable choice. For example:

     ```
     # cat 
     <
     <
     EOF 
     >
      /etc/sysconfig/docker-storage-setup
     DEVS=/dev/vdc
     VG=docker-vg
     EOF
     ```

     Then run**docker-storage-setup**and review the output to ensure the**docker-pool**volume was created:

     ```
     # docker-storage-setup                                                                                                                                                                                                                                [5/1868]
     0
     Checking that no-one is using this disk right now ...
     OK

     Disk /dev/vdc: 31207 cylinders, 16 heads, 63 sectors/track
     sfdisk:  /dev/vdc: unrecognized partition table type

     Old situation:
     sfdisk: No partitions found

     New situation:
     Units: sectors of 512 bytes, counting from 0

        Device Boot    Start       End   #sectors  Id  System
     /dev/vdc1          2048  31457279   31455232  8e  Linux LVM
     /dev/vdc2             0         -          0   0  Empty
     /dev/vdc3             0         -          0   0  Empty
     /dev/vdc4             0         -          0   0  Empty
     Warning: partition 1 does not start at a cylinder boundary
     Warning: partition 1 does not end at a cylinder boundary
     Warning: no primary partition is marked bootable (active)
     This does not matter for LILO, but the DOS MBR will not boot this disk.
     Successfully wrote the new partition table

     Re-reading the partition table ...

     If you created or changed a DOS partition, /dev/foo7, say, then use dd(1)
     to zero the first 512 bytes:  dd if=/dev/zero of=/dev/foo7 bs=512 count=1
     (See fdisk(8).)
       Physical volume "/dev/vdc1" successfully created
       Volume group "docker-vg" successfully created
       Rounding up size to full physical extent 16.00 MiB
       Logical volume "docker-poolmeta" created.
       Logical volume "docker-pool" created.
       WARNING: Converting logical volume docker-vg/docker-pool and docker-vg/docker-poolmeta to pool's data and metadata volumes.
       THIS WILL DESTROY CONTENT OF LOGICAL VOLUME (filesystem etc.)
       Converted docker-vg/docker-pool to thin pool.
       Logical volume "docker-pool" changed.
     ```

   * **Option B\)**Use an existing, specified volume group.

     In_**/etc/sysconfig/docker-storage-setup**_, set**VG**to the desired volume group. For example:

     ```
     # cat 
     <
     <
     EOF 
     >
      /etc/sysconfig/docker-storage-setup
     VG=docker-vg
     EOF
     ```

     Then run**docker-storage-setup**and review the output to ensure the**docker-pool**volume was created:

     ```
     # docker-storage-setup
       Rounding up size to full physical extent 16.00 MiB
       Logical volume "docker-poolmeta" created.
       Logical volume "docker-pool" created.
       WARNING: Converting logical volume docker-vg/docker-pool and docker-vg/docker-poolmeta to pool's data and metadata volumes.
       THIS WILL DESTROY CONTENT OF LOGICAL VOLUME (filesystem etc.)
       Converted docker-vg/docker-pool to thin pool.
       Logical volume "docker-pool" changed.
     ```

   * **Option C\)**Use the remaining free space from the volume group where your root file system is located.

     Verify that the volume group where your root file system resides has the desired free space, then run**docker-storage-setup**and review the output to ensure the**docker-pool**volume was created:

     ```
     # docker-storage-setup
       Rounding up size to full physical extent 32.00 MiB
       Logical volume "docker-poolmeta" created.
       Logical volume "docker-pool" created.
       WARNING: Converting logical volume rhel/docker-pool and rhel/docker-poolmeta to pool's data and metadata volumes.
       THIS WILL DESTROY CONTENT OF LOGICAL VOLUME (filesystem etc.)
       Converted rhel/docker-pool to thin pool.
       Logical volume "docker-pool" changed.
     ```

2. Verify your configuration. You should have a**dm.thinpooldev**value in the_**/etc/sysconfig/docker-storage**_file and a**docker-pool**logical volume:

   ```
   # cat /etc/sysconfig/docker-storage
   DOCKER_STORAGE_OPTIONS=--storage-opt dm.fs=xfs --storage-opt
   dm.thinpooldev=/dev/mapper/docker--vg-docker--pool

   # lvs
     LV          VG   Attr       LSize  Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
     docker-pool rhel twi-a-t---  9.29g             0.00   0.12
   ```

   |  | Before using Docker or OpenShift Origin, verify that the**docker-pool**logical volume is large enough to meet your needs. The**docker-pool**volume should be 60% of the available volume group and will grow to fill the volume group via LVM monitoring. |
   | :--- | :--- |

3. Check if Docker is running:

   ```
   # systemctl is-active docker
   ```

4. If Docker has not yet been started on the host, enable and start the service:

   ```
   # systemctl enable docker
   # systemctl start docker
   ```

   If Docker is already running, re-initialize Docker:

   |  | This will destroy any containers or images currently on the host. |
   | :--- | :--- |


   ```
   # systemctl stop docker
   # rm -rf /var/lib/docker/*
   # systemctl restart docker
   ```

   If there is any content in_**/var/lib/docker/**_, it must be deleted. Files will be present if Docker has been used prior to the installation of OpenShift Origin.

### Reconfiguring Docker Storage {#reconfiguring-docker-storage}

Should you need to reconfigure Docker storage after having created the**docker-pool**, you should first remove the**docker-pool**logical volume. If you are using a dedicated volume group, you should also remove the volume group and any associated physical volumes before reconfiguring**docker-storage-setup**according to the instructions above.

See[Logical Volume Manager Administration](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Logical_Volume_Manager_Administration/index.html)for more detailed information on LVM management.

### Enabling Image Signature Support {#enabling-image-signature-support}

OpenShift Origin is capable of cryptographically verifying images are from trusted sources. The[Container Security Guide](https://docs.openshift.org/latest/security/deployment.html#security-deployment-from-where-images-deployed)provides a high-level description of how image signing works.

You can configure image signature verification using the`atomic`command line interface \(CLI\), version 1.12.5 or greater.

Install the**atomic**package if it is not installed on the host system:

```
$ yum install atomic
```

The**atomic trust**sub-command manages trust configuration. The default configuration is to whitelist all registries. This means no signature verification is configured.

```
$ atomic trust show
* (default)                         accept
```

A reasonable configuration might be to whitelist a particular registry or namespace, blacklist \(reject\) untrusted registries, and require signature verification on a vendor registry. The following set of commands performs this example configuration:

Example Atomic Trust Configuration

```
$ atomic trust add --type insecureAcceptAnything 172.30.1.1:5000

$ atomic trust add --sigstoretype atomic \
  --pubkeys pub@example.com \
  172.30.1.1:5000/production

$ atomic trust add --sigstoretype atomic \
  --pubkeys /etc/pki/example.com.pub \
  172.30.1.1:5000/production

$ atomic trust add --sigstoretype web \
  --sigstore https://access.redhat.com/webassets/docker/content/sigstore \
  --pubkeys /etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release \
  registry.access.redhat.com

$ sudo atomic trust show
* (default)                         accept
172.30.1.1:5000                     accept
172.30.1.1:5000/production          signed security@example.com
registry.access.redhat.com          signed security@redhat.com,security@redhat.com
```

When all the signed sources are verified, nodes may be further hardened with a global`reject`default:

```
$ atomic trust default reject

$ atomic trust show
* (default)                         reject
172.30.1.1:5000                     accept
172.30.1.1:5000/production          signed security@example.com
registry.access.redhat.com          signed security@redhat.com,security@redhat.com
```

Use the`atomic`man page`man atomic-trust`for additional examples.

The following files and directories comprise the trust configuration of a host:

* _**/etc/containers/registries.d/\***_

* _**/etc/containers/policy.json**_

The trust configuration may be managed directly on each node or the generated files managed on a separate host and distributed to the appropriate nodes using Ansible, for example. See this[Red Hat Knowledgebase Article](https://access.redhat.com/articles/2750891#automating-cluster-configuration)for an example of automating file distribution with Ansible.

### Managing Container Logs {#managing-docker-container-logs}

Sometimes a container’s log file \(the_**/var/lib/docker/containers/&lt;hash&gt;/&lt;hash&gt;-json.log**_file on the node where the container is running\) can increase to a problematic size. You can manage this by configuring Docker’s`json-file`logging driver to restrict the size and number of log files.

|  | Aggregated logging is only supported using the`journald`driver in Docker. See[Updating Fluentd’s Log Source After a Docker Log Driver Update](https://docs.openshift.org/latest/install_config/aggregate_logging.html#fluentd-upgrade-source)for more information. |
| :--- | :--- |


| Option | Purpose |
| :--- | :--- |
| `--log-opt max-size` | Sets the size at which a new log file is created. |
| `--log-opt max-file` | Sets the file on each host to configure the options. |

For example, to set the maximum file size to 1MB and always keep the last three log files, edit the_**/etc/sysconfig/docker**_file to configure`max-size=1M`and`max-file=3`:

```
OPTIONS='--insecure-registry=172.30.0.0/16 --selinux-enabled --log-opt max-size=1M --log-opt max-file=3'
```

Next, restart the Docker service:

```
# systemctl restart docker
```

### Viewing Available Container Logs {#viewing-available-container-logs}

Container logs are stored in the_**/var/lib/docker/containers/&lt;hash&gt;/**_directory on the node where the container is running. For example:

```
# ls -lh /var/lib/docker/containers/f088349cceac173305d3e2c2e4790051799efe363842fdab5732f51f5b001fd8/
total 2.6M
-rw-r--r--. 1 root root 5.6K Nov 24 00:12 config.json
-rw-r--r--. 1 root root 649K Nov 24 00:15 f088349cceac173305d3e2c2e4790051799efe363842fdab5732f51f5b001fd8-json.log
-rw-r--r--. 1 root root 977K Nov 24 00:15 f088349cceac173305d3e2c2e4790051799efe363842fdab5732f51f5b001fd8-json.log.1
-rw-r--r--. 1 root root 977K Nov 24 00:15 f088349cceac173305d3e2c2e4790051799efe363842fdab5732f51f5b001fd8-json.log.2
-rw-r--r--. 1 root root 1.3K Nov 24 00:12 hostconfig.json
drwx------. 2 root root    6 Nov 24 00:12 secrets
```

See Docker’s documentation for additional information on how to[Configure Logging Drivers](https://docs.docker.com/engine/admin/logging/overview/#/options).

## Ensuring Host Access {#ensuring-host-access}

The[advanced installation](https://docs.openshift.org/latest/install_config/install/advanced_install.html#install-config-install-advanced-install)method requires a user that has access to all hosts. If you want to run the installer as a non-root user, passwordless**sudo**rights must be configured on each destination host.

For example, you can generate an SSH key on the host where you will invoke the installation process:

```
# ssh-keygen
```

Do**not**use a password.

An easy way to distribute your SSH keys is by using a`bash`loop:

```
# for host in master.example.com \
    node1.example.com \
    node2.example.com; \
    do ssh-copy-id -i ~/.ssh/id_rsa.pub $host; \
    done
```

Modify the host names in the above command according to your configuration.

## What’s Next? {#what-s-next}

If you are interested in installing OpenShift Origin using the containerized method \(optional for Fedora, CentOS, or RHEL but required for RHEL Atomic Host\), see[Installing on Containerized Hosts](https://docs.openshift.org/latest/install_config/install/rpm_vs_containerized.html#install-config-install-rpm-vs-containerized)to prepare your hosts.

If you came here from[Getting Started for Administrators](https://docs.openshift.org/latest/getting_started/administrators.html#getting-started-administrators), you can now continue there by choosing an[installation method](https://docs.openshift.org/latest/getting_started/administrators.html#installation-methods). Alternatively, you can install OpenShift Origin using the[advanced installation](https://docs.openshift.org/latest/install_config/install/advanced_install.html#install-config-install-advanced-install)method.

If you are installing a stand-alone registry, continue with[Installing a Stand-alone Registry](https://docs.openshift.org/latest/install_config/install/stand_alone_registry.html#registry-installation-methods).

