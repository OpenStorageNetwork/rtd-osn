.. role:: strike
    :class: strike

Failure Recovery
================

When a host goes down, the cluster is configured to keep the osds
in as loss of the host does not mean that the osds data were destroyed.
When repairing, however, it's possible to bring up a partially configured
host which could cause the associated disks to be marked out (i.e. host
is up but disks are in intermediate state). We do not want this to 
happen as it would trigger re-balancing. To prevent this, whenever
recovering from a failure, set the cluster to noout: (`ceph osd set noout`).

Replacement of Storcon0 or Mon0
-----------------------------------
If a storage controller host needs to be recreated (either because the
host failed or the OS needs to be reinstalled) take the following steps.

  * Protect Cluster

    * sudo cephadm shell
    * ceph osd set noout
    * ceph osd set nobackfill
    * ceph osd set norecover

  * Use the customized installer to reinstall the OS and bring the OOB
    port/connection online.
  * Use ansible to configure host

    * Note that all of these should be run with the --limit flag for the specific host being recovered.

    * Run the recovery playbook (just copies keys right now)
    * Run the preflight playbook
    * Run the networking playbook
  * Activate OSDs

      * sudo cephadm shell
      * cephadm osd activate <<hostname>>
  * Wait for all OSDs up and in
  * Un-protect Cluster

    * sudo cephadm shell
    * ceph osd unset noout
    * ceph osd unset nobackfill
    * ceph osd unset norecover

Replacement of Storcon1
-----------------------

Differs because we need to bring up the temp link
to regain monitor quorum

Replacement of Disk
-------------------
RMAs are through Seagate.


Visit the `Seagate Warranty and Replacement website <https://www.seagate.com/support/warranty-and-replacements/>`_ 
and create an account so you will be able to RMA the disks.

Accounts must be created with a personal email, they don't allow admin groups.


Two things that were not immediately obvious:

#. On the customer returns page, the tab used to create the RMA is called "Create Order"

#. There is only one line on the RMA page to enter model + serial, below that line there is an easy-to-miss link named "add more products" clicking that allows you to add more than one drive to the RMA.

The serial nuymber to enter is likely the first 8 digits given by smartctl, i.e.  ZA1F0TKV0000C9366HQD is ZA1F0TKV

When offered, the free option is fine to use (we don't need advanced
replacement).

Once the RMA is created and you have shipping info and RMA number Kevin or Brendan can help you getting it shipped from MGHPCC.


MGHPCC handles shipping

Address to ship to:

| Seagate RMA United States CSO Service Center
| Seagate Technology c/o Agility Logistics
| 21906 Arnold Center Road
| Carson, CA 90810 United States

They should provide a pdf with address and rma number already on it
