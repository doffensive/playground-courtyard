# Import .ova virtual appliance (collection of VMs)

Place .ova file in /var/lib/vz/images.

Extract .ova file.
```
# tar -xvf image.ova
```

Convert .vmdk file to .raw.
```
# qemu-img convert image.vmdk -O raw image.raw
```

Gather image requirements.
* ID # of cores and amount of memory: `# cat image.ovf`
* ID virtual disk size: `# qemu-img info image.vmdk`

Create a new VM in Proxmox GUI and match or exceed image hardware requirements. Select “Do not use any media” in the CD/DVD tab and IDE as the Bus/Device in the Hard Disk tab.

Clone the .raw file into the newly created logical volume located at /dev/pve/:
```
# dd if=/var/lib/vz/images/image.raw of=/dev/pve/vm-100-disk-1 bs=1M
```
