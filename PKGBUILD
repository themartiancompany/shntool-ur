# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2022, 2023, 2024, 2025  Pellegrino Prevete
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
# Maintainer: schuay <jakob.gruber@gmail.com>
# Contributor: Michal Hybner <dta081@gmail.com>

_os="$( \
  uname \
    -o)"
if [[ "${_os}" == "Android" ]]; then
  _libc="ndk-sysroot"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _libc="glibc"
fi
_pkg=shntool
_proj="shnutils"
pkgname="${_pkg}"
pkgver=3.0.10
pkgrel=7
_pkgdesc=(
  "A multi-purpose WAVE data"
  "processing and reporting utility"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'x86_64'
  'i686'
  'arm'
  'aarch64'
)
url="http://${_proj}.freeshell.org/${_pkg}"
license=(
  'GPL'
)
options=(
  !emptydirs
)
depends=(
  "${_libc}"
)
optdepends=(
  'mac: support for ape format'
  'flac: support for flac format'
  'wavpack: support for wv format'
)
# Patches taken from
# https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=684600
# https://salsa.debian.org/debian/shntool/-/tree/master/debian/patches
_patches=(
  'debian_patches_950803.patch'
  'shntool-3.0.10-large-size.diff'
  'shntool-3.0.10-large-times.diff'
  'debian_patches_no-cdquality-check.patch'
)
_patches_sums=(
  'a3aa5b817cedb4226fa32340609a5995'
  '596398b13e02b243078320ebde4743fb'
  '4265935ef1d684a4b49041278ffda7de'
  '6f0d61ddbf8cbee5c0b51a99e987ddda'
)
_tarname="${_pkg}-${pkgver}"
_uri="${url}/dist/src/${_tarname}.tar.gz"
_src="${_tarname}.tar.xz::${_uri}"
_sum='5d41f8f42c3c15e3145a7a43539c3eae'
source=(
  "${_src}"
  "${_patches[@]}"
)
md5sums=(
  "${_sum}"
  "${_patches_sums[@]}"
)
# sha256sums=(
#   "${_sum}"
#   "${_patches_sums[@]}"
# )

prepare() {
	cd \
    "${srcdir}/${_tarname}"
  for _patch in "${_patches[@]}"; do
    patch \
      -Np1 < \
      "${srcdir}/${_patch}"
  done
}

build() {
  local \
    _configure_opts=()
  _configure_opts+=(
    --prefix="/usr"
  )
	cd \
    "${srcdir}/${_tarname}"
	./configure \
    "${_configure_opts[@]}"
	make
}

package() {
  local \
    _make_opts=()
  _make_opts+=(
    DESTDIR="${pkgdir}"
  )
	cd \
    "${srcdir}/${_tarname}"
	make \
    "${_make_opts[@]}" \
    install
}


# vim:set ts=2 sw=2 et:
