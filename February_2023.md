Daily Progress Journal
======================

"Tracking My Progress: Daily Journaling to Achieve Goals"

* **February 2023**

|Mon  |Tue  |Wed  |Thu  |Fri  |Sat  |Sun  |
|---:|---:|---:|---:|---:|---:|---:|
|     |     |1    |2    |[3](#2023-02-03)    |4    |5    |
|[6](#2023-02-06)    |[7](#2023-02-07)    |[8](#2023-02-08)     |[9](#2023-02-09)   |[10](#2023-02-10)   |11   |12   |
|[13](#2023-02-13)   |[14](#2023-02-14)   |15   |16   |17   |18   |19   |
|20   |21   |22   |23   |24   |25   |26   |
|27   |28   |     |     |     |     |     |



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
>But I still need to figure out why the solution given by Codecademy does not work. 

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
- [ ] **Create the transactions** → __72%__
- [ ] **Test the transactions** → __72%__
- [ ] **Test the transactions endpoints** → __72%__
- [ ] **Write the documentation using SWAGGER** → __50%__
- [ ] **Deploy the application on Heroku** → __0%__
- Total Progression → __79%__

__Last commits:__

- I did not add any new features to my app today.

**Happy reporting !**
