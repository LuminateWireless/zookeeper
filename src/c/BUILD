licenses(["unencumbered"])  # Apache 2.0

genrule(
  name = "generate_jute_c",
  tools = [
    "//third_party/zookeeper/src/java:jute"
  ],
  srcs = [
    "//third_party/zookeeper:src/zookeeper.jute"
  ],
  cmd = "TOP=$$PWD; cd $(@D)/generated; $$TOP/$(location //third_party/zookeeper/src/java:jute) -l c $$TOP/$<",
  outs = [
    "generated/zookeeper.jute.h",
    "generated/zookeeper.jute.c",
  ],
)

cc_library(
  name = "zookeeper_mt",
  visibility = ["//visibility:public"],
  nocopts = "-Wall",
  copts = [
    "-DHAVE_CONFIG_H",
    "-DTHREADED",
    "-D_GNU_SOURCE",
    "-I./third_party/zookeeper/src/c/build-x64",
    "-I./third_party/zookeeper/src/c/src",
  ],
  hdrs = [
    "include/proto.h",
    "include/recordio.h",
    "include/zookeeper.h",
    "include/zookeeper_log.h",
    "include/zookeeper_version.h",
    "src/zk_hashtable.h",
  ],
  includes = [
    "generated",
    "include",
  ],
  srcs = [
    ":generate_jute_c",
    "src/hashtable/hashtable.c",
    "src/hashtable/hashtable_itr.c",
    "src/mt_adaptor.c",
    "src/recordio.c",
    "src/zk_hashtable.c",
    "src/zk_log.c",
    "src/zookeeper.c",
    "src/addrvec.c",
    # Private headers
    "build-x64/config.h",
    "src/hashtable/hashtable.h",
    "src/hashtable/hashtable_private.h",
    "src/hashtable/hashtable_itr.h",
    "src/addrvec.h",
    "src/zk_adaptor.h",
  ],
  deps = [
    "//third_party/google/base:dynamic_annotations",
  ]
)

cc_binary(
  name = "cli_mt",
  copts = [
    "-DTHREADED"
  ],
  srcs = [
    "src/cli.c"
  ],
  deps = [
    ":zookeeper_mt"
  ]
)
