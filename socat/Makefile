#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License, Version 1.0 only
# (the "License").  You may not use this file except in compliance
# with the License.
#
# You can obtain a copy of the license at COPYING
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at COPYING.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#
# Copyright (c) 2012 Joyent Inc.,  All rights reserved.
#

VER=socat-1.7.1.3
BASE=$(PWD)
DESTDIR=$(BASE)/../proto
GCC=$(DESTDIR)/usr/sfw/bin/gcc

all: $(VER)/config.status
	(cd $(VER); env - \
	    PATH=$(PATH) \
	    CC=$(GCC) \
	    gmake $(PARALLEL) )

install: all
	mkdir -p $(DESTDIR)
	( cd $(VER); \
	    gmake DESTDIR=$(DESTDIR) install)

clean:
	rm -rf $(VER)

$(VER)/config.status: $(VER)/configure
	(cd $(VER); \
	    CC=$(GCC) \
	    ./configure --prefix=/usr --disable-interface --disable-readline)

$(VER)/configure: $(VER).tar.gz
	gtar -zxf $(VER).tar.gz

