# Source plugin : Kafka [Flink]

## Description

To consumer data from `Kafka` , the supported `Kafka version >= 0.10.0` .

## Options

| name                       | type   | required | default value |
| -------------------------- | ------ | -------- | ------------- |
| topics                     | string | yes      | -             |
| consumer.group.id          | string | yes      | -             |
| consumer.bootstrap.servers | string | yes      | -             |
| schema                     | string | yes      | -             |
| format.type                | string | yes      | -             |
| format.*                   | string | no       | -             |
| consumer.*                 | string | no       | -             |
| rowtime.field              | string | no       | -             |
| watermark                  | long   | no       | -             |
| offset.reset               | string | no       | -             |
| common-options             | string | no       | -             |

### topics [string]

Kafka topic name. If there are multiple topics, use `,` to split, for example: `"tpc1,tpc2"` .

### consumer.group.id [string]

Kafka consumer group id, used to distinguish different consumer groups.

### consumer.bootstrap.servers [string]

Kafka cluster address, separated by `,`

### format.type [string]

Currently supports three formats

- json

- csv

- avro

### format.* [string]

The `csv` format uses this parameter to set the separator and so on. For example, set the column delimiter to `\t` , `format.field-delimiter=\\t`

### schema [string]

- csv

    - The `schema` of `csv` is a string of `jsonArray` , such as `"[{\"field\":\"name\",\"type\":\"string\"},{\"field\":\"age\ ",\"type\":\"int\"}]"` .

- json

    - The `schema` parameter of `json` is to provide a `json string` of the original data, and the `schema` can be automatically generated, but the original data with the most complete content needs to be provided, otherwise the fields will be lost.

- avro

    - The `schema` parameter of `avro` is to provide a standard `avro schema JSON string` , such as `{\"name\":\"test\",\"type\":\"record\",\"fields\":[{ \"name\":\"name\",\"type\":\"string\"},{\"name\":\"age\",\"type\":\"long\"} ,{\"name\":\"addrs\",\"type\":{\"name\":\"addrs\",\"type\":\"record\",\"fields\" :[{\"name\":\"province\",\"type\":\"string\"},{\"name\":\"city\",\"type\":\"string \"}]}}]}`

    - To learn more about how the `Avro Schema JSON string` should be defined, please refer to: https://avro.apache.org/docs/current/spec.html

### consumer.* [string]

In addition to the above necessary parameters that must be specified by the `Kafka consumer` client, users can also specify multiple `consumer` client non-mandatory parameters, covering [all consumer parameters specified in the official Kafka document](https://kafka.apache.org/documentation.html#consumerconfigs).

The way to specify parameters is to add the prefix `consumer.` to the original parameter name. For example, the way to specify `ssl.key.password` is: `consumer.ssl.key.password = xxxx` . If these non-essential parameters are not specified, they will use the default values given in the official Kafka documentation.

### rowtime.field [string]

Set the field for generating `watermark`

### watermark [long]

Set the allowable delay for generating `watermark`

### offset.reset [string]

The consumer's initial `offset` is only valid for new consumers. There are three modes

- latest

    - Start consumption from the latest offset

- earliest

    - Start consumption from the earliest offset

- specific

    - Start consumption from the specified `offset` , and specify the `start offset` of each partition at this time. The setting method is through `offset.reset.specific="{0:111,1:123}"`

### common options [string]

Source plugin common parameters, please refer to [Source Plugin](./source-plugin.md) for details

## Examples

```bash
  KafkaTableStream {
    consumer.bootstrap.servers = "127.0.0.1:9092"
    consumer.group.id = "seatunnel5"
    topics = test
    result_table_name = test
    format.type = csv
    schema = "[{\"field\":\"name\",\"type\":\"string\"},{\"field\":\"age\",\"type\":\"int\"}]"
    format.field-delimiter = ";"
    format.allow-comments = "true"
    format.ignore-parse-errors = "true"
  }
```
