#
# Copyright (C) 2009-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# The newer versions require new kernel

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=oprofile_legacy
PKG_VERSION:=0.9.9
PKG_RELEASE:=1

PKG_SOURCE:=oprofile-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/oprofile
PKG_HASH:=00aec1287da2dfffda17a9b1c0a0186800aec1287da2dfffda17a9b1c0a01868

PKG_BUILD_DIR:=$(KERNEL_BUILD_DIR)/oprofile-$(PKG_VERSION)

PKG_MAINTAINER:=Felix Fietkau <nbd@openwrt.org>

PKG_BUILD_DEPENDS:=binutils
PKG_LICENSE:=GPL-2.0+

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/oprofile_legacy
  SECTION:=devel
  CATEGORY:=Development
  TITLE:=OProfile System Profiler
  URL:=http://oprofile.sourceforge.net
  DEPENDS:=+libpopt +libstdcpp +objdump +librt @LINUX_2_6_22
endef

define Package/oprofile_legacy/description
 A transparent low-overhead system-wide profiler.
endef

define Package/oprofile-utils_legacy
  SECTION:=devel
  CATEGORY:=Development
  TITLE:=OProfile System Profiler (extra utilities)
  URL:=http://oprofile.sourceforge.net
  DEPENDS:=oprofile_legacy
endef

CONFIGURE_ARGS += \
	--disable-optimization \
	--disable-account-check \
	--enable-gui=no \
	--without-x

CONFIGURE_VARS += \
	ac_cv_lib_bfd_bfd_openr=no

TARGET_CXXFLAGS += -fpermissive

define Package/oprofile-utils_legacy/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/bin/opannotate \
		$(PKG_INSTALL_DIR)/opt/bin/oparchive \
		$(PKG_INSTALL_DIR)/opt/bin/opgprof \
		$(1)/opt/bin
endef

define Package/oprofile_legacy/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/bin/* \
		$(1)/opt/bin

	rm -f \
		$(1)/opt/bin/opannotate \
		$(1)/opt/bin/oparchive \
		$(1)/opt/bin/opgprof

	$(INSTALL_DIR) $(1)/opt/lib/oprofile
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/oprofile/*.so* \
		$(1)/opt/lib/oprofile

	$(INSTALL_DIR) $(1)/opt/share/oprofile
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/share/oprofile/stl.pat \
		$(PKG_INSTALL_DIR)/opt/share/oprofile/$(patsubst x86,i386,$(LINUX_KARCH)) \
		$(1)/opt/share/oprofile
endef

$(eval $(call BuildPackage,oprofile_legacy))
$(eval $(call BuildPackage,oprofile-utils_legacy))
