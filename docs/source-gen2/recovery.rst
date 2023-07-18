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

