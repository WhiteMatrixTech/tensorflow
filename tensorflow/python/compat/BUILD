load("//tensorflow:strict.default.bzl", "py_strict_library")
load("//tensorflow:tensorflow.default.bzl", "tf_py_strict_test")

package(
    # copybara:uncomment default_applicable_licenses = ["//tensorflow:license"],
    licenses = ["notice"],
)

py_strict_library(
    name = "v2_compat",
    srcs = ["v2_compat.py"],
    srcs_version = "PY3",
    visibility = ["//tensorflow:internal"],
    deps = [
        "//tensorflow/python:tf2",
        "//tensorflow/python/data/experimental/ops:counter",
        "//tensorflow/python/data/experimental/ops:interleave_ops",
        "//tensorflow/python/data/experimental/ops:random_ops",
        "//tensorflow/python/data/experimental/ops:readers",
        "//tensorflow/python/data/ops:dataset_ops",
        "//tensorflow/python/data/ops:readers",
        "//tensorflow/python/eager:monitoring",
        "//tensorflow/python/framework:ops",
        "//tensorflow/python/framework:tensor",
        "//tensorflow/python/framework:tensor_shape",
        "//tensorflow/python/ops:control_flow_v2_toggles",
        "//tensorflow/python/ops:resource_variables_toggle",
        "//tensorflow/python/util:tf_export",
    ],
)

py_strict_library(
    name = "compat",
    srcs = ["compat.py"],
    srcs_version = "PY3",
    visibility = ["//tensorflow:internal"],
    deps = [
        "//tensorflow/python/platform:tf_logging",
        "//tensorflow/python/util:tf_contextlib",
        "//tensorflow/python/util:tf_export",
    ],
)

tf_py_strict_test(
    name = "compat_test",
    size = "small",
    srcs = ["compat_test.py"],
    tags = ["nofwdcompat"],
    deps = [
        ":compat",
        "//tensorflow/python/platform:client_testlib",
    ],
)

tf_py_strict_test(
    name = "disable_v2_behavior_test",
    size = "small",
    srcs = ["disable_v2_behavior_test.py"],
    deps = [
        ":v2_compat",
        "//tensorflow/python/framework:constant_op",
        "//tensorflow/python/framework:ops",
        "//tensorflow/python/platform:_pywrap_tf2",
        "//tensorflow/python/platform:client_testlib",
    ],
)
