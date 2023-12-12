## Description
Let me in. Let me iiiiiiinnnnnnnnnnnnnnnnnnnn http://mercury.picoctf.net:52362/

### Hint
- It ain't much, but it's an RFC https://tools.ietf.org/html/rfc2616
## Solution
Visiting the challenge prompts us with a message stating "The website can only be accessed using an official PicoBrowser." To get the flag, use header manipulation. First, capture the request using Burp Suite and send it to the repeater. Next, change the `User-Agent` header to "PicoBrowser" and send the request. You can refer to the RFC provided to figure out the header tags or google "List of request header" and read about them on wiki. As you proceed, manipulate the request with different headers such as `Referer`, `Date`, `DNT`, `X-Forwarded-For`, and `Accept-Language` to find the appropriate tag for the challenge you face in the path."
