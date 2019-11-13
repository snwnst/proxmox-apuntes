# proxmox-apuntes

## Creating an extra LV for /var/lib/vz
    This can be easily done by creating a new thin LV.
        - lvcreate -n <Name> -V <Size[M,G,T]> <VG>/<LVThin_pool>
    
    A real world example:
        - lvcreate -n vz -V 10G pve/data
    
    Now a filesystem must be created on the LV.
        - mkfs.ext4 /dev/pve/vz
        At last this has to be mounted.

    Warning	be sure that /var/lib/vz is empty. On a default installation it’s not.
    To make it always accessible add the following line in /etc/fstab.
        - echo '/dev/pve/vz /var/lib/vz ext4 defaults 0 2' >> /etc/fstab

## Create a LVM-thin pool
    A thin pool has to be created on top of a volume group. How to create a volume group see Section LVM.
        - lvcreate -L 80G -T -n vmstore vmdata