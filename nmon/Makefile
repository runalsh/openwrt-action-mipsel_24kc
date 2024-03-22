include $(TOPDIR)/rules.mk

PKG_NAME:=nmon
PKG_VERSION:=16p
PKG_RELEASE:=1.0

PKG_LICENSE:=GPL-3.0

include $(INCLUDE_DIR)/package.mk

define Package/nmon
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Nmon linux performance monitoring tool
	MAINTAINER:=sameeruddin shaik <sameeruddin.shaik8@gmail.com>
	DEPENDS:=+libncurses
	URL:=https://sourceforge.net/projects/nmon/
	FILES:=$(PKG_BUILD_DIR)/lmon16p.c
endef

TARGET_LDFLAGS+= -lncurses

define Package/nmon/description
 nmon is short for Nigel\'s Performance Monitor It either shows you the stats on-screen updating once a second or saves the data to a CSV file for later analysis and graphing.
endef
 
define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	cp -fpR lmon16p.c $(PKG_BUILD_DIR)/
	for patch in `ls patches/*`; do \
		patch -d $(PKG_BUILD_DIR)/ -F3 -t -p0 -i "$$$$(pwd)/$$$${patch}"; \
	done
	cp -f Makefile $(PKG_BUILD_DIR)
endef

define Build/Compile
	$(TARGET_CC) $(TARGET_CPPFLAGS) $(TARGET_CFLAGS)  -o $(PKG_BUILD_DIR)/nmon  $(PKG_BUILD_DIR)/lmon16p.c $(TARGET_LDFLAGS)
endef

define Package/nmon/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/nmon $(1)/usr/sbin/nmon
endef

$(eval $(call BuildPackage,nmon))