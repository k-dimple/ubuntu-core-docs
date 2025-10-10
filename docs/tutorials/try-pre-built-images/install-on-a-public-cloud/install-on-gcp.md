# Install a pre-build Ubuntu Core image on a GCE instance

Pre-built images are ideal for exploration and experimentation of Ubuntu Core, but they are not intended for deployment or use at scale. 

You can find more information about building Core images for public clouds in the [Build a public cloud image](/tutorials/build-a-public-cloud-image/index) tutorial.


## Requirements

You will need:

- An existing GCP account and
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

Now that the instance is launched, you can log into it using:

~~~bash
gcloud compute ssh YOUR_INSTANCE_NAME --zone=YOUR_ZONE
~~~

where YOUR_INSTANCE_NAME and YOUR_ZONE correspond to the values used above in the previous command. 

An example command looks like:

~~~bash
gcloud compute ssh my-ubuntu-core-instance --zone=us-central1-a
~~~


Congratulations! You have successfully launched a GCE instance with a pre-built Ubuntu Core image.

----- TODO: Change the following to point to a new how-to-guide that is public cloud specific. In that guide, use some specific example (TBD) to show how one can experiment with the image. ———

See [First steps with Ubuntu Core](/how-to-guides/using-ubuntu-core) for an introduction to using your new Ubuntu Core installation or learn how to [build your own Ubuntu Core image for public clouds](/tutorials/build-a-public-cloud-image/index).
