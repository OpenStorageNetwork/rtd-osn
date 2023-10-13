Open Access & Protected Datasets
================================

OSN datasets can be either open access or protected. In the former case, keys are only needed to write
new objects to the dataset otherwise, read access can be accomplished anonymously
(e.g. as shown earlier for the anonymous cyberduck configuration).
Protected datasets require keys for both reading and writing.
When an open access dataset is created only one pair of keys are created, which are accessible
to the data manager for a project and are used to upload data to the allocation.
No keys are needed by users to download/read the data stored in the allocation.

Protected datasets have two sets of keys.
One set allows writing to the dataset and is identical in function to the on previously described for open access datasets.
The second set of keys provides read access to the dataset.
Anonymous access is not allowed on protected datasets.

Keys are shared with users in two ways.
Data managers can choose to share keys with other users "out of band" by simply sending
other users keys that they are interested in via whatever secure mechanisms the project
uses to store and communicate project-specific secrets
(e.g. username/passwords, certificates, PKI material, access keys, etc.).
Keys can also be managed using the OSN portal.
A project in the OSN portal may have multiple allocations associated with it.
Data managers for a project have access to all keys for a project's allocations.
A data manager may share all project keys with another portal user by:

1. Adding the portal user to the data manager's group
2. Assigning that group member the data manager role

Once another portal user has been added to a group and given the data manager role for that group,
she will have access to all the keys (and have the same privileges in the portal) as the original data manager for the group.
Data managers may also add users to a group without assigning the user the data manager role.
When this happens the user will only have access to keys that the data manager has made "visible".
Visible keys are available to all group members whereas non-visible keys are only available to
group members in the data manager role.
In the image below, culbertj@mit.edu and jtgoodhue@mghpcc.org have access to all the keys in the
project because they are both data managers for the project "JIMTEST", dsimmel@psc.edu will only
have access to the two keys shown with the "visible" checkbox checked.

.. .. figure:: images/osn-data-management.png
..   :width: 600
..   :align: center
..   :alt: Data Management Example

..   Data Management Example
