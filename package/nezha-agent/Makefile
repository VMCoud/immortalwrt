include $(TOPDIR)/rules.mk

PKG_NAME:=nezha-agent
PKG_VERSION:=2.3.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/nezhahq/agent/tar.gz/v$(PKG_VERSION)?
# codeload tarball top-level dir is "agent-$(PKG_VERSION)", not
# "nezha-agent-$(PKG_VERSION)"; tell the build system to rename it.
PKG_SOURCE_SUBDIR:=agent-$(PKG_VERSION)
PKG_HASH:=7be24650557baff43900338685436d321e8ff7c336e3149d127bd14b4c491af7

PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=msdos03 <jiconglu58@gmail.com>

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1

GO_PKG:=github.com/nezhahq/agent
GO_PKG_BUILD_PKG:=$(GO_PKG)/cmd/agent
GO_PKG_LDFLAGS_X:=$(GO_PKG)/pkg/monitor.Version=$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/nezha-agent
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Monitoring
  TITLE:=Nezha monitoring agent (self-built, ARMv5 compatible)
  URL:=https://github.com/nezhahq/agent
  DEPENDS:=$(GO_ARCH_DEPENDS)
endef

define Package/nezha-agent/description
  Nezha monitoring agent built from source for Marvell Avanta
  (ARMv5/xscale) targets. The official prebuilt linux_arm binary
  is ARMv7-only and cannot run on this platform.
endef

define Package/nezha-agent/install
	$(call GoPackage/Package/Install/Bin,$(PKG_INSTALL_DIR))
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/agent $(1)/usr/bin/nezha-agent
endef

$(eval $(call GoBinPackage,nezha-agent))
$(eval $(call BuildPackage,nezha-agent))
