# Create a model

At the heart of custom Ubuntu Core image creation is the _model assertion_. An assertion is a signed recipe that describes the components that comprise a complete image. An assertion is provided as JSON in a text file which is signed by a GPG key associated with the publisher's Ubuntu One account.

The model contains:
* identification information, such as the developer-id and model name.
* which [essential snaps](/explanation/core-elements/snaps-in-ubuntu-core) make up the device system.
* other required or optional snaps that implement the device application functionality.

See below for details on how to download and modify a model file to include your own selection of snaps.

## Download a model file

The quickest way to create a new model assertion is to edit a model that already exists. Reference models for every supported Ubuntu Core device can be found in the [snapcore/models](https://github.com/snapcore/models) GitHub repository, including ones for the different public clouds. Depending on the cloud that you are interested in, choose the appropriate tab below:

````{tabs}

```{group-tab} AWS

For AWS, we're going to modify [cloud/aws/aws-core-24-amd64.json](https://github.com/canonical/models/blob/master/cloud/aws/aws-core-24-amd64.json).


Download and save the file locally with the following _wget_ command. We've called the file `my-model.json`:

~~~bash
wget -O my-model.json https://github.com/canonical/models/blob/master/cloud/aws/aws-core-24-amd64.json
~~~
```

```{group-tab} Azure

Content to be added
```

```{group-tab} GCP

Content to be added
```
````

## Edit the model file

We now need to edit `my-model.json` using a text editor:

```
nano my-model.json
```

The following fields in `my-model.json` need to be changed:


###  "authority-id" and "brand-id"

```json
"authority-id": "canonical",
"brand-id": "canonical",
```

These properties define the authority responsible for the image. Change both instances of the string "canonical" to your developer id, retrieved with the `snapcraft whoami` command. ("xSfWKGdLoQBoQx88", in our example output). This links the image to your Ubuntu One account and ensures that only *you* can push image updates to devices using your model.

### timestamp


```json
   "timestamp": "2025-05-19T07:49:42+00:00",
```

This needs to be provided at the end of the process; we’ll come back to this.

###  snaps

````{tabs}

```{group-tab} AWS

~~~json
    "snaps": [
        {
            "name": "aws-gadget",
            "type": "gadget",
            "default-channel": "24/stable",
            "id": "mfDoEMcyOtXRpzrpIFuNDkJ2oAQWOquG"
        },
       ...
~~~

This section lists the snaps to be included in the image. **aws-gadget** (shown above), **aws-kernel**, **core24** and **snapd** are the four snaps required for a functioning Ubuntu Core image to be used on AWS.
```

```{group-tab} Azure

Content to be added
```

```{group-tab} GCP

Content to be added
```
````

Additional snaps are included using the same schema, with each snap requiring the following fields:
- `name`: simply the snap name.
- `type`: the [type of snap](/explanation/core-elements/snaps-in-ubuntu-core.md#types-of-snap). This is `app` for standard application snaps.
- `default-channel`: the [channel](https://snapcraft.io/docs/channels) to install the snap from.
- `id`: a unique snap identifier associated with every published snap. This is `snap-id` in the output from `snap info <snap-name>`.

### Complete model example

After finishing all your edits, the completed **my-model.json** text file should now contain the following:

````{tabs}

```{group-tab} AWS

~~~json
{
    "type": "model",
    "series": "16",
    "model": "aws-core-24-amd64",
    "architecture": "amd64",
    "authority-id": "canonical",
    "brand-id": "canonical",
    "timestamp": "2025-05-19T07:49:42+00:00",
    "base": "core24",
    "grade": "signed",
    "snaps": [
        {
            "name": "aws-gadget",
            "type": "gadget",
            "default-channel": "24/stable",
            "id": "mfDoEMcyOtXRpzrpIFuNDkJ2oAQWOquG"
        },
        {
            "name": "aws-kernel",
            "type": "kernel",
            "default-channel": "24/beta",
            "id": "pYVQrBcKmBa0mZ4CCN7ExT6jH8rY1hza"
        },
        {
            "name": "core24",
            "type": "base",
            "default-channel": "latest/stable",
            "id": "dwTAh7MZZ01zyriOZErqd1JynQLiOGvM"
        },
        {
            "name": "snapd",
            "type": "snapd",
            "default-channel": "latest/stable",
            "id": "PMrrV4ml8uWuEUDBT8dSGnKUYbevVhc4"
        }
    ]
}
~~~

```
```{group-tab} Azure

Content to be added
```

```{group-tab} GCP

Content to be added
```
````

After the file has been created, the next step is to sign it. See [Sign the model](/tutorials/build-a-public-cloud-image/sign-the-model) for further details.
