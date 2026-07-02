include $(TOPDIR)/rules.mk

PKG_NAME:=daed
PKG_VERSION:=2026.07.02
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/daeuniverse/daed.git
PKG_SOURCE_VERSION:=main

PKG_LICENSE:=AGPL-3.0
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/daed
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Web Servers/Proxies
  TITLE:=A modern dashboard for dae based on eBPF
  URL:=https://github.com/daeuniverse/daed
  DEPENDS:=+dae +ip-full +kmod-xdp +kmod-tun +libbpf
endef

define Package/daed/description
  DAE is a Linux high-performance transparent proxy solution based on eBPF.
  And DAED is a modern dashboard for dae.
endef

define Build/Compile
	# eBPF/Go 编译由独立工具链或预编译提取处理，此处主要进行结构打包
endef

define Package/daed/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DIR) $(1)/etc/hotplug.d/iface

	$(INSTALL_BIN) ./files/daed.init $(1)/etc/init.d/daed
	$(INSTALL_CONF) ./files/daed.config $(1)/etc/config/daed
	$(INSTALL_BIN) ./files/98-daed $(1)/etc/hotplug.d/iface/98-daed
endef

$(eval $(call BuildPackage,daed))
