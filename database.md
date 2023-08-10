# Database
## Environments
There are three commonly used environments.
Production may be used initially, once a product is live, breaking changes must be made on another instance.
If multiple people work on the same project in different branches and database changes are made, multiple instances must be created.

| | |
:-- | :--
Development | Local instance for development (one for each developer)
Test | Hosted instance to emulate productive instance to ensure correct interface integration before release
Productive | Hosted instance for official product used by clients

### Connection naming constraints
For each instance of the application a separate user login is created that specifically is the owner of this database.

| | |
:-- | :--
host | localhost or hosting domain (example.com)
database | {application name}_{instance}
user | {application name}_{instance}
password | {application name}_{instance}

The exception is the development instance, where the instance type can be ignored. This results into the following names:
- application_productive
- application_test
- application

> 💡 Give each instance in any database-management-client a clear and striking background **tint** to minimize accidents. (Make changes on the productive instance)

## Migrations
**@acryps/query** uses a database first approach. To keep track of the migrations applied to the database (especially when having multiple instances) version control has to be ensured.

Database changes are made in SQL scripts in the `database` directory of a project.
The are numbered, starting with `1-initial.sql`
They must be sequentially executeable, use `ALTER` instead of dropping & recreating.

## Seed/Example Data
Seed data is data which is `required` for the application to work. Not just any values, but the **exact values used within them** (Example: Genesis Block in a blockchain).
Example/testing data may be `required` for the application to work, but it could also contain other values (Example: 'Silver' Material in Ringbaker, for all we know it could be steel too).

Example data should **not** be data usually used in the application and should cover as many cases as possible (Example: Create a 'Steel' material instead of 'Silver' to test).

Seed data must be directly embedded within the scripts in `database/*.sql`.
Example data can be stored sequentially with a number prefix in `database/example/*.sql`.