pkgname=qtjambi-git
pkgver=20110929
pkgrel=2

arch=('i686' 'x86_64')

pkgdesc="Java bindings for the Qt C++ toolkit."
url='http://qt-jambi.org/'
license=('GPL')

source=('build.patch' 'webkit.patch')
md5sums=('bd44983a29fcbf92b4d2e69f886e243f' '9f9ddb0719c304f9807fec10d46a4b76')

depends=('qt>=4.7.4' 'java-environment>=6')
makedepends=('phonon' 'wget' 'apache-ant')
conflicts=('qtjambi')
provides=('qtjambi')

build() {
	cd "$srcdir"
	
	#download latest source tarball
	if [ -f "master" ]; then
		rm master
	fi
	wget http://qt.gitorious.org/qt-jambi/qtjambi-community/archive-tarball/master
	if [[ $(file --mime-type -b master) = "text/plain" ]]; then
		echo "Source currently not available. Cause:" 1>&2
		cat master 1>&2
		rm master
		exit 1
	fi
	tar -xf master --strip-components=1 -C qtjambi-git
	
	cd $pkgname
	
	#patch build.properties
	patch -p0 < "$srcdir/build.patch"
	#patch in webkit linking
	patch -p0 < "$srcdir/webkit.patch"
	
	#build
	ant all
}

package() {
	cd "$srcdir/$pkgname"
	
	# Install qtjambi
	mkdir -p "$pkgdir/usr/share/java/"
	install -Dm644 qtjambi-*.jar "$pkgdir/usr/share/java/"
	# Install qtjambi-jni
	mkdir -p "$pkgdir/usr/lib/jni/"
	install -Dm644 build/platform-output/lib/libcom_trolltech_qt_* build/platform-output/lib/libqtjambi.so* "$pkgdir/usr/lib/jni/"
	# Install qtjambi-designer
	mkdir -p "$pkgdir/usr/lib/qt/plugins/designer/"
	install -Dm644 build/platform-output/plugins-designer/designer/*.so "$pkgdir/usr/lib/qt/plugins/designer/"
}