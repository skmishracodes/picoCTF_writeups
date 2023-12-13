## Description
The flag is somewhere on this web application not necessarily on the website. Find it. Check this out.
### Hint
- No Hints
## Solution
Upon visiting the website, we can see a landing page. According to the description, we know that the flag is on the web app but not on the website. But to make sure, we can check the source code of the website. There is nothing. But if we notice the challenge name "Roboto sans," it makes no sense except it points towards something. We can check everything on the website, but there is no clue. Maybe "Roboto sans" is pointing toward the "robots" file of the web app. If we check for "robots.txt," it is there and contains a few paths and a random encrypted text. If we try to decode that encrypted text, we can see a few more paths like "flag1.txt, js/myfi, js/myfile.txt." Upon checking these paths, we can see that our flag is in "js/myfile.txt."
