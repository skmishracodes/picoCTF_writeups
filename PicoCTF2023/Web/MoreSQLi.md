### Description

Can you find the flag on this website.

### Objective

Find the flag hidden in the machine.

### Concepts

*   SQL injection
*   Request-Response Analysis

### Solution

After launching the machine we can visit the URL and Its a login page. From the title of the machine we know that we need to exploit SQL injection vulnerability at some point in this machine so lets try bypassing this page using SQL injection. First lets test the page by enter random username and password. On Login with random credentials it redirect us to a page which show the SQL query for the authentication. After looking at this we can have a better understanding of the SQL attack now. Open Burp suite and try simple SQL Injection payloads in the login for e.g:- ' or 1=1 -- . The username field is not vulnerable to SQL injection because we are unable to see any difference after try few different payloads of different SQL databases. But when we test the password field we can get our flag in the response of the request.
