#
# Copyright (C) 2023 OpenWrt
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=websocat
PKG_VERSION:=1.13.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/vi/websocat.git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/websocat
  SECTION:=net
  CATEGORY:=Network
  TITLE:=WebSocket to WebSocket and other protocol bridge
  URL:=https://github.com/vi/websocat
endef

define Package/websocat/description
  Websocat is a command-line client for WebSockets, like netcat but for WebSockets.
endef

define Build/Configure
	$(call Build/Configure/Default)
endef

define Build/Compile
	# Ensure Rust is configured to build static binaries
	cd $(PKG_BUILD_DIR) && \
	cargo build --release --target $(TARGET_CC_ARCH) --target-dir $(PKG_BUILD_DIR)/target --bin websocat
endef

define Package/websocat/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/target/$(TARGET_CC_ARCH)/release/websocat $(1)/usr/bin/
endef

$(eval $(call BuildPackage,websocat))

