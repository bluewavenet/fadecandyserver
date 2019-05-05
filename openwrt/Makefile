include $(TOPDIR)/rules.mk

PKG_NAME:=fcserver
PKG_VERSION:=2.1.05
PKG_RELEASE:=1-beta

#PKG_REV:=0c39f05138b606e2bef6a29672b57793896e9126

#PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
#PKG_SOURCE_URL:=git://github.com/scanlime/fadecandy
#PKG_SOURCE_PROTO:=git
#PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
#PKG_SOURCE_VERSION:=$(PKG_REV)

PKG_SOURCE_URL:=https://codeload.github.com/bluewavenet/fadecandyserver/tar.gz/v$(PKG_VERSION)?
PKG_SOURCE:=fcserver-$(PKG_VERSION).tar.gz
PKG_HASH:= #shasum -a 256 of tar.gz of source files goes here
PKG_BUILD_DIR:=$(BUILD_DIR)/fcserver-$(PKG_VERSION)

PKG_MAINTAINER:=Rob White <rob@blue-wave.net>
PKG_BUILD_PARALLEL:=1
PKG_LICENSE:=MIT


#PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

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

#define Build/Compile
#	$(MAKE) -C $(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)/server \
#		CXX=$(TARGET_CC) \
#		CC="$(TARGET_CC) -fhonour-copts" \
#		STRIP_CMD="$(TARGET_STRIP) $(TARGET)"
#endef

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

$(eval $(call BuildPackage,fcserver,+libpthread +librt +uclibcxx +libstdcpp))
