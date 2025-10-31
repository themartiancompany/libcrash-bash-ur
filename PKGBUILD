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

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>

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
if [[ ! -v "_docs" ]]; then
  _docs="true"
fi
_archive_format="tar.gz"
if [[ "${_git_http}" == "github" ]]; then
  _archive_format="zip"
fi
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
pkgver="0.0.0.0.0.0.0.0.0.0.0.1.1.1.1"
_commit="8b1ce8109c57769acc0f1131e5aba53699cbec4b"
pkgrel=1
_pkgdesc=(
  "A Bash library of GNU"
  "Privacy Guard related"
  "functions."
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
  "coreutils"
  "gawk"
  "gnupg"
  "grep"
  "util-linux"
)
_libcrash_bash_docs_optdepends=(
  "${_pkg}-docs:"
    "Crash Bash"
    "library documentation"
    "and manuals."
)
_libcrash_bash_docs_ref_optdepends+=(
 "${_pkg}:"
   "the package this documentation"
   "package pertains to."
)
optdepends=(
  "${_libcrash_bash_docs_optdepends[*]}"
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
_tarfile="${_tarname}.${_archive_format}"
_sum="1d3cd2121f1a5087e043ee50a420f715389bcbe072fca5dbdaa5fa62c77d84e5"
_sig_sum="550a9a30d6688ac8c7831cad90f0a19972862d9a7d04477dfe46191c93e40c01"
# Dvorak
_evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_evmfs_uri="${_evmfs_dir}/${_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_sig_uri="${_evmfs_dir}/${_sig_sum}"
_sig_src="${_tarfile}.sig::${_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs"
  )
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
  if [[ "${_git}" == "true" ]]; then
    makedepends+=(
      "git"
    )
    _uri="git+${_url}#${_tag_name}=${_tag}?signed"
    _src="${_tarname}::${_uri}"
    _sum="SKIP"
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_tag_name}" == 'pkgver' ]]; then
      _uri="${_url}/archive/refs/tags/${_tag}.${_archive_format}"
    elif [[ "${_tag_name}" == "commit" ]]; then
      _uri="${_url}/archive/${_commit}.${_archive_format}"
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
  local \
    _make_opts=()
  _make_opts+=(
    PREFIX="/usr"
    DESTDIR="${pkgdir}"
  )
  cd \
    "${_tarname}"
  make \
    "${_make_opts[@]}" \
    "install-${_pkg}"
  install \
    -vDm755 \
    "COPYING" \
    "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
}

package_libcrash-bash-docs() {
  local \
    _make_opts=()
  optdepends=(
    "${_libcrash_bash_docs_ref_optdepends[*]}"
  )
  _make_opts+=(
    PREFIX="/usr"
    DESTDIR="${pkgdir}"
  )
  cd \
    "${_tarname}"
  depends=()
  make \
    "${_make_opts[@]}" \
    install-doc \
    install-man
  install \
    -vDm755 \
    "COPYING" \
    "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
}

# vim: ft=sh syn=sh et
