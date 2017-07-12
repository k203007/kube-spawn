# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV["TERM"] = "xterm-256color"
ENV["LC_ALL"] = "en_US.UTF-8"

Vagrant.configure("2") do |config|
  config.vm.box = "jhcook/fedora26"
  config.vm.provision "shell", inline: "dnf install -y btrfs-progs docker git go kubernetes strace tmux"
  # config.vm.box = "ubuntu/zesty64"
  # config.vm.provision "shell", inline: "DEBIAN_FRONTEND=noninteractive apt-get install -y golang git docker.io systemd-container tmux"

  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder ".", "/home/vagrant/go/src/github.com/kinvolk/kube-spawn", create: true, type: "rsync"

  config.vbguest.auto_update = false
  config.vm.provider :virtualbox do |vb|
      vb.check_guest_additions = false
      vb.functional_vboxsf = false
      vb.customize ["modifyvm", :id, "--memory", "4094"]
      vb.customize ["modifyvm", :id, "--cpus", "1"]
  end

  config.vm.provision "shell", env: {"GOPATH" => "/home/vagrant/go"}, privileged: false, path: "scripts/vagrant-setup-env.sh"
  config.vm.provision "shell", path: "scripts/vagrant-mod-env.sh"
end
