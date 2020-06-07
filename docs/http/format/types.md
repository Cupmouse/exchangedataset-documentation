# Types

Here we explain field types used in JSON formatting.

We use non-standard field type to distinguish fields for the later analyze.

In this article, we show the appropriate mapping from field types to standard JSON data types with the descriptions of what a value we should anticipate.

## Standard JSON Data Types

These are the data types supported by JSON:

- object
- string
- number
- boolean
- null
- array

## Type Mapping Table

| Type        | JSON Data Type | Predicted Value                                                                                                                                                                                            |
| ----------- | -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `pair`      | string         | Name of the pair                                                                                                                                                                                           |
| `price`     | number         | Price in floating point number                                                                                                                                                                             |
| `size`      | number         | Size of order in floating point number                                                                                                                                                                     |
| `guid`      | string         | GUID in string                                                                                                                                                                                             |
| `timestamp` | string         | Timestamp in UNIX time, but in nano second. <br /> Given `unixtime` as a UNIX time in second and nano second part as `nanosec`, this is calculated as follows: <br /> `unixtime * 1,000,000,000 + nanosec` |
| `duration`  | string         | Time duration in nano second                                                                                                                                                                               |
| `boolean`   | boolean        | Boolean value                                                                                                                                                                                              |
| `int`       | number         | Integer value                                                                                                                                                                                              |
| `float`     | number         | Floating point value                                                                                                                                                                                       |
| `string`    | string         | String                                                                                                                                                                                                     |

