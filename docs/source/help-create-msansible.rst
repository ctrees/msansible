=====================
help-create-msansible
=====================

Intent
  Step by Step help tutorial of how msansible-github_ repo and support template was created.
Success
  Replicate msansible-github_ pattern locally and generally be useful refernce.

Resources

#. msansible-local-docs_ local work in progress generated docs in ~/Demo/msansible/docs/build/html/index.html
#. msansible-github_  github repo for msansible
#. msansible-rtdocs_ readthedocs for msansible
#. galaxy-bertvv_ bertvv ansible galaxy
#. galaxy-geerlingguy_ geerlingguy ansible galaxy
#. Sphinx_ Sphinx is used to generate docs
#. rst-cheatsheet_ Restructured Text 

Manual Steps

#. Using the following
    #. node --version (v8.9.3)
    #. npm --version (5.6.0)
    #. yarn --version (1.3.2)
    #. python --version (Python 2.7.10)
    #. pip --version (pip 9.0.1 from /Library/Python/2.7/site-packages (python 2.7))
    #. vagrant --version (Vagrant 2.0.1)
    #. vboxmanage --version (5.2.4r119785)
#. Create msansible-github_ repo on https://github.com/ctrees
#. Clone the reference repos into ~/Demo
    #. git clone https://github.com/ctrees/msansible.git
    #. git clone https://github.com/2cld/readthedocsdemo.git
    #. git clone https://github.com/bertvv/ansible-skeleton.git
#. Setup docs in msansible
    #. Copy tree ~/Demo/readthedocsdemo/docs to ~/Demo/msansible/docs
    #. Edit ~/Demo/msansible/docs/source/conf.py
        #. Change rtddemo to msansible (lines 48,113,140,150,161,162)
        #. Commenent out line 95 (we are not going overwrite css)
        #. Update other things as you see fit
    #. Delete all files in ~/Demo/msansible/docs/source except the following
        #. conf.py
        #. help.rst
        #. index.rst
    #. Cleanup index.rst and help.rst
        #. cd ~/Demo/msansible/docs
        #. make html
        #. Edit errors until it builds clean
    #. Commit and push
        #. git status
        #. git add .
        #. git commit -m "Setup docs"
        #. git push
#. Setup msansible-rtdocs_ at https://readthedocs.org/
    #. Create account (I use ctrees) and login
    #. Establish a connection to your github account
    #. Go To ctrees -> My Projects ( https://readthedocs.org/dashboard/ )
    #. Import a Project (you should see all github projects you have commit access too)
    #. Select ctrees/msansible
    #. Click build
    #. Wait... doc site should show at msansible-rtdocs_ http://msansible.readthedocs.io/
#. Setup package.json .gitignore and README.md
    #. I use yarn as a build tool so I pulled in .gitignore and package.json
    #. Clean up package.json build tools
    #. cp ~/Demo/ansible-skeleton/README.md ~/Demo/msansible
    #. Clean up README.md
#. Setup ansible and Vagrant
    #. cp ~/Demo/ansible-skeleton/LICENSE ~/Demo/msansible
    #. cp ~/Demo/ansible-skeleton/Vagrantfile ~/Demo/msansible
    #. cp ~/Demo/ansible-skeleton/vagrant-hosts.yml ~/Demo/msansible
    #. mv ~/Demo/ansible-skeleton/test ~/Demo/msansible
    #. mv ~/Demo/ansible-skeleton/scripts ~/Demo/msansible
    #. mv ~/Demo/ansible-skeleton/ansible ~/Demo/msansible
#. Clean up
    #. LICENSE, README.md -> add maintainer of repo, Copyright and other reference instructions
    #. Vagrantfile -> Set "FORCE_LOCAL_RUN = true" so always runs ansible on a vm (not host)
    #. vagrant-hosts.yml -> set "box: bento/centos-7.4" (reuse the same box for both servers)
    #. add ~/Demo/ansible-skeleton/.gitignore to ~/Demo/msansible/.gitignore
#. Fire up cluster via vagrant
    #. vagrant up
    #. wait... (see help-create-msansible-vagrantup.txt for my output)
    #. When servers are up... test acces to them::

        catmini:msansible msops$ vagrant ssh srv001
        [vagrant@srv001 ~]$ ls
        [vagrant@srv001 ~]$ exit
        logout
        Connection to 127.0.0.1 closed.
        catmini:msansible msops$ vagrant ssh srv002
        [vagrant@srv002 ~]$ ls
        [vagrant@srv002 ~]$ exit
        logout
        Connection to 127.0.0.1 closed.
        catmini:msansible msops$ 

#. Looking at what just happened
    #. Should have the 2 servers srv001 and srv002 setup in the vagrant-hosts.yml file
    #. Each are attached to different networks
        #. srv001 -> 192.168.56.10 (as specified in vagrant-hosts.yml)
        #. srv002 -> 172.28.128.3 (default via dhcp on vboxnet1)
    #. Each attached the specified shares
        #. srv001 -> /vagrant/ -> ~/Demo/msansible/  (default)
        #. srv002 -> /vagrant/ -> ~/Demo/msansible/  (default)
        #. srv002 ->[vagrant@srv002 ~]$ ls /tmp/test/ (runbats.sh)
        #. srv002 ->[vagrant@srv002 ~]$ ls /var/www/html
    #. Both are bento/centos-7.4 boxes from https://vagrantcloud.com/bento/centos-7.4
        #. srv001 -> Setting the name of the VM: msansible_srv001_1516894292045_38682
        #. srv002 -> Setting the name of the VM: msansible_srv002_1516894379718_80483
    #. Since we Set "FORCE_LOCAL_RUN = true" the vagrant shell issues ansible provision command::

          ==> srv001: Running provisioner: shell...
          srv001: Running: /var/folders/r3/7__qq0zj6mq_27889bsn9rmm0000gv/T/vagrant-shell20180125-1060-rbgk7n.sh
          srv001: >>> Running Ansible playbook /vagrant/ansible/site.yml locally on host srv001.
          srv001: >>> CentOS: installing Ansible from the EPEL repository

    #. This triggers the scripts/run-playbook-locally.sh which detects ansible is not installed and installs it
        #. see line 67 in ~/Demo/msansible/scripts/run-playbook-locally.sh
        #. Later we will setup a special ansible msops vm for running commands
        #. If you look at the output... no ansible actions were taken as we have not roles in the sites.yml
#. Now lets put in a basic webserver on srv002 which is why we mapped /var/www/html


Video Track

#. tc_ Show Video


Video 

.. raw:: html

    <div style="position: relative; padding-bottom: 5.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
    <span>Put youtube embedded code here</span>
    </div>

.. Video time code (tc) links

.. _tc: https://youtu.be/

.. document includes

.. include:: include-msansible-common.rst



