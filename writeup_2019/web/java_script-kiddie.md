
## Description
The image link appears broken... https://jupiter.challenges.picoctf.org/problem/58112 or http://jupiter.challenges.picoctf.org:58112.
### Hint
- This is only a JavaScript problem.
## Solution
Upon visiting the website, we can see an input area where we need to enter something. However, we don't know what we need to enter. Testing this field with simple text returns nothing except a broken image. Checking the source code gives us a better understanding of the input and the broken image. If you pay attention and read the JavaScript, you can understand that the script takes an input of 16 numbers (how we can say 16 numbers because of ` key.charCodeAt(i) - 48;` it converts it into numbers) and then arranges the bytes based on the input to create a PNG image. If you capture the request-response, you can see the bytes being fetched and used in the `assembly_png()` function. We can try to brute force this input to get a valid PNG but the possibility is `**10,000,000,000,000,000**`. Now, we can try to recreate the image by rearranging the bytes. However, we don't know which bytes to move to create a valid image. If you know about PNGs, you may know that the first 16 bytes of a PNG image never change because they are the header bytes. The first 8 bytes are the identifier bytes, and the second 8 bytes are `IHDR` bytes. You can read about PNGs and their headers and signatures on the internet. Now we know that the first 16 bytes of data will look like what. To recreate the image, we need to rearrange the bytes to make a valid PNG file, and its first 16 bytes should match the default bytes. We can write a script to perform this step. I am using Python and a few other libraries to complete this step.
## Script development:

- Before developing this script, we need to understand its basic needs. Generate random keys containing 16 digits.
- shift the bytes according to the key, and create an image. 
- Compare if the first 16 bytes are matching or not.
-  Is the generated image a valid PNG image?

### Import Libraries:
* We need to check our PNG Image is valid or not.
```
from PIL import Image
```

* We need io: To convert the shifted number list into bytes, os: to define output file path (optional), and itertools: to perform iteration and key combination from.
```
import os, io, itertools
```
### Default Variables:

- Output directory.

```
out_dir_path = "file_path_where_you_want_to_save"
```

- Exepected Array

```
expected = [0x89, 0x50, 0x4E, 0x47, 0x0D, 0x0A, 0x1A, 0x0A, 0x00, 0x00, 0x00, 0x0D, 0x49, 0x48, 0x44, 0x52]
```

- Key length

```
KEY_LEN = 16
```

- Store the bytes in a file called `bytes.txt` and then read the file and create a list of number from the `bytes.txt` file.

```
# Open the bytes.txt file
with open("bytes.txt") as f:
# Split every digit from the file and convert it into an interger 
# Then store it inside a list.
    bytes_arr = list(map(int, f.read().split()))
```

### Generate keys:
- Create a list containing 16 empty list inside to store values.
```
shifters = [[] for _ in range(KEY_LEN)]
# result: [[], [], [], [], [], [], [], []....]
```

- Loop to determine valid shifter values for each position i in the shifters list.
```
for i in range(KEY_LEN):
    for shifter in range(10):
        j = 0
        offset = (((j + shifter) * KEY_LEN) % len(bytes_arr)) + i
        if bytes_arr[offset] == expected[i]:
            shifters[i].append(shifter)
```

**Outer Loop (for i in range(KEY_LEN):):**
- This loop iterates over the positions i in the expected list, where KEY_LEN is the length of the key.

**Inner Loop (for shifter in range(10):):**
- This loop iterates over possible shifter values ranging from 0 to 9.

**Offset Calculation:**
- The offset is calculated using the formula: (((j + shifter) * KEY_LEN) % len(bytes_arr)) + i
- j is set to 0 in each iteration.
- The shifter value is used to introduce a shifting mechanism.
- KEY_LEN is used in the calculation.
- The result is wrapped around using modulo (%) to ensure it stays within the bounds of the bytes_arr array.
- The final i is added to the offset.

**Comparison:**
- It checks if the byte at the calculated offset in bytes_arr matches the expected byte at position i.
- If the bytes match, it means the current shifter value is a valid one for the current position i.

**Appending Valid Shifters:**
- If the condition is met, the current shifter value is appended to the list at position i in the shifters list.


### Write a function to create valid PNG image:
- Main function:

```
def create_png(bytes_arr, key, out_dir_path):
    result = [0] * len(bytes_arr)
    for i in range(KEY_LEN):
        shifter = int(key[i])
        for j in range(len(bytes_arr) // KEY_LEN):
            result[(j * KEY_LEN) + i] = bytes_arr[(((j + shifter) * KEY_LEN) % len(bytes_arr)) + i]
    img_bytes = io.BytesIO(bytes(result))

    try:
        img = Image.open(img_bytes)
        img.save(os.path.join(out_dir_path, f"{key}.png"))
        print(f"KEY:{key} produces a valid PNG - Saving")
    except:
        print(f"KEY:{key} produces a invalid png - Ignoring")
```

**Initialization of Result List:**
- result = [0] * len(bytes_arr): Initializes a list of zeros with a length equal to the length of bytes_arr. This list (result) will be used to store rearranged bytes.

**Loop Over Key Positions:**
- for i in range(KEY_LEN):: Iterates over positions in the key, where KEY_LEN is assumed to be a constant representing the length of the key.

**Conversion of Character to Shifter:**
- shifter = int(key[i]): Converts the character at position i in the key to an integer. This value is used as a shifter in the byte rearrangement.

**Double Loop for Byte Rearrangement:**
- Nested loop for j in range(len(bytes_arr) // KEY_LEN): iterates over chunks of bytes_arr based on KEY_LEN.
- Bytes are rearranged based on the shifter value and the key, and the result is stored in the result list.

**Conversion to Image and Saving:**
- img_bytes = io.BytesIO(bytes(result)): Converts the result list to bytes using BytesIO. This is necessary for creating a PIL Image object.
- img = Image.open(img_bytes): Attempts to open the image using PIL. To check whether it's a valid image or not.
- img.save(os.path.join(out_dir_path, f"{key}.png")): Saves the image to the specified output directory with the key as the filename.

**Exception Handling:**
- The function includes a try-except block to catch any exceptions that may occur during image processing. If an exception occurs, it prints an error message indicating that the key produces an invalid PNG.

### Create keys and call the function to generate image.

```
for p in itertools.product(*shifters):
    key = "".join("{}".format(n) for n in p)
    create_png(bytes_arr, key, out_dir_path)
```

**itertools.product(*shifters):**
- itertools.product is used to generate the Cartesian product of the elements in shifters.
- The *shifters syntax is used to unpack the list of lists into separate arguments for itertools.product.
- This generates all possible combinations of shifter values, where each element in the resulting tuple represents a shifter value for a specific position in the key.

**for p in itertools.product(...):**
- Iterates over each combination generated by itertools.product.

**key = "".join("{}".format(n) for n in p):**
- Converts the tuple p to a string key.
- It iterates over each element n in the tuple, converts it to a string, and joins the strings together to form the key.
- 
**create_png(bytes_arr, key, out_dir_path):**
- Calls the create_png function with the generated key, creating a PNG image based on the bytes in bytes_arr and saving it to the specified output directory.

### FINISHED SCRIPT
```
import io, os, itertools
from PIL import Image

# output directory 
out_dir_path = input("Output Directory path: ")

# Length of the keys required
KEY_LEN = 16

# create a list consisting 16 empty list result: [[], [], [], [], [], [], [], []....]
shifters = [[] for _ in range(KEY_LEN)]

# expected ouput file header
expected = [0x89, 0x50, 0x4E, 0x47, 0x0D, 0x0A, 0x1A, 0x0A, 0x00, 0x00, 0x00, 0x0D, 0x49, 0x48, 0x44, 0x52]

# Bytes of data. Read bytes from bytes.tx file.
with open("bytes.txt") as f:
    # create a list by reading the bytes from the file spliting every number after space, convert the splitted number into interger and save it inside the list. 
    bytes_arr = list(map(int, f.read().split()))
    
for i in range(KEY_LEN):
    for shifter in range(10):
        j = 0
        # Add 0 + current shifter value * 16 % length of bytes_arr and then add current value of i and store it in offset.
        offset = (((j + shifter) * KEY_LEN) % len(bytes_arr)) + i
        if bytes_arr[offset] == expected[i]:
            shifters[i].append(shifter)

def create_png(bytes_arr, key, out_dir_path):
    result = [0] * len(bytes_arr)
    for i in range(KEY_LEN):
        shifter = int(key[i])
        for j in range(len(bytes_arr) // KEY_LEN):
            result[(j * KEY_LEN) + i] = bytes_arr[(((j + shifter) * KEY_LEN) % len(bytes_arr)) + i]
    img_bytes =  io.BytesIO(bytes(result))

    try:
        img = Image.open(img_bytes)
        img.save(os.path.join(out_dir_path, f"{key}.png"))
        print(f"KEY:{key} produces a valid PNG - Saving")
    except:
        print(f"KEY:{key} produces a invalid png - Ignoring")

for p in itertools.product(*shifters):
    key = "".join("{}".format(n) for n in p)
    create_png(bytes_arr, key, out_dir_path)
```

### Execution

Now we can execute our script. Before doing so, make sure you have saved the bytes into a file named `bytes.txt` and defined the `out_dir_path` in the script.
```
python script.py

Key 4894748485167104 produces a valid PNG - Saving
Key 4894748485267104 produces an invalid PNG - Ignoring
Key 4894748486167104 produces an invalid PNG - Ignoring
Key 4894748486267104 produces an invalid PNG - Ignoring
```

After executing the script, a PNG file will be saved into the directory you specified. When you open the image, you'll see a QR code. You can scan it using your mobile phone or read it using any tool like `zbarimg`. You can find more information about this tool on the Internet.
