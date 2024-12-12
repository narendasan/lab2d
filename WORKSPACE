workspace(name = "org_deepmind_lab2d")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "com_google_googletest",
    sha256 = "f179ec217f9b3b3f3c6e8b02d3e7eda997b49e4ce26d6b235c9053bec9c0bf9f",
    strip_prefix = "googletest-1.15.2",
    urls = ["https://github.com/google/googletest/archive/refs/tags/v1.15.2.zip"],
)

http_archive(
    name = "com_google_benchmark",
    sha256 = "8a63c9c6adf9e7ce8d0d81f251c47de83efb5e077e147d109fa2045daac8368b",
    strip_prefix = "benchmark-1.9.1",
    urls = ["https://github.com/google/benchmark/archive/refs/tags/v1.9.1.zip"],
)

http_archive(
    name = "rules_cc",
    sha256 = "e7c1639aa227d2cd335825d37caa2a234b40373be3ef8f87c25724ed01cab5e8",
    strip_prefix = "rules_cc-0.0.17",
    urls = ["https://github.com/bazelbuild/rules_cc/archive/refs/tags/0.0.17.zip"],
)

http_archive(
    name = "rules_python",
    sha256 = "7149fff45f7925bb6d45543ed99bfd3544ec63df82ef70cf0ce38b669c9d3bd6",
    strip_prefix = "rules_python-1.0.0",
    urls = ["https://github.com/bazelbuild/rules_python/archive/refs/tags/1.0.0.zip"],
)

http_archive(
    name = "bazel_skylib",
    sha256 = "23ef380aa62e2f1b631d02d0c9d163e43be03e880953dafe133d754fb8d96f0a",
    strip_prefix = "bazel-skylib-1.7.1",
    urls = ["https://github.com/bazelbuild/bazel-skylib/archive/refs/tags/1.7.1.zip"],
)

http_archive(
    name = "com_google_absl",
    sha256 = "95e90be7c3643e658670e0dd3c1b27092349c34b632c6e795686355f67eca89f",
    strip_prefix = "abseil-cpp-20240722.0",
    urls = ["https://github.com/abseil/abseil-cpp/archive/refs/tags/20240722.0.zip"],
)

http_archive(
    name = "com_google_absl_py",
    sha256 = "e11083ee5a69afe5c82321ec2505061407ec315789b9b886cbfaf46560431c0b",
    strip_prefix = "abseil-py-2.1.0",
    urls = ["https://github.com/abseil/abseil-py/archive/refs/tags/v2.1.0.zip"],
)

http_archive(
    name = "eigen_archive",
    build_file = "@//bazel:eigen.BUILD",
    sha256 = "8586084f71f9bde545ee7fa6d00288b264a2b7ac3607b974e54d13e7162c1c72",
    strip_prefix = "eigen-3.4.0",
    urls = [
        "https://mirror.bazel.build/gitlab.com/libeigen/eigen/-/archive/3.4.0/eigen-3.4.0.tar.gz",
        "https://gitlab.com/libeigen/eigen/-/archive/3.4.0/eigen-3.4.0.tar.gz",
    ],
)

http_archive(
    name = "png_archive",
    build_file = "@//bazel:png.BUILD",
    sha256 = "0b35b4bbdf454d589bf8195bc281fefecc4b2529b42ddfbe8b6c108b986841f9",
    strip_prefix = "libpng-1.6.44",
    urls = [
        "https://mirror.bazel.build/github.com/pnggroup/libpng/archive/v1.6.44.zip",
        "https://github.com/pnggroup/libpng/archive/refs/tags/v1.6.44.zip",
    ],
)

http_archive(
    name = "zlib_archive",
    build_file = "@//bazel:zlib.BUILD",
    sha256 = "9a93b2b7dfdac77ceba5a558a580e74667dd6fede4585b91eefb60f03b72df23",
    strip_prefix = "zlib-1.3.1",
    urls = [
        "https://mirror.bazel.build/zlib.net/zlib-1.3.1.tar.gz",
        "https://zlib.net/zlib-1.3.1.tar.gz",
    ],
)

http_archive(
    name = "lua5_1_archive",
    build_file = "@//bazel:lua5_1.BUILD",
    sha256 = "2640fc56a795f29d28ef15e13c34a47e223960b0240e8cb0a82d9b0738695333",
    strip_prefix = "lua-5.1.5/src",
    urls = [
        "https://mirror.bazel.build/www.lua.org/ftp/lua-5.1.5.tar.gz",
        "https://www.lua.org/ftp/lua-5.1.5.tar.gz",
    ],
)

http_archive(
    name = "lua5_2_archive",
    build_file = "@//bazel:lua5_2.BUILD",
    sha256 = "b9e2e4aad6789b3b63a056d442f7b39f0ecfca3ae0f1fc0ae4e9614401b69f4b",
    strip_prefix = "lua-5.2.4/src",
    urls = [
        "https://mirror.bazel.build/www.lua.org/ftp/lua-5.2.4.tar.gz",
        "https://www.lua.org/ftp/lua-5.2.4.tar.gz",
    ],
)

http_archive(
    name = "luajit_archive",
    build_file = "@//bazel:luajit.BUILD",
    sha256 = "4af5d94608a7ab72c9a7f72833a9222a7e0a298255e058902c4a59012c53bbfc",
    strip_prefix = "LuaJIT-f0ff869bc2fffa17bb765c4c773457578da125a9",
    urls = ["https://github.com/LuaJIT/LuaJIT/archive/f0ff869bc2fffa17bb765c4c773457578da125a9.tar.gz"],
)

http_archive(
    name = "dm_env_archive",
    build_file = "@//bazel:dm_env.BUILD",
    sha256 = "ed832e301bfddb6e98812567ee0217f6016c862357a0af2a94088ac6e6224af6",
    strip_prefix = "dm_env-ea2a17bed7a60c82f637891c53f3a37f70d91486",
    urls = ["https://github.com/deepmind/dm_env/archive/ea2a17bed7a60c82f637891c53f3a37f70d91486.zip"],
)

http_archive(
    name = "tree_archive",
    build_file = "@//bazel:tree.BUILD",
    sha256 = "407606263ee3f049da5c49071522cf5d37142c2de04ba52c9d599da948f4ee08",
    strip_prefix = "tree-0.1.8",
    urls = ["https://github.com/google-deepmind/tree/archive/refs/tags/0.1.8.zip"],
)

http_archive(
    name = "pybind11_archive",
    build_file = "@//bazel:pybind11.BUILD",
    sha256 = "d0a116e91f64a4a2d8fb7590c34242df92258a61ec644b79127951e821b47be6",
    strip_prefix = "pybind11-2.13.6",
    urls = ["https://github.com/pybind/pybind11/archive/refs/tags/v2.13.6.zip"],
)

http_archive(
    name = "build_bazel_apple_support",
    sha256 = "b53f6491e742549f13866628ddffcc75d1f3b2d6987dc4f14a16b242113c890b",
    urls = ["https://github.com/bazelbuild/apple_support/releases/download/1.17.1/apple_support.1.17.1.tar.gz"],
)

load("@build_bazel_apple_support//lib:repositories.bzl", "apple_support_dependencies")

apple_support_dependencies()

load("@bazel_features//:deps.bzl", "bazel_features_deps")

bazel_features_deps()

load("@rules_python//python:repositories.bzl", "py_repositories")

py_repositories()

load("@//:python_system.bzl", "python_repo")

python_repo(
    name = "python_system",
)

register_toolchains("@python_system//:python_toolchain")
