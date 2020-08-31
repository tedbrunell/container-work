The purpose of this project is to post dockerfiles and buildah scripts that can be used to create container images.

## ubi-nano

*"ubi-nano"* is an attempt to create a Red Hat UBI based image that is as small as possible and without bloat from a package manager or uneeded packages.  Using the included ubi-nano dockerfile, the reulting size is 35.6MB.  Using <a href="https://github.com/fatherlinux/ubi-micro">Scott McCarty's excellent ubi-mini</a> file as a starting point, I was able to experiment with removing additional packages and the effects of those removals on package size and container functionality.  I ended up remove one additional package, after the intitial install completes, to reduce the size by another 700KB.

### So, what was removed?
The "setup" package was removed post install.  This file, according to dnf info, "contains a set of important system configuration and setup files, such as passwd, group, and profile."  The files that this package creates (and are subsequently removed) are:

/etc/aliases\
/etc/bashrc\
/etc/csh.cshrc\
/etc/csh.login\
/etc/environment\
/etc/ethertypes\
/etc/exports\
/etc/filesystems\
/etc/fstab\
/etc/group\
/etc/gshadow\
/etc/host.conf\
/etc/hosts\
/etc/inputrc\
/etc/motd\
/etc/motd.d\
/etc/networks\
/etc/passwd\
/etc/printcap\
/etc/profile\
/etc/profile.d/csh.local\
/etc/profile.d/lang.csh\
/etc/profile.d/lang.sh\
/etc/profile.d/sh.local\
/etc/protocols\
/etc/services\
/etc/shadow\
/etc/shells\
/etc/subgid\
/etc/subuid\
/run/motd\
/run/motd.d\
/usr/lib/motd\
/usr/lib/motd.d\
/usr/lib/tmpfiles.d/setup.conf\
/usr/share/doc/setup\
/usr/share/doc/setup/uidgid\
/usr/share/licenses/setup\
/usr/share/licenses/setup/COPYING\
/var/log/lastlog

In most cases, these files are probably not needed to run an application server within a container and their removal may help with some security aspects of the container itself 
