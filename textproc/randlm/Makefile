# Created by: Dmitry Sivachenko <demon@FreeBSD.org>
# $FreeBSD$

PORTNAME=	randlm
PORTVERSION=	0.2.5
PORTREVISION=	5
CATEGORIES=	textproc
MASTER_SITES=	SF/${PORTNAME}

MAINTAINER=	demon@FreeBSD.org
COMMENT=	A toolkit for building randomized language models

BUILD_DEPENDS=	${LOCALBASE}/include/google/sparse_hash_map:devel/sparsehash
LIB_DEPENDS=	libboost_thread.so:devel/boost-libs
RUN_DEPENDS=	${LOCALBASE}/include/google/sparse_hash_map:devel/sparsehash

GNU_CONFIGURE=	yes
USE_PERL5=	run
USE_LDCONFIG=	yes
USES=		autoreconf libtool compiler:c++11-lang
GNU_CONFIGURE=	yes
MAKE_JOBS_UNSAFE=yes
CXXFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib
INSTALL_TARGET=	install-strip

BROKEN_aarch64=		fails to compile: invalid output constraint =a in asm
BROKEN_armv6=		fails to compile: invalid output constraint =a in asm
BROKEN_powerpc64=	fails to compile: error: 'itr' does not name a type

post-patch:
	cd ${WRKSRC}/hadoop && ${MV} strings.cpp strings.cc && ${MV} strings.h s.h
	${REINPLACE_CMD} -e s#strings.h#s.h# ${WRKSRC}/hadoop/r_compute_ngram_counts.cpp ${WRKSRC}/hadoop/m_compute_ngram_counts_batch.cpp

.include <bsd.port.mk>
