# $OpenBSD: Makefile,v 1.3 2019/10/06 13:35:07 semarie Exp $

MODPY_EGG_VERSION =	5.2.2
TRYTON_MODULE =		timesheet

TRYTON_DEPENDS +=	company \
			company_work_time

RUN_DEPENDS +=		databases/py-sql${MODPY_FLAVOR}

.include <bsd.port.mk>
