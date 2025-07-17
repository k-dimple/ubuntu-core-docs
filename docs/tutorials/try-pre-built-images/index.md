# Try pre-built images

Ubuntu Core runs on a variety of hardware, and pre-built images are available for various platforms. Generic images can also be installed on a virtual machine.

Pre-built images are ideal for exploration and experimentation, but they are not intended for deployment or use at scale. They include snaps to provide an onboarding and evaluation experience, alongside an SSH connection, and these are unlikely to be required in your own Ubuntu Core deployment. 

Ubuntu Core has instead been designed to facilitate creating, deploying, and managing secure custom images running on your hardware.

See [Supported testing platforms](/reference/testing-platforms) for links to image downloads, and to learn how to create your own custom image, read our [Build an image](/tutorials/build-your-first-image/index) guide.

## Install on a virtual machine

You can try Ubuntu Core without any specific hardware from within a virtual machine using Multipass on Windows, Mac and Linux.

* [Install on a VM](install-on-a-vm): Try Ubuntu Core on a local machine

## Install on a generic device

Ubuntu Core runs on a large range of hardware, and pre-built images are available for amd64 and Raspberry Pi reference platforms.

- [Use Raspberry Pi imager](install-on-a-device/use-raspberry-pi-imager): install a pre-built Ubuntu Core image on a Raspberry Pi
- [Use the dd command](install-on-a-device/use-the-dd-command): write an Ubuntu Core reference image to internal storage

## Install on a specific device

Pre-built test images are also available for Renesas GZ/G2L and MediaTek Genio devices.

- [Install on a Renesas RZ/G2L](install-on-a-device/install-on-renesas): Install a pre-built image on a Renesas RZ/G2L device <install-on-renesas>
- [Install on a MediaTek Genio](install-on-a-device/install-on-mediatek): Install a pre-built image on a MediaTek Genio device <install-on-mediatek>

## Install on a public cloud

Pre-built Ubuntu Core images are available on different public cloud platforms. Currently they are available on Amazon AWS, Microsoft Azure and Google cloud.  
-- TODO: Update as required ----

* [Install on AWS](install-on-a-public-cloud/install-on-aws): Try Ubuntu Core on an AWS EC2 instance
* [Install on Azure](install-on-a-public-cloud/install-on-azure): Try Ubuntu Core on Azure
* [Install on GCP](install-on-a-public-cloud/install-on-gcp): Try Ubuntu Core on a GCE instance in Google cloud. 


```{toctree}
:hidden:
:titlesonly:
:maxdepth: 2
:glob:

Install on a VM <install-on-a-vm>
Install on a device <install-on-a-device/index>
Install on a public cloud <install-on-a-public-cloud/index>
