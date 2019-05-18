include $(TOPDIR)/rules.mk

PKG_NAME:=fadecandyserver
PKG_VERSION:=2.1.05
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://codeload.github.com/bluewavenet/fadecandyserver/tar.gz/v$(PKG_VERSION)?
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
#PKG_HASH:= #shasum -a 256 of tar.gz of source files goes here
PKG_HASH:= 082fbeaed40fd23afba4abfabde8a6c31809508866bf3b05cb50578606828908
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
	USB communications with Fadecandy LED Controller boards.
	Pixel data can be sent to a Fadecandy Server over the Open Pixel Control protocol,
	or from a web app via WebSockets.

	* Support multiple Fadecandy boards
	* Mix Fadecandy and DMX lighting devices
	* Listen on a configurable TCP port
	* Listen for connections from the network, not just from local programs

	This package contains the FadeCandy fcserver utility. 
endef

define Package/fadecandyserver/install
	$(INSTALL_DIR) $(1)/usr
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/fcserver $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/openwrt/etc/initd/fadecandyserver $(1)/etc/init.d/
	$(CP) $(PKG_BUILD_DIR)/openwrt/etc/config/fadecandyserver $(1)/etc/config/
endef

define Package/fadecandyserver/postinst
	#!/bin/sh
	echo "Enabling autostart for Fadecandy Server"
	/etc/init.d/fcserver enable
	exit 0
endef

$(eval $(call BuildPackage,fadecandyserver))
