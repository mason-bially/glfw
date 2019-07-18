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
    ] + glob([
        "src/egl_*.c",
        "src/osmesa_*.c"
    ]) + select({
        "@bazel_tools//src/conditions:windows": glob(["src/win32_*.c", "src/wgl_*.c"]),
        "@bazel_tools//src/conditions:darwin": glob(["src/cocoa*.c"]),
        "//conditions:default": glob(["src/x11_*.c", "src/xkb_*.c", "src/glx_*.c", "src/linux_*.c", "src/posix_*.c"]),
    }),

    hdrs = glob(["src/*.h", "include/**/*.h"]),

    defines = [ ] + select({
        "@bazel_tools//src/conditions:windows": ["_GLFW_WIN32"],
        "@bazel_tools//src/conditions:darwin": ["_GLFW_COCOA"],
        "//conditions:default": ["_GLFW_X11"],
    }),

    includes = [
        "include"
    ],

    linkopts = [ ] + select({
        "@bazel_tools//src/conditions:windows": [
            "-DEFAULTLIB:user32.lib",
            "-DEFAULTLIB:shell32.lib",
            "-DEFAULTLIB:gdi32.lib",
        ],
        "@bazel_tools//src/conditions:darwin": [
            
        ],
        "//conditions:default": [
            "-ldl",
            "-lpthread",
            "-lX11",
        ],
    }),
)