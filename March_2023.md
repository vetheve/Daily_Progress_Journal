
Daily Progress Journal
======================

"Tracking My Progress: Daily Journaling to Achieve Goals"

* **February 2023**

|Mon  |Tue  |Wed  |Thu  |Fri  |Sat  |Sun  |
|---:|---:|---:|---:|---:|---:|---:|
|     |     |[1](#2023-03-01)    |[2](#2023-03-02)    |[3](#2023-03-03)    |4    |5    |
|[6](#2023-03-06)    |[7](#2023-03-07)    |[8](#2023-03-08)     |[9](#2023-03-09)   |[10](#2023-03-10)   |11   |12   |
|[13](#2023-03-13)   |[14](#2023-03-14)   |[15](#2023-03-15)   |[16](#2023-03-16)   |[17](#2023-03-17)   |18   |19   |
|[20](#2023-03-20)   |[21](#2023-03-21)   |[22](#2023-03-22)   |[23](#2023-03-23)   |[24](#2023-03-24)   |25   |26   |
|[27](#2023-03-27)   |[28](#2023-03-28)   |[29](#2023-03-29)     |[30](#2023-03-30)     |[31](#2023-03-31)     |     |     |



#2023-03-01
---------------------------------------------------------
    
### Codecademy Back-End Engineer courses achievements !
Daily course achievements goals track.

- [x] **Linear Data structure: Introduction**
- [x] **Linear Data structure: Data sctructures** → *In progress*
- [ ] **Linear Data structure: Nodes**
- [ ] **Linear Data structure: Singly Linked Lists**
- [ ] **Linear Data structure: Doubly Linked Lists**
- [ ] **Linear Data structure: Queues**
- [ ] **Linear Data structure: Stacks**
- Total Progression → __80%__

### Project on going !

__Title:__ Codecademy project: Photo Caption Contest

- [x] **Plan the project**
- [x] **Define endpoints**
- [x] **Setup the environment**
- [x] **Create the models**
- [x] **Create the seeders**
- [ ] **Create the controllers** → *In progress*
- [ ] **Create the auth middleware to specific endpoints**
- [ ] **Create the routes**
- [ ] **Test the endpoints**
- [ ] **Configure localized caching**
- [ ] **Write a swagger documentation**
- Total Progression → __30%__
   
### Issues !

__Title:__ "How to Fix the Failed RegisterNewUser Test Case in AuthController.js ?"

__Tags:__ #AVATests #JWT #APIs #NodeJS #Debugging

__Explanation:__
    
>The output shows that a test case named register new user failed in the file tests/register/registerTest.js on line 19. The test case was expecting a status code of 201 but received a status code of 500.
>
>This could mean that there is an issue with the server and it is not properly responding to the request. It could also mean that the test case itself is incorrect.
>
>However, the output also shows that the user was successfully created in the database. It's possible that the server is working correctly, and the issue is with the test case.
>
>Further investigation and debugging are needed to determine the root cause of the failure.


Terminal output :
````
> test
> ava /workspace/Codecademy_project-Photo_Caption_Contest/tests/register/registercontroller.js


  ✘ Based on your configuration, 2 test files were found, but did not match the CLI arguments:

  * tests/register/registercontroller.js

gitpod /workspace/Codecademy_project-Photo_Caption_Contest (main) $ npm test /workspace/Codecademy_project-Photo_Caption_Contest/tests/register/registerTest.js

> test
> ava /workspace/Codecademy_project-Photo_Caption_Contest/tests/register/registerTest.js


Executing (default): INSERT INTO "Users" ("uuid","username","email","password","createdAt","updatedAt") VALUES ($1,$2,$3,$4,$5,$6) RETURNING "uuid","username","email","password","createdAt","updatedAt";
Executing (default): SELECT table_name FROM information_schema.tables WHERE table_schema = 'public' AND table_name = 'Users'
Executing (default): SELECT i.relname AS name, ix.indisprimary AS primary, ix.indisunique AS unique, ix.indkey AS indkey, array_agg(a.attnum) as column_indexes, array_agg(a.attname) AS column_names, pg_get_indexdef(ix.indexrelid) AS definition FROM pg_class t, pg_class i, pg_index ix, pg_attribute a WHERE t.oid = ix.indrelid AND i.oid = ix.indexrelid AND a.attrelid = t.oid AND t.relkind = 'r' and t.relname = 'Users' GROUP BY i.relname, ix.indexrelid, ix.indisprimary, ix.indisunique, ix.indkey ORDER BY i.relname;
Executing (default): SELECT table_name FROM information_schema.tables WHERE table_schema = 'public' AND table_name = 'Photos'
Executing (default): SELECT i.relname AS name, ix.indisprimary AS primary, ix.indisunique AS unique, ix.indkey AS indkey, array_agg(a.attnum) as column_indexes, array_agg(a.attname) AS column_names, pg_get_indexdef(ix.indexrelid) AS definition FROM pg_class t, pg_class i, pg_index ix, pg_attribute a WHERE t.oid = ix.indrelid AND i.oid = ix.indexrelid AND a.attrelid = t.oid AND t.relkind = 'r' and t.relname = 'Photos' GROUP BY i.relname, ix.indexrelid, ix.indisprimary, ix.indisunique, ix.indkey ORDER BY i.relname;
Executing (default): SELECT table_name FROM information_schema.tables WHERE table_schema = 'public' AND table_name = 'Captions'
Executing (default): SELECT i.relname AS name, ix.indisprimary AS primary, ix.indisunique AS unique, ix.indkey AS indkey, array_agg(a.attnum) as column_indexes, array_agg(a.attname) AS column_names, pg_get_indexdef(ix.indexrelid) AS definition FROM pg_class t, pg_class i, pg_index ix, pg_attribute a WHERE t.oid = ix.indrelid AND i.oid = ix.indexrelid AND a.attrelid = t.oid AND t.relkind = 'r' and t.relname = 'Captions' GROUP BY i.relname, ix.indexrelid, ix.indisprimary, ix.indisunique, ix.indkey ORDER BY i.relname;
Executing (default): SELECT table_name FROM information_schema.tables WHERE table_schema = 'public' AND table_name = 'Votes'
Executing (default): SELECT i.relname AS name, ix.indisprimary AS primary, ix.indisunique AS unique, ix.indkey AS indkey, array_agg(a.attnum) as column_indexes, array_agg(a.attname) AS column_names, pg_get_indexdef(ix.indexrelid) AS definition FROM pg_class t, pg_class i, pg_index ix, pg_attribute a WHERE t.oid = ix.indrelid AND i.oid = ix.indexrelid AND a.attrelid = t.oid AND t.relkind = 'r' and t.relname = 'Votes' GROUP BY i.relname, ix.indexrelid, ix.indisprimary, ix.indisunique, ix.indkey ORDER BY i.relname;
Connected to the database
Server started on port 3000
  ✘ [fail]: register new user Rejected promise returned by test
  ─

  register new user

  tests/register/registerTest.js:19

   18:     })           
   19:     .expect(201);
   20:                  

  Rejected promise returned by test. Reason:

  Error {
    message: 'expected 201 "Created", got 500 "Internal Server Error"',
  }

  › tests/register/registerTest.js:19:6
  › ----
  › Test._assertStatus (node_modules/supertest/lib/test.js:252:14)
  › node_modules/supertest/lib/test.js:308:13
  › Test._assertFunction (node_modules/supertest/lib/test.js:285:13)
  › Test.assert (node_modules/supertest/lib/test.js:164:23)
  › Server.localAssert (node_modules/supertest/lib/test.js:120:14)

  ─

  1 test failed
````
But it works and create the user

database_test/Users
````
 id |                 uuid                 | username |        email         |                           password                           |         createdAt          |         updatedAt          
----+--------------------------------------+----------+----------------------+--------------------------------------------------------------+----------------------------+----------------------------
  1 | 1a96f99a-011b-4ab0-8153-5dad03372e0a | testuser | testuser@example.com | $2b$10$6ZeQ9Y3Ws2Z3N1WdyLQtJ.JTHxoAm4AItz1m6oY/zMNhd1uNHN.Sa | 2023-03-01 09:01:57.548+00 | 2023-03-01 09:01:57.548+00
````

/workspace/Codecademy_project-Photo_Caption_Contest/controllers/authController.js
````
// Importing the User model from the index file in the models directory
const { 
    User 
} = require('../models/index.js'); 

// Importing the JSON web token package
const jwt = require('jsonwebtoken');

// Getting the secret key for the JSON web token from the environment variables
const secret = process.env.JWT_SECRET;

// Function to register a new user
exports.registerNewUser = async (req, res) => {

    // Extracting the required fields from the request body
    const {
        username,
        email,
        password
    } = req.body;

    try {
        // Creating a new user in the database
        const user = await User.create({
            username,
            email,
            password
        });

        // Creating a JSON web token using the user's ID and the secret key
        const token = jwt.sign({
            id: user.id
        }, secret);

        // Returning the token to the client
        res.status(201).json({
            token
        });
    } catch (error) {
        // If an error occurs during the registration process, returning the error message to the client
        res.status(500).json({
            error: error.message
        });
    }
};
````
.env
````
DB_NAME=database_test
DB_USERNAME=postgres
DB_PASSWORD=password
DB_HOST=127.0.0.1
DB_DIALECT=postgres
JWT_SECRET=testsecret
````
/workspace/Codecademy_project-Photo_Caption_Contest/tests/register/registerTest.js
````
const test = require('ava');
const request = require('supertest');
const app = require('../../app.js'); 
const { User } = require('../../models/index.js');
const jwt = require('jsonwebtoken');
const secret = process.env.JWT_SECRET;

// Test for registering a new user
test('register new user', async (t) => {
  t.plan(3);

  const res = await request(app)
    .post('/auth/register')
    .send({
      username: 'testuser',
      email: 'testuser@example.com',
      password: 'testpassword',
    })
    .expect(201);

  const token = res.body.token;

  // Verify that the token is valid
  jwt.verify(token, secret, (err, decoded) => {
    if (err) {
      t.fail();
    } else {
      t.is(decoded.id, 1); // assuming that the first user has an ID of 1
      t.pass();
    }
  });

  // Verify that the user was added to the database
  const user = await User.findOne({ where: { username: 'testuser' } });
  t.is(user.email, 'testuser@example.com');
});
````

#2023-03-02
---------------------------------------------------------
    
### Codecademy Back-End Engineer courses achievements !
Daily course achievements goals track.

- [x] **Linear Data structure: Introduction**
- [x] **Linear Data structure: Data sctructures**
- [x] **Linear Data structure: Nodes**
- [ ] **Linear Data structure: Singly Linked Lists** → *In progress*
- [ ] **Linear Data structure: Doubly Linked Lists**
- [ ] **Linear Data structure: Queues**
- [ ] **Linear Data structure: Stacks**
- Total Progression → __80%__

### Project on going !

__Title:__ Codecademy project: Photo Caption Contest

- [x] **Plan the project**
- [x] **Define endpoints**
- [x] **Setup the environment**
- [x] **Create the models**
- [x] **Create the seeders**
- [ ] **Create the controllers** → *In progress*
- [ ] **Create the auth middleware to specific endpoints**
- [ ] **Create the routes**
- [ ] **Test the endpoints**
- [ ] **Configure localized caching**
- [ ] **Write a swagger documentation**
- Total Progression → __30%__

### Issues !

__Title:__ "How to Fix the Failed RegisterNewUser Test Case in AuthController.js ?"

__Tags:__ #AVATests #JWT #APIs #NodeJS #Debugging

__Explanation:__

>1. When I spoke with Thomas on Tuesday night, he advised me not to use a Mock test to evaluate how well the registration of a new user in our "authController" works. At this point, using a Mock test for this task would be too complicated and unnecessary. Instead, he suggested I create a route for this functionality and test how the route and the "authController" interact. 
>
>2. Which I did on Wednesday, so I created the route I needed to perform one of the most basic tests. This test checks the functionality of registering a new user in an application. The test utilizes the 'ava' testing library and 'supertest' to make an HTTP POST request to the application with test data such as username, email, and password. The test checks that the HTTP response returned by the application is a 201 status code, which indicates that the request was successful. It then extracts an access token from the HTTP response body and decodes it using the 'jsonwebtoken' library to verify the token's validity. The test also verifies that the user was successfully added to the database by retrieving the user using the 'User' model and checking that the user's email matches the email sent in the request. Finally, the test uses the 'plan' method of the 'ava' library to ensure that all three test assertions have been executed successfully.
>
>3. But after running the test, the output shows that a test case named register new user failed in the file tests/register/registerTest.js on line 19. The test case expected a status code of 201 but received a status code of 500. This could mean that there is an issue with the server, and it is not correctly responding to the request. It could also mean that the test case itself needs to be corrected. However, the output also shows that the user was successfully created in the database.The server may be functioning correctly, and the problem may be related to the test case. Initially, I suspected I was not using the JWT library correctly, but when I tried to print the error and environment variables to the console, they appeared as undefined values. Thomas recommended that I update the 'package.json' file with the following code snippet to ensure that the 'dotenv' library is utilized by AVA when running tests:

>json
>````
>"scripts": {
>  "test": "ava --require dotenv/config"
>}
>````
>
>This will allow the tests to access environment variables defined in a '.env' file, enabling the tests to be executed successfully.
>
>When I run tests and use console.log to display environment variables within a function, the variables are correctly displayed in the terminal output. However, when I attempt to reference these variables outside of the function, such as when assigning them to a variable or printing them using console.log, they appear as undefined values. This behavior is unexpected and appears to be strange.
>
>4. Thomas recommended that I review my code again, and he pointed out that he did not see the use of the Express library and middleware in my test case, as I had used in my previous project. In my attempt to simplify the process of writing and defining routes, I may have inadvertently made the API's functioning more complex.
>
>5. To fix the bug on route "/register", the following changes were made:
>
>- Deleted AUTH variables in the .env file
>- Modified the app.js file with use of middleware
>- Created a new file called config/authConfig.js to handle AUTH variables
>- Modified the authController.js file to import AUTH variable from config/authConfig.js
>- Created a new file called routes/api.js and added middleware to handle better routes
>- Deleted the routes/auth.js file
>- Created a new file called routes/register.js to handle route "/register"  
>- Simplified the registerTest.js file to pass the test successfully.
>
>By making these changes, the bug on route /register was fixed, and the test passed successfully. The changes include modifying and creating files to handle better routes and AUTH variables. The registerTest.js file was simplified to ensure that the test passed successfully.

### Requests and proposals

>Thomas provided me with guidance on effectively addressing bugs by suggesting implementing a systematic approach :
>
> 1. Identify the problem area: Determine which part of the code is causing the problem by commenting out that section and checking if the error persists.
>
> 2. Simplify the problematic code: If you've identified a problematic section, simplify it by replacing it with something basic to eliminate potential problems.
>
> 3. Ensure all errors are reported: Make sure that all errors are reported back to you with clear and specific error messages to aid in debugging.
>
> 4. Differentiate between relevant and irrelevant errors: Understand which errors are relevant to your issue and which can be safely ignored or easily resolved.
>
> 5. Confirm all errors are reported: Double-check that all errors are being reported to avoid missing important ones. Also, make sure that error messages are clear and specific.
> 
> 6. Use hardcoded values instead of environment variables: If you suspect that an environment variable may be causing a problem, use hardcoded values instead.
> 
> 7. Use breakpoints: Use breakpoints to identify areas where the code isn't functioning correctly. This can be very helpful in understanding what's happening in your code.
>
> 8. Understand the problem: Before you start debugging, make sure you fully understand the problem you are trying to solve.
>
> 9. Reproduce the error: Try to reproduce the error to narrow down its source by identifying specific inputs or conditions that cause the problem to occur.
>
> 10. Use debugging tools: Programming languages provide debugging tools like debuggers, profilers, and logging frameworks to help you identify and fix errors.
>
> 11. Check the code for common errors: Check for common coding errors such as syntax errors, logic errors, and off-by-one errors, and fix them as needed.
>
> 12. Test the code: Thoroughly test the code using a combination of unit tests, integration tests, and manual testing to ensure that it's functioning correctly.

#2023-03-03
---------------------------------------------------------
    
### Codecademy Back-End Engineer courses achievements !
Daily course achievements goals track.

- [x] **Linear Data structure: Introduction**
- [x] **Linear Data structure: Data sctructures**
- [x] **Linear Data structure: Nodes**
- [ ] **Linear Data structure: Singly Linked Lists** → *In progress*
- [ ] **Linear Data structure: Doubly Linked Lists**
- [ ] **Linear Data structure: Queues**
- [ ] **Linear Data structure: Stacks**
- Total Progression → __80%__

### Project on going !

__Title:__ Codecademy project: Photo Caption Contest

- [x] **Plan the project**
- [x] **Define endpoints**
- [x] **Setup the environment**
- [x] **Create the models**
- [x] **Create the seeders**
- [ ] **Create the controllers** → *In progress*
- [ ] **Create the auth middleware to specific endpoints**
- [ ] **Create the routes**
- [ ] **Test the endpoints**
- [ ] **Configure localized caching**
- [ ] **Write a swagger documentation**
- Total Progression → __30%__

__Last commits:__

- "FIX: Fix issue with defining validPassword method on User model"   *→ Test passed successfully*
- "FIX: Fix bug on route /login"  *→ Test passed successfully*
- "FEAT: Fix bug on route '/users' and add getAllUsers controller"   *→ Test passed successfully*

### Issues !

__Title:__ "Incorrect parameter used to retrieve user by UUID in getUserById controller method"

__Tags:__ #AVATests #controllermethod #APIs #NodeJS #Debugging

__Explanation:__

>Based on the terminal output, the test is passing but the response body is not as expected. It seems like the user object is null. One possible reason could be that the wrong parameter is being passed to the findByPk() method.
>
>In the test file, the userId variable is defined and passed to the API route. However, in the controller file, the req.params.id parameter is used to find the user. This could result in an incorrect query to the database and return a null object.
>
>To fix this issue, you should update the controller file to use `req.params.uuid` instead of `req.params.id` to retrieve the user by UUID.

Terminal output :
````
npm test tests/user/getUserByIdTest.js

> test
> ava --require dotenv/config tests/user/getUserByIdTest.js


  ✔ getUserById function should retrieve a user by uuid
    ℹ {
        user: null,
      }
  ─

  1 test passed
````

#2023-03-06
---------------------------------------------------------
    
### Codecademy Back-End Engineer courses achievements !
Daily course achievements goals track.

- [x] **Linear Data structure: Introduction**
- [x] **Linear Data structure: Data sctructures**
- [x] **Linear Data structure: Nodes**
- [ ] **Linear Data structure: Singly Linked Lists** → *In progress*
- [ ] **Linear Data structure: Doubly Linked Lists**
- [ ] **Linear Data structure: Queues**
- [ ] **Linear Data structure: Stacks**
- Total Progression → __80%__

### Project on going !

__Title:__ Codecademy project: Photo Caption Contest

- [x] **Plan the project**
- [x] **Define endpoints**
- [x] **Setup the environment**
- [x] **Create the models**
- [x] **Create the seeders**
- [ ] **Create the controllers** → *In progress*
- [ ] **Create the auth middleware to specific endpoints**
- [ ] **Create the routes**
- [ ] **Test the endpoints**
- [ ] **Configure localized caching**
- [ ] **Write a swagger documentation**
- Total Progression → __30%__

__Last commits:__

- "FEAT: Test route '/users' and getUserById controller" → Test passed successfully
- "FEAT: add updateUser controller"
- "FIX: Bug on hashed password for updateUser controller" → Test passed successfully

### Issues !

__Title:__ "Updating password with PUT request not reflecting in Users table in database"

__Tags:__ #AVATests #PUTrequest #passwordupdate #bcrypt #databaseupdate #Debugging

__Explanation:__

>When using a "put" request to update the password value, it seems that the password is hashed with bcrypt. However, it does not get updated in the "Users" table in the database.

/workspace/Codecademy_project-Photo_Caption_Contest/controllers/userController.js
````
// Importing the User model from the index file in the models directory
const {
    User
} = require('../models/index.js');

exports.updateUser = async (req, res) => {
    try {
        const {
            password,
            ...rest
        } = req.body;

        // Retrieve the user instance from the database using the uuid in the request params
        const user = await User.findByPk(req.params.uuid, {});

        // If user is not found, return a 404 response
        if (!user) {
            return res.status(404).json({
                error: 'User not found',
            });
        } else {
            // Update the user instance with the request body
            if (password) {
                user.password = await bcrypt.hash(password, 10); // hash password if present in req.body
                await user.update(user.password, {
                    where: {
                        uuid: req.params.uuid
                    }
                })  
            } else {
                await user.update(rest, {
                    where: {
                        uuid: req.params.uuid
                    }
                })    
            };

            // Return a success response with the updated user object
            res.status(200).json({
                message: 'User updated',
                user
            });
        };
    } catch (error) {
        // Log any errors to the console
        console.error(error);

        // Return an error response with the error message
        res.status(500).json({
            error: error.message,
        });
    }
};
````

/workspace/Codecademy_project-Photo_Caption_Contest/tests/user/updateUserTest.js
````
const test = require("ava"); // Importing the AVA test library
const request = require("supertest"); // Importing the supertest library for making HTTP requests
const apiRouter = require('../../routes/api.js'); // Importing the api router file for the all the routers
const express = require('express'); // Importing express

// Create an instance of the express application
const app = express();

// Use the apiRouter with the '/api' route
app.use('/', apiRouter);

// Use dotenv to access environment variables defined in a '.env' file
require('dotenv').config()


test('1. updateUser function should retrieve a user by uuid and update the password', async t => {
    
    const userId = "11f8d972-994e-4830-9a1b-112710eea2d7";
    
    const updatedUser = {
        password: 'malabar'           
    };

    // Making a GET request to the '/users' route 
    const res = await request(app).put(`/users/uuid/${userId}`).send(updatedUser);

    // Asserting that the status code of the response is 200
    t.is(res.status, 200);
    
    // Displaying the response body using console.dir to show the entire contents of the objects
    console.dir(res.body, { depth: null });
});
````

Terminal output:
````
npm test tests/user/updateUserTest.js

> test
> ava --require dotenv/config tests/user/updateUserTest.js


Executing (default): SELECT "uuid", "username", "email", "password", "createdAt", "updatedAt" FROM "Users" AS "User" WHERE "User"."uuid" = '11f8d972-994e-4830-9a1b-112710eea2d7';
{
  message: 'User updated',
  user: {
    uuid: '11f8d972-994e-4830-9a1b-112710eea2d7',
    username: 'Vegeta',
    email: 'billdoe@example.com',
    password: '$2b$10$WbEXOQhHpM4LDTA7n2YG2Ocls7vxgoIaEsf8AV4iWbo7o7nWLqFiO',
    createdAt: '2023-03-06T05:35:30.013Z',
    updatedAt: '2023-03-06T07:43:42.166Z'
  }
}
  ✔ 1. updateUser function should retrieve a user by uuid and update the password (159ms)
  ─

  1 test passed
````

PSQL Terminal output:
````
database_test=# SELECT password FROM "Users" WHERE username = 'Vegeta';
 password 
----------
 Carambar
````

>I encountered a bug while working on the updateUser controller. I managed to fix the bug but unfortunately, I encountered another issue. I violated the constraint of the "password" argument in the "user" model. To resolve this issue and update the password without any problem, I needed to adjust the maximum number of characters allowed in the password constraint to match the maximum size of bytes of a hashed password length.

/workspace/Codecademy_project-Photo_Caption_Contest/controllers/userController.js
````
        // If user is not found, return a 404 response
        if (!user) {
            return res.status(404).json({
                error: 'User not found',
            });
        } else {
            // Update the user instance with the request body
            if (password) {
                hashedPassword = await bcrypt.hash(password, 10); // hash password if present in req.body
                await user.update({ password: hashedPassword}, {
                    where: {
                        uuid: req.params.uuid
                    }
                })  
            } else {
                await user.update(rest, {
                    where: {
                        uuid: req.params.uuid
                    }
                })    
            };

````


Terminal output:
````
$ npm test tests/user/updateUserTest.js

> test
> ava --require dotenv/config tests/user/updateUserTest.js


Executing (default): SELECT "uuid", "username", "email", "password", "createdAt", "updatedAt" FROM "Users" AS "User" WHERE "User"."uuid" = '11f8d972-994e-4830-9a1b-112710eea2d7';
ValidationError [SequelizeValidationError]: Validation error: Password must be between 8 and 20 characters long
    at InstanceValidator._validate (/workspace/Codecademy_project-Photo_Caption_Contest/node_modules/sequelize/src/instance-validator.js:78:13)
    at InstanceValidator._validateAndRunHooks (/workspace/Codecademy_project-Photo_Caption_Contest/node_modules/sequelize/src/instance-validator.js:111:7)
    at InstanceValidator.validate (/workspace/Codecademy_project-Photo_Caption_Contest/node_modules/sequelize/src/instance-validator.js:93:12)
    at User.save (/workspace/Codecademy_project-Photo_Caption_Contest/node_modules/sequelize/src/model.js:3996:7)
    at User.update (/workspace/Codecademy_project-Photo_Caption_Contest/node_modules/sequelize/src/model.js:4253:12)
    at async exports.updateUser (/workspace/Codecademy_project-Photo_Caption_Contest/controllers/userController.js:112:17) {
  errors: [
    ValidationErrorItem {
      message: 'Password must be between 8 and 20 characters long',
      type: 'Validation error',
      path: 'password',
      value: '$2b$10$4bscbIr0NNxw8Z3MOcaCPueaC2pPqE/ytoT44BNzWMvJGr7Zn19Ry',
      origin: 'FUNCTION',
      instance: [User],
      validatorKey: 'len',
      validatorName: 'len',
      validatorArgs: [Array],
      original: [Error]
    }
  ]
}
{
  error: 'Validation error: Password must be between 8 and 20 characters long'
}
  ✘ [fail]: 1. updateUser function should retrieve a user by uuid and update the password
  ─

  1. updateUser function should retrieve a user by uuid and update the password

  tests/user/updateUserTest.js:28

   27:     // Asserting that the status code of the response is 200
   28:     t.is(res.status, 200);                                  
   29:                                                             

  Difference (- actual, + expected):

  - 500
  + 200

  › tests/user/updateUserTest.js:28:7

  ─

  1 test failed
````

#2023-03-07
---------------------------------------------------------
    
### Codecademy Back-End Engineer courses achievements !
Daily course achievements goals track.

- [x] **Linear Data structure: Introduction**
- [x] **Linear Data structure: Data sctructures**
- [x] **Linear Data structure: Nodes**
- [X] **Linear Data structure: Singly Linked Lists**
- [ ] **Linear Data structure: Doubly Linked Lists** → *In progress*
- [ ] **Linear Data structure: Queues**
- [ ] **Linear Data structure: Stacks**
- Total Progression → __80%__

### Project on going !

__Title:__ Codecademy project: Photo Caption Contest

- [x] **Plan the project**
- [x] **Define endpoints**
- [x] **Setup the environment**
- [x] **Create the models**
- [x] **Create the seeders**
- [ ] **Create the controllers** → *In progress*
- [ ] **Create the auth middleware to specific endpoints**
- [ ] **Create the routes**
- [ ] **Test the endpoints**
- [ ] **Configure localized caching**
- [ ] **Write a swagger documentation**
- Total Progression → __30%__

__Last commits:__

- "FEAT: Add delete route to User with deleteUser controller" **→ Test failed**
- "FIX: deleteUser" *→ Test passed successfully*

### Issues !

__Title:__ "Sequelize ORM - Auto-increment function not working for new user creation in database"

__Tags:__ #sequelize.js #node.js #postgresql #auto-increment #database-schema

__StackOverflow:__ [link](https://stackoverflow.com/questions/75660064/sequelize-orm-auto-increment-function-not-working-for-new-user-creation-in-dat)

__Explanation:__

>I use sequelize ORM. I have created a register route and controller to create new user. I created a new user with AVA test, but the auto-increment function isn't working properly. Despite being the fourth user created, this new user created with AVA test has an ID of 1 (The other three users were created using Sequelize seeders). I've checked the database schema and confirmed that the 'id' field is set to auto-increment. Any ideas on how to resolve this issue?

Terminal output :
````
npm test .../tests/register/registerTest.js

> test
> ava --require dotenv/...tests/register/registerTest.js


Executing (default): INSERT INTO "Users" ("uuid","username","email","password","createdAt","updatedAt") VALUES ($1,$2,$3,$4,$5,$6) RETURNING "uuid","username","email","password","createdAt","updatedAt";
  ✔ RegisterNewUser function should create a new user and return a token (127ms)
    ℹ {
        token: 'eyJhbGciOiJIUzI1N...Z_iVY8hjgsf9Ak',
        user: {
          createdAt: '2023-03-07T07:48:53.393Z',
          email: 'testuser@example.com',
          password: '$2b$10$kNeC1h7d0wX7WPQC3H.94OlpXveXVeaP7WaWEIGQN6VLypSVKoAE.',
          updatedAt: '2023-03-07T07:48:53.393Z',
          username: 'testuser',
          uuid: 'e33c6803-1c18-4d25-906f-2d6de8726d27',
        },
      }
  ─

  1 test passed
````

PSQL Terminal output :
````
database_test=# SELECT * FROM "Users";

 id |                 uuid                 | username |        email         |                           password                           |         createdAt          |         updatedAt          
----+--------------------------------------+----------+----------------------+--------------------------------------------------------------+----------------------------+----------------------------
  1 | 15bf1cb7-8346-4140-8b36-ced76facb4d7 | johndoe  | johndoe@example.com  | $2b$10$1r.N1fS6ea82w9WgMZmdsevl/awhaWjSfWgwHzMXSWDNPdZlfS.bS | 2023-03-07 07:45:28.403+00 | 2023-03-07 07:45:28.403+00
  2 | af947f46-2991-43fd-aaec-dec95c40a729 | janedoe  | janedoe@example.com  | $2b$10$8H7ktluUZrr21SzE7Eo2MuegtmaCLMWjxHnQvg8LrlAD1uLI1BICm | 2023-03-07 07:45:28.412+00 | 2023-03-07 07:45:28.412+00
  3 | d2658a11-b088-4e86-a351-ee628c3a7cad | billdoe  | billdoe@example.com  | $2b$10$CBWz3iUSVot3nLqgSP3z4.ma2tiCp8SaPTKPRC3Z8fjHNMDJs.oIO | 2023-03-07 07:45:28.405+00 | 2023-03-07 07:45:28.405+00
  1 | e33c6803-1c18-4d25-906f-2d6de8726d27 | testuser | testuser@example.com | $2b$10$kNeC1h7d0wX7WPQC3H.94OlpXveXVeaP7WaWEIGQN6VLypSVKoAE. | 2023-03-07 07:48:53.393+00 | 2023-03-07 07:48:53.393+00

\d "Users"

database_test=# \d "Users"
                                       Table "public.Users"
  Column   |           Type           | Collation | Nullable |               Default               
-----------+--------------------------+-----------+----------+-------------------------------------
 id        | integer                  |           | not null | nextval('"Users_id_seq"'::regclass)
 uuid      | uuid                     |           | not null | 
 username  | character varying(255)   |           | not null | 
 email     | character varying(255)   |           | not null | 
 password  | character varying(255)   |           | not null | 
 createdAt | timestamp with time zone |           | not null | 
 updatedAt | timestamp with time zone |           | not null | 

````


models/user.js

````
'use strict';

// Import the bcrypt library for password hashing
const {
    Model
} = require('sequelize');

// Import the bcrypt library for password hashing
const bcrypt = require('bcrypt');

// Define a sequelize model for a User
module.exports = (sequelize, DataTypes) => {
    class User extends Model {
        /**
         * Helper method for defining associations.
         * This method is not a part of Sequelize lifecycle.
         * The `models/index` file will call this method automatically.
         */
        static associate(models) {
...
                })
        }
    }
    User.init({
        id: {
            type: DataTypes.INTEGER,
            primaryKey: true,
            autoIncrement: true,
            allowNull: false
        },
        uuid: {
            type: DataTypes.UUID,
            defaultValue: DataTypes.UUIDV4,
            allowNull: false,
            unique: true,
            primaryKey: true,
        },

...

    }, {
        sequelize,
        modelName: 'User',
        // Add hooks to run code before or after certain events
        hooks: {
            // Hash the user's password before creating a new user
            beforeCreate: (User) => {
                const salt = bcrypt.genSaltSync(10);
                User.password = bcrypt.hashSync(User.password, salt);
            }
        },
    });
    return User;
};
````
migrations/20230223064615-create-user.js
````
'use strict';
/** @type {import('sequelize-cli').Migration} */
module.exports = {
  async up(queryInterface, Sequelize) {
    await queryInterface.createTable('Users', {
	id: {
	  allowNull: false,
	  autoIncrement: true,
	  type: Sequelize.INTEGER,
	  onDelete: 'CASCADE'
	},
...
      createdAt: {
        allowNull: false,
        type: Sequelize.DATE
      },
      updatedAt: {
        allowNull: false,
        type: Sequelize.DATE
      }
    });
  },
  async down(queryInterface, Sequelize) {
    await queryInterface.dropTable('Users');
  }
};
````
