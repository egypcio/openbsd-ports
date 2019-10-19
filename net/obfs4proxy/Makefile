# $OpenBSD: Makefile,v 1.5 2019/07/12 20:48:34 sthen Exp $

COMMENT =		a look-like nothing obfuscation protocol for TCP

DISTNAME =		obfs4proxy-0.0.11

REVISION =		0

MASTER_SITES =	https://people.torproject.org/~yawning/releases/obfs4proxy/
MASTER_SITES0 =	https://gitlab.com/yawning/utls/-/archive/v0.0.11-1/
MASTER_SITES1 = https://gitlab.com/yawning/bsaes/-/archive/${ALL_TARGET_BSAES_TAG}/
MASTER_SITES2 = https://github.com/dsnet/compress/archive/
	
DISTFILES =	obfs4proxy-0.0.11.tar.xz \
		utls-v0.0.11-1.tar.gz:0 \
		bsaes-${ALL_TARGET_BSAES_TAG}.tar.gz:1 \
		${ALL_TARGET_COMPRESS_T}.tar.gz:2		# dsnet/compress

CATEGORIES =		net www

HOMEPAGE =	https://gitlab.com/yawning/obfs4/blob/master/README.md

MAINTAINER =		Sean Levy <attila@stalphonsos.com>

# BSD
PERMIT_PACKAGE =	Yes

WANTLIB +=		c pthread

MODULES +=		lang/go

ALL_TARGET =		gitlab.com/yawning/obfs4.git
ALL_TARGET_BSAES =	git.schwanenlied.me/yawning/bsaes.git
ALL_TARGET_BSAES_TAG =	0a714cd429ec754482b4001e918db30cd2094405
ALL_TARGET_COMPRESS =	github.com/dsnet/compress
ALL_TARGET_COMPRESS_T =	da652975a8eea9fa0735aba8056747a751db0bd3

BUILD_DEPENDS +=	devel/go-goptlib \
			devel/go-sys \
			net/go-net \
			security/go-crypto \
			security/go-ed25519 \
			security/go-siphash \
			textproc/go-text

MODGO_SUBDIR =		${WRKDIR}
MODGO_WORKSPACE =	${WRKDIR}
MODGO_GOPATH =		${WRKDIR}:${MODGO_PACKAGE_PATH}

MODGO_SETUP_WORKSPACE = mkdir -p ${WRKSRC:H} ; \
	mkdir -p ${WRKDIR}/src/${ALL_TARGET_BSAES:H} ; \
	mkdir -p ${WRKDIR}/src/${ALL_TARGET_COMPRESS:H} ; \
	ln -sf ${WRKDIR}/bsaes-${ALL_TARGET_BSAES_TAG} ${WRKDIR}/src/${ALL_TARGET_BSAES} ; \
	ln -sf ${WRKDIR}/bsaes-${ALL_TARGET_BSAES_TAG} ${WRKSRC:H}/bsaes.git ; \
	ln -sf ${WRKDIR}/compress-${ALL_TARGET_COMPRESS_T} ${WRKDIR}/src/${ALL_TARGET_COMPRESS} ; \
	ln -sf ${WRKDIR}/utls-v0.0.11-1 ${WRKSRC:H}/utls.git ; \
	ln -sf ${WRKDIR} ${WRKSRC} 

do-build:
	cd ${WRKSRC} ; \
		${MODGO_CMD} build ${MODGO_FLAGS} \
		-o ${WRKDIR}/bin/obfs4proxy ./obfs4proxy

.include <bsd.port.mk>
