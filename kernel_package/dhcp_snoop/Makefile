#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=dhcp_snoop
PKG_RELEASE:=1
PKG_VERSION:=1.0

PKG_SOURCE_URL:=https://github.com/JagadeeshPagadala/dhcp_snoop_vlan.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
#PKG_SOURCE_VERSION:=aaf953e1baf9cd65979103c4fda98c0bd48f4759
PKG_SOURCE:=https://codeload.github.com/JagadeeshPagadala/dhcp_snoop_vlan/zip/master

include $(INCLUDE_DIR)/package.mk

define KernelPackage/dhcp_snoop
  SUBMENU:=Network
  TITLE:=DHCP Snooping
  FILES:=$(PKG_BUILD_DIR)/dhcp_snoop_IP_spoof.ko
  FILES:=$(PKG_BUILD_DIR)/dhcp_snoop.ko
  AUTOLOAD:=$(call AutoLoad,50,dhcp_snoop)
endef

define KernelPackage/dhcp_snoop/description
 Kernel module for dhcp snooping 
endef

MAKE_OPTS:= \
	ARCH="$(LINUX_KARCH)" \
	CROSS_COMPILE="$(TARGET_CROSS)" \
	SUBDIRS="$(PKG_BUILD_DIR)" \
	EXTRA_CFLAGS="$(EXTRA_CFLAGS)" \
	$(EXTRA_KCONFIG)

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		$(MAKE_OPTS) \
		modules
endef

$(eval $(call KernelPackage,dhcp_snoop))
