# Reverse Engineering – patchme.py 
## Description
Can you get the flag? Run this [Python program](https://artifacts.picoctf.net/c/388/patchme.flag.py) in the same directory as this [encrypted flag](https://artifacts.picoctf.net/c/388/flag.txt.enc).

## Provided Hints (0)
No hints are provided for this challenge

## Breaking it down
We are told to run the Python program in the same directory as the encrypted flag. It can be assumed when we do this we will either be given the decrypted version of the flag or we will need to do some more work to get it. So lets download the two files and do just that.

## Step 1 | Running the program with the encrypted flag
We can run the program and pass the encrypted flag on the command line, once we do this we are prompted for a password in order to receive the flag. 

![image](https://user-images.githubusercontent.com/95002315/162255849-3368a569-ce2f-453a-9ab6-8d1e90172a9d.png)

## Step 2 | Checking the source code
Since we need a password in order to obtain the flag and there are no hints, the next thing to do is check the source code for any clues. The first thing I noticed was a function called `level_1_pw_check`. We can see this function checks to see if user_pw is equal to a few values added together.       

![image](https://user-images.githubusercontent.com/95002315/162255904-2458f93d-fab0-4be8-8014-38cd9c1e61f9.png)

## Step 3 | Changing the function
Now realistically I could enter the added together values as the password but, since this is a reverse engineering challenge I figured I would edit the source code to fit my needs. I decided to change the function to check if the value entered is equal to the string "Flag" and if so, print the flag.

![image](https://user-images.githubusercontent.com/95002315/162255930-baac90b5-fcda-48a1-974e-c762ee2a8f78.png)

## Step 3 | Running the program again
Now that I have changed the program, when I run it and enter the password "flag" I should be presented with the flag. As you can see below, it worked!

![image](https://user-images.githubusercontent.com/95002315/162255967-42abecde-5160-4a76-9cf2-4e59974542e7.png)

Flag = picoCTF{p47ch1ng_l1f3_h4ck_21d62e33}
