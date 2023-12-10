## Description
This website can be rendered only by picobrowser, go and catch the flag! https://jupiter.challenges.picoctf.org/problem/26704/ (link) or http://jupiter.challenges.picoctf.org:26704
### Hint
- You don't need to download a new web browser
## Solution
Upon visiting the website URL, we see a homepage containing a button flag. Upon clicking the button, a message pops up saying "You're not picobrowser! {BROWSER_DETAILS}". According to the hint, we don't need to install a new browser or something, which means we need to switch the user-agent in the request. I am using a user-agent switcher extension, but it can also be done using Burp Suite or ZAP. So, I tried changing my browser to `PicoBrowser` and refreshed the tab, and now the message says "You're not picoBrowser! PicoBrowser". We are still getting an error, but if you notice, in the error, it's saying "you're not `picobrowser! {your-browser}`". So, let's try adding `picobrowser!` in front of our user agent and after changing the user-agent to `picobrowser! {browser_details}`, we are able to get our flag.
