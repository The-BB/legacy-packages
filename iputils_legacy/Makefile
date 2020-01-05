#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=iputils_legacy
PKG_VERSION:=20101006
PKG_RELEASE:=1

PKG_SOURCE:=iputils-s$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://www.skbuff.net/iputils
PKG_HASH:=fd3af46c80ebb99607c2ca1f2a3608b6fe828e25bbec6e54f2afd25f6ddb6ee7

PKG_MAINTAINER:=Jo-Philipp Wich <jo@mein.io>
PKG_LICENSE:=GPL-2.0+
PKG_CPE_ID:=cpe:/a:skbuff:iputils

PKG_BUILD_DEPENDS:=sysfsutils
PKG_BUILD_DIR:=$(BUILD_DIR)/iputils-s$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk


define Package/iputils_legacy/Default
  SECTION:=net
  CATEGORY:=Network
  URL:=http://www.skbuff.net/iputils
  PROVIDES:=iputils
  DEPENDS:=@LINUX_2_6_22
endef


define Package/iputils_legacy-arping
$(call Package/iputils_legacy/Default)
  TITLE:=iputils_legacy - arping
  DEPENDS+= +libsysfs
endef

define Package/iputils_legacy-arping/description
  Program arping from iputils.
  Sends ARP REQUEST to a neighbour host.
endef


define Package/iputils_legacy-clockdiff
$(call Package/iputils_legacy/Default)
  TITLE:=iputils_legacy - clockdiff
endef

define Package/iputils_legacy-clockdiff/description
  Program clockdiff from iputils.
  Measures clock difference between hosts.
endef


define Package/iputils_legacy-ping
$(call Package/iputils_legacy/Default)
  TITLE:=iputils_legacy - ping
endef

define Package/iputils_legacy-ping/description
  Program ping from iputils.
  Sends ICMP ECHO_REQUEST to network hosts (IPv4).
endef


define Package/iputils_legacy-ping6
$(call Package/iputils_legacy/Default)
  TITLE:=iputils_legacy - ping6
  DEPENDS+= @IPV6 +USE_GLIBC:libopenssl
endef

define Package/iputils_legacy-ping6/description
  Program ping6 from iputils.
  Sends ICMP ECHO_REQUEST to network hosts (IPv6).
endef


define Package/iputils_legacy-tftpd
$(call Package/iputils_legacy/Default)
  TITLE:=iputils_legacy - tftpd
endef

define Package/iputils_legacy-tftpd/description
  Program tftpd from iputils
  Trivial File Transfer Protocol server.
endef


define Package/iputils_legacy-tracepath
$(call Package/iputils_legacy/Default)
  TITLE:=iputils_legacy - tracepath
endef

define Package/iputils_legacy-tracepath/description
  Program tracepath from iputils.
  Traces path to a network host discovering MTU along this path (IPv4).
endef


define Package/iputils_legacy-tracepath6
$(call Package/iputils_legacy/Default)
  TITLE:=iputils_legacy - tracepath6
  DEPENDS+= @IPV6
endef

define Package/iputils_legacy-tracepath6/description
  Program tracepath6 from iputils.
  Traces path to a network host discovering MTU along this path (IPv6).
endef


define Package/iputils_legacy-traceroute6
$(call Package/iputils_legacy/Default)
  TITLE:=iputils_legacy - traceroute6
  DEPENDS+= @IPV6
endef

define Package/iputils_legacy-traceroute6/description
  Program traceroute6 from iputils.
  Traces path to a network host (IPv6).
endef

ifdef CONFIG_USE_MUSL
  TARGET_CFLAGS += -D__UCLIBC__
endif

MAKE_FLAGS += \
	CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS) $(TARGET_LDFLAGS)" \
	CONFIG_IPV6="$(CONFIG_IPV6)" \
	CONFIG_USE_UCLIBC="$(CONFIG_USE_UCLIBC)$(CONFIG_USE_MUSL)" \

define Package/iputils_legacy-arping/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/arping $(1)/opt/bin/
endef

define Package/iputils_legacy-clockdiff/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/clockdiff $(1)/opt/bin/
endef

define Package/iputils_legacy-ping/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ping $(1)/opt/bin/
endef

define Package/iputils_legacy-ping6/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ping6 $(1)/opt/bin/
endef

define Package/iputils_legacy-tftpd/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tftpd $(1)/opt/sbin/
endef

define Package/iputils_legacy-tracepath/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tracepath $(1)/opt/bin/
endef

define Package/iputils_legacy-tracepath6/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tracepath6 $(1)/opt/bin/
endef

define Package/iputils_legacy-traceroute6/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/traceroute6 $(1)/opt/bin/
endef

$(eval $(call BuildPackage,iputils_legacy-arping))
$(eval $(call BuildPackage,iputils_legacy-clockdiff))
$(eval $(call BuildPackage,iputils_legacy-ping))
$(eval $(call BuildPackage,iputils_legacy-tftpd))
$(eval $(call BuildPackage,iputils_legacy-tracepath))
$(eval $(call BuildPackage,iputils_legacy-ping6))
$(eval $(call BuildPackage,iputils_legacy-tracepath6))
$(eval $(call BuildPackage,iputils_legacy-traceroute6))
