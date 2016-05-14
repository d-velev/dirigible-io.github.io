---
layout: api
title: Database
icon: fa-check
---

Database
===

Standard access to the registered relational data sources.

- Module: **api/database**
- Definition: https://github.com/dirigiblelabs/core_api/issues/9
- Source: https://github.com/dirigiblelabs/core_api/blob/master/core_api/ScriptingServices/api/database.js
- Status: **stable**

Basic Usage
---

```javascript
/* globals $ */
/* eslint-env node, dirigible */

var database = require('api/database');
var response = require('api/http/response');

var datasource = database.getDatasource(); // default
//var datasource = db.getNamedDatasource("name-of-the-datasource");

var connection = datasource.getConnection();
try {
    var statement = connection.prepareStatement("select * from DGB_FILES where FILE_PATH like ?");
    var i = 0;
    statement.setString(++i, "%");
    var resultSet = statement.executeQuery();
    while (resultSet.next()) {
        response.println("[path]: " + resultSet.getString("FILE_PATH"));
    }
    resultSet.close();
    statement.close();
} catch(e) {
    console.trace(e);
    response.println(e.message);
} finally {
    connection.close();
}

response.flush();
response.close();
```