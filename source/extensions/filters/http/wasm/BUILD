licenses(["notice"])  # Apache 2

# Public docs: docs/root/configuration/http_filters/wasm_filter.rst

load(
    "@envoy//bazel:envoy_build_system.bzl",
    "envoy_cc_library",
    "envoy_package",
)

envoy_package()

envoy_cc_library(
    name = "wasm_filter_lib",
    repository = "@envoy",
    srcs = ["wasm_filter.cc"],
    hdrs = ["wasm_filter.h"],
    deps = [
        "@envoy//include/envoy/http:codes_interface",
        "@envoy//include/envoy/server:filter_config_interface",
        "@envoy//include/envoy/upstream:cluster_manager_interface",
        "//source/extensions/common/wasm:wasm_lib",
        "@envoy//source/extensions/filters/http:well_known_names",
        "@envoy_api//envoy/extensions/filters/http/wasm/v3:pkg_cc_proto",
    ],
)

envoy_cc_library(
    name = "config",
    repository = "@envoy",
    srcs = ["config.cc"],
    hdrs = ["config.h"],
    deps = [
        ":wasm_filter_lib",
        "@envoy//include/envoy/registry",
        "@envoy//source/common/common:empty_string",
        "@envoy//source/common/config:datasource_lib",
        "//source/extensions/common/wasm:wasm_lib",
        "@envoy//source/extensions/filters/http:well_known_names",
        "@envoy//source/extensions/filters/http/common:factory_base_lib",
        "@envoy_api//envoy/extensions/filters/http/wasm/v3:pkg_cc_proto",
    ],
)
