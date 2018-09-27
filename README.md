The module store the data using JavaScript Object directly into a JSON file. You can easily traverse the data to reach directly the interesting property using the DataPath. The principle of DataPath is the same as XMLPath.

var JsonDB = require('node-json-db');
// The second argument is used to tell the DB to save after each push
// If you put false, you'll have to call the save() method.
// The third argument is to ask JsonDB to save the database in an human readable format. (default false)
var db = new JsonDB("myDataBase", true, false);
 
// Pushing the data into the database
// With the wanted DataPath
// By default the push will override the old value
db.push("/test1","super test");
 
// It also create automatically the hierarchy when pushing new data for a DataPath that doesn't exists
db.push("/test2/my/test",5);
 
// You can also push directly objects
db.push("/test3", {test:"test", json: {test:["test"]}});

// Get the data from the root
var data = db.getData("/");
 
// From a particular DataPath
var data = db.getData("/test1");
console.log(data);
// If you try to get some data from a DataPath that doesn't exists
// You'll get an Error
//try {
//    var data = db.getData("/test1/test/dont/work");
//} catch(error) {
    // The error will tell you where the DataPath stopped. In this case test1
    // Since /test1/test does't exist.
//    console.error(error);
//};
 
// Deleting data
db.delete("/test1");
 
// Save the data (useful if you disable the saveOnPush)
db.save();
 
// In case you have a exterior change to the databse file and want to reload it
// use this method
db.reload();
