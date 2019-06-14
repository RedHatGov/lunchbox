custom_install_image
====================

Create a custom installation disk from a base Enterprise Linux 7 (RHEL, Fedora, CentOS) install image.

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
| `custom_install_image_src_iso` | :heavy_check_mark: | | Fully qualified location of EL7 ISO (RHEL, Fedora, CentOS) |
| `custom_install_image_dst_iso` | :heavy_check_mark: | | Fully qualified location to save the newly created ISO (will be overwritten if it exists) |
| `custom_install_image_ks_file` | :heavy_check_mark: | | Fully qualified location of the custom kickstart file |
| `custom_install_image_splash_png` | :x: | Black Screen | Image that appears behind the installer menu (must be 14-color indexed png, should be 640x480) |
| `custom_install_image_menu_label` | :x: | ```Custom Image``` | Label that appears in the installer menu |
| `custom_install_image_disk_label` | :x: | `{{ custom_install_image_menu_label }}` | Label that appears when the custom ISO/disk is mounted |

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
