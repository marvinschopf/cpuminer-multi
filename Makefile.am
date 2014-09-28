
if WANT_JANSSON
JANSSON_INCLUDES= -I$(top_srcdir)/compat/jansson
else
JANSSON_INCLUDES=
endif

AUTOMAKE_OPTIONS= subdir-objects
ACLOCAL_AMFLAGS = -I .

EXTRA_DIST	= example-cfg.json nomacro.pl

SUBDIRS		= compat

AM_CPPFLAGS	= $(PTHREAD_FLAGS) $(JANSSON_INCLUDES)
AM_CFLAGS	= 

bin_PROGRAMS	= minerd

dist_man_MANS	= minerd.1

minerd_SOURCES	= elist.h \
		  miner.h \
		  compat.h \
		  cpu-miner.c \
		  util.c \
		  cryptonight_common.c \
		  crypto/c_keccak.c \
		  crypto/c_groestl.c \
		  crypto/c_blake256.c \
		  crypto/c_jh.c \
		  crypto/c_skein.c 

# These CFLAGS stop the lobotomized implementation from breaking
if USE_LOBOTOMIZED_AES
minerd_SOURCES += cryptonight_lobotomized.c crypto/oaes_lib.c
AM_CFLAGS += -O2 -fno-strict-aliasing
else
AM_CFLAGS +=  
minerd_SOURCES += cryptonight_aesni.c
endif

minerd_LDFLAGS	= $(AM_LDFLAGS)
minerd_LDADD	= @LIBCURL@ @JANSSON_LIBS@ @PTHREAD_LIBS@ @WS2_LIBS@
minerd_CPPFLAGS = $(AM_CPPFLAGS) @LIBCURL_CPPFLAGS@
minerd_CFLAGS   = $(AM_CFLAGS)

if HAVE_WINDOWS
minerd_CFLAGS += -Wl,--stack,10485760
endif
