# Build the image

Images are built from the recipe contained in the [model assertion](/tutorials/build-a-public-cloud-image/create-a-model) using [ubuntu-image](https://github.com/canonical/ubuntu-image), a tool to generate a bootable image.

## Compile the image

First, install the `ubuntu-image` command from its snap:

```
sudo snap install ubuntu-image --classic
```

The `ubuntu-image` command requires two arguments; `snap` to indicate we're building a snap-based Ubuntu Core image, and the filename of our previously-signed model assertion to build an image:

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


## Register the image

The next step is to upload and register the image for use on a cloud.

````{tabs}

```{group-tab} AWS
Before you can register the image, you need to change its format by converting the raw image into a _.vmdk_ file. To do this, first install _qemu-utils_:

~~~bash
sudo apt install qemu-utils
~~~

Now use the _qemu-img_ command to perform the format conversion:

~~~bash
qemu-img convert -f raw -O vmdk -o subformat=streamOptimized pc.img pc.vmdk
~~~

To register / publish the image, we'll use a tool called _awspub_. Install it using:

~~~bash
snap install awspub
~~~

Now create a config file called `config.yaml` containing:

~~~bash
awspub:
  source:
    path: "pc.vmdk"
    architecture: "x86_64"
  s3:
    bucket_name: "my-bucket"
  images:
    "my-ubuntu-core-image":
      description: |
        My Ubuntu Core image for AWS
      boot_mode: "uefi"
      root_device_volume_type: "gp3"
      root_device_volume_size: 8
      root_device_name: "/dev/sda1"
      imds_support: "v2.0"
      public: false
      regions:
        - "us-east-1"
~~~

In the above, the region specified is "us-east-1", but if you have created your S3 bucket in a different region, use that instead. You can also rename "my-bucket" and "my-ubuntu-core-image" appropriately.

Finally, register the image using:

~~~bash
awspub create config.yaml
~~~

The output will include the Amazon Machine Image (AMI) ID of the published image, with the relevant portion looking something like:

~~~bash
{
  "images": {
    "my-ubuntu-core-image": {
      "us-east-1": "ami-00710b821b31f5c78"
    ...
~~~
Make a note of the AMI ID since it'll be needed in the next step while [launching the image](launch-the-image).
 
```
```{group-tab} Azure

Content to be added
```

```{group-tab} GCP

Content to be added
```
````