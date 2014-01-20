Sgoettschkes/openshift-php54
============================

This is a sample repository to get php 5.4 running on openshift. It's a 
work in progress!

More information about this project: tbd

More information about openshift: https://openshift.redhat.com/

What's inside
-------------

The misc/install.sh script installs:

* Apache 2.4.7
* PHP 5.4.24 (updated with zip, zlib and GD modules)

It configures apache to have the diy folder as the document root. It also
uses the php.ini-development from the php archive and moves it into the 
correct folder.

The script does not remove the source files, so you can easily recompile 
Apache or PHP. Have a look at the shell script to see with which options
both were compiled the first time.

The misc/httpconf.py script takes the httpd.conf from misc/templates and
replaces some variables with the actual folder pathes (because these 
depend on the application, they cannot be hardcoded). It then copies
the file into the apache conf folder.

Usage
-----

To get PHP 5.4 working at OpenShift, you have to do the following:

1. Create a new Openshift "Do-It-Yourself" application
2. Clone this repository
3. Add a new remote "openshift" (You can find the URL to your git repository
   on the Openshift application page)
4. Run `git push --force "openshift" master:master`
5. SSH into your gear
6. `nohup $OPENSHIFT_REPO_DIR/misc/install.sh > $OPENSHIFT_DIY_LOG_DIR/install.log`
7. Wait (This may take at least an hour)
8. Open http://appname-namespace.rhcloud.com/phpinfo.php to verify running 
   apache
9. You can remove the misc content


Useful Commands
----------------

1. Server can be started using command ` $OPENSHIFT_HOMEDIR/app-root/runtime/srv/httpd/bin/apachectl start > $OPENSHIFT_DIY_LOG_DIR/server.log 2>&1 &`

To Append new PHP location to System path 
----------------------------------------

Still we will get old php while typing `php --version` on console. To get a new version we need to override the path which is not as simple as it should be.

In short ` rhc env add OPENSHIFT_$UNIQUESTRING_PATH_ELEMENT=value ` will work for you Provided $UNIQUESTRING doesn't conflict with the Cartridge-Short-Name element of any cartridge already in your app's gears, this will result in value being added to the PATH exposed to the various execution contexts (including your SSH sessions).

More details here https://www.openshift.com/forums/openshift/action-hook-path-export-not-sticking  

Thanks
------

Thanks to the following people (ordered by name):

* [@marekjelen](https://github.com/marekjelen)
* [@venu](https://github.com/venu)

Todos
-----

This is stuff which needs to be done right now. Feel free to do a pull request!

* Add config description
* (Add link to blog with more in-depth explanation)
