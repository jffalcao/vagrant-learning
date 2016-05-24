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
