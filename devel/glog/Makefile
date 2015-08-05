# Created by: Cheng-Lung Sung <clsung@FreeBSD.org>
# $FreeBSD: head/devel/glog/Makefile 382151 2015-03-24 18:24:27Z sunpoet $

PORTNAME=	glog
PORTVERSION=	0.3.4
CATEGORIES=	devel

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Library of C++ classes for flexible logging

LICENSE=	BSD3CLAUSE

LIB_DEPENDS=	libgflags.so:${PORTSDIR}/devel/gflags

OPTIONS_DEFINE=	DOCS

CPPFLAGS+=	-I${LOCALBASE}/include
GNU_CONFIGURE=	yes
INSTALL_TARGET=	install-strip
LDFLAGS+=	-L${LOCALBASE}/lib -lexecinfo
USE_LDCONFIG=	yes
USES=		execinfo libtool pathfix

PORTDOCS=	*

GH_ACCOUNT=	google
GH_PROJECT=	${PORTNAME}
GH_TAGNAME=	v${PORTVERSION}
USE_GITHUB=	yes

post-patch:
	@${REINPLACE_CMD} -e '/^docdir = / s| = .*| = ${DOCSDIR}|' ${WRKSRC}/Makefile.in

regression-test test: build
	cd ${WRKSRC}/ && ${SETENV} ${MAKE_ENV} ${MAKE_CMD} check

.include <bsd.port.mk>