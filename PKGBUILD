# Contributor: Joker-jar <joker-jar@yandex.ru>

#TODO: cleanup depends

pkgname="psi-plus"
pkgver=0.16.latest
pkgrel=4
pkgdesc="Psi+ is a powerful Jabber client (Qt, C++) designed for the Jabber power users"
url="http://psi-plus.com"
license=('GPL2')
arch=('i686' 'x86_64')
depends=('qt4' 'qca-ossl' 'qca-gnupg' 'aspell' 'libxss' 'openssl' 'dbus' 'zlib')
makedepends=('wget' 'git' 'patch' 'qconf')
# Plugins (space-separated, * - build all plugins)
# Available plugins: https://github.com/psi-plus/plugins/tree/master/generic
_plugins_list="*"
# Selected translations (space-separated, leave empty to autodetect by $LANG)
# Available translations: be bg ca cs de en eo es et fi fr hu it ja mk nl pl pt pt_BR ru sk sl sr@latin sv sw uk ur_PK vi zh_CN zh_TW
_translations=""
# Use WebKit
_usewebkit=1
 
build() {

  #sleep 0;pkgrel="archlinux"
  sleep 0;pkgrel=1
  cd $srcdir
  
  #Do not modify these variables!
  PSI_DIR=$srcdir
  ICONSETS="system clients activities moods affiliations roster"
  WORK_OFFLINE=0
  PATCH_LOG="${PSI_DIR}/psipatch.log"
  SKIP_INVALID_PATCH=1
  CONF_OPTS="--prefix=/usr --libdir=/usr/lib"
  [ $_usewebkit -eq "1" ] && CONF_OPTS="${CONF_OPTS} --enable-webkit"
  INSTALL_ROOT=$pkgdir 
  PLUGINS=$_plugins_list
  TRANSLATIONS=$_translations
  
  die() { error "$@"; exit 1; }
  [ -f libpsibuild.sh ] && { rm libpsibuild.sh || die "Delete error"; }
  # checkout libpsibuild
  wget --no-check-certificate "https://raw.github.com/psi-plus/maintenance/master/scripts/posix/libpsibuild.sh" || die "Failed to update libpsibuild";
  
  . ./libpsibuild.sh
   
  #############
  # Go Go Go! #
  #############
  
  check_env $CONF_OPTS || true
  prepare_workspace || true
  fetch_all || true
  prepare_all || true
  
  sed "s/yyyyMMdd/yyyy-MM-dd/" -i ${PSI_DIR}/build/qcm/conf.qcm
  
  revision=$rev
  [ $_usewebkit -eq "1" ] && revision="${revision}webkit"
  sleep 0;pkgver=`echo $pkgver | sed "s/latest/$revision/"`
  
  compile_all || true
  install_all || true

}
