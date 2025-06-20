# Launch the image

After [building and registering](/tutorials/build-your-first-image/build-the-image) a custom Ubuntu Core image for a public cloud, it has to be launched for use. You can launch it using either the cloud's graphical interface or through a command line interface (CLI). Here we'll be using the CLI. 


## Install the CLI

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

Use your access key credentials for the first two, specify a region and choose your preferred CLI output format from one of json, text or table. A sample response would look like:

---- TODO: Add a sample response -----
 
```
```{group-tab} Azure

Content to be added
```

```{group-tab} GCP

Content to be added
```
````

## Launch Ubuntu Core

````{tabs}

```{group-tab} AWS
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

In the above command, replace `<image id>` with the AMI ID obtained above, `<your key pair>` with your secret key pair and `<instance type>` with one of the AMD64 [instance types available on Amazon](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-types.html). Do not choose an instance that does not have UEFI support. ---- TODO: Check if this bit about instance types is correct and enough. e.g. How do we check if the instance type has UEFI support or not. -----

An example command would look like:

---- TODO: Update this to a correct example ---- 
~~~bash
aws ec2 run-instances --image-id ami-0014ce3e52359afbd --key-name TestKeyPair --instance-type t3.medium
~~~

The output of this command includes an instance ID. Save the value as it'll be needed as an input in the next command.

```
```{group-tab} Azure
Content to be added
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

---- TODO: Check the command ------
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
Content to be added
```

```{group-tab} GCP
Content to be added
```
````

Congratulations! You have successfully built your own Ubuntu Core image, launched it on a VM on a public cloud, and logged into that VM.

----------- TODO: Change this to point to a new how-to-guide that is public cloud specific. In that guide, use some specific example (TBD) to show how one can experiment with the image. ----------

See [First steps with Ubuntu Core](/how-to-guides/using-ubuntu-core) for an introduction to using Ubuntu Core.

