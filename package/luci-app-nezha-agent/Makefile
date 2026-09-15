include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-nezha-agent
PKG_VERSION:=1.2.0
PKG_RELEASE:=1
PKG_PO_VERSION:=$(PKG_VERSION)

PKG_LICENSE:=MIT Apache-2.0
PKG_MAINTAINER:=OpenWrt LuCI Community

# Modified for Marvell Avanta (ARMv5/xscale):
# The upstream package downloads the official prebuilt nezha-agent binary
# (linux_arm = ARMv7 only), which cannot run on this platform. The agent
# binary is instead provided by the self-built 'nezha-agent' package.

LUCI_TITLE:=LuCI support for Nezha Agent
LUCI_DEPENDS:=+luci-base +ca-bundle +nezha-agent

define Package/$(PKG_NAME)/postinst
#!/bin/sh
[ -n "$${IPKG_INSTROOT}" ] || {
	/etc/init.d/nezha-agent enable 2>/dev/null || true
	rm -f /tmp/luci-indexcache.* 2>/dev/null
	rm -rf /tmp/luci-modulecache 2>/dev/null
	killall -HUP rpcd 2>/dev/null || true
}
exit 0
endef

define Package/$(PKG_NAME)/prerm
#!/bin/sh
[ -n "$${IPKG_INSTROOT}" ] || {
	/etc/init.d/nezha-agent stop 2>/dev/null || true
	/etc/init.d/nezha-agent disable 2>/dev/null || true
}
exit 0
endef

define Package/$(PKG_NAME)/postrm
#!/bin/sh
[ -n "$${IPKG_INSTROOT}" ] || {
	rm -f /tmp/luci-indexcache.* 2>/dev/null
	rm -rf /tmp/luci-modulecache 2>/dev/null
	killall -HUP rpcd 2>/dev/null || true
	printf '%s\n' 'Nezha Agent configuration was retained.'
	printf '%s\n' 'Remove it manually if no longer needed:'
	printf '%s\n' '  rm -f /etc/config/nezha-agent /etc/config/nezha-agent-opkg'
	printf '%s\n' '  rm -rf /etc/nezha-agent'
}
exit 0
endef

include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature
