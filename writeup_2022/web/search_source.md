## Description
The developer of this website mistakenly left an important artifact in the website source, can you find it? The website is here
### Hint
- How could you mirror the website on your local machine so you could use more powerful tools for searching?
## Solution
This website only has a landing page, but there are many files in the source code. According to a hint, we can mirror the website to our local machine. I'm using `wget -m "target_url"` to perform this. This allows us to search for the flag using local tools. Our objective is to find a flag that is located in one of the directories or files. To do that, we can use the command `grep -lir picoCTF` to search for the string "picoCTF" in every file and directory of the mirrored website directory and print the path to the console. This command will quickly return the location of our flag, which is in the `css/style.css` file. You can either manually look for the flag in this file, or use a combined command to print the flag. To print the flag, use `cat style.css | grep picoCTF`. This command will print the entire line containing the matching text.
