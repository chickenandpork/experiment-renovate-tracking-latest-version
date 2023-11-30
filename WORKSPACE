# Declare the local Bazel workspace.
# This is *not* included in the published distribution.
workspace(
    name = "rules_jq",
)

load(":internal_deps.bzl", "rules_jq_internal_deps")

# Fetch deps needed only locally for development
rules_jq_internal_deps()

load("//jq:repositories.bzl", "jq_register_toolchains", "rules_jq_dependencies")

# Fetch our "runtime" dependencies which users need as well
rules_jq_dependencies()

jq_register_toolchains(
    name = "jq",
    jq_version = "1.7",
)

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")

############################################
# Gazelle, for generating bzl_library targets
load("@io_bazel_rules_go//go:deps.bzl", "go_download_sdk", "go_register_toolchains", "go_rules_dependencies")

# We give the SDK keys and SHA256s to reduce the delay during Analysis to hit a remote server and
# dynamically choose from its responses.  Also avoids impact of sunset versions disappearing from
# the live query we're processing.
go_download_sdk(
    name = "go_sdk",
    sdks = {
        # NOTE: In most cases the whole sdks attribute is not needed.
        # There are 2 "common" reasons you might want it:
        #
        # 1. You need to use an modified GO SDK, or an unsupported version
        #    (for example, a beta or release candidate)
        #
        # 2. You want to avoid the dependency on the index file for the
        #    SHA-256 checksums. In this case, You can get the expected
        #    filenames and checksums from https://go.dev/dl/
        "linux_amd64": ("go1.19.5.linux-amd64.tar.gz", "36519702ae2fd573c9869461990ae550c8c0d955cd28d2827a6b159fda81ff95"),
        "darwin_amd64": ("go1.19.5.darwin-amd64.tar.gz", "23d22bb6571bbd60197bee8aaa10e702f9802786c2e2ddce5c84527e86b66aa0"),
        "darwin_arm64": ("go1.19.5.darwin-arm64.tar.gz", "4a67f2bf0601afe2177eb58f825adf83509511d77ab79174db0712dc9efa16c8"),
    },
    #goos = "linux",
    #goarch = "amd64",
    version = "1.19.5",
)

go_rules_dependencies()

go_register_toolchains()

gazelle_dependencies()
