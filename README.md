# I no longer recommend this guide
This guide is now several years old, and no fuirther progress has been made for a while. The issue with the stock firmwares for these devices is the manufacturer will eventually give up on the firmware updates, and then the kernel and services running on them will become outdated and potentially vulnerable.

Jusdging by the fact OwnCloud installed officially on these boxes is already super old, this does not give confidence in future updates

# Where do we go from here?
I would like to see the NAS326 ported to OpenWRT, which a few other ZyXEL NASes are already. This may be something I start to work on in the future myself, and if I do, I will be sure to update this readme to point to it.

The hardware of the NAS326 is well known and I believe well supported in the mainline kernel, and I think OpenWRT would be a good candidate for this box. This may seem like an odd choice, seeing as this NAS definitely isn't wireless, let alone a router, but OpenWRT is very capable of running other services and can serve things over Ethernet perfectly fine, and it is also well maintained with automated builds and bugfixes, as well as providing a vast `opkg` repo for package management.

# Thank you
Thank you for all the people who have starred and watched this repo! Keep watching, because I will keep you updated when I have more news!

---

# ZyXEL NAS326 Hacking and Modernisation
**Disclaimer**: I am not responsible for any use or interaction with this guide. This guide is provided to be educational and additionally provide a useful end result which is a NAS326 by ZyXEL becoming more capable than ZyXEL currently supports it for.

---
## How this all started
So I recently purchased a NAS326 from Amazon for around £100. This is a 2 bay NAS which appears to run an extremely cut down version of Arch Linux ARM, with an unlocked UBoot boot loader. The device seems very capable in itself, with an App Center for installation of new software provided officially by ZyXEL, however this software appears to be largely outdated. This is where I intend to focus - on the installation of modern software.

**Noob Alert**: I am a noob. Although A lot of what I do will be correct and work fine, it may not be the best and most efficient way. If you want to correct me or provide a better way of doing something, please kindly open an issue. I have absolutely no problem with constructive criticism!

---
## The Alternative
There is a way to put Debian on the ZyXEL NAS326. I have not yet had time to test this but I have seen a lot of activity on this forum and have also posted a little myself.

Whenever people contact me about this I always back up the latest pages of this forum to the Wayback Machine

https://forum.doozan.com/read.php?2,27108

---
## Sources of Information
So I have had many sources of information during the process of working on this NAS. I will provide links (and sometimes direct page links) to as many sources of information as I can think of below:

 - ~~http://nas-central.org/ - Provided most information on existing hacks and NAS details~~
   - ~~http://zyxel.nas-central.org/wiki/Category:NAS326 - Technical details of the NAS326 including the UBoot map~~
   - ~~http://zyxel.nas-central.org/wiki/3rd_party_zypkgs - Installation guide used to build my guides for the installation of third party packages on to the NAS326~~
   - ~~http://zyxel.nas-central.org/wiki/FFP_as_zypkg - FFP which we will use for the installation of packages~~
 - nas-central.org is dead - here are the wayback links - Provided most information on existing hacks and NAS details
   - https://web.archive.org/web/20190415163227/http://zyxel.nas-central.org/wiki/Category:NAS326 - Technical details of the NAS326 including the UBoot map
   - https://web.archive.org/web/20190426053311/http://zyxel.nas-central.org/wiki/3rd_party_zypkgs - Installation guide used to build my guides for the installation of third party packages on to the NAS326
   - https://web.archive.org/web/20190409100747/http://zyxel.nas-central.org/wiki/FFP_as_zypkg - FFP which we will use for the installation of packages
 - http://www.craigamos.rocks/building-the-zyxel-nas326/ - Directory structure and Apache config location
 - https://www.smallnetbuilder.com/nas/nas-reviews/33001-zyxel-nas326-2-bay-personal-cloud-storage-reviewed?limitstart=0 - Internal board picture, technical specs
 - https://www.sammyk.me/compiling-php-from-source-writing-tests-for-php-source - PHP compilation from source guide

 - https://www.reddit.com/r/archlinux/comments/av2evg/nas_running_arch_linux_arm_zyxel_nas326/ - The original place I started this

---
## Goals
All of the guides assume you are using ZyXEL's V5.21(AAZF.3) firmware. In this firmware a few things are broken but the guides will explain how to fix them. If you need a copy of this firmware, please email me with the email at the bottom, as it is no longer available on the ZyXEL website. This repository has not yet been validated for firmware versions newer than V5.21(AAZF.3). The latest available firmware version at the time of writing this disclaimer is V5.21(AAZF.9) which is untested.

Here are the goals I intend to achieve. I will mark them as completed as I make my way through them:

 - PHP7
   - Compile and run successfully - DONE
   - Persist across reboots - DONE (ffp install directory)
   - Get working with Apache
 - MySQL Latest
   - Compile and run successfully
   - Persist across reboots
   - Auto start on boot
 - Get a VirtualHost system working on Apache
   - Support HTTP Port 80
   - Support HTTPS Port 443
   - Support multiple subdomains
   - Support other ports
 - Get the latest OwnCloud working

---
## If all the external sources disappear
~~I intend to keep a copy of all of the resources required to carry out the goals. I will write all of my guided information as if the original resources *DO* exist, and if they suddenly disappear you can either try to grab them on https://archive.org and please open an issue on this repository so I can rewrite parts of the guide so that they work with sources I can provide.~~

New repo: http://zyxel.diskstation.eu/Users/Mijzelf/zypkg-repo/

For web resources such as documentation and guides that already exist and I link to, I will try to make sure they are available on https://archive.org by manually starting a page crawl and save.

---
## Guides (ordered)
 - metarepo.md - MetaRepository, the App Center third-party repository tweak
 - ffp.md - FFP, the third-party software manager and installer
 - php7.md - PHP7, the latest PHP as of writing used for modern web apps on the NAS' Apache server

---
## Additional Resources
 - img - Folder holding all images used in the MD files
 - portscan.md - The result of a port scan run against the NAS326

---
## Contact me!
If there is an issue with this repository in ANY way, such as a broken link, broken instruction in the guide, missing resource or ANYTHING else, please open an issue on the repository.

If you are interested in helping, please contact me via email at ahorner@programmer.net preferrably with some information on what you are capable of doing and I'll see what I can give you as something I cannot do. Of course I will give credit where credit is due!
