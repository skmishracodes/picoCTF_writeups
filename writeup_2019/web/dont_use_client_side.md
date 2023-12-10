## Description
Can you break into this super secure portal? https://jupiter.challenges.picoctf.org/problem/37821/ (link) or http://jupiter.challenges.picoctf.org:37821

### Hint
- Never trust the client
## Solution
Upon visiting the challenges, you will notice an input field that asks for valid credentials. If we test this field by entering random values, a message pops up stating "incorrect password". Upon checking the source code, we can see a program that contains our flag, but it is split into different parts. After analyzing the function, we can understand that it is checking if the input is a valid flag. We can get our flag by rearranging the pattern of splitting in the function and then verifying it using the input field to check if our flag is valid or not.
