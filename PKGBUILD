pkgname=qtjambi-git
pkgver=20110929
pkgrel=1

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
	cd "${srcdir}"
	
	#download latest source tarball
	if [ -f "master" ];then
	rm master
	fi
	wget http://qt.gitorious.org/qt-jambi/qtjambi-community/archive-tarball/master
	tar -xf master
	if [ $? -eq 2 ]; then
		cat master
	fi
	cd qt-jambi-qtjambi-community
	
	#patch build.properties
	patch -p0 < "$srcdir/build.patch"
	#patch in webkit linking
	patch -p0 < "$srcdir/webkit.patch"
	
	#build
	ant all
	
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
