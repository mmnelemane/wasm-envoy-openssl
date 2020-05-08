licenses(["notice"])  # Apache 2

load(
    "@envoy//bazel:envoy_build_system.bzl",
    "envoy_cc_library",
    "envoy_package",
)

envoy_package()

envoy_cc_library(
    name = "well_known_names",
    repository = "@envoy",
    hdrs = ["well_known_names.h"],
    deps = [
        "@envoy//source/common/singleton:const_singleton",
    ],
)

# NB: Used to break the circular dependency between wasm_lib and null_plugin_lib.
envoy_cc_library(
    name = "wasm_hdr",
    repository = "@envoy",
    hdrs = [
        "context.h",
        "foreign.h",
        "wasm.h",
        "wasm_vm.h",
    ],
    deps = [
        ":well_known_names",
        "@envoy//include/envoy/http:codes_interface",
        "@envoy//include/envoy/http:filter_interface",
        "@envoy//include/envoy/server:wasm_interface",
        "@envoy//include/envoy/upstream:cluster_manager_interface",
        "@envoy//source/common/config:datasource_lib",
        "@envoy//source/common/stats:stats_lib",
        "@envoy//source/extensions/filters/common/expr:evaluator_lib",
        "@envoy//source/extensions/filters/http:well_known_names",
        "@com_google_cel_cpp//eval/public:activation",
        "@envoy_api//envoy/extensions/wasm/v3:pkg_cc_proto",
        "@proxy_wasm_cpp_host//:include",
        "@proxy_wasm_cpp_sdk//:common_lib",
    ],
)

envoy_cc_library(
    name = "wasm_interoperation_lib",
    repository = "@envoy",
    srcs = [
        "wasm_state.cc",
    ],
    hdrs = [
        "wasm_state.h",
    ],
    deps = [
        "@envoy//include/envoy/stream_info:filter_state_interface",
        "@envoy//source/common/protobuf",
    ],
)

envoy_cc_library(
    name = "wasm_lib",
    repository = "@envoy",
    srcs = [
        "context.cc",
        "foreign.cc",
        "wasm.cc",
        "wasm_vm.cc",
    ],
    external_deps = [
        "abseil_base",
        "abseil_node_hash_map",
    ],
    deps = [
        ":wasm_hdr",
        ":wasm_interoperation_lib",
        "@envoy//include/envoy/server:lifecycle_notifier_interface",
        "@envoy//source/common/buffer:buffer_lib",
        "@envoy//source/common/common:enum_to_int",
        "@envoy//source/common/http:message_lib",
        "@envoy//source/common/http:utility_lib",
        "@envoy//source/common/tracing:http_tracer_lib",
        "@envoy//source/extensions/filters/common/expr:context_lib",
        "@com_google_cel_cpp//eval/eval:field_access",
        "@com_google_cel_cpp//eval/eval:field_backed_list_impl",
        "@com_google_cel_cpp//eval/eval:field_backed_map_impl",
        "@com_google_cel_cpp//eval/public:builtin_func_registrar",
        "@com_google_cel_cpp//eval/public:cel_expr_builder_factory",
        "@com_google_cel_cpp//eval/public:cel_value",
        "@com_google_cel_cpp//eval/public:value_export_util",
        "@com_google_cel_cpp//parser",
        "@envoy_api//envoy/extensions/wasm/v3:pkg_cc_proto",
        "@proxy_wasm_cpp_host//:lib",
        "//boringssl_compat:bssl_compat_lib",
        "//boringssl_compat:bssl_compat_cbs_lib",
    ],
)
