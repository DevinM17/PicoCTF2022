# Cryptography - substitution0
## Description
A message has come in but it seems to be all scrambled. Luckily it seems to have the key at the beginning. Can you crack this substitution cipher? Download the message [here](https://artifacts.picoctf.net/c/381/message.txt).

## Provided Hints (1)
Try a frequency attack. An online tool might help.

## Breaking it down
So we know the message we were provided is scrambled and we need to unscramble it. The key to unscrambling it is at the beginning of the message. The hint tells us to try a frequency attack and that an online too may help. Thankfully dcode.fr has a variety of tools that may help us solve this challenge.

## Step 1 | Decoding using dcode.fr
Dcode.fr has a great Mono-alphabetic Substitution decoding tool (found [here](https://www.dcode.fr/monoalphabetic-substitution)) that we can use. We can paste in the bulk of the message (excluding the first line) into the ciphertext box and then copy the first line into the "Knowing the substitution alphabet used" box. Once we press decode we can see in the results pane the message has been decoded. 

Flag = PICOCTF{5UB5717U710N_3V0LU710N_357BF9FF}