# This file is part of BlackArch Linux ( http://blackarch.org ).
# See COPYING for license details.

pkgname='v3n0m'
pkgver=99.f588898
pkgrel=5
groups=('blackarch' 'blackarch-scanner')
pkgdesc='A tool to automate mass SQLi d0rk scans and Metasploit Vulns.'
arch=('any')
url='https://github.com/v3n0m-Scanner/V3n0M-Scanner'
license=('GPL2')
depends=('python' 'python-httplib2' 'python-aiohttp' 'python-asyncio'
         'python-socksipy-branch' 'pip')
makedepends=('git')
source=('git+https://github.com/v3n0m-Scanner/V3n0M-Scanner.git')
sha1sums=('SKIP')

prepare() {
  cd "$srcdir/V3n0M-Scanner"

  find src/modules/. -type f -name '*.py' -exec \
    sed -i '/usr\/bin\/python/ {$!N;d;}' {} \;

  find src/modules/. -type f -name '*.py' -exec \
    sed -i '1 i\#!/usr/bin/python3' {} \;
}

package() {
  cd "$srcdir/V3n0M-Scanner"

  mkdir -p "$pkgdir/usr/bin"
  mkdir -p "$pkgdir/usr/share/v3n0m"

  install -Dm755 src/v3n0m.py "$pkgdir/usr/bin/v3n0m"
  install -Dm644 README.md "$pkgdir/usr/share/doc/v3n0m/README.md"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/v3n0m/LICENSE"

  rm README.md LICENSE PKGBUILD setup.py

  cp -a src/* "$pkgdir/usr/share/v3n0m"

  cat > "$pkgdir/usr/bin/v3n0m" << EOF
#!/bin/sh
cd /usr/share/v3n0m
python3 v3n0m.py "\$@"
EOF

  chmod a+x "$pkgdir/usr/bin/v3n0m"
}
