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
- AWS CLI installed (see instructions below)
- An Amazon S3 bucket in the region where you want your image to reside (see instructions below)

```
```{group-tab} Azure

- An existing Azure account
- ---- TODO: Check if anything more is needed -----
```

```{group-tab} GCP


- An existing GCP account
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

To install the Azure CLI refer to our documentation about [installing Azure CLI on Ubuntu](https://documentation.ubuntu.com/azure/azure-how-to/instances/install-azure-cli/)
```

```{group-tab} GCP

Refer to Google's documentation about [installing gcloud](https://cloud.google.com/sdk/docs/install#deb) to install the gcloud CLI.

Create a cloud storage bucket on GCP using their instructions for [creating a new bucket](https://cloud.google.com/storage/docs/creating-buckets#command-line).
```
````
