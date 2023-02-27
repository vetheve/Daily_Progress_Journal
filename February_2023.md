Daily Progress Journal
======================

"Tracking My Progress: Daily Journaling to Achieve Goals"

* **February 2023**

|Mon  |Tue  |Wed  |Thu  |Fri  |Sat  |Sun  |
|---:|---:|---:|---:|---:|---:|---:|
|     |     |1    |2    |[3](#2023-02-03)    |4    |5    |
|[6](#2023-02-06)    |[7](#2023-02-07)    |[8](#2023-02-08)     |[9](#2023-02-09)   |[10](#2023-02-10)   |11   |12   |
|[13](#2023-02-13)   |[14](#2023-02-14)   |[15](#2023-02-15)   |[16](#2023-02-16)   |[17](#2023-02-17)   |18   |19   |
|[20](#2023-02-20)   |[21](#2023-02-21)   |22   |[23](#2023-02-23)   |[24](#2023-02-24)   |25   |26   |
|[27](#2023-02-27)   |28   |     |     |     |     |     |



#2023-02-03
---------------------------------------------------------
### Courses achievements !
Daily course achievements goals track.

- [x] **25. WEB Security Fundamentals : OSWAP 2017**
- [x] **25. WEB Security Fundamentals : OSWAP Top 10**
- [x] **25. WEB Security Fundamentals : Review**
- [x] **26. User Athentication and Authorization : Introduction**
- [x] **26. User Athentication and Authorization : Authentication, Authorization, and Encryption**
- [ ] **26. User Athentication and Authorization : Session Authetication in Express.js** → *In progress*
- Total Progression → __60%__

### Project on going !

__Title:__ Portfolio Project: Personal Budget II

>In this project, you will extend the Personal Budget API created in Personal Budget, Part I. In the first Budget API, we did not have a way to persist data on the server. Now, we are going to build out a persistence layer (aka a database or DB) to keep track of the budget envelopes and their balances. You will need to plan out your database design, then use PostgreSQL to create the necessary tables. Once your database is set up, connect your API calls to a database. Once you’ve added and connected your database, you will add a new feature to your server that allows users to enter transactions. This feature will put your envelope system into action! Finally, you will make your API available for others to use by documenting it with Swagger and deploying it with Heroku.

- [x] **Setting up Git tracking** → __100%__
- [x] **Design the database** → __100%__
- [x] **Setup the database** → __100%__
- [x] **Create the tables** → __100%__
- [x] **Connect the database** → __100%__
- [x] **Create your transactions endpoints** → __100%__
- [ ] **Create the transactions** → __50%__
- [ ] **Test the transactions** → __50%__
- [ ] **Test the transactions endpoints** → __50%__
- [ ] **Write the documentation using SWAGGER** → __50%__
- [ ] **Deploy the application on Heroku** → __0%__
- Total Progression → __72%__

__Last commits:__

- "ADD: Implement and test Endpoints /budgets for POST Request new budget and GET Request all budgets." → *Tests passed successfully*
- "ADD: Implement and test Endpoints /budgets/:id for GET Request." → *Test passed successfully*

### Issues !

__Title:__ Test Fails When Checking Budget Balance from GET Request

__Tags:__ #Node.js #Express.js #Testing #PostgreSQL #AVA

__Explanation:__

> In this case, there is a test that checks the response from a GET request to the /budgetbalance/:category route. This route is designed to return the total budget balance for a specific category. The test is using the AVA testing framework and makes a request to the route with a specified category.
>
> The expected result is a 200 status code with a response body that contains the budget balance for that category with the key budget_balance. However, the actual result is a 200 status code, but the value of budget_balance is null. This means that the test is failing because the expected value of budget_balance is 300, but the actual value is null.
>
> This issue could be caused by a number of things, errors in the SQL query, or a mistake in the implementation of the route. The data in the database is valid, no problem was observed.

__Code:__

AVA test - [[1]](https://github.com/vetheve/-Codecademy-Portfolio-Project-Personal-Budget-2/blob/main/test/balance/budget_balance_test.js)
```
// Test to check if the Get request to '/budgetbalance/:category' route returns the total budget balance by category
test('5.4 Get /budgetbalance/:category should returns the total budget balance by category', async t => {

    // Selecting an category to test with
    const category = 'housing';

    // Making a Get request to the '/budgetbalance/:category' route which does not exist yet
    const res = await request(app).get(`/budgetbalance/${category}`);
    
    // Asserting that the status code of the response is 200
    t.is(res.status, 200);
    
    // Print the object in the console
    t.log(res.body)
        
    // Asserting that the response body is an object and contains the key 'Budget balance'
    t.true(typeof res.body === 'object' && 'budget_balance' in res.body);
    
    // Asserting that the value of the 'Budget balance' key is 300
    t.is(res.body['budget_balance'], '300');
});
```

Request to test - [[2]](https://github.com/vetheve/-Codecademy-Portfolio-Project-Personal-Budget-2/blob/main/server/budget_balance.js)
```
budgetBalanceRouter
  .route('/:category')
  // Get the total budget balance for a specific category
  .get((req, res) => {
    const category = req.params.category;
    // Connect to the PostgreSQL database using the connection pool
    pool.query(`
    -- Define the subquery to calculate the total amount of budgets
    WITH budget_total AS (
    SELECT SUM(amount) as total_budgets
    FROM budgets
    WHERE category = $1),
    -- Define the subquery to calculate the total amount of expenses 
    expense_total AS (
    SELECT SUM(amount) as total_expenses
    FROM expenses
    WHERE category = $1)
    -- Calculate the budget balance by subtracting the total expenses from the total budgets
    SELECT total_budgets - total_expenses as budget_balance
    FROM budget_total, expense_total;`, [category], (err, result) => {
        if (err) {
            // If there was an error, return a 500 status code with an error message
            res.status(500).json({
                error: "Error fetching budget balance"
            });
        } else {
            // If the query was successful, return a 200 status code with the result
            res.status(200).json(result.rows[0]);
        }
    });
});
```

Terminal output :
```
✘ [fail]: budget_balance_test › 5.4 Get /budgetbalance/:category should returns the total budget balance by category
    ℹ {
        budget_balance: null,
      }
  ─

  budget_balance_test › 5.4 Get /budgetbalance/:category should returns the total budget balance by category
  test/balance/budget_balance_test.js:103

   102:     // Asserting that the value of the 'Budget balance' key is 300
   103:     t.is(res.body['budget_balance'], '300');                      
   104: });                                                               

  Difference (- actual, + expected):

  - null
  + '300'

  › test/balance/budget_balance_test.js:103:7

  ─

  1 test failed
```
### Requests and proposals

>The error in the endpoint is that the variables are being used directly in the endpoint URL instead of being defined correctly, which could result in unexpected behavior and incorrect results when the endpoint is called. It's recommended to properly define the variables, instead of `/:category` it is necessary to use `/budgetbalance/category/:category`.



#2023-02-06
---------------------------------------------------------
### Courses achievements !
Daily course achievements goals track.

- [x] **26. User Athentication and Authorization : Session Authetication in Express.js**
- [ ] **26. User Athentication and Authorization : Password Authentication** → *In progress*
- Total Progression → __60%__

### Project on going !

__Title:__ Portfolio Project: Personal Budget II

- [x] **Setting up Git tracking** → __100%__
- [x] **Design the database** → __100%__
- [x] **Setup the database** → __100%__
- [x] **Create the tables** → __100%__
- [x] **Connect the database** → __100%__
- [x] **Create your transactions endpoints** → __100%__
- [ ] **Create the transactions** → __60%__
- [ ] **Test the transactions** → __60%__
- [ ] **Test the transactions endpoints** → __60%__
- [ ] **Write the documentation using SWAGGER** → __50%__
- [ ] **Deploy the application on Heroku** → __0%__
- Total Progression → __76%__

__Last commits:__

- "FIX: try to fix PUT request to /budgets/id/:id." → *Test failed*
- "ADD: Implement and test Endpoint for deleting budget with DELETE Request."  → *Test passed successfully*
- "ADD: Implement and test Endpoint for Fetching all expenses records with GET request."  → *Test passed successfully*
- "FIX: Fix endpoint /budgets/budget_id/:budget_id." → *PUT request test failed but other tests passed successfully*

### Issues !

__Title:__ Test Fails When Updating Budget from PUT Request

__Tags:__ #Node.js #Express.js #Testing #PostgreSQL #AVA

__StackOverflow:__ [link](https://stackoverflow.com/questions/75385383/syntax-error-in-postgresql-query-how-to-dynamically-update-a-specific-column)

__Explanation:__

>The AVA test for the PUT request to the "/budgets/id/:id" route is failing. The expected response status code is 201, indicating a successful update, but the actual status code received is 500, indicating an internal server error. This is likely due to an error in the endpoint code's SQL query that prevents the budget from being updated in the budgets table. The terminal output and PSQL result shows that the budget has not been updated with the new "Very personal" category value, as expected.
>The error message "syntax error at or near "$2"" suggests that there's a problem in the SQL query in the PUT endpoint of the "/budgets/id/:id" route. It seems that the query is attempting to set the value of an object's key to the value of a variable in the query, which is not allowed in SQL. To resolve this, I need to modify the query to properly reference the keys of the element object, or use a different approach to dynamically build the SQL query.

__Code:__

AVA test - [[3]](https://github.com/vetheve/-Codecademy-Portfolio-Project-Personal-Budget-2/blob/main/test/budgets/budgets_test.js)
````
// Test to check if the PUT request to '/budgets/id/:id' route updates a budget in the list budgets
test('1.4 PUT /budgets/budget_id/:budget_id should update a budget in the list', async t => {

    // Selecting a budget ID to test with
    const budgetId = "2022-02 Personnal Budget";

    // Creating a new budget object to update
    const updatedBudget = {
        item: "category",
        value: "Very personnal"
    };
    
    // Making a PUT request to the '/budgets/budget_id/:budget_id' route with the updated budget object
    const res = await request(app).put(`/budgets/budget_id/${budgetId}`).send(updatedBudget);

    // Asserting that the status code of the response is 201
    t.is(res.status, 201);

    // Print the object in the console
    t.log(res.body)
});

````
Request to test - [[4]](https://github.com/vetheve/-Codecademy-Portfolio-Project-Personal-Budget-2/blob/main/server/budgets.js)
````
// Endpoint to handle requests to a specific budget resource by ID
budgetsRouter
    .route('/budget_id/:budget_id')
    // Update an existing budget in the list
        // Update an existing budget in the list
    .put((req, res) => {
        // Destructure budget_id, item, and value from the request body
        const budget_id = req.params.budget_id
        const {
            item,
            value
        } = req.body;

        // Generate a timestamp and convert it to an ISO string format
        const timestamp = Date.now();
        const isoString = new Date(timestamp).toISOString();

        // Create a budget object with the provided information and default timestamp and ID values
        const element = {
            budget_id: budget_id,
            item: item,
            value: value,
            dt_update: isoString
        };

        // Execute a query to update the existing budget in the budgets table
        pool.query(`
      -- Define the subquery to update an existing record in the budgets table
      UPDATE budgets
      SET $2 = $3, dt_update = to_timestamp($4, 'YYYY-MM-DD"T"HH24:MI:SS.MS')
      WHERE budget_id = $1;
        `, [element.budget_id, element.item, element.value, element.dt_update], (err, result) => {
            // If there is an error, return a 500 status code with an error message
            if (err) {
                res.status(500).json({
                    error: "Error updating budget"
                });
            }
            // If the query is successful, return a 201 status code with a success message
            else {
                res.status(201).json({
                    message: "Budget updated successfully"
                });
            }
        });
    });
````

Terminal output :

````
/workspace/-Codecademy-Portfolio-Project-Personal-Budget-2/node_modules/pg-protocol/src/parser.ts:369
      name === 'notice' ? new NoticeMessage(length, messageValue) : new DatabaseError(messageValue, length, name)
                                                                    ^

error: syntax error at or near "$2"
    at Parser.parseErrorMessage (/workspace/-Codecademy-Portfolio-Project-Personal-Budget-2/node_modules/pg-protocol/src/parser.ts:369:69)
    at Parser.handlePacket (/workspace/-Codecademy-Portfolio-Project-Personal-Budget-2/node_modules/pg-protocol/src/parser.ts:188:21)
    at Parser.parse (/workspace/-Codecademy-Portfolio-Project-Personal-Budget-2/node_modules/pg-protocol/src/parser.ts:103:30)
    at Socket.<anonymous> (/workspace/-Codecademy-Portfolio-Project-Personal-Budget-2/node_modules/pg-protocol/src/index.ts:7:48)
    at Socket.emit (node:events:513:28)
    at addChunk (node:internal/streams/readable:315:12)
    at readableAddChunk (node:internal/streams/readable:289:9)
    at Socket.Readable.push (node:internal/streams/readable:228:10)
    at TCP.onStreamRead (node:internal/stream_base_commons:190:23) {
  length: 92,
  severity: 'ERROR',
  code: '42601',
  detail: undefined,
  hint: undefined,
  position: '112',
  internalPosition: undefined,
  internalQuery: undefined,
  where: undefined,
  schema: undefined,
  table: undefined,
  column: undefined,
  dataType: undefined,
  constraint: undefined,
  file: 'scan.l',
  line: '1145',
  routine: 'scanner_yyerror'
}

  ✘ [fail]: 1.4 PUT /budgets/budget_id/:budget_id should update a budget in the list
    ℹ {
        error: 'Error updating budget',
      }
  ─

  1.4 PUT /budgets/id/:id should update a budget in the list
  test/budgets/budgets_test.js:96

   95:     // Asserting that the status code of the response is 201
   96:     t.is(res.status, 201);                                  
   97:                                                             

  Difference (- actual, + expected):

  - 500
  + 201

  › test/budgets/budgets_test.js:96:7

  ─

  1 test failed
````

PSQL result
````
balance_budget=# SELECT * FROM budgets
balance_budget-# WHERE budget_id = '2022-02 Personnal Budget';
 id |        budget_id         |        dt_create        |        dt_update        |        dt_value         | category  | amount 
----+--------------------------+-------------------------+-------------------------+-------------------------+-----------+--------
 61 | 2022-02 Personnal Budget | 2023-01-25 06:49:04.171 | 2023-01-25 06:49:04.171 | 2023-01-25 06:49:04.171 | personnal |      0
(1 row)
````

Expected PSQL result
````
balance_budget=# SELECT * FROM budgets
balance_budget-# WHERE budget_id = '2022-02 Personnal Budget';
 id |        budget_id         |        dt_create        |        dt_update        |        dt_value         |    category    | amount 
----+--------------------------+-------------------------+-------------------------+-------------------------+----------------+--------
 61 | 2022-02 Personnal Budget | 2023-01-25 06:49:04.171 | 2023-02-06 06:49:04.171 | 2023-01-25 06:49:04.171 | Very personnal |      0
(1 row)
````
### Requests and proposals
>I plan to change the process for changing a record's information. The user will only be able to modify the description, the "dt_value" & category. The previous process allowed the user to modify any value, including the creation date, which was a problem because it allowed the user to falsify the data. 


#2023-02-07
---------------------------------------------------------
### Courses achievements !
Daily course achievements goals track.

- [x] **26. User Athentication and Authorization : Password Authentication**
- [x] **26. User Athentication and Authorization : OAuth 2.0**
- [x] **26. User Athentication and Authorization : Review**
- [x] **27. Data Security : Introduction**
- [x] **27. Data Security : Transport Layer Security (TLS)** → *In progress*
- [ ] **27. Data Security : Role-Based Access Control (RBAC)** → *Not begin yet*
- Total Progression → __61%__

### Project on going !

__Title:__ Portfolio Project: Personal Budget II

- [x] **Setting up Git tracking** → __100%__
- [x] **Design the database** → __100%__
- [x] **Setup the database** → __100%__
- [x] **Create the tables** → __100%__
- [x] **Connect the database** → __100%__
- [x] **Create your transactions endpoints** → __100%__
- [ ] **Create the transactions** → __60%__
- [ ] **Test the transactions** → __60%__
- [ ] **Test the transactions endpoints** → __60%__
- [ ] **Write the documentation using SWAGGER** → __50%__
- [ ] **Deploy the application on Heroku** → __0%__
- Total Progression → __76%__

__Last commits:__

- I did not add any new features to my app today.


#2023-02-08
---------------------------------------------------------
### Courses achievements !
Daily course achievements goals track.

- [x] **27. Data Security : Role-Based Access Control (RBAC)**
- [x] **27. Data Security : Authentification and Authorization in Postgre**
- [x] **27. Data Security : Managing Environment Variables, Api Keys, etc...**
- [x] **27. Data Security : Off-Platform Project Securing School Data**
- [x] **27. Data Security : Review**
- [x] **28. Common Attacks on Web Applications : Introduction**
- [ ] **28. Common Attacks on Web Applications : Preventing Cross-Site Request Forgery (CSRF) Attacks** → *In progress*
- Total Progression → __63%__

### Project on going !

__Title:__ Portfolio Project: Personal Budget II

- [x] **Setting up Git tracking** → __100%__
- [x] **Design the database** → __100%__
- [x] **Setup the database** → __100%__
- [x] **Create the tables** → __100%__
- [x] **Connect the database** → __100%__
- [x] **Create your transactions endpoints** → __100%__
- [ ] **Create the transactions** → __64%__
- [ ] **Test the transactions** → __64%__
- [ ] **Test the transactions endpoints** → __64%__
- [ ] **Write the documentation using SWAGGER** → __50%__
- [ ] **Deploy the application on Heroku** → __0%__
- Total Progression → __77%__

__Last commits:__

- "ADD: Implement and test Endpoints for updating a budget record." → *Test passed successfully*
- "ADD: Implement and test Endpoints for updating a budget record - PUT Request."  → *Test passed successfully*


#2023-02-09
---------------------------------------------------------
### Courses achievements !
Daily course achievements goals track.

- [x] **28. Common Attacks on Web Applications : Preventing Cross-Site Request Forgery (CSRF) Attacks**
- [x] **28. Common Attacks on Web Applications : Preventing SQL Injection Attacks**
- [x] **28. Common Attacks on Web Applications : Preventing Cross-Site Scripting (XSS) Attacks**
- [x] **28. Common Attacks on Web Applications : Defensive Coding in JS**
- [x] **28. Common Attacks on Web Applications : Remediation and Incident Response**
- [ ] **28. Common Attacks on Web Applications : Securing Acme Bank - Defending Node Applications** → *In progress*
- [x] **28. Common Attacks on Web Applications : Review**
- Total Progression → __66%__

### Project on going !

__Title:__ Portfolio Project: Personal Budget II

- [x] **Setting up Git tracking** → __100%__
- [x] **Design the database** → __100%__
- [x] **Setup the database** → __100%__
- [x] **Create the tables** → __100%__
- [x] **Connect the database** → __100%__
- [x] **Create your transactions endpoints** → __100%__
- [ ] **Create the transactions** → __64%__
- [ ] **Test the transactions** → __64%__
- [ ] **Test the transactions endpoints** → __64%__
- [ ] **Write the documentation using SWAGGER** → __50%__
- [ ] **Deploy the application on Heroku** → __0%__
- Total Progression → __77%__

__Last commits:__

- I did not add any new features to my app today.

#2023-02-10
---------------------------------------------------------
### Courses achievements !
Daily course achievements goals track.

- [ ] **28. Common Attacks on Web Applications : Securing Acme Bank - Defending Node Applications** → *In progress*
- [x] **29. Fundamentals of Operating Systems : Introduction**
- [x] **29. Fundamentals of Operating Systems : Operating System basics**
- [x] **29. Fundamentals of Operating Systems : Process and Threads**
- [x] **29. Fundamentals of Operating Systems : Process Scheduling**
- [ ] **29. Fundamentals of Operating Systems : Synchronization + Deadlock** → *In progress*
- [ ] **29. Fundamentals of Operating Systems : Memory Managment**
- [ ] **29. Fundamentals of Operating Systems : Files Systems**
- [ ] **29. Fundamentals of Operating Systems : Review**
- Total Progression → __67%__

### Project on going !

__Title:__ Portfolio Project: Personal Budget II

- [x] **Setting up Git tracking** → __100%__
- [x] **Design the database** → __100%__
- [x] **Setup the database** → __100%__
- [x] **Create the tables** → __100%__
- [x] **Connect the database** → __100%__
- [x] **Create your transactions endpoints** → __100%__
- [ ] **Create the transactions** → __72%__
- [ ] **Test the transactions** → __72%__
- [ ] **Test the transactions endpoints** → __72%__
- [ ] **Write the documentation using SWAGGER** → __50%__
- [ ] **Deploy the application on Heroku** → __0%__
- Total Progression → __79%__

__Last commits:__

- "ADD: Implement and test Endpoint for adding a expense record - POST Request." → *Test passed successfully*
- "ADD: Implement and test Endpoint for fecthing a specfific expense record - GET Request." → *Test passed successfully*

### Issues !

__Title:__ Install DB Browser Fails on GitPod

__Tags:__ #GitPod #sqlitebrowser #Install #vscode-sqlite #sqlite3

__vscode-sqlite:__ [link](https://open-vsx.org/extension/alexcvzz/vscode-sqlite)

__Explanation:__

>As part of Codecademy project ["Securing Acme Bank - Defending Node Applications"](https://www.codecademy.com/paths/back-end-engineer-career-path/tracks/becp-22-fundamentals-of-operating-systems/modules/wdcp-22-operating-system-basics/articles/basics-of-operating-systems-article), I need to install "BD Browers" application on GitPod so I can manage a database.
>
>The issue I have encountered is related to the display of GUI applications in Linux. The error message says that the SQLite Database Browser application is using the Qt framework and it is trying to use the X Window System to display its user interface.
>
>However, the X Window System is not available or cannot be connected to, and as a result, the Qt platform plugin "xcb" could not be loaded. The message also says that there are other available platform plugins that could be used, but none of them could be initialized.
>
>The message also suggests that reinstalling the application might solve the problem, but it could also be a result of a more general issue with the X Window System or the display environment.
>
>After trying to fix the issue, I found out that "DB Browser" cannot be installed on GitPod. So, I decided to install "vscode-sqlite" instead, which works well.

#2023-02-13
---------------------------------------------------------
### Courses achievements !
Daily course achievements goals track.

- [x] **28. Common Attacks on Web Applications : Securing Acme Bank - Defending Node Applications**
- [x] **29. Fundamentals of Operating Systems : Synchronization + Deadlock**
- [x] **29. Fundamentals of Operating Systems : Memory Managment**
- [x] **29. Fundamentals of Operating Systems : Files Systems**
- [x] **29. Fundamentals of Operating Systems : Review**
- [ ] **29. Fundamentals of Operating Systems : IO Systems** → *In progress*
- Total Progression → __70%__

### Project on going !

__Title:__ Portfolio Project: Personal Budget II

- [x] **Setting up Git tracking** → __100%__
- [x] **Design the database** → __100%__
- [x] **Setup the database** → __100%__
- [x] **Create the tables** → __100%__
- [x] **Connect the database** → __100%__
- [x] **Create your transactions endpoints** → __100%__
- [ ] **Create the transactions** → __72%__
- [ ] **Test the transactions** → __72%__
- [ ] **Test the transactions endpoints** → __72%__
- [ ] **Write the documentation using SWAGGER** → __50%__
- [ ] **Deploy the application on Heroku** → __0%__
- Total Progression → __79%__

__Last commits:__

- I did not add any new features to my app today.

### Issues !

__Title:__ TypeError: validator.escape is not a function

__Tags:__ #XSS #CommonAttacksOnWeb #express-validator #validator.escape #SecuringAcmeBank #DefendingNodeApplications

__Codecademy video:__ [link](https://youtu.be/d0pWvLyngHM?t=605)

__StackOverflow:__ [link](https://stackoverflow.com/questions/75432493/typeerror-validator-escape-is-not-a-function-express-validator6-12-1-packag/75434130#75434130)

__Explanation:__

>As part of my Codecademy Back-End Engineer training, I have to do a project outside of their platform. The goal of this project is to make sure a node application is protected from common web attacks.
>
>One challenge I faced was securing the code from Cross-Site Scripting (XSS) attacks. To do this, I used a tool called express-validator. The code uses a function called validator.escape which is supposed to protect against any malicious code being inserted into an input form. However, I am getting an error in the console when I try to use it.

Terminal output :
````
TypeError: validator.escape is not a function
    at /workspace/Codecademy-Acme_Bank_Codecademy-Project/app.js:172:29
    at Layer.handle [as handle_request] (/workspace/Codecademy-Acme_Bank_Codecademy-Project/node_modules/express/lib/router/layer.js:95:5)
    at next (/workspace/Codecademy-Acme_Bank_Codecademy-Project/node_modules/express/lib/router/route.js:144:13)
    at Route.dispatch (/workspace/Codecademy-Acme_Bank_Codecademy-Project/node_modules/express/lib/router/route.js:114:3)
    at Layer.handle [as handle_request] (/workspace/Codecademy-Acme_Bank_Codecademy-Project/node_modules/express/lib/router/layer.js:95:5)
    at /workspace/Codecademy-Acme_Bank_Codecademy-Project/node_modules/express/lib/router/index.js:284:15
    at Function.process_params (/workspace/Codecademy-Acme_Bank_Codecademy-Project/node_modules/express/lib/router/index.js:346:12)
    at next (/workspace/Codecademy-Acme_Bank_Codecademy-Project/node_modules/express/lib/router/index.js:280:10)
    at jsonParser (/workspace/Codecademy-Acme_Bank_Codecademy-Project/node_modules/body-parser/lib/types/json.js:101:7)
    at Layer.handle [as handle_request] (/workspace/Codecademy-Acme_Bank_Codecademy-Project/node_modules/express/lib/router/layer.js:95:5)
````
Here is the code :
````
const validator = require("express-validator");

app.post("/public_forum", function (request, response) {
  if (request.session.loggedin) {
    var comment = validator.escape(request.body.comment);
    var username = request.session.username;
    if (comment) {
      db.all(
        `INSERT INTO public_forum (username,message) VALUES ('${username}','${comment}')`,
        (err, rows) => {
          console.log(err);
        }
      );
      db.all(`SELECT username,message FROM public_forum`, (err, rows) => {
        console.log(rows);
        console.log(err);
        response.render("forum", { rows });
      });
    } else {
      db.all(`SELECT username,message FROM public_forum`, (err, rows) => {
        console.log(rows);
        console.log(err);
        response.render("forum", { rows });
      });
    }
    comment = "";
  } else {
    response.redirect("/");
  }
  comment = "";
  //response.end();
});
````

My solution :
````
// This code defines a post request handler for the "/public_forum" endpoint.
app.post('/public_forum', async function (request, response) {
  // Check if the user is logged in by checking the session data.
  if (request.session.loggedin) {
    // Trim and escape the incoming comment.
    await check('comment').trim().escape().run(request);
    // Get the validation result of the incoming comment.
    const errors = validationResult(request);
    // If the validation result contains errors, return a 400 status with the errors in a JSON format.
    if (!errors.isEmpty()) {
      return response.status(400).json({ errors: errors.array() });
    }
    // Get the comment from the request body.
    const { comment } = request.body;
    // If a valid comment exists, insert it into the "public_forum" database table.
    if (comment) {
      db.run(
        `INSERT INTO public_forum (username,message) VALUES (?,?)`, [request.session.username, comment],
        (err) => {
          // If an error occurs while inserting the comment, log the error.
          if (err) {
            console.error(err);
          }
        }
      );
    }
    // Select all the rows from the "public_forum" table.
    db.all(`SELECT username,message FROM public_forum`, (err, rows) => {
      // If an error occurs while selecting the rows, log the error.
      if (err) {
        console.error(err);
      }
      // Log the selected rows.
      console.log(rows);
      // Render the "forum" template, passing in the selected rows as a parameter.
      response.render("forum", { rows });
    });
  } else {
    // If the user is not logged in, redirect them to the homepage.
    response.redirect("/");
  }
});
````
>The method described in the Codecademy video does not exist. It is a mistake. 

#2023-02-14
---------------------------------------------------------
### Courses achievements !
Daily course achievements goals track.

- [x] **29. Fundamentals of Operating Systems : IO Systems**
- [x] **30. Caching and CDNs: Introduction**
- [x] **30. Caching and CDNs**
- [x] **30. Caching and CDNs: Review**
- [x] **31. Scalability: Introduction**
- [x] **31. Scalability**
- [x] **31. Scalability: Review**
- [ ] **32. DevOps Fundamentals: Introduction** → *In progress*
- Total Progression → __72%__

### Project on going !

__Title:__ Portfolio Project: Personal Budget II

- [x] **Setting up Git tracking** → __100%__
- [x] **Design the database** → __100%__
- [x] **Setup the database** → __100%__
- [x] **Create the tables** → __100%__
- [x] **Connect the database** → __100%__
- [x] **Create your transactions endpoints** → __100%__
- [ ] **Create the transactions** → __76%__
- [ ] **Test the transactions** → __76%__
- [ ] **Test the transactions endpoints** → __76%__
- [ ] **Write the documentation using SWAGGER** → __50%__
- [ ] **Deploy the application on Heroku** → __0%__
- Total Progression → __80%__

__Last commits:__

- "ADD: Implement and test Endpoint for deleting a expense record - DELETE Request." → Test passed successfully.
- "ADD: Implement and test Endpoint for updating a expense record - PUT Request." → Test failed

### Issues !

__Title:__ Error: insert or update on table "expenses" violates foreign key constraint "expenses_budget_id_fkey"

__Tags:__ #PostgreSQL #database #foreignkeyconstraint

__Explanation:__

>The failed test indicates that there is an error in updating an expense in the list. The error message indicates that the update violates a foreign key constraint, indicating that the specified budget ID is not present in the `budgets` table. The detail message shows the specific key that is not present in the `budgets` table.
>
>The date must exist in `budgets` table before using it in `expenses` table.

Terminal output :
````
/workspace/-Codecademy-Portfolio-Project-Personal-Budget-2/node_modules/pg-protocol/src/parser.ts:369
      name === 'notice' ? new NoticeMessage(length, messageValue) : new DatabaseError(messageValue, length, name)
                                                                    ^

error: insert or update on table "expenses" violates foreign key constraint "expenses_budget_id_fkey"
    at Parser.parseErrorMessage (/workspace/-Codecademy-Portfolio-Project-Personal-Budget-2/node_modules/pg-protocol/src/parser.ts:369:69)
    at Parser.handlePacket (/workspace/-Codecademy-Portfolio-Project-Personal-Budget-2/node_modules/pg-protocol/src/parser.ts:188:21)
    at Parser.parse (/workspace/-Codecademy-Portfolio-Project-Personal-Budget-2/node_modules/pg-protocol/src/parser.ts:103:30)
    at Socket.<anonymous> (/workspace/-Codecademy-Portfolio-Project-Personal-Budget-2/node_modules/pg-protocol/src/index.ts:7:48)
    at Socket.emit (node:events:513:28)
    at addChunk (node:internal/streams/readable:315:12)
    at readableAddChunk (node:internal/streams/readable:289:9)
    at Socket.Readable.push (node:internal/streams/readable:228:10)
    at TCP.onStreamRead (node:internal/stream_base_commons:190:23) {
  length: 290,
  severity: 'ERROR',
  code: '23503',
  detail: 'Key (budget_id)=(2022-01 Monthly Candy expense) is not present in table "budgets".',
  hint: undefined,
  position: undefined,
  internalPosition: undefined,
  internalQuery: undefined,
  where: undefined,
  schema: 'public',
  table: 'expenses',
  column: undefined,
  dataType: undefined,
  constraint: 'expenses_budget_id_fkey',
  file: 'ri_triggers.c',
  line: '2463',
  routine: 'ri_ReportViolation'
}

  ✘ [fail]: 2.5 PUT /expenses/ulid_id/:ulid_id should update a expense in the list
    ℹ {
        error: 'Error updating expense',
      }
  ─

  2.5 PUT /expenses/ulid_id/:ulid_id should update a expense in the list
  test/expenses/expenses_test.js:114

   113:     // Asserting that the status code of the response is 201
   114:     t.is(res.status, 201);                                  
   115:                                                             

  Difference (- actual, + expected):

  - 500
  + 201

  › test/expenses/expenses_test.js:114:7

  ─

  1 test failed
````

#2023-02-15
---------------------------------------------------------
### Courses achievements !
Daily course achievements goals track.

- [x] **32. DevOps Fundamentals: Introduction**
- [x] **32. DevOps Fundamentals: Culture**
- [ ] **32. DevOps Fundamentals: Infrastructures** → *In progress*
- [ ] **32. DevOps Fundamentals: System Health**
- [ ] **32. DevOps Fundamentals: Processes**
- [x] **32. DevOps Fundamentals: Review**
- Total Progression → __73%__

### Project on going !

__Title:__ Portfolio Project: Personal Budget II

- [x] **Setting up Git tracking** → __100%__
- [x] **Design the database** → __100%__
- [x] **Setup the database** → __100%__
- [x] **Create the tables** → __100%__
- [x] **Connect the database** → __100%__
- [x] **Create your transactions endpoints** → __100%__
- [ ] **Create the transactions** → __76%__
- [ ] **Test the transactions** → __76%__
- [ ] **Test the transactions endpoints** → __76%__
- [ ] **Write the documentation using SWAGGER** → __50%__
- [ ] **Deploy the application on Heroku** → __0%__
- Total Progression → __80%__

__Last commits:__

- I did not add any new features to my app today.


#2023-02-16
---------------------------------------------------------
### Courses achievements !
Daily course achievements goals track.

- [x] **32. DevOps Fundamentals: Infrastructures**
- [x] **32. DevOps Fundamentals: System Health**
- [x] **32. DevOps Fundamentals: Processes**
- [x] **32. DevOps Fundamentals: Review**
- Total Progression → __75%__

### Project on going !

__Title:__ Portfolio Project: Personal Budget II

- [x] **Setting up Git tracking** → __100%__
- [x] **Design the database** → __100%__
- [x] **Setup the database** → __100%__
- [x] **Create the tables** → __100%__
- [x] **Connect the database** → __100%__
- [x] **Create your transactions endpoints** → __100%__
- [ ] **Create the transactions** → __84%__
- [ ] **Test the transactions** → __84%__
- [ ] **Test the transactions endpoints** → __84%__
- [ ] **Write the documentation using SWAGGER** → __50%__
- [ ] **Deploy the application on Heroku** → __0%__
- Total Progression → __82%__

__Last commits:__

- "ADD: Implement and test Endpoint for updating a expense record - PUT Request." → Test passed successfully.
- "ADD: Implement and test Endpoint for fetching all revenues - GET Request." → Tests passed successfully.


#2023-02-17
---------------------------------------------------------
### Courses achievements !
Daily course achievements goals track.

- Total Progression → __75%__

### Project on going !

__Title:__ Portfolio Project: Personal Budget II

- [x] **Setting up Git tracking** → __100%__
- [x] **Design the database** → __100%__
- [x] **Setup the database** → __100%__
- [x] **Create the tables** → __100%__
- [x] **Connect the database** → __100%__
- [x] **Create your transactions endpoints** → __100%__
- [ ] **Create the transactions** → __100%__
- [ ] **Test the transactions** → __100%__
- [ ] **Test the transactions endpoints** → __100%__
- [ ] **Write the documentation using SWAGGER** → __50%__
- [ ] **Deploy the application on Heroku** → __0%__
- Total Progression → __86%__

__Last commits:__

- "ADD: Implement and test Endpoint for adding new revenue records - POST Request." → Test passed successfully.
- "ADD: Implement and test Endpoint for fetching records of a specific revenue - GET Request." → Test passed successfully.
- "ADD: Implement and test Endpoint for deleting a revenue record - DELETE Request." → Test passed successfully.
- "ADD: Implement and test Endpoint for updating records of a specific revenue - PUT Request." → Test passed successfully.
- "DELETE: Remove unnecessary files and helper functions."

### Issues !

__Title:__ "Error adding revenue to PostgreSQL database: value too long for type character varying(20)"

__Tags:__ #PostgreSQL #database #typecharacter 

__Explanation:__

>The error occurred when trying to add new revenue to a PostgreSQL database using a NodeJS server. The error message shows that the value being added to the database is too long for the specified data type "character varying(20)". The error occurred in the file "parser.ts" of the "pg-protocol" module, which is a dependency of the PostgreSQL driver for NodeJS.
>
>The error message also includes details of the PostgreSQL error, which has a code of "22001". This error code is related to a data type mismatch or data value out-of-range error. The error message indicates that the value being added to the database is longer than the specified character limit of 20.
>
>As a result of this error, the test case for adding new revenue to the database has failed, returning a status code of 500 instead of the expected 201.
>
>Here's the query I have to use to change the data type of the description column in the revenues table from VARCHAR(20) to VARCHAR(50):
````
ALTER TABLE revenues ALTER COLUMN description TYPE VARCHAR(50);
````

Terminal output :
````
/workspace/-Codecademy-Portfolio-Project-Personal-Budget-2/node_modules/pg-protocol/src/parser.ts:369
      name === 'notice' ? new NoticeMessage(length, messageValue) : new DatabaseError(messageValue, length, name)
                                                                    ^

error: value too long for type character varying(20)
    at Parser.parseErrorMessage (/workspace/-Codecademy-Portfolio-Project-Personal-Budget-2/node_modules/pg-protocol/src/parser.ts:369:69)
    at Parser.handlePacket (/workspace/-Codecademy-Portfolio-Project-Personal-Budget-2/node_modules/pg-protocol/src/parser.ts:188:21)
    at Parser.parse (/workspace/-Codecademy-Portfolio-Project-Personal-Budget-2/node_modules/pg-protocol/src/parser.ts:103:30)
    at Socket.<anonymous> (/workspace/-Codecademy-Portfolio-Project-Personal-Budget-2/node_modules/pg-protocol/src/index.ts:7:48)
    at Socket.emit (node:events:513:28)
    at addChunk (node:internal/streams/readable:315:12)
    at readableAddChunk (node:internal/streams/readable:289:9)
    at Socket.Readable.push (node:internal/streams/readable:228:10)
    at TCP.onStreamRead (node:internal/stream_base_commons:190:23) {
  length: 98,
  severity: 'ERROR',
  code: '22001',
  detail: undefined,
  hint: undefined,
  position: undefined,
  internalPosition: undefined,
  internalQuery: undefined,
  where: undefined,
  schema: undefined,
  table: undefined,
  column: undefined,
  dataType: undefined,
  constraint: undefined,
  file: 'varchar.c',
  line: '633',
  routine: 'varchar'
}

  ✘ [fail]: 3.3 POST /revenues should add a new revenue to the list
    ℹ {
        error: 'Error adding revenue',
      }
  ─

  3.3 POST /revenues should add a new revenue to the list
  test/revenues/revenues_test.js:48

   47:     // Asserting that the status code of the response is 201
   48:     t.is(res.status, 201);                                  
   49:                                                             

  Difference (- actual, + expected):

  - 500
  + 201

  › test/revenues/revenues_test.js:48:7

  ─

  1 test failed
````



__Title:__ "Express server returning 404 error for valid route when using Thunder Client for API testing"

__Tags:__ #ExpressJS #NodeJS #APItesting #ThunderClient #404Error

__Explanation:__

>The error `Cannot GET /revenues` means that the server received a request for the `/revenues` URL path, but it was unable to find a matching route to handle this request.
>
> In the provided code, the `revenuesRouter` is set up to handle requests with a route of `/`, but it does not have a route to handle `/revenues`.
Since the `apiRouter` has mounted revenuesRouter under the `/revenues` path, any requests to `/api/revenues` will be handled by `revenuesRouter`.
>
>However, if I make a request directly to the `/revenues` path, it will not be matched by any of the routes defined in the `revenuesRouter`, resulting in a `404 error`.To fix the issue, I need to update the route path for revenuesRouter to match the expected path, which is `http://localhost:4001/api/revenues`.
>
>I try to retrieve revenue data for a specific ULID identifier, but I get the full list of revenues records.

Request
````
http://localhost:4001/revenues?ulid_id=01EXBDPV5NM0W5RSMG31WMQM6B
````

Internet page :
````
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Error</title>
  </head>
  <body>
    <pre>Cannot GET /revenues</pre>
  </body>
</html>
````

Expected output :
````
    {
      "ulid_id": "01EXBDPV5NM0W5RSMG31WMQM6B",
      "dt_create": "2021-01-31T05:12:36.789Z",
      "dt_update": "2021-01-31T05:12:36.789Z",
      "dt_value": "2021-01-31T05:12:36.789Z",
      "amount": "1500",
      "description": "salary 2021/01"
    }
````

Terminal output
````
Status: 404 Not Found
````


#2023-02-20
---------------------------------------------------------
### Courses achievements !
Daily course achievements goals track.

- Total Progression → __80%__

### Project on going !

__Title:__ Codecademy project: Photo Caption Contest

>The "Photo Caption Contest" project is a component of the Codecademy Back-End Engineer course, which involves creating a backend for a photo caption contest platform. The project objectives include using Git version control, creating documentation using the Swagger API, implementing a database with PostgreSQL and ORM sequelize, integrating existing API endpoints with the database layer, implementing database transactions, deploying the app using Heroku, and optimizing performance using a localized cache. Prerequisites for this project include familiarity with the command line, Git and GitHub, Javascript, Node.js/Express, Postman, database relationships and configuration, Sequelize, and Heroku.


- [x] **Define Enpoints**
- [x] **Define processus of registration and login**
- Total Progression → __2%__

### Issues !

__Title:__ "Mastering RBAC with Node.js and Sequelize: Key to Successful Project Implementation"

__Tags:__ #RBAC #NodeJS #Sequelize #BackendDevelopment #RoleBasedAccessControl

__Explanation:__

>To complete the project, I must implement RBAC (Role-Based Access Control) with Node.js and Sequelize, an Object-Relational Mapping library. While the project has mentioned these concepts, they have not been fully developed in the Codecademy Back-End Engineer course. Therefore, it is important to thoroughly understand RBAC, Node.js, and Sequelize before beginning the implementation. To ensure the project succeeds, I must master these concepts before moving forward.

#2023-02-21
---------------------------------------------------------

### Courses achievements !
Daily course achievements goals track.

- Total Progression → __80%__

### Project on going !

__Title:__ Codecademy project: Photo Caption Contest

- [x] **Define Enpoints**
- [x] **Define processus of registration and login**
- Total Progression → __2%__

### Issues !

__Title:__ "Mastering RBAC with Node.js and Sequelize: Key to Successful Project Implementation"

__Tags:__ #RBAC #NodeJS #Sequelize #BackendDevelopment #RoleBasedAccessControl

__Explanation:__

>In order to successfully implement RBAC with Node.js, Sequelize and PostgreSQL for the project, it's crucial to have a comprehensive understanding of these concepts, which are not fully covered in the Codecademy course for Back-End Engineers. Here's a plan to learn how to use various libraries :

###Step 1:
>On the first step, I will focus on learning the basics of Sequelize, and PostgreSQL. I will also set up a basic Node.js project and connect it to a PostgreSQL database using Sequelize.

__Topics to cover:__
- Introduction to Sequelize
- Setting up a PostgreSQL database
- Getting Started with Sequelize and PostgreSQL

__Resources:__
- [Sequelize Docs](https://sequelize.org/docs/v6/)
- [PostgreSQL Docs](https://www.postgresql.org/docs/)
- [Getting Started with Sequelize and PostgreSQL](https://youtu.be/p-yKR7GusqM)
- [Node.js Express & PostgreSQL: CRUD Rest APIs example with Sequelize](https://www.bezkoder.com/node-express-sequelize-postgresql/)

__Plan:__
1. Install the required dependencies for the project, including Sequelize and the PostgreSQL driver.
2. Follow the steps in the "Getting Started with Node.js, Sequelize, and PostgreSQL" tutorial to set up a PostgreSQL database and connect it to a Node.js project using Sequelize.
3. Test the connection by creating a simple database query.

###Step 2:
>On the second step, I will focus on implementing RBAC with JWT and Sequelize. I will create a basic user authentication system with JWT and then add RBAC functionality to restrict access to certain routes based on the user's role.

__Topics to cover:__
- Introduction to JSON Web Tokens (JWT)
- Creating a basic user authentication system with JWT
- Adding RBAC functionality to restrict access to certain routes based on the user's role

__Resources:__
- [JWT.io](https://jwt.io/)
- [Node.js JWT Authentication Tutorial](https://www.section.io/engineering-education/how-to-build-authentication-api-with-jwt-token-in-nodejs/)
- [RBAC with Node.js, JWT, and Sequelize](https://medium.com/@michael.svr/node-js-rest-api-with-rbac-jwt-repository-and-mvc-pattern-part-3-648c7b5a4700)

__Plan:__
1. Start by learning about JWT and how it can be used for authentication and authorization.
2. Integrate JWT with your Node.js project and use it for authentication.
3. Implement RBAC with Sequelize by creating a User, Role, and Permission model and their associations as described in the Sequelize Associations resource.
4. Test the RBAC implementation by creating different user roles and trying to access routes that are restricted to certain roles. Verify that the RBAC implementation is working as expected.

###Step 3:
>On the third step, I will focus on refining the RBAC implementation and adding more advanced features. I will also learn about best practices for RBAC and security.

__Topics to cover:__
- Refining the RBAC implementation
- Adding more advanced features, such as dynamic role assignment and resource-based access control
- Best practices for RBAC and security

__Resources:__
- [Building Role-Based Access Control in Node.js with JWT and Sequelize](https://soshace.com/implementing-role-based-access-control-in-a-node-js-application/)
- [Security Best Practices for Node.js]

__Plan:__
1. Start by reading the "Building Role-Based Access Control in Node.js with JWT and Sequelize" tutorial to learn how to refine your RBAC implementation and add more advanced features, such as dynamic role assignment and resource-based access control.
2. Test the RBAC implementation by creating different user roles and trying to access routes that are restricted to certain roles. Verify that the RBAC implementation is working as expected.
3. Follow the "Security Best Practices for Node.js" guide to learn about best practices for securing your Node.js application, including RBAC implementation. 
4. Implement any recommended security measures that are relevant to your project.
5. Review your code and ensure that it follows best practices for security and RBAC implementation.
6. Document your RBAC implementation and security measures for future reference.


#2023-02-23
---------------------------------------------------------

### Courses achievements !
Daily course achievements goals track.

- Total Progression → __80%__

### Project on going !

__Title:__ Codecademy project: Photo Caption Contest

- [x] **Plan the project**
- [x] **Define endpoints**
- [x] **Setup the environment**
- [ ] **Create the models** → *In progress*
- [ ] **Create the controllers**
- [ ] **Create the auth middleware to specific endpoints**
- [ ] **Create the routes**
- [ ] **Test the endpoints**
- [ ] **Configure localized caching**
- [ ] **Write a swagger documentation**
- Total Progression → __15%__

__Last commits:__

- "ADD: .gitpod.yml file with environment setup".
- "SETUP: environment setup".
- "SETUP : environment setup bcrypt jsonwebtoken dotenv".
- "SETUP: environment setup with npx sequelize-cli init".
- "ADD: models/user.js".
- "UPDATE: config/config.json".
- "ADD: create photo.js and user.js".
- "ADD: Create caption.js".
- "Merge remote-tracking branch 'refs/remotes/origin/main'"
- "UPDATE: models".

### Issues !

__Title:__ "PostgreSQL error: relation does not exist, even though table exists in Sequelize migration with uppercase table name"

__Tags:__ #PostgreSQL #Sequelize #migration #tablecase #error

__Explanation:__

>The terminal output shows that a migration script was executed to create a table named 'Users' in the 'database_development' database. However, when attempting to query the table using `SELECT * FROM Users`, the error message "relation 'Users' does not exist" was returned. The same error message was returned when attempting to query the table using `SELECT * FROM users`.
>
>The issue is likely due to the fact that the 'sequelize' ORM (Object-Relational Mapping) tool named the table 'Users' with an uppercase 'U', but PostgreSQL is case-sensitive and expects the table name to be in lowercase letters. Therefore, the table was not found when queried in uppercase or lowercase.
>
>To fix this issue, the migration needs to be undone with the command `npx sequelize-cli db:migrate:undo --name 20230223064615-create-user.js`, and the migration file '20230223064615-create-user.js' needs to be modified to name the table as 'users' instead of 'Users'. Then, the migration needs to be re-run with the command npx sequelize-cli db:migrate to create the 'users' table in the database.

Terminal output :
````
postgres=# \c database_development
You are now connected to database "database_development" as user "postgres".
database_development=# \dt
             List of relations
 Schema |     Name      | Type  |  Owner   
--------+---------------+-------+----------
 public | SequelizeMeta | table | postgres
 public | Users         | table | postgres
(2 rows)

database_development=# SELECT * FROM Users;
ERROR:  relation "users" does not exist
LINE 1: SELECT * FROM Users;
                      ^
database_development=# SELECT * FROM users;
ERROR:  relation "users" does not exist
LINE 1: SELECT * FROM users;
                      ^
database_development=# \dn
 List of schemas
  Name  | Owner  
--------+--------
 public | gitpod
(1 row)

database_development=# \d+
                            List of relations
 Schema |     Name      |   Type   |  Owner   |    Size    | Description 
--------+---------------+----------+----------+------------+-------------
 public | SequelizeMeta | table    | postgres | 8192 bytes | 
 public | Users         | table    | postgres | 8192 bytes | 
 public | Users_id_seq  | sequence | postgres | 8192 bytes | 
(3 rows)
````

### Issues !

__Title:__ "Issue with Sequelize ORM when inserting a new caption record"

__Tags:__ #SequelizeORM #NodeJS #PostgreSQL #Database #InsertionIssue

__StackOverflow:__ [link](https://stackoverflow.com/questions/75544854/issue-with-sequelize-orm-when-inserting-a-new-record-in-table-postgresql)

__Explanation:__

>When I try to insert a new record in the Captions table, the promise returns <pending> and nothing is inserted in the table. However, when I log the returned object, I can see that the Caption object has been created with all the required attributes.

Here is the code I am using to insert the record:
````
const newCaption = await Caption.create({
  ulid_id: 'qdslf,lkqsdnlksvd',
  text: 'djfbsdkjfbqlksjdcnbkqjsdnc'
});

console.log(newCaption);

````
Terminal output :     
````
Promise { <pending> }
Executing (default): INSERT INTO "Captions" ("ulid_id","text","createdAt","updatedAt") VALUES ($1,$2,$3,$4) RETURNING "ulid_id","text","createdAt","updatedAt";
Caption {
  dataValues: {
    ulid_id: 'qdslf,lkqsdnlksvd',
    text: 'djfbsdkjfbqlksjdcnbkqjsdnc',
    updatedAt: 2023-02-23T11:30:16.720Z,
    createdAt: 2023-02-23T11:30:16.720Z
  },
  _previousDataValues: {
    ulid_id: 'qdslf,lkqsdnlksvd',
    text: 'djfbsdkjfbqlksjdcnbkqjsdnc',
    createdAt: 2023-02-23T11:30:16.720Z,
    updatedAt: 2023-02-23T11:30:16.720Z
  },
  uniqno: 1,
  _changed: Set(0) {},
  _options: {
    isNewRecord: true,
    _schema: null,
    _schemaDelimiter: '',
    attributes: undefined,
    include: undefined,
    raw: undefined,
    silent: undefined
  },
  isNewRecord: false
}

````
    
#2023-02-24
---------------------------------------------------------
    
### Courses achievements !
Daily course achievements goals track.

- Total Progression → __80%__

### Project on going !

__Title:__ Codecademy project: Photo Caption Contest

- [x] **Plan the project**
- [x] **Define endpoints**
- [x] **Setup the environment**
- [ ] **Create the models** → *In progress*
- [ ] **Create the seeders**
- [ ] **Create the controllers**
- [ ] **Create the auth middleware to specific endpoints**
- [ ] **Create the routes**
- [ ] **Test the endpoints**
- [ ] **Configure localized caching**
- [ ] **Write a swagger documentation**
- Total Progression → __15%__
    
__Last commits:__
    
- "FIX: Fix verbose - table name". 
- "ADD: Add validation and error handling in Sequelize User model" → Test passed successfully. (implemented bcryt to hash password)
- "ADD: Add validation and error handling in Sequelize Caption model" → Test passed successfully.
- "ADD: Add validation and error handling in Sequelize Photo model" → Test passed successfully.
- "ADD: Add validation and error handling in Sequelize Vote model" → Test passed successfully.
- "FIX: Fix issue with table association between Votes and Users" → Test passed successfully. 
- "ADD: Association of User and Photo models" → Test passed successfully.
- "ADD: Association of Caption and Photo models" → Test passed successfully. 
    
#2023-02-27
---------------------------------------------------------
    
### Codecademy Back-End Engineer courses achievements !
Daily course achievements goals track.

- [ ] *Linear Data structure** → *In progress*
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

- "ADD: Association of Vote and Photo models" → Test passed successfully.
- "FEAT: Create seeders codes for generating random values for the database".

**Happy reporting !**
