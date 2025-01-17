---
title: Miscellaneous SQL functions
list_title: Miscellaneous functions
description: >
  Use miscellaneous SQL functions to perform a variety of operations in SQL queries.
menu:
  influxdb_cloud_iox:
    name: Miscellaneous
    parent: sql-functions
weight: 310
---

The InfluxDB SQL implementation supports the following miscellaneous functions
for performing a variety of operations:

- [arrow_cast](#arrow_cast)
- [arrow_typeof](#arrow_typeof)
<!-- - [struct](#struct) -->

### `arrow_cast`

Casts a value to a specific Arrow data type.

```sql
arrow_cast(expression, datatype)
```

#### Arguments

- **expression**: Expression to cast.
  Can be a constant, column, or function, and any combination of arithmetic or
  string operators.
- **datatype**: [Arrow data type](https://arrow.apache.org/datafusion/user-guide/sql/data_types.html)
  to cast to.

{{< expand-wrapper >}}
{{% expand "View `arrow_cast` query example" %}}

_The following example uses the sample data set provided in
[Get started with InfluxDB tutorial](/influxdb/cloud-iox/get-started/write/#construct-line-protocol)._

```sql
SELECT
  arrow_cast(time, 'Int64') AS time,
  arrow_cast(temp, 'Utf8') AS temp,
  arrow_cast(co, 'Float64')AS co
FROM home
LIMIT 1
```

| time                | temp |  co |
| :------------------ | ---: | --: |
| 1641024000000000000 | 21.0 |   0 |

{{% /expand %}}
{{< /expand-wrapper >}}

## arrow_typeof

Returns the underlying [Arrow data type](https://arrow.apache.org/datafusion/user-guide/sql/data_types.html)
of the the expression:

```sql
arrow_typeof(expression)
```

##### Arguments

- **expression**: Expression to evaluate.
  Can be a constant, column, or function, and any combination of arithmetic or
  string operators.

{{< expand-wrapper >}}
{{% expand "View `arrow_typeof` query example" %}}

_The following example uses the sample data set provided in
[Get started with InfluxDB tutorial](/influxdb/cloud-iox/get-started/write/#construct-line-protocol)._

```sql
SELECT
  arrow_typeof(time) AS time,
  arrow_typeof(room) AS room,
  arrow_typeof(temp) AS temp,
  arrow_typeof(co) AS co
FROM home
LIMIT 1
```

| time                        | room                    | temp    | co    |
| :-------------------------- | :---------------------- | :------ | :---- |
| Timestamp(Nanosecond, None) | Dictionary(Int32, Utf8) | Float64 | Int64 |

{{% /expand %}}
{{< /expand-wrapper >}}

<!--
## struct

Returns an Arrow struct using the specified input expressions.
Fields in the returned struct use the `cN` naming convention.
For example: `c0`, `c1`, `c2`, etc.

```sql
struct(expression1[, ..., expression_n])
```

##### Arguments

- **expression_n**: Expression to include in the output struct.
  Can be a constant, column, or function, and any combination of arithmetic or
  string operators.

{{< expand-wrapper >}}
{{% expand "View `struct` example" %}}

```sql
struct('A', 'B', 3, 4)
-- Returns {c0: A, c1: B, c3: 3, c4: 4}
```
{{% /expand %}}
{{< /expand-wrapper >}}
-->
