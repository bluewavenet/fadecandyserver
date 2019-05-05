include $(TOPDIR)/rules.mk

PKG_NAME:=fadecandyserver
PKG_VERSION:=2.1.05
PKG_RELEASE:=1-beta

PKG_SOURCE_URL:=https://codeload.github.com/bluewavenet/fadecandyserver/tar.gz/v$(PKG_VERSION)?
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
#PKG_HASH:= #shasum -a 256 of tar.gz of source files goes here
PKG_HASH:= 39b3dd49cbf61c29689d35d0479afd96ceb2719f718cc8c8261ff3c3ed2df681
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_MAINTAINER:=Rob White <rob@blue-wave.net>
PKG_BUILD_PARALLEL:=1
PKG_LICENSE:=MIT


include $(INCLUDE_DIR)/package.mk

define Package/fadecandyserver
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=FadeCandy Server
	URL:=https://github.com/scanlime/fadecandy
	DEPENDS:=+libpthread +librt +uclibcxx +libstdcpp +libc 
endef

define Package/fadecandyserver/description
	FadeCandy Server For OpenWrt.
	The Fadecandy Server is a background process that handles
	USB communications with one or more Fadecandy LED Controller boards.
endef

define Package/fadecandyserver/install
	$(INSTALL_DIR) $(1)/usr
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/fcserver $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/openwrt/etc/fcserver.config $(1)/etc/
	$(CP) $(PKG_BUILD_DIR)/openwrt/etc/init.d/fcserver $(1)/etc/init.d/
endef

define Package/fadecandyserver/postinst
	#!/bin/sh
	echo "Enabling autostart for Fadecandy Server"
	/etc/init.d/fcserver enable
	exit 0
endef

$(eval $(call BuildPackage,fadecandyserver))
