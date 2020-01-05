#
# Copyright (C) 2006-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# 4.15 and newer requres DM_* includes, which is absent in 2.6.22

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=strace_legacy
PKG_VERSION:=4.14
PKG_RELEASE:=1

PKG_SOURCE:=strace-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@SF/$(PKG_NAME)
PKG_HASH:=5bed5110b243dce6864bedba269446c18c8c63f553cdd7fd4f808d89a764712f

PKG_BUILD_DIR:=$(KERNEL_BUILD_DIR)/strace-$(PKG_VERSION)

PKG_LICENSE:=BSD-3c
PKG_LICENSE_FILES:=COPYRIGHT
PKG_CPE_ID:=cpe:/a:paul_kranenburg:strace

PKG_MAINTAINER:=Felix Fietkau <nbd@nbd.name>

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

PKG_CONFIG_DEPENDS:= \
	CONFIG_STRACE_LEGACY_LIBUNWIND

include $(INCLUDE_DIR)/package.mk

HOST_CFLAGS += -I$(LINUX_DIR)/user_headers/include

CONFIGURE_VARS+= \
	LDFLAGS_FOR_BUILD="$(HOST_LDFLAGS)" \
	CPPFLAGS_FOR_BUILD="$(HOST_CPPFLAGS)" \
	CFLAGS_FOR_BUILD="$(HOST_CFLAGS)" \
	CC_FOR_BUILD="$(HOST_CC)"

define Package/strace_legacy
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=System call tracer
  DEPENDS:=+STRACE_LEGACY_LIBUNWIND:libunwind @LINUX_2_6_22
  URL:=http://strace.sourceforge.net/
  PROVIDES:=strace
endef

define Package/strace_legacy/description
A useful diagnostic, instructional, and debugging tool. Allows you to track what
system calls a program makes while it is running.
endef

define Package/strace_legacy/config
choice
	prompt "stack tracing support"
	default STRACE_LEGACY_NONE
	depends on LINUX_2_6_22

	config STRACE_LEGACY_NONE
		bool "None"
		depends on LINUX_2_6_22

	config STRACE_LEGACY_LIBUNWIND
		bool "libunwind (experimental)"
		depends on LINUX_2_6_22
endchoice
endef

CONFIGURE_ARGS += \
	--with-libunwind=$(if $(CONFIG_STRACE_LIBUNWIND),yes,no)

TARGET_CFLAGS += -I$(LINUX_DIR)/user_headers/include

MAKE_FLAGS := \
	CCOPT="$(TARGET_CFLAGS)"

define Package/strace_legacy/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/strace $(1)/opt/bin/
endef

$(eval $(call BuildPackage,strace_legacy))
