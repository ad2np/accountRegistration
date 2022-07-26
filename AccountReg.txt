const express = require("express");
const app = express();
const bodyParser = require("body-parser");
const { SocketAddress } = require("net");
const encoder = bodyParser.urlencoded();
const MongoClient=require("mongodb").MongoClient;

var url="mongodb://localhost:27017/";
app.get("/",function(req,res){res.sendFile(__dirname + "/AccountRegistration.html")});

MongoClient.connect(url,function(err,db){
if(err) throw err;
console.log("Server Started");

var db= db.db("userDBMongo");

app.post("/",encoder, function(req,res){ 
    var fullname = req.body.Fname;
    var email = req.body.Email;
    var password = req.body.Pass;
    var data = {Fname:fullname, Email:email, Pass:password}

db.collection("Accounts").insertOne(data, function (err,result){if(err) throw err;
console.log ("Successfully Inserted Data on the Database")})

})
})
app.listen(4000)