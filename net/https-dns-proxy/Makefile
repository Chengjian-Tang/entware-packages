include $(TOPDIR)/rules.mk

PKG_NAME:=https_dns_proxy
PKG_VERSION:=2018-04-23
PKG_RELEASE=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_MIRROR_HASH:=24b7e4238c37e646f33eee3a374f6b7beb5c167b9c5008cc13b51e5f1f3a44ea
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/aarond10/https_dns_proxy/
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=bea68401330e611f6e9b75cec84e2dc4e81e52de
PKG_MAINTAINER:=Aaron Drew <aarond10@gmail.com>
PKG_LICENSE:=MIT

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/https_dns_proxy
  SECTION:=net
  CATEGORY:=Network
  TITLE:=DNS over HTTPS proxy server
  DEPENDS:=+libcares +libcurl +libev +ca-bundle
endef

define Package/https_dns_proxy/install
	$(INSTALL_DIR) $(1)/opt/sbin $(1)/opt/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/https_dns_proxy $(1)/opt/sbin/
	$(INSTALL_BIN) ./files/S09https_dns_proxy $(1)/opt/etc/init.d/
endef

$(eval $(call BuildPackage,https_dns_proxy))
