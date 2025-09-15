# Maintainer: Fabian Bornschein <fabiscafe@archlinux.org>
# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Contributor: Jan de Groot <jgc@archlinux.org>

pkgbase=gdm
pkgname=(
  gdm
  libgdm
)
pkgver=49rc
pkgrel=1
pkgdesc="Display manager and login screen"
url="https://gitlab.gnome.org/GNOME/gdm"
arch=(x86_64)
license=(GPL-2.0-or-later)
depends=(
  accountsservice
  audit
  bash
  gcc-libs
  glib2
  glibc
  gnome-session
  gnome-shell
  json-glib
  keyutils
  libcanberra
  libgudev
  pam
  systemd-libs
  upower
)
makedepends=(
  dconf
  docbook-xsl
  git
  glib2-devel
  gobject-introspection
  meson
  plymouth
  yelp-tools
)
checkdepends=(check)
source=(
  "git+https://gitlab.gnome.org/GNOME/gdm.git#tag=${pkgver/[a-z]/.&}"
)
b2sums=('92b3d2f711cff8e348cdb09c35d8ff06198ab07dfb4ef80b329286aa09adb45b0051a1d9ea6dfc6ffe84234513909e4be8928f68eb0b0359c4748019535f5924')

prepare() {
  cd gdm
}

build() {
  local meson_options=(
    -D dbus-sys="/usr/share/dbus-1/system.d"
    -D default-pam-config=arch
    -D default-path="/usr/local/bin:/usr/local/sbin:/usr/bin"
    -D ipv6=true
    -D run-dir=/run/gdm
    -D selinux=disabled
  )

  arch-meson gdm build "${meson_options[@]}"
  meson compile -C build
}

check() {
  meson test -C build --print-errorlogs
}

_pick() {
  local p="$1" f d; shift
  for f; do
    d="$srcdir/$p/${f#$pkgdir/}"
    mkdir -p "$(dirname "$d")"
    mv "$f" "$d"
    rmdir -p --ignore-fail-on-non-empty "$(dirname "$f")"
  done
}

package_gdm() {
  depends+=(libgdm)
  optdepends=('fprintd: fingerprint authentication')
  backup=(
    etc/gdm/PostSession/Default
    etc/gdm/PreSession/Default
    etc/gdm/custom.conf
    etc/pam.d/gdm-autologin
    etc/pam.d/gdm-fingerprint
    etc/pam.d/gdm-launch-environment
    etc/pam.d/gdm-password
    etc/pam.d/gdm-smartcard
  )
  groups=(gnome)

  meson install -C build --destdir "$pkgdir"

  cd "$pkgdir"

  install -d -o   0 -g   0 -m 0755 var
  install -d -o   0 -g   0 -m 0755 var/lib
  install -d -o 120 -g 120 -m 1770 var/lib/gdm
  install -d -o 120 -g 120 -m 0700 var/lib/gdm/.config
  install -d -o 120 -g 120 -m 0700 var/lib/gdm/.config/pulse

  # https://src.fedoraproject.org/rpms/gdm/blob/master/f/default.pa-for-gdm
  install -o120 -g120 -m644 /dev/stdin var/lib/gdm/.config/pulse/default.pa <<END
load-module module-device-restore
load-module module-card-restore
load-module module-udev-detect
load-module module-native-protocol-unix
load-module module-default-device-restore
load-module module-always-sink
load-module module-intended-roles
load-module module-suspend-on-idle
load-module module-systemd-login
load-module module-position-event-sounds
END

  install -Dm644 /dev/stdin usr/lib/sysusers.d/gdm.conf <<END
g gdm 120 -
u gdm 120 "Gnome Display Manager" /var/lib/gdm
END

  install -Dm644 /dev/stdin usr/share/glib-2.0/schemas/org.gnome.login-screen.gschema.override <<END
[org.gnome.login-screen]
enable-smartcard-authentication=false
logo='/usr/share/pixmaps/archlinux-logo-text-dark.svg'
END

  _pick libgdm usr/include
  _pick libgdm usr/lib/{girepository-1.0,libgdm*,pkgconfig}
  _pick libgdm usr/share/{gir-1.0,glib-2.0}
}

package_libgdm() {
  pkgdesc+=" - support library"
  depends=(
    dconf
    gcc-libs
    glib2
    glibc
    libg{lib,object,io}-2.0.so
    libsystemd.so
    systemd-libs
  )
  provides=(libgdm.so)

  mv libgdm/* "$pkgdir"
}

# vim:set sw=2 sts=-1 et:
