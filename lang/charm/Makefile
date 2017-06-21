#
# Copyright (C) 2007-2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=charm
PKG_VERSION:=0.50
PKG_RELEASE:=1

#https://github.com/JHUISI/charm/archive/2.7-dev.zip
PKG_SOURCE:=2.7-dev.zip
PKG_SOURCE_URL:=http://127.0.0.1:8000/
PKG_MD5SUM:=4afb9a3b24af6b4c1aa8847ff78e894c 
PKG_MAINTAINER:=Claudio Pisa <claudio.pisa@uniroma2.it>
PKG_DEPENDS:=+libgmp +pbc +libopenssl +python-pyparsing

# include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

#PKG_BUILD_DIR:=$(BUILD_DIR)/Charm-Crypto-$(PKG_VERSION)

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

#CONFIGURE_ARGS += --with-pbc-lib=$(BUILD_DIR)/pbc-0.5.14/
#CONFIGURE_ARGS += --with-pbc-include=$(BUILD_DIR)/pbc-0.5.14/include/ 
#CONFIGURE_ARGS += --with-bswabe-include=$(BUILD_DIR)/libbswabe-0.9/ 
#CONFIGURE_ARGS += --with-bswabe-lib=$(BUILD_DIR)/libbswabe-0.9/ 

#define Build/Configure
#  $(call Build/Configure/Default, --with-pbc-lib=$(BUILD_DIR)/pbc-0.5.14/.libs/ --with-pbc-include=$(BUILD_DIR)/pbc-0.5.14/include/ --with-bswabe-include=$(BUILD_DIR)/libbswabe-0.9/ --with-bswabe-lib=$(BUILD_DIR)/libbswabe-0.9/)
#endef

define Build/Prepare
	$(PKG_UNPACK)
	rmdir $(BUILD_DIR)/charm-$(PKG_VERSION)
	mv $(BUILD_DIR)/charm-2.7-dev $(BUILD_DIR)/charm-$(PKG_VERSION)
	$(Build/Patch)
	cd $(PKG_BUILD_DIR) && ./configure.sh --cpu=arm --prefix=$(1) --extra-cflags="-I$(BUILD_DIR)/pbc-0.5.14/include/"
	mkdir -p $(PKG_BUILD_DIR)/build/lib.linux2-2.7
	ln -s $(STAGING_DIR)/usr/lib/python2.7/setuptools $(PKG_BUILD_DIR)/build/lib.linux2-2.7/setuptools
endef

#define Build/Prepare
#	$(Build/Prepare/Default)
#	cd $(PKG_BUILD_DIR)
#	#sed -i '/GMP_4_0_CHECK/d' $(PKG_BUILD_DIR)/configure.ac
#	tar xf $(PKG_BUILD_DIR)/pbc-0.5.14.tar.gz -C $(PKG_BUILD_DIR)
#	cd $(PKG_BUILD_DIR)/pbc-0.5.14/ && ./configure
#	cd $(PKG_BUILD_DIR)/pbc-0.5.14/ && make
#	cd $(PKG_BUILD_DIR)/ && ./configure --with-pbc-lib=$(PKG_BUILD_DIR)/pbc-0.5.14/.libs/ --with-pbc-include=$(PKG_BUILD_DIR)/pbc-0.5.14/include/ --with-bswabe-include=$(PKG_BUILD_DIR)/libbswabe-0.9/ --with-bswabe-lib=$(PKG_BUILD_DIR)/libbswabe-0.9/ 
#endef

#define Build/Compile
#	cd $(PKG_BUILD_DIR)/ && ./configure --with-pbc-lib=$(PKG_BUILD_DIR)/pbc-0.5.14/.libs/ --with-pbc-include=$(PKG_BUILD_DIR)/pbc-0.5.14/include/ --with-bswabe-include=$(PKG_BUILD_DIR)/libbswabe-0.9/ --with-bswabe-lib=$(PKG_BUILD_DIR)/libbswabe-0.9/ 
#	make
#endef

define Build/Compile
	$(call Build/Compile/PyMod,,build)
endef

define Package/charm/install
	# $(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	# $(CP) \
	#     $(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
	#     $(1)$(PYTHON_PKG_DIR)
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(call Build/Compile/PyMod,,install --prefix=/usr --root=$(1))
	#cd $(PKG_BUILD_DIR) && python setup.py install --prefix=/usr --root=$(1)
endef

#define Package/charm/install
#	$(INSTALL_DIR) $(1)/usr/bin
#	$(INSTALL_BIN) $(PKG_BUILD_DIR)/cpabe-dec    $(1)/usr/bin/
#	$(INSTALL_BIN) $(PKG_BUILD_DIR)/cpabe-enc    $(1)/usr/bin/
#	$(INSTALL_BIN) $(PKG_BUILD_DIR)/cpabe-keygen $(1)/usr/bin/
#	$(INSTALL_BIN) $(PKG_BUILD_DIR)/cpabe-setup  $(1)/usr/bin/
#endef

$(eval $(call BuildPackage,charm))

