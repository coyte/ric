# ric = Remote Installation &amp; Configuration

The goal for this project is to have complete hands-off deployment of linux server with different configurations.
This project combines PXEBOOT chained into Ubuntu Server install, followed by ansible-pull.

It is assumed that an external router exists, providing DHCP with options needed for PXE.

The boot server contains a tftp server (tftpd-hpa) and a web server (lighttpd), they need to be configured to serve the tftp and www directories from this repo. For tftpd-hpa the configuration file is /etc/default/tftpd-hpa, change `TFTP_DIRECTORY="/var/ric/tftp"`. The configuration file for lighttpd is /etc/lighttpd/lighttpd.conf, change line `server.document-root        = "/var/ric/www"`

The approach is to PXEBOOT into a minimal installation of Jammy (Ubuntu 22.04), with in cloud-init just miminal configuration and packages to be able to run ansible-pull. The ansible-pull command is chainlinked in user-data.
