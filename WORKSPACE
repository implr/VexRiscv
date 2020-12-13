workspace(name = "vexriscv")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("@bazel_tools//tools/build_defs/repo:git.bzl","git_repository")

skylib_version = "1.0.3"
http_archive(
    name = "bazel_skylib",
    type = "tar.gz",
    url = "https://github.com/bazelbuild/bazel-skylib/releases/download/{}/bazel-skylib-{}.tar.gz".format (skylib_version, skylib_version),
    sha256 = "1c531376ac7e5a180e0237938a2536de0c54d93f5c278634818e0efc952dd56c",
)
load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")
bazel_skylib_workspace()

protobuf_version="3.12.2"
protobuf_version_sha256="bb8ce9ba11eb7bccf080599fe7cad9cc461751c8dd1ba61701c0070d58cde973"

http_archive(
    name = "com_google_protobuf",
    url = "https://github.com/protocolbuffers/protobuf/archive/v%s.tar.gz" % protobuf_version,
    strip_prefix = "protobuf-%s" % protobuf_version,
    sha256 = protobuf_version_sha256,
)
load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")
protobuf_deps()


rules_scala_version="67a7ac178a73d1d5ff4c2b0663a8eda6dfcbbc56"
rules_scala_version_sha256="95054009fd938ac7ef53a20619f94a5408d8ae74eb5b318cd150a3ecb1a6086f"

http_archive(
    name = "io_bazel_rules_scala",
    strip_prefix = "rules_scala-%s" % rules_scala_version,
    type = "zip",
    url = "https://github.com/bazelbuild/rules_scala/archive/%s.zip" % rules_scala_version,
    sha256 = rules_scala_version_sha256,
)

load("@io_bazel_rules_scala//:scala_config.bzl", "scala_config")
scala_config(scala_version = "2.11.12")

load("@io_bazel_rules_scala//scala:scala.bzl", "scala_repositories")
scala_repositories((
    "2.11.12",
    {
        "scala_compiler": "3e892546b72ab547cb77de4d840bcfd05c853e73390fed7370a8f19acb0735a0",
        "scala_library": "0b3d6fd42958ee98715ba2ec5fe221f4ca1e694d7c981b0ae0cd68e97baf6dce",
        "scala_reflect": "6ba385b450a6311a15c918cf8688b9af9327c6104f0ecbd35933cfcd3095fe04",
    }
))

load("@io_bazel_rules_scala//scala:toolchains.bzl", "scala_register_toolchains")
scala_register_toolchains()

RULES_JVM_EXTERNAL_TAG = "3.0"
RULES_JVM_EXTERNAL_SHA = "62133c125bf4109dfd9d2af64830208356ce4ef8b165a6ef15bbff7460b35c3a"

http_archive(
    name = "rules_jvm_external",
    strip_prefix = "rules_jvm_external-%s" % RULES_JVM_EXTERNAL_TAG,
    sha256 = RULES_JVM_EXTERNAL_SHA,
    url = "https://github.com/bazelbuild/rules_jvm_external/archive/%s.zip" % RULES_JVM_EXTERNAL_TAG,
)

load("@rules_jvm_external//:defs.bzl", "maven_install")

#load("@io_bazel_rules_scala//testing:scalatest.bzl", "scalatest_repositories", "scalatest_toolchain")
#scalatest_repositories()
#register_toolchains("@io_bazel_rules_scala//testing:testing_toolchain")
local_repository(
        name = "spinal",
        path = "/home/implr/dev/SpinalHDL",
)

#spinalVersion = "1.4.0"
maven_install(
    artifacts = [
            "commons-io:commons-io:2.5",
            "org.yaml:snakeyaml:1.8",
            "com.github.oshi:oshi-core:3.4.0",
            "net.openhft:affinity:3.1.11",
            "org.slf4j:slf4j-simple:1.7.25",
            "com.github.scopt:scopt_2.11:3.4.0",
            "net.liftweb:lift-json_2.11:3.1.0-M2",
            "com.github.purejavacomm:purejavacomm:1.0.2.RELEASE",
        ],
    repositories = [
        "https://maven.google.com",
        "https://repo1.maven.org/maven2/",
        "https://oss.sonatype.org/content/repositories/snapshots",
        ],
    #maven_install_json = "//:maven_install.json",
    excluded_artifacts = [
        "com.github.dblock:oshi-core",
    ],
    override_targets = {
        "org.scala-lang:scala-library": "@io_bazel_rules_scala_scala_library//:io_bazel_rules_scala_scala_library",
        "org.scala-lang:scala-reflect": "@io_bazel_rules_scala_scala_reflect//:io_bazel_rules_scala_scala_reflect",
        "org.scala-lang:scala-compiler": "@io_bazel_rules_scala_scala_compiler//:io_bazel_rules_scala_scala_compiler",
        "org.scala-lang.modules:scala-parser-combinators": "@io_bazel_rules_scala_scala_parser_combinators//:io_bazel_rules_scala_scala_parser_combinators",
        "org.scala-lang.modules:scala-xml": "@io_bazel_rules_scala_scala_xml//:io_bazel_rules_scala_scala_xml",
    },
)

load("@maven//:defs.bzl", "pinned_maven_install")
pinned_maven_install()
