## Process this file with automake to produce Makefile.in

NULL =

AM_CPPFLAGS = \
	-I$(top_builddir)/src -I$(top_srcdir)/src		\
	-DPACKAGE_LIBEXEC_DIR=\""$(libexecdir)"\"		\
	-DPACKAGE_SYSCONF_DIR=\""$(sysconfdir)"\"		\
	-DPACKAGE_DATA_DIR=\""$(datadir)"\"			\
	-DPACKAGE_BIN_DIR=\""$(bindir)"\"			\
	-DPACKAGE_LOCALSTATE_DIR=\""$(localstatedir)"\"		\
	-DPACKAGE_LOCALE_DIR=\""$(localedir)"\"			\
	-DPACKAGE_LIB_DIR=\""$(libdir)"\"			\
	-D_POSIX_PTHREAD_SEMANTICS -D_REENTRANT			\
	-I$(top_srcdir)						\
	$(GIO_CFLAGS)						\
	$(POLKIT_CFLAGS)					\
	$(XML_CFLAGS)						\
	$(GLIB_CFLAGS)						\
	$(HYBRIS_WIFI_CFLAGS)					\
	$(HYBRIS_PROPS_CFLAGS)


libexec_PROGRAMS = urfkilld

urfkilld_SOURCES =						\
	urf-arbitrator.h					\
	urf-arbitrator.c					\
	urf-device.h						\
	urf-device.c						\
	urf-device-kernel.h					\
	urf-device-kernel.c					\
	urf-device-ofono.h					\
	urf-device-ofono.c					\
	urf-killswitch.h					\
	urf-killswitch.c					\
	urf-input.h						\
	urf-input.c						\
	urf-config.h						\
	urf-config.c						\
	urf-polkit.h						\
	urf-polkit.c						\
	urf-ofono-manager.h					\
	urf-ofono-manager.c					\
	urf-utils.h						\
	urf-utils.c						\
	urf-daemon.h						\
	urf-daemon.c						\
	urf-main.c						\
	$(NULL)

if WITH_HYBRIS
urfkilld_SOURCES += \
	urf-device-hybris.h					\
	urf-device-hybris.c					\
	$(NULL)
endif

if SESSION_TRACKING_SYSTEMD
urfkilld_SOURCES += \
	urf-session-checker-logind.h				\
	urf-session-checker-logind.c				\
	urf-seat-logind.h					\
	urf-seat-logind.c					\
	$(NULL)
else
if SESSION_TRACKING_CK
urfkilld_SOURCES += \
	urf-session-checker-consolekit.h			\
	urf-session-checker-consolekit.c			\
	urf-seat-consolekit.h					\
	urf-seat-consolekit.c					\
	$(NULL)
else
urfkilld_SOURCES += \
	urf-session-checker-none.h				\
	urf-session-checker-none.c				\
	$(NULL)
endif
endif
urfkilld_CPPFLAGS =						\
	-I$(top_srcdir)/src					\
	-DG_LOG_DOMAIN=\"URfkill\"				\
	$(WARNINGFLAGS_C)					\
	$(AM_CPPFLAGS)

urfkilld_LDADD =						\
	-lm							\
	$(LIBUDEV_LIBS)						\
	$(GIO_LIBS)						\
	$(POLKIT_LIBS)						\
	$(XML_LIBS)						\
	$(HYBRIS_WIFI_LIBS)					\
	$(HYBRIS_PROPS_LIBS)

CLEANFILES = $(BUILT_SOURCES)

clean-local :
	rm -f *~


-include $(top_srcdir)/git.mk
