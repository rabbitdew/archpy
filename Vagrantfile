# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "archlinux/archlinux"
   config.vm.provision "shell", inline: <<-SHELL
     set -x
     sed -i 's/#LLMNR=yes/LLMNR=no/' /etc/systemd/resolved.conf
     systemctl daemon-reload
     systemctl restart systemd-resolved
     grep -A1 'United States' /etc/pacman.d/mirrorlist | sed 's/--//' > /tmp/mirrorlist
     mv /tmp/mirrorlist /etc/pacman.d/mirrorlist
     pacman -Sy
     pacman -Su --noconfirm extra/python python-pip git tmux vim-jedi vim
     su -c 'pip3 install --user flask ipython' vagrant
     su -c 'echo export PATH=${PATH}:~vagrant/.local/bin' >> /etc/environment
     printf 'set nu
set list
syntax on
filetype indent plugin on
autocmd FileType yaml setlocal ts=2 sts=2 sw=2 expandtab' > /home/vagrant/.vimrc
   SHELL
end
