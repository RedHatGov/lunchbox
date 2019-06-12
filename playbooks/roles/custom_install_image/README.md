custom_install_image
====================

Create a custom installation disk from a base Enterprise Linux 7 install image.  Currently only works with RHEL Server 7.6 ISO.  Currently only customizes the UEFI boot menu.

Requirements
------------

- Runs as user with privileges to create temporary files
- Runs as user with privileges to mount loop devices
- Either needs the following packages installed or runs as user with privileges to install them:
  - `mkisofs`
  - `syslinux`
  - `isomd5sum`

Role Variables
--------------

| Variable | Required | Default | Description |
| -------- | -------- | ------- | ----------- |
| `custom_install_image_src_iso` | :heavy_check_mark: | | Fully qualified location of EL7 ISO (currently only RHEL 7.6 functions) |
| `custom_install_image_dst_iso` | :heavy_check_mark: | | Fully qualified location to save the newly created ISO (will be overwritten if it exists) |
| `custom_install_image_ks_file` | :heavy_check_mark: | | Fully qualified location of the custom kickstart file |
| `custom_install_image_label` | :x: | ```custom_image``` | Label that appears when the custom ISO/disk is mounted |
| `custom_install_image_menu_label` | :x: | ```Custom Image``` | Label that appears in the installer menu |

Dependencies
------------

None

Example Playbook
----------------

```yaml
- hosts: localhost
  become: yes
  vars:
    custom_install_image_src_iso: /root/isos/rhel-server-7.6-x86_64-dvd.iso
    custom_install_image_dst_iso: /root/isos/custom.iso
    custom_install_image_ks_file: /root/custom-ks.cfg
    custom_install_image_label: "my_custom_installer"
    custom_install_image_menu_label: "My Custom Installer"
  tasks:
    - name: Create custom image
      include_role:
        name: custom_install_image_src_iso
```

License
-------

GPLv3

Author Information
------------------

[Red Hat North American Public Sector Solution Architects](https://redhatgov.io)
