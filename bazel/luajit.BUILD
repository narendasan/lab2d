# Description:
#   Build rule for LuaJit.

load("@bazel_skylib//rules:common_settings.bzl", "bool_flag", "string_flag")

string_flag(
    name = "target_arch",
    build_setting_default = "x86_64",
    values = [
        "arm64",
        "x86_64",
    ],
)

config_setting(
    name = "target_arch_arm64",
    flag_values = {"target_arch": "arm64"},
)

config_setting(
    name = "target_arch_x86_64",
    flag_values = {"target_arch": "x86_64"},
)

bool_flag(
    name = "use_external_unwinder",
    build_setting_default = True,
)

config_setting(
    name = "external_unwinder",
    flag_values = {"use_external_unwinder": "True"},
)

UNWINDER_DEFINES = select({
    ":external_unwinder": ["LUAJIT_UNWIND_EXTERNAL"],
    "//conditions:default": ["LUAJIT_NO_UNWIND"],
})

DEFINES = [
    "LJ_ARCH_HASFPU=1",
    "LJ_ABI_SOFTFP=0",
    "LUAJIT_ENABLE_GC64",
] + UNWINDER_DEFINES + select(
    {
        ":target_arch_arm64": ["LUAJIT_TARGET=LUAJIT_ARCH_arm64"],
        "@platforms//cpu:x86_64": ["LUAJIT_TARGET=LUAJIT_ARCH_x64"],
        "@platforms//cpu:aarch64": ["LUAJIT_TARGET=LUAJIT_ARCH_arm64"],
        "@build_bazel_apple_support//configs:darwin_arm64": ["LUAJIT_TARGET=LUAJIT_ARCH_arm64"],
    },
)

# This linker flag is needed only when using the gold linker: that linker does
# not correctly retain the symbol "lj_err_unwind_dwarf" when --gc-sections is
# used, and we need to request explicitly that that symbol be retained. Neither
# LLD nor LD64 have this problem, but the flag also does not hurt those linkers.
cc_library(
    name = "personality_linkopts",
    linkopts = select({
        "@platforms//os:linux": ["-ulj_err_unwind_dwarf"],
        "@platforms//os:macos": ["-u_lj_err_unwind_dwarf"],
        "//conditions:default": [],
    }),
)

cc_library(
    name = "luajit",
    srcs = [
        "src/lauxlib.h",
        "src/lib_aux.c",
        "src/lib_base.c",
        "src/lib_bit.c",
        "src/lib_buffer.c",
        "src/lib_debug.c",
        "src/lib_ffi.c",
        "src/lib_init.c",
        "src/lib_io.c",
        "src/lib_jit.c",
        "src/lib_math.c",
        "src/lib_os.c",
        "src/lib_package.c",
        "src/lib_string.c",
        "src/lib_table.c",
        "src/lj_alloc.c",
        "src/lj_alloc.h",
        "src/lj_api.c",
        "src/lj_arch.h",
        "src/lj_asm.c",
        "src/lj_asm.h",
        "src/lj_asm_arm.h",
        "src/lj_asm_arm64.h",
        "src/lj_asm_ppc.h",
        "src/lj_asm_x86.h",
        "src/lj_assert.c",
        "src/lj_bc.c",
        "src/lj_bc.h",
        "src/lj_bcdump.h",
        "src/lj_bcread.c",
        "src/lj_bcwrite.c",
        "src/lj_buf.c",
        "src/lj_buf.h",
        "src/lj_carith.c",
        "src/lj_carith.h",
        "src/lj_ccall.c",
        "src/lj_ccall.h",
        "src/lj_ccallback.c",
        "src/lj_ccallback.h",
        "src/lj_cconv.c",
        "src/lj_cconv.h",
        "src/lj_cdata.c",
        "src/lj_cdata.h",
        "src/lj_char.c",
        "src/lj_char.h",
        "src/lj_clib.c",
        "src/lj_clib.h",
        "src/lj_cparse.c",
        "src/lj_cparse.h",
        "src/lj_crecord.c",
        "src/lj_crecord.h",
        "src/lj_ctype.c",
        "src/lj_ctype.h",
        "src/lj_debug.c",
        "src/lj_debug.h",
        "src/lj_def.h",
        "src/lj_dispatch.c",
        "src/lj_dispatch.h",
        "src/lj_emit_arm.h",
        "src/lj_emit_arm64.h",
        "src/lj_emit_ppc.h",
        "src/lj_emit_x86.h",
        "src/lj_err.c",
        "src/lj_err.h",
        "src/lj_errmsg.h",
        "src/lj_ff.h",
        "src/lj_ffrecord.c",
        "src/lj_ffrecord.h",
        "src/lj_frame.h",
        "src/lj_func.c",
        "src/lj_func.h",
        "src/lj_gc.c",
        "src/lj_gc.h",
        "src/lj_gdbjit.c",
        "src/lj_gdbjit.h",
        "src/lj_ir.c",
        "src/lj_ir.h",
        "src/lj_ircall.h",
        "src/lj_iropt.h",
        "src/lj_jit.h",
        "src/lj_lex.c",
        "src/lj_lex.h",
        "src/lj_lib.c",
        "src/lj_lib.h",
        "src/lj_load.c",
        "src/lj_mcode.c",
        "src/lj_mcode.h",
        "src/lj_meta.c",
        "src/lj_meta.h",
        "src/lj_obj.c",
        "src/lj_obj.h",
        "src/lj_opt_dce.c",
        "src/lj_opt_fold.c",
        "src/lj_opt_loop.c",
        "src/lj_opt_mem.c",
        "src/lj_opt_narrow.c",
        "src/lj_opt_sink.c",
        "src/lj_opt_split.c",
        "src/lj_parse.c",
        "src/lj_parse.h",
        "src/lj_profile.c",
        "src/lj_profile.h",
        "src/lj_prng.c",
        "src/lj_prng.h",
        "src/lj_record.c",
        "src/lj_record.h",
        "src/lj_serialize.c",
        "src/lj_serialize.h",
        "src/lj_snap.c",
        "src/lj_snap.h",
        "src/lj_state.c",
        "src/lj_state.h",
        "src/lj_str.c",
        "src/lj_str.h",
        "src/lj_strfmt.c",
        "src/lj_strfmt.h",
        "src/lj_strfmt_num.c",
        "src/lj_strscan.c",
        "src/lj_strscan.h",
        "src/lj_tab.c",
        "src/lj_tab.h",
        "src/lj_target.h",
        "src/lj_target_arm.h",
        "src/lj_target_arm64.h",
        "src/lj_target_ppc.h",
        "src/lj_target_x86.h",
        "src/lj_trace.c",
        "src/lj_trace.h",
        "src/lj_traceerr.h",
        "src/lj_udata.c",
        "src/lj_udata.h",
        "src/lj_vm.h",
        "src/lj_vmevent.c",
        "src/lj_vmevent.h",
        "src/lj_vmmath.c",
        "src/lua.h",
        "src/luaconf.h",
        "src/luajit.h",
        "src/lualib.h",

        # Generated files.
        "src/lj_bcdef.h",
        "src/lj_ffdef.h",
        "src/lj_folddef.h",
        "src/lj_libdef.h",
        "src/lj_recdef.h",
        "lj_vm.S",
    ],
    hdrs = [
        "src/lauxlib.h",
        "src/lj_arch.h",
        "src/lua.h",
        "src/lua.hpp",
        "src/luaconf.h",
        "src/lualib.h",

        # Generated files.
        "src/luajit.h",
    ],
    defines = UNWINDER_DEFINES,
    includes = ["src"],
    linkopts = ["-ldl"],
    visibility = ["//visibility:public"],
    deps = select({
        ":external_unwinder": [":personality_linkopts"],
        "//conditions:default": [],
    }),
)

cc_binary(
    name = "minilua",
    srcs = ["src/host/minilua.c"],
    copts = [
        "-O2",
        "-fomit-frame-pointer",
        "-Wall",
    ],
    local_defines = DEFINES,
)

DYNASM_FLAGS_ARM64 = " -D ENDIAN_LE -D P64 -D JIT -D FFI -D DUALNUM -D FPU -D HFABI -D VER=80"

DYNASM_FLAGS_X86_64 = " -D ENDIAN_LE -D P64 -D JIT -D FFI -D FPU -D HFABI -D VER="

DYNASM_FLAGS_ARCH = select({
    ":target_arch_arm64": DYNASM_FLAGS_ARM64,
    "@platforms//cpu:x86_64": DYNASM_FLAGS_X86_64,
    "@platforms//cpu:aarch64": DYNASM_FLAGS_ARM64,
    "@build_bazel_apple_support//configs:darwin_arm64": DYNASM_FLAGS_ARM64,
})

DYNASM_SOURCE = select({
    ":target_arch_arm64": "vm_arm64.dasc",
    "@platforms//cpu:x86_64": "vm_x64.dasc",
    "@platforms//cpu:aarch64": "vm_arm64.dasc",
    "@build_bazel_apple_support//configs:darwin_arm64": "vm_arm64.dasc",
})

DYNASM_FLAGS_UNWIND = select({
    ":external_unwinder": "",
    "//conditions:default": " -D NO_UNWIND",
})

genrule(
    name = "buildvm_archconf",
    srcs = glob([
        "dynasm/*.lua",
        "src/vm_*.dasc",
    ]),
    outs = ["src/host/buildvm_arch.h"],
    cmd = "$(location :minilua) $(location dynasm/dynasm.lua)" + DYNASM_FLAGS_ARCH + DYNASM_FLAGS_UNWIND + " -o $@ $(location :src/" + DYNASM_SOURCE + ")",
    tools = [":minilua"],
)

genrule(
    name = "luajit_h",
    srcs = glob([
        "src/luajit_rolling.h",
        "src/host/genversion.lua",
        ".relver"
    ]),
    outs = ["src/luajit.h"],
    cmd = "$(location :minilua) $(location src/host/genversion.lua) $(location src/luajit_rolling.h) $(location .relver) $(location src/luajit.h)",
    tools = [":minilua"],
)

cc_binary(
    name = "buildvm",
    srcs = [
        "dynasm/dasm_arm64.h",
        "dynasm/dasm_proto.h",
        "dynasm/dasm_x86.h",
        "src/host/buildvm.c",
        "src/host/buildvm.h",
        "src/host/buildvm_arch.h",
        "src/host/buildvm_asm.c",
        "src/host/buildvm_fold.c",
        "src/host/buildvm_lib.c",
        "src/host/buildvm_libbc.h",
        "src/host/buildvm_peobj.c",
        "src/lj_arch.h",
        "src/lj_bc.h",
        "src/lj_ccall.h",
        "src/lj_ctype.h",
        "src/lj_def.h",
        "src/lj_dispatch.h",
        "src/lj_frame.h",
        "src/lj_gc.h",
        "src/lj_ir.h",
        "src/lj_ircall.h",
        "src/lj_jit.h",
        "src/lj_lib.h",
        "src/lj_obj.h",
        "src/lj_traceerr.h",
        "src/lua.h",
        "src/luaconf.h",
        "src/luajit.h",
    ],
    includes = [
        "src",
        "src/host",
    ],
    local_defines = DEFINES,
)

genrule(
    name = "lj_vm",
    outs = ["lj_vm.S"],
    cmd = select(
        {
            "@platforms//os:linux": "$(location :buildvm) -m elfasm -o $@",
            "@platforms//os:macos": "$(location :buildvm) -m machasm -o $@",
        },
        no_match_error = "Must build for either Linux or MacOS",
    ),
    tools = [":buildvm"],
    visibility = ["//visibility:public"],
)

LJ_LIB_SRCS = [
    "src/lib_base.c",
    "src/lib_math.c",
    "src/lib_bit.c",
    "src/lib_string.c",
    "src/lib_table.c",
    "src/lib_io.c",
    "src/lib_os.c",
    "src/lib_package.c",
    "src/lib_debug.c",
    "src/lib_jit.c",
    "src/lib_ffi.c",
    "src/lib_buffer.c",
]

genrule(
    name = "lj_ffdef",
    srcs = LJ_LIB_SRCS,
    outs = ["src/lj_ffdef.h"],
    cmd = "$(location :buildvm) -m ffdef -o $@ $(SRCS)",
    tools = [":buildvm"],
)

genrule(
    name = "lj_bcdef",
    srcs = LJ_LIB_SRCS,
    outs = ["src/lj_bcdef.h"],
    cmd = "$(location :buildvm) -m bcdef -o $@ $(SRCS)",
    tools = [":buildvm"],
)

genrule(
    name = "lj_recdef",
    srcs = LJ_LIB_SRCS,
    outs = ["src/lj_recdef.h"],
    cmd = "$(location :buildvm) -m recdef -o $@ $(SRCS)",
    tools = [":buildvm"],
)

genrule(
    name = "lj_libdef",
    srcs = LJ_LIB_SRCS,
    outs = ["src/lj_libdef.h"],
    cmd = "$(location :buildvm) -m libdef -o $@ $(SRCS)",
    tools = [":buildvm"],
)

genrule(
    name = "lj_folddef",
    srcs = ["src/lj_opt_fold.c"],
    outs = ["src/lj_folddef.h"],
    cmd = "$(location :buildvm) -m folddef -o $@ $(SRCS)",
    tools = [":buildvm"],
)

genrule(
    name = "vmdef",
    srcs = LJ_LIB_SRCS,
    outs = ["src/jit/vmdef.lua"],
    cmd = "$(location :buildvm) -m vmdef -o $@ $(SRCS)",
    tools = [":buildvm"],
)

filegroup(
    name = "jit_fs",
    srcs = ["src/jit/{}".format(s) for s in [
        "bc.lua",
        "bcsave.lua",
        "dis_arm.lua",
        "dis_arm64.lua",
        "dis_mips.lua",
        "dis_mipsel.lua",
        "dis_ppc.lua",
        "dis_x64.lua",
        "dis_x86.lua",
        "dump.lua",
        "v.lua",
        "vmdef.lua",
    ]],
    visibility = ["//visibility:public"],
)
