# Launch a pre-build Ubuntu Core image on a GCE instance

Pre-built images are ideal for exploration and experimentation of Ubuntu Core, but they are not intended for deployment or use at scale. 

You can find more information about building Core images for public clouds in the [Build a public cloud image](/tutorials/build-a-public-cloud-image/index) tutorial.


## Requirements

You will need:

- An existing GCP account
- Credentials - A [public SSH key added to your project](https://cloud.google.com/compute/docs/connect/add-ssh-keys#add_ssh_keys_to_project_metadata)
- Google CLI '`gcloud`' installed ([installation instructions](https://cloud.google.com/sdk/docs/install#deb))

## Launch an Ubuntu Core image

To launch a pre-built image in GCE, run:

~~~bash

gcloud compute instances create YOUR_INSTANCE_NAME \
    --image-family=IMAGE_FAMILY \
    --image-project=IMAGE_PROJECT
    --zone=YOUR_ZONE
~~~

with YOUR_INSTANCE_NAME changed to a VM name of your choosing. 

----- TODO: replace IMAGE_FAMILY, IMAGE_PROJECT and YOUR_ZONE with some valid values ------

## Log in to the instance

Now that the instance is launched, we can determine its IP address and then log into it.

To find the IP address, run:

~~~bash
gcloud compute instances describe "YOUR_INSTANCE_NAME" --zone="YOUR_ZONE" \
            --format='get(networkInterfaces[0].accessConfigs[0].natIP)')
~~~

where `YOUR_INSTANCE_NAME` and `YOUR_ZONE` is replaced with the corresponding values that you chose above. Save the IP address and log in to the instance using:

~~~bash
ssh -i PRIVATE_SSH_KEY_FILE ubuntu@IP_ADDRESS
~~~

where 
* `PRIVATE_SSH_KEY_FILE` is the filename of your private SSH key that corresponds to the public key set up in your GCP project and
* `IP_ADDRESS` is the IP address that was just found.

An example command looks like:

~~~bash
ssh -i ~/.ssh/gcp_key ubuntu@104.198.153.7
~~~

Congratulations! You have successfully launched a GCE instance with a pre-built Ubuntu Core image.

See [First steps with Ubuntu Core](/how-to-guides/using-ubuntu-core) for an introduction to using your new Ubuntu Core installation or learn how to [build your own Ubuntu Core image for public clouds](/tutorials/build-a-public-cloud-image/index).
