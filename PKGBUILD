# SPDX-License-Identifier: AGPL-3.0

#    -----------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    -----------------------------------------------------
#
#    This program is free software: you can redistribute
#    it and/or modify it under the terms of the
#    GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of
#    the License, or (at your option) any later version.
#
#    This program is distributed in the hope that it
#    will be useful, but WITHOUT ANY WARRANTY;
#    without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#    See the GNU Affero General Public License for
#    more details.
#
#    You should have received a copy of the
#    GNU Affero General Public License
#    along with this program.
#    If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Contributors:
#   Fabian Bornschein
#     <fabiscafe@archlinux.org>
#   Jan Alexander Steffens (heftig)
#     <heftig@archlinux.org>
#   Jan de Groot
#     <jgc@archlinux.org>

_os="$(
  uname \
    -o)"
if [[ "${_os}" == "Android" ]]; then
  _libc="ndk-sysroot"
  _compiler="clang"
  _libcompiler="llvm-libs"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _libc="glibc"
  _compiler="gcc"
  _libcompiler="libgcc"
elif [[ "${_os}" == "Msys" ]]; then
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
  _sh="sh"
else
  _msg=(
    "Unknown os '${_os}'."
  )
  msg \
    "${_msg[*]}"
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
  _npth="npth"
  _pcsclite="pcsclite"
  _pcsclite="pcsclite"
  _sh="sh"
fi
_evmfs_available="$(
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi

if [[ ! -v "_systemd" ]]; then
  _systemd="true"
  if [[ "${_os}" == "Android" || \
        "${_os}" == "Msys" ]]; then
    _systemd="false"
  fi
fi
if [[ ! -v "_distro" ]]; then
  _distro="dogeos"
fi
if [[ ! -v "_domain" ]]; then
  if [[ "${_distro}" == "dogeos" ]]; then
    _domain="humaninstrumentalityproject.org"
  elif [[ "${_distro}" == "archlinux" ]]; then
    _domain="${_distro}.org"
  fi
fi
if [[ ! -v "_proj" ]]; then
  _proj="gnome"
fi
if [[ ! -v "_ns" ]]; then
  _ns="themartiancompany"
  _ns="GNOME"
fi
if [[ ! -v "_git" ]]; then
  _git="true"
fi
if [[ ! -v "_git_service" ]]; then
  _git_service="github"
fi
if [[ ! -v "_http" ]]; then
  if [[ "${_proj}" == "gnome" ]]; then
    _http="https://gitlab.${_proj}.org"
  fi
  if [[ "${_ns}" == "themartiancompany" ]]; then
    if [[ "${_git_service}" == "gitlab" ]]; then
      _http="https://gitlab.com"
    elif [[ "${_git_service}" == "github" ]]; then
      _http="https://github.com"
    fi
  fi
fi
if [[ ! -v "_docs" ]]; then
  _docs="true"
fi
_pkg=gdm
pkgbase="${_pkg}"
pkgname=(
  "${_pkg}"
  "lib${_pkg}"
)
pkgver=50.0
pkgrel=2
pkgdesc="Display manager and login screen"
_http="https://gitlab.${_proj}.org"
_ns="GNOME"
url="${_http}/${_ns}/${_pkg}"
arch=(
  "aarch64"
  "arm"
  "armv7l"
  "armv8l"
  "i686"
  "mips"
  "pentium4"
  "powerpc"
  "x86_64"
)
license=(
  "GPL-2.0-or-later"
)
depends=(
  "accountsservice"
  "audit"
  "bash"
  "gdk-pixbuf2"
  "glib2"
  "${_libc}"
  "gnome-session"
  "gnome-shell"
  "json-glib"
  "keyutils"
  "libcanberra"
  "${_libcompiler}"
  "libgudev"
  "libxau"
  "libxcb"
  "pam"
  "polkit"
  "upower"
)
if [[ "${_systemd}" == "true" ]]; then
  depends+=(
    "systemd"
    "systemd-libs"
  )
fi
makedepends=(
  "dconf"
  "glib2-devel"
  "gobject-introspection"
  "meson"
  "plymouth"
)
if [[ "${_docs}" == "true" ]]; then
  makedepends+=(
    "docbook-xsl"
    "yelp-tools"
  )
fi
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
if [[ "${_os}" == "Msys" ]]; then
  makedepends+=(
    "${_libc_headers}"
    "windows-default-manifest"
  )
fi
checkdepends=(
  "check"
)
_fprintd_optdepends=(
  'fprintd:'
    'fingerprint authentication'
)
_url="${url}"

source=(
  "git+${_url}.git#tag=${pkgver/[a-z]/.&}"
  "0001-Xsession-Don-t-start-ssh-agent-by-default.patch"
)
b2sums=(
  '5c3784315c8718aabe6c4abacfca3bc00ac8d028f2a0442d397496633f1e0af44ac4dd156d8b2025212b68a43b3d837d32423aa82cc2be7d565f2445c8144839'
  'f7e868fdd7cc121433de1572583eb728f4d186cd4f52c6d6c8f2ccf4a3cf781144ff71f704f13571ddb97a1ff4ec55cfa3df25d38737ad19da21e84ddc2d3ee4'
)

prepare() {
  cd \
    "${_pkg}"
  # Don't start ssh-agent by default
  git \
    apply \
    -3 \
    "../0001-Xsession-Don-t-start-ssh-agent-by-default.patch"
}

build() {
  local \
    _meson_opts=()
  _meson_opts+=(
    -D
      dbus-sys="/usr/share/dbus-1/system.d"
    -D
      default-pam-config="arch"
    -D
      default-path="/usr/local/bin:/usr/local/sbin:/usr/bin"
    -D
      gdm-xsession="true"
    -D
      run-dir="/run/${_pkg}"
    -D
      selinux="disabled"
  )

  arch-meson \
    "${_pkg}" \
    "build" \
    "${_meson_opts[@]}"
  meson \
    compile \
    -C \
      "build"
}

check() {
  meson \
    test \
    -C \
      "build" \
    --print-errorlogs
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
  local \
    _logo_dir \
    _logo_name
  depends+=(
    "lib${_pkg}"
  )
  optdepends=(
    "${_fprintd_optdepends[*]}"
  )
  backup=(
    "etc/${_pkg}/PostSession/Default"
    "etc/${_pkg}/PreSession/Default"
    "etc/${_pkg}/Xsession"
    "etc/${_pkg}/custom.conf"
    "etc/pam.d/${_pkg}-autologin"
    "etc/pam.d/${_pkg}-fingerprint"
    "etc/pam.d/${_pkg}-launch-environment"
    "etc/pam.d/${_pkg}-password"
    "etc/pam.d/${_pkg}-smartcard"
  )
  groups=(
    "${_proj}"
  )
  meson \
    install \
    -C \
      "build" \
    --destdir \
      "${pkgdir}"

  cd \
    "${pkgdir}"
  install \
    -vDm644 \
    "/dev/stdin" \
    "usr/lib/sysusers.d/${_pkg}.conf" <<END
g ${_pkg} 120 -
END
  mkdir \
    -p \
    "var/lib/${_pkg}"
  if [[ "${_distro}" == "archlinux" ]]; then
    _logo_dir="/usr/share/pixmaps"
    _logo_name="${_distro}-logo-text-dark.svg"
    _logo="${_logo_dir}/${_logo_name}"
  elif [[ "${_distro}" == "dogeos" ]]; then
    logo=""
  fi
  install \
    -vDm644 \
    "/dev/stdin" \
    "usr/share/glib-2.0/schemas/30_${_domain}.${_pkg}.gschema.override" <<END
[org.gnome.login-screen]
enable-smartcard-authentication=false
logo='${_logo}'
END
  _pick \
    "lib${_pkg}" \
    "usr/include"
  _pick \
    "libgdm" \
    "usr/lib/"{"girepository-1.0","libgdm"*,"pkgconfig"}
  _pick \
    "libgdm" \
    "usr/share/"{"gir-1.0","glib-2.0"}
}

package_libgdm() {
  pkgdesc+=" - support library"
  depends=(
    "dconf"
    "glib2"
    "${_libc}"
    "${_libcompiler}"
    "libg"{"lib","object","io"}"-2.0.so"
  )
  if [[ "${_systemd}" == "true" ]]; then
    depends+=(
      "libsystemd.so"
      "systemd-libs"
    )
  fi
  provides=(
    "libgdm.so"
  )

  mv libgdm/* "$pkgdir"
}

# vim:set sw=2 sts=-1 et:
