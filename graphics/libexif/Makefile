# $OpenBSD: Makefile,v 1.29 2019/06/03 16:06:51 sthen Exp $

COMMENT=	extract digital camera info tags from JPEG images

DISTNAME=	libexif-0.6.21
SHARED_LIBS=	exif	13.1
REVISION=	2

CATEGORIES=	graphics

HOMEPAGE=	http://libexif.sourceforge.net/

MAINTAINER=	Stuart Henderson <sthen@openbsd.org>

# LGPLv2.1
PERMIT_PACKAGE=   Yes

MASTER_SITES=		${MASTER_SITE_SOURCEFORGE:=libexif/}
EXTRACT_SUFX=		.tar.bz2

LIB_DEPENDS=		devel/gettext,-runtime
SEPARATE_BUILD=		Yes
CONFIGURE_STYLE=	gnu
CONFIGURE_ARGS=		--disable-docs
USE_GMAKE=		Yes
WANTLIB=		iconv intl m

post-install:
	chown -R ${SHAREOWN}:${SHAREGRP} ${PREFIX}/share/doc/libexif

.include <bsd.port.mk>
