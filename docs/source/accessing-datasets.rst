Accessing Datasets
==================

OSN supports a RESTful API that is compatible with the basic data access model of the 
`Amazon S3 API <https://docs.aws.amazon.com/AmazonS3/latest/API/Welcome.html>`_.
Any software that complies with that API can access data stored on the OSN.

There are three common methods for connecting to and using OSN resources:

#. OSN portal built-in web tools
#. Third party desktop applications (e.g. Cyberduck, Rclone)
#. Third party data management server applications (e.g. Globus and iRods)

OSN Portal Built-in Web Tools
-----------------------------
The OSN portal (`portal.osn.xsede.org <http://portal.osn.xsede.org>`_) supports
a simple UI that allows end users to browse allocations and to upload and 
download objects via the browser. This mode of access is most appropriate for 
browsing a dataset and uploading/downloading smaller files (typically <100G).

To use the built-in browser, a user logs onto the OSN portal and clicks on one
of the allocations that they have been granted access to. This brings the user
to a searchable/sortable table listing of the allocation and its subdirectories.
Clicking on any of the objects shown initiates a download of the object to the local disk.

To upload a file, the user locates the file on their local filesystem and drags the file to the browser window. This initiates an upload to the bucket location that the user is currently browsing.


OSN Basic Bucket Browser
^^^^^^^^^^^^^^^^^^^^^^^^
.. figure:: images/osn-bbb.png
  :width: 600
  :align: center
  :alt: OSN Basic Bucket Explorer

  OSN Basic Bucket Explorer

Third Party Applications
------------------------
There are numerous commercial and open source software tools for moving files to and 
from S3 buckets. These tools provide more sophisticated capabilities than the 
built-in browser tool including transfer management, multi-upload management, and 
provide configuration options that can help optimize data transfer for a given 
computer/network environment.

To use these tools, you will need to retrieve a pair of keys that are used to access
the buckets stored on OSN. To retrieve these keys, you can contact your data manager
and she will either give you keys or create an account for you on the OSN portal where
you can retrieve these keys. If your data manager creates a portal account for you and
gives you access to the keys you can visit `OSN Portal <https://portal.osn.xsede.org>`_
to retrieve them; the allocations you have access tto and their associated keys will
be listed on your home page.

.. figure:: images/osn-smp.png
  :width: 600
  :align: center
  :alt: OSN Portal User Home page

  OSN Portal User Home page

Note that the "Bucket" information displayed in the portal has two components
(this will be important when you configure third party tools). 
The bucket information contains the OSN site/pod location and the specific 
allocation on that pod.

Cyberduck
^^^^^^^^^
Cyberduck is a popular file transfer tool that supports the S3 API.
The following describes how to configure Cyberduck to connect to an OSN resource.
Cyberduck is a "cloud storage browser" for Mac and Windows that supports multiple
storage providers/protocols.
The software may be downloaded at: `The Cyberduck Download Page <https://cyberduck.io/download/>`_ 

Using Cyberduck with OSN is straightforward.

#. Visit the OSN portal to retrive your Bucket location and allocation names (see image below)
#. Visit the OSN portal and retrieve your allocation keys or retrieve them from the data manager for your project
#. Open Cyberduck and select the bookmarks icon (see image below)
#. Click the add icon at the bottom left of the screen to create the bookmark 
#. Edit the new bookmark to point at the desired OSN pod using you allocation key pair

.. image:: images/osn-loc.png
  :width: 600
  :align: center
  :alt: OSN Portal Location and Allocation

.. figure:: images/osn-bmark.png
  :width: 600
  :align: center
  :alt: Selecting the bookmarks page and adding new bookmark

  Selecting the bookmarks page and adding new bookmark

When specifying the server, use the hostname portion of the location 
(i.e. if the location is https://mghp.osn.xsede.org the hostname is "mghp.osn.xsede.org").

When specifying "Port", use 443 if the location starts with "https://";
use 80 if the location starts with "http://".

.. figure:: images/osn-cyberdemo.png
  :width: 600
  :align: center
  :alt: Adding OSN pod and user information to bookmark

  Adding OSN pod and user information to bookmark

Anonymous Access Data Sets
""""""""""""""""""""""""""
Some datasets provide anonymous read access; if you are accessing buckets anonymously,
type "anonymous" into the Access ID portion and Cyberduck will then select the grayed
out anonymous access box in the window.

.. figure:: images/osn-cyberanon.png
  :width: 600
  :align: center
  :alt: Using anonymous access as your user

  Using anonymous access as your user

Exit the window for the bookmark to save.

Browsing, Uploading, and Downloading
""""""""""""""""""""""""""""""""""""
Once a bookmark is created, you can use it to access data by double-clicking the bookmark.
This logs your user in and lists the contents of the dataset.

**Note:** If your buckets have large object counts, you will need to increase the Timeout
settings for connections.

Go to Preference > Connection and change the box next to Timeout for opening connections
(seconds) and change the setting to 90 seconds.

.. figure:: images/osn-cyberdir.png
  :width: 600
  :align: center
  :alt: Directory listing within bucket

  Directory listing within bucket

Cyberduck client is a full-fledged transfer client so desktop up/downloads can be easily
performed for data sets.

The tool supports multiple upload/download streams, chunking, pausing and restarting.


Rclone
^^^^^^^
The most straightforward way to configure Rclone for OSN is to edit the rclone configuration file.
This file may be found by typing the command "rclone config file". 
The command will return the path to the rclone config file. 
Open this file with a text editor and add the following stanza to the end of the file: ::

	[<alias>]
	type = s3
	provider = Ceph
	access_key_id = <access key>
	secret_access_key =<secret key>
	endpoint = <location> 

Where:
* <alias> – nickname of your choice for the allocation
* <access key> – the access key from the data manager or from the portal
* <secret key> – the secret key from the data manager of the portal
* <location> – the location information provided by the data manager or portal

An example of a configuration stanza might look like: ::

	[ocean-data]
	type = s3
	provider = Ceph
	access_key_id = ASasd8KJHDAKH**&asd
	secret_access_key =asd(*&Adskj*(*(&868778
	endpoint = https://mghp.osn.xsede.org


Rclone Configuration
""""""""""""""""""""

Rclone Commands
"""""""""""""""

Third Party Data Management
---------------------------





