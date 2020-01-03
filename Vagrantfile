# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-16.04"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.memory = "3072"

    vb.customize [
      "modifyvm", :id,
      "--vram", "256",
      "--clipboard-mode", "bidirectional",
      "--draganddrop", "bidirectional",
      "--cpus", "2",
      "--ioapic", "on"
    ]
    
    config.vm.provision "shell", inline: <<-SHELL
      sudo wget -q https://www.ubuntulinux.jp/ubuntu-ja-archive-keyring.gpg -O- | sudo apt-key add -
      sudo wget -q https://www.ubuntulinux.jp/ubuntu-jp-ppa-keyring.gpg -O- | sudo apt-key add -
      sudo wget https://www.ubuntulinux.jp/sources.list.d/xenial.list -O /etc/apt/sources.list.d/ubuntu-ja.list
      sudo apt -y update
      sudo apt-get -y upgrade
      sudo apt-get -y install ubuntu-defaults-ja
      sudo apt-get -y install ubuntu-desktop
      sudo apt -y install openjdk-8-jdk
      sudo curl -s "https://get.sdkman.io" | bash
      source /home/vagrant/.sdkman/bin/sdkman-init.sh
      sdk install gradle
      sudo wget https://download.springsource.com/release/STS4/4.5.0.RELEASE/dist/e4.14/spring-tool-suite-4-4.5.0.RELEASE-e4.14.0-linux.gtk.x86_64.tar.gz
      tar xvzf spring-tool-suite-4-4.5.0.RELEASE-e4.14.0-linux.gtk.x86_64.tar.gz
      sudo wget https://projectlombok.org/downloads/lombok.jar
      sudo chmod 775 lombok.jar
      git config --global user.name user1
      git config --global user.email user1@vagrant.demo
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
      sudo apt-key fingerprint 0EBFCD88
      sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
      sudo apt-get update
      sudo apt-get -y install docker-ce
      sudo groupadd docker
      sudo usermod -aG docker $USER
      sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
      sudo chmod +x /usr/local/bin/docker-compose
      sudo curl -L https://raw.githubusercontent.com/docker/compose/1.25.0/contrib/completion/bash/docker-compose -o /etc/bash_completion.d/docker-compose
    SHELL
  end
end