# Forensics - Operation Orchid
## Description
Download this disk image and find the flag. Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.
-   [Download compressed disk image](https://artifacts.picoctf.net/c/238/disk.flag.img.gz)

## Provided Hints (0)
No hints are provided for this challenge

## Breaking it down
We have another challenge which requires us to deal with a disk image. This time the image comes as .img.gz which means we must first use the gunzip command to decompress the image. Once the image is decompressed we can begin to analyze it and attempt to find the flag.

## Step 1 | Using fiwalk 
I used fiwalk piped into grep to search for a flag file, this way I can know which directory to look in when analyzing the image in FTK imager. The output shows there is a flag.txt.enc file in the root directory.

![image](https://user-images.githubusercontent.com/95002315/162245544-4e03607a-cba0-4e9a-a186-cd4ffce5a613.png)

## Step 2 | FTK Imager Analysis    
After loading the image in FTK imager I searched the root directory and found two files. .ash_history and flag.txt.enc can be seen, the history file shows command history and it can be seen that the user used the openssl command to encrypt the flag.txt file. This explains why when using fiwalk it showed flag.txt and flag.txt.enc, it knows that flag.txt existed but we know from the command history file that the file was encrypted.

![image](https://user-images.githubusercontent.com/95002315/162245592-001242db-6605-4e11-9778-48f68fc0d47f.png)

![image](https://user-images.githubusercontent.com/95002315/162245607-05f4a54e-3319-436d-8764-40be23d2e914.png)

## Step 3 | Decrypting flag.txt.enc
Now to find the flag we need to decrpyt the flag.txt.enc file, we can use ftk imager to export the file to our system. Then since the command history shows us how the file was encrypted we can run the inverse of the command to decrypt it. Then we just have to use the cat command to view the contents of file.txt and the flag is found! 

![image](https://user-images.githubusercontent.com/95002315/162245649-82d41d16-3e8f-41a8-b84b-44f1e4ec34fe.png)

Flag = picoCTF{h4un71ng_p457_1d02081e}
