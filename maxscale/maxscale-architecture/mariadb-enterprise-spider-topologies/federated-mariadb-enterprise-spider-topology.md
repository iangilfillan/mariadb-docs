# Federated MariaDB Enterprise Spider Topology

## Overview

In the Federated MariaDB Enterprise Spider topology, a Spider Node contains one or more "virtual" Spider Tables. A Spider Table does not store data. When a Spider Table is queried, the Enterprise Spider storage engine uses a MariaDB foreign data wrapper to read from and write to a Data Table on a Data Node.

## Benefits

MariaDB Enterprise Spider:

* Supports a MariaDB foreign data wrapper. The MariaDB foreign data wrapper can be used to replace the older Federated and FederatedX storage engines.
* Supports an ODBC foreign data wrapper in [MariaDB Enterprise Server 10.5](https://github.com/mariadb-corporation/docs-server/blob/test/en/mariadb-server-releases-mariadb-enterprise-server-10-5/README.md) and later. The ODBC foreign data wrapper is beta maturity. The maturity can be confirmed by querying the [information\_schema.SPIDER\_WRAPPER\_PROTOCOLS](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/information-schema-spider_wrapper_protocols-table) table.

The Spider Federated topology:

* Can be used to query tables located on a different MariaDB Enterprise Server node from the Spider Node using the MariaDB foreign data wrapper.
* Can be used to join tables located on a different MariaDB Enterprise Server node with tables on the Spider Node using the MariaDB foreign data wrapper.
* Can be used to migrate tables located on a different MariaDB Enterprise Server node to the Spider Node using the MariaDB foreign data wrapper.

## Federated MariaDB Enterprise Spider Topology

![spider-federated](https://github.com/mariadb-corporation/docs-server/blob/test/maxscale/.gitbook/assets/federated-mariadb-enterprise-spider-topology/+image/spider-federated.png)

In the Spider Federated topology, a Spider Node contains one or more "virtual" Spider Tables. A Spider Table does not store data. When a Spider Table is queried, the Enterprise Spider storage engine uses a MariaDB foreign data wrapper to read from and write to a Data Table on a Data Node.

The Spider Federated topology consists of:

* One MariaDB Enterprise Server node is a Spider Node
* One MariaDB Enterprise Server node is a Data Node

The Spider Node:

* Contains one or more Spider Tables
* Uses the [Enterprise Spider storage engine](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-storage-engine-introduction/) plugin for Spider Tables
* Uses a MariaDB foreign data wrapper to query the Data Table on the Data Node

The Data Node:

* Contains a Data Table for each Spider Table
* Uses a non-Spider storage engine for each Data Table, such as [InnoDB](https://github.com/mariadb-corporation/docs-server/blob/test/en/storage-engines-overview-innodb-storage-engine/README.md) or [ColumnStore](https://github.com/mariadb-corporation/docs-server/blob/test/en/columnstore-storage-engine/README.md)

## Term Definitions

| Term                | Definition                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Term                | Definition                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Data Node           | A Data Node is a MariaDB Enterprise Server node that contains one or more Data Tables.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Data Table          | A Data Table stores data for a Spider Table. When a Spider Table is queried, the Enterprise Spider storage engine uses the MariaDB foreign data wrapper to read from and write to the Data Table on a Data Node. The Data Table must be created on the Data Node with the same structure as the Spider Table. The Data Table must use a non-Spider storage engine, such as [InnoDB](https://github.com/mariadb-corporation/docs-server/blob/test/en/storage-engines-overview-innodb-storage-engine/README.md) or [ColumnStore](https://github.com/mariadb-corporation/docs-server/blob/test/en/columnstore-storage-engine/README.md). |
| ODBC Data Source    | An ODBC Data Source relies on an ODBC Driver and an ODBC Driver Manager to query an external data source.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ODBC Driver         | An ODBC Driver is a library that integrates with a ODBC Driver Manager to query an external data source.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ODBC Driver Manager | An ODBC Driver Manager allows applications to use ODBC Drivers.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Spider Node         | A Spider Node is a MariaDB Enterprise Server node that contains one or more Spider Tables.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Spider Table        | A Spider Table is a virtual table that does not store data. When a Spider Table is queried, the [Enterprise Spider storage engine](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-storage-engine-introduction/) uses foreign data wrappers to read from and write to Data Tables on Data Nodes or ODBC Data Sources.                                                                                                                                                                                                                                                                          |

## Example Use Cases

### Query MariaDB Enterprise Server Nodes

The Spider Federated topology can be used to query tables located on another MariaDB Enterprise Server node:

* The MariaDB Enterprise Server node with the desired table is configured as a Data Node.
* The MariaDB Enterprise Server node that needs to query the table is configured as a Spider Node.
* The Data Table is the desired table on the Data Node.
* A Spider Table is created on the Spider Node that references the Data Table on the Data Node.
* On the Spider Node, the Data Table is queried by querying the Spider Table like the following:

```
SELECT * FROM spider_tab;
```

* Non-Spider tables can also be referenced in queries with the Spider Table:

```
SELECT *
FROM spider_tab s
JOIN innodb_tab i
ON s.id=i.id;
```

### Migrate Tables from MariaDB Enterprise Server Nodes

The Spider Federated topology can be used to migrate tables from one MariaDB Enterprise Server node to another MariaDB Enterprise Server node:

* The MariaDB Enterprise Server node with the source table is configured as a Data Node.
* The MariaDB Enterprise Server node with the destination table is configured as a Spider Node.
* The Data Table is the source table on the Data Node.
* A Spider Table is created on the Spider Node that references the Data Table on the Data Node.
* On the Spider node, the Data Table's data is migrated to the destination table by querying the Spider Table like the following:

```
INSERT INTO innodb_tab
   SELECT * FROM spider_tab;
```

## Examples

### Load Spider with Configuration File (ES 10.4+)

```
[mariadb]
...
plugin_load_add = "ha_spider"
```

### Load Spider with INSTALL SONAME (ES 10.4+)

```
INSTALL SONAME "ha_spider";
```

### View Foreign Data Wrappers (ES 10.5+)

```
SELECT * FROM information_schema.SPIDER_WRAPPER_PROTOCOLS;
```

### Create Federated Spider Table

```
CREATE SERVER hq_server
FOREIGN DATA WRAPPER mariadb
OPTIONS (
   HOST "192.0.2.2",
   PORT 5801,
   USER "spider_user",
   PASSWORD "password",
   DATABASE "hq_sales"
);

CREATE DATABASE spider_hq_sales;

CREATE TABLE spider_hq_sales.invoices (
   branch_id INT NOT NULL,
   invoice_id INT NOT NULL,
   customer_id INT,
   invoice_date DATETIME(6),
   invoice_total DECIMAL(13, 2),
   payment_method ENUM('NONE', 'CASH', 'WIRE_TRANSFER', 'CREDIT_CARD', 'GIFT_CARD'),
   PRIMARY KEY(branch_id, invoice_id)
) ENGINE=Spider
COMMENT='server "hq_server", table "invoices"';
```

## Resources

### Deployment

* [Deploy MariaDB Enterprise Spider](https://app.gitbook.com/s/aEnK0ZXmUbJzqQrTjFyb/mariadb-enterprise-server-release-notes/mariadb-enterprise-server-differences/deployment#spider-topologies)

### Operations

* [Operations](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-storage-engine-introduction/mariadb-enterprise-spider-operations/federated-mariadb-enterprise-spider-topology-operations/)
* [Backup and Restore](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-storage-engine-introduction/mariadb-enterprise-spider-operations/federated-mariadb-enterprise-spider-topology-operations/federated-mariadb-enterprise-spider-topology-backup-and-restore)
* [Migrate Tables](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-storage-engine-introduction/mariadb-enterprise-spider-operations/federated-mariadb-enterprise-spider-topology-operations/federated-mariadb-enterprise-spider-topology-migrate-tables)

### Schema Design

* [Schema Design](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-storage-engine-introduction/mariadb-enterprise-spider-schema-design)

### Storage Engines

* [Enterprise Spider Storage Engine](https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/reference/storage-engines/spider/spider-storage-engine-introduction/)

<sub>_This page is: Copyright © 2025 MariaDB. All rights reserved._</sub>

{% @marketo/form formId="4316" %}
