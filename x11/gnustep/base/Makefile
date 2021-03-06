# $OpenBSD: Makefile,v 1.74 2019/10/16 13:45:04 ajacoutot Exp $

COMMENT=	GNUstep base library

DISTNAME=	gnustep-base-1.26.0
REVISION=	1

SHARED_LIBS=	gnustep-base 10.2
CATEGORIES=	devel

LIBDIR=		lib/GNUstep/Libraries/gnustep-base/Versions/${LIBgnustep-base_VERSION}
SUBST_VARS=	LIBDIR

HOMEPAGE=	http://www.gnustep.org/

WANTLIB += avahi-client avahi-common c ffi gmp gnutls iberty iconv
WANTLIB += m objc2 pthread lzma xml2 xslt z
WANTLIB += ${COMPILER_LIBCXX}

.if ${MACHINE_ARCH} != "i386" && ${MACHINE_ARCH} != "amd64"
WANTLIB += iberty
.endif

MASTER_SITES=	${MASTER_SITE_GNUSTEP:=core/}

MODULES =	x11/gnustep
MODGNUSTEP_NEEDS_GUI=	No
MODGNUSTEP_NEEDS_BASE=	No

LIB_DEPENDS +=	converters/libiconv \
		devel/libffi \
		devel/gmp \
		textproc/libxslt \
		security/gnutls \
		net/avahi \
		x11/gnustep/libobjc2

CONFIGURE_STYLE=gnu
CONFIGURE_ENV=	ac_cv_header_execinfo_h=false
CONFIGURE_ARGS +=	--disable-procfs \
			--disable-procfs-psinfo \
			--disable-icu
MAKE_FLAGS +=		libgnustep-base_INTERFACE_VERSION=${LIBgnustep-base_VERSION}

.include <bsd.port.mk>
