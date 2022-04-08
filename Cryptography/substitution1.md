# Cryptography - substitution1
## Description
A second message has come in the mail, and it seems almost identical to the first one. Maybe the same thing will work again. Download the message [here](https://artifacts.picoctf.net/c/416/message.txt).

## Provided Hints (2)
- Try a frequency attack
- Do the punctuation and the individual words help you make any substitutions?

## Breaking it down
Just like substitution0 we can use the online Mono-alphabetic Substitution decoder by dcode.fr to solve this challenge. We should try a frequency attach, but this time we can attack with a probable word.

## Step 1 | Decoding
On the dcode website we have the option to attack with probable or known works in plain text. We can enter "PicoCTF" as our known word and allow the decoding tool to attempt to decrypt the message based on that plaintext value. We can see the results were almost correct, initially the flag starts with `FR3JU3NCY` when it really should be `FR3QU3NCY`. Picking out a small error like that can be tough but, just make sure to pay attention to detail when it comes to these types of challenges.

![image](https://user-images.githubusercontent.com/95002315/162519071-530ef77f-70f0-4f17-bf12-1fd32bbc91e1.png)

![image](https://user-images.githubusercontent.com/95002315/162519087-c37e4f8b-0cdf-40be-b840-da993f294965.png)

Flag = PicoCTF{FR3qU3NCY_4774CK5_4R3_C001_6E0659FB}
