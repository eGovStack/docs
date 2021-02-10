# VSphere

## Overview <a id="vsphere"></a>

The Kubernetes vSphere driver contains bugs related to detaching volumes from offline nodes. See the [**Volume detach bug**](vsphere.md#volume-detach-bug) section for more details.

## VM Images

When creating worker nodes for a user cluster, the user can specify an existing image. Defaults may be set in the [datacenters.yaml](https://docs.kubermatic.io/installation/install_kubermatic/#defining-the-datacenters).

Supported operating systems

* Ubuntu 18.04 [ova](https://cloud-images.ubuntu.com/releases/18.04/release/ubuntu-18.04-server-cloudimg-amd64.ova)
* CoreOS [ova](https://stable.release.core-os.net/amd64-usr/current/coreos_production_vmware_ova.ova)
* CentOS 7 [qcow2](https://cloud.centos.org/centos/7/images/CentOS-7-x86_64-GenericCloud.qcow2)

## **Importing the OVA**

1. Go into the VSphere WebUI, select your data centre, right-click onto it and choose “Deploy OVF Template”
2. Fill in the “URL” field with the appropriate URL
3. Click through the dialogue until “Select storage”
4. Select the same storage you want to use for your machines
5. Select the same network you want to use for your machines
6. Leave everything in the “Customize Template” and “Ready to complete” dialogue as it is
7. Wait until the VM got fully imported and the “Snapshots” =&gt; “Create Snapshot” button is not greyed out anymore.
8. The template VM must have the disk.enable UUID flag set to 1, this can be done using the [govc tool](https://github.com/vmware/govmomi/tree/master/govc) with the following command:

```text
govc vm.change -e="disk.enableUUID=1" -vm='/PATH/TO/VM'
```

## **Importing the QCOW2**

1. Convert it to vmdk: `qemu-img convert -f qcow2 -O vmdk CentOS-7-x86_64-GenericCloud.qcow2 CentOS-7-x86_64-GenericCloud.vmdk`
2. Upload it to a Datastore of your vSphere installation
3. Create a new virtual machine that uses the uploaded vmdk as rootdisk.

## **Modifications**

Modifications like Network, disk size, etc. must be done in the ova template before creating a worker node from it. If user clusters have dedicated networks, all user clusters, therefore, need a custom template.

## VM Folder

During the creation of a user cluster Kubermatic creates a dedicated VM folder in the root path on the Datastore \(Defined in the [datacenters.yaml](https://docs.kubermatic.io/installation/install_kubermatic/#defining-the-datacenters)\). That folder will contain all worker nodes of a user cluster.

## Credentials / Cloud-Config

Kubernetes needs to talk to the vSphere to enable Storage inside the cluster. For this, kubernetes needs a config called `cloud-config`. This config contains all details to connect to a vCenter installation, including credentials.

As this Config must also be deployed onto each worker node of a user cluster, its recommended to have individual credentials for each user cluster.

## Permissions

The VSphere user must have the following permissions on the correct resources

## **Seed Cluster**

* Role `k8c-storage-vmfolder-propagate`
  * Granted at **VM Folder** and **Template Folder**, propagated
  * Permissions
    * Virtual machine
      * Change Configuration
        * Add existing disk
        * Add new disk
        * Add or remove the device
        * Remove disk
    * Folder
      * Create folder
      * Delete folder
* Role `k8c-storage-datastore-propagate`
  * Granted at **Datastore**, propagated
  * Permissions
    * Datastore
      * Allocate space
      * Low-level file operations
* Role `Read-only` \(predefined\)
  * Granted at …, **not** propagated
    * Datacenter

## **User Cluster**

* Role `k8c-user-vcenter`
  * Granted at **vcentre** level, **not** propagated
  * Needed to customize VM during provisioning
  * Permissions
    * VirtualMachine
      * Provisioning
        * Modify customization specification
        * Read customization specifications
* Role `k8c-user-datacenter`
  * Granted at **datacentre** level, **not** propagated
  * Needed for cloning the template VM \(obviously this is not done in a folder at this time\)
  * Permissions
    * Datastore
      * Allocate space
      * Browse datastore
      * Low-level file operations
      * Remove file
    * vApp
      * vApp application configuration
      * vApp instance configuration
    * Virtual Machine
      * Change CPU count
      * Memory
      * Settings
    * Inventory
      * Create from existing
* Role `k8c-user-cluster-propagate`
  * Granted at the **cluster** level, propagated
  * Needed for upload of `cloud-init.iso` \(Ubuntu and CentOS\) or defining the Ignition config into Guestinfo \(CoreOS\)
  * Permissions
    * Host
      * Configuration
        * System Management
      * Local operations
        * Reconfigure virtual machine
    * Resource
      * Assign virtual machine to the resource pool
      * Migrate powered off the virtual machine
      * Migrate powered-on virtual machine
    * vApp
      * vApp application configuration
      * vApp instance configuration
* Role k8s-network-attach
  * Granted for each network that should be used
  * Permissions
    * Network
      * Assign network
* Role `k8c-user-datastore-propagate`
  * Granted at **datastore/datastore cluster** level, propagated
  * Permissions
    * Datastore
      * Allocate space
      * Browse datastore
      * Low-level file operations
* Role `k8c-user-folder-propagate`
  * Granted at **VM Folder** and **Template Folder** level, propagated
  * Needed for managing the node VMs
  * Permissions
    * Folder
      * Create folder
      * Delete folder
    * Global
      * Set custom attribute
    * Virtual machine
      * Change Configuration
      * Edit Inventory
      * Guest operations
      * Interaction
      * Provisioning
      * Snapshot management

The described permissions have been tested with vSphere 6.7 and might be different for other vSphere versions.

## **Volume Detach Bug**

After a node is powered-off, the Kubernetes vSphere driver doesn’t detach disks associated with PVCs mounted on that node. This makes it impossible to reschedule pods using these PVCs until the disks are manually detached in vCenter.

Upstream Kubernetes has been working on the issue for a long time now and tracking it under the following tickets:

* [https://github.com/kubernetes/kubernetes/issues/63577](https://github.com/kubernetes/kubernetes/issues/63577)
* [https://github.com/kubernetes/kubernetes/issues/61707](https://github.com/kubernetes/kubernetes/issues/61707)
* [https://github.com/kubernetes/kubernetes/issues/67900](https://github.com/kubernetes/kubernetes/issues/67900)
* [https://github.com/kubernetes/kubernetes/issues/71829](https://github.com/kubernetes/kubernetes/issues/71829)
* [https://github.com/kubernetes/kubernetes/issues/75342](https://github.com/kubernetes/kubernetes/issues/75342)

