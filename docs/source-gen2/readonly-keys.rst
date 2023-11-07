
OSN Bucket Read-only Keys
========================

* Required tools

  * aws-cli - install v 2.13+
  * jq

.. note::
    * Note that with the 2.13+ version of aws-cli, you can spec endpoint in config. If not using that, specify endpoint on command line i.e., --endpoint-url //endpoint//<code>


* Create aws profile with osnadmin site user (or equivalent priviged user) for <<site>>

    * if you're wondering what the keys are just cephadm/radosgw-admin to the site and look at the user...

*  Create new radosgw user == <<bucketname>>_readonly

::

  ssh <<site>> 'sudo cephadm shell radosgw-admin user create --uid=<<bucketname>>_readonly --display-name="<<bucketname>> readonly user"'

* Record the keys for the new user

* Get current bucket policy (save the original in case you mess up)

::

  aws s3api get-bucket-policy --profile <<site>> --bucket <<bucketname>> | jq '.Policy | fromjson' > <<bucketname>>-orig.json
  cp <<bucketname>>-orig.json <<bucketname>>-readonly.json

* Remove the anon read policy stanza if one exists (will have a principal "AWS": ["*"])

* Add the following stanza to the <<bucketname>>-readonly.json policy file

::

  {
    "Sid":"bucket read-only policy",
    "Effect":"Allow",
    "Principal": {"AWS": ["arn:aws:iam:::user/<<bucketname>>_readonly"]},
    "Action":["s3:GetObject","s3:ListBucket"],
    "Resource":[
      "arn:aws:s3:::<<bucketname>>/*",
      "arn:aws:s3:::<<bucketname>>"
     ]
  }

* Apply the updated policy

::

  aws s3api put-bucket-policy --profile <<site>> --bucket <<bucketname>> --policy file://<<bucketname>>-readonly.json


* Test the new <<bucketname>>_readonly user keys however you like to test
* Goto OSN portal and find project
* "Magic Click" on project name

  * windows-key + alt (window/linux kbd)
  * option + command (mac)

* Click <<projectname>>_datamanagers link
* Click "Add new Read Only key" and add key information

.. note::
  Note that we got rid of RO key support a while back so this just adds to the RW list. As
  a result, when specifying the bucket, use the bucket name suffixed with "(RO)" e.g.

    * RW Bucket: "https://usgs.osn.mghpcc.org/mdmf-workspace"
    * RO Bucket: "https://usgs.osn.mghpcc.org/mdmf-workspace (RO)"

  The RO suffix approach may break some other functionality that
  expects the bucket to be a valid URI but it's all we have for now.

* Visit project and verify that the keys are showing (may need to make yourself a datamanager...)
