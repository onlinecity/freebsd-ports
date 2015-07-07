# $FreeBSD$

PORTNAME=     norm
PORTVERSION=  1.5r5
CATEGORIES=   net
MASTER_SITES= http://downloads.pf.itd.nrl.navy.mil/norm/archive/
DISTNAME=     src-norm-${DISTVERSION}

MAINTAINER=   hd@oc.dk
COMMENT=      NACK-Oriented Reliable Multicast (NORM)

WRKSRC=       ${WRKDIR}/norm-${DISTVERSION}

USES=         waf tar:tgz libtool
USE_LDCONFIG= yes

post-install:
	${INSTALL_DATA} ${WRKSRC}/include/normApi.h ${STAGEDIR}${PREFIX}/include/

.include <bsd.port.mk>
