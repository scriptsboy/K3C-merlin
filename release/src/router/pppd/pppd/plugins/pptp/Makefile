#***********************************************************************
#
# Makefile
#
# This program may be distributed according to the terms of the GNU
# General Public License, version 2 or (at your option) any later version.
#
#***********************************************************************

DESTDIR = $(INSTROOT)/usr
LIBDIR = $(DESTDIR)/lib/pppd/$(PPPDVERSION)

PPPDVERSION = $(shell awk -F '"' '/VERSION/ { print $$2; }' ../../patchlevel.h)

INSTALL	= install

# Version is set ONLY IN THE MAKEFILE!  Don't delete this!
PLUGINVERSION=0.8.5b

COPTS=-O2 -g
CFLAGS= $(COPTS) -I. -I../.. -I../../../include '-DPLUGINVERSION="$(PLUGINVERSION)"' $(EXTRACFLAGS) 
all: pptp.so

pptp.so: libplugin.a pptp.o
	$(LD) -o pptp.so -shared pptp.o libplugin.a

install: all
	$(INSTALL) -d -m 755 $(LIBDIR)
	$(INSTALL) -s -c -m 755 pptp.so $(LIBDIR)

pptp.o: pptp.c
	$(CC) $(CFLAGS) -I../../.. -c -o $@ -fPIC $^

libplugin.a: dirutil.o orckit_quirks.o pptp_callmgr.o pptp_ctrl.o pptp_quirks.o util.o vector.o inststr.o
	$(AR) -rc $@ $^

clean:
	rm -f *.o *.so *.a

%.o: %.c
	$(CC) $(CFLAGS) -c -o $@ -fPIC $^
