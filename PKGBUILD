# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=cleo
pkgname="${_py}-${_pkg}"
pkgver=2.1.0
pkgrel=2
pkgdesc="create beautiful and testable command-line interfaces"
arch=(
  any
)
_http="https://github.com"
_ns="python-poetry"
url="${_http}/${_ns}/${_pkg}"
license=(
  MIT
)
depends=(
  "${_py}-crashtest"
  "${_py}-rapidfuzz"
  "${_py}-typing_extensions"
)
makedepends=(
  "${_py}-"{"build","installer","wheel"}
  "${_py}-poetry-core"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-pytest-mock"
)
_archive="${_pkgname}-${pkgver}"
source=(
  "${url}/archive/${pkgver}/${_archive}.tar.gz"
)
sha256sums=(
  'f5905052d783d540271de62b546c8ad89792e8c2787a59c41b0d8c8c31934093'
)
b2sums=(
  '7c9d0cc869d1e185c2c5a092a8aa1d1b3cce5fc25246939c0ff94920ac7070000b110be9f6cd9d1f827ed951ff22b9ad62e3c17a941022967b7599e456cda837'
)

prepare() {
  cd \
    "${_archive}"
  # we do not use overly strict version constraints
  sed \
    -e \
      's/\^/>=/g' \
    -e \
      's/~=/>=/g' \
    -i \
    "pyproject.toml"
}

build(){
  cd \
    "${_archive}"
  "${_py}" \
    -m \
      build \
    -wn
}

check() {
  cd \
    "${_archive}"
  export \
    PYTHONPATH="${PWD}/src"
  pytest \
    -vv
}

package() {
  cd \
    "${_archive}"
  "${_py}" \
    -m installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dm0644 \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/" \
    LICENSE
}
