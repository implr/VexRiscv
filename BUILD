package(default_visibility = ["//visibility:public"])
load("@io_bazel_rules_scala//scala:scala.bzl", "scala_binary", "scala_library")

scala_library(
        name = "VexRiscV",
        srcs = glob(
            ["src/main/scala/**/*.scala"],
            exclude = ["src/main/scala/demo/**/*"]
        ),
        #plugins = ["@spinal//idslplugin"],
        deps = [
            "@maven//:org_yaml_snakeyaml",
            "@maven//:commons_io_commons_io",
            "@io_bazel_rules_scala_scala_compiler//:io_bazel_rules_scala_scala_compiler",
            "@io_bazel_rules_scala_scala_library//:io_bazel_rules_scala_scala_library"
            ],
)

scala_binary(
        name = "test1",
        srcs = glob(["src/main/scala/vexriscv/demo/*.scala"]),
        main_class="vexriscv.demo.GenFull",
        plugins = ["@spinal//idslplugin"],
        deps = [
            ":VexRiscV",
        ],
)
