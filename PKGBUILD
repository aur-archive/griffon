# $Id$
# Maintainer: Erich Paul <erpl@gmx.net>

pkgname=griffon
pkgver=1.4.0
pkgrel=1
pkgdesc="A Grails-like Rich Application Platform"
arch=('any')
url="http://griffon.codehaus.org/"
depends=('java-environment' 'bash' 'sh')
makedepends=('setconf')
optdepends=('groovy')
options=(!emptydirs)
license=('APACHE')
source=("http://dl.bintray.com/content/aalmiray/Griffon/griffon-$pkgver-bin.tgz?direct"
        "griffon.sh")
md5sums=('e247f9a287bcaeeff3f4ffde77cba4be'
         '61a30165001e39bf9fa361e06e0a9555')

build() {
  cd "$srcdir/$pkgname-$pkgver"

  msg2 "Configuring paths..."
  setconf bin/griffon DIRNAME /usr/share/griffon
  setconf bin/griffonsh DIRNAME /usr/share/griffon
  setconf bin/griffon-debug DIRNAME /usr/share/griffon
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  msg2 "Packaging executables..."
  install -Dm755 bin/griffon-debug \
    "$pkgdir/usr/share/$pkgname/bin/griffon-debug"
  install -Dm755 bin/startGriffon \
    "$pkgdir/usr/share/$pkgname/startGriffon"
  install -Dm755 bin/griffonsh \
    "$pkgdir/usr/share/$pkgname/griffonsh"
  install -Dm755 "$srcdir/griffon.sh" \
    "$pkgdir/usr/bin/$pkgname"
  install -Dm755 "$srcdir/griffon.sh" \
    "$pkgdir/usr/share/$pkgname/bin/$pkgname"

  msg2 "Packaging jars..."
  install -d "$pkgdir/usr/share/$pkgname"
  cp -r $srcdir/$pkgname-$pkgver/lib \
    "$pkgdir/usr/share/$pkgname/"
  cp -r $srcdir/$pkgname-$pkgver/dist \
    "$pkgdir/usr/share/$pkgname/"

  msg2 "Packaging class and sourcefiles..."
  mkdir -p "$pkgdir/usr/share/$pkgname/target/"
  cp -r "$srcdir/$pkgname-$pkgver/src" \
    "$pkgdir/usr/share/$pkgname/"

  msg2 "Packaging icons..."
  mkdir -p "$pkgdir/usr/share/pixmaps/"
  cp $srcdir/$pkgname-$pkgver/media/*.png \
    "$pkgdir/usr/share/pixmaps/"

  msg2 "Packaging scripts..."
  mkdir -p "$pkgdir/usr/share/$pkgname/scripts/"
  cp $srcdir/$pkgname-$pkgver/scripts/*.groovy \
    "$pkgdir/usr/share/$pkgname/scripts/"
  cp "$srcdir/$pkgname-$pkgver/scripts/log4j.properties" \
    "$pkgdir/usr/share/$pkgname/scripts/"

  msg2 "Packaging settings and configuration files..."
  mkdir -p "$pkgdir/usr/share/$pkgname/conf/"
  cp $srcdir/$pkgname-$pkgver/conf/* \
    "$pkgdir/usr/share/$pkgname/conf/"
  echo "export GRIFFON_HOME=/usr/share/griffon" \
    > "$srcdir/$pkgname-$pkgver/griffon.sh"
  install -Dm755 "$srcdir/$pkgname-$pkgver/griffon.sh" \
    "$pkgdir/etc/profile.d/griffon.sh"

  msg2 "Packaging license..."
  install -Dm644 "$srcdir/$pkgname-$pkgver/LICENSE" \
    "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
