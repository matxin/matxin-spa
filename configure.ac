#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.59)
AC_INIT([matxin-spa], [1.5.0])
PACKAGE=matxin-spa

GENERIC_MAJOR_VERSION=1
GENERIC_MINOR_VERSION=5
GENERIC_MICRO_VERSION=0

GENERIC_RELEASE=$GENERIC_MAJOR_VERSION.$GENERIC_MINOR_VERSION
GENERIC_RELEASE=$GENERIC_MAJOR_VERSION.$GENERIC_MINOR_VERSION.$GENERIC_MICRO_VERSION
AC_SUBST(GENERIC_RELEASE)
AC_SUBST(GENERIC_VERSION)

AC_PROG_CXX

#
# API version (often = GENERIC_MAJOR_VERSION.GENERIC_MINOR_VERSION)
#
GENERIC_API_VERSION=$GENERIC_MAJOR_VERSION
AC_SUBST(GENERIC_API_VERSION)

AC_SUBST(GENERIC_LIBRARY_NAME, $PACKAGE)

#
# Required library versions
#
m4_define([required_lttoolbox_version], [3.2.0])
m4_define([required_libxml_version], [2.6.17])
m4_define([required_matxin_version], [1.4.0])
m4_define([required_libpcre_version], [6.4])

#
# Our configure script should create Makefiles
#
AM_INIT_AUTOMAKE([-Wall -Werror foreign])
#AM_INIT_AUTOMAKE

#
# Set default paths for PKG_CONFIG_PATH in case it's not defined
#
if ! test $PKG_CONFIG_PATH ; then
  PKG_CONFIG_PATH="/usr/lib/pkgconfig:/usr/local/lib/pkgconfig"
fi

AC_ARG_WITH(freeling,
            [AS_HELP_STRING([--with-freeling=DIR],
                            [Look for freeling include/libs in DIR])],
            [ case "$withval" in
               no)
                 ;;
               *)
                 CPPFLAGS="-I$withval/include $CPPFLAGS"
                 LDFLAGS="-L$withval/lib $LDFLAGS"
                 ;;
              esac ])



AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET
AC_PROG_AWK
AC_LANG([C++])


AC_MSG_CHECKING([Operating System])
OSTYPE=$($(which uname) -s)
AC_MSG_RESULT([$OSTYPE])
AC_SUBST(OSTYPE)

# We need this to determine whether we use zcat or gzcat
AM_CONDITIONAL(OS_IS_SOLARIS, [test x"$OSTYPE" = xSunOS])
AM_CONDITIONAL(OS_IS_DARWIN, [test x"$OSTYPE" = xDarwin])

#
# These programs are required during the make process so we
# must test they're available on the current system
#
if test x$ARCH = xppc
then
  AC_PATH_PROG(XSLTPROC, sabcmd, no)
  if test x$ac_cv_path_XSLTPROC = x
  then
    AC_MSG_ERROR([sablotron not found. You may want to adjust your PATH.])
  fi
  if test x$ac_cv_path_XSLTPROC = xno
  then
    AC_MSG_ERROR([sablotron not found. You may want to adjust your PATH.])
  fi
else
  AC_PATH_PROG(XSLTPROC, xsltproc, no)
  if test x$ac_cv_path_XSLTPROC = x
  then
    AC_MSG_ERROR([xsltproc not found. You may want to adjust your PATH.])
  fi
  if test x$ac_cv_path_XSLTPROC = xno
  then
    AC_MSG_ERROR([xsltproc not found. You may want to adjust your PATH.])
  fi
fi

AC_PATH_PROG(LT_COMP, lt-comp, no)
if test x$ac_cv_path_LT_COMP = x
then
  AC_MSG_ERROR([lt-comp not found. You may want to adjust your PATH.])
fi
if test x$ac_cv_path_LT_COMP = xno
then
  AC_MSG_ERROR([lt-comp not found. You may want to adjust your PATH.])
fi


PKG_CHECK_MODULES(MATXIN, [dnl
 lttoolbox >= required_lttoolbox_version dnl
 matxin >= required_matxin_version dnl
 libpcre >= required_libpcre_version], CPPFLAGS="$CPPFLAGS $MATXIN_CPPFLAGS $MATXIN_CFLAGS"; LIBS="$LIBS")

# libpcre >= required_libpcre_version], CPPFLAGS="$CPPFLAGS $MATXIN_CPPFLAGS $MATXIN_CFLAGS"; LIBS="$LIBS $MATXIN_LIBS")

AP_MKINCLUDE

#
# Generate these files
#
AC_CONFIG_FILES([
                 Makefile
		 matxin-spa.pc
		 matxin-spa.spa.cfg
		 freeling/Makefile
		 freeling/common/Makefile
		 freeling/common/nec/Makefile
		 freeling/common/corrector/Makefile
		 freeling/chunker/Makefile
		 freeling/corrector/Makefile
		 freeling/dep/Makefile
		 freeling/nerc/Makefile
		 freeling/nerc/data/Makefile
		 freeling/nerc/nec/Makefile
		 freeling/nerc/ner/Makefile
                 ])
AC_OUTPUT

#
# Print summary for the selected configuration
#
echo
echo "**  $PACKAGE_NAME $PACKAGE_VERSION - selected build configuration  **"
echo
echo "Install prefix ................... : $prefix"
echo
echo "Build architecture ............... : $ARCH"
echo "Operating System ................. : $OSTYPE"
echo
echo "Now type 'make', followed by 'make install' as root."
echo "If there are any problems, read the INSTALL file."
echo

