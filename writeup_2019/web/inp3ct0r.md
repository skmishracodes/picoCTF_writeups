## Description
Kishor Balan tipped us off that the following code may need inspection: https://jupiter.challenges.picoctf.org/problem/41511/ (link) or http://jupiter.challenges.picoctf.org:41511

### Hint
- How do you inspect web code on a browser?
- There's 3 parts
## Solution
When you visit the website, you'll see two buttons labeled "What" and "How". When you click on "What", a message appears saying "I made a website". Clicking on "How" will show you the message "I used these to make this site: HTML, CSS, JS (JavaScript)". If you check the page source code, you'll find the first part of the flag in a comment. The flag has three parts. There are also two file links in the page source code that we have to proceed. By checking the CSS file link provided in the header tag of the page source code, we can find the second part of the flag. Similarly, by checking the JavaScript file, we can find the third part of the flag.
