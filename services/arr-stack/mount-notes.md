On proxmox host I shared the zfs pool to the 192.168.8.0/24 subnet by doing:
line was added to /etc/exports

/mnt/tank 192.168.8.0/24(rw,sync,no_subtree_check,no_root_squash)

Mounted on the docker vm by running:
sudo mount -t nfs 192.168.8.250:/mnt/tank /mnt/tank/
192.168.8.250 = being the proxmox host that nfs server was setup on

Added line to /etc/fstab to have mount persist between restarts:
192.168.8.250:/mnt/tank  /mnt/tank  nfs  defaults,_netdev  0 0

Test if it worked:

sudo mount -a
df -h | grep tank
