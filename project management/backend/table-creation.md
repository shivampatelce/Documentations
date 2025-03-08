# Table creation

Let's consider we want to create table for all projects.

## Create table from admin side

```json
{
  "tableName": "Projects",
  "columns": {
    "Project Name": {
      "type": "String",
      "isSortable": true
    },
    "Project Description": {
      "type": "String",
      "isSortable": false
    }
  }
}
```

While creating table we will store table's meta data in TableMetaData table and then create actual table for table.

#### what if table has a relation with other table. here consider each projects has a list of tasks.

```json
{
  "tableName": "Projects",
  "columns": {
    "Project Name": {
      "type": "String",
      "isSortable": true
    },
    "Project Description": {
      "type": "String",
      "isSortable": false
    }
  },
  "ref": [
    {
      "tableName": "Tasks" // or tableId: "1234567"
    }
  ]
}
```

```json
{
  "tableName": "Tasks",
  "columns": {
    "Title": {
      "type": "String",
      "isSortable": true
    },
    "Description": {
      "type": "String",
      "isSortable": false
    }
  }
}
```

#### Cases need to be handled

1. While defining relationship between table need to check is it possible or not

## Edit table

```json
{
  "tableName": "Projects",
  "columns": {
    "Project Name": {
      "type": "String",
      "isSortable": true
    },
    "Project Description": {
      "type": "String",
      "isSortable": true
    }
  }
}
```

#### Cases need to be handled

1. Check the case is type changing is possible.

## Delete table

```json
{
  "tableId": 1
}
```

#### Cases need to be handled

1. Check table's relationship with other table
