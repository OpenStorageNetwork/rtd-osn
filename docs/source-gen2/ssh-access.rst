SSH Access to OSN Pods
========================

OSN ansible scripts distribute administrator public keys to the pods.
All pods implement firewall rules that are source-limiting to the
control machines (ctl01, ctl02 and ctl03).

Gen2 Access
-----------
The following ssh config file pattern is convenient for accessing 
gen2 pods::

    # ------ALL PODS------
    Host *-storcon0
            User osnadmin

    Host *-storcon1
            User osnadmin

    Host *-mon0
            User osnadmin

    # ------AMNH1 POD------

    Host amnh1-storcon0 amnh1-storcon1 amnh1-mon0
        SetEnv "PS1=AMNH1 [\u@\h \W]\$ "
        IdentityFile ~/.ssh/myprivatekey
        ProxyJump ctl01

    Host amnh1-storcon0
        LocalForward 9443 172.16.3.25:443
        Hostname 216.73.243.141

    Host amnh1-storcon1
        LocalForward 9443 172.16.3.21:443
        Hostname 216.73.243.142

    Host amnh1-mon0
        LocalForward 9443 172.16.3.23:443
        Hostname 216.73.243.143

This example is for a pod named amnh1; substitute your podname for all 
instances of amnh1. The Host IP addresses are the OOB addresses
for each of the pod nodes. A list of IP addresses for hosts at pod sites
can be found in the :doc:`installation-information` document. Note that 
the ``SetEnv "PS1=AMNH1 [\u@\h \W]\$ "`` config line will set your prompt so that
you are less likely to accidentally execute a command on the wrong node.

Gen1 Access
-----------

  * Logon to either ctl01 or ctl02
  * sudo -u ansible bash
  * export SITE_ID=<<siteid>>
  * Where <<siteid>> is one of:
    * mghp
    * renc
    * ncsa
    * sdsc
    * jhui
  * ssh <<hostip>>
    * Where <<hostip>> is one of:
      * 172.16.2.11 (mon1)
      * 172.16.2.12 (mon2)
      * 172.16.2.13 (mon3)
      * 172.16.2.111 (dat01)
      * 172.16.2.112 (dat02)
      * 172.16.2.113 (dat03)
      * 172.16.2.114 (dat04)
      * 172.16.2.115 (dat05)





