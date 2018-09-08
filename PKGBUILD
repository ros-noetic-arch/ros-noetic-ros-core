# Script generated with import_catkin_packages.py.
# For more information: https://github.com/bchretien/arch-ros-stacks.
pkgdesc="ROS - A metapackage to aggregate the packages required to use publish / subscribe, services, launch files, and other core ROS concepts."
url='http://www.ros.org/'

pkgname='ros-melodic-ros-core'
pkgver='1.4.1'
_pkgver_patch=0
arch=('any')
pkgrel=1
license=('BSD')

ros_makedepends=(
	ros-melodic-catkin
)

makedepends=(
	'cmake'
	'ros-build-tools'
	${ros_makedepends[@]}
)

ros_depends=(
	ros-melodic-message-generation
	ros-melodic-cmake-modules
	ros-melodic-geneus
	ros-melodic-rosgraph-msgs
	ros-melodic-roslisp
	ros-melodic-rosconsole-bridge
	ros-melodic-genpy
	ros-melodic-message-runtime
	ros-melodic-std-srvs
	ros-melodic-genmsg
	ros-melodic-rospack
	ros-melodic-catkin
	ros-melodic-ros-comm
	ros-melodic-rosconsole
	ros-melodic-class-loader
	ros-melodic-common-msgs
	ros-melodic-genlisp
	ros-melodic-ros
	ros-melodic-std-msgs
	ros-melodic-roscpp-core
	ros-melodic-pluginlib
	ros-melodic-rosbag-migration-rule
	ros-melodic-gencpp
	ros-melodic-gennodejs
)

depends=(
	${ros_depends[@]}
)

_dir=${pkgname}
source=("${_dir}"::"git+https://github.com/ros-gbp/metapackages-release.git")
sha256sums=('SKIP')

prepare() {
	cd ${srcdir}/${_dir}
	git checkout upstream
	_pkgname=$(echo ${pkgname} | sed 's/ros-lunar-//' | sed 's/-/_/g')

	if [ -d ${_pkgname} ]; then
		git subtree split -P ${_pkgname} --branch ${_pkgname}
		git checkout ${_pkgname}
	fi
}

build() {
	# Use ROS environment variables.
	source /usr/share/ros-build-tools/clear-ros-env.sh
	[ -f /opt/ros/melodic/setup.bash ] && source /opt/ros/melodic/setup.bash

	# Create the build directory.
	[ -d ${srcdir}/build ] || mkdir ${srcdir}/build
	cd ${srcdir}/build

	# Fix Python2/Python3 conflicts.
	/usr/share/ros-build-tools/fix-python-scripts.sh -v 3 ${srcdir}/${_dir}

	# Build the project.
	cmake ${srcdir}/${_dir} \
		-DCMAKE_BUILD_TYPE=Release \
		-DCATKIN_BUILD_BINARY_PACKAGE=ON \
		-DCMAKE_INSTALL_PREFIX=/opt/ros/melodic \
		-DPYTHON_EXECUTABLE=/usr/bin/python3 \
		-DPYTHON_INCLUDE_DIR=/usr/include/python3.7m \
		-DPYTHON_LIBRARY=/usr/lib/libpython3.7m.so \
		-DPYTHON_BASENAME=.cpython-37m \
		-DSETUPTOOLS_DEB_LAYOUT=OFF
	make
}

package() {
	cd "${srcdir}/build"
	make DESTDIR="${pkgdir}/" install
}