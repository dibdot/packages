include $(TOPDIR)/rules.mk

PKG_NAME:=ninja
PKG_VERSION:=1.10.2
PKG_RELEASE:=3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/ninja-build/ninja/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=ce35865411f0490368a8fc383f29071de6690cbadc27704734978221f25e2bed

PKG_MAINTAINER:=Andre Heider <a.heider@gmail.com>
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk

CONFIGURE_ARGS:=
ifneq ($(findstring c,$(OPENWRT_VERBOSE)),)
  CONFIGURE_ARGS+=--verbose
endif

define Package/ninja
  SECTION:=devel
  CATEGORY:=Development
  TITLE:=ninja
  URL:=https://ninja-build.org/
  DEPENDS:=+libstdcpp
endef

define Package/ninja/description
  Ninja is a small build system with a focus on speed. It differs from other build systems in two major respects: it is designed to have its input files generated by a higher-level build system, and it is designed to run builds as fast as possible.
endef

define Package/ninja/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ninja $(1)/usr/bin/
endef

define Build/Configure
	cd $(PKG_BUILD_DIR) && \
		CXX="$(TARGET_CXX)" \
		CXXFLAGS="$(TARGET_CXXFLAGS) $(EXTRA_CXXFLAGS) $(TARGET_CPPFLAGS) $(EXTRA_CPPFLAGS)" \
		LDFLAGS="$(TARGET_LDFLAGS) $(EXTRA_LDFLAGS)" \
		$(STAGING_DIR_HOST)/bin/$(PYTHON) configure.py $(CONFIGURE_ARGS)
endef

define Build/Compile
	+$(NINJA) -C $(PKG_BUILD_DIR) $(1)
endef

$(eval $(call BuildPackage,ninja))
