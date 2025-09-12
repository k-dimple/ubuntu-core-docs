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
- AWS CLI installed (installation instructions below)
- An Amazon S3 bucket in the region where you want your image to reside

```
```{group-tab} Azure

- An existing Azure account
- ---- TODO: Check if anything more is needed -----
```

```{group-tab} GCP

Content to be added
```
````


## CLI installation instructions

Since most of the tutorial uses CLI commands, you'll need the respective cloud CLI to be installed.  

````{tabs}

```{group-tab} AWS

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

```
```{group-tab} Azure

Content to be added
```

```{group-tab} GCP

Content to be added
```
````
