# Reverse Engineering - unpackme.py
## Description
Can you get the flag? Reverse engineer this [Python program](https://artifacts.picoctf.net/c/466/unpackme.flag.py).

## Provided Hints (0)
No hints are provided for this challenge

## Breaking it down
As with many reverse engineering challenges we may need to take a look at the programs source code and see how we can make it work to our advantage.

## Step 1 | Analyzing and modifying the source code
After downloading the program I opened the program in my text editor of choice (vim). I can see some values but, nothing that looks like out flag. My first through is to add a simple print statement at the end of the program that would print the value of "plain" as it was seen being decoded a few lines above.

![image](https://user-images.githubusercontent.com/95002315/162525354-36b2f03a-0633-46f5-8317-7005eda86b86.png)

## Step 2 | Testing the print statement
Once I made the changes I saved the program and ran it like normal, as we are prompted for a password I just entered a random value and pressed enter. Since the print statement I added was at the very end of the code, the last thing to occur was a print statement which printed the following. Looks like out flag.

![image](https://user-images.githubusercontent.com/95002315/162525394-d9cffa9e-c849-4cc5-bf74-38ee69113de4.png)

## Step 3 | Demonstration 
Now for demonstration purposes I want to enter the correct password and be rewarded the flag. In the output seen in the last step we can see it checking of password is equal to `batteryhorse` and if so, providing the flag. I reran the program one last time and entered in that value as the password, of course I was given the flag.

![image](https://user-images.githubusercontent.com/95002315/162525414-16fc36cb-82a7-487b-b12e-ffc349df25d7.png)

Flag = picoCTF{175_chr157m45_85f5d0ac}
