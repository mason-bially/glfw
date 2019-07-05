
cc_library(
    name = "glfw",
    visibility = ["//visibility:public"],

    srcs = [
        "src/context.c",
        "src/init.c",
        "src/input.c",
        "src/monitor.c",
        "src/vulkan.c",
        "src/window.c",
    ] + select({
        "@bazel_tools//src/conditions:windows": glob(["src/win32_*.c", "src/wgl_*.c", "src/egl_*.c", "src/osmesa_*.c"]),
        "//conditions:default": [],
    }),

    hdrs = glob(["src/*.h"]),

    defines = [ ] + select({
        "@bazel_tools//src/conditions:windows": ["_GLFW_WIN32"],
        "//conditions:default": [],
    }),

    includes = [
        "include"
    ],

    linkopts = [ ] + select({
        "@bazel_tools//src/conditions:windows": [
            "-DEFAULTLIB:user32.lib",
            "-DEFAULTLIB:shell32.lib",
            "-DEFAULTLIB:gdi32.lib"
        ],
        "//conditions:default": [],
    }),
)
