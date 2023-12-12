Description
Who doesn't love cookies? Try to figure out the best one. http://mercury.picoctf.net:21485/
### Hint
* No Hints
## Solution
Upon visiting the website in this challenge, a greeting message and a search bar are visible. If something random is entered into the search bar, an invalid cookie message pops up. Checking the page source code does not provide any informative details. From the name of the challenge, we can get a vague idea that the challenge revolves around the session cookies of the website. Let's inspect them and see what we can find. Upon looking at the cookies, a cookie with a value of "-1" is present. Let's test it by double-clicking on the value and changing it to something else. If we put a value other than -1, such as 0, the homepage changes and shows a different message. Now let's change 0 to 1 and reload the website the message changes again. Thus, we know that we can obtain our flag using this method. 

Let's test the upper and lower limits. For the upper limit test, we can enter different values, and at the end, we find that the upper limit of the cookie is 28. For the lower limit, we can enter random values, and we found that the lower limit is -2, which shows the search page the same as -1. Now that we know the upper and lower limits, we can conclude that our flag is between these values. You can now use Burp Suite Intruder to brute-force the cookie and find the flag.
