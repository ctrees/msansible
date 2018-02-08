======================
help-export-confluence
======================

Intent
  Step by Step help tutorial of how export msansible-github_ repo documentation to a Atlassian Confluence Server.
Success
  Push msansible-github_ documentation to an Atlassian Confluence Server.

Resources

#. msansible-local-docs_ local work in progress generated docs in ~/Demo/msansible/docs/build/html/index.html
#. msansible-github_  github repo for msansible
#. msansible-rtdocs_ readthedocs for msansible
#. galaxy-bertvv_ bertvv ansible galaxy
#. galaxy-geerlingguy_ geerlingguy ansible galaxy
#. Sphinx_ Sphinx is used to generate docs
#. rst-cheatsheet_ Restructured Text
#. ConfluenceBuilder_ Export documentation to Confluence
#. sphinxcontrib-confluencebuilder_ github for ConfluenceBuilder_

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
#. Generate docs for msansible (this builds docs in the local directory structure THIS IS Optional)
    #. cd ~/Demo/msansible/docs
    #. make html
    #. open build/html/index.html
    #. Verify documentation build
#. Fire up the controlled enviroment build system
    #. cd ~/Demo/msansible
    #. vagrant up
        #. box should be pulled down
        #. ansible should configure a vmbox called docs
    #. vagrant status
    #. vagrant ssh docs ::

        catmini:msansible msops$ vagrant ssh docs
        Welcome to docs..
        enp0s3     : 10.0.2.15         fe80::9869:415b:fc91:2aa8/64  
        enp0s8     : 172.28.128.3      fe80::a00:27ff:fe1b:19d0/64  
        [vagrant@docs ~]$ 
    
    #. exit
    #. ssh msops@172.28.128.3 ::

        catmini:msansible msops$ ssh msops@172.28.128.3
        Last login: Wed Feb  7 22:51:06 2018 from 172.28.128.1
        Welcome to docs..
        enp0s3     : 10.0.2.15         fe80::9869:415b:fc91:2aa8/64  
        enp0s8     : 172.28.128.3      fe80::a00:27ff:fe1b:19d0/64  
        [msops@docs ~]$ python -m sphinxcontrib.confluencebuilder --version
        sphinxcontrib.confluencebuilder 0.8
        [msops@docs ~]$ 

#. Setup conf.py to add confluencebuilder_ 
    #. Add the extension to conf.py ::

        extensions = ['sphinxcontrib.confluencebuilder']

    #. Add the target confluence server to conf.py ::

        confluence_publish = True
        confluence_space_name = 'TEST'
        confluence_parent_page = 'Documentation'
        confluence_server_url = 'https://intranet-wiki.example.com'
        confluence_server_user = 'username'
        confluence_server_pass = 'password'
    
    #. Publish to site ::

        make confluence
            (or)
        sphinx-build -b confluence . _build/confluence
            (or)
        python -m sphinx -b confluence . _build/confluence

    #. Verify site by browsing https://intranet-wiki.example.com/pages/viewpage.action?title=TEST&spaceKey=Documentation

#. The END ?

.. document includes

.. include:: include-msansible-common.rst