[![Build](https://img.shields.io/travis/sapbuild/node-sap-mongo.svg?style=flat-square)](http://travis-ci.org/sapbuild/node-sap-mongo)
[![Version](https://img.shields.io/npm/v/node-sap-mongo.svg?style=flat-square)](https://npmjs.org/package/node-sap-mongo)
[![Dependency Status](https://david-dm.org/sapbuild/node-sap-mongo.svg)](https://david-dm.org/sapbuild/node-sap-mongo)
[![devDependency Status](https://david-dm.org/sapbuild/node-sap-mongo/dev-status.svg)](https://david-dm.org/sapbuild/node-sap-mongo#info=devDependencies)
[![Coverage](https://img.shields.io/coveralls/sapbuild/node-sap-mongo/master.svg?style=flat-square)](https://coveralls.io/r/sapbuild/node-sap-mongo?branch=master)
node-sap-mongo
==============

MongoDB connectivity layer

##Using the Common MongoDB Connection

###Initializing the connection 
This must be done once by the main server process. This is done by the Norman AppServer, you may do this manually in your service tests. 

```javascript
commonServer.db.connection.initialize({ database: "norman-test" }, function (err)  {
  if (err) {
    console.error("Oops, no magic today!");
  }
});
```

Optional second parameter allows configuring the deployment strategy. Default strategy "single" stores all Norman collection into a single database. Production strategy "distribute" spreads the collections over multiple domain databases to reduce write contention. Database distribution may be fine-tuned with the "map" strategy. 

###Getting a mongoose connection
The following code snippet returns a connection to the database configured for the module "my-module" according to the deployment strategy. 

```javascript
var connection = commonserver.db.connection.getMongooseConnection("my-module");
```

###Getting a Mongo database connection
```javascript
var db1 = commonserver.db.connection.getDb("my-module");
var db2 = commonserver.db.connection.getMongooseConnection("my-other-module").db;
```


###Creating mongoose models
We offer a simple way to define mongoose model on a specific connection :

```javascript
var commonServer = require('norman-common-server'),
    mongoose = commonServer.db.mongoose;

var MySchema = mongoose.createSchema('my-module', { ... });


module.exports = mongoose.createModel('MyModel', MySchema);

```


# BUILD on GitHub

[Click here](https://github.com/SAP/BUILD) to visit the central BUILD project on GitHub, where you can find out more!

[Click here](https://github.com/SAP/BUILD/blob/master/Contributing.md) to view the BUILD Contribution Guidelines. 

