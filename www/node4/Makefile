# Created by: Jin-Sih Lin <linpct@gmail.com>
# $FreeBSD$

PORTNAME=	node
PORTVERSION=	4.8.3
DISTVERSIONPREFIX=	v
CATEGORIES=	www
MASTER_SITES=	http://nodejs.org/dist/v${PORTVERSION}/
PKGNAMESUFFIX=	4

MAINTAINER=	bradleythughes@fastmail.fm
COMMENT=	V8 JavaScript for client and server (4.x LTS)

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

OPTIONS_DEFINE=	BUNDLED_SSL DOCS NLS
OPTIONS_DEFAULT=
OPTIONS_SUB=	yes

OPTIONS_DEFAULT_FreeBSD_10=	BUNDLED_SSL
OPTIONS_DEFAULT+=		${OPTIONS_DEFAULT_${OPSYS}_${OSREL:R}}

BUNDLED_SSL_DESC=		Use node.js's bundled OpenSSL implementation #'
BUNDLED_SSL_USES_OFF=		ssl
BUNDLED_SSL_CONFIGURE_OFF=	--shared-openssl

NLS_CONFIGURE_ON=	--with-intl=system-icu
NLS_LIB_DEPENDS=	libicui18n.so:devel/icu

USES=		compiler:c++11-lib execinfo gmake python:2 pkgconfig localbase
HAS_CONFIGURE=	yes
USE_LDCONFIG=	yes

CONFLICTS_INSTALL=	node[56]-[0-9]* node01[02]-[0-9]* node-[0-9]* node-devel-[0-9]* iojs-[0-9]*

ONLY_FOR_ARCHS=	i386 amd64
CONFIGURE_ARGS=	--prefix=${PREFIX_RELDEST} \
	 	--without-npm \
		--shared-libuv \
		--shared-zlib
PREFIX_RELDEST=	${PREFIX:S,^${DESTDIR},,}
REINPLACE_ARGS=	-i ''
MAKE_ENV+=	CC.host=${CC} CXX.host=${CXX} LINK.host=${CXX} LINK.target=${CXX}

LIB_DEPENDS+=	libuv.so:devel/libuv

.include <bsd.port.options.mk>

.if empty(PORT_OPTIONS:MBUNDLED_SSL)

.if ${OPSYS} == FreeBSD && ${OSVERSION} < 1100085 && ${SSL_DEFAULT} == base
IGNORE=		node.js requires openssl 1.0.2, add DEFAULT_VERSIONS+=ssl=openssl to /etc/make.conf or enable BUNDLED_SSL option
.endif

.if !empty(SSL_DEFAULT:Mlibressl*)
IGNORE=		cannot build node.js with LibreSSL. You must enable BUNDLED_SSL
.endif

.endif

post-patch:
	@${REINPLACE_CMD} -e 's|/usr/local|${LOCALBASE}|' \
		${WRKSRC}/deps/v8/tools/gyp/v8.gyp
	@${REINPLACE_CMD} -e 's|/usr/bin/env python|${PYTHON_CMD}|' \
		${WRKSRC}/configure
	@${REINPLACE_CMD} -e "s|python -c|${PYTHON_CMD} -c|" \
		${WRKSRC}/deps/v8/build/toolchain.gypi
	@${REINPLACE_CMD} -e "s|'python',|'${PYTHON_CMD}',|" \
		${WRKSRC}/common.gypi \
		${WRKSRC}/deps/v8/build/shim_headers.gypi \
		${WRKSRC}/deps/v8/build/standalone.gypi \
		${WRKSRC}/deps/v8/src/d8.gyp \
		${WRKSRC}/deps/v8/tools/gyp/v8.gyp \
		${WRKSRC}/node.gyp \
		${WRKSRC}/tools/icu/icu-generic.gyp

post-configure:
	# Post-process Makefile and *.mk files created by node-gyp and remove
	# all occurrences of -I${LOCALBASE}/include. C*FLAGS include this
	# before all -I../deps/* for bundled code. This can cause build
	# breakages if the dependency is installed in ${LOCALBASE}. The
	# USES+=localbase above will ensure that we pick up includes for real
	# external dependencies.
	${FIND} ${WRKSRC}/out -type f -print0 \
		| ${XARGS} -0 ${REINPLACE_CMD} -e "s|-I${LOCALBASE}/include||g"

post-install:
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/node

.include <bsd.port.mk>
