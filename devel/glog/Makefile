# Created by: Cheng-Lung Sung <clsung@FreeBSD.org>
# $FreeBSD: head/devel/glog/Makefile 412346 2016-04-01 14:00:51Z mat $

PORTNAME=	glog
PORTVERSION=	0.3.4
PORTREVISION= 1
DISTVERSIONPREFIX=	v
CATEGORIES=	devel

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Library of C++ classes for flexible logging

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/COPYING

LIB_DEPENDS=	libgflags.so:devel/gflags

OPTIONS_DEFINE=	DOCS

GNU_CONFIGURE=	yes
INSTALL_TARGET=	install-strip
LDFLAGS+=	-lexecinfo
TEST_TARGET=	check
USE_LDCONFIG=	yes
USES=		execinfo libtool localbase pathfix

PORTDOCS=	*

GH_ACCOUNT=	google
USE_GITHUB=	yes

post-patch:
	@${REINPLACE_CMD} -e '/^docdir = / s| = .*| = ${DOCSDIR}|' ${WRKSRC}/Makefile.in

.include <bsd.port.mk>
