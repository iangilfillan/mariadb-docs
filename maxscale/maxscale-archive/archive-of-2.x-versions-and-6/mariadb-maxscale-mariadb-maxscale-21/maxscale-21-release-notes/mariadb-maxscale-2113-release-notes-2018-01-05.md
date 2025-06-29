# MariaDB MaxScale 2.1.13 Release Notes -- 2018-01-05

##

## MariaDB MaxScale 2.1.13 Release Notes -- 2018-01-05

Release 2.1.13 is a GA release.

This document describes the changes in release 2.1.13, when compared\
to release [2.1.12](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/).

If you are upgrading from release 2.0, please also read the following\
release notes:

* [2.1.12](https://mariadb.com/kb/en/node:mariadb-maxscale-2112-release-notes-2017-12-14)
* [2.1.11](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [2.1.10](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [2.1.9](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [2.1.8](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [2.1.7](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [2.1.6](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [2.1.5](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [2.1.4](mariadb-maxscale-21-mariadb-maxscale-214-release-notes-2017-07-03.md)
* [2.1.3](../../../archive-of-2x.xx-versions/mariadb-maxscale-21-06/)
* [2.1.2](mariadb-maxscale-21-mariadb-maxscale-212-release-notes-2017-04-03.md)
* [2.1.1](mariadb-maxscale-21-mariadb-maxscale-211-release-notes-2017-03-14.md)
* [2.1.0](mariadb-maxscale-21-mariadb-maxscale-210-release-notes-2017-02-16.md)

For any problems you encounter, please consider submitting a bug report at[Jira](https://jira.mariadb.org).

### Bug fixes

[Here is a list of bugs fixed in MaxScale 2.1.13.](https://jira.mariadb.org/issues/?jql=project%20%3D%20MXS%20AND%20issuetype%20%3D%20Bug%20AND%20status%20%3D%20Closed%20AND%20fixVersion%20%3D%202.1.13)

* [MXS-1585](https://jira.mariadb.org/browse/MXS-1585) Crash in MaxScale 2.1.12
* [MXS-1582](https://jira.mariadb.org/browse/MXS-1582) Maxscale leaving socket behind after shutdown
* [MXS-1581](https://jira.mariadb.org/browse/MXS-1581) CREATE TABLE AS not supported
* [MXS-1580](https://jira.mariadb.org/browse/MXS-1580) Invalid handling of BIT values
* [MXS-1527](https://jira.mariadb.org/browse/MXS-1527) SELECT with session var is not supported
* [MXS-1516](https://jira.mariadb.org/browse/MXS-1516) existing connection don't change routing even if master switched

### Packaging

RPM and Debian packages are provided for the Linux distributions supported by\
MariaDB Enterprise.

Packages can be downloaded [here](https://mariadb.com/resources/downloads).

### Source Code

The source code of MaxScale is tagged at GitHub with a tag, which is identical\
with the version of MaxScale. For instance, the tag of version X.Y.Z of MaxScale\
is maxscale-X.Y.Z.

The source code is available [here](https://github.com/mariadb-corporation/MaxScale).

<sub>_This page is licensed: CC BY-SA / Gnu FDL_</sub>

{% @marketo/form formId="4316" %}
