# Build a public cloud image

Ubuntu Core images can be used on the public clouds. To **build and register an Ubuntu Core image on different public clouds** such as AWS, Azure and GCP, follow the steps of this tutorial.

## Step-by-step guide

1. [Requirements](requirements)
1. [Create an Ubuntu One account](access-ubuntu-one)
   1. [Create the account online](access-ubuntu-one.md#create-an-ubuntu-one-account)
   1. [Retrieve your developer account id](access-ubuntu-one.md#retrieve-your-developer-account-id)
1. [Create the model assertion](create-a-model)
   1. [Download a model assertion](create-a-model.md#download-a-model-file)
   1. [Edit the model assertion](create-a-model.md#edit-the-model-file)
   1. [authority-id and brand-id](create-a-model.md#authority-id-and-brand-id)
   1. [timestamp](create-a-model.md#timestamp)
   1. [snaps](create-a-model.md#snaps)
   1. [A complete model assertion](create-a-model.md#complete-model-example)
1. [Sign the model assertion](sign-the-model)
   1. [Create a key](sign-the-model.md#create-a-key)
   1. [Register the key](sign-the-model.md#register-the-key)
   1. [Sign the model](sign-the-model.md#sign-the-model)
1. [Build and register the image](build-the-image)
   1. [Compile the image](build-the-image.md#compile-the-image)
   1. [Register the image](build-the-image.md#register-the-image)
1. [Launch the image](launch-the-image)
   1. [Launch Ubuntu Core](launch-the-image.md#launch-ubuntu-core)
   1. [Connect to the device](launch-the-image.md#connect-to-the-device)

```{toctree}
:hidden:
:titlesonly:
:maxdepth: 2
:glob:

Requirements <requirements>
Access Ubuntu One <access-ubuntu-one>
Create a model <create-a-model>
Sign the model <sign-the-model>
Build the image <build-the-image>
Launch the image <launch-the-image>
