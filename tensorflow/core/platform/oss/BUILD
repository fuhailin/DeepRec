# Description:
# OSS file system implementation.

package(
    default_visibility = ["//visibility:public"],
    licenses = ["notice"],  # Apache 2.0
)

cc_library(
    name = "oss_file_system",
    srcs = ["oss_file_system.cc"],
    hdrs = ["oss_file_system.h"],
    deps = [
        "//tensorflow/core:lib",
        "//tensorflow/core:lib_internal",
        "@aliyun_oss_c_sdk",
    ],
    alwayslink = 1,
)