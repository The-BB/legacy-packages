#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Can't be upgraded, we've got too old kernel
#

include $(TOPDIR)/rules.mk

PKG_NAME:=bluez3-utils
PKG_VERSION:=3.36
PKG_RELEASE:=12

PKG_SOURCE:=bluez-utils-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://bluez.sourceforge.net/download
PKG_HASH:=5704737aaf72104eeaf77335218a18275704737aaf72104eeaf77335218a1827

PKG_BUILD_DIR:=$(BUILD_DIR)/bluez-utils-$(PKG_VERSION)

PKG_FIXUP:=autoreconf

PKG_CHECK_FORMAT_SECURITY:=0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/bluez3-utils
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+bluez3-libs +libpthread +dbus $(INTL_DEPENDS) $(ICONV_DEPENDS) @LINUX_2_6_22
  TITLE:=Bluetooth utilities
  URL:=http://www.bluez.org/
endef

define Package/bluez-utils/conffiles
/opt/etc/bluetooth/hcid.conf
/opt/etc/bluetooth/rfcomm.conf
/opt/etc/config/bluetooth
endef

CONFIGURE_ARGS += \
	--disable-glib \
	--enable-pand \
	--enable-rfcomm \
	--enable-dund \
	--enable-serial \
	--enable-network \
	--enable-usb \
	--enable-input \
	--disable-audio \
	--with-bluez="$(STAGING_DIR)/opt/include" \
	--with-usb=yes \

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		LDFLAGS="$(TARGET_LDFLAGS) \
			-L$(ICONV_PREFIX)/lib \
			-L$(INTL_PREFIX)/lib -lm" \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

define Package/bluez3-utils/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/sbin
	$(CP) $(PKG_INSTALL_DIR)/opt/sbin/* $(1)/opt/sbin/
	$(INSTALL_DIR) $(1)/opt/etc/bluetooth
	$(CP) $(PKG_INSTALL_DIR)/opt/etc/bluetooth/hcid.conf $(1)/opt/etc/bluetooth/
	$(CP) $(PKG_INSTALL_DIR)/opt/etc/bluetooth/rfcomm.conf $(1)/opt/etc/bluetooth/
	$(INSTALL_DIR) $(1)/opt/etc/dbus-1/system.d/
	$(INSTALL_DATA) ./files/bluetooth.dbus $(1)/opt/etc/dbus-1/system.d/bluetooth.conf
endef

$(eval $(call BuildPackage,bluez3-utils))
