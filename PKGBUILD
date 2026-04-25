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
  elif [[ "${_os}" == "GNU/Linux" ]]; then
    _systemd="true"
  fi
fi
if [[ ! -v "_distro" ]]; then
  _distro="archlinux"
  _distro="dogeos"
fi
if [[ ! -v "_shell" ]]; then
  _shell="bash"
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
if [[ ! -v "_git_service" ]]; then
  if [[ "${_distro}" == "dogeos" ]]; then
    _git_service="github"
  else 
    _git_service="gitlab"
  fi
fi
if [[ ! -v "_ns" ]]; then
  if [[ "${_git_service}" == "github" ]]; then
    _ns="themartiancompany"
  elif [[ "${_git_service}" == "gitlab" ]]; then
    _ns="GNOME"
  fi
fi
if [[ ! -v "_git" ]]; then
  _git="true"
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
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      _archive_format="zip"
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _archive_format="tar.gz"
    fi
  fi
fi
if [[ ! -v "_docs" ]]; then
  _docs="true"
fi
if [[ ! -v "_tag_name" ]]; then
  _tag_name="commit"
fi
_pkg=gdm
pkgbase="${_pkg}"
pkgname=(
  "${_pkg}"
  "lib${_pkg}"
)
pkgver=50.0
_commit="7aa5c1a3d73b51b9ccf89c51d33bfa53cc57d52e"
_bundle_commit="8e557895f05313665fa27c31e121be7693728c9e"
pkgrel=6
pkgdesc="Display manager and login screen"
if [[ ! -v "_http" ]]; then
  if [[ "${_ns}" == "GNOME" ]]; then
    _http="https://gitlab.${_proj}.org"
  elif [[ "${_ns}" == "themartiancompany" ]]; then
    if [[ "${_git_service}" == "github" || \
          "${_git_service}" == "gitlab" ]]; then
      _http="https://${_git_service}.com"
    fi
  fi
fi
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
  "${_shell}"
  "gdk-pixbuf2"
  "glib2"
  "${_libc}"
  "${_proj}-session"
  "${_proj}-shell"
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
  "${_libc}"
  "${_compiler}"
  "${_libcompiler}"
  # "cmake"
  "dconf"
  "glib2-devel"
  "gobject-introspection"
  "json-glib"
  "libgudev"
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
if [[ "${_tag_name}" == "commit" ]]; then
  _tag="${_commit}"
elif [[ "${_tag_name}" == "tag" ]]; then
  _tag="${pkgver/[a-z]/.&}"
fi
_tarname="${_pkg}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
if [[ "${_git}" == "true" ]]; then
  _src="${_tarname}::git+${_url}.git#${_tag_name}=${_tag}"
  _sum="SKIP"
fi
_ssh_agent_patch="0001-Xsession-Don-t-start-ssh-agent-by-default.patch"
_ssh_agent_patch_sum="39a7e1189d423dd428ace9baac77ba0442c6706a861d3c3db9eb3a6643e223f8"
source=(
  "${_ssh_agent_patch}"
)
sha256sums=(
  "${_ssh_agent_patch_sum}"
)
_gitlab_sum="55558c197571937f8ee88b2e962e2d62c34f046a2a4480d284bdb70bb8fde1d1"
_gitlab_sig_sum="30270a48e0b3e9c0292e325b3f87c028daf7f177a779237e02521280624488b2"
_github_sum="3cfb5ecb6370b31bb763441f20760c913f8bea4897bb923d9f4a9ebf1bac23f0"
_github_sig_sum="eb2a47031dfafd2ee94984fd42317afb6ce50aa34b48a6a03ec327c010e3a802"
_bundle_sum="ec2bd72b4af9195d6e9312498328675b3f33c6c6edc1b6a5e75c05ecbc49d359"
_bundle_sig_sum="8591dac542dd56deb8fc96d8610b646d3a840b7530c2282c77977f73df8943c1"
# that crazy kid address
_kid_ns="0x926acb6aA4790ff678848A9F1C59E578B148C786"
# Dvorak
_dvorak_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
if [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _sum="${_bundle_sum}"
    _sig_sum="${_bundle_sig_sum}"
    # Tallero
    # _evmfs_ns="0x6ec7cC56dCeC0a00CB15E97C64B1a5Ec7A31403c"
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      _sum="${_github_sum}"
      _sig_sum="${_github_sig_sum}"
      # Truocolo
      # _evmfs_ns="0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b"
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _sum="${_gitlab_sum}"
      _sig_sum="${_gitlab_sig_sum}"
      # Tallero
      # _evmfs_ns="0x6ec7cC56dCeC0a00CB15E97C64B1a5Ec7A31403c"
    fi
  fi
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_tag_name}" == "commit" ]]; then
      _sum="SKIP"
      _sig_sum="SKIP"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      _sum="${_github_sum}"
      _sig_sum="${_github_sig_sum}"
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _sum="${_gitlab_sig_sum}"
      _sig_sum="${_gitlab_sig_sum}"
    fi
  fi
fi
_evmfs_ns="${_dvorak_ns}"
_evmfs_sig_ns="${_dvorak_ns}"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_evmfs_uri="${_evmfs_dir}/${_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_sig_uri="${_evmfs_dir}/${_sig_sum}"
_sig_src="${_tarfile}.sig::${_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_git}" == "false" ]]; then
    _src="${_evmfs_src}"
    source+=(
      "${_sig_src}"
    )
    sha256sums+=(
      "${_sig_sum}"
    )
  fi
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == true ]]; then
    _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
    _sum="SKIP"
  elif [[ "${_git}" == false ]]; then
    _uri=""
    if [[ "${_git_service}" == "github" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/archive/${_commit}.${_archive_format}"
        _sum="${_github_sum}"
      fi
    elif [[ "${_git_service}" == "gitlab" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/-/archive/${_tag}/${_tag}.${_archive_format}"
      fi
    fi
    _src="${_tarfile}::${_uri}"
  fi
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)

prepare() {
  cd \
    "${_tarname}"
  # Don't start ssh-agent by default
  if [[ "${_git}" == "true" ]]; then
    git \
      apply \
      -3 \
      "../0001-Xsession-Don-t-start-ssh-agent-by-default.patch"
  else
    _msg=(
      "Missing patch."
    )
    echo \
      "${_msg[*]}" \
      1>&2
    exit \
      1
  fi
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
    "${_tarname}" \
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
  local \
    p="$1" \
    f \
    d; \
  shift
  for f; do
    d="${srcdir}/${p}/${f#${pkgdir}/}"
    mkdir \
      -p \
      "$(dirname "${d}")"
    mv \
      "$f" \
      "$d"
    rmdir \
      -p \
      --ignore-fail-on-non-empty \
      "$(dirname \
           "${f}")"
  done
}

_etc_get() {
  local \
    _etc \
    _os
  _os="$(
    uname \
      -o)"
  if [[ "${_os}" == "Android" ]]; then
    _etc="usr/etc"
  else
    _etc="etc"
  fi
  echo \
    "${_etc}"
}

_usr_get() {
  local \
    _env \
    _msg=()
  _env="$(
    command \
      -v \
      "env" || \
      true)"
  if [[ "${_env}" == "" ]]; then
    _msg=(
      "Big trouble."
    )
    echo \
      "${_msg[*]}" \
      1>&2
    exit \
      1
  fi
  dirname \
    "$(dirname \
         "${_env}")"
}

_etc="$(
  _etc_get)"

package_gdm() {
  local \
    _logo_dir \
    _logo_name
    _usr
  _usr="$(
    _usr_get)"
  depends+=(
    "lib${_pkg}"
  )
  optdepends=(
    "${_fprintd_optdepends[*]}"
  )
  backup=(
    "${_etc}/${_pkg}/PostSession/Default"
    "${_etc}/${_pkg}/PreSession/Default"
    "${_etc}/${_pkg}/Xsession"
    "${_etc}/${_pkg}/custom.conf"
    "${_etc}/pam.d/${_pkg}-autologin"
    "${_etc}/pam.d/${_pkg}-fingerprint"
    "${_etc}/pam.d/${_pkg}-launch-environment"
    "${_etc}/pam.d/${_pkg}-password"
    "${_etc}/pam.d/${_pkg}-smartcard"
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
    "${_usr}/lib/sysusers.d/${_pkg}.conf" <<END
g ${_pkg} 120 -
END
  mkdir \
    -p \
    "var/lib/${_pkg}"
  if [[ "${_distro}" == "archlinux" ]]; then
    _logo_dir="${_usr}/share/pixmaps"
    _logo_name="${_distro}-logo-text-dark.svg"
    _logo="${_logo_dir}/${_logo_name}"
  elif [[ "${_distro}" == "dogeos" ]]; then
    _logo_dir="${_usr}/share/icons"
    # I have produced a dark logo for
    # dogeos
    _logo_name="dogeos-transparent-dark.png"
    # but Ur logo seems more appropriate for an OS
    _logo_name="ur-logo.png"
    _logo="${_logo_dir}/${_logo_name}"
  fi
  install \
    -vDm644 \
    "/dev/stdin" \
    "usr/share/glib-2.0/schemas/30_${_domain}.${_pkg}.gschema.override" <<END
[org.${_proj}.login-screen]
enable-smartcard-authentication=false
logo='${_logo}'
END
  _pick \
    "lib${_pkg}" \
    "usr/include"
  _pick \
    "lib${_pkg}" \
    "usr/lib/"{"girepository-1.0","lib${_pkg}"*,"pkgconfig"}
  _pick \
    "lib${_pkg}" \
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
    "lib${_pkg}.so"
  )
  mv \
    "lib${_pkg}/"* \
    "${pkgdir}"
}

# vim:set sw=2 sts=-1 et:
