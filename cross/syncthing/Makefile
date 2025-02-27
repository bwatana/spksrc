PKG_NAME = syncthing
PKG_VERS = 1.19.1
PKG_EXT = tar.gz
PKG_DIST_NAME = $(PKG_NAME)-source-v$(PKG_VERS).$(PKG_EXT)
PKG_DIST_SITE = https://github.com/syncthing/syncthing/releases/download/v$(PKG_VERS)
PKG_DIST_FILE = $(PKG_NAME)-$(PKG_VERS).$(PKG_EXT)
EXTRACT_PATH = $(WORK_DIR)/src/github.com/$(PKG_NAME)
PKG_DIR = $(PKG_NAME)

# use go 1.17
# as soon as syncthing builds with go 1.18:
# - use native/go
# - remove path overwrite below
# - remove native/go_1.17
BUILD_DEPENDS = native/go_1.17

HOMEPAGE = https://www.syncthing.net/
COMMENT  = Syncthing replaces Dropbox and BitTorrent Sync with something open, trustworthy and decentralized. Your data is your data alone and you deserve to choose where it is stored, if it is shared with some third party and how ...
LICENSE  = MPL-2.0

COMPILE_TARGET = syncthing_compile

GO_SRC_DIR = $(EXTRACT_PATH)/$(PKG_NAME)
GO_BIN_DIR = $(GO_SRC_DIR)/$(PKG_NAME)

include ../../mk/spksrc.cross-go.mk

# use go 1.17
ENV += PATH=$(WORK_DIR)/../../../native/go_1.17/work-native/go/bin/:$$PATH

BUILD_ARGS = -goos=$(GOOS) -goarch=$(GO_ARCH) -version=v$(PKG_VERS)

# use custom build to remove GOARCH from ENV and for custom BUILD_ARGS
syncthing_compile:
	cd $(GO_SRC_DIR) && env $(filter-out GOARCH=%, $(ENV)) go run build.go $(BUILD_ARGS) build
