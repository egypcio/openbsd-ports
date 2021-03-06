# $OpenBSD: Makefile,v 1.86 2019/07/12 20:47:26 sthen Exp $

COMMENT=		RSS reader plugin for evolution

GNOME_PROJECT=		evolution-rss
GNOME_VERSION=		0.3.95
REVISION=		27

CATEGORIES=		mail

HOMEPAGE=		http://gnome.eu.org/evo/index.php/Evolution_RSS_Reader_Plugin

MAINTAINER=		Jasper Lievisse Adriaanse <jasper@openbsd.org>, \
			Antoine Jacoutot <ajacoutot@openbsd.org>

# GPLv2
PERMIT_PACKAGE=	Yes

WANTLIB += ${COMPILER_LIBCXX} EGL GL ICE SM X11 X11-xcb Xau Xcomposite
WANTLIB += Xcursor Xdamage Xdmcp Xext Xfixes Xi Xinerama Xrandr
WANTLIB += Xrender Xt Xxf86vm archive aspell atk-1.0 atk-bridge-2.0
WANTLIB += brotlicommon brotlidec bz2 c cairo cairo-gobject camel-1.2
WANTLIB += canberra canberra-gtk3 crypto curl db drm ebackend-1.2
WANTLIB += ebook-1.2 ebook-contacts-1.2 ecal-1.2 edata-book-1.2
WANTLIB += edataserver-1.2 edataserverui-1.2 enchant enchant-2
WANTLIB += epoxy expat ffi fontconfig freetype fribidi gailutil-3
WANTLIB += gbm gck-1 gcr-base-3 gcr-ui-3 gcrypt gdata gdk-3 gdk_pixbuf-2.0
WANTLIB += gio-2.0 glapi glib-2.0 gmodule-2.0 gnome-autoar-0 gnome-autoar-gtk-0
WANTLIB += gnome-desktop-3 goa-1.0 gobject-2.0 gpg-error graphite2
WANTLIB += gstapp-1.0 gstaudio-1.0 gstbase-1.0 gstfft-1.0 gstgl-1.0
WANTLIB += gstpbutils-1.0 gstreamer-1.0 gsttag-1.0 gstvideo-1.0
WANTLIB += gthread-2.0 gtk-3 gtkspell3-3 harfbuzz harfbuzz-icu
WANTLIB += hyphen ical icalss icalvcal iconv icudata icui18n icuuc
WANTLIB += idn2 intl javascriptcoregtk-4.0 jpeg json-glib-1.0
WANTLIB += lber-2.4 ldap-2.4 ltdl lz4 lzma m nghttp2 notify nspr4
WANTLIB += nss3 nssutil3 oauth ogg openjp2 orc-0.4 p11-kit pango-1.0
WANTLIB += pangocairo-1.0 pangoft2-1.0 pcre pixman-1 plc4 plds4
WANTLIB += png psl sasl2 secret-1 smime3 soup-2.4 soup-gnome-2.4
WANTLIB += sqlite3 ssl ssl3 tasn1 unistring vorbis vorbisfile
WANTLIB += webkit2gtk-4.0 webp webpdemux woff2common woff2dec
WANTLIB += xcb xcb-dri2 xcb-dri3 xcb-glx xcb-present xcb-render
WANTLIB += xcb-shm xcb-sync xcb-xfixes xml2 xshmfence xslt z zstd
WANTLIB += lib/evolution/eabutil
WANTLIB += lib/evolution/econtacteditor
WANTLIB += lib/evolution/econtactlisteditor
WANTLIB += lib/evolution/email-engine
WANTLIB += lib/evolution/essmime
WANTLIB += lib/evolution/evolution-mail-composer
WANTLIB += lib/evolution/evolution-mail-formatter
WANTLIB += lib/evolution/evolution-mail
WANTLIB += lib/evolution/evolution-shell
WANTLIB += lib/evolution/evolution-smime
WANTLIB += lib/evolution/evolution-util
WANTLIB += lib/evolution/gnomecanvas

COMPILER =		base-clang ports-gcc base-gcc

MASTER_SITES=		http://gnome.eu.org/

MODULES=		devel/dconf \
			x11/gnome

LIB_DEPENDS=		mail/evolution

MODGNOME_TOOLS=		desktop-file-utils

AUTOCONF_VERSION=	2.69

CONFIGURE_STYLE=	autoconf
CONFIGURE_ENV = ac_cv_path_GPP="${CXX}"

post-install:
	rm ${PREFIX}/lib/evolution/{plugins,modules}/*.{a,la}

.include <bsd.port.mk>
