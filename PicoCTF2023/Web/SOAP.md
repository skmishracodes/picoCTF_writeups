### Description

The web project was rushed and no security assessment was done. Can you read the /etc/passwd file?

### Objective

Find the flag hidden in the machine.

### Concepts

*   Request-Response Analysis
*   Code Inspection
*   XML External Entity Attack

### Solution

To begin, start up the machine and navigate to the web page provided. The web page appears to be standard, but there is a "detail" button on images that send request to "/data". We can examine the request and response of this form using Burp Suite. Upon inspection, we can see that the request sends its data in XML format, which may make it susceptible to an XML entity attack. To test this theory, we can try using an XML payload to obtain the desired file. By exploiting this vulnerability, we should be able to obtain the flag.
