# TIMESTAMP FUNCTION

This page is about the TIMESTAMP function. For the timestamp data type, see [TIMESTAMP](../../data-types/date-and-time-data-types/timestamp.md).

## Syntax

```
TIMESTAMP(expr), TIMESTAMP(expr1,expr2)
```

## Description

With a single argument, this function returns the date or datetime\
expression `expr` as a datetime value. With two arguments, it adds the\
time expression `expr2` to the date or datetime expression `expr1` and\
returns the result as a datetime value.

## Examples

```
SELECT TIMESTAMP('2003-12-31');
+-------------------------+
| TIMESTAMP('2003-12-31') |
+-------------------------+
| 2003-12-31 00:00:00     |
+-------------------------+

SELECT TIMESTAMP('2003-12-31 12:00:00','6:30:00');
+--------------------------------------------+
| TIMESTAMP('2003-12-31 12:00:00','6:30:00') |
+--------------------------------------------+
| 2003-12-31 18:30:00                        |
+--------------------------------------------+
```

<sub>_This page is licensed: GPLv2, originally from [fill\_help\_tables.sql](https://github.com/MariaDB/server/blob/main/scripts/fill_help_tables.sql)_</sub>

{% @marketo/form formId="4316" %}
