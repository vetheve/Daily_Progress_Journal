Daily Progress Journal
======================

"Tracking My Progress: Daily Journaling to Achieve Goals"


[2023-02-03](#2023-02-03)

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

Requête - [[1]](https://github.com/vetheve/-Codecademy-Portfolio-Project-Personal-Budget-2/blob/main/server/budget_balance.js)
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
Test avec AVA - [[2]](https://github.com/vetheve/-Codecademy-Portfolio-Project-Personal-Budget-2/blob/main/test/balance/budget_balance_test.js)
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

**Happy reporting !**
