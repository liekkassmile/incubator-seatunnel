# Source plugin: InfluxDB

## Description

Read data from InfluxDB.

## Options

| name        | type           | required | default value |
| ----------- | -------------- | -------- | ------------- |
| server_url  | `String`       | yes      | -             |
| username    | `String`       | no       | -             |
| password    | `String`       | no       | -             |
| database    | `String`       | yes      | -             |
| measurement | `String`       | yes      | -             |
| fields      | `List<String>` | yes      | -             |
| field_types | `List<String>` | yes      | -             |

### server_url [`String`]

The URL of InfluxDB Server.

### username [`String`]

The username of InfluxDB Server.

### password [`String`]

The password of InfluxDB Server.

### datasource [`String`]

The DataSource name in InfluxDB.

### measurement [`String`]

The Measurement name in InfluxDB.

### fields [`List<String>`]

The list of Field in InfluxDB.

### field_types [`List<String>`]

The list of Field Types in InfluxDB.

## Example

### Simple

```hocon
InfluxDbSource {
  server_url = "http://127.0.0.1:8086/"
  database = "influxdb"
  measurement = "m"
  fields = ["time", "temperature"]
  field_types = ["STRING", "DOUBLE"]
}
```

### Auth

```hocon
InfluxDbSource {
  server_url = "http://127.0.0.1:8086/"
  username = "admin"
  password = "password"
  database = "influxdb"
  measurement = "m"
  fields = ["time", "temperature"]
  field_types = ["STRING", "DOUBLE"]
}
```
