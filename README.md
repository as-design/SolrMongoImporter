# Solr Mongo Importer
Welcome to the Solr Mongo Importer project. This project provides MongoDb support for the Solr Data Import Handler.

## Features
* Retrive data from a MongoDb collection
* Authenticate using MongoDb authentication
* Map Mongo fields to Solr fields

## Classes

* MongoDataSource - Provides a MongoDb datasource
    * database (required) - The name of the data base you want to connect to
    * host (optional - default: localhost)
    * port (optional - default: 27017)
    * username (optional)
    * password (optional)
* MongoEntityProcessor - Use with the MongoDataSource to query a MongoDb collection
    * collection (required)
    * query (required)
* MongoMapperTransformer - Map MongoDb fields to your Solr schema
    * mongoField (required)

## Installation
1. Firstly you will need a copy of the Solr Mongo Importer jar.
    1. You can either download a copy here
     james75/SolrMongoImporter
    2. Build your own using the ant build script.
2. You will also need the Mongo Java driver, you can get this from:
   mongodb/mongo-java-driver
3. Place both of these jar's in your Solr libaries folder ( I put mine in 'dist' folder with the other jar's)
4. Add lib directives to your solrconfig.xml
```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <lib path="../../dist/solr-mongo-importer.jar" />
    <lib path="../../dist/mongo.jar" />
```

##Usage
Here is a sample data-config.xml showing the use of all components
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<dataConfig>
     <dataSource name="MyMongo" type="MongoDataSource" database="Inventory" />
     <document name="Products">
         <entity processor="MongoEntityProcessor"
                 query="{'Active':1}"
                 collection="ProductData"
                 datasource="MyMongo"
                 transformer="MongoMapperTransformer" >
             <field column="title"           name="title"       mongoField="Title"/>
             <field column="description"     name="description" mongoField="Long Description"/>
             <field column="brand"           name="brand"  />
         </entity>
     </document>
 </dataConfig>
```
