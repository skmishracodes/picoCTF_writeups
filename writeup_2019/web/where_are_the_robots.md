## Description
Can you find the robots? https://jupiter.challenges.picoctf.org/problem/36474/ (link) or http://jupiter.challenges.picoctf.org:36474

### Hint
- What part of the website could tell you where the creator doesn't want you to look?
## Solution
On the website, there is a message asking "Where are the robots". From this message, we can have an idea that this may be referring to the 'robots.txt' file. After inspecting the page source, we found nothing. However, upon checking the "robots.txt" file, we discovered another HTML file path. By appending the path and visiting the page, we were able to obtain the flag for the challenge.
