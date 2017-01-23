dnl                                               -*- Autoconf -*-
dnl Process this file with autoconf to produce a configure script.

AC_PREREQ([2.67])
AC_INIT([udns], [0.4], [mjt@corpit.ru])
AC_CONFIG_SRCDIR([udns.h])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_AUX_DIR(auto)
AC_USE_SYSTEM_EXTENSIONS

AM_INIT_AUTOMAKE([subdir-objects foreign -Wno-gnu -Werror])
m4_ifdef([AM_PROG_AR], [AM_PROG_AR])
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])
AM_MAINTAINER_MODE
AM_DEP_TRACK

dnl Checks for lib
AC_DISABLE_STATIC
AC_DISABLE_SHARED
LT_INIT([dlopen])

dnl Checks for inet_ntop
ss_FUNC_INET_NTOP

dnl Checks for programs.
AC_PROG_CC
AM_PROG_CC_C_O
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_LIBTOOL
AC_PROG_MAKE_SET
AC_LANG_SOURCE

dnl Checks for host.
AC_MSG_CHECKING(for what kind of host)

case $host in
  *-linux*)
    os_support=linux
    AC_MSG_RESULT(Linux)
    ;;
  *-mingw*)
    dnl Add custom macros for libev
    AC_DEFINE([FD_SETSIZE], [2048], [Reset max file descriptor size.])
    AC_DEFINE([EV_FD_TO_WIN32_HANDLE(fd)], [(fd)], [Override libev default fd conversion macro.])
    AC_DEFINE([EV_WIN32_HANDLE_TO_FD(handle)], [(handle)], [Override libev default handle conversion macro.])
    AC_DEFINE([EV_WIN32_CLOSE_FD(fd)], [closesocket(fd)], [Override libev default fd close macro.])

    os_support=mingw
    AC_MSG_RESULT(MinGW)
    ;;
  *)
    AC_MSG_RESULT(transparent proxy does not support for $host)
    ;;
esac

AC_C_BIGENDIAN

dnl Checks for typedefs, structures, and compiler characteristics.
AC_C_INLINE
AC_TYPE_SSIZE_T

dnl Checks for header files.
AC_HEADER_ASSERT
AC_HEADER_STDC
AC_HEADER_SYS_WAIT

dnl Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_TYPE_PID_T
AC_TYPE_SIZE_T
AC_TYPE_SSIZE_T
AC_TYPE_UINT16_T
AC_TYPE_UINT8_T
AC_HEADER_TIME

dnl Checks for library functions.
AC_FUNC_FORK
AC_FUNC_SELECT_ARGTYPES
AC_TYPE_SIGNAL
AC_CHECK_FUNCS([memset select setresuid setreuid strerror getpwnam_r setrlimit])

dnl Checks for library functions.
AC_CHECK_FUNCS([malloc memset socket])

dnl Add define for libudns to enable IPv6 support
dnl This is an option defined in the origin configure script
AC_DEFINE([HAVE_IPv6], [1], [Enable IPv6 support in libudns])

AC_CONFIG_FILES([Makefile])

AC_OUTPUT
