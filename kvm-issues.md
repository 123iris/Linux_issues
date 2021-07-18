
While taking commit then got this error

```
Starting backup for mzworker5.sbMosip2Node2 on 03-06-2021 11:27:22
Domain snapshot backup-mzworker5.sbMosip2Node2 created
Backup does not exist, creating a full sparse copy
sending incremental file list
mzworker5.sbMosip2Node2.qcow2

sent 6,849,251,545 bytes  received 35 bytes  11,839,674.30 bytes/sec
total size is 11,319,574,528  speedup is 1.65
error: 
Commit failed

Could not merge changes for disk of vda of vmNamw. VM may be in invalid state.

```

Solution: edit vm xml file and add these things as below at storage tag. remove block quote and other thing

```
$ virsh edit vmName

    <disk type='file' device='disk'>
      <driver name='qemu' type='qcow2'/>
      <source file='/mnt/infra/mzworker2.sbMosip2Node2.qcow2'/>
      <target dev='vda' bus='virtio'/>
    </disk>
```