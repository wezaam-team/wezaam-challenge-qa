																Wezaam qa challenge
													
The purpose of this challenge is to evaluate your testing automation skills. The challenge consist of two different exercises about both UI and API testing automation.

### Requirements
	•	Any programing language can be used, although Java is a plus.
	•	Any framework/tool can be used.
	•	The use of design patterns is a plus. If implement any, please explain them.
	•	The solution must be platform agnostic.
	•	The solution must include test execution report.
	•	Add a README.md file at the project root with instruction to build the project and run the tests.
	•	All the software required to build and run the project should be included in the project.
	•	Once finished send us a mail and attach the solution as a single archive.


	
### Exercise 1: API automation

	The exercise consists of writing automation test to validate the withdraw API of Wezaam.

	# Description
	
		We are building service that allows users to withdrawal (the process that allows to transfer money from company to employee accounts) some amount using selected payment method (e.q. bank account) with the business rules:

		- We have a list of users (`/v1/users` endpoint)
		- A user has several payment methods
		- A user can execute a withdrawal request using one of a payment methods. A request must contain one or more withdrawals following the rules:
			- Withdrawals count must not exceed value of `maxWithdrawals` field
			- Sum of all withdrawals must not exceed value of `maxWithdrawalAmount`
			- Every withdrawal in the request can be executed immediately (set `executeAt` as now) or scheduled to be executed in future within the current month (set `executeAt` to future date). The field value is expected to be in UTC

		How the withdrawal processing works:

		- After accepting a request, the service creates and stores items with status `PENDING` in DB
		- There is a worker that runs every n time (5 seconds by default) and send all `PENDING` withdrawals before current timestamp to processing
		- For this test "happy path" is implemented only, so every withdrawal will be updated with status `SUCESSS`

	# The challenge:
	
		- Fork the repository
		- Run the app using `docker-compose up`
		- The service will be running on port `7070`. There is swagger available by the address: `http://localhost:7070/swagger-ui.html`
		- The service is using embedded H2 database by default. If needed you can enable mysql (uncomment related lines in docker-compose)
		- Detect all visible problems and cover them by automation tests
		- Automate the immediate withdrawal processing


### Exercise 2: UI automation

	This exercise is about writing automated tests to validate a feature from UI point of view.

	# Description
	
	Visit Facebook page and validate the login view functionality: https://www.facebook.com.

	# The challenge:
	
		- Define the three most valuable test cases from your point of view. Please explain your choice.
		- Automate two of them. Please justify your choice.

