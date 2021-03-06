# $OpenBSD: Makefile,v 1.46 2019/09/26 21:59:30 sthen Exp $

# undefined ref's to libicon*, libintl*
USE_LLD=	Yes

COMMENT-main=	MS Exchange groupware suite replacement
COMMENT-mapi=	kopano MAPI extensions for PHP

PKGNAME-main=	kopano-core-${V}.${BUILD}
PKGNAME-mapi=	kopano-mapi-${V}.${BUILD}

REVISION-main=	1
REVISION-mapi=	1

CATEGORIES=	mail www productivity

EXTRACT_SUFX =	.tar.xz

SHARED_LIBS +=  mapi			  3.0 # 0.0
SHARED_LIBS +=  kcarchiver                0.0 # 0.0
SHARED_LIBS +=  kcarchivercore            0.0 # 0.0
SHARED_LIBS +=  kcfreebusy                0.0 # 0.0
SHARED_LIBS +=  kcicalmapi                0.0 # 0.0
SHARED_LIBS +=  kcindex                   0.0 # 0.0
SHARED_LIBS +=  kcinetmapi                0.0 # 0.0
SHARED_LIBS +=  kcpyplug                  0.0 # 0.0
SHARED_LIBS +=  kcrosie                   0.0 # 0.0
SHARED_LIBS +=  kcserver                  0.0 # 0.0
SHARED_LIBS +=  kcsoap                    0.0 # 0.0
SHARED_LIBS +=  kcutil                    0.0 # 0.0

MULTI_PACKAGES=	-main -mapi

# C++11
COMPILER=	base-clang ports-gcc base-gcc

MODULES=	lang/python \
		lang/php

MODPY_VERSION=	${MODPY_DEFAULT_VERSION_3}
MODPHP_DO_SAMPLE=mapi
MESSAGE-main=	# empty
UNMESSAGE-main=	# empty

BUILD_DEPENDS=	devel/gettext,-tools \
		devel/py-setuptools${MODPY_FLAVOR} \
		devel/swig \
		shells/bash \
		sysutils/coreutils \
		textproc/xmlto

WANTLIB += m pthread z vmime iconv icudata icui18n icuuc intl
WANTLIB += lzma crypto ssl kvm

WANTLIB-main += c ${WANTLIB} ${MODPY_WANTLIB}
WANTLIB-main += curl nghttp2 ical icalss
WANTLIB-main += mariadb curses ssl xml2
WANTLIB-main += gsoapssl++ tidy
WANTLIB-main += ${LIBCXX}
WANTLIB-main += icalvcal ldap_r HX jsoncpp
WANTLIB-main += db_cxx uuid xapian
WANTLIB-main += X11 Xext Xrender expat fontconfig freetype pixman-1
WANTLIB-main += xcb xcb-render xcb-shm
WANTLIB-main += cairo fribidi glib-2.0 gobject-2.0 graphite2
WANTLIB-main += gthread-2.0 harfbuzz pango-1.0 pangocairo-1.0
WANTLIB-main += pangoft2-1.0 png rrd

# Do not substitute MODULE_NAME
UPDATE_PLIST_ARGS+=	-i MODULE_NAME

RUN_DEPENDS-main= ${MODPY_RUN_DEPENDS} \
		databases/xapian-bindings,-python \
		devel/libmagic \
		devel/py-dateutil${MODPY_FLAVOR} \
		mail/p5-Mail-SpamAssassin \
		textproc/catdoc \
		www/py-jwt${MODPY_FLAVOR}
LIB_DEPENDS-main= databases/mariadb \
		databases/openldap \
		databases/xapian-core \
		devel/gettext,-runtime \
		devel/gsoap>=2.8.50 \
		devel/jsoncpp \
		devel/libHX \
		devel/libvmime>=0.9.4 \
		net/curl \
		net/rrdtool,-main \
		textproc/icu4c \
		textproc/libical \
		textproc/libxml \
		www/tidy

WANTLIB-mapi += ${WANTLIB}
WANTLIB-mapi += ical icalss mapi
WANTLIB-mapi += xml2
WANTLIB-mapi += ${LIBCXX}
WANTLIB-mapi += icalvcal kcfreebusy kcicalmapi kcinetmapi
WANTLIB-mapi += kcutil kcrosie tidy
WANTLIB-mapi += HX curl jsoncpp nghttp2

LIB_DEPENDS-mapi= ${BASE_PKGPATH}>=${V}
RUN_DEPENDS-mapi= ${MODPHP_RUN_DEPENDS}

USE_GMAKE=	Yes

USE_LIBTOOL=	gnu

MODPY_ADJ_FILES=tools/python-scripts/optimize-imap.py \
		tools/python-scripts/update-resource-recipients \
		ECtools/utils/kopano-mailbox-permissions \
		ECtools/utils/kopano-set-oof

CONFIGURE_STYLE=	autoconf
AUTOCONF_VERSION=	2.69

CONFIGURE_ENV=	CPPFLAGS="-fpermissive -I${LOCALBASE}/include" \
		PHP_SYSCONF_DIR="${SYSCONFDIR}/php-${MODPHP_VERSION}" \
		ac_cv_lib_pam_pam_start=no
CONFIGURE_ARGS=	--disable-static \
		--with-mapi-configdir=${SYSCONFDIR}/mapi \
		--with-userscript-prefix=${SYSCONFDIR}/kopano/userscripts \
		--with-quotatemplate-prefix=${SYSCONFDIR}/kopano/quotamail \
		--with-searchscripts-prefix=${SYSCONFDIR}/kopano/searchscripts \
		--enable-release \
		--enable-unicode \
		--enable-python \
		--with-distro=openbsd \
		--with-ical-prefix=${LOCALBASE}/include \
		--with-php-config=${MODPHP_PHP_CONFIG}

# force build with clucene >= 2.x
CONFIGURE_ENV +=ac_cv_lib_clucene__ZN6lucene5index11IndexReader4openEPKc=yes
MAKE_FLAGS +=	CLUCENE_CFLAGS="$$(pkg-config --cflags libclucene-core)" \
		CLUCENE_LIBS="$$(pkg-config --libs libclucene-core)"

FAKE_FLAGS=	sysconfdir=${PREFIX}/share/examples \
		phpsysconfdir=${PREFIX}/share/examples/php-${MODPHP_VERSION} \
		USERSCRIPTDIR=${PREFIX}/share/examples/kopano/userscripts \
		QUOTATEMPLATEDIR=${PREFIX}/share/examples/kopano/quotamail \
		SEARCHSCRIPTSDIR=${PREFIX}/share/examples/kopano/searchscripts \
		MAPICONFIGDIR=${PREFIX}/share/examples/kopano/mapi

SUB_SCRIPTS=	createcompany.d/00createpublic groups_common.sh \
		createuser.d/00createstore companies_common.sh \
		users_common.sh

post-patch:
	ln -sf ${MODPY_BIN} ${WRKDIR}/bin/python
	ln -sf ${LOCALBASE}/bin/gcp ${WRKDIR}/bin/cp
	ln -sf ${LOCALBASE}/bin/gmv ${WRKDIR}/bin/mv

pre-configure:
	cd ${WRKSRC}/installer/linux && \
		for i in *.cfg ldap.m4 createuser.dotforward ; do \
			${SUBST_CMD} $$i; \
			perl -pi -e 's/\r\n/\n/;' $$i; done
#	for i in ${SUB_SCRIPTS}; do \
#		${SUBST_CMD} ${WRKSRC}/installer/userscripts/$$i; done
	${SUBST_CMD} ${WRKSRC}/spooler/{DAgent,Spooler}.cpp \
		${WRKSRC}/tools/python-scripts/kopano-cachestat
	perl -pi -e 's,/bin/bash,/bin/sh,g' \
		${WRKSRC}/installer/searchscripts/{attachments_parser,zmktemp}

post-install:
	${INSTALL_DATA_DIR} ${WRKINST}${INSTDIR}
	${INSTALL_DATA_DIR} ${PREFIX}/share/examples/php-${MODPHP_VERSION}

	${SUBST_CMD} -m 0644 -c ${FILESDIR}/kopano.m4 ${PREFIX}/share/examples/kopano/kopano.m4
	${SUBST_CMD} -m 0644 -c ${FILESDIR}/local_kopano.m4 ${PREFIX}/share/examples/kopano/local_kopano.m4

	# move files where we want them to be
	mv ${PREFIX}/share/doc/kopano-gateway/* \
		${PREFIX}/share/doc/kopano
	mv ${PREFIX}/share/doc/kopano/example-config/* \
		${PREFIX}/share/examples/kopano
	mv ${PREFIX}/share/doc/kopano/kopano.schema \
		${PREFIX}/share/examples/kopano
	perl -pi -e 's,/usr/bin/env python,${MODPY_BIN},g' \
		${PREFIX}/sbin/kopano-search \
		${PREFIX}/sbin/kopano-search-xapian-compact.py \
		${PREFIX}/lib/python${MODPY_VERSION}/site-packages/kopano_search/__init__.py \
		${PREFIX}/lib/python${MODPY_VERSION}/site-packages/kopano_search/plaintext.py \
		${PREFIX}/lib/python${MODPY_VERSION}/site-packages/kopano/daemon/version/version_info.py

	find ${PREFIX} -name "*.la" -exec rm {} \;

	${MODPY_BIN} ${MODPY_LIBDIR}/compileall.py \
		${PREFIX}/share/kopano-dagent/python \
		${PREFIX}/share/kopano-spooler/python \
		${PREFIX}/lib/python${MODPY_VERSION}/site-packages

	chown -R ${SHAREOWN}:${SHAREGRP} ${WRKINST}${INSTDIR}
	chown -R ${SHAREOWN}:${SHAREGRP} ${PREFIX}/share/doc/kopano
	chown ${BINOWN}:${BINGRP} ${PREFIX}/share/examples/kopano/kopano.m4 \
		${PREFIX}/share/examples/kopano/local_kopano.m4
	chmod ${SHAREMODE} ${PREFIX}/share/examples/kopano/kopano.m4 \
		${PREFIX}/share/examples/kopano/local_kopano.m4

.include <bsd.port.mk>
