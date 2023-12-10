## Description
The factory is hiding things from all of its users. Can you login as Joe and find what they've been looking at? https://jupiter.challenges.picoctf.org/problem/13594/ (link) or http://jupiter.challenges.picoctf.org:13594
### Hint
- Hmm it doesn't seem to check anyone's password, except for Joe's?
## Solution
On accessing the website, we come across a login page. By using `test:test` on the login page, we are able to login successfully and are directed to a page that displays a message saying "Success: You logged in! Not sure you'll be able to see the flag though.". After several attempts with different username and password combinations, we realize that we can log in with any username and password. Unfortunately, checking the source code of the page does not provide any useful information. However, we can examine the cookie of the page after logging in. The cookies are updated and three values are added - "username", "password", and "admin". The values of "username" and "password" are those provided on the login page and the value of "admin" is set to false. By changing the value of "admin" to "True" and reloading the page, we are able to obtain our flag.
