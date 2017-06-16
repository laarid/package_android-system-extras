ACLOCAL_AMFLAGS = -I m4 ${ACLOCAL_FLAGS}

# Distribution
# ------------
EXTRA_DIST =
BUILT_SOURCES =
CLEANFILES =
DISTCLEANFILES =
MAINTAINERCLEANFILES = \
    $(GITIGNORE_MAINTAINERCLEANFILES_TOPLEVEL) \
    $(GITIGNORE_MAINTAINERCLEANFILES_M4_LIBTOOL) \
    $(GITIGNORE_MAINTAINERCLEANFILES_MAKEFILE_IN)

# We're running CI in docker, which reports host architecture as host,
# not the docker image architecture as we expected, so specifying the
# host/build information is necessary here.
DISTCHECK_CONFIGURE_FLAGS = \
    --host=$(host_alias) \
    --build=$(build_alias) \
    --disable-dependency-tracking \
    --disable-maintainer-mode

GITIGNOREFILES = \
    build \
    debian \
    $(DIST_ARCHIVES)

# Common/global flags
# -------------------
AM_CPPFLAGS = \
    -include config.h

AM_CFLAGS = \
    -Wall -Werror \
    -std=gnu99

AM_CXXFLAGS = \
    -Wall -Werror \
    -std=gnu++11

libtool_opts = \
    -version-info $(LT_VERSION_INFO) \
    -export-dynamic \
    -rpath $(libdir)

# Various build targets
# ---------------------
bin_PROGRAMS =
lib_LTLIBRARIES =
pkgconfig_DATA =
TESTS =
check_PROGRAMS =
check_LIBRARIES =
check_LTLIBRARIES =
noinst_LIBRARIES =
system_extras_inc_HEADERS =

system_extras_incdir = $(includedir)/android/system-extras-$(LAARID_API_VERSION)
include $(srcdir)/Android.mk

# PKG-CONFIG data files
# ---------------------
pkgconfigdir = $(libdir)/pkgconfig

$(pkgconfig_DATA): config.status

EXTRA_DIST += $(pkgconfig_DATA:.pc=.pc.in)
DISTCLEANFILES += \
    $(pkgconfig_DATA)

CLEANFILES += $(BUILT_SOURCES)
GITIGNOREFILES += $(BUILT_SOURCES)

-include $(top_srcdir)/git.mk
