### Description

How about trying to match a regular expression

### Objective

Find the flag hidden in the machine.

### Concepts

*   Regular expression
*   Code Inspection

### Solution

Once the machine is launched, a URL is provided to access an input field for validation. Examining the page's source code reveals the function responsible for validating input. Interestingly, the function contains a comment with a regular expression "^p…..F!?" which is a 7-letter word starting with lowercase p and ending with uppercase F. I tried  "picoCTF" into the field and  able to successfully obtain the flag.
