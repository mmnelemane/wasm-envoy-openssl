workspace(name = "envoy_openssl")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "openssl",
    build_file = "@//:openssl.BUILD",
    sha256 = "23011a5cc78e53d0dc98dfa608c51e72bcd350aa57df74c5d5574ba4ffb62e74",
    strip_prefix = "openssl-OpenSSL_1_1_1d",
    urls = ["https://github.com/openssl/openssl/archive/OpenSSL_1_1_1d.tar.gz"],
)

new_local_repository(
    name = "openssl_shared",
    build_file = "openssl_host_shared.BUILD",
    path = "/usr/lib/x86_64-linux-gnu",
)

local_repository(
    name = "envoy_build_config",
    path = "envoy_build_config",
)

local_repository(
    name = "envoy",
    path = "envoy",
    repo_mapping = {
        "@boringssl": "@openssl",
    },
)

load("@envoy//bazel:api_binding.bzl", "envoy_api_binding")

envoy_api_binding()

load("@envoy//bazel:api_repositories.bzl", "envoy_api_dependencies")

envoy_api_dependencies()

load("@envoy//bazel:repositories.bzl", "envoy_dependencies")

envoy_dependencies()

load("@envoy//bazel:dependency_imports.bzl", "envoy_dependency_imports")

envoy_dependency_imports()

load("@envoy//bazel:repository_locations.bzl", "REPOSITORY_LOCATIONS")

http_archive(
    name = "com_github_google_jwt_verify_patched",
    patch_args = ["-p1"],
    patches = ["//:jwt_verify-make-compatible-with-openssl.patch"],
    sha256 = REPOSITORY_LOCATIONS["com_github_google_jwt_verify"]["sha256"],
    strip_prefix = REPOSITORY_LOCATIONS["com_github_google_jwt_verify"].get("strip_prefix", ""),
    urls = REPOSITORY_LOCATIONS["com_github_google_jwt_verify"]["urls"],
)

# TODO: Consider not using `bind`. See https://github.com/bazelbuild/bazel/issues/1952 for details.
bind(
    name = "jwt_verify_lib",
    actual = "@com_github_google_jwt_verify_patched//:jwt_verify_lib",
)

http_archive(
    name = "rules_antlr",
    sha256 = "7249d1569293d9b239e23c65f6b4c81a07da921738bde0dfeb231ed98be40429",
    strip_prefix = "rules_antlr-3cc2f9502a54ceb7b79b37383316b23c4da66f9a",
    urls = ["https://github.com/marcohu/rules_antlr/archive/3cc2f9502a54ceb7b79b37383316b23c4da66f9a.tar.gz"],
)

http_archive(
    name = "antlr4_runtimes",
    build_file_content = """
package(default_visibility = ["//visibility:public"])
cc_library(
    name = "cpp",
    srcs = glob(["runtime/Cpp/runtime/src/**/*.cpp"]),
    hdrs = glob(["runtime/Cpp/runtime/src/**/*.h"]),
    includes = ["runtime/Cpp/runtime/src"],
)
""",
    sha256 = "992d52444b81ed75e52ea62f9f38ecb7652d5ce2a2130af143912b3042a6d77e",
    patch_args = ["-p1"],
    # Patches ASAN violation of initialization fiasco
    patches = ["@envoy//bazel:antlr.patch"],
    strip_prefix = "antlr4-4.8",
    urls = ["https://github.com/antlr/antlr4/archive/4.8.tar.gz"],
)

http_archive(
    name = "proxy_wasm_cpp_host",
    sha256 = "40558ce134552ba9afb082ad5cf7c2cf157baeb38539810edb43b6eb109596dc",
    strip_prefix = "proxy-wasm-cpp-host-375ce583a79ca98afa86a2e56f196ea7321d6b1e",
    urls = ["https://github.com/proxy-wasm/proxy-wasm-cpp-host/archive/375ce583a79ca98afa86a2e56f196ea7321d6b1e.tar.gz"],
)

http_archive(
    name = "proxy_wasm_cpp_sdk",
    sha256 = "f9d744997172333110766a4bcb613206064aebe103dbb9293bc1b532d19a8d7d",
    strip_prefix = "proxy-wasm-cpp-sdk-9ab06092c4579a74efee16ec37becd42aca66074",
    urls = ["https://github.com/proxy-wasm/proxy-wasm-cpp-sdk/archive/9ab06092c4579a74efee16ec37becd42aca66074.tar.gz"],
)
