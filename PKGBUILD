# Maintainer: tc1911 <tc191_dev@163.com>
pkgname=ene-rgb
pkgver=1.0.0
pkgrel=1
pkgdesc="铭瑄等主板 ENE 6K7750 板载 ARGB 灯效控制（常亮守护进程 + GTK4 面板）"
arch=('any')
url="https://github.com/tc1911/ene-rgb"
license=('MIT')
depends=('python-pyusb' 'python-gobject' 'gtk4' 'libadwaita')
makedepends=('git')
source=("git+$url.git#tag=v$pkgver")
sha256sums=('SKIP')

package() {
  local src="$srcdir/$pkgname"

  install -Dm755 "$src/src/ene-rgb" "$pkgdir/usr/bin/ene-rgb"
  install -Dm755 "$src/src/ene-rgb-daemon" "$pkgdir/usr/bin/ene-rgb-daemon"
  install -Dm755 "$src/src/ene-rgb-gui" "$pkgdir/usr/bin/ene-rgb-gui"
  install -Dm644 "$src/src/ene_fanctl.py" "$pkgdir/usr/share/$pkgname/ene_fanctl.py"

  install -Dm644 "$src/system/ene-rgb.service" \
    "$pkgdir/usr/lib/systemd/user/ene-rgb.service"
  install -Dm644 "$src/system/60-ene-6k7750.rules" \
    "$pkgdir/usr/lib/udev/rules.d/60-ene-6k7750.rules"
  install -Dm644 "$src/system/ene-rgb.desktop" \
    "$pkgdir/usr/share/applications/ene-rgb.desktop"

  install -Dm644 "$src/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 "$src/NOTICE" "$pkgdir/usr/share/licenses/$pkgname/NOTICE"
}
