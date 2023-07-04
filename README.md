# CICD_kittygram
The workflow was build using github actions checkouts, for example:
### Tests
- Trigger: This job is triggered whenever there is a push to the main branch.
- Runs on: Ubuntu latest
- Services: This job runs a PostgreSQL service using the postgres:13.10 image.
- Steps:
* Checks out the repository using actions/checkout@v3.
* Sets up Python using actions/setup-python@v4 and installs the required dependencies.
* Runs flake8 linting and Django tests to ensure the application is functioning correctly.
