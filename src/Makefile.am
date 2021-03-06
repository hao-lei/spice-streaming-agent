# Makefile configuration for SPICE streaming agent
#
# \copyright
# Copyright 2016-2017 Red Hat Inc. All rights reserved.

NULL =

if ENABLE_TESTS
SUBDIRS = . unittests
endif

plugin_LTLIBRARIES =
plugindir = $(pkglibdir)/plugins

AM_CPPFLAGS = \
	-DSPICE_STREAMING_AGENT_PROGRAM \
	-I$(top_srcdir)/include \
	-DPLUGINSDIR=\"$(pkglibdir)/plugins\" \
	$(SPICE_PROTOCOL_CFLAGS) \
	$(X11_CFLAGS) \
	$(XFIXES_CFLAGS) \
	$(NULL)

AM_CFLAGS = \
	$(WARN_CFLAGS) \
	$(NULL)

AM_CXXFLAGS = \
	$(WARN_CXXFLAGS) \
	$(NULL)

bin_PROGRAMS = spice-streaming-agent
noinst_LIBRARIES = libstreaming-utils.a

libstreaming_utils_a_SOURCES = \
	hexdump.c \
	hexdump.h \
	$(NULL)

spice_streaming_agent_LDFLAGS = \
	$(RELRO_LDFLAGS) \
	$(NO_INDIRECT_LDFLAGS) \
	$(NULL)

spice_streaming_agent_LDADD = \
	-ldl \
	-lpthread \
	libstreaming-utils.a \
	$(X11_LIBS) \
	$(XFIXES_LIBS) \
	$(JPEG_LIBS) \
	$(NULL)

spice_streaming_agent_SOURCES = \
	spice-streaming-agent.cpp \
	concrete-agent.cpp \
	concrete-agent.hpp \
	cursor-updater.cpp \
	cursor-updater.hpp \
	error.cpp \
	error.hpp \
	frame-log.cpp \
	frame-log.hpp \
	mjpeg-fallback.cpp \
	mjpeg-fallback.hpp \
	jpeg.cpp \
	jpeg.hpp \
	stream-port.cpp \
	stream-port.hpp \
	$(NULL)

if HAVE_GST
plugin_LTLIBRARIES += gst-plugin.la

gst_plugin_la_LDFLAGS = \
	-module -avoid-version \
	$(RELRO_LDFLAGS) \
	$(NO_INDIRECT_LDFLAGS) \
	$(NULL)

gst_plugin_la_LIBADD = \
	$(GST_LIBS) \
	$(NULL)

gst_plugin_la_SOURCES = \
	gst-plugin.cpp \
	$(NULL)

gst_plugin_la_CPPFLAGS = \
	-I$(top_srcdir)/include \
	$(SPICE_PROTOCOL_CFLAGS) \
	$(GST_CFLAGS) \
	$(NULL)
endif
