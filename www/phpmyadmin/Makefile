# $OpenBSD: Makefile,v 1.137 2019/09/26 21:59:02 sthen Exp $

COMMENT=	tool to handle the administration of MySQL over the web

V=		4.9.0.1
REVISION=	0

PKGNAME=	phpMyAdmin-$V
DISTNAME=	phpMyAdmin-$V-all-languages
CATEGORIES=	www
HOMEPAGE=	http://www.phpmyadmin.net/

PORTROACH=	site:https://www.phpmyadmin.net/files/

MAINTAINER=	Giovanni Bechis <giovanni@openbsd.org>

# GPLv2
PERMIT_PACKAGE=	Yes

MASTER_SITES=	http://files.phpmyadmin.net/phpMyAdmin/${V}/

NO_BUILD=	Yes
NO_TEST=	Yes
PKG_ARCH=	*

PREFIX=		${VARBASE}/www
INSTDIR=	${PREFIX}/phpMyAdmin
SUBST_VARS=	INSTDIR V VARBASE

MODULES=	lang/php
RUN_DEPENDS=	lang/php/${MODPHP_VERSION},-mysqli \
		lang/php/${MODPHP_VERSION},-gd

post-extract:
	${SUBST_CMD} -m 0644 -c ${FILESDIR}/phpMyAdmin-apache2.conf \
	    ${WRKSRC}/examples/phpMyAdmin-apache2.conf
	${SUBST_CMD} -m 0644 -c ${FILESDIR}/phpMyAdmin-nginx.conf \
	    ${WRKSRC}/examples/phpMyAdmin-nginx.conf

do-install:
	@find ${WRKSRC} -type f -name "*.orig" -exec rm -f {} \;
	${INSTALL_DATA_DIR} ${INSTDIR}/
	cd ${WRKSRC}; pax -rw ./ ${INSTDIR}/

.include <bsd.port.mk>
