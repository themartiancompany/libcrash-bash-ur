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
_docs="true"
_py="python"
_py2="python2"
_offline="false"
_git="false"
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
pkgver="0.0.0.0.0.1.1"
_commit="4e95a96ef5d51ed42500d5ea30c36edd02dae348"
pkgrel=1
_pkgdesc=(
  "A collection of bash utility functions."
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'any'
)
_http="https://github.com"
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
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
# Dvorak
_evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
_archive_sum='5a80a815e4935cea2355c7dcca737e85ce6be245a2283bd3aa9186296e1d4024'
_evmfs_archive_uri="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}/${_archive_sum}"
_evmfs_archive_src="${_tarname}.zip::${_evmfs_archive_uri}"
_archive_sig_sum="1a9dbc07933d8f745b95dd18ac63e5c795f07375b1737a46b1dcf8d81d2427fd"
_archive_sig_uri="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}/${_archive_sig_sum}"
_archive_sig_src="${_tarname}.zip.sig::${_archive_sig_uri}"
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
    _src="${_tarname}.tar.gz::${_url}/archive/refs/tags/${_tag}.tar.gz"
    _sum="d4f4179c6e4ce1702c5fe6af132669e8ec4d0378428f69518f2926b969663a91"
  elif [[ "${_tag_name}" == "commit" ]]; then
    _src="${_tarname}.zip::${_url}/archive/${_commit}.zip"
    _sum="${_archive_sum}"
  fi
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
  if [[ ! -d "${srcdir}/${_tarname}" ]]; then
    cd \
      "${srcdir}"
    unzip \
      "${srcdir}/${_tarname}.zip"
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
