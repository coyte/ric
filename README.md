# ric = Remote Installation &amp; Configuration

The goal for this project is to have complete hands-off deployment of linux server with different configurations.
This project combines PXEBOOT chained into Ubuntu Server install, followed by ansible-pull.

It is assumed that an external router exists, providing DHCP with options needed for PXE.

The boot server contains a tftp server (tftpd-hpa) and a web server (lighttpd), they need to be configured to serve the tftp and www directories from this repo. For tftpd-hpa the configuration file is /etc/default/tftpd-hpa, change `TFTP_DIRECTORY="/var/ric/tftp"`. The configuration file for lighttpd is /etc/lighttpd/lighttpd.conf, change line `server.document-root        = "/var/ric/www"`

The approach is to PXEBOOT into a minimal installation of Jammy (Ubuntu 22.04), with in cloud-init just miminal configuration and packages to be able to run ansible-pull. The ansible-pull command is chainlinked in user-data...


Let's start with PXEBOOT
We need to get files: 
    vmlinuz, initrd
    Mount the ubuntu iso file in /mnt.
    Find the required file in /mnt/caspar
    copy them in the ric/tftp/tftpboot/ubuntu-server-22.04

    ldlinux.c32, ldlinux.e32, ldlinux.e64, libcom32.c32, libutil.c32, pxelinux.0
    install the syslinux and pxelinux on a temporary Jammy server.
    find the files on the server and copy them to ric/tftp/tftpboot

