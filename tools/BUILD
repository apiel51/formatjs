load("@aspect_bazel_lib//lib:copy_to_bin.bzl", "copy_to_bin")
load("@aspect_rules_js//js:defs.bzl", "js_binary")
load("@aspect_rules_ts//ts:defs.bzl", "ts_project")

exports_files([
    "tsconfig.golden.json",
    "supported-locales-gen.ts",
])

copy_to_bin(
    name = "check-package-json",
    srcs = ["check-package-json.ts"],
    visibility = ["//visibility:public"],
)

copy_to_bin(
    name = "supported-locales-gen",
    srcs = ["supported-locales-gen.ts"],
    visibility = ["//visibility:public"],
)

ts_project(
    name = "supported-locales-gen-transpiled",
    srcs = ["supported-locales-gen.ts"],
    declaration = True,
    resolve_json_module = True,
    tsconfig = "//:tsconfig.node",
    deps = [
        "//:node_modules/@types/fs-extra",
        "//:node_modules/@types/json-stable-stringify",
        "//:node_modules/@types/minimist",
        "//:node_modules/@types/node",
        "//:node_modules/fast-glob",
        "//:node_modules/fs-extra",
        "//:node_modules/json-stable-stringify",
        "//:node_modules/minimist",
        "//:node_modules/tslib",
    ],
)

js_binary(
    name = "generate_supported_locales",
    data = [
        ":supported-locales-gen-transpiled",
        "//:node_modules/@types/fs-extra",
        "//:node_modules/@types/json-stable-stringify",
        "//:node_modules/@types/minimist",
        "//:node_modules/@types/node",
        "//:node_modules/fast-glob",
        "//:node_modules/fs-extra",
        "//:node_modules/json-stable-stringify",
        "//:node_modules/minimist",
        "//:node_modules/tslib",
    ],
    entry_point = ":supported-locales-gen-transpiled",
    visibility = ["//visibility:public"],
)
