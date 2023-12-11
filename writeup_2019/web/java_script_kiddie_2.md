
## Description
The image link appears broken... twice as badly... https://jupiter.challenges.picoctf.org/problem/42899 or http://jupiter.challenges.picoctf.org:42899
### Hint
* This is only a JavaScript problem.
## Solution
This challenge is very similar to the `JavaScript kiddie` one. However, if you take a closer look, there is a minor difference in the script of this challenge. Notice that the key is 32 digits long, and the shifter is slicing every second value of the key. Therefore, at the end, it's a 16-digit code containing 32 digits, and every second value is just a filter value that can be anything.

We need to make two modifications to the script.
#### Frist change:
Modify the code in the main function.
```
before:
	shifter = int(key[i])
after:
	shifter = int(key[i*2:i*2+1])
```
because we need to remove next value from the key.

#### Second change:
Add a filler value after each digit of the key in the main for loop where we are creating keys for our main function.
```
before:
	for p in itertools.product(*shifters):
   	 	key = "".join("{}".format(n) for n in p)
   	 	create_png(bytes_arr, key, out_dir_path)
after:
	for p in itertools.product(*shifters):
   		key = "".join("{}a".format(n) for n in p)  # add "a" after every digit which will be remove in the main function while converting it into interger.
		create_png(bytes_arr, key, out_dir_path)
```

You can follow the exact same steps to create a valid PNG image from the script which creats a QR code. After that, you can use either the `zbarimg` or your phone to extract the text from it.
