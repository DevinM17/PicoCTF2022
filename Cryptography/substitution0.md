# Cryptography - substitution0
## Description
A message has come in but it seems to be all scrambled. Luckily it seems to have the key at the beginning. Can you crack this substitution cipher? Download the message [here](https://artifacts.picoctf.net/c/381/message.txt).

## Provided Hints (1)
Try a frequency attack. An online tool might help.

## Breaking it down
So we know the message we were provided is scrambled and we need to unscramble it. The key to unscrambling it is at the beginning of the message. The hint tells us to try a frequency attack and that an online too may help. Thankfully dcode.fr has a variety of tools that may help us solve this challenge.

## Step 1 | Decoding using dcode.fr
Dcode.fr has a great Mono-alphabetic Substitution decoding tool (found [here](https://www.dcode.fr/monoalphabetic-substitution)) that we can use. We can paste in the bulk of the message (excluding the first line) into the ciphertext box and then copy the first line into the "Knowing the substitution alphabet used" box. Once we press decode we can see in the results pane the message has been decoded. 

![image](https://user-images.githubusercontent.com/95002315/162517816-bc2fed75-becc-42dd-9d22-7ef1313070d7.png)

![image](https://user-images.githubusercontent.com/95002315/162517835-872df5c3-f9c9-4fe4-9f5e-05c682fbb78e.png)

Flag = PICOCTF{5UB5717U710N_3V0LU710N_357BF9FF}
