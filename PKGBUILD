#!/bin/bash

# Created from the original package by Peter Bartfai, "pbartfai[at]stardust[dot]hu"

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154

# Maintainer: Ross Clark <https://github.com/Archiv8/ldview/discussions>
# Contributor: Ross Clark <https://github.com/Archiv8/ldview/discussions>

# New variables

# Official variables
# pkgbase=""
pkgname="ldview"
pkgdesc="A real-time 3D viewer for displaying LDraw models using hardware-accelerated 3D graphics"
pkgver=4.4.1
pkgrel=1
#epoch=
url="https://github.com/tcobbs/ldview"
license=("GPL2" "LGPL2.1")
arch=(x86_64)
# groups=()
depends=(
  "gl2ps"
  "glu"
  "libjpeg-turbo"
  "libpng"
  "mesa-libgl"
  "qt5-base"
  "tinyxml"
  "zlib"
)
makedepends=(
  "boost"
  "boost-libs"
  "extra-cmake-modules"
  "kdelibs4support"
  "qt5-tools"
  "unzip"
)
# checkdepends=()
optdepends=(
  "qt5-svg: to use SVG icon themes"
  "qt5-wayland: to run Qt applications in a Wayland session"
)
# provides=()
# conflicts=()
# replaces=()
# Options=()
# install=
# changelog=
source=(
  "ldview-v4.4.1.tar.gz::https://github.com/tcobbs/ldview/archive/refs/tags/v4.4.1.tar.gz"
)
# noextract=()
sha512sums=(
  "454aeb6b20548f5e53c698f02f75ca7bd5fd1ff687ffd3651bd6ed393582ece4466528ca68eb3994466c0b579a15f9b5266d30cc163207262bd7ac00a8750ac0"
)
# validpgpkeys=()

# prepare() function.  Use for preparing sources ready for compilation
# prepare() {
#
# }

# pkgver() function.  Use when needing to update pkgver variable during a
# makepkg stage
# pkgver() {
#
# }

# build() function.  Use to compile the software
build() {

  # Qmake and lrelease need to be run from the QT subdirectory
  cd ${srcdir}/${pkgname}-${pkgver}/mQT || printf "The directory for compiling was not found.  This is likely to be an issue with the packaging.  Please report an issue at https://github.com/Archiv8/ldview/issues"

  qmake -spec linux-g++-64

  lrelease LDView.pro

  make "TESTING=-I ../gl2ps -I ../3rdParty/tinyxml" clean all

  cd kde5

  mkdir -p build

  cd build

  cmake -DCMAKE_INSTALL_PREFIX=$(kf5-config --prefix) ..

  make

  cd ../../../OSMesa

  make all

}

# check() function. Us to run any checks provided by the software authors
# check() {
#
# }

# package() function. Use to put the compiled files in a directory where
# makepkg can retrieve them to create a package.
package() {

  # Needs to be installed from the QT folder
  cd "${srcdir}/${pkgname}-${pkgver}/QT"

  make INSTALL_ROOT="${pkgdir}" install

}
