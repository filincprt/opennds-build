#
# libmicrohttpd 1.0.2, deliberately built as the no-SSL variant only.
# Based on the official OpenWrt packages feed recipe for OpenWrt 25.12.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libmicrohttpd
PKG_VERSION:=1.0.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@GNU/libmicrohttpd
PKG_HASH:=df324fcd0834175dab07483133902d9774a605bfa298025f69883288fd20a8c7

PKG_MAINTAINER:=Alexander Couzens <lynxis@fe80.eu>
PKG_LICENSE:=LGPL-2.1-or-later
PKG_LICENSE_FILES:=COPYING
PKG_CPE_ID:=cpe:/a:gnu:libmicrohttpd

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libmicrohttpd-no-ssl
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=GNU libmicrohttpd embedded HTTP server library (without SSL)
  URL:=https://www.gnu.org/software/libmicrohttpd/
  VARIANT:=nossl
  DEFAULT_VARIANT:=1
  PROVIDES:=libmicrohttpd
endef

define Package/libmicrohttpd-no-ssl/description
  GNU libmicrohttpd is a small C library for running an HTTP server.
  This build intentionally disables HTTPS/TLS because openNDS only needs HTTP.
endef

CONFIGURE_ARGS += \
	--disable-curl \
	--disable-rpath \
	--disable-doc \
	--disable-examples \
	--enable-epoll \
	--with-pic \
	--disable-https \
	--without-gnutls

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/include/microhttpd.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libmicrohttpd.{so*,a,la} $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libmicrohttpd.pc $(1)/usr/lib/pkgconfig/
endef

define Package/libmicrohttpd-no-ssl/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libmicrohttpd.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libmicrohttpd-no-ssl))
