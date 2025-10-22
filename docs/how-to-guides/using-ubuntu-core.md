(how-to-guides-using-ubuntu-core)=
# Using Ubuntu Core

Ubuntu Core and its applications run within a confined and transaction-based environment. This provides the robustness and security that makes Ubuntu Core ideal for embedded device deployment, but it also requires a different approach from classic Ubuntu systems. 

Application management, system configuration and update schedules in Ubuntu Core are managed by *snapd*, the snap packaging daemon. Snap features are explained comprehensively in the [Snap documentation](https://snapcraft.io/docs), while our [Ubuntu Core documentation](https://documentation.ubuntu.com/core/) handles the elements of the _snap_ ecosystem that are specifically applicable to Ubuntu Core.

```{admonition} Create your own images
:class: tip
While Ubuntu Core is primarily intended for developers to build custom images tailored for their application and targeted hardware, this page is a great place to start after you've just installed [pre-built Ubuntu Core images](/how-to-guides/index/) and want to learn a few of the basic principles quickly.
```

## Quickstart project - Install LXD

Once you have installed a pre-built image on any cloud and logged in to the instance using SSH, you can try out any application that is available as a classic snap. You can install a snap using:

```bash
sudo snap install $SNAP
```
where $SNAP should be replaced with the specific snap that you are interested in trying out. Once installed, you can use and test the application as you would usually do. 

An an example you can try out the LXD snap using the following commands.

### Install LXD

```bash
ubuntu@ip-172-31-46-212:~$ sudo -i

root@ip-172-31-46-212:~# snap install lxd
lxd (5.21/stable) 5.21.4-8b5e998 from Canonical✓ installed
```

### Initialize LXD
```bash
root@ip-172-31-46-212:~# lxd init
Would you like to use LXD clustering? (yes/no) [default=no]: 
Do you want to configure a new storage pool? (yes/no) [default=yes]: 
Name of the new storage pool [default=default]: 
Name of the storage backend to use (zfs, dir, powerflex, btrfs, ceph, lvm, pure) [default=zfs]: 
Create a new ZFS pool? (yes/no) [default=yes]: 
Would you like to use an existing empty block device (e.g. a disk or partition)? (yes/no) [default=no]: 
Size in GiB of the new loop device (1GiB minimum) [default=5GiB]: 
Would you like to connect to a MAAS server? (yes/no) [default=no]: 
Would you like to create a new local network bridge? (yes/no) [default=yes]: 
What should the new bridge be called? [default=lxdbr0]: 
What IPv4 address should be used? (CIDR subnet notation, “auto” or “none”) [default=auto]: 
What IPv6 address should be used? (CIDR subnet notation, “auto” or “none”) [default=auto]: 
Would you like the LXD server to be available over the network? (yes/no) [default=no]: 
Would you like stale cached images to be updated automatically? (yes/no) [default=yes]: 
Would you like a YAML "lxd init" preseed to be printed? (yes/no) [default=no]: 
```

### Use LXC to launch an instance

Launch an ubuntu instance using LXC:

```bash
root@ip-172-31-46-212:~# lxc launch ubuntu:noble test
Launching test
```

Access the shell prompt of the new instance and finally logout:

```bash
root@ip-172-31-46-212:~# lxc shell test
root@test:~# ls

root@test:~# 
logout
root@ip-172-31-46-212:~#
```

 

## Snap management

Some common commands used to list and manage your snaps are explained below.

### List snaps

You can list which snaps are installed on your Ubuntu Core system with:

```bash
snap list
```

The default state for an Ubuntu Core image, including which snaps it includes, is defined by its [model assertion](https://documentation.ubuntu.com/core/reference/assertions/model/). You can view the one being used on the current system with:

```bash
snap known model
```

For more details on which snaps are included with Ubuntu Core, see [Snaps in Ubuntu Core](https://documentation.ubuntu.com/core/explanation/core-elements/snaps-in-ubuntu-core/).


### List snapped services

If your snap runs specific services in the background, these snapped services can be viewed with:

```bash
$ snap services
```

The `snap stop <service-name>`, `snap start <service-name>` and `snap restart <service-name>` commands can all be used to start and stop services.  If a service offers a reload function, usually to reload a configuration file without requiring a full restart, this can be added to `restart` with the `--reload` argument.

Similarly, services can be stopped from starting automatically, and re-enabled, with the `snap disable <service-name>` and `snap enable <service-name>` commands respectively.

For more information on services, take a look at [Services and daemons](https://snapcraft.io/docs/services-and-daemons).

### Remove snaps
Any snaps you manually install can be removed with:

```bash
snap remove $SNAP
```
where $SNAP is to be replaced with the name of the snap to be removed.


## Next steps

The snap command includes comprehensive help output. To see this, type `snap help` followed by the command. The output will often include additional arguments that can be useful. Autocompletion can also help when tying snap commands, both to complete a command itself, and also to complete the names of snaps or interfaces. Type `snap` followed by a space and then the tab key to see the list of all possible commands, for instance.

For more information on how to work with snaps, including how to make data snapshots, how to install specific revisions, see the [Snap Documentation ](https://snapcraft.io/docs/). 

To learn how to create your own custom image for a cloud, see our guide for [Building an image for public clouds](/tutorials/build-a-public-cloud-image/index) guide.

