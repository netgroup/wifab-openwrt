#
# Copyright (C) 2017 Claudio Pisa <claudio.pisa@uniroma2.it>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=charm
PKG_VERSION:=0.50
PKG_RELEASE:=1

PKG_SOURCE:=2.7-dev.zip
PKG_SOURCE_URL:=https://github.com/JHUISI/charm/archive/2.7-dev.zip
PKG_MD5SUM:=4afb9a3b24af6b4c1aa8847ff78e894c 
PKG_MAINTAINER:=Claudio Pisa <claudio.pisa@uniroma2.it>
PKG_DEPENDS:=+libgmp +pbc +libopenssl +python-pyparsing

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/charm
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=charm
  URL:=https://github.com/JHUISI/charm
  DEPENDS:=+libgmp +pbc +libopenssl +python-pyparsing
  PKG_BUILD_DEPENDS:=+python-setuptools +python-pyparsing
endef

define Package/charm/description
 charming cpabe
endef

define Build/Prepare
	$(PKG_UNPACK)
	rmdir $(BUILD_DIR)/charm-$(PKG_VERSION)
	mv $(BUILD_DIR)/charm-2.7-dev $(BUILD_DIR)/charm-$(PKG_VERSION)
	$(Build/Patch)
	cd $(PKG_BUILD_DIR) && ./configure.sh --cpu=arm --prefix=$(1) --extra-cflags="-I$(BUILD_DIR)/pbc-0.5.14/include/"
	mkdir -p $(PKG_BUILD_DIR)/build/lib.linux2-2.7
	ln -s $(STAGING_DIR)/usr/lib/python2.7/setuptools $(PKG_BUILD_DIR)/build/lib.linux2-2.7/setuptools
endef

define Build/Compile
	$(call Build/Compile/PyMod,,build)
endef

define Package/charm/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(call Build/Compile/PyMod,,install --prefix=/usr --root=$(1))
endef

$(eval $(call BuildPackage,charm))

