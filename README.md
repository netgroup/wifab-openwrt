# WI-FAB packages feed

## Description

This is an OpenWrt/LEDE [package feed](https://wiki.openwrt.org/doc/devel/feeds) containing cryptographic and wireless networking packages.

## Usage

To use these packages, add the following line to the feeds.conf
in the OpenWrt/LEDE buildroot:

```
  src-git wifab git://github.com/netgroup/openwrt-lede-wifab.git
```
  
Update the feed:

```
  ./scripts/feeds update wifab
```
  
Activate the package:

```
  ./scripts/feeds install -a -p wifab -f
```
  
The new packages should now appear in menuconfig.

