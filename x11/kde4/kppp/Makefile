# $OpenBSD: Makefile,v 1.8 2018/06/29 22:16:30 espie Exp $

COMMENT =	dialer and pppd front-end for KDE
DISTNAME =	kppp-${MODKDE4_VERSION}
REVISION =	5

CATEGORIES =	net
HOMEPAGE =	http://projects.kde.org/projects/kde/kdenetwork/kppp

WANTLIB =  c m pthread
WANTLIB += ${COMPILER_LIBCXX}
WANTLIB += lib/qt4/Qt3Support lib/qt4/QtDBus lib/qt4/QtGui
WANTLIB += lib/qt4/QtNetwork lib/qt4/QtSql lib/qt4/QtSvg lib/qt4/QtXml
WANTLIB += ${KDE4LIB}/kde3support ${KDE4LIB}/kdeui ${KDE4LIB}/kio

RUN_DEPENDS =	devel/desktop-file-utils \
		x11/gtk+3,-guic

CONFIGURE_ARGS =	-DHAVE_NET_IF_PPP_H:Bool=Yes

.include <bsd.port.mk>
