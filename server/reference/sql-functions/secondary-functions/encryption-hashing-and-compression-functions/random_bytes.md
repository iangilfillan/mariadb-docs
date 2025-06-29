# RANDOM\_BYTES

**MariaDB starting with** [**10.10.0**](https://app.gitbook.com/s/aEnK0ZXmUbJzqQrTjFyb/mariadb-community-server-release-notes/old-releases/release-notes-mariadb-10-10-series/mariadb-10100-release-notes)

The RANDOM\_BYTES function generates a binary string of random bytes. It was added in [MariaDB 10.10.0](https://app.gitbook.com/s/aEnK0ZXmUbJzqQrTjFyb/mariadb-community-server-release-notes/old-releases/release-notes-mariadb-10-10-series/mariadb-10100-release-notes).

## Syntax

```
RANDOM_BYTES(length)
```

## Description

Given a _length_ from 1 to 1024, generates a binary string of _length_ consisting of random bytes generated by the SSL library's random number generator.

See the RAND\_bytes() function documentation of your SSL library for information on the random number generator. In the case of [OpenSSL](https://www.openssl.org/docs/man1.1.1/man3/RAND_bytes.html), a cryptographically secure pseudo random generator (CSPRNG) is used.

Statements containing the RANDOM\_BYTES function are [unsafe for statement-based replication](../../../../ha-and-performance/standard-replication/unsafe-statements-for-statement-based-replication.md).

An error occurs if _length_ is outside the range 1 to 1024.

<sub>_This page is licensed: CC BY-SA / Gnu FDL_</sub>

{% @marketo/form formId="4316" %}
