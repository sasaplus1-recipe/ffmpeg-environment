# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = 'ubuntu/trusty64'

  config.vm.provider 'virtualbox' do |vb|
    vb.memory = '4096'
  end

  config.vm.synced_folder './share', '/home/vagrant/share', create: true

  config.vm.provision 'shell', privileged: false, inline: <<-SHELL
    # change to use JAIST mirror server
    if grep '//ftp.jaist.ac.jp/pub/Linux' /etc/apt/sources.list
    then
      echo 'already used JAIST mirror server'
    else
      sudo sed -i.bak -e 's|//archive.ubuntu.com|//ftp.jaist.ac.jp/pub/Linux|' /etc/apt/sources.list
    fi

    # update
    sudo apt-get update
    sudo apt-get --yes upgrade

    # download binary
    wget -q https://johnvansickle.com/ffmpeg/releases/ffmpeg-release-64bit-static.tar.xz

    # extract
    tar xvf ffmpeg-release-64bit-static.tar.xz

    # setup PATH
    echo "export PATH=$(find $HOME -maxdepth 1 -type d -name 'ffmpeg-*-64bit-static'):$PATH" >> $HOME/.bashrc
  SHELL
end
