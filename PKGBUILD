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
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>

_py="python"
_py2="python2"
_offline="false"
_git="false"
_pkg="crash-bash"
pkgname="lib${_pkg}"
pkgver="0.0.0.0.0.0.1.1.1.1.1.1"
_commit="56fde992c1c65b57c22eb8e3a9e9a851d28518df"
pkgrel=1
_pkgdesc=(
  "A collection of bash utility functions."
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  any
)
_http="https://github.com"
_ns="themartiancompany"
url="${_http}/${_ns}/${_pkg}"
license=(
  AGPL3
)
depends=(
  "bash"
)
_os="$( \
  uname \
    -o)"
optdepends=(
  "${_py}-pygments: colorized output and syntax highlighting"
  "${_py2}-pygments: colorized output and syntax highlighting (Python 2)"
)
[[ "${_os}" != "GNU/Linux" ]] && \
[[ "${_os}" == "Android" ]] && \
  optdepends+=(
  )
makedepends=()
checkdepends=(
  "shellcheck"
)
source=()
sha256sums=()
_url="${url}"
[[ "${_offline}" == "true" ]] && \
  url="file://${HOME}/${_pkg}"
if [[ "${_git}" == true ]]; then
  makedepends+=(
    "git"
  )
  _src="${pkgname}-${pkgver}::git+${_url}#tag=${pkgver}"
  _sum='SKIP'
elif [[ "${_git}" == false ]]; then
  _src="${pkgname}-${pkgver}.tar.gz::${_url}/archive/refs/tags/${pkgver}.tar.gz"
  _sum='889803bd83774efe2bbd576855c61b45a38656a63e1d066ac4b62ac6985b7236'
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)

check() {
  cd \
    "${_pkg}-${pkgver}"
  make \
    -k \
    check
}

package() {
  cd \
    "${_pkg}-${pkgver}"
  make \
    PREFIX="/usr" \
    DESTDIR="${pkgdir}" \
    install
}

# vim: ft=sh syn=sh et
