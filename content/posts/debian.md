---
title: Debian
date: 2017-12-23T17:57:02
tags: [ public ]
guid: 53432697-6ee0-4c34-b37c-dd99c002b5e9
---


<!--more-->

 * Why is a package installed: `aptitude why $package`
 * What versions could be / are installed: `apt-cache policy $package`
 * List contents of package: `dpkg -L $package`
 * List contents of package on disk: `dpkg-deb --contents $deb`
 * Extract contents of package on disk: `dpkg-deb --raw-extract $deb t'$dir`
 * Leave out a file from a package: `dpkg-divert --divert /etc/init/filebeat.conf --rename /etc/init/filebeat.disabled`

## How to Pull Some Packages From Sid

(h/t Ryan Voots)

`sources.list`:

```
deb http://ftp.us.debian.org/debian/ jessie main contrib non-free
deb-src http://ftp.us.debian.org/debian/ jessie main contrib non-free

deb http://security.debian.org/ jessie/updates main contrib non-free
deb-src http://security.debian.org/ jessie/updates main contrib non-free

deb http://ftp.us.debian.org/debian/ jessie-updates main contrib non-free
deb-src http://ftp.us.debian.org/debian/ jessie-updates main contrib non-free

deb http://ftp.us.debian.org/debian/ jessie-backports main contrib non-free
deb-src http://ftp.us.debian.org/debian/ jessie-backports main contrib non-free

#deb http://http.us.debian.org/debian/ sid main contrib non-free
#deb-src http://http.us.debian.org/debian/ sid main contrib non-free
deb http://repo.varnish-cache.org/debian/ jessie varnish-3.0
```


`/etc/apt/preferences`:

```
package: *
pin: release n=jessie
pin-Priority: 1000

package: *
pin: release n=jessie-updates
pin-Priority: 1001

package: *
pin: release n=jessie-backports
pin-Priority: 1002

package: *
pin: release n=sid
pin-Priority: 100
```


`/etc/apt/preferences.d/git`:
```
package: git git-man git-daemon-run gitweb git-doc git-el git-email git-gui gitk git-arch git-cvs git-mediawiki git-svn
pin: release n=sid
pin-Priority: 1010
```
