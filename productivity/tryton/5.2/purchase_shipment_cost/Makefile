# $OpenBSD: Makefile,v 1.1.1.1 2019/05/09 11:48:59 semarie Exp $

MODPY_EGG_VERSION =	5.2.0
TRYTON_MODULE =		purchase_shipment_cost

TRYTON_DEPENDS +=	carrier \
			currency \
			stock

TEST_DEPENDS +=		devel/py-mock${MODPY_FLAVOR}

TRYTON_TEST_DEPENDS +=	account_stock_continental \
			account_stock_anglo_saxon \
			purchase

.include <bsd.port.mk>
