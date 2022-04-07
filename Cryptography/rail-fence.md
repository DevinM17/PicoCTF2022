# Cryptography - rail-fence
## Description

A type of transposition cipher is the rail fence cipher, which is described [here](https://en.wikipedia.org/wiki/Rail_fence_cipher). Here is one such cipher encrypted using the rail fence with 4 rails. Can you decrypt it? Download the message [here](https://artifacts.picoctf.net/c/274/message.txt). Put the decoded message in the picoCTF flag format, `picoCTF{decoded_message}`.

## Provided Hints (1)

Once you've understood how the cipher works, it's best to draw it out yourself on paper

## Breaking it down

The description of this challenge tells us that the message file provided is encrypted using a rail fence cipher, more specifically a rail cipher using 4 rails. We can use a web-based tool called CyberChef to decode this message and possibly retrieve the flag.

## Step 1 | Decoding value in CyberChef

After downloading the message file we can copy and paste the value into CyberChef, then since we know it was encrypted using a rail cipher I searched for rail fence cipher decoder tool. Thankfully CyberChef had such a tool and I entered in the key value of 4 (we were told the message was encrypted with 4 rails).

PICTURE OF DECODE

Flag = picoCTF{WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_D00AFDD3}