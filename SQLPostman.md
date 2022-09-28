// this is the example in class for linking modules to server in postman

let express = require("express");

// need to point to the correct file!
let { router } = require("./router2");
// or you can use let api = require("./router");

let application = express();
application.use(express.json());
application.use(router);

//transfered to router.js
//let router = express.Router();
//router.get("/", (request, response) => {
//  response.status(200).send("Hello there! Welcome to our server!");
//});

application.use(router);

application.listen(3000, (errors) => {
  if (errors) {
    console.log(errors);
  } else {
    console.log("Server running at port 3000");
  }
});




DATABASE.js ( to set up connection with MySql database to server)
// connecting to Mysql database

const mysql = require("mysql");

let connection = mysql.createConnection({
  host: "34.142.130.96",
  port: 3306,
  user: "root",
  password: "fintechsg",
  database: "nus_money",
});

connection.connect((errors) => {
  if (errors) {
    console.log(errors);
  } else {
    console.log("Connected to MySQL server!");
  }
});

module.exports = { connection };

router.js (this is to talk to router and connect to server)
// this is to link router with env and mysql database

// Import express module so that we can define router object
//let express = require("express");

// define APIs using the router object
//let router = express.Router();

const express = require("express");
const { connection } = require("./database2");

let router = express.Router();

// to pull information from connected sql database
router.get("/user/all", (request, response) => {
  connection.query("select * from user", (errors, results) => {
    response.status(200).send(results); //Convert Mysql results to API response
  });
});

router.get("/user/by-uid", (request, response) => {
  // the value for user_id will come from the request
  let uid = request.query.uid;
  connection.query(
    `select * from user where user_id = ${uid}`,
    (errors, results) => {
      response.status(200).send(results);
    }
  );
});

router.post("/user/add", (request, response) => {
  connection.query(
    `insert into 
    user (first_name, last_name, email, phone, plan_id) 
    values (
      '${request.body.first_name}', 
      '${request.body.last_name}', 
      '${request.body.email}', 
      '${request.body.phone}',
      '${request.body.plan_id}')`,
    (errors, results) => {
      if (errors) {
        console.log(errors);
        response.status(500).send("Some error occurred...");
      } else {
        response.status(200).send("Added a new user!");
      }
    }
  );
});

module.exports = { router };

