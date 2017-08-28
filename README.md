# WI-FAB packages feed

## Description

This is an OpenWrt/LEDE [package feed](https://wiki.openwrt.org/doc/devel/feeds) containing cryptographic and wireless networking packages, used for [WI-FAB](http://www.recred.eu/sites/default/files/1570287769.pdf), an attribute-based WLAN access control, without pre-shared keys and backend infrastructure.

## Usage

To use these packages, add the following line to the feeds.conf
in the OpenWrt/LEDE buildroot:

```
  src-git wifab https://github.com/netgroup/wifab-openwrt.git
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

