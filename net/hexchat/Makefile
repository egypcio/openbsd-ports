# $OpenBSD: Makefile,v 1.26 2019/07/12 20:48:27 sthen Exp $

COMMENT =		GTK+2 IRC Client
DISTNAME =		hexchat-2.12.3
EXTRACT_SUFX =		.tar.xz
CATEGORIES =		net x11
REVISION =		8

HOMEPAGE =		http://hexchat.github.io/
# GPLv2+
PERMIT_PACKAGE =	Yes

WANTLIB += X11 Xcomposite Xcursor Xdamage Xext Xfixes Xi Xinerama
WANTLIB += Xrandr Xrender atk-1.0 c cairo crypto dbus-1 dbus-glib-1
WANTLIB += expat ffi fontconfig freetype gdk-x11-2.0 gdk_pixbuf-2.0
WANTLIB += gio-2.0 glib-2.0 gmodule-2.0 gobject-2.0 graphite2
WANTLIB += gthread-2.0 gtk-x11-2.0 harfbuzz iconv intl ${MODLUA_WANTLIB} m
WANTLIB += notify pango-1.0 pangocairo-1.0 pangoft2-1.0 pcre perl pixman-1
WANTLIB += png proxy pthread ${MODPY_WANTLIB} ssl ${COMPILER_LIBCXX} util
WANTLIB += xcb xcb-render xcb-shm z fribidi

COMPILER =		base-clang ports-gcc base-gcc

MASTER_SITES =		http://dl.hexchat.net/hexchat/

MODULES =		textproc/intltool \
			lang/lua \
			lang/python

MODLUA_VERSION =	5.3

BUILD_DEPENDS =		devel/iso-codes

LIB_DEPENDS =		devel/gettext,-runtime \
			devel/libnotify \
			net/libproxy \
			x11/gtk+2 \
			x11/dbus-glib \
			${MODPY_LIB_DEPENDS} \
			${MODLUA_LIB_DEPENDS}

MODPY_BUILDDEP =	No

RUN_DEPENDS =		devel/desktop-file-utils \
			devel/iso-codes \
			x11/gtk+3,-guic

CONFIGURE_STYLE =	gnu
CONFIGURE_ARGS +=	--enable-ipv6 \
			--enable-dbus \
			--disable-sysinfo \
			--disable-libcanberra
CONFIGURE_ENV =		CPPFLAGS=-I${LOCALBASE}/include \
			LDFLAGS=-L${LOCALBASE}/lib \
			OBJC="${CC}" \
			LUA=${MODLUA_FLAVOR}

LIBTOOL_FLAGS =		--tag=disable-static

USE_GMAKE =		Yes

NO_TEST =		Yes

.include <bsd.port.mk>
