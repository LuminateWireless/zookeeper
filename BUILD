# Top level bazel(http://bazel.io) BUILD file to zookeeper
# It's expected to be placed under third_party/zookeeper
licenses(["unencumbered"])  # Apache 2.0

exports_files([
  "src/zookeeper.jute"
])

filegroup(
  name = "log4j_config",
  visibility = ["//visibility:public"],
  srcs = [
    "conf/log4j.properties",
  ]
)

java_binary(
  name = "zookeeper_server",
  visibility = ["//visibility:public"],
  main_class = "org.apache.zookeeper.server.quorum.QuorumPeerMain",
  classpath_resources = [
    ":log4j_config",
  ],
  runtime_deps = [
    "//third_party/zookeeper/src/java:zookeeper",
  ],
)
