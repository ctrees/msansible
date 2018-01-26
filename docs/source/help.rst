Need Help
=========

Ping ctrees_at_mailserviceslc_dot_com


=================
msansible Install
=================

Quick Start::

 $ node --version
 v8.9.3
 $ cd ~/Demo
 $ git clone https://github.com/ctrees/msansible.git
 $ cd msansible
 $ yarn install
 $ yarn run docs

=================
Build ReadTheDocs
=================

To edit and update the readthedocs::

 $ cd ~/Code
 $ git clone https://github.com/ctrees/msansible.git
 $ cd msansible/docs
 $ make html
 $ open build/html/index.html
 $ vi source/help.rst
 $ make html
 $ open build/html/index.html
 (verify changes)
 $ make clean
 $ cd ~/Demo/msansible
 $ git add .
 $ git commit -m "Update documents"
 $ git push
 (wait some min for webhooks to hit)
 $ open http://msansible.readthedocs.io/en/latest/
 (inspect changes)

==============
Sphinx Install
==============

To install Sphinx via pip ( pip-install_ ) to make documentation::

 $ python --version
 Python 2.7.10
 $ python get-pip.py
 $ pip --version
 pip 9.0.1 from /Library/Python/2.7/site-packages (python 2.7)
 $ sudo pip install --ignore-installed Sphinx

==========
References
==========

 + github repo msansible-github_
 + ReadTheDocs msansible-rtdocs_
 + Docs created via Sphinx_ using doc-name.rst
 + rst-cheatsheet_ Cheatsheet for rst
 + python-install_
 + pip-install_ 
 + ansible-install_
 + node-install_
 + yarn_ is a new npm (node package manager)

.. document includes

.. include:: include-msansible-common.rst
