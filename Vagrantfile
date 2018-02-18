Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.hostname = "ntc"
  config.vm.synced_folder ".", "/vagrant", type: "nfs"
  config.vm.network "private_network", ip: "192.168.33.95"
  config.vm.network :forwarded_port, guest: 3389, host: 5389
  config.vm.provider "virtualbox" do |v|
  	v.memory = 4096
  	v.cpus = 2
  end
  config.vm.provision "shell", inline: <<-SHELL
 	sudo yum -y groupinstall "GNOME Desktop"
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
  sudo rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-1.el7.nux.noarch.rpm
  sudo wget -O /etc/yum.repos.d/xrdp.repo https://gist.githubusercontent.com/dancwilliams/f048ba1deb506bd08dfe202f32996e33/raw/83f9a741aaefd3899975464e740463f0dd3c6396/xrdp.repo
  sudo yum -y install xrdp tigervnc-server
  sudo systemctl start xrdp.service
  sudo systemctl enable xrdp.service
 	sudo systemctl set-default graphical.target
 	sudo systemctl start graphical.target
  sudo rpm -v --import https://download.sublimetext.com/sublimehq-rpm-pub.gpg
  sudo yum-config-manager --add-repo https://download.sublimetext.com/rpm/stable/x86_64/sublime-text.repo
  sudo yum -y install sublime-text
  sudo yum -y install shutter
  sudo yum -y install pip
  sudo yum -y install sshpass
  yes w | sudo pip install --upgrade pip
  yes w | sudo pip install ansible
  sudo useradd ntc
  echo "ntc:ntc123"|sudo chpasswd
  sudo gpasswd -a ntc wheel
  SHELL
end