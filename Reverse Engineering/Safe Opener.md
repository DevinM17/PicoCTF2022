# Reverse Engineering – Safe Opener
## Description
Can you open this safe? I forgot the key to my safe but this [program](https://artifacts.picoctf.net/c/463/SafeOpener.java) is supposed to help me with retrieving the lost key. Can you help me unlock my safe? Put the password you recover into the picoCTF flag format like: `picoCTF{password}`

## Provided Hints (0)
No hints are provided for this challenge

## Breaking it down
We have another reverse engineering challenge that has us digging into the programs code. Start by downloading the SafeOpener.java file and open it with a text editor of your choice.

## Step 1 | Finding the encoded password
In the source code we can see a string encoded key which has a value which is unreadable at first. Lets copy that value and see if we can manage to decode it. If we do that we may have our flag.
PICTURE OF VALUE

## Step 2 | Cooking with CyberChef
Using Cyber Chefs magic recipe I can see the value is most likely base64 encoded, when using a decoder we are presented with a password which is also out flag!


Flag = picoCTF{pl3as3_l3t_m3_1nt0_th3_saf3}