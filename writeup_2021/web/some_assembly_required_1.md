## Description
http://mercury.picoctf.net:15472/index.html
### Hint
- No hints
## Solution
At the website, you will come across a text box where you can input a flag. After inspecting the page source, we are left with a link to a JavaScript file. The file initially appears to be a string of hexadecimal code, but upon closer inspection, it reveals another URL. The URL can be found after the text "Incorrect!" and has the path "./pathname". If you append this path to the website's URL, you will discover the challenge's flag.
