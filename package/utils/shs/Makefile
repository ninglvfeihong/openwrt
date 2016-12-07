include $(TOPDIR)/rules.mk

PKG_NAME:=shs
PKG_VERSION:=0.0.1
PKG_RELEASE:=1

PKG_MAINTAINER:Xiao WANG <ninglvfeihong@163.com>

include $(INCLUDE_DIR)/package.mk

define Package/shs
  SECTION:=base
  CATEGORY:=Utilities
  DEPENDS:=+boost-regex +libpthread +libopenssl +libstdcpp +librt
  TITLE:=Smart Hotel System
endef

define Package/shs/description
  Smart Hotel System. Smart system for smart people.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Package/shs/preinst
#!/bin/sh
#backup some system file
if [ -f "/etc/config/system.bak" ] ; then
	[ -f "/etc/config/system" ] && rm -f /etc/config/system
else
	mv -f /etc/config/system /etc/config/system.bak
fi
if [ -f "/etc/inittab.bak" ] ; then
	[ -f "/etc/inittab" ] && rm -f /etc/config/system
else
        mv -f /etc/inittab /etc/inittab.bak
fi
#avoid intrrupt install procedure
return 0
endef

define Package/shs/postinst
#!/bin/sh
chmod 755 /etc/init.d/SHS
/etc/init.d/SHS enable
[ -f "/usr/lib/libboost_regex.so.1.58.0" ] && ln -s /usr/lib/libboost_regex.so.1.58.0 /usr/lib/libboost_regex.so.1.51.0
echo Please restart the router!!!
endef

define Package/shs/prerm
#!/bin/sh
/etc/init.d/SHS stop
endef

define Package/shs/postrm
#!/bin/sh
[ -f "/etc/config/system.bak" ] && mv -f /etc/config/system.bak /etc/config/system
[ -f "/etc/inittab.bak" ] && mv -f /etc/inittab.bak /etc/inittab
[ -f "/usr/lib/libboost_regex.so.1.58.0" ] && [ -f "/usr/lib/libboost_regex.so.1.51.0" ] && rm -f /usr/lib/libboost_regex.so.1.51.0
echo Please restart the router!!!
endef

define Package/shs/install
	$(INSTALL_DIR) $(1)/usr/SHS/bin
	$(CP) ./files/* $(1)/
	$(RM) -r $(1)/other
	$(INSTALL_BIN) ./files/usr/SHS/bin/* $(1)/usr/SHS/bin/
endef

$(eval $(call BuildPackage,shs))
