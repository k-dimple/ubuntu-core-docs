# Install a pre-build Ubuntu Core image on an Azure VM

Pre-built images are ideal for exploration and experimentation of Ubuntu Core, but they are not intended for deployment or use at scale. 

You can find more information about building Core images for public clouds in the [Build a public cloud image](/tutorials/build-a-public-cloud-image/index) tutorial.


## Requirements

You will need:

- A valid Microsoft Azure account
- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/?view=azure-cli-latest)

## Launch an Ubuntu Core image

To launch an Ubuntu Core image in Azure, run:

~~~bash
az vm create \
    --resource-group VM_RESOURCE_GROUP \
    --name VM_NAME \
    --image IMAGE_REFERENCE \
    --admin-username USERNAME \
    --generate-ssh-keys
~~~

--- TODO: Replace IMAGE_REFERENCE with the correct Marketplace URN once it is available ----


where 
- `VM_RESOURCE_GROUP` is the name of your VM's resource group,
- `VM_NAME` is the name that you want to give your VM and 
- `USERNAME` is the username that you'd like to use.

The `-generate-ssh-keys` option will generate a SSH keypair in your local ~/.ssh directory.

The output of this command includes the public IP address of the instance. Save the value as it'll be needed as an input in the next command.


## Log in to the instance

Now that the instance is launched, it can be accessed using SSH:

~~~bash
ssh -i <private_ssh_key_path> <username>@<public_ip_address>

~~~

Use the private SSH key present in the `~/.ssh` directory and the IP address saved from the previous step. 

An example command looks like:
~~~bash
ssh -i ~/.ssh/id_rsa ubuntu@20.112.118.62
~~~


Congratulations! You have successfully launched an Azure VM with a pre-built Ubuntu Core image.

----- TODO: Change the following to point to a new how-to-guide that is public cloud specific. In that guide, use some specific example (TBD) to show how one can experiment with the image. ———

See [First steps with Ubuntu Core](/how-to-guides/using-ubuntu-core) for an introduction to using your new Ubuntu Core installation or learn how to [build your own Ubuntu Core image for public clouds](/tutorials/build-a-public-cloud-image/index).

