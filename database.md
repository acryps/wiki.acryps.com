# Database
## Environments
There are three commonly used environments.

| | |
:-- | :--
Development | Local instance for development (one for each developer)
Test | Hosted instance to emulate productive instance to ensure correct interface integration before release
Productive | Hosted instance for official product used by clients

### Usage depending on scope
In the early prototyping stage of development without official releases, multiple environments aren't necessary and only slows down development.

But as soon as the scope expands, multiple developers need different versions of the database or at the latest when an official release is dropped these three environments **must** be created.

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
**Vlquery** uses a database first approach. To keep track of the migrations applied to the database (especially when having multiple instances) version control has to be ensured.

Instead of using a complex database migration framework the migrations are written manually into the codespace. With this approach the complexity of migrations doesn't ever reach any limitations and ultimately is far less time consuming.

### File structure
1. Create a folder named `database` in the root of your project.
2. The first migration file is **always** named `0-initial.sql` and creates the first version of the database
3. Further changes to the database are written into new files named `{index}-{tag}.sql`. The index is incremented for each file to keep the correct order of the scripts. The tag should be a short, clear description of what the script is doing. They assemble the commit message but without the `Add` or `Fix` keywords.
	- 0-initial.sql
	- 1-book-state.sql
	- 2-book-reservation.sql
4. If needed create a seed data folder named `seed` inside the `database` folder. Seed data fills the database with data that is crucial for the application to work. For example (available, rented, reserved) states have to be added to the book state table. The file with the data should be named `{index}-{tag}.sql`. The index matches the migration index where the seed script works with the database version. The tag again is a short, clear description for the type of seed data.

The final structure could look like this:

> database
>> seed
>>> 1-book-state.sql
>>
>> 0-initial.sql<br>
>> 1-book-state.sql<br>
>> 2-book-reservation.sql