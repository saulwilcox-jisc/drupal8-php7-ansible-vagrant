# drupal-bootstrap
Quick-start for Drupal sites: bootstrap and provision a development VM with Ansible and Vagrant, using a Debian 8 box.

You will need:
- Ansible (2.3.0.0)
- Virtualbox (5.1)
- Vagrant (1.9.5)

Example Install on Mac using homebrew:
brew cask install virtualbox
brew cask install vagrant
brew install ansible

First get a vagrant base box:
vagrant box add --name debian-jessie https://github.com/kraksoft/vagrant-box-debian/releases/download/8.1.0/debian-8.1.0-amd64.box

Navigate to your home folder and try the following:

$ vagrant init

$ vagrant up --provision

This will take a moment while all the relevant packages are installed.

For a terminal inside the VM:

$ vagrant ssh

In the Vagrantfile you'll see that the VM has a fixed IP of 88.88.88.8.
Typically this would be mapped to something more meaningful in your /etc/hosts file.

You may need to run the drupal install script if you don't have a complete sites folder already.
Then clone the codebase and import a database dump.

When that's all done, the usual 'drush cr all' command should give you a working site.

Troubleshooting shared folders:
- NFS works best and is recommended.
- Try using the rsync folder type in the Vagrantfile instead of VFS:
  config.vm.synced_folder "~/project", "/var/www", type: 'rsync'
  Then use 'vagrant rsync auto' to watch the files and sync as they change.

You can keep your VirtualBox Guest additions up to date automatically using the following plugin:
vagrant plugin install vagrant-vbguest
