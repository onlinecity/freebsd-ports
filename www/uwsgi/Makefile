# Created by: Daniel Gerzo <danger@FreeBSD.org>
# $FreeBSD: head/www/uwsgi/Makefile 391052 2015-07-01 12:12:08Z demon $

PORTNAME=	uwsgi
PORTVERSION=	2.0.14
CATEGORIES=	www python
MASTER_SITES=	http://projects.unbit.it/downloads/

MAINTAINER=	demon@FreeBSD.org
COMMENT=	Developer-friendly WSGI server which uses uwsgi protocol

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		python:3.5
#USE_PYTHON=     concurrent distutils
USE_RC_SUBR=	uwsgi

OPTIONS_DEFINE= DEBUG JSON PCRE XML

DEBUG_VARS=     PYDISTUTILS_BUILDARGS+=--debug

# Also depend on Python 3.5
#BUILD_DEPENDS+= python3.5:${PORTSDIR}/lang/python35
BUILD_DEPENDS+= python2.7:${PORTSDIR}/lang/python27
JSON_LIB_DEPENDS=	libjansson.so:devel/jansson
PCRE_LIB_DEPENDS=	libpcre.so:devel/pcre
XML_LIB_DEPENDS=	libxml2.so:textproc/libxml2

# Also depend on PyPy
#BUILD_DEPENDS+= pypy:${PORTSDIR}/lang/pypy

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MJSON}
O_JSON=		jansson
.else
O_JSON=		false
.endif

.if ${PORT_OPTIONS:MPCRE}
O_PCRE=		true
.else
O_PCRE=		false
.endif

.if ${PORT_OPTIONS:MXML}
O_XML=		libxml2
.else
O_XML=		false
.endif

# Don't build Python 2.7 into binary
MAKE_ENV= PROFILE="nolang"

LDFLAGS+=	"-L${LOCALBASE}/lib"
MAKE_ENV+=      CPUCOUNT=${MAKE_JOBS_NUMBER}
MAKE_ARGS+=     UWSGI_EMBED_PLUGINS=cgi

#PYSETUP=                        uwsgiconfig.py
#PYDISTUTILS_BUILD_TARGET=       --build
#PYDISTUTILS_BUILDARGS=          --verbose

PLIST_FILES=	bin/uwsgi \
		%%PYTHON_SITELIBDIR%%/uwsgidecorators.py \
		share/uwsgi/python35_plugin.so \
		share/uwsgi/python27_plugin.so
#		share/uwsgi/python27_plugin.so \
#		share/uwsgi/pypy_plugin.so

post-patch:
#	${REINPLACE_CMD} -e 's|python|${PYTHON_CMD}|' ${WRKSRC}/Makefile
	${REINPLACE_CMD} -e 's|python|python2.7|' ${WRKSRC}/Makefile
	${REINPLACE_CMD} -e s#@JSON@#${O_JSON}# -e s#@XML@#${O_XML}# -e s#@PCRE@#${O_PCRE}# ${WRKSRC}/buildconf/base.ini

pre-install:
	cd ${WRKSRC} && PYTHON=python2.7 ./uwsgi --build-plugin "plugins/python python27"
	cd ${WRKSRC} && PYTHON=python3.5 ./uwsgi --build-plugin "plugins/python python35"
#	cd ${WRKSRC} && PYTHON=python2.7 ./uwsgi --build-plugin "plugins/pypy"

do-configure:
	@${DO_NADA}

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/${PORTNAME} ${STAGEDIR}${PREFIX}/bin/
	${MKDIR} ${STAGEDIR}${PYTHONPREFIX_SITELIBDIR}
	${INSTALL_DATA} ${WRKSRC}/uwsgidecorators.py ${STAGEDIR}${PYTHONPREFIX_SITELIBDIR}
	${MKDIR} -p ${STAGEDIR}${PREFIX}/share/uwsgi
	${INSTALL_PROGRAM} ${WRKSRC}/python35_plugin.so ${STAGEDIR}${PREFIX}/share/uwsgi/
	${INSTALL_PROGRAM} ${WRKSRC}/python27_plugin.so ${STAGEDIR}${PREFIX}/share/uwsgi/
#	${INSTALL_PROGRAM} ${WRKSRC}/pypy_plugin.so ${STAGEDIR}${PREFIX}/share/uwsgi/

.include <bsd.port.mk>
