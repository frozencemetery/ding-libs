TRACE_LEVEL=@TRACE_VAR@

RPMBUILD ?= $(PWD)/rpmbuild

#Some old versions of automake don't define builddir
builddir ?= .

dist_noinst_DATA = \
    m4 \
    COPYING \
    COPYING.LESSER \
    path_utils/libpath_utils.sym \
    dhash/libdhash.sym \
    collection/libcollection.sym \
    refarray/libref_array.sym \
    basicobjects/libbasicobjects.sym \
    ini/libini_config.sym

##############################################################################
# Common
##############################################################################
AM_CFLAGS =
if HAVE_GCC
    AM_CFLAGS += \
        -Wall -Wshadow -Wstrict-prototypes -Wpointer-arith -Wcast-qual \
        -Wcast-align -Wwrite-strings -Wextra -Wno-unused-parameter \
        -Wno-sign-compare -Wformat-security -Wmissing-prototypes -Wundef
endif

AM_CPPFLAGS = \
    -I$(srcdir)/collection \
    -I$(srcdir)/path_utils \
    -I$(srcdir)/refarray \
    -I$(srcdir)/dhash \
    -I$(srcdir)/ini \
    -I$(srcdir)/basicobjects \
    -I$(srcdir) \
    -I$(srcdir)/trace \
    $(TRACE_LEVEL)

ACLOCAL_AMFLAGS = -I m4

DOXYGEN = @DOXYGEN@

pkgconfigdir = $(libdir)/pkgconfig

dist_pkgconfig_DATA =
dist_doc_DATA =
dist_examples_DATA =
dist_include_HEADERS =
lib_LTLIBRARIES =
check_PROGRAMS =
TESTS =

examplesdir = $(docdir)/examples

##############################################################################
# Path Utils
##############################################################################

lib_LTLIBRARIES += libpath_utils.la
dist_pkgconfig_DATA += path_utils/path_utils.pc
dist_include_HEADERS += path_utils/path_utils.h

libpath_utils_la_SOURCES = path_utils/path_utils.c
libpath_utils_la_DEPENDENCIES = path_utils/libpath_utils.sym
libpath_utils_la_LDFLAGS = \
    -version-info 1:1:0 \
    -Wl,--version-script=$(top_srcdir)/path_utils/libpath_utils.sym

if HAVE_CHECK
    check_PROGRAMS += path_utils_ut ini_configmod_ut_check
    TESTS += path_utils_ut ini_configmod_ut_check
endif

path_utils_ut_SOURCES = path_utils/path_utils_ut.c
path_utils_ut_CFLAGS = \
    $(AM_CFLAGS) \
    $(CHECK_CFLAGS)
path_utils_ut_LDADD = \
    $(CHECK_LIBS) \
    libpath_utils.la

path_utils-docs:
if HAVE_DOXYGEN
	cd path_utils; \
	$(DOXYGEN) path_utils.cfg.doxy;
endif

dist_doc_DATA += path_utils/README.path_utils

##############################################################################
# dhash
##############################################################################

lib_LTLIBRARIES += libdhash.la
dist_pkgconfig_DATA += dhash/dhash.pc
dist_include_HEADERS += dhash/dhash.h

libdhash_la_SOURCES = dhash/dhash.c
libdhash_la_DEPENDENCIES = dhash/libdhash.sym
libdhash_la_LDFLAGS = \
    -version-info 1:2:0 \
    -Wl,--version-script=$(top_srcdir)/dhash/libdhash.sym

check_PROGRAMS += dhash_test dhash_example
TESTS += dhash_test dhash_example

dhash_test_SOURCES = dhash/examples/dhash_test.c
dhash_test_LDADD = libdhash.la

dhash_example_SOURCES = dhash/examples/dhash_example.c
dhash_example_LDADD = libdhash.la

dist_examples_DATA += \
    dhash/examples/dhash_test.c \
    dhash/examples/dhash_example.c

dist_doc_DATA += dhash/README.dhash

##############################################################################
# collection
##############################################################################

lib_LTLIBRARIES += libcollection.la
dist_pkgconfig_DATA += collection/collection.pc
dist_include_HEADERS += \
    collection/collection.h \
    collection/collection_tools.h \
    collection/collection_queue.h \
    collection/collection_stack.h

libcollection_la_SOURCES = \
    collection/collection.c \
    collection/collection_tools.c \
    collection/collection_cnv.c \
    collection/collection_queue.c \
    collection/collection_stack.c \
    collection/collection_cmp.c \
    collection/collection_iter.c \
    collection/collection_priv.h \
    trace/trace.h
libcollection_la_DEPENDENCIES = collection/libcollection.sym
libcollection_la_LDFLAGS = \
    -version-info 5:0:1 \
    -Wl,--version-script=$(top_srcdir)/collection/libcollection.sym

check_PROGRAMS += \
    collection_ut \
    collection_stack_ut \
    collection_queue_ut
TESTS += \
    collection_ut \
    collection_stack_ut \
    collection_queue_ut

collection_ut_SOURCES = collection/collection_ut.c
collection_ut_LDADD = libcollection.la
collection_stack_ut_SOURCES = collection/collection_stack_ut.c
collection_stack_ut_LDADD = libcollection.la
collection_queue_ut_SOURCES = collection/collection_queue_ut.c
collection_queue_ut_LDADD = libcollection.la

collection-docs:
if HAVE_DOXYGEN
	cd collection; \
	$(DOXYGEN) collection.cfg.doxy
endif

##############################################################################
# refarray
##############################################################################

lib_LTLIBRARIES += libref_array.la
dist_pkgconfig_DATA += refarray/ref_array.pc
dist_include_HEADERS += refarray/ref_array.h

libref_array_la_SOURCES = \
    refarray/ref_array.c \
    trace/trace.h
libref_array_la_DEPENDENCIES = refarray/libref_array.sym
libref_array_la_LDFLAGS = \
    -version-info 3:1:2 \
    -Wl,--version-script=$(top_srcdir)/refarray/libref_array.sym

check_PROGRAMS += ref_array_ut
TESTS += ref_array_ut
ref_array_ut_SOURCES = refarray/ref_array_ut.c
ref_array_ut_LDADD = libref_array.la

dist_doc_DATA += refarray/README.ref_array

ref_array-docs:
if HAVE_DOXYGEN
	cd refarray; \
	$(DOXYGEN) ref_array.cfg.doxy
endif

##############################################################################
# basicobjects
##############################################################################

lib_LTLIBRARIES += libbasicobjects.la
dist_pkgconfig_DATA += basicobjects/basicobjects.pc
dist_include_HEADERS += basicobjects/simplebuffer.h

libbasicobjects_la_SOURCES = \
    basicobjects/simplebuffer.c \
    trace/trace.h
libbasicobjects_la_DEPENDENCIES = basicobjects/libbasicobjects.sym
libbasicobjects_la_LDFLAGS = \
    -version-info 1:0:1 \
    -Wl,--version-script=$(top_srcdir)/basicobjects/libbasicobjects.sym

check_PROGRAMS += simplebuffer_ut
TESTS += simplebuffer_ut
simplebuffer_ut_SOURCES = basicobjects/simplebuffer_ut.c
simplebuffer_ut_LDADD = libbasicobjects.la

basicobjects-docs:
if HAVE_DOXYGEN
	cd basicobjects; \
	$(DOXYGEN) basicobjects.cfg.doxy
endif


##############################################################################
# ini_config
##############################################################################

lib_LTLIBRARIES += libini_config.la
dist_pkgconfig_DATA += ini/ini_config.pc
dist_include_HEADERS += ini/ini_config.h ini/ini_configobj.h \
                        ini/ini_valueobj.h ini/ini_comment.h \
                        ini/ini_configmod.h

libini_config_la_SOURCES = \
    ini/ini_config.c \
    ini/ini_config.h \
    ini/ini_get_value.c \
    ini/ini_get_array.c \
    ini/ini_list.c \
    ini/ini_print.c \
    ini/ini_parse.c \
    ini/ini_metadata.c \
    ini/ini_metadata.h \
    ini/ini_defines.h \
    ini/ini_comment.c \
    ini/ini_comment.h \
    ini/ini_valueobj.c \
    ini/ini_valueobj.h \
    ini/ini_serialize.c \
    ini/ini_fileobj.c \
    ini/ini_configobj.c \
    ini/ini_configobj.h \
    ini/ini_configmod.h \
    ini/ini_configmod.c \
    ini/ini_config_priv.h \
    ini/ini_get_valueobj.c \
    ini/ini_get_array_valueobj.c \
    ini/ini_list_valueobj.c \
    ini/ini_augment.c \
    trace/trace.h
EXTRA_libini_config_la_DEPENDENCIES = ini/libini_config.sym
libini_config_la_LIBADD = \
    libcollection.la \
    libpath_utils.la \
    libref_array.la \
    libbasicobjects.la
libini_config_la_LDFLAGS = \
    -version-info 6:0:1 \
    -Wl,--version-script=$(top_srcdir)/ini/libini_config.sym

dist_noinst_DATA += \
    ini/ini.conf \
    ini/ini.d/real.conf \
    ini/ini.d/test.conf \
    ini/ini.d/ipa.conf \
    ini/ini.d/foo.conf.in \
    ini/ini.d/mysssd.conf \
    ini/ini.d/smerge.conf \
    ini/ini.d/sexpect.conf \
    ini/ini.d/first.conf \
    ini/ini.d/second.conf \
    ini/ini.d/space.conf \
    ini/ini.d/mergecheck.conf \
    ini/ini.d/comment.conf \
    ini/ini.d/real8.conf \
    ini/ini.d/real16be.conf \
    ini/ini.d/real16le.conf \
    ini/ini.d/real32be.conf \
    ini/ini.d/real32le.conf \
    ini/ini.d/symbols.conf \
    ini/ini.d/new_line.conf \
    ini/ini.d/merge.validator \
    ini/ini2.d/real8.conf \
    ini/ini2.d/real16be.conf \
    ini/ini2.d/real16le.conf \
    ini/ini2.d/real32be.conf \
    ini/ini2.d/real32le.conf


check_PROGRAMS += \
    ini_config_ut \
    ini_comment_ut \
    ini_valueobj_ut \
    ini_parse_ut \
    ini_augment_ut \
    ini_configmod_ut \
    ini_save_ut

TESTS += \
    ini_config_ut \
    ini_comment_ut \
    ini_valueobj_ut \
    ini_parse_ut \
    ini_augment_ut \
    ini_configmod_ut \
    ini_save_ut


ini_config_ut_SOURCES = ini/ini_config_ut.c
ini_config_ut_LDADD = \
    libini_config.la \
    libcollection.la

ini_comment_ut_SOURCES = ini/ini_comment_ut.c
ini_comment_ut_LDADD = libini_config.la

ini_valueobj_ut_SOURCES = ini/ini_valueobj_ut.c
ini_valueobj_ut_LDADD = libini_config.la libbasicobjects.la

ini_parse_ut_SOURCES = ini/ini_parse_ut.c
ini_parse_ut_LDADD = libini_config.la libcollection.la libbasicobjects.la

ini_augment_ut_SOURCES = ini/ini_augment_ut.c
ini_augment_ut_LDADD = libini_config.la libcollection.la \
                       libbasicobjects.la libpath_utils.la libref_array.la

ini_configmod_ut_SOURCES = ini/ini_configmod_ut.c
ini_configmod_ut_LDADD = libini_config.la libcollection.la \
                         libbasicobjects.la libpath_utils.la libref_array.la

ini_configmod_ut_check_SOURCES = ini/ini_configmod_ut_check.c
ini_configmod_ut_check_CFLAGS = $(AM_CFLAGS) $(CHECK_CFLAGS)
ini_configmod_ut_check_LDADD = libini_config.la libcollection.la \
                               libbasicobjects.la libpath_utils.la \
                               libref_array.la \
                               $(CHECK_LIBS)

ini_save_ut_SOURCES = ini/ini_save_ut.c
ini_save_ut_LDADD = libini_config.la libcollection.la \
                         libbasicobjects.la libpath_utils.la libref_array.la

ini_config-docs:
if HAVE_DOXYGEN
	cd ini; \
	$(DOXYGEN) ini_config.cfg.doxy
endif

clean-local-ini_config:
	rm -f ./*.out
	rm -f test.ini
	rm -f ./foo.conf ./bom* #From ini_parse_ut
	rm -f ./merge.validator.* #From ini_augment_ut
	rm -f ./real.conf.manual
	rm -f ./modtest.conf.real
	rm -f ./modtest.conf.exp
	rm -f ./test_*



##############################################################################
# Additional rules
##############################################################################


rpmroot:
	mkdir -p $(RPMBUILD)/BUILD
	mkdir -p $(RPMBUILD)/RPMS
	mkdir -p $(RPMBUILD)/SOURCES
	mkdir -p $(RPMBUILD)/SPECS
	mkdir -p $(RPMBUILD)/SRPMS

rpms: dist-gzip rpmroot
	cp $(builddir)/contrib/ding-libs.spec $(RPMBUILD)/SPECS
	cp $(distdir).tar.gz $(RPMBUILD)/SOURCES
	cd $(RPMBUILD); \
	rpmbuild --define "_topdir $(RPMBUILD)" -ba SPECS/ding-libs.spec

if GIT_CHECKOUT
prerelease-rpms:
	cp $(srcdir)/version.m4 $(srcdir)/version.m4.orig
	sed -e "s/m4_define(\[PRERELEASE_VERSION_NUMBER\], \[.*\])/m4_define(\[PRERELEASE_VERSION_NUMBER\], \[.`date +%Y%m%d%H`git`git log -1 --pretty=format:%h`\])/" < $(srcdir)/version.m4.orig > $(srcdir)/version.m4
	$(MAKE) rpms
	mv $(srcdir)/version.m4.orig $(srcdir)/version.m4
endif

# make srpms will use the old digest algorithm to be compatible
# with RHEL5
srpm: dist-gzip rpmroot
	cp $(builddir)/contrib/ding-libs.spec $(RPMBUILD)/SPECS
	cp $(distdir).tar.gz $(RPMBUILD)/SOURCES
	cd $(RPMBUILD); \
	rpmbuild --define "_topdir $(RPMBUILD)" \
	         --define _source_filedigest_algorithm=1 \
	         -bs SPECS/ding-libs.spec

if GIT_CHECKOUT
prerelease-srpm:
	cp $(srcdir)/version.m4 $(srcdir)/version.m4.orig
	sed -e "s/m4_define(\[PRERELEASE_VERSION_NUMBER\], \[.*\])/m4_define(\[PRERELEASE_VERSION_NUMBER\], \[.`date +%Y%m%d%H`git`git log -1 --pretty=format:%h`\])/" < $(srcdir)/version.m4.orig > $(srcdir)/version.m4
	$(MAKE) srpm
	mv $(srcdir)/version.m4.orig $(srcdir)/version.m4
endif

tests: all $(check_PROGRAMS)

docs: path_utils-docs collection-docs ref_array-docs ini_config-docs basicobjects-docs

clean-local: clean-local-ini_config
	rm -Rf doc
