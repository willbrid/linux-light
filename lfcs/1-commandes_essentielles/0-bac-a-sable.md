# Bac à sable

Nous allons mettre en place notre bac à sable avec vagrant sous virtualbox 7.0.

### Installation de Rocky Linux 8

```
cd ~
mkdir rocky
cd rocky
wget https://download.virtualbox.org/virtualbox/7.0.12/VBoxGuestAdditions_7.0.12.iso
```

```
vi Vagrantfile
```

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vbguest.auto_update = false
  config.vbguest.no_remote = true
  config.vbguest.iso_path = "./VBoxGuestAdditions_7.0.12.iso"

  # General Vagrant VM configuration.
  config.vm.box = "willbrid/rockylinux8"
  config.vm.box_version = "0.0.2"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.provider :virtualbox do |v|
    v.memory = 4096
    v.cpus = 3
    v.linked_clone = true
  end
  config.vm.disk :disk, name: "storage1", size: "5GB"
  config.vm.disk :disk, name: "storage2", size: "3GB"

  # Rocky Server
  config.vm.define "rocky-server" do |srv|
    srv.vm.hostname = "rocky-server"
    srv.vm.network :private_network, ip: "192.168.56.110"
  end
end
```

```
vagrant up
```

### Installation de Ubuntu 20.04

```
cd ~
mkdir ubuntu
cd ubuntu
wget https://download.virtualbox.org/virtualbox/7.0.12/VBoxGuestAdditions_7.0.12.iso
```

```
vi Vagrantfile
```

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vbguest.auto_update = false
  config.vbguest.no_remote = true
  config.vbguest.iso_path = "./VBoxGuestAdditions_7.0.12.iso"

  # General Vagrant VM configuration.
  config.vm.box = "geerlingguy/ubuntu2004"
  config.vm.box_version = "1.0.4"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.provider :virtualbox do |v|
    v.memory = 4096
    v.cpus = 3
    v.linked_clone = true
  end
  config.vm.disk :disk, name: "storage1", size: "5GB"
  config.vm.disk :disk, name: "storage2", size: "3GB"

  # Ubuntu Server
  config.vm.define "ubuntu-server" do |srv|
    srv.vm.hostname = "ubuntu-server"
    srv.vm.network :private_network, ip: "192.168.56.111"
  end
end
```

```
vagrant up
```