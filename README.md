# Hive OS PXE Diskless
Network boot for diskless BC-250 Rigs

This is just a temperorary fix while HiveOs gets off their asses, check if they've fixed.

This is a modified version of the Hiveos Pxe diskless to work with BC-250 Mining cards. 
The opencl version in hiveramfs says its 21.40.1 but its actually version 22.20 with rocm and fully is compatiable with the BC-250. 

Before you start, it took me a bit of time to figure this out, no thanks to the hive devs so i’d be much appreciate if you donated a little wart. (I did save you a lot in nvme’s 🙂)
09485c66d358f2178e479aa07fb668a4d7bffb48c8c0cf69
Thanks, James. 

Copy the install link below 
Then build the Ubuntu18 with ./deploy_pxe ubuntu18 --build (it will take awhile)
then re run ./pxe_setup.sh

Other Notes

Do not use ./deploy_pxe ubuntu18 --upgrade it will break the permissions on the BC-250 Rig. 

In BC-250 Bios change network boot to enable and Ipv4 PXE (Http isnt used do not enable)
In bios you can enable SVM if needed (but does not make a difference) but do not enable IOMMU it will not work.

Documentation
https://forum.hiveos.farm/t/hive-os-diskless-pxe/12319

Requires : sudo, xz-utils, pxz
```apt-get install -yqq sudo xz-utils pxz```

For installation directly from the GitHub, execute the following command in the terminal:

```wget https://raw.githubusercontent.com/TheJames5/hiveos-pxe-diskless/master/pxe-setup.sh && sudo bash pxe-setup.sh```

```cd  path_to_pxeserver```

Type ```./deploy_pxe ubuntu18 --build```.
This command create new hiveramfs image in pxeserver/hiveramfs/ folder. Rootfs stored in pxeserver/build/ubuntu18/_fs.
Try ```./deploy_pxe --help``` for see more options

If you need support Nvidia cards, use ```./deploy_pxe nvidia list``` for list all avaliable drivers and ```./deploy_pxe nvidia --build <VER>``` to create nvidia-<VER>.tar.xz image.
This image will be stored in pxeserver/hiveramfs/nvidia folder.

**Below part deprecated and will be removed in next release!!!**
**Important note:** the file system archive is splitting into several files. Due to github restrictions on file size.
In case you clone or download this repository yourself - you need to collect parts of the archive back into one file:

```cat pxeserver/hiveramfs/x* > pxeserver/hiveramfs/hiveramfs.tar.xz```