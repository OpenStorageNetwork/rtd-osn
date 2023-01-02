Managing Files and Data
=======================
There are four roles associated with an OSN allocation:
* Principal Investigator - Responsible for the allocation and serves as either the Data Manager or the Alternate Data Manager for the allocation.
* Data Manager:

	* Adds/removes data curators and data managers
	* Adds/removes end users for protected data
	* Maintain Data Set Landing Page Information
	* Monitors capacity vs utilization and requests allocation changes when needed

* The OSN Portal is used by PIs/Data managers to manage their allocations. The Portal uses CiLogon for authentication, and provides bucket administration tools to the PI/Data Manager who requested the allocation. When requesting an allocation, the PI provides an identity that is recognized by CILogon. After the bucket is created, the PI can log in to the OSN Portal and administer access to the bucket.
* Data Curator - Maintains the data set
* End User:

	* Has read access to all of the data in the bucket. Public-access buckets allow access to anyone who has the name of the pod and bucket. Authenticated access buckets allow access to anyone who has the READ key.
	* Registers via any identity service that is trusted by the data manager (InCommon, ORCID, Github, Google, Amazon, etc.
	* Logs in after receiving an invitation from a Data Manager or OSN Operations

