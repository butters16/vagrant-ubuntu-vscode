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

  config.vm.provision "shell", inline: <<-INSTALL_CHROME
    wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - 
    sh -c 'echo "deb https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list'
    apt-get update
    apt-get install -y google-chrome-stable
  INSTALL_CHROME

  config.vm.provision "shell", inline: <<-INSTALL_NODEJS_AND_NPM
    curl -sL https://deb.nodesource.com/setup_6.x | bash -
    apt-get install -y nodejs build-essential
  INSTALL_NODEJS_AND_NPM

  config.vm.provision "shell", inline: <<-INSTALL_GIT
    apt-get update
    apt-get install -y git
  INSTALL_GIT

  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.provision "shell", privileged: false, inline: <<-INSTALL_ANGULAR2_SEED
    git clone https://github.com/angular/angular2-seed.git
    cd angular2-seed
    npm install
    sed -i 's/--port 3000/--port 3000 --host 0.0.0.0/' package.json
  INSTALL_ANGULAR2_SEED
end
