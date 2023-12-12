## Description
Can you beat the filters? Log in as admin http://jupiter.challenges.picoctf.org:54319/ http://jupiter.challenges.picoctf.org:54319/filter.php

### Hint
* You are not allowed to login with valid credentials.
* Write down the injections you use in case you lose your progress.
* For some filters it may be hard to see the characters, always (always) look at the raw hex in the response.
* sqlite
* If your cookie keeps getting reset, try using a private browser window

## Solution

Upon visiting the URLs provided in the challenge description, the URL `http://jupiter.challenges.picoctf.org:54319/` redirects us to a login page with a heading of `1/5`. The second URL `http://jupiter.challenges.picoctf.org:54319/filter.php` takes us to a page where we encounter `Round 1: or`. Let's begin testing the form using random credentials, such as `admin: pass`. After entering these credentials, we observe a SQL query in the background, which is `SELECT * FROM users WHERE username="admin" and password="password"`. This informs us that the form is using SQL to authenticate user credentials, allowing us to test it for SQL injection. Using burpsuite you can have a better understanding of the application. Let's input `admin' or 1=1 -- ` as the username and `password` as the password. After entering this information, we received `302 found` and a redirection to the same page. Considering all the information in the description, hints, and URLs provided up to this point, we can safely assume that this form has a filter, and the `filter.php` file shows us what is filtered in the backend. We now have all the necessary information to bypass this authentication.

#### Round 1
In this round, the backend is only filtering 'or'. Therefore, we can use payloads that do not contain 'or' to bypass authentication. I am using a basic payload of `' --`, which will end the string and comment out everything after it. As a result, the SQL query will appear as follows.
```
SELECT * FROM users WHERE username="admin" -- " AND password="password"
```
Let's execute this payload in Burp Suite Repeater. The payload successfully bypassed the filter with this payload. You can try other payloads as well but it should not contain `or` in it. After bypassing we are now at round 2 with a message `Congrats! on to round 5`.
#### Round 2 
If you refresh the `filter.php` file now, it will display `Round2: or and like = --`, which means that we cannot use these elements in the payload to bypass the filter of round 2. Consequently, we are not allowed to use comments in our payload. In SQL, we use `;` which is similar to a full stop in English, indicating the end of the query. I am using `';` to bypass the filter, so our SQL query will look like this.
```
SELECT * FROM users WHERE username="admin"; " AND password="password"
```
With the use of this payload, we can bypass the filter.

#### Round 3
In this round, the form is filtering `Round3: or and = like > < --`, which you can see at `filter.php`. Our payload cannot contain any of these characters. In the last round, we used `';`, which is still valid because the filters do not filter for `;`. Therefore, we can use the same payload of round 2 to bypass this round.

#### Round 4
In this round, the form is filtering `Round4: or and = like > < -- admin`. Now we cannot use admin as the username. But in the hint, we can see `sqllite`, which is also not very informative. The form is filtering `admin`, so we cannot pass admin as the input. We need a way to bypass the filter but have the same username in the SQL. After searching for a while, I found a way: `String concatenation`, which means joining two strings using `||` in the query. Let's try this to bypass the filter. So we cannot pass `admin` as the whole word. We can pass `ad` and `min` separately, which gets concatenated once executed in the query. So our payload will be `ad' || 'min';` and our SQL query will look like this: 

```
SELECT * FROM users WHERE username='ad' || 'min'; ' AND password='password' 
``` 
'ad' and 'min' will be joined before getting queried from the database, and it will become `admin`. Using this we can successfully bypass this filter.

#### Round 5
In this round, the form is filtering for 'Round5: or and = like > < -- union admin'. This means that we cannot use any of these characters in the payload. However, in the last round, we used the '||' pipe character to bypass the filter, which is still valid. Therefore, we can use the payload from round 4 to bypass the round 5 filters.


After bypassing 5 rounds, we now have a message that reads, "Congrats! You won! Check out `filter.php`". If we refresh the `filter.php` page now, we can see a PHP script containing the filter script and our flag at the end.
