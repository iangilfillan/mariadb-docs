# MariaDB MaxScale Configuration Guide

* [MariaDB MaxScale Configuration Guide](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#mariadb-maxscale-configuration-guide)
* [Introduction](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#introduction)
* [Concepts](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#concepts)
  * [Glossary](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#glossary)
  * [Objects](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#objects)
    * [Server](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#server)
    * [Monitor](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#monitor)
    * [Filter](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#filter)
    * [Router](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#router)
    * [Service](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#service)
    * [Listener](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#listener)
* [Administration](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#administration)
  * [Static Configuration Parameters](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#static-configuration-parameters)
* [Configuration](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#configuration)
  * [Names](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#names)
  * [Dynamic Configuration](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#dynamic-configuration)
  * [Special Parameter Types](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#special-parameter-types)
    * [Sizes](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#sizes)
    * [Durations](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#durations)
    * [Regular Expressions](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#regular-expressions)
      * [Standard regular expression settings for filters](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#standard-regular-expression-settings-for-filters)
    * [Enumerations](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#enumerations)
  * [Global Settings](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#global-settings)
    * [threads](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#threads)
    * [thread\_stack\_size](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#thread_stack_size)
    * [rebalance\_period](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#rebalance_period)
    * [rebalance\_threshold](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#rebalance_threshold)
    * [rebalance\_window](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#rebalance_window)
    * [skip\_name\_resolve](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#skip_name_resolve)
    * [auth\_connect\_timeout](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#auth_connect_timeout)
    * [auth\_read\_timeout](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#auth_read_timeout)
    * [auth\_write\_timeout](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#auth_write_timeout)
    * [query\_retries](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#query_retries)
    * [query\_retry\_timeout](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#query_retry_timeout)
    * [passive](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#passive)
    * [ms\_timestamp](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#ms_timestamp)
    * [skip\_permission\_checks](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#skip_permission_checks)
    * [syslog](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#syslog)
    * [maxlog](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#maxlog)
    * [log\_warning](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#log_warning)
    * [log\_notice](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#log_notice)
    * [log\_info](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#log_info)
    * [log\_debug](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#log_debug)
    * [log\_warn\_super\_user](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#log_warn_super_user)
    * [log\_messages](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#log_messages)
    * [log\_trace](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#log_trace)
    * [log\_augmentation](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#log_augmentation)
    * [log\_throttling](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#log_throttling)
    * [logdir](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#logdir)
    * [datadir](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#datadir)
    * [libdir](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#libdir)
    * [sharedir](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#sharedir)
    * [cachedir](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#cachedir)
    * [piddir](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#piddir)
    * [execdir](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#execdir)
    * [connector\_plugindir](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#connector_plugindir)
    * [persistdir](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#persistdir)
    * [module\_configdir](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#module_configdir)
    * [language](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#language)
    * [query\_classifier](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#query_classifier)
    * [query\_classifier\_cache\_size](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#query_classifier_cache_size)
    * [query\_classifier\_args](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#query_classifier_args)
      * [log\_unrecognized\_statements](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#log_unrecognized_statements)
    * [substitute\_variables](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#substitute_variables)
    * [sql\_mode](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#sql_mode)
    * [local\_address](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#local_address)
    * [users\_refresh\_time](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#users_refresh_time)
    * [users\_refresh\_interval](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#users_refresh_interval)
    * [retain\_last\_statements](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#retain_last_statements)
    * [dump\_last\_statements](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#dump_last_statements)
    * [session\_trace](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#session_trace)
    * [writeq\_high\_water](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#writeq_high_water)
    * [writeq\_low\_water](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#writeq_low_water)
    * [load\_persisted\_configs](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#load_persisted_configs)
    * [max\_auth\_errors\_until\_block](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#max_auth_errors_until_block)
    * [debug](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#debug)
    * [REST API Configuration](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#rest-api-configuration)
    * [admin\_host](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#admin_host)
    * [admin\_port](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#admin_port)
    * [admin\_auth](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#admin_auth)
    * [admin\_ssl\_key](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#admin_ssl_key)
    * [admin\_ssl\_cert](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#admin_ssl_cert)
    * [admin\_ssl\_ca\_cert](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#admin_ssl_ca_cert)
    * [admin\_ssl\_version](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#admin_ssl_version)
    * [admin\_enabled](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#admin_enabled)
    * [admin\_gui](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#admin_gui)
    * [admin\_secure\_gui](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#admin_secure_gui)
    * [admin\_log\_auth\_failures](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#admin_log_auth_failures)
    * [admin\_pam\_readwrite\_service and admin\_pam\_readonly\_service](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#admin_pam_readwrite_service-and-admin_pam_readonly_service)
  * [Events](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#events)
    * ['authentication\_failure'](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#authentication_failure)
  * [Service](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#service_1)
    * [router](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#router_1)
    * [router\_options](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#router_options)
    * [filters](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#filters)
    * [targets](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#targets)
    * [servers](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#servers)
    * [cluster](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#cluster)
    * [user and password](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#user-and-password)
    * [enable\_root\_user](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#enable_root_user)
    * [localhost\_match\_wildcard\_host](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#localhost_match_wildcard_host)
    * [version\_string](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#version_string)
    * [weightby](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#weightby)
    * [auth\_all\_servers](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#auth_all_servers)
    * [strip\_db\_esc](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#strip_db_esc)
    * [log\_auth\_warnings](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#log_auth_warnings)
    * [connection\_timeout](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#connection_timeout)
    * [max\_connections](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#max_connections)
    * [session\_track\_trx\_state](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#session_track_trx_state)
    * [retain\_last\_statements](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#retain_last_statements_1)
    * [connection\_keepalive](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#connection_keepalive)
    * [force\_connection\_keepalive](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#force_connection_keepalive)
    * [net\_write\_timeout](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#net_write_timeout)
  * [Server](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#server_1)
    * [address](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#address)
    * [port](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#port)
    * [socket](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#socket)
    * [monitoruser and monitorpw](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#monitoruser-and-monitorpw)
    * [extra\_port](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#extra_port)
    * [persistpoolmax](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#persistpoolmax)
    * [persistmaxtime](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#persistmaxtime)
    * [proxy\_protocol](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#proxy_protocol)
    * [disk\_space\_threshold](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#disk_space_threshold)
    * [rank](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#rank)
    * [priority](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#priority)
  * [Monitor](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#monitor_1)
  * [Listener](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#listener_1)
    * [service](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#service_2)
    * [protocol](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#protocol)
    * [address](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#address_1)
    * [port](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#port_1)
    * [socket](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#socket_1)
    * [authenticator](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#authenticator)
    * [authenticator\_options](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#authenticator_options)
    * [sql\_mode](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#sql_mode_1)
    * [connection\_init\_sql\_file](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#connection_init_sql_file)
* [Available Protocols](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#available-protocols)
  * [MariaDBClient](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#mariadbclient)
  * [CDC](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#cdc)
* [TLS/SSL encryption](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#tlsssl-encryption)
  * [ssl](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#ssl)
  * [ssl\_key](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#ssl_key)
  * [ssl\_cert](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#ssl_cert)
  * [ssl\_ca\_cert](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#ssl_ca_cert)
  * [ssl\_version](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#ssl_version)
  * [ssl\_cipher](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#ssl_cipher)
  * [ssl\_cert\_verify\_depth](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#ssl_cert_verify_depth)
  * [ssl\_verify\_peer\_certificate](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#ssl_verify_peer_certificate)
  * [ssl\_verify\_peer\_host](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#ssl_verify_peer_host)
  * [ssl\_crl](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#ssl_crl)
    * [Example SSL enabled server configuration](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#example-ssl-enabled-server-configuration)
    * [Example SSL enabled listener configuration](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#example-ssl-enabled-listener-configuration)
* [Module Types](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#module-types)
  * [Routing Modules](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#routing-modules)
  * [Monitor Modules](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#monitor-modules)
  * [Filter Modules](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#filter-modules)
* [Encrypting Passwords](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#encrypting-passwords)
  * [Creating Encrypted Passwords](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#creating-encrypted-passwords)
* [Runtime Configuration Changes](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#runtime-configuration-changes)
  * [Backing Up Configuration Changes](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#backing-up-configuration-changes)
* [Error Reporting](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#error-reporting)
* [Limitations](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#limitations)
* [Performance Optimization](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#performance-optimization)
* [Troubleshooting](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#troubleshooting)
  * [Systemd Watchdog](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#systemd-watchdog)

## Introduction

This document describes how to configure MariaDB MaxScale and presents some\
possible usage scenarios. MariaDB MaxScale is designed with flexibility in mind,\
and consists of an event processing core with various support functions and\
plugin modules that tailor the behavior of the program.

## Concepts

### Glossary

| Word                | Description                                                                                                                                                                                                                                                                                                                                      |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Word                | Description                                                                                                                                                                                                                                                                                                                                      |
| connection routing  | Connection routing is a method of handling requests in which MariaDB MaxScale will accept connections from a client and route data on that connection to a single database using a single connection. Connection based routing will not examine individual requests on a connection and it will not move that connection once it is established. |
| statement routing   | Statement routing is a method of handling requests in which each request within a connection will be handled individually. Requests may be sent to one or more servers and connections may be dynamically added or removed from the session.                                                                                                     |
| module              | A module is a separate code entity that may be loaded dynamically into MariaDB MaxScale to increase the available functionality. Modules are implemented as run-time loadable shared objects.                                                                                                                                                    |
| connection failover | When a connection currently being used between MariaDB MaxScale and the database server fails a replacement will be automatically created to another server by MariaDB MaxScale without client intervention                                                                                                                                      |
| backend database    | A term used to refer to a database that sits behind MariaDB MaxScale and is accessed by applications via MariaDB MaxScale.                                                                                                                                                                                                                       |
| REST API            | HTTP administrative interface                                                                                                                                                                                                                                                                                                                    |

### Objects

#### Server

A server represents an individual database server to which a client can be\
connected via MariaDB MaxScale. The status of a server varies during the lifetime\
of the server and typically the status is updated by some monitor. However, it\
is also possible to update the status of a server manually.

| Status                   | Description                                                                                                                                                                                                                                                                                                               |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Status                   | Description                                                                                                                                                                                                                                                                                                               |
| Running                  | The server is running.                                                                                                                                                                                                                                                                                                    |
| Master                   | The server is the master.                                                                                                                                                                                                                                                                                                 |
| Slave                    | The server is a slave.                                                                                                                                                                                                                                                                                                    |
| Draining                 | The server is being drained. Existing connections can continue to be used, but no new connections will be created to the server. Typically this status bit is turned on manually using maxctrl, but a monitor may also turn it on.                                                                                        |
| Drained                  | The server has been drained. The server was being drained and now the number of connections to the server has dropped to 0.                                                                                                                                                                                               |
| Auth Error               | The monitor cannot login and query the server due to insufficient privileges.                                                                                                                                                                                                                                             |
| Maintenance              | The server is under maintenance. Typically this status bit is turned on manually using maxctrl, but it will also be turned on for a server that for some reason is blocking connections from MaxScale. When a server is in maintenace mode, no connections will be created to it and existing connections will be closed. |
| Slave of External Master | The server is a slave of a master that is not being monitored.                                                                                                                                                                                                                                                            |

For more information on how to manually set these states via MaxCtrl, read the[Administration Tutorial](../maxscale-25-tutorials/mariadb-maxscale-25-mariadb-maxscale-administration-tutorial.md).

#### Monitor

A monitor module is capable of monitoring the state of a particular kind\
of cluster and making that state available to the routers of MaxScale.

Examples of monitor modules are `mariadbmon` that is capable of monitoring\
a regular master-slave cluster and in addition of performing both _switchover_\
and _failover_, `galeramon` that is capable of monitoring a Galera cluster,`csmon` that is capable of monitoring a Columnstore cluster and `clustrixmon`\
that is capable of monitoring a Clustrix cluster.

Monitor modules have sections of their own in the MaxScale configuration\
file.

#### Filter

A filter module resides in front of routers in the request processing chain\
of MaxScale. That is, a filter will see a request before it reaches the router\
and before a response is sent back to the client. This allows filters to\
reject, handle, alter or log information about a request.

Examples of filters are `dbfwfilter` that is a configurable firewall, `cache`\
that provides query caching according to rules, `regexfilter` that can rewrite\
requests according to regular expressions, and `qlafilter` that logs\
information about requests.

Filters have sections of their own in the MaxScale configuration file that are\
referred to from _services_.

#### Router

A router module is capable of routing requests to backend servers according to\
the characteristics of a request and/or the algorithm the router\
implements. Examples of routers are `readconnroute` that provides _connection_\
\&#xNAN;_routing_, that is, the server is chosen according to specified rules when the\
session is created and all requests are subsequently routed to that server,\
and `readwritesplit` that provides _statement routing_, that is, each\
individual request is routed to the most appropriate server.

Routers do not have sections of their own in the MaxScale configuration file,\
but are referred to from _services_.

#### Service

A service abstracts a set of databases and makes them appear as a single one\
to the client. Depending on what router (e.g. `readconnroute` or`readwritesplit`) the service uses, the servers are used in some particular\
way. If the service uses filters, then all requests will be pre-processed in\
some way before they reach the router.

Services have sections of their own in the MaxScale configuration file.

#### Listener

A listener defines a port MaxScale listens on. Connection requests arriving on\
that port will be forwarded to the service the listener is associated with. A\
listener may be associated with a single service, but several listeners may be\
associated with the same service.

Listeners have sections of their own in the MaxScale configuration file.

## Administration

The administation of MaxScale can be divided in two parts:

* Writing the MaxScale configuration file, which is described in the following[section](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#configuration).
* Performing runtime modifications using [MaxCtrl](../maxscale-25-reference/mariadb-maxscale-25-maxctrl.md)

For detailed information about _MaxCtrl_ please refer to the specific\
documentation referred to above. In the following it will only be explained how\
MaxCtrl relate to each other, as far as user credentials go.

**Note**: By default all runtime configuration changes are saved on disk and\
loaded on startup. Refer to the[Dynamic Configuration](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#dynamic-configuration) section for more details\
on how it works and how to disable it.

MaxCtrl can connect using TCP/IP sockets. When connecting with MaxCtrl using\
TCP/IP sockets, the user and password must be provided and are checked against a\
separate user credentials database. By default, that database contains the user`admin` whose password is `mariadb`.

Note that if MaxCtrl is invoked without explicitly providing a user and password\
then it will by default use `admin` and `mariadb`. That means that when the\
default user is removed, the credentials must always be provded.

### Static Configuration Parameters

The following list of global configuration parameters can **NOT** be changed at\
runtime and can only be defined in a configuration file:

* `admin_auth`
* `admin_enabled`
* `admin_gui`
* `admin_host`
* `admin_pam_readonly_service`
* `admin_pam_readwrite_service`
* `admin_port`
* `admin_secure_gui`
* `admin_ssl_ca_cert`
* `admin_ssl_cert`
* `admin_ssl_key`
* `admin_ssl_version`
* `cachedir`
* `connector_plugindir`
* `datadir`
* `debug`
* `execdir`
* `language`
* `libdir`
* `load_persisted_configs`
* `local_address`
* `log_augmentation`
* `log_warn_super_user`
* `logdir`
* `module_configdir`
* `persistdir`
* `piddir`
* `query_classifier_args`
* `query_classifier`
* `query_retries`
* `sql_mode`
* `sharedir`
* `substitute_variables`
* `threads`

All other parameters that relate to objects can be altered at runtime or can be\
changed by destroying and recreating the object in question.

## Configuration

The MariaDB MaxScale configuration is read from a file that MariaDB MaxScale\
will look for in the following places:

1. By default, the file `maxscale.cnf` in the directory `/etc`
2. The location given with the `--configdir=<path>` command line argument.

MariaDB MaxScale will further look for a directory with the same name as the\
configuration file, followed by `.d` (for instance `/etc/maxscale.cnf.d`) and\
recursively read all files, having a `.cnf` suffix, it finds in the directory\
hierarchy. All other files will be ignored.

There are no restrictions on how different configuration sections are arranged,\
but the strong suggestion is to place global settings into the configuration\
file MariaDB MaxScale is invoked with, and then, if deemed necessary, create\
separate configuration files for _servers_, _filters_, etc.

The configuration file itself is based on the[.ini](https://en.wikipedia.org/wiki/INI_file) file format and consists of\
various sections that are used to build the configuration; these sections define\
services, servers, listeners, monitors and global settings. Parameters, which\
expect a comma-separated list of values can be defined on multiple lines. The\
following is an example of a multi-line definition.

```
[MyService]
type=service
router=readconnroute
servers=server1,
        server2,
        server3
```

The values of the parameter that are not on the first line need to have at least\
one whitespace character before them in order for them to be recognized as a\
part of the multi-line parameter.

Comments are defined by prefixing a row with a hash (`#`). Trailing comments are\
not supported.

```
# This is a comment before a parameter
some_parameter=123
```

### Names

Section names may not contain whitespace and must not start with the characters`@@`, but otherwise there are no restrictions.

### Dynamic Configuration

By default all changes done at runtime via the MaxScale GUI, MaxCtrl or the REST\
API will be saved on disk, inside the [persistdir](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#persistdir) directory. The\
changes done at runtime will override the configuration found in the static\
configuration files for that particular object.

This means that if an object that is found in `/etc/maxscale.cnf` is modified at\
runtime, all future changes to it must also be done at runtime. Any\
modifications done to `/etc/maxscale.cnf` after a runtime change has been made\
are ignored for that object.

To prevent the saving of runtime changes and to make all runtime changes\
volatile, add [load\_persisted\_configs=false](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#load_persisted_configs) under\
the `[maxscale]` section. This will make MaxScale behave like the MariaDB server\
does: any changes done with `SET GLOBAL` statements are lost if the process is\
restarted.

### Special Parameter Types

#### Sizes

Where _specifically noted_, a number denoting a size can be suffixed by a subset\
of the IEC binary prefixes or the SI prefixes. In the former case the number\
will be interpreted as a certain multiple of 1024 and in the latter case as a\
certain multiple of 1000. The supported IEC binary suffixes are `Ki`, `Mi`, `Gi`\
and `Ti` and the supported SI suffixes are `k`, `M`, `G` and `T`. In both cases,\
the matching is case insensitive.

For instance, the following entries

```
max_size=1099511628000
max_size=1073741824Ki
max_size=1048576Mi
max_size=1024Gi
max_size=1Ti
```

are equivalent, as are the following

```
max_size=1000000000000
max_size=1000000000k
max_size=1000000M
max_size=1000G
max_size=1T
```

#### Durations

A number denoting a duration can be suffixed by one of the case-insensitive\
suffixes `h`, `m` or `min`, `s` and `ms`, for specifying durations in hours,\
minutes, seconds and milliseconds, respectively.

For instance, the following entries

```
soft_ttl=1h
soft_ttl=60m
soft_ttl=60min
soft_ttl=3600s
soft_ttl=3600000ms
```

are equivalent.

Note that if an explicit unit is not specified, then it is specific to the\
configuration parameter whether the duration is interpreted as seconds or\
milliseconds.

_Not_ providing an explicit unit has been deprecated in MaxScale 2.4.

#### Regular Expressions

Many modules have settings which accept a regular expression. In most cases, these\
settings are named either _match_ or _exclude_, and are used to filter users or queries.\
MaxScale uses the [PCRE2-library](https://www.pcre.org/current/doc/html/) for matching\
regular expressions.

When writing a regular expression (regex) type parameter to a MaxScale configuration file,\
the pattern string should be enclosed in slashes e.g. `^select` -> `match=/^select/`. This\
clarifies where the pattern begins and ends, even if it includes whitespace. Without\
slashes the configuration loader trims the pattern from the ends. The slashes are removed\
before compiling the pattern. For backwards compatibility, the slashes are not yet\
mandatory. Omitting them is, however, deprecated and will be rejected in a future release\
of MaxScale. Currently, _binlogfilter_, _ccrfilter_, _qlafilter_, _tee_ and _avrorouter_\
accept parameters in this type of regular expression form. Some other modules may not\
handle the slashes yet correctly.

PCRE2 supports a complicated regular expression[syntax](https://www.pcre.org/current/doc/html/pcre2syntax.html). MaxScale typically uses\
regular expressions simply, only checking whether the pattern and subject match at some\
point. For example, using the QLAFilter and setting `match=/SELECT/` causes the filter to\
accept any query with the text "SELECT" somewhere within. To force the pattern to only\
match at the beginning of the query, set `match=/^SELECT/`. To only match the end, set`match=/SELECT$/`.

Modules which accept regular expression parameters also often accept options which affect\
how the patterns are compiled. Typically, this setting is called _options_ and accepts\
values such as `ignorecase`, `case` and `extended`.

* `ignorecase`: Causes the regular expression matcher to ignore letter case, and\
  is often on by default. When enabled, `/SELECT/` would match both `SELECT` and`select`.
* `extended`: Ignores whitespace and `#` comments in the pattern. Note that this\
  is not the same as the extended regular expression syntax that for example`grep -E` uses.
* `case`: Turns on case-sensitive matching. This means that `/SELECT/` will not\
  match `select`.

These settings can also be defined in the pattern itself, so they can be\
used even in modules without pattern compilation settings. The pattern\
settings are `(?i)` for `ignorecase` and `(?x)` for `extended`. See the[PCRE2 syntax documentation](https://www.pcre.org/current/doc/html/pcre2syntax.html#SEC16)\
for more information.

**Standard regular expression settings for filters**

Many filters use the settings _match_, _exclude_ and _options_. Since these settings are\
used in a similar way across these filters, the settings are explained here. The\
documentation of the filters link here and describe any exceptions to this\
generalized explanation.

These settings typically limit the queries the filter module acts on. _match_ an&#x64;_&#x65;xclude_ define PCRE2 regular expression patterns while _options_ affects how both of the\
patterns are compiled. _options_ works as explained above, accepting the values`ignorecase`, `case` and `extended`, with `ignorecase` being the default.

The queries are matched as they arrive to the filter on their way to a routing module. I&#x66;_&#x6D;atch_ is defined, the filter only acts on queries matching that pattern. If _match_ is\
not defined, all queries are considered to match.

If _exclude_ is defined, the filter only acts on queries not matching that pattern. I&#x66;_&#x65;xclude_ is not defined, nothing is excluded.

If both are defined, the query needs to match _match_ but not match _exclude_.

Even if a filter does not act on a query, the query is not lost. The query is simply\
passed on to the next module in the processing chain as if the filter was not there.

#### Enumerations

Enumeration type parameters have a pre-defined set of accepted values. For types\
declared as `enum`, only one value is accepted. For `enum_mask` types, multiple\
values can be defined by separating them with commas. All enumeration values in\
MaxScale are case-sensitive.

For example the `router_options` parameter in the `readconnroute` router is a\
mask type enumeration:

```
router_options=master,slave
```

### Global Settings

The global settings, in a section named `[MaxScale]`, allow various parameters\
that affect MariaDB MaxScale as a whole to be tuned. This section must be\
defined in the root configuration file which by default is `/etc/maxscale.cnf`.

#### `threads`

This parameter controls the number of worker threads that are handling the\
events coming from the kernel. The default is 1 thread. It is recommended that\
you start with one thread and increase the number if you require greater\
performance. Increasing the amount of worker threads beyond the number of\
processor cores does not improve the performance, rather is likely to degrade\
it, and can consume resources needlessly.

You can enable automatic configuration of this value by setting the value to`auto`. This way MariaDB MaxScale will detect the number of available processors\
and set the amount of threads to be equal to that number. This should only be\
used for systems dedicated for running MariaDB MaxScale.

The maximum value for threads is 100.

```
# Valid options are:
#       threads=[<number of threads> | auto ]

[MaxScale]
threads=1
```

Additional threads will be created to execute other internal services within\
MariaDB MaxScale. This setting is used to configure the number of threads that\
will be used to manage the user connections.

#### `thread_stack_size`

Ignored and deprecated in 2.3.

If you need to explicitly set the stack size, do so using `ulimit -s` before\
starting MaxScale.

#### `rebalance_period`

This duration parameter controls how often the load of the worker threads\
should be checked. The default value is 0, which means that no checks and\
no rebalancing will be performed.

```
rebalance_period=10s
```

Note that the value of `rebalance_period` should not be smaller than the\
value of `rebalance_window` whose default value is 10.

**NOTE** The rebalancing functionality is currently disabled and an attempt\
to enable it will be ignored.

If the value of `rebalance_period` is significantly shorter than that\
of `rebalance_window`, it may lead to oscillation where work is constantly\
moved from one thread to another.

#### `rebalance_threshold`

This integer parameter controls at which point MaxScale should start\
moving work from one worker thread to another.

If the difference in load between the thread with the maximum load and\
the thread with the minimum load is larger than the value of this parameter,\
then work will be moved from the former to the latter.

Although the load of a thread can vary between 0 and 100, the value of this\
parameter must be between 5 and 100. The default value is 20.

```
rebalance_threshold=15
```

Note that rebalancing will not be performed unless `rebalance_period`\
has been specified.

#### `rebalance_window`

This integer parameter controls how many seconds of load should be\
taken into account when deciding whether work should be moved from\
one thread to another.

The default value is 10, which means that the load during the last 10\
seconds is considered when deciding whether work should be moved.

The minimum value is 1 and the maximum 60.

#### `skip_name_resolve`

* Type: boolean
* Default: false
* Dynamic: Yes

This parameter controls whether reverse domain name lookups are made to convert\
client IP addresses to hostnames. If enabled, client IP addresses will not be\
resolved to hostnames during authentication or for the REST API even if requested.

If you have database users that use a hostname in the host part of the user\
(i.e. `'user'@'my-hostname.org'`), a reverse lookup on the client IP address is\
done to see if it matches the host. Reverse DNS lookups can be very slow which\
is why it is recommended that they are disabled and that users are defined using\
an IP address.

#### `auth_connect_timeout`

Duration, default 10s. This setting defines the connection timeout when\
attempting to fetch MariaDB/MySQL/Clustrix users from a backend server. The same\
value is also used for read and write timeouts. Increasing this value causes\
MaxScale to wait longer for a response from a server before user fetching fails.\
Other servers may then be attempted.

```
auth_connect_timeout=10s
```

The value is given as [a duration](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#durations). If no explicit unit is provided,\
the value is interpreted as seconds. In subsequent versions a value without a\
unit may be rejected. Since the granularity of the timeout is seconds, a timeout\
specified in milliseconds will be rejected even if the given value is longer\
than a second.

#### `auth_read_timeout`

Deprecated and ignored as of MaxScale 2.5.0. See _auth\_connect\_timeout_ above.

#### `auth_write_timeout`

Deprecated and ignored as of MaxScale 2.5.0. See _auth\_connect\_timeout_ above.

#### `query_retries`

The number of times an interrupted internal query will be retried. The default\
is to retry the query once. This feature was added in MaxScale 2.1.10 and was\
disabled by default until MaxScale 2.3.0.

An interrupted query is any query that is interrupted by a network\
error. Connection timeouts are included in network errors and thus is it\
advisable to make sure that the value of `query_retry_timeout` is set to an\
adequate value. Internal queries are only used to retrieve authentication data\
and monitor the servers.

#### `query_retry_timeout`

The total timeout in seconds for any retried queries. The default value is 5\
seconds.

An interrupted query is retried for either the configured amount of attempts or\
until the configured timeout is reached.

The value is specified as documented [here](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#durations). If no explicit unit\
is provided, the value is interpreted as seconds in MaxScale 2.4. In subsequent\
versions a value without a unit may be rejected. Note that since the granularity\
of the timeout is seconds, a timeout specified in milliseconds will be rejected,\
even if the duration is longer than a second.

#### `passive`

Controls whether MaxScale is a passive node in a cluster of multiple MaxScale\
instances. The default value is false.

This parameter is intended to be used with multiple MaxScale instances that use\
failover functionality to manipulate the cluster in some form. Passive nodes\
only observe the clusters being monitored and take no direct actions.

The following functionality is disabled when passive mode is enabled:

* Automatic failover in the `mariadbmon` module
* Automatic rejoin in the `mariadbmon` module
* Launching of monitor scripts

**NOTE:** Even if MaxScale is in passive mode, it will still accept clients and\
route any traffic sent to it. The **only** operations affected by the passive\
mode are the ones listed above.

#### `ms_timestamp`

Enable or disable the high precision timestamps in logfiles. Enabling this adds\
millisecond precision to all logfile timestamps.

```
# Valid options are:
#       ms_timestamp=<0|1>
ms_timestamp=1
```

#### `skip_permission_checks`

Skip service and monitor user permission checks. This is useful when you know\
the permissions are OK and you want to speed up the startup process. This\
parameter takes a boolean value and is disabled by default.

It is recommended to not disable the permission checks so that any missing\
privileges are detected when maxscale is starting up. If you are experiencing a\
slow startup of MaxScale due to large amounts of connection timeouts when\
permissions are checked, disabling the permission checks could speed up the\
startup process.

```
skip_permission_checks=true
```

#### `syslog`

Enable or disable the logging of messages to _syslog_.

By default logging to _syslog_ is enabled.

```
# Valid options are:
#       syslog=<0|1>
syslog=1
```

To enable logging to syslog use the value 1 and to disable use the value 0.

#### `maxlog`

Enable to disable to logging of messages to MariaDB MaxScale's log file.

By default logging to _maxlog_ is enabled.

```
# Valid options are:
#       syslog=<0|1>
maxlog=1
```

To enable logging to the MariaDB MaxScale log file use the value 1 and to\
disable use the value 0.

#### `log_warning`

Enable or disable the logging of messages whose syslog priority is _warning_.\
Messages of this priority are enabled by default.

```
# Valid options are:
#       log_warning=<0|1>
log_warning=0
```

To disable these messages use the value 0 and to enable them use the value 1.

#### `log_notice`

Enable or disable the logging of messages whose syslog priority is _notice_.\
Messages of this priority provide information about the functioning of MariaDB\
MaxScale and are enabled by default.

```
# Valid options are:
#       log_notice=<0|1>
log_notice=0
```

To disable these messages use the value 0 and to enable them use the value 1.

#### `log_info`

Enable or disable the logging of messages whose syslog priority is _info_. These\
messages provide detailed information about the internal workings of MariaDB\
MaxScale and should not, due to their frequency, be enabled, unless there is a\
specific reason for that. For instance, from these messages it will be evident,\
e.g., why a particular query was routed to the master instead of to a slave.\
These informational messages are disabled by default.

```
# Valid options are:
#       log_info=<0|1>
log_info=1
```

To disable these messages use the value 0 and to enable them use the value 1.

#### `log_debug`

Enable or disable the logging of messages whose syslog priority is _debug_. This\
kind of messages are intended for development purposes and are disabled by\
default. Note that if MariaDB MaxScale has been built in release mode, then\
debug messages are excluded from the build and this setting will not have any\
effect.

```
# Valid options are:
#       log_debug=<0|1>
log_debug=1
```

To disable these messages use the value 0 and to enable them use the value 1.

#### `log_warn_super_user`

Boolean, default:false. When enabled, a warning is logged whenever a client with\
SUPER-privilege successfully authenticates. This also applies to\
COM\_CHANGE\_USER-commands. The setting is intended for diagnosing situations\
where a client interferes with a master server switchover. Super-users bypass\
the _read\_only_-flag which switchover uses to block writes to the master. This\
setting cannot be modified during runtime.

#### `log_messages`

**Deprecated** Use _log\_notice_ instead.

#### `log_trace`

**Deprecated** Use _log\_info_ instead.

#### `log_augmentation`

Enable or disable the augmentation of messages. If this is enabled, then each\
logged message is appended with the name of the function where the message was\
logged. This is primarily for development purposes and hence is disabled by\
default.

```
# Valid options are:
#       log_augmentation=<0|1>
log_augmentation=1
```

To disable the augmentation use the value 0 and to enable it use the value 1.

#### `log_throttling`

It is possible that a particular error (or warning) is logged over and over\
again, if the cause for the error persistently remains. To prevent the log from\
flooding, it is possible to specify how many times a particular error may be\
logged within a time period, before the logging of that error is suppressed for\
a while.

```
# A valid value looks like
#       log_throttling = X, Y, Z
#
# where the first value X is a positive integer and means the number of times
# a specific error may be logged within a duration of Y, before the logging
# of that error is suppressed for a duration of Z.
log_throttling=8, 2s, 15000ms
```

In the example above, the logging of a particular error will be suppressed for\
15 seconds if the error has been logged 8 times in 2 seconds.

The default is `10, 1000ms, 10000ms`, which means that if the same error is\
logged 10 times in one second, the logging of that error is suppressed for the\
following 10 seconds.

To disable log throttling, add an entry with an empty value

```
log_throttling=
```

or one where any of the integers is 0.

```
log_throttling=0, 0, 0
```

The durations can be specified as documented [here](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#durations). If no explicit\
unit is provided, the value is interpreted as milliseconds in MaxScale 2.4. In\
subsequent versions a value without a unit may be rejected.

Note that _notice_, _info_ and _debug_ messages are never throttled.

#### `logdir`

Set the directory where the logfiles are stored. The folder needs to be both\
readable and writable by the user running MariaDB MaxScale.

The default value is `/var/log/maxscale/`.

```
logdir=/var/log/maxscale/
```

#### `datadir`

Set the directory where the data files used by MariaDB MaxScale are stored.\
Modules can write to this directory and for example the binlogrouter uses this\
folder as the default location for storing binary logs.

This is also the directory where the password encryption key is read from that\
is generated by `maxkeys`.

The default value is `/var/lib/maxscale/`.

```
datadir=/var/lib/maxscale/
```

#### `libdir`

Set the directory where MariaDB MaxScale looks for modules. The library\
directory is the only directory that MariaDB MaxScale uses when it searches for\
modules. If you have custom modules for MariaDB MaxScale, make sure you have\
them in this folder.

The default value depends on the operating system. For RHEL versions the value\
is `/usr/lib64/maxscale/`. For Debian and Ubuntu it is`/usr/lib/x86_64-linux-gnu/maxscale/`

```
libdir=/usr/lib64/maxscale/
```

#### `sharedir`

Sets the directory where static data assets are loaded.

The MaxScale GUI static files are located in the `gui/` subdirectory. If the GUI\
files have been manually moved somewhere else, this path must be configured to\
point to the parent directory of the `gui/` subdirectory.

The MaxScale REST API only serves files for the GUI that are located in the`gui/` subdirectory of the configured `sharedir`. Any files whose real path\
resolves to outside of this directory are not served by the MaxScale GUI: this\
is done to prevent other files from being accessible via the MaxScale REST\
API. This means that path to the GUI source directory can contain symbolic links\
but all parts after the `/gui/` directory must reside inside it.

The default value is `/usr/share/maxscale/`.

#### `cachedir`

Configure the directory MariaDB MaxScale uses to store cached data.

The default value is `/var/cache/maxscale/`.

```
cachedir=/var/cache/maxscale/
```

#### `piddir`

Configure the directory for the PID file for MariaDB MaxScale. This file\
contains the Process ID for the running MariaDB MaxScale process.

The default value is `/var/run/maxscale/`.

```
piddir=/var/run/maxscale/
```

#### `execdir`

Configure the directory where the executable files reside. All internal\
processes which are launched will use this directory to look for executable\
files.

The default value is `/usr/bin/`.

```
execdir=/usr/bin/
```

#### `connector_plugindir`

Location of the MariaDB Connector-C plugin directory. The MariaDB Connector-C\
used in MaxScale can use this directory to load authentication plugins. The\
versions of the plugins must be binary compatible with the connector version\
that MaxScale was built with.

The default value is `/usr/lib/mysql/plugin/`.

```
connector_plugindir=/usr/lib/mysql/plugin/
```

#### `persistdir`

Configure the directory where persisted configurations are stored. When a new\
object is created via MaxCtrl, it will be stored in this directory. Do not use\
this directory for normal configuration files, use _/etc/maxscale.cnf.d/_\
instead. The user MaxScale is running as must be able to write into this\
directory.

The default value is `/var/lib/maxscale/maxscale.cnf.d/`.

```
persistdir=/var/lib/maxscale/maxscale.cnf.d/
```

#### `module_configdir`

Configure the directory where module configurations are stored. Path arguments\
are resolved relative to this directory. This directory should be used to store\
module specific configurations e.g. dbfwfilter rule files.

Any configuration parameter that is not an absolute path will be interpreted as\
a relative path. The relative paths use the module configuration directory as\
the working directory.

For example, the configuration parameter `file=my_file.txt` would be interpreted\
as `/etc/maxscale.modules.d/my_file.txt` whereas `file=/home/user/my_file.txt` would\
be interpreted as `/home/user/my_file.txt`.

The default value is `/etc/maxscale.modules.d/`.

```
module_configdir=/etc/maxscale.modules.d/
```

#### `language`

Set the folder where the errmsg.sys file is located in. MariaDB MaxScale will\
look for the errmsg.sys file installed with MariaDB MaxScale from this folder.

The default value is `/var/lib/maxscale/`.

```
language=/var/lib/maxscale/
```

#### `query_classifier`

The module used by MariaDB MaxScale for query classification. The information\
provided by this module is used by MariaDB MaxScale when deciding where a\
particular statement should be sent. The default query classifier i&#x73;_&#x71;c\_sqlite_.

#### `query_classifier_cache_size`

Specifies the maximum size of the query classifier cache. The default limit is\
15% of total system memory starting with MaxScale 2.3.7. In older versions the\
default limit was 40% of total system memory. This feature was added in MaxScale\
2.3.0.

When the query classifier cache has been enabled, MaxScale will, after a\
statement has been parsed, store the classification result using the\
canonicalized version of the statement as the key.

If the classification result for a statement is needed, MaxScale will first\
canonicalize the statement and check whether the result can be found in the\
cache. If it can, the statement will not be parsed at all but the cached result\
is used.

The configuration parameter takes one integer that specifies the maximum size of\
the cache. The size of the cache can be specifed as explained [here](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#sizes).

```
# 1MB query classifier cache
query_classifier_cache_size=1MB
```

Note that MaxScale uses a separate cache for each worker thread. To obtain the\
amount of memory available for each thread, divide the cache size with the value\
of `threads`. If statements are evicted from the cache (visible in the\
diagnostic output), consider increasing the cache size.

Note also that limit is not a hard limit, but an approximate one. Namely, although\
the memory needed for storing the canonicalized statement and the classification\
result is correctly accounted for, there is additional overhead whose size is not\
exactly known and over which we do not have direct control.

Using `maxctrl show threads` it is possible to check what the actual size of\
the cache is and to see performance statistics.

| Key                | Meaning                                                                                                                 |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------- |
| Key                | Meaning                                                                                                                 |
| QC cache size      | The current size of the cache (bytes).                                                                                  |
| QC cache inserts   | How many entries have been inserted into the cache.                                                                     |
| QC cache hits      | How many times the classification result has been found from the cache.                                                 |
| QC cache misses    | How many times the classification result has not been found from the cache, but the classification had to be performed. |
| QC cache evictions | How many times a cache entry has had to be removed from the cache, in order to make place for another.                  |

#### `query_classifier_args`

Arguments for the query classifier. What arguments are accepted depends on the\
particular query classifier being used. The default query classifier -_qc\_sqlite_ - supports the following arguments:

**`log_unrecognized_statements`**

An integer argument taking the following values:

* 0: Nothing is logged. This is the default.
* 1: Statements that cannot be parsed completely are logged. They may have been\
  partially parsed, or classified based on keyword matching.
* 2: Statements that cannot even be partially parsed are logged. They may have\
  been classified based on keyword matching.
* 3: Statements that cannot even be classified by keyword matching are logged.

```
query_classifier=qc_sqlite
query_classifier_args=log_unrecognized_statements=1
```

This will log all statements that cannot be parsed completely. This may be\
useful if you suspect that MariaDB MaxScale routes statements to the wrong\
server (e.g. to a slave instead of to a master).

#### `substitute_variables`

Enable or disable the substitution of environment variables in the MaxScale\
configuration file. If the substitution of variables is enabled and a\
configuration line like

```
some_parameter=$SOME_VALUE
```

is encountered, then `$SOME_VALUE` will be replaced with the actual value\
of the environment variable `SOME_VALUE`. Note:_Variable substitution will be made only if '$' is the first character_\
\&#xNAN;_of the value._ _Everything_ following '$' is interpreted as the name of the environment\
variable.

* Referring to a non-existing environment variable is a fatal error.

By default, the value of `substitute_variables` is `false`.

```
substitute_variables=true
```

The setting of `substitute_variables` will have an effect on all parameters\
in the all other sections, irrespective of where the `[maxscale]` section\
is placed in the configuration file. However, in the `[maxscale]` section,\
to ensure that substitution will take place, place the`substitute_variables=true` line first.

#### `sql_mode`

Specifies whether the query classifier parser should initially expect _MariaDB_\
or _PL/SQL_ kind of SQL.

The allowed values are:`default`: The parser expects regular _MariaDB_ SQL.`oracle` : The parser expects PL/SQL.

```
sql_mode=oracle
```

The default value is `default`.

**NOTE** If `sql_mode` is set to `oracle`, then MaxScale will also assume\
that `autocommit` initially is off.

At runtime, MariaDB MaxScale will recognize statements like

```
set sql_mode=oracle;
```

and

```
set sql_mode=default;
```

and change mode accordingly.

**NOTE** If `set sql_mode=oracle;` is encountered, then MaxScale will also\
behave as if `autocommit` had been turned off and conversely, if`set sql_mode=default;` is encountered, then MaxScale will also behave\
as if `autocommit` had been turned on.

Note that MariaDB MaxScale is **not** explicitly aware of the sql mode of\
the server, so the value of `sql_mode` should reflect the sql mode used\
when the server is started.

#### `local_address`

What specific local address/interface to use when connecting to servers.

This can be used for ensuring that MaxScale uses a particular interface\
when connecting to servers, in case the computer MaxScale is running on\
has multiple interfaces.

```
local_address=192.168.1.254
```

#### `users_refresh_time`

How often, in seconds, MaxScale at most may refresh the users from the\
backend server.

MaxScale will at startup load the users from the backend server, but if\
the authentication of a user fails, MaxScale assumes it is because a new\
user has been created and will thus refresh the users. By default, MaxScale\
will do that at most once per 30 seconds and with this configuration option\
that can be changed. A value of 0 allows infinite refreshes and a negative\
value disables the refreshing entirely.

```
users_refresh_time=120s
```

The value is specified as documented [here](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#durations). If no explicit unit\
is provided, the value is interpreted as seconds in MaxScale 2.4. In subsequent\
versions a value without a unit may be rejected. Note that since the granularity\
of the timeout is seconds, a timeout specified in milliseconds will be rejected,\
even if the duration is longer than a second.

In MaxScale 2.3.9 and older versions, the minimum allowed value was 10 seconds\
but, due to a bug, the default value was 0 which allowed infinite refreshes.

#### `users_refresh_interval`

How often, in seconds, MaxScale will automatically refresh the users from the\
backend server.

This configuration is used to periodically refresh the backend users, making sure\
they are up to date. The default value for this setting is 0, meaning the users\
are not periodically refreshed. However, they can still be refreshed in case of\
failed authentication depending on `users_refresh_time`.

```
users_refresh_interval=2h
```

The value is specified as documented [here](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#durations). If no explicit unit\
is provided, the value is interpreted as seconds in MaxScale 2.4.

#### `retain_last_statements`

How many statements MaxScale should store for each session. This is for\
debugging purposes, as in case of problems it is often of value to be able\
to find out exactly what statements were sent before a particular\
problem turned up.

**Note:** See also `dump_last_statements` using which the actual dumping\
of the statements is enabled. Unless both of the parameters are defined,\
the statement dumping mechanism doesn't work.

```
retain_last_statements=20
```

Default is `0`.

#### `dump_last_statements`

With this configuration item it is specified in what circumstances MaxScale\
should dump the last statements that a client sent. The allowed values are`never`, `on_error` and `on_close`. With `never` the statements are never\
logged, with `on_error` they are logged if the client closes the connection\
improperly, and with `on_close` they are always logged when a client session\
is closed.

```
dump_last_statements=on_error
```

Default is `never`.

Note that you need to specify with `retain_last_statements` how many statements\
MaxScale should retain for each session. Unless it has been set to another value\
than `0`, this configuration setting will not have an effect.

#### `session_trace`

How many log entries are stored in the session specific trace log. This log is\
written to disk when a session ends abnormally and can be used for debugging\
purposes. It would be good to enable this if a session is disconnected and the\
log is not detailed enough. In this case the info log might reveal the true\
cause of why the connection was closed.

```
session_trace=20
```

Default is `0`.

The session trace log is also exposed by REST API and is shown with`maxctrl show sessions`.

#### `writeq_high_water`

High water mark for network write buffer. When the size of the outbound network\
buffer in MaxScale for a single connection exceeds this value, network traffic\
throtting for that connection is started. The parameter accepts[size type values](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#sizes). The default value is 16777216 bytes.

More specifically, if the client side write queue is above this value, it will\
block traffic coming from backend servers. If the backend side write queue is\
above this value, it will block traffic from client.

The buffer that this parameter controls is the buffer internal to MaxScale and\
is not the kernel TCP send buffer. This means that the total amount of buffered\
data is determined by both the kernel TCP buffers and the value of`writeq_high_water`.

Network throttling is only enabled when both `writeq_high_water` and`writeq_low_water` have a non-zero value. To disable throttling, set the value\
to 0.

#### `writeq_low_water`

Low water mark for network write buffer. Once the traffic throttling is enabled,\
it will only be disabled when the network write buffer is below`writeq_low_water` bytes. The parameter accepts [size type values](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#sizes). The\
default value is 8192 bytes.

The value of `writeq_high_water` must always be greater than the value of`writeq_low_water`.

Network throttling is only enabled when both `writeq_high_water` and`writeq_low_water` have a non-zero value. To disable throttling, set the value\
to 0.

#### `load_persisted_configs`

Load persisted runtime changes on startup. This parameter accepts boolean values\
and is enabled by default. This parameter was added in MaxScale 2.3.6.

All runtime configuration changes are persisted in generated configuration files\
located by default in `/var/lib/maxscale/maxscale.cnf.d/` and are loaded on\
startup after main configuration files have been read. To make runtime\
configurations volatile (i.e. they are lost when maxscale is restarted), use`load_persisted_configs=false`. All changes are still persisted since it stores\
the current runtime state of MaxScale. This makes problem analysis easier if an\
unexpected outage happens.

#### `max_auth_errors_until_block`

The maximum number of authentication failures that are tolerated before a host\
is temporarily blocked. The default value is 10 failures. After a host is\
blocked, connections from it are rejected for 60 seconds. To disable this\
feature, set the value to 0.

Note that the configured value is not a hard limit. The number of tolerated\
failures is between `max_auth_errors_until_block` and `threads * max_auth_errors_until_block` where `max_auth_errors_until_block` is the\
configured value of this parameter and `threads` is the number of configured\
threads.

#### `debug`

Define debug options from the --debug command line option. Either the command\
line option or the parameter should be used, not both. The debug options are\
only for testing purposes and are not to be used in production.

#### REST API Configuration

The MaxScale REST API is an HTTP interface that provides JSON format data\
intended to be consumed by monitoring appllications and visualization tools.

The following options must be defined under the `[maxscale]` section in the\
configuration file.

#### `admin_host`

The network interface where the REST API listens on. The default value is the\
IPv4 address `127.0.0.1` which only listens for local connections.

#### `admin_port`

The port where the REST API listens on. The default value is port 8989.

#### `admin_auth`

Enable REST API authentication using HTTP Basic Access\
authentication. This is not a secure method of authentication without HTTPS but\
it does add a small layer of security. This option is enabled by default.

For more information, read the [REST API documentation](../maxscale-25-rest-api/mariadb-maxscale-25-rest-api.md).

#### `admin_ssl_key`

The path to the TLS private key in PEM format for the admin interface.

If the `admin_ssl_key` and `admin_ssl_cert` options are all defined, the admin\
interface will use encrypted HTTPS instead of plain HTTP.

#### `admin_ssl_cert`

The path to the TLS public certificate in PEM format. See `admin_ssl_key`\
documentation for more details.

#### `admin_ssl_ca_cert`

The path to the TLS CA certificate in PEM format. If defined, the client\
certificate, if provided, will be validated against it. This parameter is\
optional starting with MaxScale 2.3.19.

#### `admin_ssl_version`

Controls the minimum TLS version required to use the REST API.

Accepted values are:

* TLSv10
* TLSv11
* TLSv12
* TLSv13
* MAX

The default value is MAX which negotiates the highest level of encryption that\
both the client and server support. The list of supported TLS versions depends\
on the operating system and what TLS versions the GnuTLS library supports.

This parameter was added in MaxScale 2.5.7.

#### `admin_enabled`

Enable or disable the admin interface. This allows the admin interface to\
be completely disabled to prevent access to it.

#### `admin_gui`

Enable or disable the admin graphical user interface. This parameter takes\
a boolean value and is enabled by default.

MaxScale provides a GUI for administrative operations via the REST API. When the\
GUI is enabled, the root REST API resource (i.e. `http://localhost:8989/`) will\
serve the GUI. When disabled, the REST API will respond with a 200 OK to the\
request. By disabling the GUI, the root resource can be used as a low overhead\
health check.

#### `admin_secure_gui`

Whether to serve the GUI only over secure HTTPS connections. The default value\
is true.

To be secure by default, the GUI is only served over HTTPS connections as\
it uses a token authentication scheme. This also controls whether the`/auth` endpoint requires an encrypted connection.

To allow use of the GUI without having to configure TLS certificates for\
the MaxScale REST API, set this parameter to false.

#### `admin_log_auth_failures`

Log authentication failures for the admin interface. This parameter expects a\
boolean value and is enabled by default.

#### `admin_pam_readwrite_service` and `admin_pam_readonly_service`

Use Pluggable Authentication Modules (PAM) for REST API authentication. The settings\
accept a PAM service name which is used during authentication if normal authentication\
fails. `admin_pam_readwrite_service` should accept users who can do any\
MaxCtrl/REST-API-operation. `admin_pam_readonly_service` should accept users who can only\
do read operations. Because REST-API does not support back and forth communication between\
the client and MaxScale, the PAM services must be simple. They should only ask for the\
password and nothing else.

If only `admin_pam_readwrite_service` is configured, both read and write operations can be\
authenticated by PAM. If only `admin_pam_readonly_service` is configured, only read\
operations can be authenticated by PAM. If both are set, the service used is determined by\
the requested operation. Leave or set both empty to disable PAM for REST-API.

### Events

MaxScale logs warnings and errors for various reasons and often it is self-\
evident and generally applicable whether some occurence should warrant a\
warning or an error, or perhaps just an info-level message.

However, there are events whose seriousness is not self-evident. For\
instance, in some environments an authentication failure may simply indicate\
that someone has made a typo, while in some other environment that can only\
happen in case there has been a security breech.

To handle events like these, MaxScale defines _events_ whose logging\
facility and level can be controlled by the administrator. Given an event`X`, its facility and level are controlled in the following manner:

```
event.X.facility=LOG_LOCAL0
event.X.level=LOG_ERR
```

The above means that if event _X_ occurs, then that is logged using the\
facility `LOG_LOCAL0` and the level `LOG_ERR`.

The valid values of facility`are the facility values reported by`man\
syslog`, e.g.`LOG\_AUTH`,`LOG\_LOCAL0`and`LOG\_USER`. Likewise, the valid values for`level`are the ones also reported by`man syslog`, e.g.`LOG\_WARNING`,`LOG\_ERR`and`LOG\_CRIT\`.

Note that MaxScale does not act upon the level, that is, even if the level\
of a particular event is defined to be `LOG_EMERG`, MaxScale will not shut\
down if that event occurs.

The default facility is `LOG_USER` and the default level is `LOG_WARNING`.

Note that you may also have to configure `rsyslog` to ensure that the\
event can be logged to the intended log file. For instance, if the facility\
is chosen to be `LOG_AUTH`, then `/etc/rsyslog.conf` should contain a line\
like

```
auth,authpriv.*                 /var/log/auth.log
```

for the logged events to end up in `/var/log/auth.log`, where the initial`auth` is the relevant entry.

The available events are:

#### 'authentication\_failure'

This event occurs when there is an authentication failure.

```
event.authentication_failure.facility=LOG_AUTH
event.authentication_failure.level=LOG_CRIT
```

### Service

A service represents the database service that MariaDB MaxScale offers to the\
clients. In general a service consists of a set of backend database servers and\
a routing algorithm that determines how MariaDB MaxScale decides to send\
statements or route connections to those backend servers.

A service may be considered as a virtual database server that MariaDB MaxScale\
makes available to its clients.

Several different services may be defined using the same set of backend servers.\
For example a connection based routing service might be used by clients that\
already performed internal read/write splitting, whilst a different statement\
based router may be used by clients that are not written with this functionality\
in place. Both sets of applications could access the same data in the same\
databases.

A service is identified by a service name, which is the name of the\
configuration file section and a type parameter of service.

```
[Test-Service]
type=service
```

In order for MariaDB MaxScale to forward any requests it must have at least one\
service defined within the configuration file. The definition of a service alone\
is not enough to allow MariaDB MaxScale to forward requests however, the service\
is merely present to link together the other configuration elements.

#### `router`

The router parameter of a service defines the name of the router module that\
will be used to implement the routing algorithm between the client of MariaDB\
MaxScale and the backend databases. Additionally routers may also be passed a\
comma separated list of options that are used to control the behavior of the\
routing algorithm. The two parameters that control the routing choice are router\
and router\_options. The router options are specific to a particular router and\
are used to modify the behavior of the router. The read connection router can be\
passed options of master, slave or synced, an example of configuring a service\
to use this router and limiting the choice of servers to those in slave state\
would be as follows.

```
router=readconnroute
router_options=slave
```

To change the router to connect on to servers in the master state as well as\
slave servers, the router options can be modified to include the master state.

```
router=readconnroute
router_options=master,slave
```

A more complete description of router options and what is available for a given\
router is included with the documentation of the router itself.

#### `router_options`

Option string given to the router module. The value of this parameter should be\
a comma-separated list of key-value pairs. See router specific documentation for\
more details.

#### `filters`

The filters option allow a set of filters to be defined for a service; requests\
from the client are passed through these filters before being sent to the router\
for dispatch to the backend server. The filters parameter takes one or more\
filter names, as defined within the filter definition section of the\
configuration file. Multiple filters are separated using the | character.

```
filters=counter | QLA
```

The requests pass through the filters from left to right in the order defined in\
the configuration parameter.

#### `targets`

The `targets` parameter is a comma separated list of server and/or service names\
that comprise the routing targets of the service. This parameter was added in\
MaxScale 2.5.0.

```
targets=My-Service,server2
```

This parameter allows nested service configurations to be defined without having\
to configure listeners for all services. For example, one use-case is to use\
multiple readwritesplit services behind a schemarouter service to have both the\
sharding of schemarouter with the high-availability of readwritesplit.

**NOTE:** The `targets` parameter is mutually exclusive with the `cluster` and`servers` parameters.

#### `servers`

The servers parameter in a service definition provides a comma separated list of\
the backend servers that comprise the service. The server names are those used\
in the name section of a block with a type parameter of server (see below).

```
servers=server1,server2,server3
```

**NOTE:** The `servers` parameter is mutually exclusive with the `cluster` and`targets` parameters.

#### `cluster`

The servers the service uses are defined by the monitor specified as value\
of this configuration parameter.

```
cluster=TheMonitor
```

**NOTE:** The `cluster` parameter is mutually exclusive with the `servers` and`targets` parameters.

#### `user` and `password`

These settings define the credentials the service uses to fetch user account\
information from backends. The _password_ may be either a plain text password or\
an [encrypted password](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#encrypting-passwords).

```
user=maxscale
password=Mhu87p2D
```

See [MySQL protocol authentication documentation](../maxscale-25-authenticators/mariadb-maxscale-25-authentication-modules.md)\
for more information (such as required grants) and troubleshooting tips\
regarding user account management and client authentication.

#### `enable_root_user`

This parameter controls the ability of the root user to connect to MariaDB\
MaxScale and hence onwards to the backend servers via MariaDB MaxScale.

The default value is `0`, disabling the ability of the root user to connect to\
MariaDB MaxScale.

Example for enabling root user:

```
enable_root_user=1
```

Values of `on` or `true` may also be given to enable the root user and `off` or`false` may be given to disable the use of the root user.

```
enable_root_user=true
```

#### `localhost_match_wildcard_host`

Deprecated and ignored.

#### `version_string`

This parameter sets a custom version string that is sent in the MySQL Handshake\
from MariaDB MaxScale to clients.

Example:

```
version_string=5.5.37-MariaDB-RWsplit
```

If not set, the default value is `5.5.5-10.0.0 MaxScale <MaxScale version>`\
where `<MaxScale version>` is the version of MaxScale. If the provided string\
does not start with the number 5, a 5.5.5- prefix will be added to it. This\
means that a _version\_string_ value of _MaxScale-Service_ would result in &#x61;_&#x35;.5.5-MaxScale-Service_ being sent to the client.

#### `weightby`

This parameter has been removed. Server weights were deprecated in\
MaxScale 2.3.2 and removed in MaxScale 2.5.0. The feature has been\
replaced with the [rank](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#rank) mechanism.

If this value is found in the MaxScale configuration, a warning is logged\
and the value is ignored.

#### `auth_all_servers`

This parameter controls whether only a single server or all of the servers are\
used when loading the users from the backend servers. This takes a boolean value\
and when enabled, creates a union of all the users and grants on all the\
servers.

#### `strip_db_esc`

This setting controls whether escape characters (`\`) are removed from database\
names when loading user grants from a backend server. The setting takes a\
boolean value and is on by default. When enabled, a grant such as`grant select on` test\_`.* to 'user'@'%';` is read as`grant select on` test\_`.* to 'user'@'%';`

This setting has no effect on database-level grants fetched from a MariaDB\
Server. The database names of a MariaDB Server are compared using the LIKE\
operator to properly handle wildcards and escaped wildcards. This setting may\
affect database names in table and column level grants, although these typically\
do not contain backlashes.

This setting does affect database names when reading grants from an\
Xpand-server.

Some visual database management tools automatically escape some characters and\
this might cause conflicts when MaxScale tries to authenticate users.

#### `log_auth_warnings`

Enable or disable the logging of authentication failures and warnings. This\
parameter takes a boolean value.

MariaDB MaxScale normally suppresses warning messages about failed\
authentication. Enabling this option will log those messages into the message\
log with details about who tried to connect to MariaDB MaxScale and from where.

#### `connection_timeout`

The connection\_timeout parameter is used to disconnect sessions to MariaDB\
MaxScale that have been idle for too long. The session timeouts are disabled by\
default. To enable them, define the timeout in seconds in the service's\
configuration section. A value of zero is interpreted as no timeout, the same\
as if the parameter is not defined.

The value is specified as documented [here](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#durations). If no explicit unit\
is provided, the value is interpreted as seconds in MaxScale 2.4. In subsequent\
versions a value without a unit may be rejected. Note that since the granularity\
of the timeout is seconds, a timeout specified in milliseconds will be rejected,\
even if the duration is longer than a second.

This parameter only takes effect in top-level services. A top-level service is\
the service where the listener that the client connected to points (i.e. the\
value of `service` in the listener). If a service defines other services in its`targets` parameter, the `connection_timeout` for those is not used.

The value of `connection_timeout` should be lower than the lowest `wait_timeout`\
value on the backend servers. This way idle clients are disconnected by MaxScale\
before the backend servers have to close them. Any client-side idle timeouts\
(e.g. maximum lifetime for connection pools) should be lower than both`connection_timeout` and `wait_timeout`. This way the client application will\
end up closing the connection itself which most of the time results in better\
and more helpful error messages.

**Warning:** If a connection is idle for longer than the configured connection\
timeout, it will be forcefully disconnected and a warning will be logged in the\
MaxScale log file. If you are performing long-running maintenance operations\
(e.g. `ALTER TABLE`) either do them with a direct connection to the server or\
set `connection_timeout` to zero before executing them.

Example:

```
[Test-Service]
connection_timeout=300s
```

#### `max_connections`

The maximum number of simultaneous connections MaxScale should permit to this\
service. If the parameter is zero or is omitted, there is no limit. Any attempt\
to make more connections after the limit is reached will result in a "Too many\
connections" error being returned.

**Warning**: In MaxScale 2.5, it is possible that the number of concurrent\
connections temporarily exceeds the value of `max_connections`. This has been\
fixed in MaxScale 6.

Example:

```
[Test-Service]
max_connections=100
```

#### `session_track_trx_state`

* Type: boolean
* Default: false
* Dynamic: Yes

Enable transaction state tracking by offloading it to the backend servers.\
Getting the transaction state from the server will be more accurate for stored\
procedures or multi-statement SQL that modifies the transaction state\
non-atomically.

In general, it is better to avoid using this type of SQL as tracking the\
transaction state via the server responses is not compatible with features such\
as `transaction_replay` in readwritesplit. `session_track_trx_state` should only\
be enabled if the default transaction tracking done by MaxScale does not produce\
the desired outcome.

This is only supported by MariaDB versions 10.3 or newer. The following must be\
configured in the MariaDB server in order for this feature to work. Not\
configuring the MariaDB server with it can result in the transaction state being\
wrong in MaxScale which can result in data inconsistency.

```
session_track_state_change = ON
session_track_transaction_info = CHARACTERISTICS
```

#### `retain_last_statements`

How many statements MaxScale should store for each session of this service.\
This overrides the value of the global setting with the same name. If`retain_last_statements` has been specified in the global section of the\
MaxScale configuration file, then if it has _not_ been explicitly specified\
for the service, the global value holds, otherwise the service specific\
value rules. That is, it is possible to enable the setting globally and\
turn it off for a specific service, or just enable it for specific services.

The value of this parameter can be changed at runtime using `maxctrl` and the\
new value will take effect for sessions created thereafter.

```
maxctrl alter service MyService retain_last_statements 5
```

#### `connection_keepalive`

Keep idle connections alive by sending pings to backend servers. This feature\
was introduced in MaxScale 2.5.0 where it was changed from a\
readwritesplit-specific feature to a generic service feature. The default value\
for this parameter is 300 seconds. To disable this feature, set the value to 0.

The keepalive interval is specified as documented [here](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#durations). If no\
explicit unit is provided, the value is interpreted as seconds in MaxScale\
2.5. In subsequent versions a value without a unit may be rejected. Note that\
since the granularity of the keepalive is seconds, a keepalive specified in\
milliseconds will be rejected, even if the duration is longer than a second.

The parameter value is the interval in seconds between each keepalive ping. A\
keepalive ping will be sent to a backend server if the connection has been idle\
for longer than the configured keepalive interval.

Starting with MaxScale 2.5.21, the keepalive pings are not sent if the client\
has been idle for longer than the configured value of`connection_keepalive`. Older versions of MaxScale sent the keepalive pings\
regardless of the client state.

This parameter only takes effect in top-level services. A top-level service is\
the service where the listener that the client connected to points (i.e. the\
value of `service` in the listener). If a service defines other services in its`targets` parameter, the `connection_keepalive` for those is not used.

If the value of `connection_keepalive` is changed at runtime, the change in the\
value takes effect immediately.

As the connection keepalive pings must be done only when there's no ongoing\
query, all requests and responses must be tracked by MaxScale. In the case of`readconnroute`, this will incur a small drop in performance. For routers that\
rely on result tracking (e.g. `readwritesplit` and `schemarouter`), the\
performance will be the same with or without `connection_keepalive`.

If you want to avoid the performance cost and you don't need the connection\
keepalive feature, you can disable it with `connection_keepalive=0s`.

#### `force_connection_keepalive`

* Type: boolean
* Default: false
* Dynamic: Yes

By default, connection keepalive pings are only sent if the client is either\
executing a query or has been idle for less than the duration configured in`connection_keepalive`. When this parameter is enabled, keepalive pings are\
unconditionally sent to any backends that have been idle for longer than`connection_keepalive` seconds. This option can be used to emulate the\
pre-2.5.21 behavior if long-lived application connections rely on the old\
unconditional keepalive pings.

_Note:_ if `force_connection_keepalive` is enabled and `connection_keepalive` in\
MaxScale is set to a lower value than the `wait_timeout` on the database, the\
client idle timeouts that `wait_timeout` control are no longer effective. This\
happens because MaxScale unconditionally sends the pings which make the client\
behave like it is not idle and thus the connections will never be killed due to`wait_timeout`.

#### `net_write_timeout`

This parameter controls how long a network write to the client can stay\
buffered. This feature is disabled by default.

When `net_write_timeout` is configured and data is buffered on the client\
network connection, if the time since the last successful network write exceeds\
the configured limit, the client connection will be disconnected.

The value is specified as documented [here](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#durations). If no explicit unit\
is provided, the value is interpreted as seconds in MaxScale 2.4. In subsequent\
versions a value without a unit may be rejected. Note that since the granularity\
of the timeout is seconds, a timeout specified in milliseconds will be rejected,\
even if the duration is longer than a second.

### Server

Server sections define the backend database servers MaxScale uses. A server is\
identified by its section name in the configuration file. The only mandatory\
parameter of a server is _type_, but _address_ and _port_ are also usually\
defined. A server may be a member of one or more services. A server may only be\
monitored by at most one monitor.

```
[MyMariaDBServer1]
type=server
address=127.0.0.1
port=3000
```

#### `address`

The IP-address or hostname of the machine running the database server. MaxScale\
uses this address to connect to the server. This parameter is mandatory unles&#x73;_&#x73;ocket_ is defined.

#### `port`

The port the backend server listens on for incoming connections. MaxScale uses\
this port to connect to the server. The default value is 3306.

#### `socket`

The absolute path to a UNIX domain socket the MariaDB server is listening\
on. Either _address_ or _socket_ must be defined and defining them both is an\
error.

#### `monitoruser` and `monitorpw`

These settings define a server-specific username and password for monitoring the\
server. Monitors typically use the credentials in their own configuration\
sections to connect to all servers. If server-specific settings are given, the\
monitor uses those instead.

```
monitoruser=mymonitoruser
monitorpw=mymonitorpasswd
```

`monitorpw` may be either a plain text password or an encrypted password. See\
the section [encrypting passwords](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#encrypting-passwords) for more information.

#### `extra_port`

An alternative port used to monitor the server. This allows MaxScale to connect\
even when _max\_connections_ on the backend server has been reached. If this\
parameter is defined and a connection to the normal port fails, the alternative\
port is used.

For more information, read the[extra\_port documentation](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/ha-and-performance/optimization-and-tuning/buffers-caches-and-threads/thread-pool/thread-pool-system-status-variables).

#### `persistpoolmax`

The `persistpoolmax` parameter defaults to zero but can be set to an integer\
value for a back end server. If it is non zero, then when a DCB connected to a\
back end server is discarded by the system, it will be held in a pool for reuse,\
remaining connected to the back end server. If the number of DCBs in the pool\
has reached the value given by `persistpoolmax` then any further DCB that is\
discarded will not be retained, but disconnected and discarded.

When a MariaDB protocol connection is taken from the pool, the state of the\
session is reset. This means that a pooled connection works exactly like a fresh\
connection.

#### `persistmaxtime`

The `persistmaxtime` parameter defaults to zero but can be set to a duration as\
documented [here](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#durations). If no explicit unit is provided, the value is\
interpreted as seconds in MaxScale 2.4. In subsequent versions a value without a\
unit may be rejected. Note that since the granularity of the parameter is\
seconds, a value specified in milliseconds will be rejected, even if the\
duration is longer than a second.

A DCB placed in the persistent pool for a server will only be reused if the\
elapsed time since it joined the pool is less than the given value. Otherwise,\
the DCB will be discarded and the connection closed.

#### `proxy_protocol`

If `proxy_protocol` is set to `on`, MaxScale will send a[PROXY protocol](https://www.haproxy.org/download/1.8/doc/proxy-protocol.txt)\
header when connecting client sessions to the server. The header contains the\
original client IP address and port, as seen by MaxScale. The server will then\
read the header and perform authentication as if the connection originated from\
this address instead of MaxScale's IP address. With this feature, the user\
accounts on the backend server can be simplified to only contain the actual\
client hosts and not the MaxScale host.

PROXY protocol will be supported by MariaDB 10.3, which this feature has been\
tested with. To use it, enable the PROXY protocol in MaxScale for every\
compatible server and configure the MariaDB servers themselves to accept the\
protocol headers from MaxScale's IP address. On the server side, the protocol\
should be enabled only for trusted IPs, as it allows the sender to spoof the\
connection origin. If a proxy header is sent to a server not expecting it, the\
connection will fail. Usually PROXY protocol should be enabled for every\
server in a cluster, as they typically have similar grants.

Other SQL-servers may support PROXY protocol as well, but the implementation may\
be highly restricting. Strict adherence to the protocol requires that the\
backend server does not allow mixing of un-proxied and proxied connections from\
a given IP. MaxScale requires normal connections to backends for monitoring and\
authentication data queries, which would be blocked. To bypass this restriction,\
the server monitor needs to be disabled and the service listener needs to be\
configured to disregard authentication errors (`skip_authentication=true`).\
Server states also need to be set manually in MaxCtrl. These steps are _not_\
required for MariaDB 10.3, since its implementation is more flexible and allows\
both PROXY-headered and headerless connections from a proxy-enabled IP.

#### `disk_space_threshold`

This parameter specifies how full a disk may be, before MaxScale should start\
logging warnings or take other actions (e.g. perform a switchover). This\
functionality will only work with MariaDB server versions 10.1.32, 10.2.14 and\
10.3.6 onwards, if the `DISKS` _information schema plugin_ has been installed.

**NOTE**: In future MariaDB versions, the information will be available _only_ if\
the monitor user has the `FILE` privilege.

A limit is specified as a path followed by a colon and a percentage specifying\
how full the corresponding disk may be, before action is taken. E.g. an entry like

```
/data:80
```

specifies that the disk that has been mounted on `/data` may be used until 80%\
of the total space has been consumed. Multiple entries can be specified by\
separating them by a comma. If the path is specified using `*`, then the limit\
applies to all disks. However, the value of `*` is only applied if there is not\
an exact match.

Note that if a particular disk has been mounted on several paths, only one path\
need to be specified. If several are specified, then the one with the smallest\
percentage will be applied.

Examples:

```
disk_space_threshold=*:80
disk_space_threshold=/data:80
disk_space_threshold=/data1:80,/data2:60,*:90
```

The last line means that the disk mounted at `/data1` may be used up to\
80%, the disk mounted at `/data2` may be used up to 60% and all other disks\
mounted at any paths may be used up until 90% of maximum capacity, before\
MaxScale starts to warn to take action.

Note that the path to be used, is one of the paths returned by:

```
> use information_schema;
> select * from disks;
+-----------+----------------------+-----------+----------+-----------+
| Disk      | Path                 | Total     | Used     | Available |
+-----------+----------------------+-----------+----------+-----------+
| /dev/sda3 | /                    |  47929956 | 34332348 |  11139820 |
| /dev/sdb1 | /data                | 961301832 |    83764 | 912363644 |
...
```

There is no default value, but this parameter must be explicitly specified\
if the disk space situation should be monitored.

#### `rank`

This parameter controls the order in which servers are used. Valid values for\
this parameter are `primary` and `secondary`. The default value is`primary`. This parameter replaces the use of the `weightby` parameter as the\
primary means of controlling server usage.

This behavior depends on the router implementation but the general rule of thumb\
is that primary servers will be used before secondary servers.

Readconnroute will always use primary servers before secondary servers as long\
as they match the configured server type.

Readwritesplit will pick servers that have the same rank as the current\
master. Read the[readwritesplit documentation on server ranks](../maxscale-25-routers/mariadb-maxscale-25-readwritesplit.md#server-ranks)\
for a detailed description of the behavior.

The following example server configuration demonstrates how `rank` can be used\
to exclude `DR-site` servers from routing.

```
[main-site-master]
type=server
address=192.168.0.11
rank=primary

[main-site-slave]
type=server
address=192.168.0.12
rank=primary

[DR-site-master]
type=server
address=192.168.0.21
rank=secondary

[DR-site-slave]
type=server
address=192.168.0.22
rank=secondary
```

The `main-site-master` and `main-site-slave` servers will be used as long as\
they are available. When they are no longer available, the `DR-site-master` and`DR-site-slave` will be used.

#### `priority`

* Type: integer
* Default: 0
* Dynamic: Yes

Server priority. Currently only used by galeramon to choose the order in which\
nodes are selected as the current master server. Refer to the[Server Priorities](../maxscale-25-monitors/mariadb-maxscale-25-galera-monitor.md#interaction-with-server-priorities)\
section of the galeramon documentation for more information on how to use it.

Starting with MaxScale 2.5.21, this parameter also accepts negative values. In\
older versions, the parameter only accepted non-negative values.

### Monitor

Monitor sections are used to define the monitoring module that watches a set of\
servers. Each server can only be monitored by one monitor.

Common monitor parameters [can be found here](../maxscale-25-monitors/mariadb-maxscale-25-common-monitor-parameters.md).

### Listener

A listener defines a port MaxScale listens on for incoming connections. Accepted\
connections are linked with a MaxScale service. Multiple listeners can feed the\
same service. Mandatory parameters are _type_, _service_ and _protocol_._address_ is optional, it limits connections to a certain network interface\
only. _socket_ is also optional and is used for Unix socket connections.

The network socket where the listener listens may have a backlog of\
connections. The size of this backlog is controlled by th&#x65;_&#x6E;et.ipv4.tcp\_max\_syn\_backlog_ and _net.core.somaxconn_ kernel parameters.

Increasing the size of the backlog by modifying the kernel parameters helps with\
sudden connection spikes and rejected connections. For more information see[listen(2)](https://man7.org/linux/man-pages/man2/listen.2.html).

```
[MyListener1]
type=listener
service=MyService1
protocol=MariaDBClient
port=3006
```

#### `service`

The service to which the listener is associated. This is the name of a service\
that is defined elsewhere in the configuration file.

#### `protocol`

The name of the protocol module used for communication between the client and\
MaxScale. The same protocol is also used for backend communication. Usually this\
is set to `MariaDBClient`.

#### `address`

This sets the address the listening socket is bound to. The address may be\
specified as an IP address in 'dot notation' or as a hostname. If left undefined\
the listener will bind to all network interfaces.

#### `port`

The port the listener listens on. If left undefined a default port for the\
protocol is used.

#### `socket`

If defined, the listener uses Unix domain sockets to listen for incoming\
connections. The parameter value is the name of the socket to use.

If you want to use both network ports and UNIX domain sockets with a service,\
define two separate listeners that connect to the same service.

#### `authenticator`

The authenticator module to use. Each protocol module defines a default\
authentication module, which is used if the setting is left undefined._MariaDBClient_-protocol supports multiple authenticators and they can be used\
simultaneously by giving a comma-separated list e.g.`authenticator=PAMAuth,mariadbauth,gssapiauth`

#### `authenticator_options`

This defines additional options for authentication. As of MaxScale 2.5.0, onl&#x79;_&#x4D;ariaDBClient_ and its authenticators support additional options. The value of\
this parameter should be a comma-separated list of key-value pairs. See\
authenticator specific documentation for more details.

#### `sql_mode`

Specify the sql mode for the listener similarly to global `sql_mode` setting.\
If both are used this setting will override the global setting for this listener.

#### `connection_init_sql_file`

Path to a text file with sql queries. Any sessions created from the listener\
will send the contents of the file to backends after authentication. Each\
non-empty line in the file is interpreted as a query. Each query must succeed\
for the backend connection to be usable for client queries. The queries should\
not return any data.

```
connection_init_sql_file=/home/dba/init_queries.txt
```

Example query file:

```
set @myvar = 'mytext';
set @myvar2 = 4;
```

## Available Protocols

The protocols supported by MariaDB MaxScale are implemented as external modules\
that are loaded dynamically into the MariaDB MaxScale core. They allow MariaDB\
MaxScale to communicate in various protocols both on the client side and the\
backend side. Each of the protocols can be either a client protocol or a backend\
protocol. Client protocols are used for client-MariaDB MaxScale communication\
and backend protocols are for MariaDB MaxScale-database communication.

### `MariaDBClient`

This is the implementation of the MySQL-protocol. When defined for a listener,\
the listener will accept MySQL-connections from clients, assign them to a\
MaxScale service and route the queries from the client to backend servers. Any\
backends used by the service should be MariaDB/MySQL-servers or compatible.

### `CDC`

See [Change Data Capture Protocol](../maxscale-25-protocols/mariadb-maxscale-25-change-data-capture-cdc-protocol.md) for more information.

## TLS/SSL encryption

This section describes configuration parameters for both servers and listeners\
that control the TLS/SSL encryption method and the various certificate files\
involved in it.

To enable TLS/SSL for a listener, you must set the `ssl` parameter to`true` and provide at least the `ssl_cert` and `ssl_key` parameters.

To enable TLS/SSL for a server, you must set the `ssl` parameter to`true`. If the backend database server has certificate verification\
enabled, the `ssl_cert` and `ssl_key` parameters must also be defined.

Custom CA certificates can be defined with the `ssl_ca_cert` parameter.

After this, MaxScale connections between the server and/or the client will be\
encrypted. Note that the database must also be configured to use TLS/SSL\
connections if backend connection encryption is used.

**Note:** MaxScale does not allow mixed use of TLS/SSL and normal connections on\
the same port.

If TLS encryption is enabled for a listener, any unencrypted connections to it\
will be rejected. MaxScale does this to improve security by preventing\
accidental creation of unencrypted connections.

The separation of secure and insecure connections differs from the MariaDB\
server which allows both secure and insecure connections on the same port. As\
MaxScale is the gateway through which all connections go, in order to guarantee\
a more secure system MaxScale enforces a stricter security policy than what the\
server does.

TLS encryption must be enabled for listeners when they are created. For servers,\
the TLS can be enabled after creation but it cannot be disabled or altered.

Starting with MaxScale 2.5.20, if the TLS certificate given to MaxScale has the\
X509v3 extended key usage information, MaxScale will check it and refuse to use\
a certificate with the wrong usage. This means that a certificate with only\
clientAuth can only be used with servers and a certificate with only serverAuth\
can only be used with listeners. In order to use the same certificate for both\
listeners and servers, it must have both the clientAuth and serverAuth usages.

#### `ssl`

This enables SSL connections when set to true. The parameter takes a boolean\
value and is disabled by default. The parameter also accepts the special values`required` and `disabled` which were the only supported values before MaxScale\
2.3.0. The use of `required` and `disabled` is deprecated.

If enabled, the certificate files mentioned above must also be\
supplied. MaxScale connections to will then be encrypted with TLS/SSL.

#### `ssl_key`

A string giving a file path that identifies an existing readable file. The file\
must be the SSL client private key MaxScale should use. This is a required\
parameter for listeners but an optional parameter for servers.

#### `ssl_cert`

A string giving a file path that identifies an existing readable file. The file\
must be the SSL client certificate MaxScale should use with the server. The\
certificate must match the key defined in `ssl_key`. This is a required\
parameter for listeners but an optional parameter for servers.

#### `ssl_ca_cert`

A string giving a file path that identifies an existing readable file. The file\
must be the Certificate Authority (CA) certificate for the CA that signed the\
certificate referred to in the previous parameter. It will be used to verify\
that the certificate is valid. This is a required parameter for both listeners\
and servers. The CA certificate can consist of a certificate chain.

#### `ssl_version`

**Note:** It is highly recommended to leave this parameter to the default value\
of _MAX_. This will guarantee that the strongest available encryption is used.**Do not change this unless you know what you are doing**.

This parameter controls the level of encryption used. Accepted values are:

* TLSv10
* TLSv11
* TLSv12
* TLSv13
* MAX

The default is to use the highest level of encryption available that both the\
client and server support. MaxScale supports TLSv1.0, TLSv1.1, TLSv1.2 and\
TLSv1.3 depending on the OpenSSL library version.

The `TLSv13` value was added in MaxScale 2.3.15 ([MXS-2762](https://jira.mariadb.org/browse/MXS-2762)).

#### `ssl_cipher`

Set the list of TLS ciphers. By default, no explicit ciphers are defined and the\
system defaults are used. Note that this parameter does not modify TLSv1.3\
ciphers.

#### `ssl_cert_verify_depth`

The maximum length of the certificate authority chain that will be accepted. The\
default value is 9, same as the OpenSSL default. The configured value must be\
larger than 0.

#### `ssl_verify_peer_certificate`

Peer certificate verification. This functionality is disabled by default. In\
versions prior to 2.3.17 the feature was enabled by default.

When this feature is enabled, the peer must send a certificate. The certificate\
sent by the peer is verified against the configured Certificate Authority to\
make sure the peer is who they claim to be. For listeners, this behaves as if`REQUIRE X509` was defined for all users. For servers, this behaves like the`--ssl-verify-server-cert` command line option for the `mysql` client.

#### `ssl_verify_peer_host`

Peer host verification. This parameter takes a boolean value and is disabled by\
default.

When this feature is enabled, the peer hostname or IP is verified against the\
certificate that is sent by the peer. If the IP address or the hostname does not\
match the one in the certificate returned by the peer, the connection will be\
closed. If the peer does not provide a certificate, the host verification is not\
done. To require peer certificates, use `ssl_verify_peer_certificate`.

#### `ssl_crl`

A string giving a file path that identifies an existing readable file. The file\
must be a Certificate Revocation List in the PEM format that defines the revoked\
certificates. This parameter is only accepted by listeners.

**Example SSL enabled server configuration**

```
[server1]
type=server
address=10.131.24.62
port=3306
ssl=true
ssl_cert=/usr/local/mariadb/maxscale/ssl/crt.max-client.pem
ssl_key=/usr/local/mariadb/maxscale/ssl/key.max-client.pem
ssl_ca_cert=/usr/local/mariadb/maxscale/ssl/crt.ca.maxscale.pem
```

This example configuration requires all connections to this server to be\
encrypted with SSL. The paths to the certificate files and the Certificate\
Authority file are also provided.

**Example SSL enabled listener configuration**

```
[RW-Split-Listener]
type=listener
service=RW-Split-Router
protocol=MariaDBClient
port=3306
ssl=true
ssl_cert=/usr/local/mariadb/maxscale/ssl/crt.maxscale.pem
ssl_key=/usr/local/mariadb/maxscale/ssl/key.csr.maxscale.pem
ssl_ca_cert=/usr/local/mariadb/maxscale/ssl/crt.ca.maxscale.pem
```

This example configuration requires all connections to be encrypted with\
SSL. The paths to the certificate files and the Certificate Authority file are\
also provided.

## Module Types

### Routing Modules

The main task of MariaDB MaxScale is to accept database connections from client\
applications and route the connections or the statements sent over those\
connections to the various services supported by MariaDB MaxScale.

Currently a number of routing modules are available, these are designed for a\
range of different needs.

Connection based load balancing:

* [ReadConnRoute](../maxscale-25-routers/mariadb-maxscale-25-readconnroute.md)

Read/Write aware statement based router:

* [ReadWriteSplit](../maxscale-25-routers/mariadb-maxscale-25-readwritesplit.md)

Simple sharding on database level:

* [SchemaRouter](../maxscale-25-routers/mariadb-maxscale-25-schemarouter.md)

Binary log server:

* [Binlogrouter](../maxscale-25-routers/mariadb-maxscale-25-binlogrouter.md)

### Monitor Modules

Monitor modules are used by MariaDB MaxScale to internally monitor the state of\
the backend databases in order to set the server flags for each of those\
servers. The router modules then use these flags to determine if the particular\
server is a suitable destination for routing connections for particular query\
classifications. The monitors are run within separate threads of MariaDB\
MaxScale and do not affect MariaDB MaxScale's routing performance.

* [MariaDB Monitor](../maxscale-25-monitors/mariadb-maxscale-25-mariadb-monitor.md)
* [Galera Monitor](../maxscale-25-monitors/mariadb-maxscale-25-galera-monitor.md)

The use of monitors in MaxScale is not absolutely mandatory: it is possible to\
run MariaDB MaxScale without a monitor module. In this case an external\
monitoring system must the status of each server via MaxCtrl or the REST\
API. **Only do this if you know what you are doing.**

### Filter Modules

![](<../../../../.gitbook/assets/image_10.png (2).png>)

Filters provide a means to manipulate or process requests as they pass through\
MariaDB MaxScale between the client side protocol and the query router. A full\
explanation of each filter's functionality can be found in its documentation.

The [Filter Tutorial](../maxscale-25-tutorials/mariadb-maxscale-25-filters.md) document shows how you\
can add a filter to a service and combine multiple filters in one service.

* [Query Log All (QLA) Filter](../maxscale-25-filters/mariadb-maxscale-25-query-log-all-filter.md)
* [Regular Expression Filter](../maxscale-25-filters/mariadb-maxscale-25-regex-filter.md)
* [Tee Filter](../maxscale-25-filters/mariadb-maxscale-25-tee-filter.md)
* [Top Filter](../maxscale-25-filters/mariadb-maxscale-25-top-filter.md)
* [Database Firewall Filter](../maxscale-25-filters/mariadb-maxscale-25-database-firewall-filter.md)
* [Query Redirection Filter](../maxscale-25-filters/mariadb-maxscale-25-named-server-filter.md)

## Encrypting Passwords

Passwords stored in the maxscale.cnf file may optionally be encrypted for added security.\
This is done by creation of an encryption key on installation of MariaDB MaxScale.\
Encryption keys may be created manually by executing the maxkeys utility with the argument\
of the filename to store the key. The default location MariaDB MaxScale stores\
the keys is `/var/lib/maxscale`. The passwords are encrypted using 256-bit AES CBC encryption.

```
# Usage: maxkeys [PATH]
maxkeys /var/lib/maxscale/
```

Changing the encryption key for MariaDB MaxScale will invalidate any currently\
encrypted keys stored in the maxscale.cnf file.

### Creating Encrypted Passwords

Encrypted passwords are created by executing the maxpasswd command with the location\
of the .secrets file and the password you require to encrypt as an argument.

```
# Usage: maxpasswd PATH PASSWORD
maxpasswd /var/lib/maxscale/ MaxScalePw001
61DD955512C39A4A8BC4BB1E5F116705
```

The output of the maxpasswd command is a hexadecimal string, this should be inserted\
into the maxscale.cnf file in place of the ordinary, plain text, password.\
MariaDB MaxScale will determine this as an encrypted password and automatically decrypt\
it before sending it the database server.

```
[Split-Service]
type=service
router=readwritesplit
servers=server1,server2,server3,server4
user=maxscale
password=61DD955512C39A4A8BC4BB1E5F116705
```

## Runtime Configuration Changes

Read the following documents for different methods of altering the MaxScale\
configuration at runtime.

* MaxCtrl
* [create](../maxscale-25-reference/mariadb-maxscale-25-maxctrl.md#create)
* [destroy](../maxscale-25-reference/mariadb-maxscale-25-maxctrl.md#destroy)
* [add](../maxscale-25-reference/mariadb-maxscale-25-maxctrl.md#add)
* [remove](../maxscale-25-reference/mariadb-maxscale-25-maxctrl.md#remove)
* [alter](../maxscale-25-reference/mariadb-maxscale-25-maxctrl.md#alter)
* [REST API](../maxscale-25-rest-api/mariadb-maxscale-25-rest-api.md) documentation

All changes to the configuration done via MaxCtrl are persisted as individual\
configuration files in `/var/lib/maxscale/maxscale.cnf.d/`. The content of these\
files will override any configurations found in the main configuration file or\
any auxiliary configuration files.

Refer to the [Dynamic Configuration](mariadb-maxscale-25-mariadb-maxscale-configuration-guide.md#dynamic-configuration) section for more\
details on how this mechanism works and how to disable it.

### Backing Up Configuration Changes

The combination of configuration files can be done either manually\
(e.g. `rsync`) or with the `maxscale --export-config=FILE` command line\
option. See `maxscale --help` for more information about how to use the`--export-config` flag.

For example, to export the current runtime configuration, run the following\
command.

```
maxscale --export-config=/tmp/maxscale.cnf.combined
```

This will create the `/tmp/maxscale.cnf.combined` file and write the current\
configuration into the it. This allows new MaxScale instances to be easily set\
up without requiring copying of all runtime configuration files. The user\
executing the command must be able to read all MaxScale configuration files as\
well as create and write the provided filename.

## Error Reporting

MariaDB MaxScale is designed to be executed as a service, therefore all error\
reports, including configuration errors, are written to the MariaDB MaxScale\
error log file. By default, MariaDB MaxScale will log to a file in`/var/log/maxscale` and the system log.

## Limitations

The current limitations of MaxScale are listed in the [Limitations](../about-maxscale-25/mariadb-maxscale-25-limitations-and-known-issues-within-mariadb-maxscale.md) document.

## Performance Optimization

* Tune `query_classifier_cache_size` to allow maximal use of the query\
  classifier cache. Increase the value and/or system memory until the set of\
  unique SQL patterns fits into memory. By default at most 15% of the system\
  memory is used for this cache. To detect if the SQL statements fit into\
  memory, monitor the `QC cache evictions` value in `maxctrl show threads` to\
  see how many evictions take place. If it keeps increasing, increase the size\
  of the query classifier cache. Using the query classifier cache with a CPU\
  bound workload gives a roughly 20% improvement in performance compared to when\
  it is turned off.
* A faster CPU with more CPU cores is better. This is true for most applications\
  but especially for MaxScale as it is mostly limited by the speed of the\
  CPU. Using `threads=auto` is recommended (the default starting with MaxScale\
  6\).
* Network throughput between the client, MaxScale and the database nodes governs\
  how much traffic can be handled. The client-to-MaxScale network is likely to\
  be saturated first: having multiple MaxScales in front of the cluster is an\
  easy way of solving this problem.
* Certain MaxScale modules store data on disk. A faster disk improves their\
  performance but depending on the module, this might not be a big enough of a\
  problem to worry about. Filters like the `qlafilter` that write information to\
  disk for every SQL query can cause performance bottlenecks.

## Troubleshooting

For a list of common problems and their solutions, read the[MaxScale Troubleshooting](../../../../maxscale-management/maxscale-troubleshooting.md)\
article on the MariaDB documentation.

### Systemd Watchdog

If MaxScale is running as a systemd service, the systemd Watchdog will be\
enabled by default. To configure it, change the `WatchdogSec` option in the\
Service section of the maxscale systemd configuration file located in`/lib/systemd/system/maxscale.service`:

```
WatchdogSec=30s
```

It is not recommended to use a watchdog timeout less than 30 seconds. When\
enabled MaxScale will check that all threads are running and notify systemd\
with a "keep-alive ping".

Systemd reference: [systemd.service.html](https://www.freedesktop.org/software/systemd/man/systemd.service.html)

<sub>_This page is licensed: CC BY-SA / Gnu FDL_</sub>

{% @marketo/form formId="4316" %}
