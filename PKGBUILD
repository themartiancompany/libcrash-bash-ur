# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>

_py="python"
_py2="python2"
_offline="false"
_git="false"
_pkg="crash-bash"
pkgname="lib${_pkg}"
pkgver="0.0.0.0.0.0.1.1.1.1.1"
_commit="cb65dd5d620a0086151cbcf3b96a9c79c2fa0d2b"
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
[[ "${_git}" == true ]] && \
  makedepends+=(
    "git"
  ) && \
  source+=(
    "${pkgname}-${pkgver}::git+${_url}#tag=${pkgver}"
  ) && \
  sha256sums+=(
    SKIP
  )
[[ "${_git}" == false ]] && \
  source+=(
    "${pkgname}-${pkgver}.tar.gz::${_url}/archive/refs/tags/${pkgver}.tar.gz"
  ) && \
  sha256sums+=(
    '401ce16e6180f71979ca26198d89a9164ff2beecdd9fca7c7a2c2b4512079e23'
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
