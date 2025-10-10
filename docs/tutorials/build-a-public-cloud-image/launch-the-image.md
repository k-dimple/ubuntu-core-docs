# Launch the image

After [building and registering](/tutorials/build-a-public-cloud-image/build-the-image) a custom Ubuntu Core image for a public cloud, it has to be launched for use.

## Launch Ubuntu Core

````{tabs}

```{group-tab} AWS
To launch the image in AWS on an EC2 instance, run:

~~~bash
aws ec2 run-instances --image-id IMAGE_ID --key-name YOUR_KEY_PAIR --region YOUR_REGION --instance-type INSTANCE_TYPE 
~~~
In the above command, replace 
- `IMAGE_ID` with the saved AMI ID from the previous step of [registering the image](/tutorials/build-a-public-cloud-image/build-the-image)
- `YOUR_KEY_PAIR` with your secret key pair 
- `YOUR_REGION` with the region where you have registered your image and 
- `INSTANCE_TYPE` with one of the AMD64 [instance types available on Amazon](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-types.html). Choose an instance with UEFI support. 


An example command would look like:

~~~bash
aws ec2 run-instances --image-id ami-00710b821b31f5c78 --key-name TestKeyPair --region us-east-1 --instance-type t3.medium 
~~~

The output of this command includes an instance ID. Save the value as it'll be needed as an input in the next command.

```
```{group-tab} Azure
Content to be added
```

```{group-tab} GCP
To launch the image in GCP, create a new VM using:

~~~bash
gcloud compute instances create YOUR_INSTANCE_NAME \
    --image=YOUR_IMAGE_NAME \
    --zone=YOUR_ZONE
~~~

In the above command, replace 
- `YOUR_INSTANCE_NAME` with the name that you'd like your VM to have
- `YOUR_IMAGE_NAME` with the saved image name (“my-ubuntu-core-image”) from the previous step of [registering the image](/tutorials/build-a-public-cloud-image/build-the-image) and
- `YOUR_ZONE` with the zone where you want to create your VM. 

An example command would look like:

~~~bash
gcloud compute instances create my-ubuntu-core-instance \
    --image=my-ubuntu-core-image \
    --zone=us-central1-a
~~~
```
````

## Log in to the instance

````{tabs}

```{group-tab} AWS
Now that the instance is launched, we can determine its hostname and then log into it.

To find the hostname, run:

~~~bash
aws ec2 describe-instances --instance-ids YOUR_INSTANCE_ID
~~~

where `YOUR_INSTANCE_ID` is replaced with the instance ID that you saved above. The output will contain the required hostname in a field called _PublicDnsName_. 

Now, log in to the instance using:

~~~bash
ssh -i PRIVATE_SSH_KEY_FILE ubuntu@EXTERNAL_HOST_NAME
~~~

where 
* `PRIVATE_SSH_KEY_FILE` is the filename of the private SSH key that corresponds to the key pair used above (in the ec2 run-instances command), and
* `EXTERNAL_HOST_NAME` is the hostname just found.

An example command looks like:

~~~bash
ssh -i TestKeyPair.pem ubuntu@ec2-135-28-52-91.compute-1.amazonaws.com
~~~

```
```{group-tab} Azure
Content to be added
```

```{group-tab} GCP
Once the instance is launched, you can log into it using:

~~~bash
gcloud compute ssh YOUR_INSTANCE_NAME --zone=YOUR_ZONE
~~~

where YOUR_INSTANCE_NAME and YOUR_ZONE correspond to the values used above in the previous command. 

An example command looks like:

~~~bash
gcloud compute ssh my-ubuntu-core-instance --zone=us-central1-a
~~~

```
````

Congratulations! You have successfully built your own Ubuntu Core image, launched it on a VM on a public cloud, and logged into that VM.

----------- TODO: Change the following to point to a new how-to-guide that is public cloud specific. In that guide, use some specific example (TBD) to show how one can experiment with the image. ----------

See [First steps with Ubuntu Core](/how-to-guides/using-ubuntu-core) for an introduction to using Ubuntu Core.

