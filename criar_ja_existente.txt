Vagrant.configure("2") do |config|
  # especifica a box que será utilizada
  config.vm.box = "hashicorp/bionic64"
  config.vm.box_url = "https://vagrantcloud.com/hashicorp/bionic64"

  # eedireciona a porta 80 da VM para a porta 8080 no host
  config.vm.network "forwarded_port", guest: 80, host: 8080

  # (Opcional) Provisione um servidor HTTP Apache automaticamente
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y apache2
    sudo systemctl start apache2
  SHELL
end
