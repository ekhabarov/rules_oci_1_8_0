load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "rules_oci",
    # v1.8.0 Failed with
    # ERROR: credential helper failed:
    # STDOUT:
    # credentials not found in native keychain
    sha256 = "46ce9edcff4d3d7b3a550774b82396c0fa619cc9ce9da00c1b09a08b45ea5a14",
    strip_prefix = "rules_oci-1.8.0",
    url = "https://github.com/bazel-contrib/rules_oci/releases/download/v1.8.0/rules_oci-v1.8.0.tar.gz",

    # Works with v1.7.6
    # sha256 = "647f4c6fd092dc7a86a7f79892d4b1b7f1de288bdb4829ca38f74fd430fcd2fe",
    # strip_prefix = "rules_oci-1.7.6",
    # url = "https://github.com/bazel-contrib/rules_oci/releases/download/v1.7.6/rules_oci-v1.7.6.tar.gz",
)

load("@rules_oci//oci:dependencies.bzl", "rules_oci_dependencies")

rules_oci_dependencies()

load("@rules_oci//oci:repositories.bzl", "LATEST_CRANE_VERSION", "oci_register_toolchains")

oci_register_toolchains(
    name = "oci",
    crane_version = LATEST_CRANE_VERSION,
    # Uncommenting the zot toolchain will cause it to be used instead of crane for some tasks.
    # Note that it does not support docker-format images.
    # zot_version = LATEST_ZOT_VERSION,
)

# You can pull your base images using oci_pull like this:
load("@rules_oci//oci:pull.bzl", "oci_pull")

oci_pull(
    name = "distroless_base",
    digest = "sha256:ccaef5ee2f1850270d453fdf700a5392534f8d1a8ca2acda391fbb6a06b81c86",
    image = "gcr.io/distroless/base",
    platforms = [
        "linux/amd64",
        "linux/arm64",
    ],
)
