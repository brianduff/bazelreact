load("@npm//:defs.bzl", "npm_link_all_packages")
load("@aspect_bazel_lib//lib:copy_to_bin.bzl", "copy_to_bin")
load("@npm//frontend:vite/package_json.bzl", vite_bin = "bin")

# This macro expands to a link_npm_package for each third-party package in package.json
npm_link_all_packages(name = "node_modules")

CONFIGS = [
    "vite.config.ts",
    "package.json",
    "tsconfig.json",
    "tsconfig.node.json",
    "index.html",
]

BUILD_DEPS = [":node_modules/" + d for d in [
    "@vitejs/plugin-react-swc",
    "vite",
    "react",
    "react-dom",
]]

copy_to_bin(
    name = "vite_srcs_export",
    srcs = glob([
        "src/**/*.css",
        "src/**/*.svg",
        "src/**/*.ts",
        "src/**/*.tsx",
        "utils/**/*.ts",
        "utils/**/*.tsx",
        "public/**/*.svg",
    ]),
)

vite_bin.vite(
    name = "vite",
    srcs = BUILD_DEPS + CONFIGS + [":vite_srcs_export"],
    args = ["build"],
    chdir = package_name(),
    out_dirs = ["dist"],
)
