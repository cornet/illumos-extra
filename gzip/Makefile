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

VER=gzip-1.3.5
BASE=$(PWD)
DESTDIR=$(BASE)/../proto
BINDIR=$(DESTDIR)/usr/bin
MANDIR=$(DESTDIR)/usr/share/man/man1
GCC=$(DESTDIR)/usr/sfw/bin/gcc

all: $(VER)/config.status
	( cd $(VER); env - PATH=$(PATH) \
	    CC=$(GCC) \
	    gmake $(PARALLEL) )

install: all
	mkdir -p $(DESTDIR)
	( cd $(VER); \
	    gmake $(PARALLEL) DESTDIR=$(DESTDIR) install)
	mv $(BINDIR)/zcmp $(BINDIR)/gzcmp
	mv $(BINDIR)/zdiff $(BINDIR)/gzdiff
	mv $(BINDIR)/zegrep $(BINDIR)/gzegrep
	mv $(BINDIR)/zfgrep $(BINDIR)/gzfgrep
	mv $(BINDIR)/zforce $(BINDIR)/gzforce
	mv $(BINDIR)/zgrep $(BINDIR)/gzgrep
	mv $(BINDIR)/zless $(BINDIR)/gzless
	mv $(BINDIR)/zmore $(BINDIR)/gzmore
	mv $(BINDIR)/znew $(BINDIR)/gznew
	mv $(MANDIR)/zdiff.1 $(MANDIR)/gzdiff.1
	mv $(MANDIR)/zforce.1 $(MANDIR)/gzforce.1
	mv $(MANDIR)/zgrep.1 $(MANDIR)/gzgrep.1
	mv $(MANDIR)/zless.1 $(MANDIR)/gzless.1
	mv $(MANDIR)/zmore.1 $(MANDIR)/gzmore.1
	mv $(MANDIR)/znew.1 $(MANDIR)/gznew.1

clean:
	rm -rf $(VER)

$(VER)/config.status: $(VER)/configure
	    (cd $(VER); CC=$(GCC) ./configure --prefix=/usr)

$(VER)/configure: $(VER).tar.gz
	gtar -zxf $(VER).tar.gz
	(cd $(VER) \
	; gpatch -p3 --no-backup-if-mismatch < ../gzip-security-diff \
	; gpatch -p1 --no-backup-if-mismatch < ../gzip-6294656-6283819-diff \
	; gpatch -p1 --no-backup-if-mismatch < ../gzip.c-message-diff )
	(cd $(VER) ; autoconf -f )

