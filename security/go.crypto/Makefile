# $FreeBSD$

PORTNAME=	go.crypto
PORTVERSION=	20170330
CATEGORIES=	security devel

MAINTAINER=	jlaffaye@FreeBSD.org
COMMENT=	Additional cryptography packages for Go

LICENSE=	BSD3CLAUSE

USE_GITHUB=	yes
GH_ACCOUNT=	golang
GH_PROJECT=	crypto
GH_TAGNAME=	3cb07270c9455e8ad27956a70891c962d121a228
USES=		go
GO_PKGNAME=	golang.org/x/crypto
GO_TARGET=	${GO_PKGNAME}/bcrypt		\
		${GO_PKGNAME}/blake2b		\
		${GO_PKGNAME}/blake2s		\
		${GO_PKGNAME}/blowfish		\
		${GO_PKGNAME}/bn256		\
		${GO_PKGNAME}/cast5		\
		${GO_PKGNAME}/chacha20poly1305	\
		${GO_PKGNAME}/cryptobyte	\
		${GO_PKGNAME}/curve25519	\
		${GO_PKGNAME}/ed25519		\
		${GO_PKGNAME}/hkdf		\
		${GO_PKGNAME}/md4		\
		${GO_PKGNAME}/nacl/box		\
		${GO_PKGNAME}/nacl/secretbox	\
		${GO_PKGNAME}/ocsp		\
		${GO_PKGNAME}/openpgp		\
		${GO_PKGNAME}/openpgp/armor	\
		${GO_PKGNAME}/openpgp/clearsign	\
		${GO_PKGNAME}/openpgp/elgamal	\
		${GO_PKGNAME}/openpgp/errors	\
		${GO_PKGNAME}/openpgp/packet	\
		${GO_PKGNAME}/openpgp/s2k	\
		${GO_PKGNAME}/otr		\
		${GO_PKGNAME}/pbkdf2		\
		${GO_PKGNAME}/pkcs12		\
		${GO_PKGNAME}/poly1305		\
		${GO_PKGNAME}/ripemd160		\
		${GO_PKGNAME}/salsa20		\
		${GO_PKGNAME}/salsa20/salsa	\
		${GO_PKGNAME}/scrypt		\
		${GO_PKGNAME}/sha3		\
		${GO_PKGNAME}/ssh		\
		${GO_PKGNAME}/ssh/agent		\
		${GO_PKGNAME}/ssh/terminal	\
		${GO_PKGNAME}/ssh/test		\
		${GO_PKGNAME}/tea		\
		${GO_PKGNAME}/twofish		\
		${GO_PKGNAME}/xtea		\
		${GO_PKGNAME}/xts

.include <bsd.port.mk>
