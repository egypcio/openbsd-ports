# $OpenBSD: Makefile,v 1.50 2019/10/16 19:56:33 jasper Exp $

COMMENT=		functional language for building scalable applications

V=			1.9.2
GH_ACCOUNT=		elixir-lang
GH_PROJECT=		elixir
GH_TAGNAME=		v$V
DISTNAME=		${GH_PROJECT}-$V
CATEGORIES=		lang

HOMEPAGE=		http://elixir-lang.org/

MAINTAINER=		Jasper Lievisse Adriaanse <jasper@openbsd.org>

# Apache2
PERMIT_PACKAGE=	Yes

MODULES=		lang/erlang
MODERL_VERSION=		21

ALL_TARGET=		# empty

TEST_TARGET=		test
PORTHOME=		${WRKDIR}

MAKE_FLAGS=		PREFIX="${PREFIX}" \
			MAN_PREFIX="${PREFIX}/man" \
			Q=""

pre-configure:
	${SUBST_CMD} ${WRKSRC}/bin/elixir

pre-install:
	-rm ${WRKSRC}/bin/*.{beforesubst,orig}

.include <bsd.port.mk>
