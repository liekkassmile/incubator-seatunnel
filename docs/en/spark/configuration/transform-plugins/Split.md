# Transform plugin : Split [Spark]

## Description

Split string according to `delimiter`

## Options

| name           | type   | required | default value |
| -------------- | ------ | -------- | ------------- |
| delimiter      | string | no       | " "(空格)       |
| fields         | array  | yes      | -             |
| source_field   | string | no       | raw_message   |
| target_field   | string | no       | *root*        |
| common-options | string | no       | -             |

### delimiter [string]

Separator, the input string is separated according to the separator. The default separator is a space `(" ")` .

### fields [list]

In the split field name list, specify the field names of each character string after splitting in order. If the length of the `fields` is greater than the length of the separation result, the extra fields are assigned null characters.

### source_field [string]

The source field of the string before being split, if not configured, the default is `raw_message`

### target_field [string]

`target_field` can specify the location where multiple split fields are added to the Event. If it is not configured, the default is `_root_` , that is, all split fields will be added to the top level of the Event. If a specific field is specified, the divided field will be added to the next level of this field.

### common options [string]

Transform plugin common parameters, please refer to [Transform Plugin](./transform-plugin.md) for details

## Examples

```bash
split {
    source_field = "message"
    delimiter = "&"
    fields = ["field1", "field2"]
}
```

> Split the `message` field in the source data according to `&`, you can use `field1` or `field2` as the key to get the corresponding value

```bash
split {
    source_field = "message"
    target_field = "info"
    delimiter = ","
    fields = ["field1", "field2"]
}
```

> Split the `message` field in the source data according to `,` , the split field is `info` , you can use `info.field1` or `info.field2` as the key to get the corresponding value
