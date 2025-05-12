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
  "processing and reporting utility."
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
  "2982c4c030409f2de035b7a833048692440ec9f3445b42326e7e386caa5c9e66"
  "605f2030112e1ed6b68001d97a2ea839b00328995bbd795850fb2595f5797c68"
  "418f9cc575e9d9964ee85819b5db7b38108d2b19a32459ad5e9b5c19d5296292"
  "fc5b6b0138cb2ff492f074d8c58c1bd8f562d8dee2e536d45d9098bffc0f44e3"
)
_url="${url}"
_tarname="${_pkg}-${pkgver}"
_http_uri="${_url}/dist/src/${_tarname}.tar.gz"
_archive_sum="74302eac477ca08fb2b42b9f154cc870593aec8beab308676e4373a5e4ca2102"
_archive_sig_sum="efc003de90008e8c3dff3d5cc7913b0a173b4e6a6f167110e3c384de72fee04f"
_archive_fs_network="17000"
_archive_sig_fs_network="100"
_archive_fs_address="0x151920938488F193735e83e052368cD41F9d9362"
_archive_sig_fs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
# Dvorak
_archive_evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
_archive_evmfs_uri="evmfs://${_archive_fs_network}/${_archive_fs_address}/${_archive_sum}"
_archive_sig_evmfs_uri="evmfs://${_archive_sig_fs_network}/${_archive_sig_fs_address}/${_archive_sig_sum}"
_sum="${_archive_sum}"
source=(
  "${_patches[@]}"
)
sha256sums=(
  "${_patches_sums[@]}"
)
if [[ "${_evmfs}" == "true" ]]; then
  _archive_sig_src="${_tarname}.tar.xz.sig::${_archive_sig_evmfs_uri}"
  source+=(
    "${_archive_sig_src}"
  )
  sha256sums+=(
    "${_archive_sig_sum}"
  )
  _src="${_tarname}.tar.xz::${_archive_evmfs_uri}"
elif [[ "${_evmfs}" == "false" ]]; then
  _src="${_tarname}.tar.xz::${_http_uri}"
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)

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
