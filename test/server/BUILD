load(
    "//bazel:envoy_build_system.bzl",
    "envoy_benchmark_test",
    "envoy_cc_benchmark_binary",
    "envoy_cc_fuzz_test",
    "envoy_cc_test",
    "envoy_cc_test_library",
    "envoy_package",
    "envoy_select_hot_restart",
)
load("//source/extensions:all_extensions.bzl", "envoy_all_extensions")
load("//bazel:repositories.bzl", "PPC_SKIP_TARGETS", "WINDOWS_SKIP_TARGETS")

licenses(["notice"])  # Apache 2

envoy_package()

envoy_cc_test(
    name = "api_listener_test",
    srcs = ["api_listener_test.cc"],
    deps = [
        ":utility_lib",
        "//source/extensions/request_id/uuid:config",
        "//source/server:listener_manager_lib",
        "//test/mocks/network:network_mocks",
        "//test/mocks/server:instance_mocks",
        "//test/mocks/server:listener_component_factory_mocks",
        "//test/mocks/server:worker_factory_mocks",
        "//test/mocks/server:worker_mocks",
        "//test/test_common:utility_lib",
        "@envoy_api//envoy/config/listener/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "backtrace_test",
    srcs = ["backtrace_test.cc"],
    tags = ["backtrace"],
    deps = [
        "//source/server:backtrace_lib",
        "//test/test_common:logging_lib",
    ],
)

envoy_cc_test(
    name = "configuration_impl_test",
    srcs = ["configuration_impl_test.cc"],
    data = [
        "//test/config/integration/certs",
    ],
    deps = [
        "//source/common/api:api_lib",
        "//source/common/event:dispatcher_lib",
        "//source/common/http:context_lib",
        "//source/common/upstream:cluster_manager_lib",
        "//source/extensions/access_loggers/file:config",
        "//source/extensions/stat_sinks/statsd:config",
        "//source/extensions/transport_sockets/raw_buffer:config",
        "//source/server:configuration_lib",
        "//test/common/upstream:utility_lib",
        "//test/mocks:common_lib",
        "//test/mocks/network:network_mocks",
        "//test/mocks/server:instance_mocks",
        "//test/test_common:environment_lib",
        "//test/test_common:test_runtime_lib",
        "//test/test_common:utility_lib",
        "@envoy_api//envoy/config/bootstrap/v3:pkg_cc_proto",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
        "@envoy_api//envoy/config/metrics/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "connection_handler_test",
    srcs = ["connection_handler_test.cc"],
    deps = [
        "//source/common/common:utility_lib",
        "//source/common/config:utility_lib",
        "//source/common/network:address_lib",
        "//source/common/network:connection_balancer_lib",
        "//source/common/network:udp_packet_writer_handler_lib",
        "//source/common/stats:stats_lib",
        "//source/server:active_raw_udp_listener_config",
        "//source/server:connection_handler_lib",
        "//test/mocks/access_log:access_log_mocks",
        "//test/mocks/api:api_mocks",
        "//test/mocks/network:network_mocks",
        "//test/test_common:network_utility_lib",
        "//test/test_common:test_runtime_lib",
        "//test/test_common:threadsafe_singleton_injector_lib",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
        "@envoy_api//envoy/config/listener/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "active_tcp_listener_test",
    srcs = ["active_tcp_listener_test.cc"],
    deps = [
        "//source/common/common:utility_lib",
        "//source/common/config:utility_lib",
        "//source/common/network:address_lib",
        "//source/common/network:connection_balancer_lib",
        "//source/common/stats:stats_lib",
        "//source/server:connection_handler_lib",
        "//test/mocks/network:io_handle_mocks",
        "//test/mocks/network:network_mocks",
        "//test/test_common:network_utility_lib",
    ],
)

envoy_cc_test(
    name = "active_internal_listener_test",
    srcs = ["active_internal_listener_test.cc"],
    deps = [
        ":utility_lib",
        "//source/common/network:address_lib",
        "//source/common/network:listen_socket_lib",
        "//source/common/network:utility_lib",
        "//source/common/stats:stats_lib",
        "//source/extensions/transport_sockets/raw_buffer:config",
        "//source/server:connection_handler_lib",
        "//test/mocks/network:network_mocks",
    ],
)

envoy_cc_test(
    name = "active_udp_listener_test",
    srcs = ["active_udp_listener_test.cc"],
    deps = [
        "//source/common/network:listen_socket_lib",
        "//source/common/network:socket_option_factory_lib",
        "//source/common/network:udp_packet_writer_handler_lib",
        "//source/server:active_udp_listener",
        "//test/mocks/network:network_mocks",
        "//test/test_common:environment_lib",
        "//test/test_common:network_utility_lib",
    ],
)

envoy_cc_test(
    name = "drain_manager_impl_test",
    srcs = ["drain_manager_impl_test.cc"],
    deps = [
        "//source/server:drain_manager_lib",
        "//test/mocks/event:event_mocks",
        "//test/mocks/server:instance_mocks",
        "@envoy_api//envoy/config/listener/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "filter_config_test",
    srcs = ["filter_config_test.cc"],
    deps = [
        "//envoy/server:filter_config_interface",
        "//source/extensions/filters/http/common:pass_through_filter_lib",
        "//test/mocks/server:server_mocks",
    ],
)

envoy_cc_test(
    name = "hot_restart_impl_test",
    srcs = envoy_select_hot_restart(["hot_restart_impl_test.cc"]),
    deps = [
        "//source/common/api:os_sys_calls_lib",
        "//source/common/stats:stats_lib",
        "//source/server:hot_restart_lib",
        "//test/mocks/server:server_mocks",
        "//test/test_common:logging_lib",
        "//test/test_common:threadsafe_singleton_injector_lib",
    ],
)

envoy_cc_test(
    name = "hot_restarting_parent_test",
    srcs = envoy_select_hot_restart(["hot_restarting_parent_test.cc"]),
    deps = [
        "//source/common/stats:stats_lib",
        "//source/server:hot_restart_lib",
        "//source/server:hot_restarting_child",
        "//test/mocks/network:network_mocks",
        "//test/mocks/server:server_mocks",
    ],
)

envoy_cc_test(
    name = "hot_restarting_base_test",
    srcs = envoy_select_hot_restart(["hot_restarting_base_test.cc"]),
    deps = [
        "//source/server:hot_restart_lib",
        "//source/server:hot_restarting_base",
        "//test/mocks/api:api_mocks",
        "//test/mocks/network:network_mocks",
        "//test/test_common:threadsafe_singleton_injector_lib",
    ],
)

envoy_cc_test(
    name = "guarddog_impl_test",
    size = "small",
    srcs = ["guarddog_impl_test.cc"],
    deps = [
        "//envoy/common:time_interface",
        "//source/common/api:api_lib",
        "//source/common/common:macros",
        "//source/common/common:utility_lib",
        "//source/common/stats:stats_lib",
        "//source/server:guarddog_lib",
        "//test/mocks:common_lib",
        "//test/mocks/event:event_mocks",
        "//test/mocks/server:watchdog_config_mocks",
        "//test/mocks/stats:stats_mocks",
        "//test/test_common:registry_lib",
        "//test/test_common:simulated_time_system_lib",
        "//test/test_common:test_runtime_lib",
        "//test/test_common:utility_lib",
    ],
)

envoy_cc_test(
    name = "options_impl_test",
    srcs = ["options_impl_test.cc"],
    deps = [
        "//envoy/config:typed_config_interface",
        "//envoy/server:filter_config_interface",
        "//source/common/common:utility_lib",
        "//source/common/stats:stats_lib",
        "//source/extensions/filters/http/buffer:config",
        "//source/server:options_lib",
        "//test/mocks/api:api_mocks",
        "//test/test_common:environment_lib",
        "//test/test_common:logging_lib",
        "//test/test_common:registry_lib",
        "//test/test_common:threadsafe_singleton_injector_lib",
        "//test/test_common:utility_lib",
        "@envoy_api//envoy/admin/v3:pkg_cc_proto",
        "@envoy_api//envoy/config/bootstrap/v3:pkg_cc_proto",
        "@envoy_api//envoy/config/filter/http/buffer/v2:pkg_cc_proto",
        "@envoy_api//envoy/extensions/filters/http/buffer/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "overload_manager_impl_test",
    srcs = ["overload_manager_impl_test.cc"],
    deps = [
        "//envoy/registry",
        "//source/common/stats:isolated_store_lib",
        "//source/extensions/resource_monitors/common:factory_base_lib",
        "//source/server:overload_manager_lib",
        "//test/mocks/event:event_mocks",
        "//test/mocks/protobuf:protobuf_mocks",
        "//test/mocks/server:options_mocks",
        "//test/mocks/thread_local:thread_local_mocks",
        "//test/test_common:registry_lib",
        "//test/test_common:test_runtime_lib",
        "//test/test_common:utility_lib",
        "@envoy_api//envoy/config/overload/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "lds_api_test",
    srcs = ["lds_api_test.cc"],
    data = [
        "//test/config/integration/certs",
    ],
    deps = [
        "//source/common/protobuf:utility_lib",
        "//source/server:lds_api_lib",
        "//test/mocks/config:config_mocks",
        "//test/mocks/init:init_mocks",
        "//test/mocks/protobuf:protobuf_mocks",
        "//test/mocks/server:listener_manager_mocks",
        "//test/mocks/upstream:upstream_mocks",
        "//test/test_common:environment_lib",
        "//test/test_common:utility_lib",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
        "@envoy_api//envoy/config/listener/v3:pkg_cc_proto",
        "@envoy_api//envoy/service/discovery/v3:pkg_cc_proto",
    ],
)

envoy_cc_test_library(
    name = "listener_manager_impl_test_lib",
    hdrs = ["listener_manager_impl_test.h"],
    data = ["//test/extensions/transport_sockets/tls/test_data:certs"],
    deps = [
        "//source/common/init:manager_lib",
        "//source/extensions/common/matcher:trie_matcher_lib",
        "//source/server:listener_manager_lib",
        "//test/mocks/init:init_mocks",
        "//test/mocks/matcher:matcher_mocks",
        "//test/mocks/network:network_mocks",
        "//test/mocks/server:drain_manager_mocks",
        "//test/mocks/server:guard_dog_mocks",
        "//test/mocks/server:instance_mocks",
        "//test/mocks/server:listener_component_factory_mocks",
        "//test/mocks/server:worker_factory_mocks",
        "//test/mocks/server:worker_mocks",
        "//test/test_common:environment_lib",
        "//test/test_common:simulated_time_system_lib",
        "//test/test_common:test_runtime_lib",
        "//test/test_common:test_time_lib",
        "//test/test_common:threadsafe_singleton_injector_lib",
        "@envoy_api//envoy/admin/v3:pkg_cc_proto",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
        "@envoy_api//envoy/config/listener/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "listener_manager_impl_test",
    srcs = ["listener_manager_impl_test.cc"],
    deps = [
        ":listener_manager_impl_test_lib",
        ":utility_lib",
        "//source/common/api:os_sys_calls_lib",
        "//source/common/config:metadata_lib",
        "//source/common/network:addr_family_aware_socket_option_lib",
        "//source/common/network:listen_socket_lib",
        "//source/common/network:socket_option_lib",
        "//source/common/network:utility_lib",
        "//source/common/protobuf",
        "//source/extensions/filters/listener/original_dst:config",
        "//source/extensions/filters/listener/proxy_protocol:config",
        "//source/extensions/filters/listener/tls_inspector:config",
        "//source/extensions/filters/network/http_connection_manager:config",
        "//source/extensions/filters/network/tcp_proxy:config",
        "//source/extensions/request_id/uuid:config",
        "//source/extensions/transport_sockets/raw_buffer:config",
        "//source/extensions/transport_sockets/tls:config",
        "//source/extensions/transport_sockets/tls:ssl_socket_lib",
        "//source/server:active_raw_udp_listener_config",
        "//test/integration/filters:test_listener_filter_lib",
        "//test/test_common:network_utility_lib",
        "//test/test_common:registry_lib",
        "//test/test_common:test_runtime_lib",
        "@envoy_api//envoy/admin/v3:pkg_cc_proto",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
        "@envoy_api//envoy/config/listener/v3:pkg_cc_proto",
    ],
)

# Stand-alone quic test because of FIPS.
envoy_cc_test(
    name = "listener_manager_impl_quic_only_test",
    srcs = ["listener_manager_impl_quic_only_test.cc"],
    tags = ["nofips"],
    deps = [
        ":listener_manager_impl_test_lib",
        ":utility_lib",
        "//source/extensions/filters/http/router:config",
        "//source/extensions/request_id/uuid:config",
        "//source/extensions/transport_sockets/raw_buffer:config",
        "//source/extensions/transport_sockets/tls:config",
        "//test/test_common:threadsafe_singleton_injector_lib",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
        "@envoy_api//envoy/config/listener/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "filter_chain_manager_impl_test",
    srcs = ["filter_chain_manager_impl_test.cc"],
    data = ["//test/extensions/transport_sockets/tls/test_data:certs"],
    deps = [
        ":utility_lib",
        "//source/common/api:os_sys_calls_lib",
        "//source/common/config:metadata_lib",
        "//source/common/network:addr_family_aware_socket_option_lib",
        "//source/common/network:listen_socket_lib",
        "//source/common/network:socket_option_lib",
        "//source/common/network:utility_lib",
        "//source/common/protobuf",
        "//source/extensions/filters/network/http_connection_manager:config",
        "//source/extensions/transport_sockets/raw_buffer:config",
        "//source/extensions/transport_sockets/tls:config",
        "//source/extensions/transport_sockets/tls:ssl_socket_lib",
        "//source/server:filter_chain_manager_lib",
        "//source/server:listener_manager_lib",
        "//test/mocks/network:network_mocks",
        "//test/mocks/server:drain_manager_mocks",
        "//test/mocks/server:factory_context_mocks",
        "//test/test_common:environment_lib",
        "//test/test_common:registry_lib",
        "//test/test_common:simulated_time_system_lib",
        "//test/test_common:test_time_lib",
        "//test/test_common:threadsafe_singleton_injector_lib",
        "@envoy_api//envoy/config/listener/v3:pkg_cc_proto",
    ],
)

envoy_cc_fuzz_test(
    name = "server_fuzz_test",
    srcs = ["server_fuzz_test.cc"],
    corpus = "server_corpus",
    deps = [
        "//source/common/thread_local:thread_local_lib",
        "//source/server:server_lib",
        "//test/integration:integration_lib",
        "//test/mocks/server:options_mocks",
        "//test/mocks/server:hot_restart_mocks",
        "//test/test_common:environment_lib",
    ] + select({
        "//bazel:windows_x86_64": envoy_all_extensions(WINDOWS_SKIP_TARGETS),
        "//bazel:linux_ppc": envoy_all_extensions(PPC_SKIP_TARGETS),
        "//bazel:gcc_build": [],
        "//conditions:default": envoy_all_extensions(),
    }),
)

filegroup(
    name = "server_test_data",
    srcs = glob(["test_data/server/**"]),
)

filegroup(
    name = "runtime_test_data",
    srcs = glob(["test_data/runtime/**"]),
)

filegroup(
    name = "static_validation_test_data",
    srcs = glob(["test_data/static_validation/**"]),
)

envoy_cc_test(
    name = "server_test",
    srcs = ["server_test.cc"],
    data = [
        ":runtime_test_data",
        ":server_test_data",
        ":static_validation_test_data",
    ],
    deps = [
        "//source/common/version:version_lib",
        "//source/extensions/access_loggers/file:config",
        "//source/extensions/filters/http/buffer:config",
        "//source/extensions/filters/http/grpc_http1_bridge:config",
        "//source/extensions/filters/http/health_check:config",
        "//source/extensions/filters/http/router:config",
        "//source/extensions/filters/network/http_connection_manager:config",
        "//source/extensions/tracers/zipkin:config",
        "//source/server:process_context_lib",
        "//source/server:server_lib",
        "//test/common/config:dummy_config_proto_cc_proto",
        "//test/common/stats:stat_test_utility_lib",
        "//test/config:v2_link_hacks",
        "//test/integration:integration_lib",
        "//test/mocks/server:bootstrap_extension_factory_mocks",
        "//test/mocks/server:fatal_action_factory_mocks",
        "//test/mocks/server:hot_restart_mocks",
        "//test/mocks/server:instance_mocks",
        "//test/mocks/server:options_mocks",
        "//test/mocks/server:overload_manager_mocks",
        "//test/mocks/stats:stats_mocks",
        "//test/test_common:logging_lib",
        "//test/test_common:registry_lib",
        "//test/test_common:simulated_time_system_lib",
        "//test/test_common:test_runtime_lib",
        "//test/test_common:test_time_lib",
        "//test/test_common:utility_lib",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "ssl_context_manager_test",
    srcs = ["ssl_context_manager_test.cc"],
    deps = [
        "//source/server:ssl_context_manager_lib",
        "//test/mocks/ssl:ssl_mocks",
        "//test/mocks/stats:stats_mocks",
        "//test/test_common:simulated_time_system_lib",
        "//test/test_common:utility_lib",
    ],
)

envoy_cc_test_library(
    name = "utility_lib",
    hdrs = ["utility.h"],
    deps = [
        "//source/common/protobuf:utility_lib",
        "//test/test_common:utility_lib",
        "@envoy_api//envoy/config/listener/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "worker_impl_test",
    srcs = ["worker_impl_test.cc"],
    deps = [
        "//source/common/api:api_lib",
        "//source/common/event:dispatcher_lib",
        "//source/server:worker_lib",
        "//test/mocks/network:network_mocks",
        "//test/mocks/runtime:runtime_mocks",
        "//test/mocks/server:guard_dog_mocks",
        "//test/mocks/server:instance_mocks",
        "//test/mocks/server:overload_manager_mocks",
        "//test/mocks/thread_local:thread_local_mocks",
        "//test/test_common:utility_lib",
    ],
)

envoy_cc_benchmark_binary(
    name = "filter_chain_benchmark_test",
    srcs = ["filter_chain_benchmark_test.cc"],
    external_deps = [
        "benchmark",
        "googletest",
    ],
    deps = [
        "@envoy_api//envoy/config/listener/v3:pkg_cc_proto",
        "//source/server:filter_chain_manager_lib",
        "//test/test_common:environment_lib",
        "//test/mocks/network:network_mocks",
        "//test/mocks/server:factory_context_mocks",
        # tranport socket config registration
        "//source/extensions/transport_sockets/tls:config",
    ],
)

envoy_benchmark_test(
    name = "filter_chain_benchmark_test_benchmark_test",
    timeout = "long",
    benchmark_binary = "filter_chain_benchmark_test",
)

envoy_cc_benchmark_binary(
    name = "server_stats_flush_benchmark",
    srcs = ["server_stats_flush_benchmark_test.cc"],
    external_deps = [
        "benchmark",
    ],
    deps = [
        "//envoy/stats:stats_interface",
        "//source/common/stats:thread_local_store_lib",
        "//source/server:server_lib",
        "//test/test_common:simulated_time_system_lib",
    ],
)

envoy_benchmark_test(
    name = "server_stats_flush_benchmark_test",
    benchmark_binary = "server_stats_flush_benchmark",
)
