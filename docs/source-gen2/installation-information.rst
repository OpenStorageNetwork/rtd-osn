Installation Information
========================
Each installation has configuration that common to all pods and configuration
that is site-specific.

Common Site Configuration
-------------------------
The following configuration is common to all pods.

.. list-table::
  :header-rows: 1

  * - Hostname
    - iDrac IP
    - Mgmt. IP
    - Ceph Network IP
  * - storcon0
    - 172.16.3.21
    - 172.16.3.22
    - 172.16.2.2
  * - storcon1
    - 172.16.3.23
    - 172.16.3.24
    - 172.16.2.3
  * - mon0
    - 172.16.3.25
    - 172.16.3.26
    - 172.16.2.4

Site- Specific Configuration
----------------------------
The following configuration is site specific.

MGHPCC Test System
^^^^^^^^^^^^^^^^^^

  * JBOD SN:

.. list-table::
  :header-rows: 1

  * - Hostname
    - Service Tag
    - OOB
    - Access
  * - storcon0
    - 5Q08RT3
    - | A: 192.69.102.71
      | G: 192.69.102.1
      | M: 255.255.255.0
    - | A: 192.69.103.243
      | G: 192.69.103.241
      | M: 255.255.255.240
  * - storcon1
    - 3Q08RT3
    - | A: 192.69.102.72
      | G: 192.69.102.1
      | M: 255.255.255.0
    - | A: 192.69.103.244 [1]_
      | G: 192.69.103.241
      | M: 255.255.255.240
  * - mon0
    - 4Q08RT3
    - | A: 192.69.102.73
      | G: 192.69.102.1
      | M: 255.255.255.0
    - | A: 192.69.103.242
      | G: 192.69.103.241
      | M: 255.255.255.240

URI-mghpcc-staging
^^^^^^^^^^^^^^^^^^
Dashboard Password: crabtreeforu

.. list-table::
  :header-rows: 1

  * - Hostname
    - Service Tag
    - OOB
    - Access
  * - storcon0
    - 5GSJRT3
    - | A: 192.69.102.75
      | G: 192.69.102.1
      | M: 255.255.255.0
    - | A: 192.69.102.78
      | G: 192.69.102.1
      | M: 255.255.255.0
  * - storcon1
    - 4GSJRT3
    - | A: 192.69.102.76
      | G: 192.69.102.1
      | M: 255.255.255.0
    - | A: 192.69.102.79 [1]_
      | G: 192.69.102.1
      | M: 255.255.255.0
  * - mon0
    - 956Z1V3
    - | A: 192.69.102.77
      | G: 192.69.102.1
      | M: 255.255.255.0
    - | A: 192.69.102.80
      | G: 192.69.102.1
      | M: 255.255.255.0

URI
^^^^^^^^^^
Dashboard Password: crabtreeforu

.. list-table::
  :header-rows: 1

  * - Hostname
    - Service Tag
    - OOB
    - Access
  * - storcon0
    - 5GSJRT3
    - | A: 131.109.14.162
      | G: 131.109.14.161
      | M: 255.255.255.248
    - | A: 131.109.14.172
      | G: 131.109.14.169
      | M: 255.255.255.248
  * - storcon1
    - 4GSJRT3
    - | A: 131.109.14.163
      | G: 131.109.14.161
      | M: 255.255.255.248
    - | A: 131.109.14.173 [1]_
      | G: 131.109.14.169
      | M: 255.255.255.248
  * - mon0
    - 956Z1V3
    - | A: 131.109.14.164
      | G: 131.109.14.161
      | M: 255.255.255.248
    - | A: 131.109.14.174
      | G: 131.109.14.169
      | M: 255.255.255.248

USGS/WHOI
^^^^^^^^^

.. list-table::
  :header-rows: 1

  * - Hostname
    - Service Tag
    - OOB
    - Access
  * - storcon0
    - xxyyzz1
    - | A: 
      | G: 
      | M: 
    - | A: 
      | G: 
      | M: 
  * - storcon1
    - xxyyzz2
    - | A: 
      | G: 
      | M: 
    - | A: [1]_
      | G: 
      | M: 
  * - mon0
    - xxyyzz3
    - | A: 
      | G: 
      | M: 
    - | A: 
      | G: 
      | M: 

American Museum of Natural History
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. list-table::
  :header-rows: 1

  * - Hostname
    - Service Tag
    - OOB
    - Access
  * - **AMNH-P1**
    -
    -
    -
  * - storcon0
    - xxyyzz1
    - | A: 
      | G: 
      | M: 
    - | A: 
      | G: 
      | M: 
  * - storcon1
    - xxyyzz2
    - | A: 
      | G: 
      | M: 
    - | A: [1]_
      | G: 
      | M: 
  * - mon0
    - xxyyzz3
    - | A: 
      | G: 
      | M: 
    - | A: 
      | G: 
      | M: 
  * - **AMNH-P2**
    -
    -
    -
  * - storcon0
    - xxyyzz1
    - | A: 
      | G: 
      | M: 
    - | A: 
      | G: 
      | M: 
  * - storcon1
    - xxyyzz2
    - | A: 
      | G: 
      | M: 
    - | A: [1]_
      | G: 
      | M: 
  * - mon0
    - xxyyzz3
    - | A: 
      | G: 
      | M: 
    - | A: 
      | G: 
      | M: 


.. [1] This is a floating IP (Ingress IP) shared between mon0 and storcon0, it is not actually assigned to storcon1
