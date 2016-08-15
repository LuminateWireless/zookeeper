licenses(["unencumbered"])  # Apache 2.0

# jute compiler
genrule(
  name = "javacc_rcc",
  srcs = [
    "main/org/apache/jute/compiler/generated/rcc.jj",
  ],
  tools = [
    "//third_party/java/javacc:javacc",
  ],
  cmd = "$(location //third_party/java/javacc:javacc) -OUTPUT_DIRECTORY=$(@D)/rcc_java $<",
  outs = [
    "rcc_java/ParseException.java",
    "rcc_java/RccConstants.java",
    "rcc_java/Rcc.java",
    "rcc_java/RccTokenManager.java",
    "rcc_java/SimpleCharStream.java",
    "rcc_java/Token.java",
    "rcc_java/TokenMgrError.java",
  ]
)

java_library(
  name = "jute_runtime",
  srcs = glob([
    "main/org/apache/jute/*.java",
  ])
)

java_library(
  name = "jute_compiler",
  srcs = glob([
    "main/org/apache/jute/compiler/*.java",
  ]) + [
    ":javacc_rcc"
  ],
)

java_binary(
  name = "jute",
  visibility = [
    "//third_party/zookeeper:__subpackages__",
  ],
  main_class = "org.apache.jute.compiler.generated.Rcc",
  runtime_deps = [
    ":jute_compiler",
  ]
)

genrule(
  name = "generate_jute_java",
  tools = [
    ":jute"
  ],
  srcs = [
    "//third_party/zookeeper:src/zookeeper.jute"
  ],
  cmd = "TOP=$$PWD; cd $(@D)/jute_java; $$TOP/$(location :jute) -l java $$TOP/$<",
  outs = [
    "jute_java/org/apache/zookeeper/data/ACL.java",
    "jute_java/org/apache/zookeeper/data/Id.java",
    "jute_java/org/apache/zookeeper/data/Stat.java",
    "jute_java/org/apache/zookeeper/data/StatPersisted.java",
    "jute_java/org/apache/zookeeper/proto/AuthPacket.java",
    "jute_java/org/apache/zookeeper/proto/CheckVersionRequest.java",
    "jute_java/org/apache/zookeeper/proto/CheckWatchesRequest.java",
    "jute_java/org/apache/zookeeper/proto/ConnectRequest.java",
    "jute_java/org/apache/zookeeper/proto/ConnectResponse.java",
    "jute_java/org/apache/zookeeper/proto/Create2Response.java",
    "jute_java/org/apache/zookeeper/proto/CreateRequest.java",
    "jute_java/org/apache/zookeeper/proto/CreateResponse.java",
    "jute_java/org/apache/zookeeper/proto/DeleteRequest.java",
    "jute_java/org/apache/zookeeper/proto/ErrorResponse.java",
    "jute_java/org/apache/zookeeper/proto/ExistsRequest.java",
    "jute_java/org/apache/zookeeper/proto/ExistsResponse.java",
    "jute_java/org/apache/zookeeper/proto/GetACLRequest.java",
    "jute_java/org/apache/zookeeper/proto/GetACLResponse.java",
    "jute_java/org/apache/zookeeper/proto/GetChildren2Request.java",
    "jute_java/org/apache/zookeeper/proto/GetChildren2Response.java",
    "jute_java/org/apache/zookeeper/proto/GetChildrenRequest.java",
    "jute_java/org/apache/zookeeper/proto/GetChildrenResponse.java",
    "jute_java/org/apache/zookeeper/proto/GetDataRequest.java",
    "jute_java/org/apache/zookeeper/proto/GetDataResponse.java",
    "jute_java/org/apache/zookeeper/proto/GetMaxChildrenRequest.java",
    "jute_java/org/apache/zookeeper/proto/GetMaxChildrenResponse.java",
    "jute_java/org/apache/zookeeper/proto/GetSASLRequest.java",
    "jute_java/org/apache/zookeeper/proto/MultiHeader.java",
    "jute_java/org/apache/zookeeper/proto/ReconfigRequest.java",
    "jute_java/org/apache/zookeeper/proto/RemoveWatchesRequest.java",
    "jute_java/org/apache/zookeeper/proto/ReplyHeader.java",
    "jute_java/org/apache/zookeeper/proto/RequestHeader.java",
    "jute_java/org/apache/zookeeper/proto/SetACLRequest.java",
    "jute_java/org/apache/zookeeper/proto/SetACLResponse.java",
    "jute_java/org/apache/zookeeper/proto/SetDataRequest.java",
    "jute_java/org/apache/zookeeper/proto/SetDataResponse.java",
    "jute_java/org/apache/zookeeper/proto/SetMaxChildrenRequest.java",
    "jute_java/org/apache/zookeeper/proto/SetSASLRequest.java",
    "jute_java/org/apache/zookeeper/proto/SetSASLResponse.java",
    "jute_java/org/apache/zookeeper/proto/SetWatches.java",
    "jute_java/org/apache/zookeeper/proto/SyncRequest.java",
    "jute_java/org/apache/zookeeper/proto/SyncResponse.java",
    "jute_java/org/apache/zookeeper/proto/WatcherEvent.java",
    "jute_java/org/apache/zookeeper/server/persistence/FileHeader.java",
    "jute_java/org/apache/zookeeper/server/quorum/LearnerInfo.java",
    "jute_java/org/apache/zookeeper/server/quorum/QuorumPacket.java",
    "jute_java/org/apache/zookeeper/txn/CheckVersionTxn.java",
    "jute_java/org/apache/zookeeper/txn/CreateContainerTxn.java",
    "jute_java/org/apache/zookeeper/txn/CreateSessionTxn.java",
    "jute_java/org/apache/zookeeper/txn/CreateTxn.java",
    "jute_java/org/apache/zookeeper/txn/CreateTxnV0.java",
    "jute_java/org/apache/zookeeper/txn/DeleteTxn.java",
    "jute_java/org/apache/zookeeper/txn/ErrorTxn.java",
    "jute_java/org/apache/zookeeper/txn/MultiTxn.java",
    "jute_java/org/apache/zookeeper/txn/SetACLTxn.java",
    "jute_java/org/apache/zookeeper/txn/SetDataTxn.java",
    "jute_java/org/apache/zookeeper/txn/SetMaxChildrenTxn.java",
    "jute_java/org/apache/zookeeper/txn/Txn.java",
    "jute_java/org/apache/zookeeper/txn/TxnHeader.java",
  ],
)

java_library(
  name = "zookeeper_jute_java",
  srcs = [
    ":generate_jute_java",
  ],
  deps = [
    ":jute_runtime",
  ]
)

java_binary(
  name = "vergen",
  main_class = "org.apache.zookeeper.version.util.VerGen",
  srcs = [
    "main/org/apache/zookeeper/version/util/VerGen.java",
  ],
)

genrule(
  name = "generate_version_info",
  tools = [
    ":vergen",
  ],
  outs = [
    "org/apache/zookeeper/version/Info.java",
  ],
  cmd = "TOP=$$PWD; cd $(GENDIR)/third_party/zookeeper/src/java; $$TOP/$(location :vergen) 3.6.0 105510 20160815"
)

java_library(
  name = "zookeeper",
  visibility = ["//visibility:public"],
  srcs = glob([
    "main/org/apache/zookeeper/**/*.java",
  ]) + [
    ":generate_version_info",
  ],
  deps = [
    "//external:apache_log4j",
    "//external:slf4j",
    "//third_party/java/apache/commons_cli:commons-cli",
    "//third_party/java/jackson",
    "//third_party/java/jetty6",
    "//third_party/java/jline2",
    "//third_party/java/netty3",
    "//third_party/java/servlet-api",
    ":jute_runtime",
    ":zookeeper_jute_java",
  ],
  exports = [
    ":zookeeper_jute_java",
  ],
)
