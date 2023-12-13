## Description
Can you get the flag? Go to this website and see what you can discover.
### Hint
- How is the password checked on this website?
## Solution
On the website, you can see a login form asking for a username and password, with some text stating that only letters and numbers are allowed. We can test this form using our `admin: password` and see if we can log in but failed. Checking the source code gives us good information that the login form sends the entered username and password to the `login.php` file, which shows the login failed page. Further examination of `login.php` file source code reveals another function that filters input and checks the entered username and password in a function called `checkPassword`. We also have another form that sends data to `admin.php` and a script file called `secure.js`. On the admin page, it says "not authorized," but in the `secure.js` file, we have the `checkPassword` function, which compares our entered username and password to the valid ones. Now, we can log in with the found credentials, and it will redirect us to the flag.
