# $OpenBSD: Makefile,v 1.50 2019/06/10 14:57:59 cwen Exp $

COMMENT=	read and manipulate raw images from digital cameras

DISTNAME=	ufraw-0.22
REVISION=	4

CATEGORIES=	graphics
MASTER_SITES=	${MASTER_SITE_SOURCEFORGE:=ufraw/}
HOMEPAGE=	http://ufraw.sourceforge.net/

MAINTAINER=	Stuart Henderson <sthen@openbsd.org>

# GPLv2+
PERMIT_PACKAGE=	Yes

WANTLIB += X11 Xcomposite Xcursor Xdamage Xext Xfixes Xi Xinerama
WANTLIB += Xrandr Xrender atk-1.0 bz2 c cairo cfitsio exiv2
WANTLIB += fontconfig freetype gdk-x11-2.0 gdk_pixbuf-2.0 gimp-2.0
WANTLIB += gimpbase-2.0 gimpcolor-2.0 gimpconfig-2.0 gimpmath-2.0
WANTLIB += gimpmodule-2.0 gimpui-2.0 gimpwidgets-2.0 gio-2.0 glib-2.0
WANTLIB += gobject-2.0 gthread-2.0 gtk-x11-2.0 gtkimageview iconv intl
WANTLIB += jasper jpeg lcms2 m pango-1.0 pangocairo-1.0 pangoft2-1.0
WANTLIB += png pthread ${COMPILER_LIBCXX} tiff z

# don't remove unless you are sure:
WANTLIB += lensfun

COMPILER=		base-clang ports-gcc base-gcc

BUILD_DEPENDS=	devel/gettext,-tools

LIB_DEPENDS=	gimp->=2,<3:graphics/gimp/stable \
		graphics/lcms2 \
		archivers/bzip2 \
		graphics/exiv2 \
		math/cfitsio \
		graphics/gtkimageview \
		graphics/lensfun

USE_GMAKE=	Yes
CONFIGURE_STYLE=gnu
CONFIGURE_ENV=	CPPFLAGS="-I${LOCALBASE}/include" \
		LDFLAGS="-L${LOCALBASE}/lib -pthread" \
		CFITSIO_CFLAGS="-I${LOCALBASE}/include" \
		CFITSIO_LIBS="-lcfitsio"
CONFIGURE_ARGS=	--enable-extras

.include <bsd.port.mk>
