Email Listserv
================

The email list server for openstoragenetwork.org is run by a postfix server
hosted at osn-smtp-idies.jhu.edu. Access to this system is requires
an SSH key and the source IP added to the firewall rules and to tcp_wrappers.


Once that happens, you access it via SSH: ::

	$ ssh root@osn-smtp.idies.jhu.edu


/etc/postfix/main.cf has: ::

	virtual_alias_domains = openstoragenetwork.org
	relay_recipient_maps = hash:/etc/postfix/relay_recipients
	transport_maps = hash:/etc/postfix/transport
	virtual_alias_maps = hash:/etc/postfix/virtual

After updating one of the *_maps files, run `postmap <map_file>` then
restart postfix. Finally, check in the updated text files to SVN.

For example, to add an email alias, do: ::

	$ cd /etc/postfix

	$ vi virtual      # map the new OSN alias to a local alias, e.g.:
        # osn-help@openstoragenetwork.org          osn-help

	$ postmap virtual # update virtual.db

	$ vi relay_recipients # allow relay for the OSN alias, e.g.:
        # osn-help@openstoragenetwork.org          x

	$ postmap relay_recipients # update relay_recipients.db

	$ vi /etc/aliases # add a line for the local alias, e.g.:
        # osn-help:      jtgoodhue@mghpcc.org,kcoakley@sdsc.edu

	$ newaliases      # update the alias database

	$ systemctl restart postfix # restart the postfix server

	$ svn commit <modified file list>

