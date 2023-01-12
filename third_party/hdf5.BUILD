# Copyright (C) 2022 Swift Navigation Inc.
# Contact: Swift Navigation <dev@swift-nav.com>
#
# This source is subject to the license found in the file 'LICENSE' which must
# be be distributed together with this source. All other rights reserved.
#
# THIS CODE AND INFORMATION IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
# EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE IMPLIED
# WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A PARTICULAR PURPOSE.

"""
hdf5@1.12.2

An hdf5 build file based on the one found in tensorflow repository:
https://github.com/tensorflow/io/blob/master/third_party/hdf5.BUILD
"""

exports_files(["COPYING"])

cc_library(
    name = "hdf5",
    srcs = glob(
        [
            "src/**/*.c",
            "hl/src/*.c",
        ],
        exclude = [
            "src/H5make_libsettings.c",
            "src/H5detect.c",
        ],
    ) + [
        "config/H5Tinit.c",
        "config/H5lib_settings.c",
    ],
    copts = select({
        "@bazel_tools//src/conditions:windows": [
            "/Zc:preprocessor-",
        ],
        "//conditions:default": [
            "-Wno-error=implicit-function-declaration",
        ],
    }),
    includes = [
        "config",
        "src",
        "src/H5FDsubfiling",
    ],
    linkopts = [],
    visibility = ["//visibility:public"],
    deps = [
        ":header",
    ],
)

cc_library(
    name = "hdf5_hl",
    srcs = glob(["hl/src/*.c"]),
    copts = select({
        "@bazel_tools//src/conditions:windows": [
            "/Zc:preprocessor-",
        ],
        "//conditions:default": [
            "-Wno-error=implicit-function-declaration",
        ],
    }),
    includes = [
        "hl/src",
    ],
    visibility = ["//visibility:public"],
    deps = [
        ":hdf5",
    ],
)

cc_library(
    name = "header",
    srcs = [],
    hdrs = glob([
        "src/**/*.h",
        "hl/src/*.h",
        "c++/src/*.h",
    ]) + [
        "config/H5pubconf.h",
    ],
    copts = select({
        "@bazel_tools//src/conditions:windows": [
            "/Zc:preprocessor-",
        ],
        "//conditions:default": [],
    }),
    includes = [
        "c++/src",
        "config",
        "hl/src",
        "src",
        "src/H5FDsubfiling",
    ],
    linkopts = [],
    visibility = ["//visibility:public"],
    deps = [
        "@zlib",
    ],
)

genrule(
    name = "H5pubconf_h",
    outs = ["config/H5pubconf.h"],
    cmd = "\n".join([
        "cat <<'EOF' >$@",
        "#ifndef H5_CONFIG_H_",
        "#define H5_CONFIG_H_",
        "",
        "#if defined(_MSC_VER)",
        "",
        "#define H5_HAVE_WINDOWS 1",
        "#define H5_HAVE_WIN32_API 1",
        "#define H5_HAVE_VISUAL_STUDIO 1",
        "#define H5_FC_FUNC(name,NAME) name ## _",
        "#define H5_FC_FUNC_(name,NAME) name ## _",
        "#define H5_FORTRAN_C_LONG_DOUBLE_IS_UNIQUE",
        "#define H5_FORTRAN_HAVE_C_LONG_DOUBLE",
        "#define H5_Fortran_COMPILER_ID",
        "#define H5_HAVE_GETCONSOLESCREENBUFFERINFO 1",
        "#define H5_HAVE_IO_H 1",
        "#define H5_HAVE_LIBWS2_32 1",
        "#define H5_HAVE_STDINT_H_CXX 1",
        "#define H5_HAVE_WINDOW_PATH 1",
        "#define H5_HAVE_WINSOCK2_H 1",
        '#define H5_PRINTF_LL_WIDTH "I64"',
        "#define H5_SIZEOF_INT_FAST16_T 4",
        "#define H5_SIZEOF_INT_FAST32_T 4",
        "#define H5_SIZEOF_LONG 4",
        "#define H5_SIZEOF_LONG_DOUBLE 8",
        "#define H5_SIZEOF_OFF_T 4",
        "#define H5_SIZEOF_UINT_FAST16_T 4",
        "#define H5_SIZEOF_UINT_FAST32_T 4",
        "#define H5_SIZEOF___FLOAT128 0",
        "#define H5_SIZEOF___INT64 8",
        "",
        "#elif defined(__APPLE__)",
        "",
        "#define H5_CXX_HAVE_OFFSETOF 1",
        "#define H5_DEV_T_IS_SCALAR 1",
        "#define H5_HAVE_ALARM 1",
        "#define H5_HAVE_ASPRINTF 1",
        "#define H5_HAVE_ATTRIBUTE 1",
        "#define H5_HAVE_C99_DESIGNATED_INITIALIZER 1",
        "#define H5_HAVE_C99_FUNC 1",
        "#define H5_HAVE_CLOCK_GETTIME 1",
        "#define H5_HAVE_DIRENT_H 1",
        "#define H5_HAVE_DLFCN_H 1",
        "#define H5_HAVE_FCNTL 1",
        "#define H5_HAVE_FLOCK 1",
        "#define H5_HAVE_FORK 1",
        "#define H5_HAVE_FREXPF 1",
        "#define H5_HAVE_FREXPL 1",
        "#define H5_HAVE_GETPWUID 1",
        "#define H5_HAVE_GETRUSAGE 1",
        "#define H5_HAVE_IOCTL 1",
        "#define H5_HAVE_LIBDL 1",
        "#define H5_HAVE_LSTAT 1",
        "#define H5_HAVE_PREADWRITE 1",
        "#define H5_HAVE_RANDOM 1",
        "#define H5_HAVE_RAND_R 1",
        '#define H5_PRINTF_LL_WIDTH "l"',
        "#define H5_HAVE_DARWIN 1",
        "#define H5_HAVE_MACH_MACH_TIME_H 1",
        "#define H5_HAVE_SIGSETJMP 1",
        "#define H5_HAVE_SIGLONGJMP 1",
        "#define H5_HAVE_SIGPROCMASK 1",
        "#define H5_HAVE_SNPRINTF 1",
        "#define H5_HAVE_SRANDOM 1",
        "#define H5_HAVE_STRINGS_H 1",
        "#define H5_HAVE_SYMLINK 1",
        "#define H5_HAVE_SYS_FILE_H 1",
        "#define H5_HAVE_SYS_IOCTL_H 1",
        "#define H5_HAVE_SYS_RESOURCE_H 1",
        "#define H5_HAVE_SYS_SOCKET_H 1",
        "#define H5_HAVE_SYS_TIME_H 1",
        "#define H5_HAVE_TIOCGETD 1",
        "#define H5_HAVE_TIOCGWINSZ 1",
        "#define H5_HAVE_TM_GMTOFF 1",
        "#define H5_HAVE_UNISTD_H 1",
        "#define H5_HAVE_VASPRINTF 1",
        "#define H5_HAVE_VSNPRINTF 1",
        "#define H5_HAVE_WAITPID 1",
        "#define H5_HAVE___INLINE__ 1",
        "#define H5_PAC_C_MAX_REAL_PRECISION 21",
        "#define H5_SIZEOF_INT_FAST16_T 2",
        "#define H5_SIZEOF_INT_FAST32_T 4",
        "#define H5_SIZEOF_SSIZE_T 8",
        "#define H5_SIZEOF_LONG 8",
        "#define H5_SIZEOF_LONG_DOUBLE 16",
        "#define H5_SIZEOF_PTRDIFF_T 8",
        "#define H5_SIZEOF_OFF_T 8",
        "#define H5_SIZEOF_UINT_FAST16_T 2",
        "#define H5_SIZEOF_UINT_FAST32_T 4",
        "#define H5_SIZEOF___FLOAT128 0",
        "#define H5_SIZEOF___INT64 0",
        "#define H5_TIME_WITH_SYS_TIME 1",
        "",
        "#else",
        "",
        "#define H5_CXX_HAVE_OFFSETOF 1",
        "#define H5_DEV_T_IS_SCALAR 1",
        "#define H5_HAVE_ALARM 1",
        "#define H5_HAVE_ASPRINTF 1",
        "#define H5_HAVE_ATTRIBUTE 1",
        "#define H5_HAVE_C99_DESIGNATED_INITIALIZER 1",
        "#define H5_HAVE_C99_FUNC 1",
        "#define H5_HAVE_CLOCK_GETTIME 1",
        "#define H5_HAVE_DIRENT_H 1",
        "#define H5_HAVE_DLFCN_H 1",
        "#define H5_HAVE_FCNTL 1",
        "#define H5_HAVE_FLOCK 1",
        "#define H5_HAVE_FORK 1",
        "#define H5_HAVE_FREXPF 1",
        "#define H5_HAVE_FREXPL 1",
        "#define H5_HAVE_GETPWUID 1",
        "#define H5_HAVE_GETRUSAGE 1",
        "#define H5_HAVE_IOCTL 1",
        "#define H5_HAVE_LIBDL 1",
        "#define H5_HAVE_LSTAT 1",
        "#define H5_HAVE_PREADWRITE 1",
        '#define H5_PRINTF_LL_WIDTH "l"',
        "#define H5_HAVE_FEATURES_H 1",
        "#define H5_HAVE_FLOAT128 1",
        "#define H5_HAVE_QUADMATH_H 1",
        "#define H5_HAVE_RANDOM 1",
        "#define H5_HAVE_RAND_R 1",
        "#define H5_HAVE_SIGLONGJMP 1",
        "#define H5_HAVE_SIGPROCMASK 1",
        "#define H5_HAVE_SNPRINTF 1",
        "#define H5_HAVE_SRANDOM 1",
        "#define H5_HAVE_STRINGS_H 1",
        "#define H5_HAVE_SYMLINK 1",
        "#define H5_HAVE_SYS_FILE_H 1",
        "#define H5_HAVE_SYS_IOCTL_H 1",
        "#define H5_HAVE_SYS_RESOURCE_H 1",
        "#define H5_HAVE_SYS_SOCKET_H 1",
        "#define H5_HAVE_SYS_TIME_H 1",
        "#define H5_HAVE_TIOCGETD 1",
        "#define H5_HAVE_TIOCGWINSZ 1",
        "#define H5_HAVE_TM_GMTOFF 1",
        "#define H5_HAVE_UNISTD_H 1",
        "#define H5_HAVE_VASPRINTF 1",
        "#define H5_HAVE_VSNPRINTF 1",
        "#define H5_HAVE_WAITPID 1",
        "#define H5_HAVE___INLINE__ 1",
        "#define H5_PAC_C_MAX_REAL_PRECISION 33",
        "#define H5_SIZEOF_INT_FAST16_T 8",
        "#define H5_SIZEOF_INT_FAST32_T 8",
        "#define H5_SIZEOF_SSIZE_T 8",
        "#define H5_SIZEOF_LONG 8",
        "#define H5_SIZEOF_LONG_DOUBLE 16",
        "#define H5_SIZEOF_PTRDIFF_T 8",
        "#define H5_SIZEOF_OFF_T 8",
        "#define H5_SIZEOF_UINT_FAST16_T 8",
        "#define H5_SIZEOF_UINT_FAST32_T 8",
        "#define H5_SIZEOF___FLOAT128 16",
        "#define H5_SIZEOF___INT64 0",
        "#define H5_TIME_WITH_SYS_TIME 1",
        "",
        "#endif",
        "",
        '#define H5_DEFAULT_PLUGINDIR "/usr/local/hdf5/lib/plugin"',
        "#define H5_HAVE_DIFFTIME 1",
        "#define H5_HAVE_EMBEDDED_LIBINFO 1",
        "#define H5_HAVE_FILTER_DEFLATE 1",
        "#define H5_HAVE_FUNCTION 1",
        "#define H5_HAVE_GETHOSTNAME 1",
        "#define H5_HAVE_GETTIMEOFDAY 1",
        "#define H5_HAVE_INLINE 1",
        "#define H5_HAVE_INTTYPES_H 1",
        "#define H5_HAVE_LIBM 1",
        "#define H5_HAVE_LIBZ 1",
        "#define H5_HAVE_LLROUND 1",
        "#define H5_HAVE_LLROUNDF 1",
        "#define H5_HAVE_LONGJMP 1",
        "#define H5_HAVE_LROUND 1",
        "#define H5_HAVE_LROUNDF 1",
        "#define H5_HAVE_MEMORY_H 1",
        "#define H5_HAVE_ROUND 1",
        "#define H5_HAVE_ROUNDF 1",
        "#define H5_HAVE_SETJMP 1",
        "#define H5_HAVE_SETJMP_H 1",
        "#define H5_HAVE_SIGNAL 1",
        "#define H5_HAVE_STDBOOL_H 1",
        "#define H5_HAVE_STDDEF_H 1",
        "#define H5_HAVE_STDINT_H 1",
        "#define H5_HAVE_STDLIB_H 1",
        "#define H5_HAVE_STRDUP 1",
        "#define H5_HAVE_STRING_H 1",
        "#define H5_HAVE_STRTOLL 1",
        "#define H5_HAVE_STRTOULL 1",
        "#define H5_HAVE_SYSTEM 1",
        "#define H5_HAVE_SYS_STAT_H 1",
        "#define H5_HAVE_SYS_TIMEB_H 1",
        "#define H5_HAVE_SYS_TYPES_H 1",
        "#define H5_HAVE_TIMEZONE 1",
        "#define H5_HAVE_TMPFILE 1",
        "#define H5_HAVE_ZLIB_H 1",
        "#define H5_HAVE___INLINE 1",
        "#define H5_INCLUDE_HL 1",
        "#define H5_LDOUBLE_TO_LLONG_ACCURATE 1",
        "#define H5_LLONG_TO_LDOUBLE_CORRECT 1",
        '#define H5_LT_OBJDIR ".libs/"',
        "#define H5_NO_ALIGNMENT_RESTRICTIONS 1",
        '#define H5_PACKAGE "hdf5"',
        '#define H5_PACKAGE_BUGREPORT "help@hdfgroup.org"',
        '#define H5_PACKAGE_NAME "HDF5"',
        '#define H5_PACKAGE_STRING "HDF5 1.12.2"',
        '#define H5_PACKAGE_TARNAME "hdf5"',
        '#define H5_PACKAGE_URL "http://www.hdfgroup.org"',
        '#define H5_PACKAGE_VERSION "1.12.2"',
        "#define H5_HAVE_PWD_H 1",
        "#define H5_SIZEOF_BOOL 1",
        "#define H5_SIZEOF_CHAR 1",
        "#define H5_SIZEOF_DOUBLE 8",
        "#define H5_SIZEOF_FLOAT 4",
        "#define H5_SIZEOF_INT 4",
        "#define H5_SIZEOF_INT16_T 2",
        "#define H5_SIZEOF_INT32_T 4",
        "#define H5_SIZEOF_INT64_T 8",
        "#define H5_SIZEOF_INT8_T 1",
        "#define H5_SIZEOF_INT_FAST64_T 8",
        "#define H5_SIZEOF_INT_FAST8_T 1",
        "#define H5_SIZEOF_INT_LEAST16_T 2",
        "#define H5_SIZEOF_INT_LEAST32_T 4",
        "#define H5_SIZEOF_INT_LEAST64_T 8",
        "#define H5_SIZEOF_INT_LEAST8_T 1",
        "#define H5_SIZEOF_LONG_LONG 8",
        "#define H5_SIZEOF_SHORT 2",
        "#define H5_SIZEOF_SIZE_T 8",
        "#define H5_SIZEOF_TIME_T 8",
        "#define H5_SIZEOF_UINT16_T 2",
        "#define H5_SIZEOF_UINT32_T 4",
        "#define H5_SIZEOF_UINT64_T 8",
        "#define H5_SIZEOF_UINT8_T 1",
        "#define H5_SIZEOF_UINT_FAST64_T 8",
        "#define H5_SIZEOF_UINT_FAST8_T 1",
        "#define H5_SIZEOF_UINT_LEAST16_T 2",
        "#define H5_SIZEOF_UINT_LEAST32_T 4",
        "#define H5_SIZEOF_UINT_LEAST64_T 8",
        "#define H5_SIZEOF_UINT_LEAST8_T 1",
        "#define H5_SIZEOF_UNSIGNED 4",
        "#define H5_SIZEOF__QUAD 0",
        "#define H5_STDC_HEADERS 1",
        "#define H5_USE_112_API_DEFAULT 1",
        '#define H5_VERSION "1.12.2"',
        "#define H5_WANT_DATA_ACCURACY 1",
        "#define H5_WANT_DCONV_EXCEPTION 1",
        "",
        "#endif",
        "EOF",
    ]),
)

genrule(
    name = "H5lib_settings_c",
    outs = ["config/H5lib_settings.c"],
    cmd = "\n".join([
        "cat <<'EOF' >$@",
        "char H5libhdf5_settings[]=\"swiftnav\";",
        "EOF",
    ]),
)

# TODO Generated file will cause problems with caching [BUILD-499]
genrule(
    name = "H5Tinit_c",
    outs = ["config/H5Tinit.c"],
    cmd = "$(location :H5detect) $@",
    tools = [":H5detect"],
)

cc_binary(
    name = "H5detect",
    srcs = [
        "src/H5detect.c",
    ],
    includes = [],
    linkopts = select({
        "@bazel_tools//src/conditions:windows": [
            "-DEFAULTLIB:ws2_32.lib",
        ],
        "//conditions:default": [],
    }),
    deps = [
        ":header",
    ],
)
