# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "bento/ubuntu-16.04"
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.memory = "3072"

    vb.customize [
      "modifyvm", :id,
      "--vram", "256", # フルスクリーンモード用
      "--clipboard", "bidirectional", # クリップボード共有
      "--draganddrop", "bidirectional", # ドラッグアンドドロップ
      "--cpus", "3",
      "--ioapic", "on" # I/O APICを有効化
    ]
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get upgrade

    apt-get install -y ubuntu-desktop


    reboot
  SHELL

  # 起動時にファイル転送しておきたい場合は以下を記載
  # config.vm.provision "file", source: "転送元", destination: "転送先"
end