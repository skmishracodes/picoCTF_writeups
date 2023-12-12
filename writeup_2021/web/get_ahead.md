## Description
Find the flag being held on this server to get ahead of the competition http://mercury.picoctf.net:15931/
### Hint
- Maybe you have more than 2 choices
- Check out tools like Burpsuite to modify your requests and look at the responses
## Solution
In this challenge, upon visiting the provided URL, you will see two buttons to choose colors. If you click on red, the background color changes to red. Similarly, if you click on blue, the color changes to blue. Upon inspecting the page source, we can see that there are two forms - the red button with the GET method and the blue button with the POST method. Now that we know the website makes different requests to the endpoint to make changes, let's test if there are any other methods allowed. In the hint, it is mentioned that there are more than two options, and if we make changes to the request using tools like burpsuite and zap, we can get the flag. 

To do this, open Burp Suite Proxy, send the request to the Repeater, and change the method to PUT, DELETE, OPTIONS, PATCH, and more. However, there is no result. Upon sending the request with the HEAD method, we get our flag. 
