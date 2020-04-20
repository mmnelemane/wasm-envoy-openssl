licenses(["notice"])  # Apache 2

# Access log implementation that calls into a WASM VM.

load(
    "@envoy//bazel:envoy_build_system.bzl",
    "envoy_cc_library",
    "envoy_package",
)

envoy_package()

envoy_cc_library(
    name = "wasm_access_log_lib",
    repository = "@envoy",
    hdrs = ["wasm_access_log_impl.h"],
    deps = [
        "@envoy//include/envoy/access_log:access_log_interface",
        "@envoy//source/common/http:header_map_lib",
    ],
)

envoy_cc_library(
    name = "config",
    repository = "@envoy",
    srcs = ["config.cc"],
    hdrs = ["config.h"],
    deps = [
        ":wasm_access_log_lib",
        "@envoy//include/envoy/registry",
        "@envoy//include/envoy/server:access_log_config_interface",
        "@envoy//source/common/access_log:access_log_formatter_lib",
        "@envoy//source/common/config:datasource_lib",
        "@envoy//source/common/protobuf",
        "@envoy//source/extensions/access_loggers:well_known_names",
        "//source/extensions/common/wasm:wasm_lib",
        "@envoy_api//envoy/extensions/access_loggers/wasm/v3:pkg_cc_proto",
    ],
)
