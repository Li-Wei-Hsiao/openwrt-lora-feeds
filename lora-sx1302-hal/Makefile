#
# Copyright (C) 2023 Leo Hsiao <leo@asiarf.com>
#
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lora-sx1302-hal
PKG_VERSION:=2.1.0
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://codeload.github.com/Lora-net/sx1302_hal/tar.gz/V$(PKG_VERSION)?
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_HASH:=1a0447d5e8183d08e6dce5f739f6872b9c57824b98f4078830d5ee21b15782c1

#PKG_MAINTAINER:=Leo Hsiao <leo@asiarf.com>
#PKG_LICENSE_FILES:=LICENSE
PKG_BUILD_DIR:=$(BUILD_DIR)/sx1302_hal-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libsx1302
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Driver/HAL library for Semtech SX1302
  URL:=https://www.semtech.com/products/wireless-rf/lora-gateways/sx1302
  DEPENDS:=+kmod-spi-dev
endef

define Package/libloragw-tests
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=LoRa-sx1302_hal
  TITLE:=Test programs for libloragw to check functionality
  DEPENDS:=libloragw
endef

define Package/libloragw-utils
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=LoRa-sx1302_hal
  TITLE:=Utility programs for libloragw
  DEPENDS:=libloragw
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/libloragw
	$(CP) $(PKG_BUILD_DIR)/libloragw/inc/loragw_* $(1)/usr/include/libloragw
	$(CP) $(PKG_BUILD_DIR)/libloragw/inc/sx1250_* $(1)/usr/include/libloragw
	$(CP) $(PKG_BUILD_DIR)/libloragw/inc/sx125x_* $(1)/usr/include/libloragw
	$(CP) $(PKG_BUILD_DIR)/libloragw/inc/sx1261_* $(1)/usr/include/libloragw
  $(CP) $(PKG_BUILD_DIR)/libloragw/config.h $(1)/usr/include/libloragw

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libloragw/libloragw.so* $(1)/usr/lib/
	$(LN) libloragw.so.0 $(1)/usr/lib/libloragw.so
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_BUILD_DIR)/loragw.pc  $(1)/usr/lib/pkgconfig/
endef

define Package/libloragw/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libloragw/libloragw.so.* $(1)/usr/lib/
endef

define Package/libloragw-tests/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libloragw/test* $(1)/usr/sbin
endef

define Package/libloragw-utils/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/util_net_downlink $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/util_chip_id $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/util_boot $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/util_spectral_scan $(1)/usr/sbin

endef

#$(eval $(call BuildPackage,libsx1302))

$(eval $(call BuildPackage,libloragw))
$(eval $(call BuildPackage,libloragw-tests))
$(eval $(call BuildPackage,libloragw-utils))
