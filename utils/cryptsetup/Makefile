#
# Copyright (C) 2006-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cryptsetup
PKG_VERSION:=1.7.5
PKG_RELEASE:=1
PKG_LICENSE:=GPL-2.0+ LGPL-2.1+
PKG_LICENSE_FILES:=COPYING COPYING.LGPL

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@KERNEL/linux/utils/cryptsetup/v1.7
PKG_HASH:=2b30cd1d0dd606a53ac77b406e1d37798d4b0762fa89de6ea546201906a251bd
PKG_MAINTAINER:=Daniel Golle <daniel@makrotopia.org>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(BUILD_VARIANT)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

TARGET_LDFLAGS+=-Wl,-rpath-link=$(STAGING_DIR)/opt/lib

define Package/cryptsetup/Default
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Encryption
  TITLE:=Cryptsetup
  DEPENDS:=+libblkid +libuuid +libpopt +libdevmapper
  URL:=http://code.google.com/p/cryptsetup/
endef

define Package/cryptsetup
$(call Package/cryptsetup/Default)
  DEPENDS+=+libgcrypt
  VARIANT:=gcrypt
endef

define Package/cryptsetup-openssl
$(call Package/cryptsetup/Default)
  TITLE+= (with openssl support)
  DEPENDS+=+libopenssl
  VARIANT:=openssl
endef

define Package/cryptsetup/Default/description
	Cryptsetup-luks
endef

define Package/cryptsetup/description
$(call Package/cryptsetup/Default/description)
linked against libgcrypt
endef


define Package/cryptsetup-openssl/description
$(call Package/cryptsetup/Default/description)
linked against openssl
endef

ifeq ($(CONFIG_LINUX_2_6_36),y)
CONFIGURE_ARGS+= \
	--disable-kernel_crypto
endif

ifeq ($(BUILD_VARIANT),openssl)
CONFIGURE_ARGS+= \
        --with-crypto_backend=openssl
endif

define Package/cryptsetup/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(CP) $(PKG_BUILD_DIR)/src/.libs/cryptsetup $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_BUILD_DIR)/lib/.libs/libcryptsetup.so* $(1)/opt/lib
endef

Package/cryptsetup-openssl/install = $(Package/cryptsetup/install)

$(eval $(call BuildPackage,cryptsetup))
$(eval $(call BuildPackage,cryptsetup-openssl))
