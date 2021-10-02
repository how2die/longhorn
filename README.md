# Longhorn 

## Install Longhorn to cluster
Install open-iscsi on all nodes:
`sudo apt-get install open-iscsi`

Deploy longhorn using kubectl:
`kubectl apply -f longhorn.yaml`, feched from https://raw.githubusercontent.com/longhorn/longhorn/v1.2.0/deploy/longhorn.yaml

Verify that everything is up and running:
`kubectl get all --namespace longhorn-system`

## Add extra storage
Connect extra storage, and SSH into the node. Create mount point:
`sudo mkdir /media/storage`

Get the PARTUUID or UUID with:
`sudo blkid`

Modify /etc/fstab and add something like (with the appropriate file system type):
`PARTUUID=[partition uuid] /media/storage ext4 defaults,noatime,nodiratime 0 2`

Test with:
`sudo mount -a`

Use the Longhorn UI to add storage under Nodes and "Edit node and disks". Click "Add Disk" and insert path (e.g. /media/storage/longhorn).
