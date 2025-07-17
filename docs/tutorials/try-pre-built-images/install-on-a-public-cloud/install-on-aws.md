# Install a pre-build Ubuntu Core image on an AWS EC2 instance

Pre-built images are ideal for exploration and experimentation of Ubuntu Core, but they are not intended for deployment or use at scale. 

You can find more information about building Core images for public clouds in the [Build a public cloud image](/tutorials/build-a-public-cloud-image/index) tutorial.


## Requirements

You will need:

- An existing AWS account
- AWS CLI installed
- [Credentials (key pairs and access keys)](https://documentation.ubuntu.com/aws/aws-how-to/instances/launch-ubuntu-ec2-instance/#setup-credentials)

## Launch an Ubuntu Core image

To launch an image in AWS, you need to know its Amazon Machine Image (AMI) ID. To find the AMI ID of your image, run:

~~~bash
aws ssm get-parameters --names \
   /aws/service/canonical/ubuntu/core/24.04/stable/current/amd64/hvm/ebs-gp3/ami-id
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


## Log in to the instance

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


Congratulations! You have successfully launched an EC2 instance with a pre-built Ubuntu Core image.

----- TODO: Change the following to point to a new how-to-guide that is public cloud specific. In that guide, use some specific example (TBD) to show how one can experiment with the image. ———

See [First steps with Ubuntu Core](/how-to-guides/using-ubuntu-core) for an introduction to using your new Ubuntu Core installation or learn how to [build your own Ubuntu Core image for public clouds](/tutorials/build-a-public-cloud-image/index).
