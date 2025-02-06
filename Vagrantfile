Vagrant.configure("2") do |config|
  config.vm.box = "perk/ubuntu-2204-arm64"
  # config.vm.provider "qemu" do |qemu|
  config.vm.provider "libvirt" do |libvirt|
    libvirt.qemu_use_session = false  # Ensure it runs as a system-wide VM
  end
  config.vm.network "forwarded_port", guest: 8000, host: 8000, auto_correct: true

  config.vm.synced_folder "/Users/hyunsoocho/Documents/Python-Rest-API", "/vagrant", type: "rsync", rsync__auto: true, rsync__reverse: true

    # set the port of your preference
    # qemu.ssh_port = "8000"
    config.vm.provision "shell", inline: <<-SHELL
      systemctl disable apt-daily.service
      systemctl disable apt-daily.timer

      sudo apt-get update
      sudo apt-get install -y python3-venv zip
      touch /home/vagrant/.bash_aliases
      if ! grep -q PYTHON_ALIAS_ADDED /home/vagrant/.bash_aliases; then
        echo "# PYTHON_ALIAS_ADDED" >> /home/vagrant/.bash_aliases
        echo "alias python='python3'" >> /home/vagrant/.bash_aliases
      fi
    SHELL
  end
# end
