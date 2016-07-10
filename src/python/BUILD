package(default_visibility = ["//visibility:public"])

licenses(["notice"])  # Apache 2.0

exports_files([
    "LICENSE",
])

LINK_OPTS = [ "-lgflags", "-lglog", "-lprotobuf", "-pthread", "-ltcmalloc_minimal", "-lm" ]

cc_library(
   name = "gbdt_py_base",
   srcs = [ "gbdt_py_base.cc" ],
   hdrs = [ "gbdt_py_base.h" ],
   deps = [
       "//external:pybind11-lib",
       "//src/utils:status",
   ],
   copts = [ "-I/usr/include/python2.7" ],
)

cc_library(
   name = "gbdt_py",
   srcs = [ "gbdt_py.cc" ],
   deps = [
       "//external:pybind11-lib",
       "//src/utils:status",
       ":datastore_py",
       ":gbdt_py_base",
   ],
   copts = [ "-I/usr/include/python2.7" ],
)


cc_library(
   name = "datastore_py",
   srcs = [ "datastore_py.cc" ],
   hdrs = [ "datastore_py.h" ],
   deps = [
       "//external:pybind11-lib",
       "//src/data_store:data_store",
       "//src/data_store:tsv_data_store",
       "//src/proto:config_proto_cc",
       ":gbdt_py_base",
   ],
   copts = [ "-I/usr/include/python2.7",  ],
)

cc_binary(
   name = "gbdt.so",
   linkstatic = 1,
   linkshared = 1,
   deps = [ ":gbdt_py" ],
   linkopts = LINK_OPTS,
)