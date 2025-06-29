# MariaDB MaxScale 2.2.0 Release Notes -- 2017-10-12

Release 2.2.0 is a Beta release.

This document describes the changes in release 2.2.0, when compared to\
release 2.1.

For any problems you encounter, please consider submitting a bug\
report at [Jira](https://jira.mariadb.org).

### Changed Features

#### Whitespace in Object Names

Significant whitespace in object names is now deprecated. All object names\
(services, servers, etc.) will be converted to a compatible format by\
squeezing repeating whitespace and replacing it with hyphens. If any\
object name conversions take place, a warning will be logged.

#### Monitor Scripts

The execution of monitor scripts has been made synchronous. This means\
that a monitor will wait until the executed script is done or until a\
timeout is exceeded. The timeout is configurable with the `script_timeout`\
parameter.

In addition to this, the output of the script is logged into the MaxScale log\
file. The message is logged on the matching log level if it is prefixed with one\
of `alert:`, `error:`, `warning:`, `notice:`, `info:` or `debug:`. If no prefix\
is provided, the message is logged on the notice level.

For more information, refer to the [monitor documentation](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/).

#### Read-only Administrative Users

Users that can only perform read-only operations can be created with `add readonly-user` and `enable readonly-account` commands. To convert\
administrative users to read-only users, delete the old administrative user and\
create it as a read-only user.

For more information about administrative interface users, refer to the[MaxAdmin](../maxscale-22-reference/mariadb-maxscale-22-maxadmin-admin-interface.md) documentation.

**Note:** Old users from pre-2.2 MaxScale versions will be converted to\
administrative users that have full access to all commands.

#### MaxAdmin

The `remove user` command now only expects one parameter, the username.

#### Regular Expression Parameters

Modules may now use a built-in regular expression (regex) string parameter type\
instead of a normal string when accepting patterns. The regex parameters are\
checked by the config file loader to compile using the PCRE2 library embedded\
within MaxScale. The only module using the new regex parameter type is currentl&#x79;_&#x51;LAFilter_.

The only action users should take is enclose their regular expressions in\
slashes, e.g. `match=/^select/` defines the pattern `^select`. The slashes allow\
whitespace to be read from the ends of the regex string contrary to a normal\
string parameter and are removed before compiling the pattern. For backwards\
compatibility, the slashes are not yet mandatory. Omitting them is, however,\
deprecated and will be rejected in the next release of MaxScale.

#### `monitor_interval`

The default value of `monitor_interval` was changed from 10000 milliseconds to\
2000 milliseconds.

#### NamedServerFilter

The filter now accepts multiple match-server pairs. Please see the[NamedServerFilter](../maxscale-22-filters/mariadb-maxscale-22-named-server-filter.md) documentation for\
details.

#### Tee Filter

The `tee` filter has been rewritten to better suit the way MaxScale now\
functions. The filter requires that the service where the branched session is\
created has at least one network listener. The users must also be able to\
connect from the local MaxScale host. Usually this means that an extra grant for\
the loopback address is required (e.g. `myuser@127.0.0.1`).

In addition to the aforementioned requirements, a failure to create a branched\
session no longer causes the actual client session to be closed. In most cases,\
this is desired behavior.

The `match` and `exclude` parameters were changed to use PCRE2 syntax for the\
regular expressions. The regular expression should be enclosed by slashes\
e.g. `match=/select.*from.*test/`.

A tee filter instance can be disabled with the new `tee disable [FILTER]` and`tee enable [FILTER]` module commands. Refer to the[module command documentation](../../mariadb-maxscale-mariadb-maxscale-21/maxscale-21-reference/mariadb-maxscale-21-module-commands.md) for more\
details on module commands and the[Tee Filter documentation](../maxscale-22-filters/mariadb-maxscale-22-tee-filter.md) for details on the tee\
filter specific commands.

#### Dbfwfilter

The `function` type rule will now match a query that does not use a function\
when the filter is in whitelist mode (`action=allow`). This means that queries\
that don't use functions are allowed though in whitelist mode.

**Rule Names**

Rule names can no longer use punctuation in them and can consist only of\
alphanumeric characters, underscores and hyphens.

**Keywords `deny` and `allow`**

The `deny` and `allow` keywords are deprecated in favor of the more descriptive`match` keyword. All instances of `deny` and `allow` can be replaced with`match` with no functional changes.

#### Logging

When known, the session id will be included in all logged messages. This allows\
a range of logged messages related to a particular session (that is, client) to\
be bound together, and makes it easier to investigate problems. In practice this\
is visible so that if a logged message earlier looked like

```
2017-08-30 12:20:49   warning: [masking] The rule ...
```

it will now look like

```
2017-08-30 12:20:49   warning: (4711) [masking] The rule ...
```

where `4711` is the session id.

#### Binlogrouter Default Values

The _binlogdir_ now has a default value of `/var/lib/maxscale/`. Previously the\
parameter was mandatory even though it was documented to have a default value.

The _mariadb10-compatibility_ is enabled by default since MaxScale 2.2.0. This\
allows easier use of the MariaDB 10 series server.

### Dropped Features

#### MaxAdmin

The following deprecated commands have been removed:

* `enable log [debug|trace|message]`
* `disable log [debug|trace|message]`
* `enable sessionlog [debug|trace|message]`
* `disable sessionlog [debug|trace|message]`

The following commands have been deprecated:

* `enable sessionlog-priority <session-id> [debug|info|notice|warning]`
* `disable sessionlog-priority <session-id> [debug|info|notice|warning]`
* `reload config`

The `{ enable | disable } sessionlog-priority` commands can be issued, but they\
have no effect.

**Filenames as MaxAdmin Arguments**

MaxAdmin no longer attempts to interpret additional command line parameters as a\
file name to load commands from (e.g. `maxadmin mycommands.txt`). The shell\
indirection operator `<` should be used to achieve the same effect (`maxadmin < mycommands.txt`).

### New Features

#### REST API

MariaDB MaxScale now exposes a REST-API for obtaining information about\
and for manipulating the resources of MaxScale. For more information please\
refer to the [REST API](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/) documentation.

#### MaxCtrl Command Line Client

The MaxCtrl is a new command line intended to replace MaxAdmin. This\
client uses the REST API to communicate with MaxScale in a secure way. The\
client is distributed separately in the `maxscale-client` package.

For more information, refer to the [MaxCtrl](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)\
documentation.

#### Limited support from Pluggable Authentication Modules (PAM).

Pluggable authentication module (PAM) is a general purpose authentication API.\
An application using PAM can authenticate a user without knowledge about the\
underlying authentication implementation. For more information please refer to\
the [PAM Authenticator](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/) documentation.

#### MySQL Monitor Crash Safety

The MySQL monitor keeps a journal of the state of the servers and the currently\
elected master. This information will be read if MaxScale suffers an\
uncontrolled shutdown. By doing the journaling of server states, the mysqlmon\
monitor is able to keep track of stale master and stale slave states across\
restarts and crashes.

#### New Variables for Monitor Scripts

The PARENT and CHILDREN variables were added to the monitor scripts. The former\
expands to the direct parent node of the server that triggers the event and the\
latter expands to a list of servers that are direct descendants of the server\
that triggered the event.

For more information, refer to the [monitor documentation](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/).

#### Avrorouter `deflate` compression

The Avrorouter now supports the `deflate` compression method. This allows the\
stored Avro format files to be compressed on disk. For more information, refer\
to the [Avrorouter](../maxscale-22-routers/mariadb-maxscale-22-avrorouter.md) documentation.

#### Preliminary proxy protocol support

The MySQL backend protocol module now supports sending a proxy protocol header\
to the server. For more information, see the server section in the[Configuration guide](../maxscale-22-getting-started/mariadb-maxscale-22-mariadb-maxscale-configuration-usage-scenarios.md).

#### KILL command support

The MySQL client protocol now supports execution of `KILL` statements through\
MaxScale. The connection IDs in these queries will be transformed into the\
correct ones by MaxScale.

`KILL QUERY ID <query_id>` is not supported by MaxScale and it needs to be\
executed directly on the relevant backend server. In addition to this, there are\
minor limitations to the `KILL` command handling. See[Limitations](../about-maxscale-22/mariadb-maxscale-22-limitations-and-known-issues-within-mariadb-maxscale.md) for more information.

#### Obfuscation and partial masking added to the masking filter.

A value can now be obfuscated instead of just masked. Further, it is\
possible to specify with a regular expression that only a specific part\
of a value should be masked. For more information, please read the[masking filter](../maxscale-22-filters/mariadb-maxscale-22-masking.md) documentation.

#### New rules for dbfwfilter

The `uses_function` type rule prevents certain columns from being used\
with functions. It is now also possible to match a function if it is\
used in conjunction with specific columns. For more information about\
the new rules, read the[dbfwfilter](../maxscale-22-filters/mariadb-maxscale-22-database-firewall-filter.md) documentation.

### Bug fixes

[Here is a list of bugs fixed in MaxScale 2.2.0.](https://jira.mariadb.org/issues/?jql=project%20%3D%20MXS%20AND%20issuetype%20%3D%20Bug%20AND%20status%20%3D%20Closed%20AND%20fixVersion%20%3D%202.2.0)

* [MXS-1450](https://jira.mariadb.org/browse/MXS-1450) Maxadmin commands with a leading space are silently ignored
* [MXS-1449](https://jira.mariadb.org/browse/MXS-1449) Database change not allowed
* [MXS-1405](https://jira.mariadb.org/browse/MXS-1405) Script launched by monitors should run synchronously
* [MXS-1397](https://jira.mariadb.org/browse/MXS-1397) ReadWriteSplit's master connection can time out if session only issues read-only queries
* [MXS-1359](https://jira.mariadb.org/browse/MXS-1359) qc\_sqlite crashes with a very large compound select
* [MXS-1351](https://jira.mariadb.org/browse/MXS-1351) Partially authenticated connections are put into the connection pool
* [MXS-1349](https://jira.mariadb.org/browse/MXS-1349) qc\_mysqlembedded accesses wrong preparable statement field
* [MXS-1346](https://jira.mariadb.org/browse/MXS-1346) Function blocking per column
* [MXS-1345](https://jira.mariadb.org/browse/MXS-1345) Empty function list is not allowed
* [MXS-1340](https://jira.mariadb.org/browse/MXS-1340) Report true table and not alias name
* [MXS-1339](https://jira.mariadb.org/browse/MXS-1339) QC should return a particular table/database just once
* [MXS-1334](https://jira.mariadb.org/browse/MXS-1334) Build on FreeBSD 11 looks for libdl - how can it be told not to?
* [MXS-1322](https://jira.mariadb.org/browse/MXS-1322) Flushing log should reopen not reopen and truncate.
* [MXS-1307](https://jira.mariadb.org/browse/MXS-1307) Add CTE tests
* [MXS-1265](https://jira.mariadb.org/browse/MXS-1265) strerror\_r calls result in compiler warnings
* [MXS-1262](https://jira.mariadb.org/browse/MXS-1262) Mantenance bit(s) should persist after maxscale restart
* [MXS-1221](https://jira.mariadb.org/browse/MXS-1221) Nagios plugin scripts does not process -S option properly
* [MXS-1214](https://jira.mariadb.org/browse/MXS-1214) Streaming Insert Filter gives errors
* [MXS-1203](https://jira.mariadb.org/browse/MXS-1203) Batch inserts through Maxscale with C/J stall
* [MXS-1198](https://jira.mariadb.org/browse/MXS-1198) Interface retry bind interval (of a listener) increases by ten seconds every time it fails (10,20,30,....) it should be a fixed interval (and maybe configurable)
* [MXS-1160](https://jira.mariadb.org/browse/MXS-1160) Load infile not working on Schemarouter
* [MXS-1146](https://jira.mariadb.org/browse/MXS-1146) JDBC connection dropping transaction when connecting to MaxScale directly
* [MXS-959](https://jira.mariadb.org/browse/MXS-959) KILL command on wrong connection ID

### Known Issues and Limitations

There are some limitations and known issues within this version of MaxScale.\
For more information, please refer to the [Limitations](../about-maxscale-22/mariadb-maxscale-22-limitations-and-known-issues-within-mariadb-maxscale.md) document.

### Packaging

RPM and Debian packages are provided for the Linux distributions supported\
by MariaDB Enterprise.

Packages can be downloaded [here](https://mariadb.com/resources/downloads).

### Source Code

The source code of MaxScale is tagged at GitHub with a tag, which is identical\
with the version of MaxScale. For instance, the tag of version X.Y.Z of MaxScale\
is X.Y.Z. Further, _master_ always refers to the latest released non-beta version.

The source code is available [here](https://github.com/mariadb-corporation/MaxScale).

<sub>_This page is licensed: CC BY-SA / Gnu FDL_</sub>

{% @marketo/form formId="4316" %}
