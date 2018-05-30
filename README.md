# Ruby on Rails and PosgreSQL 10 Vagrant Box Provisioned with Ansible

Getting a Ruby on Rails develpment environment running with PostgreSQL shouldn't be that hard.

This project makes the assumptions that you have [Vagrant](https://www.vagrantup.com/), [VirtualBox](https://www.virtualbox.org/), and [Ansible](https://docs.ansible.com/ansible/latest/) installed. You don't need to know how to use Ansible, but it needs to be installed to provision the Vagrant box.

## Dependencies
* [Vagrant](https://www.vagrantup.com/)
* [VirtualBox](https://www.virtualbox.org/)
* [Ansible](https://docs.ansible.com/ansible/latest/)

## Getting Started
1. clone this repository
2. cd ./vagrant-rails-postgres-with-ansible
3. vagrant up (this will take some time to download the base vagrant box andprovision)
4. vagrant ssh
5. cd /vagrant/projects/
6. rails new your_project
7. cd ./your_project
8. bundle exec rails s
9. from your browser, go to http://localhost:3000

## Details

By now, you should have a Ruby on Rails application running port 3000. The magic happens because we told vagrant to map the VM's port 3000 to your computer's port 3000. If you have something else running on port 3000, then you might have a conflict. If you want to fire up your application on a different port, you'll need to add the mapping to the Vagrantfile and then run `vagrant reload`.

The VM that is created is based on Ubuntu 18.04 pulled from [Ubuntu Cloud Images](https://cloud-images.ubuntu.com/). [rbenv](https://github.com/rbenv/rbenv) is setup and by default ruby 2.5.1 is installed. The gems for the most recent versiosn of bundlder and rails are installed by default.

Once you have run vagrant ssh and are inside the VM, you can go to /vagrant/projects/your_project and run `rake db:create` and/or `rake db:migrate`. This works flawlessly as the vagrant user is set up with CREATEDB rights to the database server that is running locally on the VM.

You will notice that a projects folder shows up on your host machine in /path/to/vagrant-rails-postgres-with-ansible. This folder will not be committed to this repository. This allows you to manage your rails projects in their own git repositories. The project folder is created when the VM is provisioned and exists because /vagrant on the VM maps to this project's directory on the your host computer.
