## Description
Can you login to this website?
### Hint
- admin is the user you want to login as.
## Solution
Upon visiting the website, we can see a simple login form. We can test the form using the simple `admin:password` credentials, which responds with an SQL query that is executed for authentication, and a message `login failed`. Now, we know that we can try using SQL injection in the form. I am using a simple `'--` payload to bypass. After trying to execute the payload, we see a message `Logged in! But can you see the flag, it is in plain sight.` and an SQL query. On checking the source code, we can see our flag.
