# SQL Data Types

In SQL, data types define the type of data that can be stored. Each column in a table must have a data type, which determines the kind of data that can be stored in that column. Below are some of the common data types used in SQL:

| Data Type | Description | Size | Range (Signed) | Range (Unsigned) |
|-----------|-------------|------------| ---- | ---- |
| `TINYINT` | Very small integer numbers | 1 byte | -128 to 127 | 0 to 255 |
| `SMALLINT` | Small integer numbers | 2 bytes | -32,768 to 32,767 | 0 to 65,535 |
| `INT` | Integer numbers | 4 bytes | -2,147,483,648 to 2,147,483,647 | 0 to 4,294,967,295 |
| `BIGINT` | Large integer numbers | 8 bytes | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | 0 to 18,446,744,073,709,551,615 |
| `NUMERIC(p, s)` | Exact numeric values with precision `p` and scale `s` | Variable | -10^38 +1 to 10^38 -1 | 0 to 10^38 -1 |
| `DECIMAL(p, s)` | Exact numeric values with precision `p` and scale `s`; implementation may use higher precision than specified | Variable | -10^38 +1 to 10^38 -1 | 0 to 10^38 -1 |
| `FLOAT(p)` | Approximate numeric values with precision `p` | 4 bytes | -3.402823466E+38 to 3.402823466E+38 | 0 to 3.402823466E+38 |
| `REAL` | Approximate numeric values with single precision | 4 bytes | -3.402823466E+38 to 3.402823466E+38 | 0 to 3.402823466E+38 |
| `DOUBLE PRECISION` | Approximate numeric values with double precision | 8 bytes | -1.7976931348623157E+308 to 1.7976931348623157E+308 | 0 to 1.7976931348623157E+308 |
| `CHAR(n)` | Fixed-length character string | n bytes | 0 to 255 characters | 0 to 255 characters |
| `VARCHAR(n)` | Variable-length character string | Up to n bytes | 0 to 65,535 characters | 0 to 65,535 characters |
| `TEXT` | Variable-length character string for large text data | Variable | 0 to 65,535 bytes (MySQL); 0 to 2^31-1 bytes (SQL Server) | 0 to 65,535 bytes (MySQL); 0 to 2^31-1 bytes (SQL Server) |
| `NCHAR(n)` | Fixed-length Unicode character string | 2n bytes | 0 to 4000 characters | 0 to 4000 characters |
| `NVARCHAR(n)` | Variable-length Unicode character string | 2n bytes + 2 bytes for length | 0 to 4000 characters | 0 to 4000 characters |
| `DATE` | Date values | 3 bytes | January 1, 0001 to December 31, 9999 | January 1, 0001 to December 31, 9999 |
| `TIME` | Time values or durations | 3 bytes | -838:59:59 to 838:59:59 | 00:00:00 to 838:59:59 |
| `DATETIME` | Date and time values | 8 bytes | January 1, 1753 to December 31, 9999 | January 1, 1753 to December 31, 9999 |
| `TIMESTAMP` | Date and time values, automatically tracks changes | 4 bytes | January 1, 1970 to January 19, 2038 | January 1, 1970 to January 19, 2038 |
| `YEAR` | Year values | 1 byte | 1901 to 2155 | 1901 to 2155 |
| `BOOLEAN` | Boolean values (true/false) | 1 byte | N/A | N/A |
| `BINARY(n)` | Fixed-length binary data | n bytes | 0 to 255 bytes | 0 to 255 bytes |
| `VARBINARY(n)` | Variable-length binary data | Up to n bytes | 0 to 65,535 bytes | 0 to 65,535 bytes |
