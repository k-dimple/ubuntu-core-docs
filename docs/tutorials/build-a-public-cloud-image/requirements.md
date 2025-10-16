# Requirements

In addition to having a basic understanding of Linux and running commands from the terminal, this tutorial requires the following:

For the host system used to build the image:
- [Ubuntu 22.04 LTS](https://releases.ubuntu.com/22.04/) or later installed
- Internet connectivity
- 10GB of free storage space

For the public cloud that you want the image in:
````{tabs}

```{group-tab} AWS
- An active AWS account
- [Credentials (key pairs and access keys)](https://documentation.ubuntu.com/aws/aws-how-to/instances/launch-ubuntu-ec2-instance/#setup-credentials)
- AWS CLI '`aws-cli`' (see installation instructions below)
- An Amazon S3 bucket in the region where you want your image to reside (see instructions below)

```
```{group-tab} Azure

- A valid Microsoft Azure account
- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/?view=azure-cli-latest) '`azure-cli`' (see installation instructions below)
- An existing Azure [storage account](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-overview) and [compute gallery](https://learn.microsoft.com/en-us/azure/virtual-machines/azure-compute-gallery)
```

```{group-tab} GCP


- An existing GCP account
- Credentials - A [public SSH key added to your project](https://cloud.google.com/compute/docs/connect/add-ssh-keys#add_ssh_keys_to_project_metadata)
- Google CLI '`gcloud`' (see installation instructions below)
- A Cloud Storage bucket to store your image
```
````


## Installation instructions

Since most of the tutorial uses CLI commands, you'll need the respective cloud CLI to be installed. You'll also need some storage bucket to store the image that you create.  

````{tabs}

```{group-tab} AWS

### CLI installation

To install the AWS CLI, run:

~~~bash
sudo snap install aws-cli --classic
~~~

Then, configure it:

~~~bash
aws configure
~~~

Here you'll have to enter values for each of:

~~~bash
AWS Access Key ID [None]:
AWS Secret Access Key [None]:
Default region name [None]:
Default output format [None]:
~~~

Use your access key credentials for the first two, specify a region (such as 'eu-north-1') and choose your preferred CLI output format from one of 'json', 'text' or 'table'.

### S3 bucket creation

To create an S3 bucket named "my-bucket" in the "us-east-1" region, run:

~~~bash
aws s3api create-bucket \
    --bucket my-bucket \
    --region us-east-1
~~~

You can change the bucket name and region as required. For better speeds, choose a region closer to you.

```
```{group-tab} Azure

[Instructions for installing Azure CLI on Ubuntu](https://documentation.ubuntu.com/azure/azure-how-to/instances/install-azure-cli/).
```

```{group-tab} GCP

[Instructions for installing gcloud, the Google CLI](https://cloud.google.com/sdk/docs/install#deb).

[Instructions for creating a new cloud storage bucket on GCP](https://cloud.google.com/storage/docs/creating-buckets#command-line).
```
````
