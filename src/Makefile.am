## Process this file with automake to produce Makefile.in

SUBDIRS = . tests

NULL =

EXTRA_DIST =

CLEANFILES =

CPPFLAGS =                                                                     \
	-I$(top_builddir) -I$(top_srcdir)                                      \
	-DPACKAGE_LIBEXEC_DIR=\""$(libexecdir)"\"                              \
	-DPACKAGE_SYSCONF_DIR=\""$(sysconfdir)"\"                              \
	-DPACKAGE_DATA_DIR=\""$(datadir)"\"                                    \
	-DPACKAGE_BIN_DIR=\""$(bindir)"\"                                      \
	-DPACKAGE_LOCALSTATE_DIR=\""$(localstatedir)"\"                        \
	-DPACKAGE_LOCALE_DIR=\""$(localedir)"\"                                \
	-DPACKAGE_LIB_DIR=\""$(libdir)"\"                                      \
	-DUDISKS_MODULE_DIR=\"$(libdir)/udisks2/modules\"                      \
	-D_POSIX_PTHREAD_SEMANTICS -D_REENTRANT                                \
	-DUDISKS_COMPILATION                                                   \
	-DBUILD_DIR=\"$(abs_top_builddir)/\"                                   \
	$(POLKIT_GOBJECT_1_CFLAGS)                                             \
	$(GUDEV_CFLAGS)                                                        \
	$(GLIB_CFLAGS)                                                         \
	$(GIO_CFLAGS)                                                          \
	$(GMODULE_CFLAGS)                                                      \
	$(BLOCKDEV_CFLAGS)                                                     \
	$(WARN_CFLAGS)                                                         \
	$(NULL)

# ------------------------------------------------------------------------------

BUILT_SOURCES =                                                                \
	udisks-daemon-marshal.h    udisks-daemon-marshal.c                     \
	udisks-daemon-resources.h  udisks-daemon-resources.c                   \
	$(NULL)

udisks-daemon-marshal.h: udisks-daemon-marshal.list
	glib-genmarshal $< --prefix=udisks_daemon_marshal --header > $@

udisks-daemon-marshal.c: udisks-daemon-marshal.list
	echo "#include \"udisks-daemon-marshal.h\"" > $@ &&                    \
	        glib-genmarshal $< --prefix=udisks_daemon_marshal --body >> $@

udisks-daemon-resources.h: udisks-daemon-resources.xml $(top_srcdir)/data/builtin_mount_options.conf
	glib-compile-resources --target=$@ --generate-header --sourcedir=$(top_srcdir) udisks-daemon-resources.xml

udisks-daemon-resources.c: udisks-daemon-resources.xml $(top_srcdir)/data/builtin_mount_options.conf
	glib-compile-resources --target=$@ --generate-source --sourcedir=$(top_srcdir) udisks-daemon-resources.xml

EXTRA_DIST +=                                                                  \
	udisks-daemon-marshal.list                                             \
	udisks-daemon-resources.xml                                            \
	$(NULL)

CLEANFILES += $(BUILT_SOURCES)

# ------------------------------------------------------------------------------

noinst_LTLIBRARIES = libudisks-daemon.la

libudisks_daemon_la_SOURCES =                                                    \
	udisksdaemontypes.h                                                      \
	udisksdaemon.h                   udisksdaemon.c                          \
	udisksprovider.h                 udisksprovider.c                        \
	udiskslinuxprovider.h            udiskslinuxprovider.c                   \
	udiskslinuxblockobject.h         udiskslinuxblockobject.c                \
	udiskslinuxblock.h               udiskslinuxblock.c                      \
	udiskslinuxpartition.h           udiskslinuxpartition.c                  \
	udiskslinuxpartitiontable.h      udiskslinuxpartitiontable.c             \
	udiskslinuxfilesystem.h          udiskslinuxfilesystem.c                 \
	udiskslinuxfilesystemhelpers.h   udiskslinuxfilesystemhelpers.c          \
	udiskslinuxencrypted.h           udiskslinuxencrypted.c                  \
	udiskslinuxencryptedhelpers.h    udiskslinuxencryptedhelpers.c           \
	udiskslinuxswapspace.h           udiskslinuxswapspace.c                  \
	udiskslinuxloop.h                udiskslinuxloop.c                       \
	udiskslinuxdriveobject.h         udiskslinuxdriveobject.c                \
	udiskslinuxdrive.h               udiskslinuxdrive.c                      \
	udiskslinuxdriveata.h            udiskslinuxdriveata.c                   \
	udiskslinuxmdraidobject.h        udiskslinuxmdraidobject.c               \
	udiskslinuxmdraidhelpers.h       udiskslinuxmdraidhelpers.c              \
	udiskslinuxmdraid.h              udiskslinuxmdraid.c                     \
	udiskslinuxmanager.h             udiskslinuxmanager.c                    \
	udiskslinuxmountoptions.h        udiskslinuxmountoptions.c               \
	udiskslinuxfsinfo.h              udiskslinuxfsinfo.c                     \
	udisksbasejob.h                  udisksbasejob.c                         \
	udisksspawnedjob.h               udisksspawnedjob.c                      \
	udisksthreadedjob.h              udisksthreadedjob.c                     \
	udiskssimplejob.h                udiskssimplejob.c                       \
	udisksmount.h                    udisksmount.c                           \
	udisksmountmonitor.h             udisksmountmonitor.c                    \
	udisksdaemonutil.h               udisksdaemonutil.c                      \
	udiskslogging.h                  udiskslogging.c                         \
	udisksstate.h                    udisksstate.c                           \
	udisksprivate.h                                                          \
	udisksfstabentry.h               udisksfstabentry.c                      \
	udiskscrypttabentry.h            udiskscrypttabentry.c                   \
	udiskscrypttabmonitor.h          udiskscrypttabmonitor.c                 \
	udisksutabentry.h                udisksutabentry.c                       \
	udisksutabmonitor.h              udisksutabmonitor.c                     \
	udiskslinuxdevice.h              udiskslinuxdevice.c                     \
	udisksata.h                      udisksata.c                             \
	udisksmodulemanager.h            udisksmodulemanager.c                   \
	udisksmoduleobject.h             udisksmoduleobject.c                    \
	udisksmodule.h                   udisksmodule.c                          \
	udisksconfigmanager.h            udisksconfigmanager.c                   \
	udiskslinuxnvmecontroller.h      udiskslinuxnvmecontroller.c             \
	udiskslinuxnvmenamespace.h       udiskslinuxnvmenamespace.c              \
	$(BUILT_SOURCES)                                                         \
	$(NULL)

libudisks_daemon_la_CFLAGS =                                                   \
	-I$(top_srcdir)                                                        \
	-DG_LOG_DOMAIN=\"udisks\"                                              \
	$(GLIB_CFLAGS)                                                         \
	$(GIO_CFLAGS)                                                          \
	$(GMODULE_CFLAGS)                                                      \
	$(GUDEV_CFLAGS)                                                        \
	$(LIBATASMART_CFLAGS)                                                  \
	$(LIBBLKID_CFLAGS)                                                     \
	$(LIBMOUNT_CFLAGS)                                                     \
	$(LIBUUID_CFLAGS)                                                      \
	$(POLKIT_GOBJECT_1_CFLAGS)                                             \
	$(ACL_CFLAGS)                                                          \
	$(LIBSYSTEMD_LOGIN_CFLAGS)                                             \
	$(LIBELOGIND_CFLAGS)                                                   \
	$(PART_CFLAGS)                                                         \
	$(SWAP_CFLAGS)                                                         \
	$(NULL)

libudisks_daemon_la_LIBADD =                                                   \
	$(GLIB_LIBS)                                                           \
	$(GIO_LIBS)                                                            \
	$(GMODULE_LIBS)                                                        \
	$(GUDEV_LIBS)                                                          \
	$(BLOCKDEV_LIBS)                                                       \
	-lbd_utils                                                             \
	$(LIBATASMART_LIBS)                                                    \
	$(LIBBLKID_LIBS)                                                       \
	$(LIBMOUNT_LIBS)                                                       \
	$(LIBUUID_LIBS)                                                        \
	$(POLKIT_GOBJECT_1_LIBS)                                               \
	$(ACL_LIBS)                                                            \
	$(LIBSYSTEMD_LOGIN_LIBS)                                               \
	$(LIBELOGIND_LIBS)                                                     \
	$(PART_LDFLAGS)                                                        \
	$(SWAP_LIBS)                                                           \
	$(top_builddir)/udisks/libudisks2.la                                   \
	$(NULL)

# ------------------------------------------------------------------------------

udisksdprivdir = $(libexecdir)/udisks2
udisksdpriv_PROGRAMS = udisksd

udisksd_SOURCES =                                                              \
	main.c                                                                 \
	$(NULL)

udisksd_CFLAGS =                                                               \
	-DG_LOG_DOMAIN=\"udisksd\"                                             \
	$(NULL)

udisksd_LDADD =                                                                \
	$(GLIB_LIBS)                                                           \
	$(GIO_LIBS)                                                            \
	$(GMODULE_LIBS)                                                        \
	$(BLOCKDEV_LIBS)                                                       \
	libudisks-daemon.la                                                    \
	$(NULL)

# ------------------------------------------------------------------------------

install-data-local:
	-$(mkdir_p) $(DESTDIR)$(sysconfdir)/udisks2
	-$(mkdir_p) $(DESTDIR)$(localstatedir)/lib/udisks2
	-chmod 0700 $(DESTDIR)$(localstatedir)/lib/udisks2
