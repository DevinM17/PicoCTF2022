# Cryptography - credstuff
## Description
We found a leak of a blackmarket website's login credentials. Can you find the password of the user `cultiris` and successfully decrypt it? Download the leak [here](https://artifacts.picoctf.net/c/534/leak.tar). The first user in `usernames.txt` corresponds to the first password in `passwords.txt`. The second user corresponds to the second password, and so on.

## Provided Hints (1)
Maybe other passwords will have hints about the leak?

## Breaking it down
The description of this challenge really provided me with all I needed to know in order to solve the challenge. We are told right off the bat that the first user in usernames.txt corresponds to the first password in passwords.txt, so on and so forth. The challenge itself is to find the password associated with user `cultiris` and decrypt it. We can use a text editor like vim and find the line number in which the user `cultiris` resides. Then we just need to find the same line number in the passwords.txt file.

## Step 1 | Using vim to find cultiris user
Opening the usernames.txt file in vim and entering  :set number allowed me to see all corrosponding line numbers. Then using forward slash I searched for the user. I found the username was on line 378. 
![image](https://user-images.githubusercontent.com/95002315/162091248-18a6f190-b4df-4d25-91cd-4ee40ef53a0d.png)


## Step 2 | Finding password on line 378
As I have done some programming before I have many template scripts sitting around for when I need them. I wasnt 100% sure how to search for a specific line number in vim so I thought I would use a simple line counting script in python to print out the contents of line number 378 in passwords.txt. Of course if you knew how to search for a line number in vim or another text editor or even just scroll through with line numbers visible you could do that. I figured this way was a bit more fun and it uses some of my programming knowledge as well.
![image](https://user-images.githubusercontent.com/95002315/162091323-2fc71584-1789-4b72-a4e9-54360b04e7b4.png)


![image](https://user-images.githubusercontent.com/95002315/162091339-058ae978-44c6-4867-8f55-9207ccdd5d11.png)


## Step 3 | Decrypting the password
You can see from the previous step that the password found clearly looks like a flag as it has some text before a {  and then some text within. Throwing the encrypted value in cyberchef I played around with different bases before trying ROT13 decryption. The flag was finally found.
![image](https://user-images.githubusercontent.com/95002315/162091354-21e606e4-9a4d-4a1b-adb6-cbac8d8c26b5.png)


Flag = picoCTF{C7r1F_54V35_71M3}
