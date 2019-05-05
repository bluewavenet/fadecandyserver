include $(TOPDIR)/rules.mk

PKG_NAME:=fcserver
PKG_VERSION:=2.1.05
PKG_RELEASE:=1-beta

PKG_SOURCE_URL:=https://codeload.github.com/bluewavenet/fadecandyserver/tar.gz/v$(PKG_VERSION)?
PKG_SOURCE:=fadecandyserver-$(PKG_VERSION).tar.gz
#PKG_HASH:= #shasum -a 256 of tar.gz of source files goes here
PKG_HASH:= 650fe40e8e43343988c9263f19ea7a813dbbf69c76939674b897e2e8c974138c
PKG_BUILD_DIR:=$(BUILD_DIR)/fcserver-$(PKG_VERSION)

PKG_MAINTAINER:=Rob White <rob@blue-wave.net>
PKG_BUILD_PARALLEL:=1
PKG_LICENSE:=MIT


include $(INCLUDE_DIR)/package.mk

define Package/fcserver
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=FadeCandy Server
	URL:=https://github.com/scanlime/fadecandy
	DEPENDS:=+libpthread +librt +uclibcxx +libstdcpp +libc 
endef

define Package/fcserver/description
	FadeCandy Server For OpenWrt.
	The Fadecandy Server is a background process that handles
	USB communications with one or more Fadecandy LED Controller boards.
endef

define Package/fcserver/install
	$(INSTALL_DIR) $(1)/usr
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/fcserver $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/openwrt/files/etc/fcserver.config $(1)/etc/
	$(CP) $(PKG_BUILD_DIR)/openwrt/files/etc/init.d/fcserver $(1)/etc/init.d/
endef

define Package/fcserver/postinst
	#!/bin/sh
	echo "Enabling autostart for Fadecandy Server"
	/etc/init.d/fcserver enable
	exit 0
endef

$(eval $(call BuildPackage,fcserver))
