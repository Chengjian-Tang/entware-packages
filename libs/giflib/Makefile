#
# Copyright (C) 2006-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=giflib
PKG_VERSION:=5.1.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=@SF/giflib
PKG_HASH:=76c0a084c3b02f9315ff937b8be6096186002fea26f33e2123081ba2be6e2a7c

PKG_MAINTAINER:=Ted Hess <thess@kitschensync.net>

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf
PKG_REMOVE_FILES:=autogen.sh aclocal.m4

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/giflib
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=GIF libraries
  URL:=http://sourceforge.net/projects/giflib
endef

define Package/giflib/description
  giflib is a library for reading and writing gif images.
  It is API and ABI compatible with libungif which was in wide use while
  the LZW compression algorithm was patented.
endef

TARGET_CFLAGS += $(FPIC)

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/{lib,include}
	$(CP) $(PKG_BUILD_DIR)/lib/.libs/lib*so* $(1)/opt/lib
	$(CP) $(PKG_BUILD_DIR)/lib/.libs/libgif.a $(1)/opt/lib
	$(CP) $(PKG_BUILD_DIR)/lib/libgif.la $(1)/opt/lib
	$(CP) $(PKG_BUILD_DIR)/lib/*.h $(1)/opt/include/
endef

define Package/giflib/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_BUILD_DIR)/lib/.libs/lib*so* $(1)/opt/lib/
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,giflib))
