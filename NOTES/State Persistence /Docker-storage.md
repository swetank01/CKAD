# Docker Storage

First understand how storage works with container like Docker Storage Drivers and Volume Drivers
i.e Docker Storage:  Storage Driver & Volume Driver


## PV

### Spec:

1. accessModes:

```sh
accessModes:
    - <value>
```
* supported value are 'ReadOnlyMany' , 'ReadWriteOnce', 'ReadWriteMany'.

##### Example: 

```sh
specs:
    accessModes:
        - ReadWriteOnce
```


2. capacity:

```sh
capacity:
    storage: <value>
```
* supported value are '1Gi' , '512Mi'.

##### Example: 

```sh
specs:
    capacity:
        storage: 10G

```

3. Type:
- defined directly

```sh
<value>:
    path: '/any-system-path'
```
* supported value are 'ceph', 'fc' , 'hostPath', 'local', 'nfs'.

##### Example: 

```sh
specs:
    hostPath:
        path: /tmp/data
```



#### Types of Persistent Volumes 

PersistentVolume types are implemented as plugins. Kubernetes currently supports the following plugins:

- cephfs - CephFS volume
- csi - Container Storage Interface (CSI)
- fc - Fibre Channel (FC) storage
- hostPath - HostPath volume (for single node testing only; WILL NOT WORK in a multi-node cluster; consider using local volume instead)
- iscsi - iSCSI (SCSI over IP) storage
- local - local storage devices mounted on nodes.
- nfs - Network File System (NFS) storage
- rbd - Rados Block Device (RBD) volume