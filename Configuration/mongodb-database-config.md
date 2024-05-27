---
title: MongoDB Database Configuration
label: MongoDB Database Config
order: 2;
---

For MongoDB, you do not need to create a `DbContext`. Instead, you can configure your connection settings directly in the `appsettings.json` file by adding the MongoSettings section:

```json #
{
  "MongoSettings": {
    "DatabaseName": "YourDatabase",
    "ConnectionString": "mongodb://localhost:27017"
  },
}
```

This configuration is all you need to connect to your MongoDB database. Adjust the DatabaseName and ConnectionString as necessary to match your MongoDB setup.