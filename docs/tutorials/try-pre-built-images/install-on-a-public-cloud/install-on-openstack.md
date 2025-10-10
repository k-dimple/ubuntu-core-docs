# Install a pre-built Ubuntu Core image on an OpenStack instance

Pre-built images are ideal for exploration and experimentation of Ubuntu Core, but they are not intended for deployment or use at scale. 

You can find more information about building Core images for public clouds in the [Build a public cloud image](/tutorials/build-a-public-cloud-image/index) tutorial.


## Requirements

You will need:

- An existing OpenStack environment
- An [OpenStack RC file](https://docs.openstack.org/newton/user-guide/common/cli-set-environment-variables-using-openstack-rc.html) for the OpenStack instance
- An [OpenStack command-line client](https://docs.openstack.org/newton/user-guide/common/cli-install-openstack-command-line-clients.html)
- `qemu-utils`

## Setup

Let's ensure that we have all of the packages installed before we begin. Most of these should be provided by your distribution already except for `qemu-utils`:

```bash
sudo apt update
sudo apt install wget xz-utils openssh-client qemu-utils
````

In a new directory for this project, place your OpenStack RC file from the [Requirements](#requirements) section above. Source the credentials file. This will look something like:

```bash
. PROJECT-openrc.sh
```

Download the image and convert it to QCOW format:
```bash
wget https://cdimage.ubuntu.com/ubuntu-core/24/stable/current/ubuntu-core-24-amd64.img.xz
unxz ubuntu-core-24-amd64.img.xz
qemu-img convert -c -O qcow2 ubuntu-core-24-amd64.img core24.qcow
```

Now that we have the Ubuntu Core in a format we can use with OpenStack, we're ready to deploy.

## Deploy to OpenStack

We're going to start by registering the image with OpenStack using the client you set up in the [Requirements](#requirements) section:

```bash
openstack image create TEST-ubuntu-core24 --disk-format qcow2 --file core24.qcow --property hw_firmware_type=uefi --progress
```

Use the `keypair create` subcommand to generate a new SSH key pair and save a copy to our working directory. Test the key exists in our OpenStack instance with the `keypair list` subcommand:

```bash
openstack keypair create TEST-ubuntu-core > key.pem
openstack keypair list | grep TEST-ubuntu-core
```

We need to secure the private file key. SSH will throw an error and ignore the key if its file permissions are too open, which they currently are. We don't need to modify this key in any way, so we will set the permissions as read-only for the owner:

```bash
chmod 400 key.pem
```

Now launch the instance on OpenStack using the key pair:

```bash
openstack server create TEST-core --image TEST-ubuntu-core24 --flavor b2-7 --network Ext-Net --key-name TEST-ubuntu-core --config-drive true
```

You should shortly be able to see the instance using the `server list` subcommand:

```bash
openstack server list
```

Take note of the IP address from the `Networks` column of the output as we will need it to log in to the instance. It is `01.234.567.89` format string after the `Ext-Net` value.

## Log in to the instance

Lastly connect to the instance, using the the IP from the above the previous step:

```bash
ssh -i key.pem ubuntu@<instance_ip>
```

Congratulations! You have successfully launched an OpenStack instance with a pre-built Ubuntu Core image.

## More information

See [First steps with Ubuntu Core](/how-to-guides/using-ubuntu-core) for an introduction to using your new Ubuntu Core installation or learn how to [build your own Ubuntu Core image for public clouds](/tutorials/build-a-public-cloud-image/index).
