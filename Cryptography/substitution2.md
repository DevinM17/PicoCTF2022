# Cryptography - substitution2
## Description
It seems that another encrypted message has been intercepted. The encryptor seems to have learned their lesson though and now there isn't any punctuation! Can you still crack the cipher? Download the message [here](https://artifacts.picoctf.net/c/109/message.txt)

## Provided Hints (1)
Try refining your frequency attack, maybe analyzing groups of letters would improve your results?

## Breaking it down
For the last substitution challenge it seems we will once again be using our dcode tool which can be found [here](https://www.dcode.fr/monoalphabetic-substitution). This time we may need to refine our attack as the hint suggests.

## Step 1 | Decoding
Entering the message in as the cipher text and using `PicoCTF{}` as our probable word gives us a decrypted messaged. Although it lacks spaces, we can still see the flag at the bottom of the message.

Flag = PicoCTF{N6R4M_4N41Y515_15_73D10U5_42EA1770}