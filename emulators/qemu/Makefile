# $OpenBSD: Makefile,v 1.190 2019/08/18 06:56:07 ajacoutot Exp $

ONLY_FOR_ARCHS=	aarch64 amd64 arm i386 powerpc sparc64

COMMENT=	multi system emulator

DISTNAME=	qemu-4.1.0
CATEGORIES=	emulators
MASTER_SITES=	https://download.qemu.org/
EXTRACT_SUFX=	.tar.xz

HOMEPAGE=	https://www.qemu.org/

MAINTAINER=	Brad Smith <brad@comstyle.com>

# GPLv2, LGPLv2 and BSD
PERMIT_PACKAGE=	Yes

WANTLIB=	SDL2 X11 atk-1.0 bz2 c cairo cairo-gobject capstone curl \
		curses epoxy fdt>=4.1 gbm gdk-3 gdk_pixbuf-2.0 gio-2.0 \
		glib-2.0 gnutls gobject-2.0 gthread-2.0 gtk-3 iconv intl \
		iscsi jpeg lzo2 m nettle nfs pango-1.0 pangocairo-1.0 \
		pcre2-8 pixman-1 png sndio ssh usb-1.0 util vte-2.91 \
		xkbcommon xml2 z ${COMPILER_LIBCXX}

# Using TLS emulation layer
COMPILER =	base-clang ports-gcc

MODULES=	lang/python

BUILD_DEPENDS=	devel/gettext,-tools \
		textproc/py-sphinx
LIB_DEPENDS=	archivers/bzip2 \
		archivers/lzo2 \
		converters/libiconv \
		devel/capstone/main \
		devel/dtc>=1.5.0p0 \
		devel/gettext,-runtime \
		devel/glib2 \
		devel/libiscsi \
		devel/libnfs \
		devel/libusb1 \
		devel/sdl2 \
		devel/vte3 \
		graphics/jpeg \
		graphics/png \
		net/curl \
		security/gnutls \
		security/libnettle \
		security/libssh \
		textproc/libxml \
		x11/gtk+3 \
		x11/xkbcommon

MODPY_RUNDEP=	No

MAKE_ENV=	V=1
FAKE_FLAGS=	qemu_confdir=${PREFIX}/share/examples/qemu

EXTRA_CFLAGS=	-I${LOCALBASE}/include -I${X11BASE}/include
EXTRA_LDFLAGS=	-L${LOCALBASE}/lib -L${X11BASE}/lib

# fix build with ancient ncurses. ncurses needs to be updated to 5.9 or newer.
EXTRA_CFLAGS+=	-D_XOPEN_SOURCE_EXTENDED

# until the system headers are fixed properly.
EXTRA_CFLAGS+=	-Wno-redundant-decls

USE_GMAKE=	Yes
CONFIGURE_STYLE=simple
CONFIGURE_ARGS=	--prefix=${PREFIX} \
		--sysconfdir=${SYSCONFDIR} \
		--mandir=${PREFIX}/man \
		--python=${MODPY_BIN} \
		--smbd=${LOCALBASE}/sbin/smbd \
		--cc="${CC}" \
		--cxx="${CXX}" \
		--host-cc="${CC}" \
		--extra-cflags="${EXTRA_CFLAGS}" \
		--extra-ldflags="${EXTRA_LDFLAGS}" \
		--disable-bsd-user \
		--enable-capstone=system \
		--enable-curses \
		--disable-auth-pam \
		--disable-gcrypt \
		--disable-sdl-image \
		--disable-smartcard \
		--disable-snappy \
		--disable-spice \
		--disable-usb-redir \
		--disable-vnc-sasl

FLAVORS=	debug
FLAVOR?=

.if ${FLAVOR:Mdebug}
CFLAGS+=	-O0
CONFIGURE_ARGS+=--enable-debug
INSTALL_STRIP=
.else
CONFIGURE_ARGS+=--disable-debug-info
.endif

TEST_TARGET=	check

post-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/examples/qemu
	${INSTALL_SCRIPT} ${FILESDIR}/qemu-ifup \
	    ${PREFIX}/share/examples/qemu
	${INSTALL_SCRIPT} ${FILESDIR}/qemu-ifdown \
	    ${PREFIX}/share/examples/qemu

.include <bsd.port.mk>
