# Creating a custom Vagrant box

Rolling with a default Vagrant box like centos/7 and repeatedly building
clusters can take some time, as each time you destroy -f and up, you're
likely to be running a full yum update, adding yum repos and installing
other packages.  VirtualBox doesn't do parallel provisioning so this is
like watching paint dry as data is pulled down from the Internets.

An easy way to speed up the process is extend the base box to include 
some of the steps you'd be provisioning.

You can also reduce time by having the VirtualBox client additions updated. 
One more step that doesn't need reproducing on each deployment.

```
mkdir centos7_custom_box
cd centos7_custom_box
vagrant init centos/7
vagrant up
vagrant ssh
sudo yum update
sudo yum clean all
ctrl +d
vagrant package --output centos7_updated.box
vagrant box add centos7_updated.box --name centos7_updated
vagrant box list
vagrant halt
```

Now edit the Vagrantfile of any project you wish to use it in.
