#
# Copyright (C) 2018 Onion Corporation
#
# Author: Micky Socaci <micky@nowlive.ro>, Lazar Demin  <lazar@onion.io>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
PKG_NAME:=oos-app-env-reporter
PKG_VERSION:=1.0.0
PKG_RELEASE:=1


PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=HEAD # dev for dev branch, HEAD for master
#PKG_SOURCE_URL:=https://github.com/OnionIoT/oos-app-qwiic.git
PKG_SOURCE_URL:=https://github.com/mickys/OOS-App-Sparkfun-Qwiic
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_RELEASE).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/oos-app-env-reporter
	SECTION:=nowlive
	CATEGORY:=Nowlive
	SUBMENU:=Applications
	TITLE:=Environment MQTT Reporter : based on Sparkfun Qwiic
	DEPENDS:=+libonioni2c +libmosquitto +libconfig
	#+libssl +libcrypto 
endef

define Package/oos-app-env-reporter/description
Environment MQTT Reporter : based on Sparkfun Qwiic
endef

define Package/oos-app-env-reporter/install
	$(INSTALL_DIR) $(1)/www/apps/oos-app-env-reporter $(1)/usr/bin $(1)/etc/init.d $(1)/etc/env-reporter
	# copy the web site files
	$(CP) -r $(PKG_BUILD_DIR)/omega/www/* $(1)/www/apps/oos-app-env-reporter/
	# install configuration files
	$(CP) -r $(PKG_BUILD_DIR)/omega/etc/env-reporter/* $(1)/etc/env-reporter/
	# install the program
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/omega/src/env-reporter $(1)/usr/bin/
	# install the init.d scripts
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/omega/init.d/oos-qwiic-amg8833 $(1)/etc/init.d/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/omega/init.d/oos-qwiic-env $(1)/etc/init.d/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/omega/init.d/oos-qwiic-vl53l1x $(1)/etc/init.d/
endef


# calls to build each package
$(eval $(call BuildPackage,oos-app-env-reporter))