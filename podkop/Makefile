include $(TOPDIR)/rules.mk

PKG_NAME:=podkop
PKG_VERSION:=0.4.7
PKG_RELEASE:=1

PKG_MAINTAINER:=ITDog <podkop@itdog.info>
PKG_LICENSE:=GPL-2.0-or-later

include $(INCLUDE_DIR)/package.mk

define Package/podkop
	SECTION:=net
	CATEGORY:=Network
	DEPENDS:=+sing-box +curl +jq +kmod-nft-tproxy +coreutils-base64
	CONFLICTS:=https-dns-proxy
	TITLE:=Domain routing app
	URL:=https://podkop.net
	PKGARCH:=all
endef

define Package/podkop/description
	Domain routing. Use of VLESS, Shadowsocks technologies
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/podkop/prerm
#!/bin/sh

grep -q "105 podkop" /etc/iproute2/rt_tables && sed -i "/105 podkop/d" /etc/iproute2/rt_tables

/etc/init.d/podkop stop

exit 0
endef

define Package/podkop/conffiles
/etc/config/podkop
endef

define Package/podkop/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/etc/init.d/podkop $(1)/etc/init.d/podkop
	sed -i "s/VERSION_FROM_MAKEFILE/$(PKG_VERSION)/g" $(1)/etc/init.d/podkop

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/etc/config/podkop $(1)/etc/config/podkop

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) ./files/usr/bin/podkop $(1)/usr/bin/podkop
endef

$(eval $(call BuildPackage,podkop))
