---
date: 2017-08-25 18:49:30
status: public
title: 一天：Kafka入门与项目实战
keywords: 
- Kafka
- 入门
- 教程
tags: 
- Python
- flask
- Kafka
categories: 
- 快速入门快速实践
- 一天
---
# 前言
未完待续。此文将持续更新。
- v0.1 [初稿：可运行的代码] 2017-08-25 18:50:08

# Quick Start
- [CET4没过轻松读：Apache 官方最新文档](https://kafka.apache.org/quickstart)

# For Pythoner

直接看Consumer类源码。
```
class KafkaConsumer(six.Iterator):
    """Consume records from a Kafka cluster.

    The consumer will transparently handle the failure of servers in the Kafka
    cluster, and adapt as topic-partitions are created or migrate between
    brokers. It also interacts with the assigned kafka Group Coordinator node
    to allow multiple consumers to load balance consumption of topics (requires
    kafka >= 0.9.0.0).

    The consumer is not thread safe and should not be shared across threads.

    Arguments:
        *topics (str): optional list of topics to subscribe to. If not set,
            call :meth:`~kafka.KafkaConsumer.subscribe` or
            :meth:`~kafka.KafkaConsumer.assign` before consuming records.

    Keyword Arguments:
        bootstrap_servers: 'host[:port]' string (or list of 'host[:port]'
            strings) that the consumer should contact to bootstrap initial
            cluster metadata. This does not have to be the full node list.
            It just needs to have at least one broker that will respond to a
            Metadata API Request. Default port is 9092. If no servers are
            specified, will default to localhost:9092.
        client_id (str): A name for this client. This string is passed in
            each request to servers and can be used to identify specific
            server-side log entries that correspond to this client. Also
            submitted to GroupCoordinator for logging with respect to
            consumer group administration. Default: 'kafka-python-{version}'
        group_id (str or None): The name of the consumer group to join for dynamic
            partition assignment (if enabled), and to use for fetching and
            committing offsets. If None, auto-partition assignment (via
            group coordinator) and offset commits are disabled.
            Default: None
        key_deserializer (callable): Any callable that takes a
            raw message key and returns a deserialized key.
        value_deserializer (callable): Any callable that takes a
            raw message value and returns a deserialized value.
        fetch_min_bytes (int): Minimum amount of data the server should
            return for a fetch request, otherwise wait up to
            fetch_max_wait_ms for more data to accumulate. Default: 1.
        fetch_max_wait_ms (int): The maximum amount of time in milliseconds
            the server will block before answering the fetch request if
            there isn't sufficient data to immediately satisfy the
            requirement given by fetch_min_bytes. Default: 500.
        fetch_max_bytes (int): The maximum amount of data the server should
            return for a fetch request. This is not an absolute maximum, if the
            first message in the first non-empty partition of the fetch is
            larger than this value, the message will still be returned to
            ensure that the consumer can make progress. NOTE: consumer performs
            fetches to multiple brokers in parallel so memory usage will depend
            on the number of brokers containing partitions for the topic.
            Supported Kafka version >= 0.10.1.0. Default: 52428800 (50 Mb).
        max_partition_fetch_bytes (int): The maximum amount of data
            per-partition the server will return. The maximum total memory
            used for a request = #partitions * max_partition_fetch_bytes.
            This size must be at least as large as the maximum message size
            the server allows or else it is possible for the producer to
            send messages larger than the consumer can fetch. If that
            happens, the consumer can get stuck trying to fetch a large
            message on a certain partition. Default: 1048576.
        request_timeout_ms (int): Client request timeout in milliseconds.
            Default: 40000.
        retry_backoff_ms (int): Milliseconds to backoff when retrying on
            errors. Default: 100.
        reconnect_backoff_ms (int): The amount of time in milliseconds to
            wait before attempting to reconnect to a given host.
            Default: 50.
        reconnect_backoff_max_ms (int): The maximum amount of time in
            milliseconds to wait when reconnecting to a broker that has
            repeatedly failed to connect. If provided, the backoff per host
            will increase exponentially for each consecutive connection
            failure, up to this maximum. To avoid connection storms, a
            randomization factor of 0.2 will be applied to the backoff
            resulting in a random range between 20% below and 20% above
            the computed value. Default: 1000.
        max_in_flight_requests_per_connection (int): Requests are pipelined
            to kafka brokers up to this number of maximum requests per
            broker connection. Default: 5.
        auto_offset_reset (str): A policy for resetting offsets on
            OffsetOutOfRange errors: 'earliest' will move to the oldest
            available message, 'latest' will move to the most recent. Any
            other value will raise the exception. Default: 'latest'.
        enable_auto_commit (bool): If True , the consumer's offset will be
            periodically committed in the background. Default: True.
        auto_commit_interval_ms (int): Number of milliseconds between automatic
            offset commits, if enable_auto_commit is True. Default: 5000.
        default_offset_commit_callback (callable): Called as
            callback(offsets, response) response will be either an Exception
            or an OffsetCommitResponse struct. This callback can be used to
            trigger custom actions when a commit request completes.
        check_crcs (bool): Automatically check the CRC32 of the records
            consumed. This ensures no on-the-wire or on-disk corruption to
            the messages occurred. This check adds some overhead, so it may
            be disabled in cases seeking extreme performance. Default: True
        metadata_max_age_ms (int): The period of time in milliseconds after
            which we force a refresh of metadata, even if we haven't seen any
            partition leadership changes to proactively discover any new
            brokers or partitions. Default: 300000
        partition_assignment_strategy (list): List of objects to use to
            distribute partition ownership amongst consumer instances when
            group management is used.
            Default: [RangePartitionAssignor, RoundRobinPartitionAssignor]
        heartbeat_interval_ms (int): The expected time in milliseconds
            between heartbeats to the consumer coordinator when using
            Kafka's group management feature. Heartbeats are used to ensure
            that the consumer's session stays active and to facilitate
            rebalancing when new consumers join or leave the group. The
            value must be set lower than session_timeout_ms, but typically
            should be set no higher than 1/3 of that value. It can be
            adjusted even lower to control the expected time for normal
            rebalances. Default: 3000
        session_timeout_ms (int): The timeout used to detect failures when
            using Kafka's group management facilities. Default: 30000
        max_poll_records (int): The maximum number of records returned in a
            single call to :meth:`~kafka.KafkaConsumer.poll`. Default: 500
        receive_buffer_bytes (int): The size of the TCP receive buffer
            (SO_RCVBUF) to use when reading data. Default: None (relies on
            system defaults). The java client defaults to 32768.
        send_buffer_bytes (int): The size of the TCP send buffer
            (SO_SNDBUF) to use when sending data. Default: None (relies on
            system defaults). The java client defaults to 131072.
        socket_options (list): List of tuple-arguments to socket.setsockopt
            to apply to broker connection sockets. Default:
            [(socket.IPPROTO_TCP, socket.TCP_NODELAY, 1)]
        consumer_timeout_ms (int): number of milliseconds to block during
            message iteration before raising StopIteration (i.e., ending the
            iterator). Default block forever [float('inf')].
        skip_double_compressed_messages (bool): A bug in KafkaProducer <= 1.2.4
            caused some messages to be corrupted via double-compression.
            By default, the fetcher will return these messages as a compressed
            blob of bytes with a single offset, i.e. how the message was
            actually published to the cluster. If you prefer to have the
            fetcher automatically detect corrupt messages and skip them,
            set this option to True. Default: False.
        security_protocol (str): Protocol used to communicate with brokers.
            Valid values are: PLAINTEXT, SSL. Default: PLAINTEXT.
        ssl_context (ssl.SSLContext): Pre-configured SSLContext for wrapping
            socket connections. If provided, all other ssl_* configurations
            will be ignored. Default: None.
        ssl_check_hostname (bool): Flag to configure whether ssl handshake
            should verify that the certificate matches the brokers hostname.
            Default: True.
        ssl_cafile (str): Optional filename of ca file to use in certificate
            verification. Default: None.
        ssl_certfile (str): Optional filename of file in pem format containing
            the client certificate, as well as any ca certificates needed to
            establish the certificate's authenticity. Default: None.
        ssl_keyfile (str): Optional filename containing the client private key.
            Default: None.
        ssl_password (str): Optional password to be used when loading the
            certificate chain. Default: None.
        ssl_crlfile (str): Optional filename containing the CRL to check for
            certificate expiration. By default, no CRL check is done. When
            providing a file, only the leaf certificate will be checked against
            this CRL. The CRL can only be checked with Python 3.4+ or 2.7.9+.
            Default: None.
        api_version (tuple): Specify which Kafka API version to use. If set to
            None, the client will attempt to infer the broker version by probing
            various APIs. Different versions enable different functionality.

            Examples:
                (0, 9) enables full group coordination features with automatic
                    partition assignment and rebalancing,
                (0, 8, 2) enables kafka-storage offset commits with manual
                    partition assignment only,
                (0, 8, 1) enables zookeeper-storage offset commits with manual
                    partition assignment only,
                (0, 8, 0) enables basic functionality but requires manual
                    partition assignment and offset management.

            For the full list of supported versions, see
            KafkaClient.API_VERSIONS. Default: None
        api_version_auto_timeout_ms (int): number of milliseconds to throw a
            timeout exception from the constructor when checking the broker
            api version. Only applies if api_version set to 'auto'
        metric_reporters (list): A list of classes to use as metrics reporters.
            Implementing the AbstractMetricsReporter interface allows plugging
            in classes that will be notified of new metric creation. Default: []
        metrics_num_samples (int): The number of samples maintained to compute
            metrics. Default: 2
        metrics_sample_window_ms (int): The maximum age in milliseconds of
            samples used to compute metrics. Default: 30000
        selector (selectors.BaseSelector): Provide a specific selector
            implementation to use for I/O multiplexing.
            Default: selectors.DefaultSelector
        exclude_internal_topics (bool): Whether records from internal topics
            (such as offsets) should be exposed to the consumer. If set to True
            the only way to receive records from an internal topic is
            subscribing to it. Requires 0.10+ Default: True
        sasl_mechanism (str): String picking sasl mechanism when security_protocol
            is SASL_PLAINTEXT or SASL_SSL. Currently only PLAIN is supported.
            Default: None
        sasl_plain_username (str): Username for sasl PLAIN authentication.
            Default: None
        sasl_plain_password (str): Password for sasl PLAIN authentication.
            Default: None
```


- def __next__(self)
- def _message_generator(self):

- HTTP流式响应：https://gist.github.com/CMCDragonkai/6bfade6431e9ffb7fe88

- https://www.w3.org/Protocols/rfc1341/7_2_Multipart.html


- Chrome抓包：chrome://net-internals/#requests
- Kafka入门：http://www.aboutyun.com/thread-12882-1-1.html

# 我的业务需求
已有实现是pip包客户端从flask服务器获取kafka服务器地址，在客户端直接消费。

需要加上权限认证提升安全性，因此需要交由flask转发kafka日志。

# 服务端实现
```python

# -*- coding: utf-8 -*-
from flask_restful import Resource, reqparse
from flask import Response, jsonify, g, stream_with_context
from App.common import error_util as ED
from App.views.user_views import auth
from kafka import KafkaConsumer
import json
from flask.ctx import _request_ctx_stack
from itertools import chain
@check_api_cost_time
@auth.login_required
@flask_app.route('/api/v1/logs', methods=['GET'], endpoint='task-logs')
def get_logs_of_task():
    parser = reqparse.RequestParser()
    parser.add_argument('method', type=str, location='args')
    parser.add_argument('id', type=str, location='args')
    args = parser.parse_args()
    if args.get('method') and args.get('method').lower() == 'kafka':
        task_id = args.get('id')
        if not task_id:
            return jsonify(ED.error_response_norm(ED.err_req_data))
        if not is_owned_by_guser(get_experiment_by_id(task_id)):
            return jsonify(ED.error_response_norm(ED.err_user_permission))

        res = Response(stream_with_context(chain(celery_log_generator(task_id),container_log_generator(task_id))),
                       direct_passthrough=True,
                       mimetype='multipart/x-mixed-replace')
        # res.headers['Transfer-Encoding'] = 'chunked'
        return res


def container_log_generator(task_id):
    consumer = KafkaConsumer(task_id,
                             bootstrap_servers=flask_app.config['KAFKA_BROKER_URI'],
                             auto_offset_reset='earliest',
                             enable_auto_commit=False,
                             request_timeout_ms=40000,
                             consumer_timeout_ms=10000)
    try:
        for msg in consumer:
            str_line = json.loads(msg.value).get("log").strip("\n") + b'\r\n'
            yield bytes(str_line)
    except StopIteration as e:
        return

def celery_log_generator(task_id):
    path = flask_app.config['UPLOAD_LOG_FOLDER'] + task_id + "/worker.log"
    with open(path) as f:
        for line in f:
            yield line

```
# 客户端实现
```python
def logs(id, tail, sleep_duration=1):
    """
    Print the logs of the run.
    """
    # experiment = ExperimentClient().get(id)
    # task_instance = TaskInstanceClient().get(get_module_task_instance_id(experiment.task_instances))

    # log_server = ExperimentClient().get_log_server(id)
    # if not log_server:
    #     russell_logger.info("There is not a valid task id")
    #     return
    import logging
    russell_logger.info("loading log...")
    logging.disable(sys.maxsize)

    lines = ExperimentClient().get_log_stream(id)
    if not lines:
        print("No logs....")
    for line in lines:
        print(line)
    # consumer = KafkaConsumer(id, bootstrap_servers=log_server,
    #                              auto_offset_reset='earliest', enable_auto_commit=False)
    # for msg in consumer:
    #     print(json.loads(msg.value).get("log").strip("\n"))

    logging.disable(logging.NOTSET)

'''ExperimentClinet(BaseHttpClient'''
    def get_log_stream(self, id, method='kafka'):
        timeout = 50
        response = self.request("GET",
                                "/logs",
                                params={'method':method, 'id':id},
                                stream=True,
                                timeout=timeout)
        return response.iter_lines()
'''BaseHttpClient'''
    """
    Base client for all HTTP operations
    """
class BaseHttpClient(object):
    def __init__(self):
        self.base_url = "{}/api/v1".format(host)
        self.access_token = AuthConfigManager.get_access_token()

    def request(self,
                method,
                url,
                params=None,
                data=None,
                files=None,
                timeout=5,
                access_token=None,
                stream=False):
        """
        Execute the request using requests library
        """
        request_url = self.base_url + url
        russell_logger.debug("Starting request to url: {} with params: {}, data: {}".format(request_url, params, data))
        if access_token:
            headers = {"Authorization": "Basic {}".format(access_token)}
        else:
            headers = {"Authorization": "Basic {}".format(
                self.access_token.token if self.access_token else None)
            }

        try:
            # print "url: {}".format(request_url)
            # print "params: {}".format(params)
            # print "data: {}".format(data)
            response = requests.request(method,
                                        request_url,
                                        params=params,
                                        headers=headers,
                                        data=data,
                                        files=files,
                                        timeout=timeout,
                                        stream=stream)
        except requests.exceptions.ConnectionError:
            sys.exit("Cannot connect to the Russell server. Check your internet connection.")

        if not stream:
            try:
                russell_logger.debug("Response Content: {}, Headers: {}".format(response.json(), response.headers))
            except Exception:
                russell_logger.debug("Request failed. Response: {}".format(response.content))
            self.check_response_status(response)
            print("response: {}".format(json.dumps(response.json())))
            return response.json()["data"]
        else:
            russell_logger.info('HTTP Stream Request/Response...')
            return response
```


不用flask的stream_with_context，则
```python
# @auth.login_required
# @flask_app.route('/api/v1/logs', methods=['GET'], endpoint='logs')
# def get_logs_of_task():
#     ctx = _request_ctx_stack.top.copy()
#     new_request = ctx.request
#     new_g = ctx.g
#     parser = reqparse.RequestParser()
#     parser.add_argument('method', type=str, location='args')
#     parser.add_argument('id', type=str, location='args')
#     args = parser.parse_args()
#     if args.get('method') and args.get('method').lower() == 'kafka':
#         log_server = flask_app.config['KAFKA_BROKER_URI']
#         task_id = args.get('id')
#         if not task_id:
#             return jsonify(ED.error_response_norm(ED.err_req_data))
#         if not getattr(getattr(new_g, 'user', None),'id', None) == getattr(get_experiment_by_id(task_id), 'owner_id', 0):
#             return jsonify(ED.error_response_norm(ED.err_user_permission))
    ''''''
```