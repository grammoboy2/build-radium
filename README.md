# build-radium

export RADIUM_QT_VERSION=5 

export INCLUDE_FAUSTDEV_BUT_NOT_LLVM="jadda"

make packages

RADIUM_QT_VERSION=5 BUILDTYPE=RELEASE ./build_linux.sh -j $(nproc)


Install system wide:

sudo -E ./install.sh /opt

sudo su

echo QT_QPA_PLATFORM_PLUGIN_PATH="$($(RADIUM_QT_VERSION=5 ./find_moc_and_uic_paths.sh qmake) -query QT_INSTALL_PLUGINS)" /opt/radium/radium >> /usr/local/bin/radium

chmod +x /usr/local/bin/radium

New version rebuild:

git fetch --tags

git checkout tags/tag

export INCLUDE_FAUSTDEV_BUT_NOT_LLVM="jadda"

make clean

RADIUM_QT_VERSION=5 BUILDTYPE=RELEASE ./build_linux.sh -j $(nproc)


Remove older version:

sudo rm -r /opt/radium

sudo rm /usr/local/bin/radium



See also:

https://github.com/kmatheussen/radium/issues/1249#issuecomment-621738146

https://devconnected.com/how-to-checkout-git-tags/
