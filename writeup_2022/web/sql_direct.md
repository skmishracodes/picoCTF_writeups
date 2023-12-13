## Description
Connect to this PostgreSQL server and find the flag!
Additional details will be available after launching your challenge instance.
### Hint
- What does a SQL database contain?
## Solution

After connecting to the database using the provided credentials through `psql`, we were able to successfully establish a connection to the database named pico. To verify the tables, we ran the command `\dt`, which lists four tables i.e. `public`, `flags`, `table`, and `postgres`. By attempting to access the contents of the `flags` table, we were able to retrieve our flag.
