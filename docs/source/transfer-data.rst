Transfer Data to the OSN
============================

OSN data sets are comprised of `Ceph Objects <https://docs.ceph.com/en/latest/start/intro/>`_ accessible from anywhere,
via a RESTful protocol that follows S3 conventions.
All end user access is via S3 put and get requests,
mediated by `Bucket Policies <https://docs.ceph.com/docs/master/radosgw/bucketpolicy/>`_.
All put requests to OSN buckets must include an Authorization String.
There are two modes of get request:

* Protected Dataset buckets – All requests must include an Authorization String.
* Open access buckets – Get requests do not include an Authorization String, making the bucket accessible to anyone who has the name of the bucket and pod. The Ceph Object Gateway documentation refers to requests of this type as coming from an anonymous user.

Unlike many cloud object stores, OSN Ceph Object stores contain no information about individual users.
Access to an allocation is mediated by the keys that are assigned to authorized end users.
Some of the implications of this approach include:

* Object-level access control is not supported
* There is no audit trail that identifies the originator of any request
* Keys are unique to a bucket, and buckets are unique to a pod
* For example, if a data set has been replicated across two pods, each instance has a different set of keys and separately maintained access control
* Since there is one READ key per bucket, the origin of a Get request may only be distinguished by source IP address

