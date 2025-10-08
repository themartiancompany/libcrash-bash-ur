# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>

_evmfs_available="$( \
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
_os="$( \
  uname \
    -o)"
if [[ ! -v "_git" ]]; then
  _git="false"
fi
if [[ ! -v "_offline" ]]; then
  _offline="false"
fi
if [[ ! -v "_git_http" ]]; then
  _git_http="gitlab"
fi
_archive_format="tar.gz"
if [[ "${_git_http}" == "github" ]]; then
  _archive_format="zip"
fi
_docs="true"
_py="python"
_py2="python2"
_pkg=crash-bash
pkgbase="lib${_pkg}"
pkgname=(
  "${pkgbase}"
)
if [[ "${_docs}" == "true" ]]; then
  pkgname+=(
    "${pkgbase}-docs"
  )
fi
pkgver="0.0.0.0.0.1.1.1"
_commit="7d862167df665447ce7ffb0aab881b1515ae1f9c"
pkgrel=1
_pkgdesc=(
  "A collection of bash utility functions."
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'any'
)
_http="https://${_git_http}.com"
_ns="themartiancompany"
url="${_http}/${_ns}/${_pkg}"
license=(
  'AGPL3'
)
depends=(
  "bash"
)
optdepends=(
  "${_py}-pygments: colorized output and syntax highlighting"
  "${_py2}-pygments: colorized output and syntax highlighting (Python 2)"
)
if [[ "${_os}" != "GNU/Linux" ]] && \
   [[ "${_os}" == "Android" ]]; then
  optdepends+=(
  )
fi
makedepends=(
  'make'
)
if [[ "${_docs}" == "true" ]]; then
  makedepends+=(
    "${_py}-docutils"
  )
fi
checkdepends=(
  "shellcheck"
)
source=()
sha256sums=()
_url="${url}"
if [[ "${_offline}" == "true" ]]; then
  _url="file://${HOME}/${_pkg}"
fi
_tag_name="commit"
_tag="${_commit}"
_tarname="${_pkg}-${_tag}"
_archive_sum="740c0c9ac18b06ebaed1beade7e5f0057e3b0be271ea612c6f6d7b952f86cedd"
_archive_sig_sum="5575df65232f6caeefc1670227289712257e39228787bd69e18b96b8db53492e"
_evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
# Dvorak
_evmfs_archive_uri="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}/${_archive_sum}"
_evmfs_archive_src="${_tarname}.${_archive_format}::${_evmfs_archive_uri}"
_archive_sig_uri="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}/${_archive_sig_sum}"
_archive_sig_src="${_tarname}.${_archive_format}.sig::${_archive_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs"
  )
  _src="${_evmfs_archive_src}"
  _sum="${_archive_sum}"
  source+=(
    "${_archive_sig_src}"
  )
  sha256sums+=(
    "${_archive_sig_sum}"
  )
elif [[ "${_git}" == true ]]; then
  makedepends+=(
    "git"
  )
  _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
  _sum="SKIP"
elif [[ "${_git}" == false ]]; then
  if [[ "${_tag_name}" == 'pkgver' ]]; then
    _uri="${_url}/archive/refs/tags/${_tag}.${_archive_format}"
  elif [[ "${_tag_name}" == "commit" ]]; then
    _uri="${_url}/archive/${_commit}.${_archive_format}"
  fi
  _src="${_tarname}.${_archive_format}::${_uri}"
  _sum="${_archive_sum}"
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)
validpgpkeys=(
  # Truocolo <truocolo@aol.com>
  '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
  'DD6732B02E6C88E9E27E2E0D5FC6652B9D9A6C01'
  # Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
  '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
)

check() {
  cd \
    "${_tarname}"
  make \
    -k \
    check
}

prepare() {
  local \
    _cmd=()
  if [[ ! -d "${srcdir}/${_tarname}" ]]; then
    cd \
      "${srcdir}"
    if [[ "${_archive_format}" == "tar.gz" ]]; then
      _cmd+=(
        tar
          xf
      )
    elif [[ "${_archive_format}" == "zip" ]]; then
      _cmd+=(
        unzip
      )
    fi
    "${_cmd[@]}" \
      "${_tarname}.${_archive_format}"
  fi
}

package_libcrash-bash() {
  msg \
    "${srcdir}"
  ls \
    "${srcdir}"
  cd \
    "${srcdir}/${_tarname}"
  make \
    PREFIX="/usr" \
    DESTDIR="${pkgdir}" \
    "install-${_pkg}"
  install \
    -vDm755 \
    "COPYING" \
    "${pkgdir}/usr/share/licenses/${pkgbase}/COPYING"
}

package_libcrash-bash-docs() {
  cd \
    "${_tarname}"
  make \
    PREFIX="/usr" \
    DESTDIR="${pkgdir}" \
    install-doc
  make \
    PREFIX="/usr" \
    DESTDIR="${pkgdir}" \
    install-examples
  make \
    PREFIX="/usr" \
    DESTDIR="${pkgdir}" \
    install-man
  install \
    -vDm755 \
    "COPYING" \
    "${pkgdir}/usr/share/licenses/${pkgbase}-docs/COPYING"
}

# vim: ft=sh syn=sh et
