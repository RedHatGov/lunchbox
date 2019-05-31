# All-In-One build of RHHI-V 1.6 for Lunchbox

Current build is still in draft phase, but the general steps for deploying are as follows:

1. use lunchbox-ks-rhvtest.cfg for kickstart file. This allows for the creation of more partitions for storage domains.
2. On the Ansible Control node (in this case, your laptop) ensure that the ansibile hosts file has the following:
```
[lunchbox]
192.0.2.253
```
3. ansible-playbook -u root main.yml -k



Workarounds:

- From https://bugzilla.redhat.com/show_bug.cgi?id=1692671 , if we have a DNS/dnsmasq server we'll be fine. If we do not, we must do the following in the inventory file:
```
<snip>
hosts:
    rhhihost1.example.com:
      gluster_features_fqdn_check: false  <----------------
      gluster_infra_volume_groups:
        - vgname: gluster_vg_sdb
          pvname: /dev/sdb
        - vgname: gluster_vg_sdc
          pvname: /dev/mapper/vdo_sdc
</snip>
```
- From https://bugzilla.redhat.com/show_bug.cgi?id=1713816, cannot install on partitions in RHHI-V 1.6. Workaround is to add the following to inventory. Note this has nothing to do with 512 block or 4k sizes... the gluster.ansible prereq playbook checks a pv's existence and fails if there are partitions.
  - gluster_features_512B_check: false
