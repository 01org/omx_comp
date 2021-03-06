#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.60])
AC_INIT([omx-components], [0.7.0], [daniel.charles at intel.com])
AC_CONFIG_SRCDIR([videocodec/OMXVideoEncoderH263.cpp])
AM_INIT_AUTOMAKE([foreign])
AM_CONFIG_HEADER([config.h])

AC_ARG_ENABLE(omx_debug,
    [AC_HELP_STRING([--enable-omx-debug],
                    [build with extra debug symbols @<:@default=no@:>@])],
    [], [enable_omx_debug="no"])

if test "$enable_omx_debug" = "yes"; then
AC_DEFINE([__ENABLE_DEBUG__], [1], [Defined to 1 if extra debug symbols are compiled])
fi

AC_ARG_ENABLE(libyami,
    AC_HELP_STRING([--enable-libyami],
                   [use libyami @<:@default=yes@:>@]),
   [], [enable_libyami="yes"])

if test "$enable_libyami" = "yes"; then
    AC_DEFINE([__USE_LIBYAMI__], [1], [use libyami])
else
    AC_DEFINE([__USE_LIBYAMI__], [0], [do not use libyami])
fi

# Checks for programs.
AC_PROG_CXX
AC_PROG_CC
AC_PROG_LIBTOOL

# Checks for libraries.

# Checks for header files.
AC_CHECK_HEADERS([unistd.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_HEADER_STDBOOL
AC_C_INLINE
AC_TYPE_INT32_T
AC_TYPE_UINT32_T
AC_TYPE_UINT8_T

pkgconfigdir=${libdir}/pkgconfig
AC_SUBST(pkgconfigdir)

PKG_CHECK_MODULES(OMXIL_UTILS, libomxil_utils)
PKG_CHECK_MODULES(OMXIL_BASE, libomxil_base)
PKG_CHECK_MODULES(LIBVA_DEPS, libva)

if test "$enable_libyami" = "no"; then
    PKG_CHECK_MODULES(MIXVBP, libmixvbp)
    PKG_CHECK_MODULES(MIXVBP_H264, libmixvbp-h264)
    PKG_CHECK_MODULES(MIXVBP_VP8, libmixvbp-vp8)
    PKG_CHECK_MODULES(VAVIDDEC_DEPS, libva_videodecoder)
    PKG_CHECK_MODULES(VAVIDENC_DEPS, libva_videoencoder)
else
    PKG_CHECK_MODULES(VAVIDDEC_DEPS, libyami_decoder)
    PKG_CHECK_MODULES(VAVIDENC_DEPS, libyami_encoder)
fi

# Checks for library functions.
AC_FUNC_MALLOC
AC_CHECK_FUNCS([gettimeofday memset])

AC_CONFIG_FILES([Makefile
                 videocodec/Makefile])
AC_OUTPUT
