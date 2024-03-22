include $(TOPDIR)/rules.mk

PKG_NAME:=Nmon
PKG_VERSION:=16c
PKG_RELEASE:=1.0

PKG_LICENSE:=GPL-3.0
PKG_MAINTAINER:=sameeruddin shaik <sameeruddin.shaik8@gmail.com>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)
PKG_SOURCE:=lmon$(PKG_VERSION).c


include $(INCLUDE_DIR)/package.mk

define Package/Nmon
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Nmon linux performance monitoring tool
	DEPENDS:=+libncurses 
	URL:=https://sourceforge.net/projects/nmon/
	FILES:=$(PKG_BUILD_DIR)/$(PKG_SOURCE)
endef

TARGET_LDFLAGS+= -lncurses

define Package/Nmon/description
 nmon is short for Nigel\'s Performance Monitor It either shows you the stats on-screen updating once a second or saves the data to a CSV file for later analysis and graphing.
endef
 
define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) $(TOPDIR)/dl/$(PKG_SOURCE) $(PKG_BUILD_DIR)/
	$(CP) -fpR patches/ $(PKG_BUILD_DIR)/
	cd $(PKG_BUILD_DIR)/; quilt push -a
endef

define Build/Compile
	$(TARGET_CC) $(TARGET_CPPFLAGS) $(TARGET_CFLAGS)  -o $(PKG_BUILD_DIR)/nmon  $(PKG_BUILD_DIR)/lmon16j.c $(TARGET_LDFLAGS)
endef

define Package/Nmon/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/nmon $(1)/usr/sbin/nmon
endef

$(eval $(call BuildPackage,Nmon))