# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.ssh.forward_x11 = true
  code_deb = "arbitrary_name.deb"
  config.vm.provision "shell", inline: <<-INSTALL_VSCODE
    apt-get update
    apt-get install -y libnotify4 libnss3 x11-apps libgtk2.0-0 libxss1 libgconf-2-4 libasound2
    curl -L https://go.microsoft.com/fwlink/?LinkID=760868 -o #{code_deb}
    dpkg -i #{code_deb}
    rm #{code_deb}
  INSTALL_VSCODE
end
