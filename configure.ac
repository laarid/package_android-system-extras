dnl Versioning
dnl ----------
dnl To make new release:
dnl
dnl   laarid_micro_version += 1
dnl   laarid_interface_revision += 1
dnl
dnl if any functions have been added:
dnl
dnl   laarid_micro_version += 1
dnl   laarid_interface_revision = 0
dnl
dnl   or
dnl
dnl   laarid_minor_version += 1
dnl   laarid_micro_version = 0
dnl   laarid_interface_revision = 0
dnl
dnl if backwards compatibility has been broken:
dnl
dnl   laarid_major_version += 1
dnl   laarid_minor_version = 0
dnl   laarid_micro_version = 0
dnl   laarid_interface_revision = 0
m4_define([laarid_major_version], [0])
m4_define([laarid_minor_version], [0])
m4_define([laarid_micro_version], [1])
m4_define([laarid_interface_revision], [1])
m4_define([laarid_api_version], [laarid_major_version.0])
m4_define([laarid_release_number], [laarid_major_version])
m4_define([laarid_version],
  [laarid_major_version.laarid_minor_version.laarid_micro_version])

AC_INIT([android-system-extras], [laarid_version],
  [https://github.com/laarid/package_android-system-extras/issues], [],
  [https://github.com/laarid/package_android-system-extras])

AC_CONFIG_HEADERS([config.h])
AC_CONFIG_SRCDIR([tests/include/testUtil.h])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_AUX_DIR([build-aux])

AM_INIT_AUTOMAKE([-Wall -Werror foreign subdir-objects no-define tar-ustar])
AM_MAINTAINER_MODE([enable])
AM_SILENT_RULES([yes])

LAARID_MAJOR_VERSION=laarid_major_version
LAARID_MINOR_VERSION=laarid_minor_version
LAARID_MICRO_VERSION=laarid_micro_version
LAARID_API_VERSION=laarid_api_version
LAARID_RELEASE_NUMBER=laarid_release_number
AC_SUBST([LAARID_MAJOR_VERSION])
AC_SUBST([LAARID_MINOR_VERSION])
AC_SUBST([LAARID_MICRO_VERSION])
AC_SUBST([LAARID_API_VERSION])
AC_SUBST([LAARID_RELEASE_NUMBER])

# Define _GNU_SOURCE etc. where appropriate, e.g. for strptime() on glibc
AC_USE_SYSTEM_EXTENSIONS
# Large file support
AC_SYS_LARGEFILE

# Multi-arch environment
# ----------------------
AC_CANONICAL_HOST

AM_PROG_AR
AC_PROG_CC
AC_PROG_CXX
PKG_PROG_PKG_CONFIG([0.24])

dnl libtool versioning
dnl ------------------
LT_INIT

m4_define([laarid_binary_age], [m4_eval(100 * laarid_minor_version + laarid_micro_version)])
m4_define([lt_current], [m4_eval(laarid_binary_age - laarid_interface_revision)])
m4_define([lt_revision], [laarid_interface_revision])
dnl Whenever backward compatibility is broken, we generate libraries
dnl of different release number. That follows the library files of the
dnl same release are always compatible, and they have their lt_age
dnl equal to lt_current.
m4_define([lt_age], [lt_current])
LT_VERSION_INFO="lt_current:lt_revision:lt_age"
AC_SUBST([LT_VERSION_INFO])

LT_OUTPUT

dnl Thread implementation
dnl ---------------------
AX_PTHREAD(
  [AC_DEFINE([HAVE_PTHREAD], [1],
    [Define if you have POSIX threads libraries and header files.])
  AC_DEFINE([HAVE_PTHREADS], [1],
    [Define if you have POSIX threads libraries and header files.])],
  [AC_MSG_FAILURE([pthread not available.])])

dnl Dependencies
dnl ------------
SYSTEMCORE_API_VERSION=0.0
SYSTEMCORE_REQUIRED_VERSION=0.0.20
AC_SUBST([SYSTEMCORE_API_VERSION])
AC_SUBST([SYSTEMCORE_REQUIRED_VERSION])
PKG_CHECK_MODULES([LOG], [android-log-$SYSTEMCORE_API_VERSION >= $SYSTEMCORE_REQUIRED_VERSION])

dnl Output Files
dnl ------------
AC_CONFIG_FILES([
  Makefile
  tests/lib/testUtil/android-testutil-$LAARID_API_VERSION.pc
])
AC_OUTPUT
