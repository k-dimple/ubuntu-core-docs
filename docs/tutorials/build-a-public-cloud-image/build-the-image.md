# Build the image

Images are built from the recipe contained in the [model assertion](/tutorials/build-a-public-cloud-image/create-a-model) using [ubuntu-image](https://github.com/canonical/ubuntu-image), a tool to generate a bootable image.

## Compile the image

First, install the `ubuntu-image` command from its snap:

```
sudo snap install ubuntu-image --classic
```

The `ubuntu-image` command requires two arguments; `snap` to indicate we're building a snap-based Ubuntu Core image, and the filename of our previously-signed model assertion to build an image:

----------- TODO: Check if the following needs modifications ------------

```bash
$ ubuntu-image snap my-model.model
[0] prepare_image
WARNING: proceeding to download snaps ignoring validations, this default will change in the future. For now use --validation=enforce for validations to be taken into account, pass instead --validation=ignore to preserve current behavior going forward
WARNING: the kernel for the specified UC20+ model does not carry assertion max formats information, assuming possibly incorrectly the kernel revision can use the same formats as snapd
[1] load_gadget_yaml
[2] set_artifact_names
[3] populate_rootfs_contents
[4] generate_disk_info
[5] calculate_rootfs_size
[6] populate_bootfs_contents
[7] populate_prepare_partitions
[8] make_disk
[9] generate_snap_manifest
Build successful
```
You can safely ignore both of the above warnings, and the entire process should only take a few minutes (depending on your connectivity), with the creation of a `pc.img` Ubuntu Core image file being the end result.

----------- End of TODO ------------

## Register the image

The next step is to upload and register the image for use on a cloud.

````{tabs}

```{group-tab} AWS
Before you can register the image, you need to change its format by converting the raw image into a _.vmdk_ file. That can be done using the _qemu-img_ command.

TODO: Add instructions to install qemu-utils (if it is not present already)

~~~bash
qemu-img convert -f raw -O vmdk -o subformat=streamOptimized pc.img pc.vmdk
~~~

TODO: Add instructions to register the image (maybe using awspub, or some other standard AWS method)
 
```
```{group-tab} Azure

Content to be added
```

```{group-tab} GCP

Content to be added
```
````