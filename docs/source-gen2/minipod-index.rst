Minipod Overview
================

The MINIPOD is the Open Storage Network's second-generation pod architecture
it provides similar storage capacity to the V1 rack appliance in a 7U 
footprint. The minipod is less complex to order, install, cable and manage
compared to the V1 appliance trading some component redundancy for 
a more compact hardware architecture. 

General Configuration
---------------------

The minipod consists of three identical servers and a 106 drive JBOD. 

Data availability is supported via N+1 (i.e. 2+1) redundant server infrastructure.
If any server fails, operators can reconfigure the remaining two systems to take 
over for the failed machine. 

Data integrity is supported via 8:3 erasure coding; the array can withstand the loss
of three drives simultaneously without suffering data corruption.

Data confidentiality is supported via encryption at rest; all storage volumes are encrypted.


Comparison to V1
----------------

The V1 architecture consists of 8 servers; 3 monitor machines and 5 storage machines. Unlike the minipod
where servers are interchangeable, V1 servers are split into data servers (36 drives each) and monitors.

Data availability is supported by N+1 redundancy of each server type; i.e. you can lose 
one dat server and/or one monitor server and continue to operate. 

Data integrity is supported in the V1 pod via 3:1 erasure coding. Only one disk may be lost
without data corruption. This coding ratio is maintained to support host failure domain protection
i.e. protection against loss of all the data associated with disks connected to a dat host.

Data Confidentiality on the V1 pod is supported in the same manner as it is on the Minipod. 

Both designs represent tradeoffs. The Gen2 pod does not offer
host failure immunity. If a host fails the minipod cannot automatically heal; operators need to 
reconfigure the array to resume operation . The V1 pod can heal 
in the event of a host failure but it cannot guarantee that multiple disk failures can happen
without data corruption.

The minipod tradeoff relies on the observation that servers don't frequently fail and, when they
do, they do not typically destroy the data on connected disks. 

The V1 pod tradeoff relies on the fact that the multiple failures have to happen close enough together
that the first failure has not been healed and that the second failure has to happen in the same
placement group(s) as the first.

Minipod Hardware
----------------

A minipod is built from the following components

.. list-table::
  :header-rows: 1

  * - Quantity
    - Description
  * - 3
    - Dell PowerEdge R6515 1U Server
        | 2.5" Chassis with up to 10 NVME Drives
        | AMD 7702P 2GHz,64C/128T,256M,200W,3200
        | 8x 32GB RDIMM, 3200MT/s, Dual Rank 16Gb BASE x8
        | 2x Dell 960GB NVMe, Data Center Read Intensive Express Flash
        | SAS 12Gbps HBA External Controller, LP Adapter (Low profile right riser - slot 2)
        | PowerEdge R6515 Motherboard, with 2 x 1Gb Onboard LOM V2
        | Broadcom 57414 Dual Port 25GbE SFP28 LOM Mezz Card (slot 1)
        | Intel E810-CQDA2 Dual Port 100GbE QSFP28 Adapter (Low profile left riser - slot 3)
        | iDRAC9,Enterprise 15G
        | Dual, Hot Plug, Redundant Power Supply (1+1), 550W
  * - 1
    - Seagate Exos E4U106 JBOD
        | 4x mini-SAS HD I/O connectors
        | 106x 18TB SAS HDDs
        | 2x 2m SAS Cables
        | 2x 1G Ethernet RJ-45 protocols
  * - 1 
    - **Wiring Kit**

The wiring kit consists of cabling and transceivers used to connect the servers to one another 
to the JBOD and to the customer infrastructure.

.. list-table::
  :header-rows: 1

  * - QTY
    - ITEM

  * - Internal
    -
  * - 6
    - | sfp28-25gsr-85
      | https://www.fs.com/products/68264.html
      | Customized 25G SFP28 850nm 100m Transceiver Module - FS
      | Broadcom coded
  * - 6
    - | QSFP28-SR4-100G [1]_
      | https://www.fs.com/products/48568.html
      | Customized 100G QSFP28 100GBASE-SR4 Transceiver Module - FS
      | Intel Coded
  * - 2
    - | .3M MPO12 Cable
      | https://www.fs.com/products/68017.html
      | 12-Fiber MTP® OM4 trunk Cable 1m for 40G/100G Cabling - FS
      | .3M option on this cable (custom cable length)
  * - 3
    - | .3M LC/LC UPC OM4 Cable
      | https://www.fs.com/products/40180.html
      | LC UPC to LC UPC Duplex OM4 Multimode PVC (OFNR) 2.0mm Fiber Optic Patch Cable
      | .3M option on this cable
  * - 3
    - | 1ft Cat6 Ethernet Cable
      | https://www.fs.com/products/63440.html
      | 1ft (0.3m) Cat6 Snagless Unshielded (UTP) PVC CM Slim Ethernet Network Patch Cable, Blue
      | 1FT option on this cable
  * - 4
    - | HPE Mini-SAS HD 4x to Mini-SAS HD 4x Cable, 1m
      | https://www.connection.com/product/hpe-mini-sas-hd-4x-to-mini-sas-hd-4x-cable-1m/716195-b21/16883362
      | 1M Mini-SAS HD 4x to Mini-SAS HD 4x Cable
      | Would like a shorter cable
  * - 1
    - | Qaoquda DB9 9 Pin Female to 3.5mm Male Plug Serial Cable RS232 to 1/8 inch Conversion Cable Cord- 6FT/1.8M
      | https://www.amazon.com/Wpeng-Female-3-5mm-Serial-Conversion/dp/B06WLP4LTP
      | DB9 9 Pin Female to 3.5mm Male Plug Serial Cable RS232
      | Probably does not need to be 6' (maybe: https://www.cablestogo.com/usb-and-pc/computer-cables/serial-rs232/1-5ft-0-46m-velocity-db9-female-to-3-5mm-male-adapter-cable/p/cg-02445)

  * - Customer
    -
  * - 2
    - | QSFP28-SR4-100G [1]_
      | https://www.fs.com/products/48568.html
      | Customized 100G QSFP28 100GBASE-SR4 Transceiver Module - FS
      | Customer Coded
  * - 2
    - | 10M MPO12 Cable
      | https://www.fs.com/products/68017.html
      | 12-Fiber MTP® OM4 trunk Cable 1m for 40G/100G Cabling - FS
      | 10M option on this cable
  * - 3
    - | 30ft Cat6 Ethernet Cable
      | https://www.fs.com/products/63440.html
      | 30ft (0.3m) Cat6 Snagless Unshielded (UTP) PVC CM Slim Ethernet Network Patch Cable, Blue
      | 30FT option on this cable

.. [1] The link in the list above for the QSFP28-SR4-100G transceivers selects parts with MPO
   connectors and multimode fiber. Depending on customer site infrastructure a QSFP28-LR4-100G
   part may be more appropriate (https://www.fs.com/products/167795.html?attribute=25940&id=476628).
   This transceiver uses singlemode fiber and has a duplex LC connector.

Customer 100G Uplink
^^^^^^^^^^^^^^^^^^^^
Two (2) of the four (4) 100G transceivers listed in the "internal" section and the two (2)
100G transceivers listed in the "customer" section  of the wiring kit are for uplink from 
the pod to the customer's network. As such, the exact type of optical transport is 
site-specific. Customers will select either multimode connectivity (MPO connectors) or 
singlemode (LC connectors) based on whatever makes the most sense for their existing IT 
infrastructure. 

Design Synopsis
---------------
The pod runs Ceph, Quincy release on top of Rocky Linux 8. Cephadm is used to bootstrap
and provision the cluster. Storage controller 0 (storcon0) is used as the bootstrap node.
Storage controllers 0 and 1 are directly connected to the JBOD and act as OSD hosts. The
JBOD is zoned into a "split chassis shared nothing" configuration; each storage controller
sees a JBOD of 53 disks (half of the 106 disk array). The third server, mon0, is not connected
to the JBOD. All three servers run the the manager, monitor and rados gateway services.
External access is mediated by the ingress service which runs on storcon0 and mon0
(these are the machines with external access). Load is spread across the three servers
by the ingress service via HAProxy. The ingress provides HA IP via keepalived/vrrp.

.. figure:: images/MinipodNetworking-Current.png
  :width: 600
  :align: center
  :alt: Minipod System Diagram

  Minipod System Diagram

Networking
----------
The Minipod has four networks which provide external access (to RGW services), out-of-band (OOB) administration,
server management and ceph communications. Note that the minipod does not contain
a separate networking switch. Removing switching hardware from the design simplifies
configuration and Management, removes a point of failure and reduces cost. 

Access Networking
^^^^^^^^^^^^^^^^^
For the access network, he site provider is responsible for providing two (2) 100G L3 handoffs to the minipod 
and three (3) publicly routed IP addresses. 

OOB Networking
^^^^^^^^^^^^^^
For out of band access, the site provider is responsible for providing three (3) copper 1G L3 handoffs to the minipod and 
three (3) publicly routed IP address (preferably) on separate physical infrastructure from the 
access network. 

Server Management
^^^^^^^^^^^^^^^^^
The server management network is internal to the minipod and provides access to the
BMC cards. Each server acts as a "jump host" to the BMC of one of its peers:

.. list-table::
  :header-rows: 1

  * - Jump Server
    - Reachable BMC
    - BMC Address
  * - storcon0
    - mon0
    - 172.16.3.25
  * - storcon1
    - storcon0
    - 172.16.3.21
  * - mon0
    - storcon1
    - 172.16.3.23

This allows remote, out of band BMC control for each of the
servers. The network used for these connections is 172.16.3.0/24

CEPH Public Network
^^^^^^^^^^^^^^^^^^^
The Ceph "public" network is a specific (unfortunately named) concept in the ceph architecture.
This network provides communication among the daemons that make up the storage system. You 
can learn more about ceph networking in the `Ceph Network Configuration Reference`_.
This is a 100G internal network. This network
is supported by a bridge on storcon1. Storcon0 and mon0 connect to the bridge on storcon1 where
storcon1 has virtual interface. Via this bridge, all three servers can communicate with one another. 
Each server is connected to storcon1 via a bonded pair of links (100G active / 25G standby).

.. _Ceph Network Configuration Reference: https://docs.ceph.com/en/latest/rados/configuration/network-config-ref/

Let's Build a Minipod!!
=======================
The setup of a new pod consists of a
hardware installation and initialization step performed locally by the customer and 
a remote configuration step performed by the OSN team. 

* Customer

  * Site Preparation
  * Physical Installation
  * Server Initialization
* OSN Remote DevOps

  * JBOD Configuration
  * Ansible Playbooks

    * Preflight
    * Networking
    * Bootstrap
    * RGW
  * Validation

    * Dashboard functionality
    * Rclone upload test

Customer
--------
The customer provisioning steps consist 
of preparing the site, purchasing and installing hardware and
installing the base operating system on storcon0, storcon1 and mon0.
The OSN team provides a disk image that the customer uses to install 
the operating system; this image is customized for each 
site using information provided by the customer.

Customer Preflight
^^^^^^^^^^^^^^^^^^
* Order Minipod Hardware
* Provision Minipod OOB Networking

  * 3x1G Copper access ports
  * 3x routed public IPs (specify IP address, gateway and netmask)
  * Outbound: http, https
  * Inbound: ssh 

    * Can be source limited to OSN ctl nodes
  * Verify with test endpoint machine that connections work
* Provision Minipod Access Networking

  * 2x100G QSFP28 access ports

    * Note that transceivers are specified in the cable kit BOM
      so all that is required from IT is the provisioning of a 
      QSFP28 switchport
  * 3x routed public IPs

    * One for each ingress host and a third for the VIP
  * Outbound: http, https
  * Inbound: http, https
  * Verify with test endpoint machine that connections work
* Submit Ticket for Custom Boot ISO (help@mghpcc.org)

  * For each machine provide

    * Hostname (i.e. stocon0, storcon1 or mon0)
    * Service Tag
    * OOB IP Address, Gateway and Netmask
    * Access IP Address, Gateway and Netmask (only for mon0 and storcon0)

.. note::
  All three machines are identical so which machine you 
  choose to be storcon0, storcon1 or mon0 does not matter as long as 
  they are cabled per the system diagram and that you provide the 
  correct service tag and IP information for the machines that you choose

Customer Hardware Installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* Install the hardware per the system diagram
* Make sure to correctly note the system tag information
  for each of the hosts.

Customer Software Initialization
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Download the custom installer ISO generated from the help ticket request
* Copy the installer iso to a USB3.0 drive 12G or larger

  * sudo dd if=boot.iso of=/dev/sd<??> bs=4M status=progress
* For each Server

  * Connect usb keyboard and mouse
  * Connect monitor to console video output
  * Insert the boot iso drive into a usb port
  * Power on the machine (or cycle if machine has been powered on)
  * Make sure machine is configured for UEFI boot
  * Hit F11 during power up sequence
  * Select the UEFI one shot option
  * Boot from boot iso drive
  * Confirm the OS installation

    * The machine should install the Centos 8 Stream Operating 
      system and reboot to a logon prompt.
  * Note that you will need an active internet connection during this process

* Once all three servers are initialized verify that you can ping the servers
  from an external IP address

.. note::
  At this point the servers are accessible over the internet and OSN 
  DevOps can take over the remaining provisioning steps.

OSN DevOps
----------
The customer provisioning steps prepare the servers for remote configuration.
The custom install image initializes networking and sets up the necessary
administrator accounts, passwords and keys so that OSN DevOPs can remotely
configure the storage cluster.

Custom Image Creation
^^^^^^^^^^^^^^^^^^^^^
Each pod is built from an installer customized to the pod site. The installer
is responsible for setting up a baseline CentOS 8 Stream system on each of the three
hosts. The installer configures just enough software and networking 
to allow OSN DevOPs to access the machines remotely and provision the rest 
of the storage software.

Overall Design
""""""""""""""
The site-specific OSN installer consists of a "stock" CentOS 8 Stream
installer with a custom kickstart that implements the following
customizations:

  * Intel Driver: The pod requires the most recent Intel NIC driver. That 
    driver is included in the custom installer and installed during setup.

  * Baseline networking packages: The software installs utilities needed 
    to configure the JBOD and the iDRAC IP addresses.

  * Ansible provisioning user: The installer creates a privileged
    user (osnadmin) and assigns initial credentials to the user. The 
    "bootstrap" credentials are changed as the first step of remote provisioning.

  * OOB networking - The installer encodes information provided by the pod site
    (Service Tag and Networking information) to configure the OOB network connection. 
    The install inspects the serial number of the machine it is installing on and uses
    that to choose the correct hostname and OOB IP settlings. This customization is unique 
    to each site.

The customized installer image is created using the script "minipodiso.sh"

ISO Builder
""""""""""""
In order to run the build script, the DevOps build environment requires the following 
packages be installed:

  * OS

    * sudo dnf install syslinux genisoimage isomd5sum git

  * Python/ansible

    * cd ~ && git clone https://github.com/OpenStorageNetwork/minipod.git
    * virtualenvwrapper (convenience for custom build env)

      * sudo pip3 install virtualenvwrapper
      * edit .bashrc
      
          * export VIRTUALENVWRAPPER_PYTHON=python3
          * export WORKON_HOME=$HOME/.virtualenvs
          * source /usr/local/bin/virtualenvwrapper.sh

      * source ~/.bashrc
      * mkvirtualenv -a ~/minipod minipod
      * pip install netaddr ansible
      * ansible-galaxy collection install ansible.utils ansible.posix

When run, the build script retrieves the CentOS image, loop mounts it and
copies the contents to a build directory. The script then creates a customized
kickstart file (using the same site inventories used to provision CEPH) and copies
that and the updated Intel drivers to the build directory. When those assets 
have been collected, the script modifies the bootloader config to use the 
new installer image and repackages the files into an installer iso.

This iso is then copied (dd or equivalent) to a usb drive which is used by
site sysadmins to install the initial OS on the hardware.

Intel ICE Driver
""""""""""""""""
This driver exhibited issues between two CentOS 8 Stream releases. The 
issue has to do with RDMA and its interaction with bridges (and bonds?)
It is likely the issue developed as a result of a kernel update without
an update to the ice driver (which has a fix for the RDMA issue).

This problem does not appear to be present in the Rocky 8 based
install. As a precaution, we will include the driver compiled 
for the Rocky 8 kernel used to build the minipod installer 
(4.18.0-425.3.1.el8.x86_64) in the event that more testing would have
uncovered the issue in Rocky as well. Note that this driver
only works with this specific kernel version and will not work if/when
Rocky updates are done.

Howto compile ice drivers. Note that the drivers need to be 
compiled on a system with the same kernel as the target:

  * Drivers are here: https://www.intel.com/content/www/us/en/download/19630/763930/intel-network-adapter-driver-for-e810-series-devices-under-linux.html
  * Download ice-1.10.1.2.2 release
  * Install tools and kernel headers

    * rpmbuild

      * sudo dnf install rpm-build-4.14.3-24.el8_7.x86_64

    * Development tools

      * sudo dnf group install "Development Tools"

    * Kernel headers - note you need to match exact kernel version

      * sudo dnf install kernel-devel-$(uname -r)

    * Createrepo

      * sudo dnf install createrepo

  * Build driver rpm

    * you can unpack the driver tar file to get README/details
    * rpmbuild -tb ice-1.10.1.2.2.tar.gz

  * Create a repo

    * mkdir icerepo
    * cp ./rpmbuild/RPMS/x86_64/ice-1.10.1.2.2-1.x86_64.rpm icerepo
    * cd icerepo
    * createrepo .

Once the repo has been created, you can create a tar file for it
and update the installer to reference it. The installer will
copy the repo to the install and make it available as a repo
in the installed system. It will not install the driver as there
isn't a known need for it at this point.

DevOPs Preflight
^^^^^^^^^^^^^^^^
  * Confirm networking
    
    * SSH to each machine using the bootstrap private key

      * Verify that osnadmin user has sudo privileges

    * Validate expected network device naming

      * ens3f0/1 - 100G devices, Intel NIC
      * ens1f0np0, ens1f1np1 - 25G devices, Broadcom NIC
      * eno1, eno2 - 1G devices - LOM
      * This could get cobbled due to wrong slot placement for the 
        25G and 100G nics or firmware changes (the Broadcom NICS changed
        names between driver updates)

  * Create customized inventory file for the site
    
    * This will likely be done during the ticket processing

  * On the ansible controller host run the following playbooks:
  
    * Set the AWS credentials

      * export AWS_ACCESS_KEY_ID=<keyhere>
      * export AWS_SECRET_ACCESS_KEY=<keyhere>

    * preflight - to install ceph and osn packages
    * networking-  to setup the pod networks

  * Reboot machines

  * Validate intrapod connectivity

    * Confirm ping from-to each host on the cluster network
    * Confirm gateway ping on each of the external networks
    * confirm idrac ping on each of the hosts to their peer bmc interfaces

  * Verify IPMI connectivity (portforward idracs from each host)

.. note::
     You need to disable host header checking to support port forwarding

     * ssh to the idrac of each machine using root credentials
     * On the idrac issue ``set idrac.webserver.HostHeaderCheck 0``
     * **TODO** - can we set this via ipmi either in ansible or kickstart?

Configure the JBOD
^^^^^^^^^^^^^^^^^^
  * Verify baseline == 106 disks - run lsscsi and count the disks
  * Upload firmware update to storcon0

    * 4.36 Firmware was the one tested with RHEL 8.5 and is the current version 
      validated for minipod.
    * Firmware package is: UUT4.36_generic_cp_USMR2021.13.0.RC8
    * Package contains instructions for inband update

  * Run inband controller update
  * Use minicom to connect to the JBOD

    * sudo minicom -s
    * select serial port setup

      * A - Serial Device - /dev/ttyS1
      * E - Nps/Par/Bits - 115200 8N1
      * F - HW Flow control - No
      * G - SW Flow control - No

  * Execute the GEM commands to split the chassis

    * set_zone_mode 3

      * HA2x2
      * Ports 0/2 - Group A
      * Ports 1/3 - Group B

  * Reboot storcon0 and storcon1
  * Verify that each controller sees 53 disks

.. note::
  The most recent JBOD received (3/20/23) came with updated firmware 
  and was able to execute the array split command. Firmware
  updating will likely not be needed on install in the future. 

Bootstrap Storage Cluster
^^^^^^^^^^^^^^^^^^^^^^^^^

  * Run the bootstrap playbook
  * Logon to storcon0 and run "sudo cephadm ceph status"
  * Periodically run status to monitor the progress of the cluster build

    * Your looking for "HEALTH_OK" and 106 osds, 106 up, 106 in
    * Note that this can take up to an hour to complete. 


Setup and Verify RGW
^^^^^^^^^^^^^^^^^^^^

    * Run the rgw playbook

      * Note that this step will create certs for the ingress service and
        requires access to route53 to complete the ACME domain validation.
        You need to make sure that the AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY
        environment variables are set before running the rgw playbook.

      * Safer to use short term credentials

        * Set AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY envars on local machine
        * Execute: "aws sts get-session-token --duration-seconds=900"
        * Use resulting credentials (these are limited to 15min 
          but you can choose any duration) on provisioning machine.

          * Note you need to set the additional envvar, AWS_SESSION_TOKEN

    * Verify rgw and ingress services are up (ceph orch ls)
    * Curl the external interface to make sure that they respond and have valid certs

      * ``curl --insecure -vvI https://minipod.osn.mghpcc.org 2>&1 | 
        awk 'BEGIN { cert=0 } /^\* SSL connection/ { cert=1 } /^\*/ { if (cert) print }'``
    * Verify that you can access the dashboard

      * Get dashboard admin credentials and location 

        * Logon to storcon0
        * grep -A 5 Dashboard /var/log/ceph/cephadm.log

      * Portforward dashboard port (shown in grep above) from storcon0

    * Use the dashboard to create a testbucket
    * Get dashboard user credentials from users page

      * Select Object Gateway -> Users side-menu pick
      * turn down knob on gateway user
      * select keys tab
      * select dashboard username
      * click show button
    * Add minipod config to rclone using dashboard user credentials
    * Verify object upload/download to/from the minipod using the rclone config

DOC NOTES
=========

  * Need to write down process for stomping bootstrap root pwd and key
  * Note that osnadmin *is* the default privileged user setup in kickstart

  * Proposal for ssh key Management

    * Store keys in AWS Secrets Manager
    * Give OSN admins accounts in the mghpcc org (should we create another org?)
    * Create secrets in mghpcc secrets thing
    * Grant secret read access to osn admin people

    * Steps to run ansible

      * Using your IAM credentials run the token fetch scripty thing to fetch temporary creds
      * Set envars with temporary creds returned 
      * Go have fun provisioning things for things - whee!  