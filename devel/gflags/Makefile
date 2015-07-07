# Created by: Yen-Ming Lee <leeym@FreeBSD.org>
# $FreeBSD: head/devel/gflags/Makefile 382151 2015-03-24 18:24:27Z sunpoet $

PORTNAME=	gflags
PORTVERSION=	2.1.2
CATEGORIES=	devel

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Commandline flags module for C++

LICENSE=	BSD3CLAUSE

CMAKE_ARGS=	-DBUILD_SHARED_LIBS=ON -DBUILD_TESTING=ON
USE_LDCONFIG=	yes
USES=		cmake shebangfix

GH_ACCOUNT=	schuhschuh
GH_PROJECT=	${PORTNAME}
GH_TAGNAME=	v${PORTVERSION}
USE_GITHUB=	yes

SHEBANG_FILES=	src/gflags_completions.sh

regression-test test: build
	cd ${WRKSRC}/ && ${SETENV} ${MAKE_ENV} ${MAKE_CMD} test

.include <bsd.port.mk>
