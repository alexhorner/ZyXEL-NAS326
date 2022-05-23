# PHP7 Compilation, Installation and Configuration

**Note**: This guide assumes you have followed ffp.md . If you have not followed ffp.md , please do so now.

---
## Slacker troubles
So this is where things get a little fiddly. I am assuming you're using firmware version 5.21. Slacker, the package manager and listing system which comes with FFP is a little broken in this version of the firmware so we have to mess with it a little to make it want to work. Even then it only half works, but it works enough for this process.

## Where it breaks
So, I will give an example of what slacker does when you try to get it to update it's package list using `slacker -U` :

```
Updating package lists...
fetch: rsync -q 'rsync://ffp.inreto.de/ffp/0.7/arm/packages/CHECKSUMS.md5' '/ffp/funpkg/cache/s'
fetch: (cd '/ffp/funpkg/cache/mz'; wget -Nnv 'http://downloads.zyxel.nas-central.org/Users/Mijzelf/FFP-Stick/packages/0.7/arm/CHECKSUMS.md5')
wget: invalid option -- 'N'
BusyBox v1.19.4 (2018-11-08 14:41:15 CST) multi-call binary.

Usage: wget [-c|--continue] [-s|--spider] [-q|--quiet] [-O|--output-document FILE]
        [--header 'header: value'] [-Y|--proxy on/off] [-P DIR]
        [--no-check-certificate] [-U|--user-agent AGENT] [-T SEC] URL...
```
As you can see, the rsync call works fine, however the wget call fails as the version of wget installed in firmware 5.21 does not understand ANY of the arguments supplied. This can be fixed by manually downloading the file it tried to in the directory it went to and then running it again, tricking it into thinking it downloaded successfully. For this we run `cd /ffp/funpkg/cache/mz` and then run ~~`wget http://downloads.zyxel.nas-central.org/Users/Mijzelf/FFP-Stick/packages/0.7/arm/CHECKSUMS.md5`~~ `wget https://web.archive.org/web/20180809135547/http://downloads.zyxel.nas-central.org/Users/Mijzelf/FFP-Stick/packages/0.7/arm/CHECKSUMS.md5` assuming your URL in the error is the same as mine (copy and paste that URL!) . We can then run `slacker -U` again.

## Downloading the required packages
First off, start the slacker package manager with `slacker -a` . The layout of the slacker screen shows you things from left to right:
```
[ ] install/upgrade/reinstall    repo:directory/package.txz
```
The repo is important. At the time of writing there is the `mz` repo and the `s` repo. The `mz` repo does not work from the slacker package manager as it breaks with wget again when it tries to install. the `s` repo uses rsync so it works fine. Lukily all of the packages we need are in the `s` repo.

**NOTE**: If the repositories become unavailable or slacker just doesn't work at all anymore, I am going to build a small shell script which is able to download and install all of the required packages for you from a repository I host as a mirror to the real one. For now however this is not required.

**I am going to list all of the packages from the `s` repo that I have installed. I am aware that some of these packages are completely unrelated to the compiler and libraries required, however to make it easier for me (as I am not certain which of the packages are 100% required) and to allow you to as closely match my installation as possible I will list them all:**

```
s:autoconf-2.68-arm-1.txz
s:automake-1.11.1-arm-1.txz
s:bash-4.1.011-arm-1.txz
s:binutils-2.22-arm-1.txz
s:busybox-netutils-1.18.4-arm-1.txz
s:bzip2-1.0.6-arm-1.txz
s:cmake-2.8.4-arm-1.txz
s:coreutils-8.14-arm-1.txz
s:curl-7.21.4-arm-1.txz
s:db5-5.2.36-arm-1.txz
s:dialog-1.1_20110118-arm-1.txz
s:e2fsprogs-1.41.14-arm-1.txz
s:expat-2.0.1-arm-1.txz
s:ffp-init-0.7.0-arm-1.txz
s:file-5.09-arm-1.txz
s:findutils-4.4.2-arm-1.txz
s:funpkg-0.6.3-arm-1.txz
s:gawk-4.0.0-arm-1.txz
s:gcc-4.5_20111110-arm-1.txz
s:gcc-solibs-4.5_20111110-arm-1.txz
s:gdb-7.3.1-arm-1.txz
s:gettext-0.18.1.1-arm-1.txz
s:giflib-4.1.6-arm-1.txz
s:git-1.7.8.4-arm-1.txz
s:gmp-5.0.2-arm-1.txz
s:grep-2.9-arm-1.txz
s:groff-1.21-arm-1.txz
s:gzip-1.4-arm-1.txz
s:iana-etc-2.30-arm-1.txz
s:icu4c-4.6.1-arm-1.txz
s:infozip-6.0-arm-1.txz
s:intltool-0.40.6-arm-1.txz
s:less-443-arm-1.txz
s:libarchive-2.8.4-arm-1.txz
s:libdaemon-0.14-arm-1.txz
s:libev-4.04-arm-1.txz
s:libexif-0.6.20-arm-1.txz
s:libgcrypt-1.5.0-arm-1.txz
s:libgpg-error-1.10-arm-1.txz
s:libiconv-1.14-arm-1.txz
s:libjpeg-8c-arm-1.txz
s:libpcap-1.1.1-arm-1.txz
s:libpng-1.4.7-arm-1.txz
s:libtool-2.4-arm-1.txz
s:libxml2-2.7.8-arm-1.txz
s:lighttpd-1.4.29-arm-1.tx
s:linux-headers-2.6.22-arm-1.txz
s:lsof-4.84-arm-1.txz
s:m4-1.4.16-arm-1.txz
s:make-3.81-arm-1.txz
s:man-1.6g-arm-1.txz
s:mpc-0.9-arm-1.txz
s:mpfr-3.1.0-arm-1.txz
s:ncurses-5.9_20111217-arm-1.txz
s:nfs-utils-1.2.5-arm-1.txz
s:openssh-5.9p1-arm-1.txz
s:openssl-1.0.0e-arm-1.txz
s:pcre-8.21-arm-1.txz
s:perl-5.14.2-arm-1.txz
s:php-5.3.9-arm-1.txz
s:pkg-config-0.25-arm-1.txz
s:portmap-6.0-arm-1.txz
s:procps-3.2.8-arm-1.txz
s:python-3.2.2-arm-1.txz
s:rcorder-20031013-arm-1.txz
s:readline-6.2.001-arm-1.txz
s:rsync-3.0.9-arm-1.txz
s:sed-4.2.1-arm-1.txz
s:shadow-4.1.4.3-arm-1.txz
s:strace-4.5.20-arm-1.txz
s:tar-1.26-arm-1.txz
s:tcp_wrappers-7.6-arm-1.txz
s:uClibc-0.9.33_git-arm-1.txz
s:uClibc-solibs-0.9.33_git-arm-1.txz
s:util-linux-2.20-arm-1.txz
s:vim-7.3.382-arm-1.txz
s:wget-1.12-arm-1.txz
s:xz-5.0.3-arm-1.txz
s:zlib-1.2.5-arm-1.txz
```

**Now thats a lot of packages, however if you managed to get Slacker working it shouldn't take you too long to scroll down the list and press the space bar to select the packages you need. Again, if slacker goes down i'll write a script which downloads all of them and installes them for you.**

## Building PHP7
As of now, PHP 7.3.2 is the latest PHP 7.3 available and PHP 7.2.15 is the latest PHP 7.2 available at https://php.net . At the time of writing, the latest OwnCloud 10.1.0 *DOES NOT* support PHP 7.3, only PHP 7.2 . Regardless, I am writing this to build and install PHP 7.3.2 however this should work with paractically any PHP 7 version (and PHP 8 etc if it becomes a thing) .

 - To begin, you're probably going to want to create a nice directory where you can download and compile PHP on the RAID volume. My suggestion is you run `cd /i-data/sysvol` then `mkdir compilephp` then `cd compilephp` .

 1. Go to https://php.net and go to the Downloads section.
 2. Find the version you wish to compile, and click the download link labelled `php-?.?.?.tar.xz` .
 3. Find a download location you wish to use, and RIGHT CLICK the link to it, and copy.
 4. (On SSH) Run `wget PASTE LINK HERE` pasting the link you just copied in the position.
 5. Your file should be called `mirror` . Change this by running `mv mirror php.tar.xz` .
 6. Extract the .tar.xz by running `tar -xf php.tar.xz` .
 7. Run `ls` and find the new directory, then `cd` to it.
 
Now we are ready to compile our newly downloaded PHP. I could NOT get it to compile with `libiconv` even though tthat library was installed, so I will use a `--without-iconv` argument to turn it off. You can try without that argument, but if it doesn't work you can just put that argument back.

 1. Run `./buildconf --force`
 2. Run `mkdir /ffp/php7` __!--!__
 3. Run `./configure --prefix=/ffp/php7 --without-iconv --enable-maintainer-zts --enable-debug --enable-cli` __!--!__
 4. Run `make clean`
 5. Run `make`
 6. Run `make install`

__!--!__ I chose to make a specific php7 directory, however if you have not installed FFP PHP5 then you may want to ignore the mkdir and use the prefix `/ffp` instead of `/ffp/php7`
