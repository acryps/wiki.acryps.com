# Database
**Vlquery** uses a database first approach. To keep track of the migrations applied to the database (especially when having multiple instances) version control has to be ensured.

Instead of using a complex database migration framework the migrations are written manually into the codespace. With this approach the complexity of migrations doesn't ever reach any limitations and ultimately is far less time consuming.

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