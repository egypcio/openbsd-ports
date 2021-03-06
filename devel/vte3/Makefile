# $OpenBSD: Makefile,v 1.98 2019/10/16 19:47:09 jasper Exp $

COMMENT=		terminal emulation library

GNOME_PROJECT=		vte
GNOME_VERSION=		0.56.4
API_V=			2.91

PKGNAME=		vte3-${GNOME_VERSION}

SHARED_LIBS +=  vte-2.91              2.4      # 5400.3

CATEGORIES=		devel

MAINTAINER=		Jasper Lievisse Adriaanse <jasper@openbsd.org>, \
			Antoine Jacoutot <ajacoutot@openbsd.org>

# LGPLv2.1
PERMIT_PACKAGE=	Yes

WANTLIB += X11 Xcomposite Xcursor Xdamage Xext Xfixes Xi
WANTLIB += Xinerama Xrandr Xrender atk-1.0 atk-bridge-2.0
WANTLIB += c cairo cairo-gobject epoxy expat ffi fontconfig
WANTLIB += freetype gdk-3 gdk_pixbuf-2.0 gio-2.0 glib-2.0 gmodule-2.0
WANTLIB += gmp gnutls gobject-2.0 graphite2 gthread-2.0 gtk-3
WANTLIB += harfbuzz hogweed m nettle p11-kit pango-1.0 pangocairo-1.0
WANTLIB += pangoft2-1.0 pcre pixman-1 png pthread
WANTLIB += tasn1 xcb xcb-render xcb-shm z iconv intl idn2 pcre2-8
WANTLIB += unistring fribidi
WANTLIB += ${COMPILER_LIBCXX}

MODULES=		x11/gnome

COMPILER =		base-clang ports-gcc

BUILD_DEPENDS=		devel/gperf
# src/box_drawing_generate.sh
BUILD_DEPENDS+=		shells/bash

LIB_DEPENDS=		devel/pcre2>=10.22p0 \
			security/gnutls \
			x11/gtk+3

MODGNOME_TOOLS=		gobject-introspection vala

CONFIGURE_STYLE=	gnu

# error: -Bsymbolic-functions requested but not supported by ld
CONFIGURE_ARGS +=	--disable-Bsymbolic

TEST_DEPENDS=		shells/bash

SUBST_VARS +=		API_V

# XXX: https://bugzilla.gnome.org/show_bug.cgi?id=675987
post-install:
	rm -r ${WRKINST}${SYSCONFDIR}/profile.d

.include <bsd.port.mk>
