# Created by: Daniel Gerzo <danger@FreeBSD.org>
# $FreeBSD: head/www/uwsgi/Makefile 381481 2015-03-17 11:00:14Z demon $

PORTNAME=	uwsgi
PORTVERSION=	2.0.10
CATEGORIES=	www python
MASTER_SITES=	http://projects.unbit.it/downloads/

MAINTAINER=	demon@FreeBSD.org
COMMENT=	Developer-friendly WSGI server which uses uwsgi protocol

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		python:2.7
USE_RC_SUBR=	uwsgi

# Also depend on Python 3.4
BUILD_DEPENDS+= python3.4:${PORTSDIR}/lang/python34

# Don't build Python 2.7 into binary
MAKE_ENV= PROFILE="nolang"

LDFLAGS+=	"-L${LOCALBASE}/lib"

PLIST_FILES=	bin/uwsgi \
		%%PYTHON_SITELIBDIR%%/uwsgidecorators.py \
		share/uwsgi/python34_plugin.so \
		share/uwsgi/python27_plugin.so 

post-patch:
	${REINPLACE_CMD} -e 's|python|${PYTHON_CMD}|' ${WRKSRC}/Makefile

pre-install:
	cd ${WRKSRC} && PYTHON=python2.7 ./uwsgi --build-plugin "plugins/python python27"
	cd ${WRKSRC} && PYTHON=python3.4 ./uwsgi --build-plugin "plugins/python python34"

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/${PORTNAME} ${STAGEDIR}${PREFIX}/bin/
	${MKDIR} ${STAGEDIR}${PYTHONPREFIX_SITELIBDIR}
	${INSTALL_DATA} ${WRKSRC}/uwsgidecorators.py ${STAGEDIR}${PYTHONPREFIX_SITELIBDIR}
	${MKDIR} -p ${STAGEDIR}${PREFIX}/share/uwsgi
	${INSTALL_PROGRAM} ${WRKSRC}/python34_plugin.so ${STAGEDIR}${PREFIX}/share/uwsgi/
	${INSTALL_PROGRAM} ${WRKSRC}/python27_plugin.so ${STAGEDIR}${PREFIX}/share/uwsgi/


.include <bsd.port.mk>
