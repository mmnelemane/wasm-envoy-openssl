licenses(["notice"])  # Apache 2

# WASM service.

load(
    "@envoy//bazel:envoy_build_system.bzl",
    "envoy_cc_library",
    "envoy_package",
)

envoy_package()

envoy_cc_library(
    name = "config",
    repository = "@envoy",
    srcs = ["config.cc"],
    hdrs = ["config.h"],
    deps = [
        "@envoy//include/envoy/registry",
        "@envoy//include/envoy/server:wasm_config_interface",
        "@envoy//source/common/common:assert_lib",
        "@envoy//source/common/common:empty_string",
        "@envoy//source/common/config:datasource_lib",
        "@envoy//source/common/protobuf:utility_lib",
        "//source/extensions/common/wasm:wasm_lib",
        "@envoy//source/extensions/grpc_credentials:well_known_names",
        "@envoy_api//envoy/extensions/wasm/v3:pkg_cc_proto",
    ],
)
