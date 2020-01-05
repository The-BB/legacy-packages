
include $(TOPDIR)/rules.mk

PKG_NAME:=libnsl
PKG_VERSION:=1.2.0
PKG_RELEASE:=1
PKG_REV:=113d92f29bcb778fcaa9c2a18e48bce53729ea54

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/thkukuk/$(PKG_NAME).git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_PROTO:=git

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/libnsl
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=contains the public client interface for NIS(YP) and NIS+
  URL:=https://github.com/thkukuk/libnsl
  DEPENDS:=+libtirpc $(INTL_DEPENDS) @USE_UCLIBC
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/* $(1)/opt/include/

	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libnsl.{a,so*} $(1)/opt/lib/

	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/*.pc $(1)/opt/lib/pkgconfig/
endef

define Package/libnsl/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libnsl.so.* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,libnsl))
