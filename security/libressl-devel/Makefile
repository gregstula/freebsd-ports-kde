# Created by: Bernard Spil <brnrd@FreeBSD.org>
# $FreeBSD$

PORTNAME=	libressl
PORTVERSION=	2.5.4
CATEGORIES=	security devel
MASTER_SITES=	OPENBSD/LibreSSL
PKGNAMESUFFIX=	-devel

MAINTAINER=	brnrd@FreeBSD.org
COMMENT=	Free version of the SSL/TLS protocol forked from OpenSSL

LICENSE=	BSD4CLAUSE
LICENSE_FILE=	${WRKSRC}/COPYING

CPE_VENDOR=	openbsd

OPTIONS_DEFINE=	MAN3 NC
OPTIONS_DEFAULT=	MAN3 NC
MAN3_DESC=	Install API manpages (section 3)
NC_DESC=	Install TLS-enabled netcat

CONFLICTS_INSTALL=	libressl-[0-9]* \
			openssl-[0-9]* \
			openssl-devel-[0-9]*

MAN3_EXTRA_PATCHES_OFF=	${FILESDIR}/extra-patch-MAN3
NC_CONFIGURE_ENABLE=	nc

GNU_CONFIGURE=	yes
USES=		cpe libtool pathfix pkgconfig
USE_LDCONFIG=	yes
OPTIONS_SUB=	yes
CFLAGS+=	-fpic -DPIC -Wl,-rpath,${PREFIX}/lib -Wl,--as-needed

INSTALL_TARGET=	install-strip
TEST_TARGET=	check

post-install:
	${RM} -r ${STAGEDIR}/${PREFIX}/etc/ssl/cert.pem

.include <bsd.port.mk>
