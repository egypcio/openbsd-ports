# $OpenBSD: Makefile,v 1.12 2018/06/29 22:16:27 espie Exp $

COMMENT =	Mah Jongg four players board game for KDE
DISTNAME =	kajongg-${MODKDE4_VERSION}
HOMEPAGE =	http://www.kde.org/applications/games/kajongg/
PKG_ARCH =	*
REVISION =	5

MODULES =	lang/python

BUILD_DEPENDS =	${MODKDE4_DEP_DIR}/py-kde

WANTLIB += ${COMPILER_LIBCXX}

RUN_DEPENDS =	audio/vorbis-tools \
		devel/desktop-file-utils \
		devel/py-twisted \
		x11/gtk+3,-guic \
		${MODKDE4_DEP_DIR}/libkmahjongg>=${MODKDE4_VERSION} \
		${MODKDE4_DEP_DIR}/py-kde>=${MODKDE4_VERSION}

# Avoid extra BUILD_DEPENDS
CONFIGURE_ARGS =	-DINSTALL_KAJONGG:Bool=TRUE

MODPY_ADJ_FILES =	src/deferredutil.py \
			src/kajongg.py \
			src/kajonggtest.py \
			src/kajonggserver.py \
			src/scoringtest.py \
			src/server.py \
			setup.py

.include <bsd.port.mk>
