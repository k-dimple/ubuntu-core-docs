# Launch the image

After [building and registering](/tutorials/build-a-public-cloud-image/build-the-image) a custom Ubuntu Core image for a public cloud, it has to be launched for use.

## Launch Ubuntu Core

````{tabs}

```{group-tab} AWS
To launch the image in AWS on an EC2 instance, run:

~~~bash
aws ec2 run-instances --image-id <image id> --key-name <your key pair> --region <your region> --instance-type <instance type> 
~~~
In the above command, replace 
- `<image id>` with the saved AMI ID from the previous step of [registering the image](/tutorials/build-a-public-cloud-image/build-the-image)
- `<your key pair>` with your secret key pair 
- `<your region>` with the region where you have registered your image and 
- `<instance type>` with one of the AMD64 [instance types available on Amazon](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-types.html). Choose an instance with UEFI support. 


An example command would look like:

~~~bash
aws ec2 run-instances --image-id ami-00710b821b31f5c78 --key-name TestKeyPair --region us-east-1 --instance-type t3.medium 
~~~

The output of this command includes an instance ID. Save the value as it'll be needed as an input in the next command.

```
```{group-tab} Azure
Prerequisites:

* A valid Microsoft Azure account
* [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/?view=azure-cli-latest)
* The image version registered in an Azure compute gallery as part of [building the image](/tutorials/build-a-public-cloud-image/build-the-image)

The following commands will:

1. Retrieve the image reference for the image version registered in the Azure compute gallery
2. Launch an Azure image version using the image reference

~~~bash
COMPUTE_GALLERY_RESOURCE_GROUP="..."
COMPUTE_GALLERY="..."
IMAGE_DEFINITION="..."
IMAGE_VERSION="..."

IMAGE_REFERENCE=$(
    az sig image-version show \
        --resource-group "${COMPUTE_GALLERY_RESOURCE_GROUP}" \
        --gallery-name "${COMPUTE_GALLERY}" \
        --gallery-image-definition "${IMAGE_DEFINITION}" \
        --gallery-image-version "${IMAGE_VERSION}" \
        --query "id" \
        --output tsv
)

LOCATION="..."              # See az account list-locations.
VM_RESOURCE_GROUP="..."

az group create \
    --location "${LOCATION}" \
    --name "${VM_RESOURCE_GROUP}"

VM_NAME="..."
USERNAME="..."

# --generate-ssh-keys will generate a SSH keypair in the ~/.ssh directory.
# Alternatively, existing SSH key(s) can be provided with --ssh-key-values.
az vm create \
    --resource-group "${VM_RESOURCE_GROUP}" \
    --name "${VM_NAME}" \
    --image "${IMAGE_REFERENCE}" \
    --admin-username "${USERNAME}" \
    --generate-ssh-keys
~~~

```

```{group-tab} GCP
Content to be added
```
````

## Log in to the instance

````{tabs}

```{group-tab} AWS
Now that the instance is launched, we can determine its hostname and then log into it.

To find the hostname, run:

~~~bash
aws ec2 describe-instances --instance-ids <your instance id>
~~~

where `<your instance id>` is replaced with the instance ID that you saved above. The output will contain the required hostname in a field called _PublicDnsName_. 

Now, log in to the instance using:

~~~bash
ssh -i <private SSH key file> ubuntu@<external-host-name>
~~~

where `<private SSH key file>` is the filename of the private SSH key that corresponds to the key pair used above (in the ec2 run-instances command), and `<external-host-name>` is the hostname just found.

An example command looks like:

~~~bash
ssh -i TestKeyPair.pem ubuntu@ec2-135-28-52-91.compute-1.amazonaws.com
~~~

```
```{group-tab} Azure
The launched instance can be accessed using SSH:

~~~bash
ssh -i <private_ssh_key_path> <username>@<public_ip_address>

~~~

The public IP address for the instance can be determined either from the command output of the Azure CLI command used to
create the instance, or by navigating to the virtual machine resource in the Azure Portal where it will be displayed in the
networking properties.

An example command looks like:
~~~bash
ssh -i ~/.ssh/id_rsa ubuntu@20.112.118.62
~~~

```

```{group-tab} GCP
Content to be added
```
````

Congratulations! You have successfully built your own Ubuntu Core image, launched it on a VM on a public cloud, and logged into that VM.

----------- TODO: Change the following to point to a new how-to-guide that is public cloud specific. In that guide, use some specific example (TBD) to show how one can experiment with the image. ----------

See [First steps with Ubuntu Core](/how-to-guides/using-ubuntu-core) for an introduction to using Ubuntu Core.

