load("@io_bazel_rules_go//go:def.bzl", "go_library", "go_test")
load("@bazel_gazelle//:def.bzl", "gazelle")

# gazelle:prefix github.com/godror/godror
gazelle(name = "gazelle")

go_library(
    name = "godror",
    srcs = [
        "batch.go",
        "conn.go",
        "conn_go15.go",
        "data.go",
        "drv.go",
        "drv_linux.go",
        "json.go",
        "lob.go",
        "log.go",
        "num_go14.go",
        "num_go15.go",
        "number.go",
        "obj.go",
        "orahlp.go",
        "queue.go",
        "rows.go",
        "stmt.go",
        "subscr.c",
        "subscr.go",
        "tznames_generated.go",
        "version.go",
    ],
    cdeps = [":odpi"],
    cgo = True,
    clinkopts = select({
        "@io_bazel_rules_go//go/platform:android": [
            "-ldl -lpthread",
        ],
        "@io_bazel_rules_go//go/platform:linux": [
            "-ldl -lpthread",
        ],
        "//conditions:default": [],
    }),
    copts = ["-Iodpi/include -Iodpi/src -Iodpi/embed"],
    importpath = "github.com/godror/godror",
    visibility = ["//visibility:public"],
    deps = [
        "//dsn",
        "@com_github_go_logfmt_logfmt//:logfmt",
        "@com_github_godror_knownpb//timestamppb",
    ],
)

go_test(
    name = "godror_test",
    srcs = [
        "conn_test.go",
        "data_test.go",
        "drv_test.go",
        "example_shutdown_test.go",
        "number_test.go",
        "orahlp_test.go",
        "queue_test.go",
        "z_119_test.go",
        "z_batch_test.go",
        "z_bench_113_test.go",
        "z_bench_test.go",
        "z_conc_test.go",
        "z_conncut_test.go",
        "z_heterogeneous_test.go",
        "z_issue133_test.go",
        "z_json_test.go",
        "z_lob_test.go",
        "z_plsql_types_test.go",
        "z_qrcn_test.go",
        "z_test.go",
    ],
    embed = [":godror"],
    deps = [
        "//dsn",
        "@com_github_go_logfmt_logfmt//:logfmt",
        "@com_github_google_go_cmp//cmp",
        "@com_github_oklog_ulid_v2//:ulid",
        "@org_golang_x_sync//errgroup",
    ],
)

gazelle(
    name = "gazelle-update-repos",
    args = [
        "-from_file=go.mod",
        "-to_macro=deps.bzl%go_dependencies",
        "-prune",
    ],
    command = "update-repos",
)

cc_library(
    name = "odpi",
    srcs = [
        "odpi/src/dpiConn.c",
        "odpi/src/dpiContext.c",
        "odpi/src/dpiData.c",
        "odpi/src/dpiDebug.c",
        "odpi/src/dpiDeqOptions.c",
        "odpi/src/dpiEnqOptions.c",
        "odpi/src/dpiEnv.c",
        "odpi/src/dpiError.c",
        "odpi/src/dpiGen.c",
        "odpi/src/dpiGlobal.c",
        "odpi/src/dpiHandleList.c",
        "odpi/src/dpiHandlePool.c",
        "odpi/src/dpiJson.c",
        "odpi/src/dpiLob.c",
        "odpi/src/dpiMsgProps.c",
        "odpi/src/dpiObject.c",
        "odpi/src/dpiObjectAttr.c",
        "odpi/src/dpiObjectType.c",
        "odpi/src/dpiOci.c",
        "odpi/src/dpiOracleType.c",
        "odpi/src/dpiPool.c",
        "odpi/src/dpiQueue.c",
        "odpi/src/dpiRowid.c",
        "odpi/src/dpiSodaColl.c",
        "odpi/src/dpiSodaCollCursor.c",
        "odpi/src/dpiSodaDb.c",
        "odpi/src/dpiSodaDoc.c",
        "odpi/src/dpiSodaDocCursor.c",
        "odpi/src/dpiStmt.c",
        "odpi/src/dpiSubscr.c",
        "odpi/src/dpiUtils.c",
        "odpi/src/dpiVar.c",
    ],
    hdrs = [
        "odpi/include/dpi.h",
        "odpi/src/dpiErrorMessages.h",
        "odpi/src/dpiImpl.h",
    ],
    includes = [
        "odpi/include",
        "odpi/src",
    ],
)
