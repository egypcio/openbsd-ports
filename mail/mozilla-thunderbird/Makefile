# $OpenBSD: Makefile,v 1.299 2019/10/13 17:12:15 landry Exp $

ONLY_FOR_ARCHS =	amd64 i386
COMMENT-main =		Mozilla e-mail, rss and usenet client
COMMENT-lightning =	Mozilla Thunderbird calendar extension

# Don't forget to bump mail/thunderbird-i18n after updates.

MOZILLA_VERSION =	68.1.2
MOZILLA_BRANCH =	release
MOZILLA_PROJECT =	thunderbird
MOZILLA_CODENAME =	comm/mail
EXTRACT_SUFX =		.tar.xz

MULTI_PACKAGES =	-main -lightning
PKGNAME-main =		${PKGNAME}
PKGNAME-lightning =	lightning-${MOZILLA_VERSION}
EPOCH-lightning =	0

HOMEPAGE =	http://www.mozilla.org/thunderbird/

SO_VERSION =	34.0
# NOTE: Must bump minor version if any shlib's are removed from the
# components dir to avoid pkg_add -r issues.

MOZILLA_LIBS = ldap60 ldif60 lgpllibs mozgtk mozsqlite3 prldap60 xul

CATEGORIES=	mail news

# MPL
PERMIT_PACKAGE=	Yes

MODULES =	www/mozilla lang/python
MODPY_RUNDEP =	No

COMPILER =	base-clang ports-clang
MODCLANG_ARCHS =	amd64 i386

MOZILLA_USE_BUNDLED_LIBEVENT =	Yes
# firefox >= 46 defaults to gtk+3
MOZILLA_USE_GTK3 = Yes
# use bundled sqlite which has SQLITE_ENABLE_FTS3_TOKENIZER (#1252937)
MOZILLA_USE_BUNDLED_SQLITE =	Yes
# 56 requires 59.1
MOZILLA_USE_BUNDLED_ICU =	Yes
# 59 is broken with system cairo and the option is being dropped
MOZILLA_USE_BUNDLED_CAIRO = Yes
# #1460600
MOZILLA_USE_BUNDLED_HUNSPELL = Yes

# 53 needs rust
BUILD_DEPENDS +=	lang/rust
# stylo build needs LLVM
BUILD_DEPENDS +=	devel/llvm
# 61 requires both versions of python
BUILD_DEPENDS +=	lang/python/${MODPY_DEFAULT_VERSION_3}
# 63 requires node because why not #1483595
BUILD_DEPENDS +=	lang/node
# 63 requires cbindgen #1478813
BUILD_DEPENDS +=	devel/cbindgen
# 67 requires nasm for bundled libav1d
BUILD_DEPENDS +=	devel/nasm

WRKDIST =	${WRKDIR}/${MOZILLA_DIST}-${MOZILLA_DIST_VERSION:C/b[0-9]*//}

NO_TEST =	Yes

CONFIGURE_STYLE =	simple
CONFIGURE_ARGS +=	--prefix=${PREFIX}

# SQLITE_CFLAGS is set from pkgconfig, but it's not used for all files that need it, e.g.
# mailnews/build/nsMailModule.cpp pulls in mailnews/extensions/fts3/src/nsFts3Tokenizer.h
# and .../fts3/src/fts3_tokenizer.h which fails to find sqlite3.h.
CONFIGURE_ENV =		CPPFLAGS="-I${LOCALBASE}/include"

RUN_DEPENDS-lightning = STEM->=${MOZILLA_VERSION:S/b/beta/}:${BUILD_PKGPATH},-main
WANTLIB-lightning =
WANTLIB-main += ${WANTLIB} X11-xcb Xcursor Xi intl xcb xcb-shm

# build lightning xpi
CONFIGURE_ARGS +=	--enable-calendar

ALL_TARGET =	default

GNU_ARCH =	${MACHINE_ARCH:S/amd64/x86_64/}
# guid for gdata-provider comes from em:id in install.rdf
GUIDS =	gdata-provider {a62ef8ec-5fdc-40c2-873c-223b8a6925cc} #\
#	lightning {e2fda1a4-762b-4020-b5ad-a41df1933103}

EXTDIR =	${PREFIX}/lib/${MOZILLA_PROJECT}/distribution/extensions/

post-patch:
	sed -i 's/"files":{[^}]*}/"files":{}/' \
		${WRKSRC}/third_party/rust/cssparser/.cargo-checksum.json
	
post-install:
.for xpi guid in ${GUIDS}
	cp ${WRKBUILD}/dist/xpi-stage/${xpi}*.xpi ${EXTDIR}/${guid}.xpi
.endfor

	# install prefs
	${SUBST_DATA} ${FILESDIR}/all-openbsd.js \
		${PREFIX}/lib/${MOZILLA_PROJECT}/defaults/pref/all-openbsd.js
	# install distribution.ini file
	${INSTALL_DATA_DIR} ${PREFIX}/lib/${MOZILLA_PROJECT}/distribution
	echo "[Global]\nid=OpenBSD\nversion=${OSREV}\nabout=Packaged by ${MAINTAINER}\n" > \
		${PREFIX}/lib/${MOZILLA_PROJECT}/distribution/distribution.ini
	# install desktop file
	${INSTALL_DATA_DIR} ${PREFIX}/share/applications/ ; \
	${SUBST_DATA} ${FILESDIR}/${MOZILLA_PROJECT}.desktop \
		${PREFIX}/share/applications/${MOZILLA_PROJECT}.desktop ; \
	# install icon for desktop file
	${INSTALL_DATA_DIR} ${PREFIX}/share/pixmaps/
	${INSTALL_DATA} ${PREFIX}/lib/${MOZILLA_PROJECT}/chrome/icons/default/default128.png \
		${PREFIX}/share/pixmaps/${MOZILLA_PROJECT}.png

.include <bsd.port.mk>
