PORTNAME=	protobuf
PORTVERSION=	3.0.0b3
DISTVERSIONPREFIX=	v
CATEGORIES=	devel

MAINTAINER=	hd@oc.dk
COMMENT=	Data interchange format library

LICENSE=	BSD3CLAUSE

CFLAGS+=	-DGOOGLE_PROTOBUF_NO_RTTI
GNU_CONFIGURE=	yes
INSTALL_TARGET=	install-strip
ONLY_FOR_ARCHS=	amd64 armv6 i386
PATHFIX_MAKEFILEIN=	Makefile.am
TEST_TARGET=	check
USE_LDCONFIG=	yes
USES=		autoreconf gmake libtool pathfix pkgconfig

GH_ACCOUNT=	google
GH_TAGNAME=	v3.0.0-beta-3
USE_GITHUB=	yes

.include <bsd.port.mk>
