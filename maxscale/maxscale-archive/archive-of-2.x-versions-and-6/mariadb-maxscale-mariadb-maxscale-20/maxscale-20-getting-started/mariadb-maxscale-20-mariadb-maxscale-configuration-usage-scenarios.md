# MariaDB MaxScale Configuration & Usage Scenarios

### Introduction

The purpose of this document is to describe how to configure MariaDB MaxScale and to discuss some possible usage scenarios for MariaDB MaxScale. MariaDB MaxScale is designed with flexibility in mind, and consists of an event processing core with various support functions and plugin modules that tailor the behavior of the MariaDB MaxScale itself.

## Table of Contents

* [Configuration](mariadb-maxscale-20-mariadb-maxscale-configuration-usage-scenarios.md#configuration)
* [Global Settings](mariadb-maxscale-20-mariadb-maxscale-configuration-usage-scenarios.md#global-settings)
* [Service](mariadb-maxscale-20-mariadb-maxscale-configuration-usage-scenarios.md#service)
* [Server](mariadb-maxscale-20-mariadb-maxscale-configuration-usage-scenarios.md#server)
* [Server and SSL](mariadb-maxscale-20-mariadb-maxscale-configuration-usage-scenarios.md#server-and-ssl)
* [Listener](mariadb-maxscale-20-mariadb-maxscale-configuration-usage-scenarios.md#listener)
* [Listener and SSL](mariadb-maxscale-20-mariadb-maxscale-configuration-usage-scenarios.md#listener-and-ssl)
* [Router Modules](mariadb-maxscale-20-mariadb-maxscale-configuration-usage-scenarios.md#routing-modules)
* [Diagnostic Modules](mariadb-maxscale-20-mariadb-maxscale-configuration-usage-scenarios.md#diagnostic-modules)
* [Monitor Modules](mariadb-maxscale-20-mariadb-maxscale-configuration-usage-scenarios.md#monitor-modules)
* [Filter Modules](mariadb-maxscale-20-mariadb-maxscale-configuration-usage-scenarios.md#filter-modules)
* [Reloading Configuration](mariadb-maxscale-20-mariadb-maxscale-configuration-usage-scenarios.md#reloading-configuration)
* [Authentication](mariadb-maxscale-20-mariadb-maxscale-configuration-usage-scenarios.md#authentication)
* [Error Reporting](mariadb-maxscale-20-mariadb-maxscale-configuration-usage-scenarios.md#error-reporting)

#### Terms

| Term                | Description                                                                                                                                                                                                                                                                                                                                      |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Term                | Description                                                                                                                                                                                                                                                                                                                                      |
| service             | A service represents a set of databases with a specific access mechanism that is offered to clients of MariaDB MaxScale. The access mechanism defines the algorithm that MariaDB MaxScale will use to direct particular requests to the individual databases.                                                                                    |
| server              | A server represents an individual database server to which a client can be connected via MariaDB MaxScale.                                                                                                                                                                                                                                       |
| router              | A router is a module within MariaDB MaxScale that will route client requests to the various database servers which MariaDB MaxScale provides a service interface to.                                                                                                                                                                             |
| connection routing  | Connection routing is a method of handling requests in which MariaDB MaxScale will accept connections from a client and route data on that connection to a single database using a single connection. Connection based routing will not examine individual requests on a connection and it will not move that connection once it is established. |
| statement routing   | Statement routing is a method of handling requests in which each request within a connection will be handled individually. Requests may be sent to one or more servers and connections may be dynamically added or removed from the session.                                                                                                     |
| protocol            | A protocol is a module of software that is used to communicate with another software entity within the system. MariaDB MaxScale supports the dynamic loading of protocol modules to allow for increased flexibility.                                                                                                                             |
| module              | A module is a separate code entity that may be loaded dynamically into MariaDB MaxScale to increase the available functionality. Modules are implemented as run-time loadable shared objects.                                                                                                                                                    |
| monitor             | A monitor is a module that can be executed within MariaDB MaxScale to monitor the state of a set of database. The use of an internal monitor is optional, monitoring may be performed externally to MariaDB MaxScale.                                                                                                                            |
| listener            | A listener is the network endpoint that is used to listen for connections to MariaDB MaxScale from the client applications. A listener is associated to a single service, however, a service may have many listeners.                                                                                                                            |
| connection failover | When a connection currently being used between MariaDB MaxScale and the database server fails a replacement will be automatically created to another server by MariaDB MaxScale without client intervention                                                                                                                                      |
| backend database    | A term used to refer to a database that sits behind MariaDB MaxScale and is accessed by applications via MariaDB MaxScale.                                                                                                                                                                                                                       |
| filter              | A module that can be placed between the client and the MariaDB MaxScale router module. All client data passes through the filter module and may be examined or modified by the filter modules. Filters may be chained together to form processing pipelines.                                                                                     |

### Configuration

The MariaDB MaxScale configuration is read from a file that MariaDB MaxScale will look for\
in a number of places.

1. Location given with the --configdir= command line argument
2. MariaDB MaxScale will look for a configuration file called `maxscale.cnf` in the directory `/etc/maxscale.cnf`

An explicit path to a configuration file can be passed by using the `-f` option to MariaDB MaxScale.

The configuration file itself is based on the ".ini" file format and consists of various sections that are used to build the configuration; these sections define services, servers, listeners, monitors and global settings. Parameters, which expect a comma-separated list of values can be defined on multiple lines. The following is an example of a multi-line definition.

```
[MyService]
type=service
router=readconnroute
servers=server1,
        server2,
        server3
```

The values of the parameter that are not on the first line need to have at least one whitespace character before them in order for them to be recognized as a part of the multi-line parameter.

#### Global Settings

The global settings, in a section named `[MaxScale]`, allow various parameters that affect MariaDB MaxScale as a whole to be tuned.

**`threads`**

This parameter controls the number of worker threads that are handling the\
events coming from the kernel. The default is 1 thread. It is recommended that\
you start with one thread and increase the number if you require greater\
performance. Increasing the amount of worker threads beyond the number of\
processor cores does not improve the performance, rather is likely to degrade\
it, and can consume resources needlessly.

You can enable automatic configuration of this value by setting the value to`auto`. This way MariaDB MaxScale will detect the number of available processors\
and set the amount of threads to be equal to that number minus one. This should\
only be used for systems dedicated for running MariaDB MaxScale.

```
# Valid options are:
#       threads=[<number of threads> | auto ]

[MaxScale]
threads=1
```

It should be noted that additional threads will be created to execute other internal services within MariaDB MaxScale. This setting is used to configure the number of threads that will be used to manage the user connections.

**`auth_connect_timeout`**

The connection timeout in seconds for the MySQL connections to the backend server when user authentication data is fetched. Increasing the value of this parameter will cause MariaDB MaxScale to wait longer for a response from the backend server before aborting the authentication process. The default is 3 seconds.

**`auth_read_timeout`**

The read timeout in seconds for the MySQL connection to the backend database when user authentication data is fetched. Increasing the value of this parameter will cause MariaDB MaxScale to wait longer for a response from the backend server when user data is being actively fetched. If the authentication is failing and you either have a large number of database users and grants or the connection to the backend servers is slow, it is a good idea to increase this value. The default is 1 second.

**`auth_write_timeout`**

The write timeout in seconds for the MySQL connection to the backend database when user authentication data is fetched. Currently MariaDB MaxScale does not write or modify the data in the backend server. The default is 2 seconds.

**`ms_timestamp`**

Enable or disable the high precision timestamps in logfiles. Enabling this adds millisecond precision to all logfile timestamps.

```
# Valid options are:
#       ms_timestamp=<0|1>
ms_timestamp=1
```

**`syslog`**

Enable or disable the logging of messages to _syslog_.

By default logging to _syslog_ is enabled.

```
# Valid options are:
#       syslog=<0|1>
syslog=1
```

To enable logging to syslog use the value 1 and to disable use\
the value 0.

**`maxlog`**

Enable to disable to logging of messages to MariaDB MaxScale's log file.

By default logging to _maxlog_ is enabled.

```
# Valid options are:
#       syslog=<0|1>
maxlog=1
```

To enable logging to the MariaDB MaxScale log file use the value 1 and to\
disable use the value 0.

**`log_to_shm`**

Enable or disable the writing of the _maxscale.log_ file to shared memory.\
If enabled, then the actual log file will be created under `/dev/shm` and\
a symbolic link to that file will be created in the _MaxScale_ log directory.

Logging to shared memory may be appropriate if _log\_info_ and/or _log\_debug_\
are enabled, as logging to a regular file may in that case cause performance\
degradation, due to the amount of data logged. However, as shared memory is\
a scarce resource, logging to shared memory should be used only temporarily\
and not regularly.

Since _MariaDB MaxScale_ can log to both file and _syslog_ an approach that provides\
maximum flexibility is to enable _syslog_ and _log\_to\_shm_, and to disabl&#x65;_&#x6D;axlog_. That way messages will normally be logged to _syslog_, but if\
there is something to investigate, _log\_info_ and _maxlog_ can be enabled\
from _maxadmin_, in which case informational messages will be logged to\
the _maxscale.log_ file that resides in shared memory.

By default, logging to shared memory is disabled.

```
# Valid options are:
#       log_to_shm=<0|1>
log_to_shm=1
```

To enable logging to shared memory use the value 1 and to disable use\
the value 0.

**`log_warning`**

Enable or disable the logging of messages whose syslog priority is _warning_.\
Messages of this priority are enabled by default.

```
# Valid options are:
#       log_warning=<0|1>
log_warning=0
```

To disable these messages use the value 0 and to enable them use the value 1.

**`log_notice`**

Enable or disable the logging of messages whose syslog priority is _notice_.\
Messages of this priority provide information about the functioning of\
MariaDB MaxScale and are enabled by default.

```
# Valid options are:
#       log_notice=<0|1>
log_notice=0
```

To disable these messages use the value 0 and to enable them use the value 1.

**`log_info`**

Enable or disable the logging of messages whose syslog priority is _info_.\
These messages provide detailed information about the internal workings of\
MariaDB MaxScale and should not, due to their frequency, be enabled, unless there\
is a specific reason for that. For instance, from these messages it will be\
evident, e.g., why a particular query was routed to the master instead of\
to a slave. These informational messages are disabled by default.

```
# Valid options are:
#       log_info=<0|1>
log_info=1
```

To disable these messages use the value 0 and to enable them use the value 1.

**`log_debug`**

Enable or disable the logging of messages whose syslog priority is _debug_. This kind of messages are intended for development purposes and are disabled by default.

```
# Valid options are:
#       log_debug=<0|1>
log_debug=1
```

To disable these messages use the value 0 and to enable them use the value 1.

**`log_messages`**

**Deprecated** Use _log\_notice_ instead.

**`log_trace`**

**Deprecated** Use _log\_info_ instead.

**`log_augmentation`**

Enable or disable the augmentation of messages. If this is enabled, then each logged message is appended with the name of the function where the message was logged. This is primarily for development purposes and hence is disabled by default.

```
# Valid options are:
#       log_augmentation=<0|1>
log_augmentation=1
```

To disable the augmentation use the value 0 and to enable it use the value 1.

**`logdir`**

Set the directory where the logfiles are stored. The folder needs to be both readable and writable by the user running MariaDB MaxScale.

```
logdir=/tmp/
```

**`datadir`**

Set the directory where the data files used by MariaDB MaxScale are stored. Modules can write to this directory and for example the binlogrouter uses this folder as the default location for storing binary logs.

```
datadir=/home/user/maxscale_data/
```

**`libdir`**

Set the directory where MariaDB MaxScale looks for modules. The library directory is the only directory that MariaDB MaxScale uses when it searches for modules. If you have custom modules for MariaDB MaxScale, make sure you have them in this folder.

```
libdir=/home/user/lib64/
```

**`cachedir`**

Configure the directory MariaDB MaxScale uses to store cached data. An example of cached data is the authentication data fetched from the backend servers. MariaDB MaxScale stores this in case a connection to the backend server is not possible.

```
cachedir=/tmp/maxscale_cache/
```

**`piddir`**

Configure the directory for the PID file for MariaDB MaxScale. This file contains the Process ID for the running MariaDB MaxScale process.

```
piddir=/tmp/maxscale_cache/
```

**`execdir`**

Configure the directory where the executable files reside. All internal processes which are launched will use this directory to look for executable files.

```
execdir=/usr/local/bin/
```

**`language`**

Set the folder where the errmsg.sys file is located in. MariaDB MaxScale will look for the errmsg.sys file installed with MariaDB MaxScale from this folder.

```
language=/home/user/lang/
```

**`query_classifier`**

The module used by MariaDB MaxScale for query classification. The information\
provided by this module is used by MariaDB MaxScale when deciding where a\
particular statement should be sent. The default query classifier\
is _qc\_sqlite_.

**`query_classifier_args`**

Arguments for the query classifier. What arguments are accepted depends\
on the particular query classifier being used. The default query\
classifier - _qc\_sqlite_ - supports the following arguments:

**`log_unrecognized_statements`**

An integer argument taking the following values:

* 0: Nothing is logged. This is the default.
* 1: Statements that cannot be parsed completely are logged. They may have been partially parsed, or classified based on keyword matching.
* 2: Statements that cannot even be partially parsed are logged. They may have been classified based on keyword matching.
* 3: Statements that cannot even be classified by keyword matching are logged.

```
query_classifier=qc_sqlite
query_classifier_args=log_unrecognized_statements=1
```

This will log all statements that cannot be parsed completely. This\
may be useful if you suspect that MariaDB MaxScale routes statements to the wrong\
server (e.g. to a slave instead of to a master).

#### Service

A service represents the database service that MariaDB MaxScale offers to the clients. In general a service consists of a set of backend database servers and a routing algorithm that determines how MariaDB MaxScale decides to send statements or route connections to those backend servers.

A service may be considered as a virtual database server that MariaDB MaxScale makes available to its clients.

Several different services may be defined using the same set of backend servers. For example a connection based routing service might be used by clients that already performed internal read/write splitting, whilst a different statement based router may be used by clients that are not written with this functionality in place. Both sets of applications could access the same data in the same databases.

A service is identified by a service name, which is the name of the configuration file section and a type parameter of service

```
[Test Service]
type=service
```

In order for MariaDB MaxScale to forward any requests it must have at least one service defined within the configuration file. The definition of a service alone is not enough to allow MariaDB MaxScale to forward requests however, the service is merely present to link together the other configuration elements.

**`router`**

The router parameter of a service defines the name of the router module that will be used to implement the routing algorithm between the client of MariaDB MaxScale and the backend databases. Additionally routers may also be passed a comma separated list of options that are used to control the behavior of the routing algorithm. The two parameters that control the routing choice are router and router\_options. The router options are specific to a particular router and are used to modify the behavior of the router. The read connection router can be passed options of master, slave or synced, an example of configuring a service to use this router and limiting the choice of servers to those in slave state would be as follows.

```
router=readconnroute
router_options=slave
```

To change the router to connect on to servers in the master state as well as slave servers, the router options can be modified to include the master state.

```
router=readconnroute
router_options=master,slave
```

A more complete description of router options and what is available for a given router is included with the documentation of the router itself.

**`filters`**

The filters option allow a set of filters to be defined for a service; requests from the client are passed through these filters before being sent to the router for dispatch to the backend server. The filters parameter takes one or more filter names, as defined within the filter definition section of the configuration file. Multiple filters are separated using the | character.

```
filters=counter | QLA
```

The requests pass through the filters from left to right in the order defined in the configuration parameter.

**`servers`**

The servers parameter in a service definition provides a comma separated list of the backend servers that comprise the service. The server names are those used in the name section of a block with a type parameter of server (see below).

```
servers=server1,server2,server3
```

**`user`**

The user parameter, along with the passwd parameter are used to define the credentials used to connect to the backend servers to extract the list of database users from the backend database that is used for the client authentication.

```
user=maxscale
passwd=Mhu87p2D
```

Authentication of incoming connections is performed by MariaDB MaxScale itself rather than by the database server to which the client is connected. The client will authenticate itself with MariaDB MaxScale, using the username, hostname and password information that MariaDB MaxScale has extracted from the backend database servers. For a detailed discussion of how this impacts the authentication process please see the "Authentication" section below.

The host matching criteria is restricted to IPv4, IPv6 will be added in a future release.

Existing user configuration in the backend databases must be checked and may be updated before successful MariaDB MaxScale authentication:

In order for MariaDB MaxScale to obtain all the data it must be given a username it can use to connect to the database and retrieve that data. This is the parameter that gives MariaDB MaxScale the username to use for this purpose.

The account used must be able to select from the mysql.user table, the following is an example showing how to create this user.

```
MariaDB [mysql]> CREATE USER 'maxscale'@'maxscalehost' IDENTIFIED BY 'Mhu87p2D';
Query OK, 0 rows affected (0.01 sec)

MariaDB [mysql]> GRANT SELECT ON mysql.user TO 'maxscale'@'maxscalehost';
Query OK, 0 rows affected (0.00 sec)
```

Additionally, `SELECT` privileges on the `mysql.db` and `mysql.tables_priv` tables and `SHOW DATABASES` privileges are required in order to load databases name and grants suitable for database name authorization.

```
MariaDB [(none)]> GRANT SELECT ON mysql.db TO 'maxscale'@'maxscalehost';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> GRANT SELECT ON mysql.tables_priv TO 'maxscale'@'maxscalehost';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> GRANT SHOW DATABASES ON *.* TO 'maxscale'@'maxscalehost';
Query OK, 0 rows affected (0.00 sec)
```

MariaDB MaxScale will execute the following query to retrieve the users. If you suspect that you might have problems with grants, it is recommended to run this query and see the results it returns.

```
SELECT DISTINCT
    user.user AS user,
    user.host AS host,
    user.password AS password,
    concat(user.user,user.host,user.password,
      IF((user.Select_priv+0)||find_in_set('Select',Coalesce(tp.Table_priv,0)),'Y','N') ,
      COALESCE( db.db,tp.db, '')) AS userdata,
    user.Select_priv AS anydb,
    COALESCE( db.db,tp.db, NULL) AS db
    FROM
    mysql.user LEFT JOIN
    mysql.db ON user.user=db.user AND user.host=db.host LEFT JOIN
    mysql.tables_priv tp ON user.user=tp.user AND user.host=tp.host
    WHERE user.user IS NOT NULL AND user.user <> ''
```

In versions of MySQL 5.7.6 and later, the `Password` column was replaced by `authentication_string`. Change `user.password` above with `user.authentication_string`.

**`passwd`**

The passwd parameter provides the password information for the above user and may be either a plain text password or it may be an encrypted password. See the section on encrypting passwords for use in the maxscale.cnf file. This user must be capable of connecting to the backend database and executing these SQL statements to load database names and grants from the backends:

* `SELECT user, host, password,Select_priv FROM mysql.user`.
* `SELECT user, host, db FROM mysql.db`
* `SELECT * FROM INFORMATION_SCHEMA.SCHEMATA`
* `SELECT GRANTEE,PRIVILEGE_TYPE FROM INFORMATION_SCHEMA.USER_PRIVILEGES`

**`enable_root_user`**

This parameter controls the ability of the root user to connect to MariaDB MaxScale and hence onwards to the backend servers via MariaDB MaxScale.

The default value is `0`, disabling the ability of the root user to connect to MariaDB MaxScale.

Example for enabling root user:

```
enable_root_user=1
```

Values of `on` or `true` may also be given to enable the root user and `off` or `false` may be given to disable the use of the root user.

```
enable_root_user=true
```

**`localhost_match_wildcard_host`**

This parameter enables matching of "127.0.0.1" (localhost) against "%" wildcard host for MySQL protocol authentication. The default value is `0`, so in order to authenticate a connection from the same machine as the one on which MariaDB MaxScale is running, an explicit user@localhost entry will be required in the MySQL user table.

**`version_string`**

This parameter sets a custom version string that is sent in the MySQL Handshake from MariaDB MaxScale to clients.

Example:

```
version_string=5.5.37-MariaDB-RWsplit
```

If not set, the default value is the server version of the embedded MySQL/MariaDB library. Example: 5.5.35-MariaDB

**`weightby`**

The weightby parameter is used in conjunction with server parameters in order to\
control the load balancing applied in the router in use by the service. This\
allows varying weights to be applied to each server to create a non-uniform\
distribution of the load amongst the servers.

An example of this might be to define a parameter for each server that represents\
the amount of resource available on the server, we could call this serversize.\
Every server should then have a serversize parameter set for the server.

```
serversize=10
```

The service would then have the parameter `weightby=serversize`. If there are 4\
servers defined in the service (serverA, serverB, serverC and serverD) with the\
serversize set as shown in the table below, the connections would balanced\
using the percentages in this table.

| Server  | serversize | % connections |
| ------- | ---------- | ------------- |
| Server  | serversize | % connections |
| serverA | 10         | 18%           |
| serverB | 15         | 27%           |
| serverC | 10         | 18%           |
| serverD | 20         | 36%           |

_Note: If the value of the weighting parameter of an individual server is_\
\&#xNAN;_zero or the relative weight rounds down to zero, no queries will be routed to_\
\&#xNAN;_that server as long as a server with a positive weight is available._

Here is an excerpt from an example configuration with the `serv_weight` parameter\
used as the weighting parameter.

```
[server1]
type=server
address=127.0.0.1
port=3000
protocol=MySQLBackend
serv_weight=3

[server2]
type=server
address=127.0.0.1
port=3001
protocol=MySQLBackend
serv_weight=1

[Read Service]
type=service
router=readconnroute
servers=server1,server2
weightby=serv_weight
```

With this configuration and a heavy query load, the server _server1_ will get\
most of the connections and about a third of the remaining queries are routed\
to the second server. With server weights, you can assign secondary servers\
that are only used when the primary server is under heavy load.

Without the weightby parameter, each connection counts as a single connection.\
With a weighting parameter, a single connection received its weight from\
the server's own weighting parameter divided by the sum of all weighting\
parameters in all the configured servers.

If we use the previous configuration as an example, the sum of the `serv_weight`\
parameter is 4. _Server1_ would receive a weight of `3/4=75%` and _server2_ would get`1/4=25%`. This means that _server1_ would get 75% of the connections and _server2_\
would get 25% of the connections.

**`auth_all_servers`**

This parameter controls whether only a single server or all of the servers are used when loading the users from the backend servers. This takes a boolean value and when enabled, creates a union of all the users and grants on all the servers.

**`strip_db_esc`**

The strip\_db\_esc parameter strips escape characters from database names of\
grants when loading the users from the backend server.

This parameter takes a boolean value and when enabled, will strip all backslash\
(`\`) characters from the database names. The default value for this parameter\
is true since MaxScale 2.0.1. In previous version, the default value was false.

Some visual database management tools automatically escape some characters and\
this might cause conflicts when MariaDB MaxScale tries to authenticate users.

**`retry_on_failure`**

The retry\_on\_failure parameter controls whether MariaDB MaxScale will try to restart failed services and accepts a boolean value. This functionality is enabled by default to prevent services being permanently disabled if the starting of the service failed due to a network outage. Disabling the restarting of the failed services will cause them to be permanently disabled if the services can't be started when MariaDB MaxScale is started.

**`log_auth_warnings`**

Enable or disable the logging of authentication failures and warnings. This parameter takes a boolean value.

MariaDB MaxScale normally suppresses warning messages about failed authentication. Enabling this option will log those messages into the message log with details about who tried to connect to MariaDB MaxScale and from where.

**`connection_timeout`**

The connection\_timeout parameter is used to disconnect sessions to MariaDB MaxScale that have been idle for too long. The session timeouts are disabled by default. To enable them, define the timeout in seconds in the service's configuration section.

Example:

```
[Test Service]
connection_timeout=300
```

**`max_connections`**

The maximum number of simultaneous connections MaxScale should permit to this service. If the parameter is zero or is omitted, there is no limit. Any attempt to make more connections after the limit is reached will result in a "Too many connections" error being returned.

Example:

```
[Test Service]
max_connections=100
```

#### Server

Server sections are used to define the backend database servers that can be formed into a service. A server may be a member of one or more services within MariaDB MaxScale. Servers are identified by a server name which is the section name in the configuration file. Servers have a type parameter of server, plus address port and protocol parameters.

```
[server1]
type=server
address=127.0.0.1
port=3000
protocol=MySQLBackend
```

**`address`**

The IP address or hostname of the machine running the database server that is being defined. MariaDB MaxScale will use this address to connect to the backend database server.

**`port`**

The port on which the database listens for incoming connections. MariaDB MaxScale will use this port to connect to the database server.

**`protocol`**

The name for the protocol module to use to connect MariaDB MaxScale to the database. Currently only one backend protocol is supported, the MySQLBackend module.

**`monitoruser`**

The monitor has a username and password that is used to connect to all servers for monitoring purposes, this may be overridden by supplying a monitoruser statement for each individual server

```
monitoruser=mymonitoruser
```

**`monitorpw`**

The monitor has a username and password that is used to connect to all servers for monitoring purposes, this may be overridden by supplying a monpasswd statement for the individual servers

```
monitorpw=mymonitorpasswd
```

The monpasswd parameter may be either a plain text password or it may be an encrypted password. See the section on encrypting passwords for use in the maxscale.cnf file.

**`persistpoolmax`**

The `persistpoolmax` parameter defaults to zero but can be set to an integer value for a back end server.\
If it is non zero, then when a DCB connected to a back end server is discarded by the\
system, it will be held in a pool for reuse, remaining connected to the back end server.\
If the number of DCBs in the pool has reached the value given by `persistpoolmax` then\
any further DCB that is discarded will not be retained, but disconnected and discarded.

**`persistmaxtime`**

The `persistmaxtime` parameter defaults to zero but can be set to an integer value\
indicating a number of seconds. A DCB placed in the persistent pool for a server will\
only be reused if the elapsed time since it joined the pool is less than the given\
value. Otherwise, the DCB will be discarded and the connection closed.

For more information about persistent connections, please read the [Administration Tutorial](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/).

#### Server and SSL

This section describes configuration parameters for servers that control the SSL/TLS encryption method and the various certificate files involved in it when applied to back end servers. To enable SSL between MaxScale and a back end server, you must configure the `ssl` parameter in the relevant server section to the value `required` and provide the three files for `ssl_cert`, `ssl_key` and `ssl_ca_cert`. After this, MaxScale connections to this server will be encrypted with SSL. Attempts to connect to the server without using SSL will cause failures. Hence, the database server in question must have been configured to be able to accept SSL connections.

**`ssl`**

This enables SSL connections to the server, when set to `required`. If that is done, the three certificate files mentioned below must also be supplied. MaxScale connections to this server will then be encrypted with SSL. If this is not possible, client connection attempts that rely on the server will fail.

**`ssl_key`**

A string giving a file path that identifies an existing readable file. The file must be the SSL client private key MaxScale should use with the server. This will be the private key that is used as the client side private key during a MaxScale-server SSL handshake. This is currently a required parameter for SSL enabled servers.

**`ssl_cert`**

A string giving a file path that identifies an existing readable file. The file must be the SSL client certificate MaxScale should use with the server. This will be the public certificate that is used as the client side certificate during a MaxScale-server SSL handshake. This is a required parameter for SSL enabled servers. The certificate must be compatible with the key defined above.

**`ssl_ca_cert`**

A string giving a file path that identifies an existing readable file. The file must be the SSL Certificate Authority (CA) certificate for the CA that signed the client certificate referred to in the previous parameter. It will be used to verify that the client certificate is valid. This is a required parameter for SSL enabled listeners.

**`ssl_version`**

This parameter controls the level of encryption used. Accepted values are:

* TLSv10
* TLSv11
* TLSv12
* MAX

Not all backend servers will support TLSv11 or TLSv12. If available, TLSv12 should be used.

**`ssl_cert_verification_depth`**

The maximum length of the certificate authority chain that will be accepted. Legal values are positive integers. Note that if the client is to submit an SSL certificate, the `ssl_cert_verification_depth` parameter must not be 0. If no value is specified, the default is 9.

```
# Example
ssl_cert_verification_depth=5
```

**Example SSL enabled server configuration:**

```
[server1]
type=server
address=10.131.24.62
port=3306
protocol=MySQLBackend
#persistpoolmax=200
persistmaxtime=3000
ssl=required
ssl_version=TLSv10
ssl_cert=/usr/local/mariadb/maxscale/ssl/crt.max-client.pem
ssl_key=/usr/local/mariadb/maxscale/ssl/key.max-client.pem
ssl_ca_cert=/usr/local/mariadb/maxscale/ssl/crt.ca.maxscale.pem
```

This example configuration requires all connections to this server to be encrypted with SSL. It also specifies that TLSv1.0 should be used as the encryption method. The paths to the server certificate files and the Certificate Authority file are also provided.

#### Listener

The listener defines a port and protocol pair that is used to listen for connections to a service. A service may have multiple listeners associated with it, either to support multiple protocols or multiple ports. As with other elements of the configuration the section name is the listener name and it can be selected freely. A type parameter is used to identify the section as a listener definition. Address is optional and it allows the user to limit connections to certain interface only. Socket is also optional and used for Unix socket connections.

The network socket where the listener listens will have a backlog of\
connections. The size of this backlog is controlled by the\
net.ipv4.tcp\_max\_syn\_backlog and net.core.somaxconn kernel parameters.

Increasing the size of the backlog by modifying the kernel parameters\
helps with sudden connection spikes and rejected connections. For more\
information see [listen(2)](https://man7.org/linux/man-pages/man2/listen.2.html).

```
[<Listener name>]
type=listener
service=<Service name>]
protocol=[MySQLClient|HTTPD]
address=[IP|hostname]
port=<Listen port number>
socket=<Socket path>
```

**`service`**

The service to which the listener is associated. This is the name of a service that is defined elsewhere in the configuration file.

**`protocol`**

The name of the protocol module that is used for the communication between the client and MariaDB MaxScale itself.

**`address`**

The address option sets the address that will be used to bind the listening socket. The address may be specified as an IP address in 'dot notation' or as a hostname. If the address option is not included in the listener definition the listener will bind to all network interfaces.

**`port`**

The port to use to listen for incoming connections to MariaDB MaxScale from the clients. If the port is omitted from the configuration a default port for the protocol will be used.

**`socket`**

The `socket` option may be included in a listener definition, this configures the listener to use Unix domain sockets to listen for incoming connections. The parameter value given is the name of the socket to use.

If a socket option and an address option is given then the listener will listen on both the specific IP address and the Unix socket.

**Available Protocols**

The protocols supported by MariaDB MaxScale are implemented as external modules that are loaded dynamically into the MariaDB MaxScale core. They allow MariaDB MaxScale to communicate in various protocols both on the client side and the backend side. Each of the protocols can be either a client protocol or a backend protocol. Client protocols are used for client-MariaDB MaxScale communication and backend protocols are for MariaDB MaxScale-database communication.

**`MySQLClient`**

This is the implementation of the MySQL protocol that is used by clients of MariaDB MaxScale to connect to MariaDB MaxScale.

**`MySQLBackend`**

The MySQLBackend protocol module is the implementation of the protocol that MariaDB MaxScale uses to connect to the backend MySQL, MariaDB and Percona Server databases. This implementation is tailored for the MariaDB MaxScale to MySQL Database traffic and is not a general purpose implementation of the MySQL protocol.

**`telnetd`**

The telnetd protocol module is used for connections to MariaDB MaxScale itself for the purposes of creating interactive user sessions with the MariaDB MaxScale instance itself. Currently this is used in conjunction with a special router implementation, the debugcli.

**`maxscaled`**

The protocol used used by the maxadmin client application in order to connect to MariaDB MaxScale and access the command line interface.

**`HTTPD`**

This protocol module is currently still under development, it provides a means to create HTTP connections to MariaDB MaxScale for use by web browsers or RESTful API clients.

#### Listener and SSL

This section describes configuration parameters for listeners that control the SSL/TLS encryption method and the various certificate files involved in it. To enable SSL from client to MaxScale, you must configure the `ssl` parameter to the value `required` and provide the three files for `ssl_cert`, `ssl_key` and `ssl_ca_cert`. After this, MySQL connections to this listener will be encrypted with SSL. Attempts to connect to the listener with a non-SSL client will fail. Note that the same service can have an SSL listener and a non-SSL listener if you wish, although they must be on different ports.

**`ssl`**

This enables SSL connections to the listener, when set to `required`. If that is done, the three certificate files mentioned below must also be supplied. Client connections to this listener will then be encrypted with SSL. Non-SSL connections will get an error when they try to connect to the listener.

**`ssl_key`**

A string giving a file path that identifies an existing readable file. The file must be the SSL private key the listener should use. This will be the private key that is used as the server side private key during a client-server SSL handshake. This is a required parameter for SSL enabled listeners.

**`ssl_cert`**

A string giving a file path that identifies an existing readable file. The file must be the SSL certificate the listener should use. This will be the public certificate that is used as the server side certificate during a client-server SSL handshake. This is a required parameter for SSL enabled listeners. The certificate must be compatible with the key defined above.

**`ssl_ca_cert`**

A string giving a file path that identifies an existing readable file. The file must be the SSL Certificate Authority (CA) certificate for the CA that signed the server certificate referred to in the previous parameter. It will be used to verify that the server certificate is valid. This is a required parameter for SSL enabled listeners.

**`ssl_version`**

This parameter controls the level of encryption used. Accepted values are:

* TLSv10
* TLSv11
* TLSv12
* MAX

If possible, use TLSv12 for best security. Recent Linux systems will include a version of OpenSSL that supports TLS version 1.2. Only if you are using MaxScale on a system that does not have OpenSSL with support for this should earlier versions be used. It is unlikely that TLS 1.1 will be available unless TLS 1.2 is also available. MAX will use the best available version.

**`ssl_cert_verification_depth`**

The maximum length of the certificate authority chain that will be accepted. Legal values are positive integers. Note that if the client is to submit an SSL certificate, the `ssl_cert_verification_depth` parameter must not be 0. If no value is specified, the default is 9.

```
# Example
ssl_cert_verification_depth=5
```

**Example SSL enabled listener configuration:**

```
[RW Split Listener]
type=listener
service=RW Split Router
protocol=MySQLClient
address=10.131.218.83
port=3306
authenticator=MySQL
ssl=required
ssl_cert=/usr/local/mariadb/maxscale/ssl/crt.maxscale.pem
ssl_key=/usr/local/mariadb/maxscale/ssl/key.csr.maxscale.pem
ssl_ca_cert=/usr/local/mariadb/maxscale/ssl/crt.ca.maxscale.pem
ssl_version=TLSv12
ssl_cert_verify_depth=9
```

This example configuration requires all connections to be encrypted with SSL. It also specifies that TLSv1.2 should be used as the encryption method. The paths to the server certificate files and the Certificate Authority file are also provided.

### Routing Modules

The main task of MariaDB MaxScale is to accept database connections from client applications and route the connections or the statements sent over those connections to the various services supported by MariaDB MaxScale.

Currently a number of routing modules are available, these are designed for a range of different needs.

Connection based load balancing:

* [ReadConnRoute](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)

Read/Write aware statement based router:

* [ReadWriteSplit](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)

Simple sharding on database level:

* [SchemaRouter](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)

Binary log server:

* [Binlogrouter](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)

### Diagnostic modules

These modules are used for diagnostic purposes and can tell about the status of MariaDB MaxScale and the cluster it is monitoring.

* [MaxAdmin Module](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [Telnet Module](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)

### Monitor Modules

Monitor modules are used by MariaDB MaxScale to internally monitor the state of the backend databases in order to set the server flags for each of those servers. The router modules then use these flags to determine if the particular server is a suitable destination for routing connections for particular query classifications. The monitors are run within separate threads of MariaDB MaxScale and do not affect MariaDB MaxScale's routing performance.

The use of monitors is highly recommended but it is also possible to run MariaDB MaxScale without a monitor module. In this case an external monitoring system which sets the status of each server via MaxAdmin is needed.

* [Mysql Monitor](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [Galera Monitor](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [NDBCluster Monitor](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [Multi-Master Monitor](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)

### Filter Modules

![](<../../../../.gitbook/assets/image_10.png (3).png>)

Filters provide a means to manipulate or process requests as they pass through MariaDB MaxScale between the client side protocol and the query router. A full explanation of each filter's functionality can be found in its documentation.

The [Filter Tutorial](../maxscale-20-tutorials/5948.md) document shows how you can add a filter to a service and combine multiple filters in one service.

* [Query Log All (QLA) Filter](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [Regular Expression Filter](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [Tee Filter](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [Top Filter](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [Database Firewall Filter](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [Query Redirection Filter](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [RabbitMQ Filter](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)

### Reloading Configuration

The current MariaDB MaxScale configuration may be updated by editing the\
configuration file and then forcing MariaDB MaxScale to reread the configuration\
file. To force MariaDB MaxScale to reread the configuration file, send a SIGHUP\
signal to the MariaDB MaxScale process or execute `reload config` in the`maxadmin` client.

The following list of service parameters can be updated at runtime.

* user
* passwd
* enable\_root\_user
* max\_connections
* connection\_timeout
* auth\_all\_servers
* optimize\_wildcard
* strip\_db\_esc
* localhost\_match\_wildcard\_host
* max\_slave\_connections
* max\_slave\_replication\_lag

In addition to these parameters, the server specific user credentials, _monuser_\
and _monpw_, can also be updated at runtime.

#### Limitations

Services that are removed via the configuration update mechanism can not be physically removed from MariaDB MaxScale until there are no longer any connections using the service.

When the number of threads is decreased the threads will not actually be terminated until such time as they complete the current operation of that thread.

Monitors can not be completely removed from the running MariaDB MaxScale.

### Authentication

MySQL uses username, passwords and the client host in order to authenticate a user, so a typical user would be defined as user X at host Y and would be given a password to connect. MariaDB MaxScale uses exactly the same rules as MySQL when users connect to the MariaDB MaxScale instance, i.e. it will check the address from which the client is connecting and treat this in exactly the same way that MySQL would. MariaDB MaxScale will pull the authentication data from one of the backend servers and use this to match the incoming connections, the assumption being that all the backend servers for a particular service will share the same set of user credentials.

It is important to understand, however, that when MariaDB MaxScale itself makes connections to the backend servers the backend server will see all connections as originating from the host that runs MariaDB MaxScale and not the original host from which the client connected to MariaDB MaxScale. Therefore the backend servers should be configured to allow connections from the MariaDB MaxScale host for every user that can connect from any host. Since there is only a single password within the database server for a given host, this limits the configuration such that a given user name must have the same password for every host from which they can connect.

To clarify, if a user _X_ is defined as using password _pass1_ from host _a_ and _pass2_ from host _b_ then there must be an entry in the `user` table for user _X_ from the MariaDB MaxScale host, say _pass1_.

This would result in rows in the user table as follows

| Username | Password | Client Host |
| -------- | -------- | ----------- |
| Username | Password | Client Host |
| X        | pass1    | a           |
| X        | pass2    | b           |
| X        | pass1    | MaxScale    |

In this case the user _X_ would be able to connect to MariaDB MaxScale from host a giving the password of _pass1_. In addition MariaDB MaxScale would be able to create connections for this user to the backend servers using the username _X_ and password _pass1_, since the MariaDB MaxScale host is also defined to have password _pass1_. User _X_ would not however be able to connect from host _b_ since they would need to provide the password _pass2_ in order to connect to MariaDB MaxScale, but then MariaDB MaxScale would not be able to connect to the backends as it would also use the password _pass2_ for these connections.

#### Wildcard Hosts

Hostname mapping in MariaDB MaxScale works in exactly the same way as for MySQL, if the wildcard is used for the host then any host other than the localhost (127.0.0.1) will match. It is important to consider that the localhost check will be performed at the MariaDB MaxScale level and at the MySQL server level.

If MariaDB MaxScale and the databases are on separate hosts there are two important changes in behavior to consider:

1. Clients running on the same machine as the backend database now may access the database using the wildcard entry. The localhost check between the client and MariaDB MaxScale will allow the use of the wildcard, since the client is not running on the MariaDB MaxScale host. Also the wildcard entry can be used on the database host as MariaDB MaxScale is making that connection and it is not running on the same host as the database.
2. Clients running on the same host as MariaDB MaxScale can not access the database via MariaDB MaxScale using the wildcard entry since the connection to MariaDB MaxScale will be from the localhost. These clients are able to access the database directly, as they will use the wildcard entry.

If MariaDB MaxScale is running on the same host as one or more of the database nodes to which it is routing statements then the wildcard host entries can be used to connect to MariaDB MaxScale but not to connect onwards to the database running on the same node.

In all these cases the issue may be solved by adding an explicit entry for the localhost address that has the same password as the wildcard entry. This may be done using a statement as below for each of the databases that are required:

```
MariaDB [mysql]> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP ON employee.* 'user1'@'localhost' IDENTIFIED BY 'xxx';
Query OK, 0 rows affected (0.00 sec)
```

#### Limitations

At the time of writing the authentication mechanism within MariaDB MaxScale does not support IPV6 address matching in connections rules. This is also in line with the current protocol modules that do not support IPV6.

Wildcard address supported in the current version of MariaDB MaxScale are:

192.168.3.%\
192.168.%.%\
192.%.%.%

and short notations

192.%\
192.%.%\
192.168.%

Note that currently wildcards are only supported in conjunction with IP-addresses, not with domain names.

### Error Reporting

MariaDB MaxScale is designed to be executed as a service, therefore all error reports, including configuration errors, are written to the MariaDB MaxScale error log file. By default, MariaDB MaxScale will log to a file in `/var/log/maxscale`, the only exception to this is if the log directory is not writable, in which case a message is sent to the standard error descriptor.

#### Troubleshooting

MariaDB MaxScale binds on TCP ports and UNIX sockets as well.

If there is a local firewall in the server where MariaDB MaxScale is installed, the IP and port must be configured in order to receive connections from outside.

If the firewall is a network facility among all the involved servers, a configuration update is required as well.

Example:

```
[Galera Listener]
type=listener
address=192.168.3.33
port=4408
socket=/servers/maxscale/galera.sock
```

TCP/IP Traffic must be permitted to 192.168.3.33 port 4408

For Unix socket, the socket file path (example: `/servers/maxscale/galera.sock`) must be writable by the Unix user MariaDB MaxScale runs as.

<sub>_This page is licensed: CC BY-SA / Gnu FDL_</sub>

{% @marketo/form formId="4316" %}
