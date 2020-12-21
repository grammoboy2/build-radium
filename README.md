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


Dependencies on Debian:

`
sudo apt install python2-dev libasound2-dev libjack-jackd2-dev libresample1-dev liblrdf0-dev libsndfile1-dev ladspa-sdk libglib2.0-dev calf-plugins binutils-dev libc6-dev tk8.6-dev libogg-dev libvorbis-dev libspeex-dev fftw-dev fftw3-dev guile-2.2-dev libxkbfile-dev x11-utils cmake libfreetype6-dev libxinerama-dev libxcursor-dev libxrandr-dev llvm-dev libboost-all-dev libssl-dev libncurses-dev libxcb-keysyms1-dev libqwt-qt5-dev libqt5webkit5-dev libqt5x11extras5-dev qttools5-dev-tools qtbase5-private-dev libgmp-dev libgmp3-dev libmpfr-dev libmpc-dev`



See also:

https://github.com/kmatheussen/radium/issues/1249#issuecomment-621738146

https://devconnected.com/how-to-checkout-git-tags/
