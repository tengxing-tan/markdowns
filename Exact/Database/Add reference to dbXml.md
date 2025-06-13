**Add reference to `db.xml`**
This make sure the tables are created by db updater.
```xml
In db.xml
<sqlscript name="TableName">

In TableName.xml
<xmldata name="" simpletable="true">TrainingCategories</xmldata>
```

 