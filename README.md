We are building service that allows users to withdrawal some amount using selected payment method (e.q. bank account) with the business rules:

- We have a list of users (`/v1/users` endpoint)
- A user has several payment methods
- A user can execute a withdrawal request using one of a payment methods. A request must contain one or more withdrawals following the rules:
    - Withdrawals count must not exceed value of `maxWithdrawals` field
    - Sum of all withdrawals must not exceed value of `maxWithdrawalAmount`
    - Every withdrawal in the request  can be executed immediately (set `executeAt` as now) or scheduled to be executed in future within the current month (set `executeAt` to future date). The field value is expected to be in UTC

How the withdrawal processing works:

- After accepting a request the service creates and stores items with status `PENDING` in DB
- There is a worker that runs every n time (5 seconds by default) and send all `PENDING` withdrawals before current timestamp to processing
- For this test "happy path" is implemented only, so every withdrawal will be updated with status `SUCESSS`

### The challenge:

- Fork the repository
- Run the app using `docker-compose up`
- The service will be running on port `7070`. There is swagger available by the address: `http://localhost:7070/swagger-ui.html`
- The service is using embedded H2 database by default. If needed you can enable mysql (uncomment related lines in docker-compose)
- Once complete invite `makcon` and `pbravowezaam`

We expect from you to write automated tests with following acceptance criteria:

- To be written on any language using any frameworks you are comfortable with
- All visible problems should be detected and covered by automation tests
- Immediate withdrawal processing should be tested
- We would like to see a possible solutions how to test scheduled withdrawals to be executed in a future (e.q. next day)
- Also, we would like to know the ways to test failed flow. Withdrawal object has 2 error statuses:
    - `INTERNAL_ERROR` - in case of unexpected technical happened (e.q. 3rd party payments provider is unavailable)
    - `FAILED` - related to predictable issues with payment methods (e.q. the user's bank account is blocked)
- It would be good if we could easily run the tests (e.q. with docker-compose) and see a generated test report (e.q. Serenity framework report). Please provide an instructuion
