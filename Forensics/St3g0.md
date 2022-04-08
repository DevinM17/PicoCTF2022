# Forensics - St3g0
## Description
Download this image and find the flag.
-   [Download image](https://artifacts.picoctf.net/c/423/pico.flag.png)

## Provided Hints (1)
We know the end sequence of the message will be `$t3g0`

## Breaking it down
We are provided an image for this challenge and right off the bat we know there is some hidden information embedded in it as the title suggests. The hint suggests we will find the following at the end of the message `$t3g0`.  We will need to determine what type of stego technique was used to embed the data so we can extract it.

## Step 1 | Least Significant bit
After attempting to extrach the data multiple ways I decided to research Basic Steganography in PNG files and found [this](https://shanereilly.net/posts/basic_steganography_and_png_files/) article which lead me to believe LSB was used to embed the data.

## Step 2 | Extraction
The flag can be seen in the output of the following command: `zsteg -a pico.flag.png`. The flag was embedded in b1,RGB,LSB,XY.

![image](https://user-images.githubusercontent.com/95002315/162516446-6e07094a-6f97-41cf-962b-ed8e33d0099c.png)

Flag = picoCTF{7h3r3_15_n0_5p00n_a9a181eb}
