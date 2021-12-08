# Maintainer: Evangelos Foutras <evangelos@foutrelis.com>
# Contributor: tobias <tobias funnychar archlinux.org>

pkgname=xfce4-session-lxpolkit
pkgver=4.16.0
pkgrel=2
pkgdesc="Session manager for Xfce"
arch=('x86_64')
url="https://docs.xfce.org/xfce/xfce4-session/start"
license=('GPL2')
groups=('xfce4')
conflicts=('xfce4-session')
depends=('libxfce4ui' 'libwnck3' 'xfconf' 'libsm' 'polkit' 'xorg-iceauth'
         'xorg-xinit' 'xorg-xrdb' 'hicolor-icon-theme' 'libxfce4util')
makedepends=('intltool')
optdepends=('gnome-keyring: for keyring support when GNOME compatibility is enabled'
            'xfce4-screensaver: for locking screen with xflock4'
            'xscreensaver: for locking screen with xflock4'
            'gnome-screensaver: for locking screen with xflock4'
            'xlockmore: for locking screen with xflock4'
            'slock: for locking screen with xflock4')
source=(https://archive.xfce.org/src/xfce/xfce4-session/${pkgver%.*}/xfce4-session-$pkgver.tar.bz2
        source-system-xinitrc-scripts.patch)
sha256sums=('22f273f212481d71e0b5618c62710cd85f69aea74f5ea5c0093f7918b07d17b7'
            '6f14d529e4c4f30cd547110bd444cee8dc70c90511a397de18acb6c1fd63ea3e')

prepare() {
  cd "$srcdir/xfce4-session-$pkgver"

  # https://bugzilla.xfce.org/show_bug.cgi?id=15440
  patch -Np1 -i ../source-system-xinitrc-scripts.patch
}

build() {
  cd "$srcdir/xfce4-session-$pkgver"

  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --libexecdir=/usr/lib/xfce4 \
    --localstatedir=/var \
    --disable-static \
    --disable-debug
  make
}

package() {
  cd "$srcdir/xfce4-session-$pkgver"
  make DESTDIR="$pkgdir" install

  # Provide a default PolicyKit Authentication Agent (FS#42569)
  install -d "$pkgdir/etc/xdg/autostart"
}

# vim:set ts=2 sw=2 et:
