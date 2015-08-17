pkgdesc="ROS - A library to access URDFs using the DOM model."
url='http://www.ros.org/'

pkgname='ros-groovy-urdfdom'
pkgver='0.2.8'
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')
makedepends=('ros-build-tools')

depends=(ros-groovy-console-bridge
  ros-groovy-catkin
  ros-groovy-urdfdom-headers
  boost
  tinyxml)

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/urdfdom ]; then
    cd ${srcdir}/urdfdom
    git fetch origin --tags
    git reset --hard release/groovy/urdfdom/${pkgver}-2
  else
    git clone -b release/groovy/urdfdom/${pkgver}-2 git://github.com/ros-gbp/urdfdom-release.git ${srcdir}/urdfdom
  fi
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/urdfdom
  cmake ${srcdir}/urdfdom -DCATKIN_BUILD_BINARY_PACKAGE=ON -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
