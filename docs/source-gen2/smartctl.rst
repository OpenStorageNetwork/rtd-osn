Building Smartctl
=================

In order to access the Field Access Reliability Metrics (FARM), a patched
version of smartmontools needs to be built. 
There is no release that has the sufficient features, so we need to build 
from git.

We need hash `13a3dbf` from the `smartmontools git repo <https://github.com/smartmontools/smartmontools.git>`_.

Steps to rebuild the RPM
------------------------

This was done on a fresh install and updated Rocky 8.8 box.

Install rpm build and smartmontools dependcies ::

	$ sudo dnf -y install rpm-build yum-utils

	$ sudo dnf -y install automake groff libcap-ng-devel libselinux-devel ncurses-devel readline-devel systemd-devel

Download smartmontools src RPM::

	$ mkdir ~/src && cd ~/src && yumdownloader --source smartmontools 

Install smartmontools src RPM::

	$ rpm -i ~/src/smartmontools-7.1-1.el8.src.rpm

Prepare new smartmoontools tarball::

	$ cd ~/rpmbuild/SOURCES/ && git clone https://github.com/smartmontools/smartmontools.git

	$ cd smartmontools/smartmontools && git checkout 13a3dbf

	$ cd .. && mv smartmontools smartmontools-7.4 && tar -cvf ../smartmontools-7.4.tar.gz smartmontools-7.4

Update spec file::

	$ perl -pi -e "s/7.1/7.4/" ~/rpmbuild/SPECS/smartmontools.spec
	$ perl -pi -e "s/http:\/\/downloads.sourceforge.net\/%\{name\}\/%\{name\}-%\{version\}.tar.gz/smartmontools-7.4.tar.gz/" ~/rpmbuild/SPECS/smartmontools.spec

Build the new RPM::

	$ cd ~/rpmbuild/SPECS && rpmbuild -bb smartmontools.spec

Finally, install the new RPM::

	$ sudo rpm -i ~/rpmbuild/RPMS/x86_64/smartmontools-7.4-1.el8.x86_64.rpm 

