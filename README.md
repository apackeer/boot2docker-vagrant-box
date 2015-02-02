# boot2docker Vagrant Box

This repository contains the scripts necessary to create a Vagrant-compatible
[boot2docker](https://github.com/steeve/boot2docker) box. If you work solely
with Docker, this box lets you keep your Vagrant workflow and work in the
most minimal Docker environment possible.

## Usage

The box is available on
[Hashicorp Atlas](https://atlas.hashicorp.com/apackeer/boxes/boot2docker), making
it very easy to use it:

    $ vagrant init apackeer/boot2docker
    $ vagrant up --provider=vmware_fusion

If you want the actual box file, you can download it from the
[releases page](https://github.com/apackeer/boot2docker-vagrant-box/releases).

On OS X, to use the docker client, follow the directions here:
http://docs.docker.io/installation/mac/#docker-os-x-client (you'll need to
export `DOCKER_HOST`). You should then be able to to run `docker version` from
the host.

![Vagrant Up Boot2Docker](https://raw.github.com/apackeer/boot2docker-vagrant-box/master/readme_image.gif)

## Building the Box

If you want to recreate the box, rather than using the binary, then
you can use the scripts and Packer template within this repository to
do so in seconds.

To build the box, first install the following prerequisites:

  * [Packer](http://www.packer.io) (at least version 0.5.1)
  * [VirtualBox](http://www.virtualbox.org) (at least version 4.3), VMware, or Parallels
  * [Vagrant](http://www.vagrantup.com)

Then follow the steps:

```
$ vagrant up --provider=vmware_fusion
...
$ vagrant ssh -c 'cd /vagrant && sudo ./build-iso.sh'
...
$ vagrant destroy --force
...
$ packer build --only vmware-iso template.json
...
```

You can restrict only VirtualBox, VMware, or Parallels by specifying the `-only` flag
to Packer.
