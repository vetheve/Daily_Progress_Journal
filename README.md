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
- Total Progression → __60%__

### Project on going !

__Title:__ Portfolio Project: Personal Budget II

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

Requête
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
Test avec AVA
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

Ideas, suggestions, enquiries for complementary information or requests for the allocation of additional resources.

**Happy reporting !**
