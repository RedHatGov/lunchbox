# All-In-One build of RHHI-V 1.6 for Lunchbox

Current build is still in draft phase, but the general steps for deploying are as follows:

1. use lunchbox-ks-rhvtest.cfg for kickstart file. This allows for the creation of more partitions for storage domains.
2. On the Ansible Control node (in this case, your laptop) ensure that the ansibile hosts file has the following:
```
[lunchbox]
192.0.2.253
```
3. ansible-playbook -u root main.yml -k
