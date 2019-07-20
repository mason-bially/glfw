objc_library(
    name = "glfw_macos",
    visibility = ["//visibility:public"],
    srcs = glob(["src/*.m", "src/cocoa*", "src/*.h", "include/**/*.h"])+ glob([
        "src/posix_thread.c",
        "src/osmesa_*.c",
        "src/egl_*.c",
    ]),
    
    defines = ["_GLFW_COCOA"],
    copts=[
        "-fno-objc-arc"
    ],
    sdk_frameworks = [
        "Carbon",
        "CoreFoundation",
        "CoreVideo",
        "Cocoa",
        "OpenGL",
        "IOKit",
    ],
)

cc_library(
    name = "glfw",
    visibility = ["//visibility:public"],

    deps = select({
        "@bazel_tools//src/conditions:darwin_x86_64": ["glfw_macos"],
        "//conditions:default": [],
    }),

    srcs = [
        "src/context.c",
        "src/init.c",
        "src/input.c",
        "src/monitor.c",
        "src/vulkan.c",
        "src/window.c",
    ] + glob([
        "src/osmesa_*.c",
        "src/egl_*.c",
    ]) + select({
        "@bazel_tools//src/conditions:windows": glob(["src/win32_*.c", "src/wgl_*.c"]),
        "@bazel_tools//src/conditions:darwin_x86_64": glob([]),
        "//conditions:default": glob(["src/x11_*.c", "src/xkb_*.c", "src/glx_*.c", "src/linux_*.c", "src/posix_*.c"]),
    }),

    hdrs = glob(["src/*.h", "include/**/*.h"]),

    defines = [ ] + select({
        "@bazel_tools//src/conditions:windows": ["_GLFW_WIN32"],
        "@bazel_tools//src/conditions:darwin_x86_64": ["_GLFW_COCOA"],
        "//conditions:default": ["_GLFW_X11"],
    }),

    includes = [
        "include"
    ],

    copts = [] + select({
        "@bazel_tools//src/conditions:windows": [],
        "@bazel_tools//src/conditions:darwin": [
            #"-ObjC++",
        ],
        "//conditions:default": [],
    }),

    linkopts = [ ] + select({
        "@bazel_tools//src/conditions:windows": [
            "-DEFAULTLIB:user32.lib",
            "-DEFAULTLIB:shell32.lib",
            "-DEFAULTLIB:gdi32.lib",
        ],
        "@bazel_tools//src/conditions:darwin_x86_64": [
            #"-ObjC++",
            "-framework CoreFoundation",
            "-framework CoreVideo",
            "-framework Cocoa",
            "-framework IOKit",
        ],
        "//conditions:default": [
            "-ldl",
            "-lpthread",
            "-lX11",
        ],
    }),
)