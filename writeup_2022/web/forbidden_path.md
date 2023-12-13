## Description
Can you get the flag? Here's the website. We know that the website files live in `/usr/share/nginx/html/` and the flag is at `/flag.txt` but the website is filtering absolute file paths. Can you get past the filter to read the flag?
### Hint
* Not Hints
## Solution
When visiting this web application, we can see an input field where we can input a file name, and the application will retrieve the content of the file for us. According to the description, we cannot use the absolute path of the file, and our flag is located at "/flag.txt". We may try path traversal attacks to change our directory.

However, let's first try exactly what it does on entering the filename and path. If we enter "/flag.txt", the response is "Not Authorized", and entering just "flag.txt" gives the response "File doesn't exist." Upon trying path traversal attacks such as "/../../../", we find that they do not work. But, in the page source code, we can see that the form is getting submitted at the "read.php" file. If we try reading that file, we can see a 200 response with the content of the file. In the code of the file, we can see that the script is filtering "/" at the start of the flag, so we cannot use "/" in the file path at the beginning. Therefore, if we try "../../../../flag.txt" without "/" at the start, we can read the flag.
