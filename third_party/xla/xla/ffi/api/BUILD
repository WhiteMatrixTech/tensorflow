load("//xla:xla.bzl", "xla_cc_test")
load("@local_tsl//tsl:tsl.default.bzl", "filegroup")
load("@local_tsl//tsl/platform:rules_cc.bzl", "cc_library")

package(
    default_visibility = ["//visibility:public"],
)

#===-------------------------------------------------------------------------------------------===//
# Public XLA FFI API
#===-------------------------------------------------------------------------------------------===//

# XLA FFI is a header only library that does not have any dependencies on XLA. The intent is that
# users that do want to register custom FFI handlers with XLA should copy these headers to their
# project, build a shared object with an XLA FFI handler implementation, and load it at run time.
#
# `api.h` and `ffi.h` headers provide a C++ library for decoding XLA FFI C API structs into a more
# user friendly C++ types. Shared objects defining XLA FFI handlers should be built with private
# symbol visibility to avoid potential ODR violations coming from template instantiations of
# different XLA FFI versions.
#
# `ffi.h` defines builtin decoding for canonical XLA types, but users can add their own decodings
# with template specializations.

filegroup(
    name = "api_headers",
    srcs = ["api.h"],
    visibility = ["//visibility:public"],
)

filegroup(
    name = "c_api_headers",
    srcs = ["c_api.h"],
    visibility = ["//visibility:public"],
)

cc_library(
    name = "api",
    hdrs = [":api_headers"],
    visibility = ["//visibility:public"],
    deps = [":c_api"],
)

cc_library(
    name = "c_api",
    hdrs = ["c_api.h"],
    visibility = ["//visibility:public"],
)

cc_library(
    name = "c_api_internal",
    hdrs = ["c_api_internal.h"],
    visibility = ["//visibility:public"],
    deps = [":c_api"],
)

cc_library(
    name = "ffi",
    hdrs = ["ffi.h"],
    visibility = ["//visibility:public"],
    deps = [
        ":api",
        ":c_api",
    ],
)

#===-------------------------------------------------------------------------------------------===//
# Internal tests for XLA FFI API
#===-------------------------------------------------------------------------------------------===//

xla_cc_test(
    name = "ffi_test",
    srcs = ["ffi_test.cc"],
    deps = [
        ":api",
        ":ffi",
        "//xla:xla_data_proto_cc",
        "//xla/ffi:call_frame",
        "//xla/ffi:ffi_api",
        "//xla/ffi/api:c_api",
        "//xla/service:executable",
        "//xla/stream_executor:device_memory",
        "@com_google_absl//absl/log:check",
        "@com_google_absl//absl/status",
        "@local_tsl//tsl/lib/core:status_test_util",
        "@local_tsl//tsl/platform:test",
        "@local_tsl//tsl/platform:test_benchmark",
        "@local_tsl//tsl/platform:test_main",
    ],
)
