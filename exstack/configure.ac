#/******************************************************************
#
#
#  Copyright(C) 2018, Institute for Defense Analyses
#  4850 Mark Center Drive, Alexandria, VA; 703-845-2500
#  This material may be reproduced by or for the US Government
#  pursuant to the copyright license under the clauses at DFARS
#  252.227-7013 and 252.227-7014.
# 
#
#  All rights reserved.
#  
#  Redistribution and use in source and binary forms, with or without
#  modification, are permitted provided that the following conditions are met:
#    * Redistributions of source code must retain the above copyright
#      notice, this list of conditions and the following disclaimer.
#    * Redistributions in binary form must reproduce the above copyright
#      notice, this list of conditions and the following disclaimer in the
#      documentation and/or other materials provided with the distribution.
#    * Neither the name of the copyright holder nor the
#      names of its contributors may be used to endorse or promote products
#      derived from this software without specific prior written permission.
# 
#  THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
#  "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
#  LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS
#  FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE
#  COPYRIGHT HOLDER NOR CONTRIBUTORS BE LIABLE FOR ANY DIRECT,
#  INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
#  (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
#  SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
#  HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT,
#  STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
#  ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED
#  OF THE POSSIBILITY OF SUCH DAMAGE.
# 
# *****************************************************************/ 

AC_PREREQ([2.60])     #Require Minimum Autotools version 2.60

AC_INIT([exstack],   [1.0.0],   [bale@super.org])
AM_INIT_AUTOMAKE([1.10 foreign no-define tar-ustar])

AC_CONFIG_HEADERS([config.h])

AC_ARG_WITH([upc],
            AS_HELP_STRING([--with-upc], [build a UPC version]),
            [], [with_upc=yes])
AC_ARG_WITH([shmem],
            AS_HELP_STRING([--with-shmem], [build a SHMEM version]),
            [], [with_shmem=no])


AC_PROG_RANLIB
AC_PROG_CC
AC_PROG_CC_C99
mpp_use_shmem=no
if test "x$with_shmem" = xyes; then
   with_upc=no
   mpp_use_shmem=yes
fi

if test "x$with_upc" = xyes; then
AM_PROG_UPC
else
  # must define this ugly conditional to keep automake happy
  AM_CONDITIONAL(am__fastdepUPC, [test])
fi

PKG_CHECK_MODULES([libdeps],
  [
        libgetput
  ]
)

AM_CONDITIONAL(BUILD_UPC, [test "x$with_upc" = xyes])
AM_CONDITIONAL(BUILD_SHMEM, [test "x$mpp_use_shmem" = xyes])

AC_CONFIG_FILES([
exstack.pc:exstack.pc.in
Makefile
])

AC_OUTPUT

