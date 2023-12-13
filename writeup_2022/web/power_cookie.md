## Description
Can you get the flag? Go to this website and see what you can discover.
### Hint
* Do you know how to modify cookies?
## Solution
Upon visiting the web application, we can see a button to "continue as a guest". If we click on the button, it redirects us to "/check.php" and shows the message "We apologize, but we have no guest services at the moment." In the home page source, we can see the "continueAsGuest()" function getting executed on clicking "Continue as guest" button, and a script 'guest.js' on checking the script we can see that there is a simple function which is taking us to "/check.php" and setting "isAdmin" in the cookie equals to "0". Now we know how we can proceed further. If we change "isAdmin" from "0" to "1" and refresh "/check.php", we can see our flag.
