include $(top_srcdir)/src/gallium/Automake.inc

AM_CFLAGS = \
	$(GALLIUM_TARGET_CFLAGS)

omxdir = $(OMX_LIB_INSTALL_DIR)
omx_LTLIBRARIES = libomx_mesa.la

nodist_EXTRA_libomx_mesa_la_SOURCES = dummy.cpp
libomx_mesa_la_SOURCES =

libomx_mesa_la_LDFLAGS = \
	-shared \
	-module \
	-no-undefined \
	-avoid-version \
	$(GC_SECTIONS) \
	$(LD_NO_UNDEFINED)

if HAVE_LD_VERSION_SCRIPT
libomx_mesa_la_LDFLAGS += \
	-Wl,--version-script=$(top_srcdir)/src/gallium/targets/omx/omx.sym
endif # HAVE_LD_VERSION_SCRIPT

libomx_mesa_la_LIBADD = \
	$(top_builddir)/src/gallium/state_trackers/omx/libomxtracker.la \
	$(top_builddir)/src/gallium/auxiliary/libgalliumvlwinsys.la \
	$(top_builddir)/src/gallium/auxiliary/libgalliumvl.la \
	$(top_builddir)/src/gallium/auxiliary/libgallium.la \
	$(top_builddir)/src/util/libmesautil.la \
	$(OMX_LIBS) \
	$(LIBDRM_LIBS) \
	$(GALLIUM_COMMON_LIB_DEPS)

if HAVE_PLATFORM_X11
libomx_mesa_la_LIBADD += \
	$(VL_LIBS) \
	$(XCB_DRI3_LIBS)
endif

EXTRA_libomx_mesa_la_DEPENDENCIES = omx.sym
EXTRA_DIST = omx.sym

if HAVE_GALLIUM_STATIC_TARGETS

TARGET_DRIVERS =
TARGET_CPPFLAGS =
TARGET_LIB_DEPS =


include $(top_srcdir)/src/gallium/drivers/nouveau/Automake.inc

include $(top_srcdir)/src/gallium/drivers/r600/Automake.inc
include $(top_srcdir)/src/gallium/drivers/radeonsi/Automake.inc

libomx_mesa_la_SOURCES += target.c
libomx_mesa_la_CPPFLAGS = $(TARGET_CPPFLAGS)
libomx_mesa_la_LIBADD += \
	$(top_builddir)/src/gallium/auxiliary/pipe-loader/libpipe_loader_static.la \
	$(GALLIUM_PIPE_LOADER_WINSYS_LIBS) \
	$(TARGET_LIB_DEPS) \
	$(TARGET_RADEON_WINSYS) $(TARGET_RADEON_COMMON)

else # HAVE_GALLIUM_STATIC_TARGETS

libomx_mesa_la_LIBADD += \
	$(top_builddir)/src/gallium/auxiliary/pipe-loader/libpipe_loader_dynamic.la

endif # HAVE_GALLIUM_STATIC_TARGETS

if HAVE_GALLIUM_LLVM
libomx_mesa_la_LIBADD += $(LLVM_LIBS)
libomx_mesa_la_LDFLAGS += $(LLVM_LDFLAGS)
endif
