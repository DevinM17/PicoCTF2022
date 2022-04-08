# Cryptography - Vigenere
## Description
Can you decrypt this message? Decrypt this [message](https://artifacts.picoctf.net/c/529/cipher.txt) using this key "CYLAB".

## Provided Hints (1)
https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher

## Breaking it down
Most of the times when I need to decrypt a value I turn to CyberChef and this challenge is no different. Since we are given the ciphertext and key we should be able to decrypt the message easily, as long as CyberChef has a Vigenere decrypt recipe that is.

## Step 1 | CyberChef
After a quick search it can be seen that CyberChef does in fact have a Vigenere decoding recipe. We can paste our cipher text in, load the recipe, enter the key we were provided, and bake! We can see the flag in plaintext.

![image](https://user-images.githubusercontent.com/95002315/162526154-b6636122-d02b-4b47-ba87-9fa75f9f6ad9.png)

Flag = picoCTF{D0NT_US3_V1G3N3R3_C1PH3R_2951a89h}
