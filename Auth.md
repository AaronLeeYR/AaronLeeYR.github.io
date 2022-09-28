## My 1st Repo
Pushing from Visual Studio to Github


Visual Studio command flow:
git config --global user.name "Aaron Lee"
git config --global user.email aaronlyr@gmail.com
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/AaronLeeYR/visualstudio.git
git push origin main


Node js command flow:
npm init
npm install mysql express dotenv cors express-openid-connect
    (will see node_modules, package-lock.json,package.json files added)
add a (.gitignore) folder
include (node_modules) file in (.gitignore) file
press 'ctrl c' to stop server from running
To export modules, use cmd (module.export)
To import module in main.js...use cmd(let api = require("./modulename"); ) OR(let { router } = require("./modulename"); )


AUTH0 env command:
//create a auth0 web app account and copy the information into here
//then create a (.env) file so that it can link to authdemo.js

# MySQL database environment variables
DBHOST=YourMySQLServerURLhere
DBUSER=YourUsernameHere
DBPASSWD=YourPasswordHere
DBPORT=YourPortNumberHere
DBNAME=YourDatabaseNameHere
# authentication (Auth0) environment variables
ISSUER_BASE_URL=https://YOUR_DOMAIN     # DOMAIN listed in your Auth0's application
CLIENT_ID=YOUR_CLIENT_ID                # CLIENT_ID listed in your Auth0's application
BASE_URL=https://YOUR_APPLICATION_ROOT_URL  # Where your application starts (default is http://localhost:3000)
SECRET=LONG_RANDOM_VALUE                # Any random 32-character string you want to type
# port number for express to listen on
PORT=Port_Number

AUTH0 demo.js:
// demonstration of using Auth0 to login users before allowing access to endpoints
// to step through this, see James Quick's video tutorial at https://www.youtube.com/watch?v=QQwo4E_B0y8

const express = require('express');
const data = require("./data");
const app = express();
require('dotenv').config();

const { auth, requiresAuth } = require('express-openid-connect');
app.use(
  auth({
    authRequired: false,
    auth0Logout: true,
    issuerBaseURL: process.env.ISSUER_BASE_URL,
    baseURL: process.env.BASE_URL,
    clientID: process.env.CLIENT_ID,
    secret: process.env.SECRET,
    idpLogout: true,
  })
);

// req.isAuthenticated is provided from the auth router
app.get('/', (request, response) => {
  response.send(request.oidc.isAuthenticated() ? 'Logged in' : 'Logged out')
});

app.get('/profile', requiresAuth(), (request, response) => {
    response.send(JSON.stringify(request.oidc.user));
});

app.get('/user/by-uid', requiresAuth(), (request, response) => {
    let user = data.get_user_by_user_id(request.query.user_id);
    response.status(200).send(user);
  });

const port = process.env.PORT || 3000;
app.listen(port, () => {
    console.log(`Listening on port ${port}`);
});
Auth0 dataset:

//sample data set for autho

let users = [
    {
      first_name: "Dena",
      last_name: "Charle",
      email: "dcharle0@indiegogo.com",
      user_id: 1,
      phone: "98765433",
      plan_id: 1,
      signup_date: "2021-01-01T00:00:00.000Z",
    },
    {
      first_name: "Dynah",
      last_name: "Waiting",
      email: "dwaiting1@google.com.br",
      user_id: 2,
      phone: "98765434",
      plan_id: 1,
      signup_date: "2021-01-01T00:00:00.000Z",
    },
    {
      first_name: "Marc",
      last_name: "Conibeer",
      email: "mconibeer2@desdev.cn",
      user_id: 3,
      phone: "98765555",
      plan_id: 1,
      signup_date: "2021-01-01T00:00:00.000Z",
    },
  ];
  
  function get_all_users() {
    return users;
  }
  function get_user_by_user_id(user_id) {
    for (i = 0; i < users.length; i++) {
      if (users[i].user_id == user_id) {
        return users[i];
      }
    }
  }
  
  function add_user(user) {
    users.push(user);
  }
  
  module.exports = {
    add_user,
    get_all_users,
    get_user_by_user_id,
  };
  


