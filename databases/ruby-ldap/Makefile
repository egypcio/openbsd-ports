# $OpenBSD: Makefile,v 1.37 2019/07/12 20:44:01 sthen Exp $

COMMENT=	Ruby interface to some common LDAP libraries

PKGNAME=	ldap-0.9.19
REVISION =	0
DISTNAME=	ruby-${PKGNAME}
CATEGORIES=	databases

HOMEPAGE=	https://github.com/alexey-chebotar/ruby-ldap

MAINTAINER=	Jeremy Evans <jeremy@openbsd.org>

# BSD
PERMIT_PACKAGE=	Yes

MODULES=		lang/ruby

WANTLIB=		crypto pthread ssl ldap_r lber

LIB_DEPENDS=		databases/openldap

CONFIGURE_STYLE=	ruby gem ext
CONFIGURE_ARGS=		--without-libldap

.include <bsd.port.mk>
