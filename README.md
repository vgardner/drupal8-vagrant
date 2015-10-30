Drupal Vagrant
--------------

Drupal Vagrant is a ready to go and fully configured development environment built
with VirtualBox, Vagrant, Linux and Chef Solo provisioner.

The main goal of the project is to provide easy to use, fully functional, highly
customizable and extendable Linux based environment for Drupal development.

Getting Started
---------------

Drupal Vagrant uses Chef Solo provisioner. It means that your environment is built from
the source code.

  1. Install VirtualBox
     https://www.virtualbox.org/wiki/Downloads

  2. Install Vagrant
     http://docs.vagrantup.com/v2/installation/index.html

  3. run ``git clone https://github.com/vgardner/drupal8-vagrant.git``

  4. To build your environment, in the root of the folder, run ``vagrant up``

     Vagrant will start to build your environment. You'll see green status
     messages while Chef is configuring the system.
  
  5. Add your the box's IP to your hosts file ``192.168.44.44 drupal8.dev drupal7.dev``
  
  6. To SSH into your Vagrant box, run ``vagrant ssh``
  
  7. Download or clone your Drupal 8/7 project into /var/www/drupal8 (or /var/www/drupal8)
     For a fresh D8 or 7 installation you can run:
      ```
      cd /var/www/drupal8
      git clone --branch 8.0.x http://git.drupal.org/project/drupal.git .
      drush @drupal8 si standard -y
      ```

  * Now you have ready to use virtual development server. By default 2 sites
are configured: Drupal 7 and Drupal 8. You can add new ones in config.json file
anytime.

  * Adjust configuration (optional)
     You can edit config.json file to adjust your settings. If you use VDD first
     time it's recommended to leave config.json as is. Sample config.json is
     just fine. By default Drupal 8 and Drupal 7 sites are configured.
     You can validate your JSON file at http://jsonlint.com/

Connect To Mysql
----------------
```
MySQL Host: 127.0.0.1
Username: root
Password: root
Port: 3306 (default)

SSH Host: 192.168.44.44
Username: vagrant
Password: vagrant
```

Vagrant basic Usage
-----------

In the root directory you can find 'data' directory. This directory
is visible (synchronized) to your virtual machine, so you can edit your project
locally with your favorite editor. You can safely destroy your Vagrant box, this
folder will not be altered.

Vagrant's basic commands (should be executed inside VDD directory):

  * ``$ vagrant ssh``
    SSH into virtual machine.

  * ``$ vagrant up``
    Start virtual machine.

  * ``$ vagrant halt``
    Halt virtual machine.

  * ``$ vagrant destroy``
    Destroy your virtual machine. Source code and content of data directory will
    remain unchangeable. VirtualBox machine instance will be destroyed only. You
    can build your machine again with 'vagrant up' command. The command is
    useful if you want to save disk space.

  * ``$ vagrant provision``
    Configure virtual machine after source code change.

  * ``$ vagrant reload``
    Reload virtual machine. Useful when you need to change network or
    synced folders settings.

Official Vagrant site has beautiful documentation.
http://docs.vagrantup.com/v2/

Cookbook inside chef/cookbooks/custom directory
-----------------------------------------------

  1. Take a look at vdd_example cookbook inside chef/cookbooks/custom directory.
  2. Create your own cookbook and place it inside chef/cookbooks/custom directory.
  3. Include your recipies in run_list in vdd.json role file inside chef/roles directory.

Remote cookbook using berkshelf
-------------------------------

  Berkshelf is great cookbook manager for Chef. It can automatically download
  cookbooks and their dependencies. Please, learn more at http://berkshelf.com/.

  1. Install berkshelf on your host machine.
  2. Include link to remote cookbooks' repository in Berksfile.
  3. Delete Berksfile.lock file and chef/cookbooks/berks directory.
  4. Run next command inside the root directory. It will download all dependencies.
    ``$ berks vendor chef/cookbooks/berks``

