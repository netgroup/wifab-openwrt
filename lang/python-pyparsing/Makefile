#
# Copyright (C) 2017 Claudio Pisa <claudio.pisa@uniroma2.it>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=python-pyparsing
PKG_VERSION:=2.2.0
PKG_RELEASE:=1

PKG_SOURCE:=pyparsing-2.2.0.tar.gz
PKG_SOURCE_URL:=https://freefr.dl.sourceforge.net/project/pyparsing/pyparsing/pyparsing-2.2.0/
PKG_MD5SUM:=0214e42d63af850256962b6744c948d9

PKG_BUILD_DIR:=$(BUILD_DIR)/pyparsing-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/python-pyparsing
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=General parsing module for Python
  URL:=http://pyparsing.wikispaces.com/
  DEPENDS:=+python-setuptools
endef

define Package/python-pyparsing/description
  General parsing module for Python
endef

define Build/Compile
	$(call Build/Compile/PyMod,,install --prefix=/usr --root=$(PKG_INSTALL_DIR))
endef

define PyPackage/python-pyparsing/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(CP) \
	    $(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
	    $(1)$(PYTHON_PKG_DIR)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(PYTHON_LIB_DIR)
	$(CP) \
		$(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
		$(PYTHON_LIB_DIR)
endef

define PyPackage/python-pyparsing/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(CP) \
	    $(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
	    $(1)$(PYTHON_PKG_DIR)
endef

$(eval $(call PyPackage,python-pyparsing))
$(eval $(call BuildPackage,python-pyparsing))

