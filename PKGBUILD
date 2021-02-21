# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# The following guidelines are specific to BZR, GIT, HG and SVN packages.
# Other VCS sources are not natively supported by makepkg yet.

# Maintainer: Winter Harrison <winter@wintermade.it>
pkgname=qbigscreen-git # '-bzr', '-git', '-hg' or '-svn'
pkgver=r2.4aab898
pkgrel=1
pkgdesc="a very tailored launcher"
arch=("x86_64")
url="http://wintermade.it"
license=('unknown')
groups=()
depends=('qt5-gamepad', 'streamlink', 'python', 'qjoypad', 'python-psutil')
makedepends=('git') # 'bzr', 'git', 'mercurial' or 'subversion'
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
replaces=()
backup=()
options=()
install=
source=('git+file:///home/winter/bare-repos/qbigscreen.git')
noextract=()
md5sums=('SKIP')

pkgver() {
	cd "$srcdir/${pkgname%-git}"

	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
	cd "$srcdir/${pkgname%-git}"
	patch qbigscreen.pro < ../../fix-target.patch
}

build() {
	cd "$srcdir/${pkgname%-git}"
        mkdir ../${pkgname}-build
        cd ../${pkgname}-build
        qmake PREFIX="$pkgdir" "$srcdir/${pkgname%-git}/qbigscreen.pro"
	make
}

check() {
	cd "$srcdir/${pkgname%-git}"
	# make -k check
}

package() {
	cd "$srcdir/${pkgname%-git}"
	cd ../${pkgname}-build
	make INSTALL_ROOT="$pkgdir/" install
        cd ..
        mkdir --parents $pkgdir/opt/qbigscreen
        cp ./scripts/*.* $pkgdir/opt/qbigscreen
        chmod +x $pkgdir/opt/qbigscreen/*.*
}
