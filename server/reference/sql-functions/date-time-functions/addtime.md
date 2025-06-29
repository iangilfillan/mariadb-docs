
# ADDTIME

## Syntax


```
ADDTIME(expr1,expr2)
```

## Description


`ADDTIME()` adds *expr2* to *expr1* and returns the result. *expr1* is a time
or datetime expression, and *expr2* is a time expression.


## Examples


```
SELECT ADDTIME('2007-12-31 23:59:59.999999', '1 1:1:1.000002');
+---------------------------------------------------------+
| ADDTIME('2007-12-31 23:59:59.999999', '1 1:1:1.000002') |
+---------------------------------------------------------+
| 2008-01-02 01:01:01.000001                              |
+---------------------------------------------------------+

SELECT ADDTIME('01:00:00.999999', '02:00:00.999998');
+-----------------------------------------------+
| ADDTIME('01:00:00.999999', '02:00:00.999998') |
+-----------------------------------------------+
| 03:00:01.999997                               |
+-----------------------------------------------+
```


<sub>_This page is licensed: GPLv2, originally from [fill\_help\_tables.sql](https://github.com/MariaDB/server/blob/main/scripts/fill_help_tables.sql)_</sub>


{% @marketo/form formId="4316" %}
