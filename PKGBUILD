# Maintainer: arlechann <dragnov3728@gmail.com>

pkgname=pleiades-for-android-studio
pkgver="1.0"
pkgrel=1
pkgdesc="Localize Android Studio for Japanese"
arch=('x86_64')
url="https://pleiades.io"
license=('EPL')
depends=('android-studio')
#makedepends=()
#changelog=
source=(http://ftp.jaist.ac.jp/pub/mergedoc/pleiades/build/stable/pleiades.zip)
install=$pkgname.install
md5sums=('420e5281776a58cf112a17619982a611')

build() {
  if [ ! -d $HOME/.AndroidStudio*.*/config ]; then
    exit 1
  fi
}

package() {
  _target_dir=$(echo $HOME/.AndroidStudio*.*/config | xargs -n1 | sort -r | head -n1)

  mkdir -p $pkgdir$_target_dir
  chmod 700 $pkgdir$HOME
  cp -r $srcdir/plugins/jp.sourceforge.mergedoc.pleiades $pkgdir$_target_dir/

  if [ -e $_target_dir/studio64.vmoptions ]; then
    cp $_target_dir/studio64.vmoptions $pkgdir$_target_dir/
  else
    touch $pkgdir$_target_dir/studio64.vmoptions
  fi

  if grep -qF -- '-Xverify:none' $pkgdir$_target_dir/studio64.vmoptions; then
    :
  else
    echo '-Xverify:none' >> $pkgdir$_target_dir/studio64.vmoptions
  fi

  if grep -qF -- "-javaagent:$_target_dir/jp.sourceforge.mergedoc.pleiades/pleiades.jar" $pkgdir$_target_dir/studio64.vmoptions; then
    :
  else
    echo "-javaagent:$_target_dir/jp.sourceforge.mergedoc.pleiades/pleiades.jar" >> $pkgdir$_target_dir/studio64.vmoptions
  fi
}
