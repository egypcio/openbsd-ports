# $OpenBSD: Makefile,v 1.1.1.1 2019/05/09 11:48:53 semarie Exp $

MODPY_EGG_VERSION =	5.2.0
TRYTON_MODULE =		account_invoice_stock

TRYTON_DEPENDS +=	account_invoice \
			stock \
			product

RUN_DEPENDS +=		devel/py-dateutil${MODPY_FLAVOR} \
			databases/py-sql${MODPY_FLAVOR} \
			devel/py-simpleeval${MODPY_FLAVOR}

.include <bsd.port.mk>
