#
#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#
# Copyright 2009 Sun Microsystems, Inc.  All rights reserved.
# Use is subject to license terms.
#
# Copyright (c) 2012 Joyent Inc.
#

VER=vim72
BASE=$(PWD)
DESTDIR=$(BASE)/../proto

GCC=$(DESTDIR)/usr/sfw/bin/gcc
GXX=$(DESTDIR)/usr/sfw/bin/g++

all: $(VER)/src/auto/config.status
	(cd $(VER); env \
	    "CC=$(GCC)" \
	    "CXX=$(GXX)" \
	    STRIP=/usr/bin/strip \
	    PATH=$(DESTDIR)/usr/sfw/bin:$(PATH) \
	    make -e $(PARALLEL))

install: all
	(cd $(VER); env \
	    "CC=$(GCC)" \
	    "CXX=$(GXX)" \
	    STRIP=/usr/bin/strip \
	    PATH=$(DESTDIR)/usr/sfw/bin:$(PATH) \
	    DESTDIR=$(DESTDIR) \
	    make -e install)

$(VER)/src/auto/config.status: $(VER)/configure
	(cd $(VER); env \
	    "CC=$(GCC)" \
	    "CXX=$(GXX)" \
	    STRIP=/usr/bin/strip \
	    PATH=$(DESTDIR)/usr/sfw/bin:$(PATH) \
	    ./configure --prefix=/usr \
	      --disable-gui \
	      --disable-gtktest \
	      --with-features=huge \
	      --without-x )

$(VER)/configure:
	gtar -jxf $(VER).tar.bz2
	touch $(VER)/configure

clean:
	-rm -rf $(VER)
