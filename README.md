Driver nodeJs for liteDB

(litedb for store json objects to disk.it's a little db. support query like moongodb,support crud,stored,trigger,total)

Installation
 
$ npm install --save litedb
 
connect
 
var db = require('liteDB');
db.connect('./db',["persone"]);
db.connect(['accounts']);
 
 
trigger
 
//create trigger
 
db.util.trigger("beforeUserSave", function(user) {
    user.age = 38;
    user.mail = "bona shen@gmail.com";
});
 
//assemble trigger for db.users
 
db.beforeUserSave.assemble(db.users, "beforeSaveTrigger");
 
//drop trigger
db.beforeUserSave.drop();
 
listen event
 
db.events.on("collection/onSave", function(evt) {
    console.log("collection/onSave");
});
 
save json
 
db.users.save({
    name: "bona shen",
    comments: ["peter's Father", "kerry's father"]
});
 
db.users.save({
    name: "ychunx",
    comments: ["", "kerry's mather",""],
    age:35
});
 
query
 
db.users.find({
    age: {
        $gt: 30
    }
}).forEach(function(o) {
    console.log(o);
});
 
console.log("find:", db.users.find({
    comments: /mather/
}));
 
