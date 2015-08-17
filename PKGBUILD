# Maintainer: Firat Akandere <f.akandere@gmail.com>
pkgname=tagainijisho-git
_pkgname=tagainijisho
pkgver=20130620
pkgrel=1
pkgdesc="A Free Japanese dictionary and study assistant"
arch=('i686', 'x86_64')
url="http://www.tagaini.net/"
license=('GPL3')
depends=('qt4>=4.7' 'sqlite3>=3.7.9')
makedepends=('git' 'cmake>=2.8.1' 'desktop-file-utils' 'gzip')
optdepends=('multimarkdown-git: Create multimarkdown documents')
_gitroot="git://github.com/Gnurou/${_pkgname}.git"
source=("$_gitroot"
'ftp://ftp.monash.edu.au/pub/nihongo/JMdict.gz'
'http://www.csse.monash.edu.au/~jwb/kanjidic2/kanjidic2.xml.gz'
'http://cloud.github.com/downloads/KanjiVG/kanjivg/kanjivg-20120401.xml.gz')
md5sums=('SKIP'
         '6a8e4cd261211c94209240f1c3d13542'
         'c99e3ff22b31a184d5676d1452ee5bd2'
         'ba8c661d8b16deca8e406479fdf6c215')
         
_gitname=$_pkgname

build() {  
  rm -rf "$srcdir/$_gitname/3rdparty"
  mkdir "$srcdir/$_gitname/3rdparty"
  mv "$srcdir/JMdict" "$srcdir/$_gitname/3rdparty/JMdict"
  mv "$srcdir/kanjidic2.xml" "$srcdir/$_gitname/3rdparty/kanjidic2.xml"
  mv "$srcdir/kanjivg-20120401.xml" "$srcdir/$_gitname/3rdparty/kanjivg.xml"
  
  msg "Starting make"
  
  cd "$srcdir/$_gitname"
  
  CFLAGS=`echo $CFLAGS | sed 's/-ffast-math//'` cmake -DCMAKE_EXE_LINKER_FLAGS="${CMAKE_EXE_LINKER_FLAGS} -lpthread -ldl" -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr -DQT_QMAKE_EXECUTABLE=qmake-qt4 . || return 1
  make $MAKEFLAGS || return 1
}

package() {
  cd "$srcdir/$_gitname"
  
  make DESTDIR=${pkgdir} install
  
  install -D -m 644 "${srcdir}/$_gitname/COPYING.txt" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -D -m 644 "${srcdir}/$_gitname/${_pkgname}.desktop" "${pkgdir}/usr/share/applications/${_pkgname}.desktop"
}
# vim:set ts=2 sw=2 et:
