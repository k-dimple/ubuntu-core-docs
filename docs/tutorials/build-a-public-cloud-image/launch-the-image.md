# Launch the image

After [building and registering](/tutorials/build-your-first-image/build-the-image) a custom Ubuntu Core image for a public cloud, it has to be launched for use. You can launch it using either the cloud's graphical interface or through a command line interface (CLI). Here we'll be using the CLI. 


## Install the CLI

````{tabs}

```{tab} AWS

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

Use your access key credentials for the first two, specify a region and choose your preferred CLI output format from one of json, text or table. A sample response would look like:

---- TODO: Add a sample response -----
 
```
```{tab} Azure

Content to be added
```

```{tab} GCP

Content to be added
```
````
## Launch Ubuntu Core

Using the CLI we can launch the image. The steps involved are different for each cloud.

````{tabs}

```{tab} AWS
To launch an image in AWS, you need to know its Amazon Machine Image (AMI) ID. To find the AMI ID of your image, run:

---- TODO: Replace with the correct command ------
~~~bash
aws ssm get-parameters --names \
   /aws/service/canonical/ubuntu/server/24.04/stable/current/amd64/hvm/ebs-gp3/ami-id
~~~

In the generated output, the “Value” field will have the required AMI ID. 

Now, launch the image in an EC2 instance:

~~~bash
aws ec2 run-instances --image-id <image id> --key-name <your key pair> --instance-type <instance type>
~~~

Here replace <image id> with AMI ID obtained above, <your key pair> with your secret key pair and <instance type> with one of the AMD64 instance types available mentioned in the [Amazon EC2 instance types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-types.html). Do not choose an instance that does not have UEFI support.

An example command would look like:

~~~bash
aws ec2 run-instances --image-id ami-0014ce3e52359afbd --key-name TestKeyPair --instance-type t3.medium
~~~

```
```{tab} Azure
Content to be added
```

```{tab} GCP
Content to be added
```
````


## Connect to the device

---- TODO: Add content -----

Congratulations! You have successfully built your own image, installed it, and connected to Ubuntu Core on a public cloud.

----------- TODO: Change this to point to a new how-to-guide that is public cloud specific. In that guide, use some specific example (TBD) to show how one can experiment with the image. ----------

See [First steps with Ubuntu Core](/how-to-guides/using-ubuntu-core) for an introduction to using Ubuntu Core.

