EXTRA_DIST =
noinst_PROGRAMS =

include mongoc/Makefile.include
include examples/Makefile.include
include tests/Makefile.include
include tools/Makefile.include
include doc/Makefile.include

if HAVE_PYTHON
include bindings/python/Makefile.include
endif

ACLOCAL_AMFLAGS = -I m4 ${ACLOCAL_FLAGS}
DISTCHECK_CONFIGURE_FLAGS = --enable-silent-rules

AM_CTAGSFLAGS = --fields=+l --languages=c

mongocdocdir = ${docdir}
mongocdoc_DATA =
mongocdoc_DATA += COPYING
mongocdoc_DATA += NEWS
mongocdoc_DATA += README

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA =
pkgconfig_DATA += $(top_builddir)/mongoc/libmongoc-1.0.pc
if HAVE_SSL
pkgconfig_DATA += $(top_builddir)/mongoc/libmongoc-ssl-1.0.pc
endif

EXTRA_DIST += $(mongocdoc_DATA)

dist-hook:
	@if test -d "$(srcdir)/.git"; then                              \
          (cd "$(srcdir)" &&                                            \
           $(top_srcdir)/missing --run git log --stat ) > ChangeLog.tmp \
           && mv -f ChangeLog.tmp $(top_distdir)/ChangeLog              \
           || (rm -f ChangeLog.tmp;                                     \
               echo Failed to generate ChangeLog >&2);                  \
	else                                                            \
	  echo A git checkout is required to generate a ChangeLog >&2;  \
	fi

uninstall-local:
	-rm -r $(mongocdocdir)
