Accumulo Stackscript
====================

2013-May-10 The driver-1.4.2.sh script seems to be working perfectly to install hadoop, zookeeper, and accumulo into ~/accumulo_home/bin. 


2013-May-10 The scripts that pull trunk are not working correctly. The symptom is that the Accumulo monitor page is not responding.

Provides stackscripts to install hadoop, zookeeper and accumulo on a Linode server.

I wanted a way to test the very latest Accumulo code. I could not use any of my existing systems because they were multi-use boxes. So I wrote a Stackscript in order to prepare a Linode server. Note that this script pulls a few files from my affy.com server for simplicity.

Users: hadoop, zookeeper, accumulo
Password: password

This stackscript downloads, installs and configures hadoop, zookeeper, and accumulo.

Step one is to create your own stackscript. Mine was called "InitializeAccumulo". The idea is that the starter script pulls the actual script from some server so that you don't need to deal with the 'Manage Stackscript' interface. The starter script is:

```bash
#!/bin/bash
apt-get -y install git
git clone https://github.com/medined/accumulo_stackscript.git
cd accumulo_stackscript
./stackscript
```

After the Linode server boots, it will take about 10 minutes to run this script. Then you can use ssh to login as the 'accumulo' user (the password is 'password'). Run two more commands and your server is completely setup.

```bash
accumulo init --clear-instance-name --instance-name instance --password secret
cd /usr/local/accumulo
bin/start-all.sh
```

Screen
======

http://library.linode.com/linux-tools/utilities/screen - the Stackscript installs screen which is useful so that you can always connect to the same session. Type Ctl-A+d in order to detach the session. Use screen -r to reconnect.


Git
===

Making a tag.

```bash
git tag -a 2012_DEC_14 -m "with hadoop 0.20.2"
git show 2012_DEC_14
git describe --tags
# make a file change.
git push --tags
```

