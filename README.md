# vagrant-learning

Examples for this projet are taken from the Book:  
Vagrant Up and Running  
By: Mitchell Hashimoto  
Publisher: O'Reilly, 2013


$ mkdir test  
$ cd test  
$ vagrant init precise64 http://files.vagrantup.com/precise64.box  
$ vagrant up
$ vagrant ssh  
$ vagrant destroy
$ rm *    
$ cd ..  
$ rmdir test

Create a projet in GitHub vagrant-learning  
$ cd ~/workspace
$ git clone https://github.com/jffalcao/vagrant-learning.git
$ cd vagrant-learning
$ $ vagrant init precise64 http://files.vagrantup.com/precise64.box  
$ vagrant up
$ vagrant ssh  

$ vagrant status  
$ vagrant ssh  
vagrant@precise64:~$ ls /vagrant/  
vagrant@precise64:~$ exit  

Example of port forwarding Host:8080 to guest:80 using SimpleHTTPServer

$ vagrant ssh  
vagrant@precise64:~$ cd /vagrant  
vagrant@precise64:/vagrant$ sudo python -m SimpleHTTPServer 80  
<ctrl><c>
vagrant@precise64:/vagrant$ exit

$ vagrant suspend  
$ vagrant status  
$ vagrant halt [--force]  
$ vagrant status  
$ vagrant destroy [--force]  


Vagrant configures a shared folder on the linux machine which corresponds to the host directory where the VagrantFile is.

To simplify development using the host tools we will create a symbolic link to workspace folder using the original target /var/www for the web server.

vagrant@precise64:~$ sudo rm -rf /var/www  
vagrant@precise64:~$ sudo ln -fs /vagrant /var/www

Create an index.html file in the workspace directory with the following text.

```
<strong>Hello</strong>
```

**Page 45: Using Scripts**
Installing Apache HTTP Server and redirecting /var/wwww to our workspace using Scripts

Create a **provision.sh** in the workspace directory

```
#!/usr/bin/env bash
echo "Installing Apache and setting it up..."
apt-get update >/dev/null 2>&1
apt-get install -y apache2 >/dev/null 2>&1
rm -rf /var/www
ln -fs /vagrant /var/www
```

Modify the **VagrantFile**.

```
Vagrant.configure(2) do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.provision "shell", path: "provision.sh"
end
```

$ vagrant destroy
$ vagrant up

Modify index.html to read Hello from shell script provisioning

**Page 45: Using Chef**
$ vagrant destroy
In the VagrantFile

comment the shell provisioning
config.vm.provision "chef_solo", run_list: ["vagrant_book"]

From the workspace of the project create  

$ mkdir cookbooks/vagrant_book/recipes/default.rb

**default.rb** file:

```
execute "apt-get update"
package "apache2"
execute "rm -rf /var/www"
link "/var/www" do
  to "/vagrant"
end

```


$ vagrant up

Modify index.html to read Hello from Chef Solo provisioning
