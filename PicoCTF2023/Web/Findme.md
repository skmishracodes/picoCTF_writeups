#### Description:

Help us test the form by submitting the username as `test` and password as `test!`

#### Objection:

Find the hidden flag in the machine

#### Concepts

*   Encoding/ Decoding
*   Request Analysis
*   Code Inspection

#### Solution:

After launching the machine, we were given a URL to visit. The web page appeared to be a standard login form, with normal source code. We used the provided credentials to log in but were redirected to a new page. Upon analyzing the page source, we realized that the input form did not function, so we needed to try a different approach.

We manually logged in again and paid attention to the URL, which redirected us through several URLs before arriving at the page. Using Burp Suite to analyze the request-response of the machine, we learned more about the redirection process. We noticed that there were two IDs displayed in the URL before reaching the end page.

By selecting the ID in the Burp suite request, the ID was decoded automatically, revealing half of the flag. The second ID provided the remaining flag. Concatenating both IDs, we discovered that they constituted a Base 64 encoding of the flag. We simply decoded the encoding to retrieve our flag.
