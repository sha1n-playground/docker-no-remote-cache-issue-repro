load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# Download the rules_docker repository version https://github.com/bazelbuild/rules_docker/pull/1272
rules_docker_version = "c6d5dd8ae0aa53577e4e6fe83d20f7183998946c"
rules_docker_version_sha256 = "75b49be0580f4c84167972d6d166b557bf278683ee144cccd8023608a7ea5add"
http_archive(
  name = "io_bazel_rules_docker",
  sha256 = rules_docker_version_sha256,
  strip_prefix= "bazelbuild-rules_docker-c6d5dd8",
  urls = ["https://github.com/bazelbuild/rules_docker/archive/%s.tar.gz" % rules_docker_version],
)

# OPTIONAL: Call this to override the default docker toolchain configuration.
# This call should be placed BEFORE the call to "container_repositories" below
# to actually override the default toolchain configuration.
# Note this is only required if you actually want to call
# docker_toolchain_configure with a custom attr; please read the toolchains
# docs in /toolchains/docker/ before blindly adding this to your WORKSPACE.
# BEGIN OPTIONAL segment:
load("@io_bazel_rules_docker//toolchains/docker:toolchain.bzl",
    docker_toolchain_configure="toolchain_configure"
)
docker_toolchain_configure(
  name = "docker_config",
  # OPTIONAL: Path to a directory which has a custom docker client config.json.
  # See https://docs.docker.com/engine/reference/commandline/cli/#configuration-files
  # for more details.
  client_config="<enter absolute path to your docker config directory here>",
)
# End of OPTIONAL segment.

load(
    "@io_bazel_rules_docker//repositories:repositories.bzl",
    container_repositories = "repositories",
)
container_repositories()

# This is NOT needed when going through the language lang_image
# "repositories" function(s).
load("@io_bazel_rules_docker//repositories:deps.bzl", container_deps = "deps")

container_deps()

load(
    "@io_bazel_rules_docker//container:container.bzl",
    "container_pull",
)

container_pull(
  name = "elasticsearch_elasticsearch_6.4.2",
  registry = "docker.elastic.co",
  repository = "elasticsearch/elasticsearch",
  tag = "6.4.2",
)

