# $OpenBSD: Makefile,v 1.2 2018/12/17 19:48:23 landry Exp $

COMMENT =	modern GPS tracking platform
V =		4.2
REVISION =	0
PKGNAME =	traccar-${V}
DISTNAME =	traccar-other-${V}
EXTRACT_SUFX =	.zip
WRKDIST =	${WRKDIR}

CATEGORIES =	geo
HOMEPAGE =	https://www.traccar.org/

MAINTAINER =	Renaud Allard <renaud@allard.it>

# MPL 2.0
PERMIT_PACKAGE_CDROM =	Yes

MASTER_SITES = https://github.com/traccar/traccar/releases/download/v${V}/

MODULES =               java
MODJAVA_VER =           1.8
MODJAVA_JRERUN =        yes

RUN_DEPENDS=		java/javaPathHelper

NO_BUILD =              Yes
NO_TEST =               Yes

do-configure:
	${SUBST_CMD} ${WRKSRC}/conf/{default,traccar}.xml

do-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/traccar/
	cd ${WRKSRC}; cp -r conf lib schema templates web tracker-server.jar \
	    ${PREFIX}/share/traccar/
	rm ${PREFIX}/share/traccar/conf/{default,traccar}.xml.*

.include <bsd.port.mk>