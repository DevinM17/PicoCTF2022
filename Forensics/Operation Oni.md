# Forensics - Operation Oni
Note: you must launch a challenge instance in order to view your disk image download link.
## Description
Download this disk image, find the key and log into the remote machine. Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.
-   [Download disk image](https://artifacts.picoctf.net/c/378/disk.img.gz)
-   Remote machine: `ssh -i key_file -p 52064 ctf-player@saturn.picoctf.net`

## Provided Hints (0)
No hints are provided for this challenge

## Breaking it down
Upon launching the instance, we are given a disk image and are told to find the key to login to the remote machine. We need to find a public key and use it to connect to the remote machine which should have the flag somewhere.

## Step 1 | Opening disk image in FTK imager
FTK imager is a powerful tool and in this case I used it to investigate the disk image we were given. As in most cases a public key can be found in the /ssh folder under the root user. In that folder I found one public key.

![image](https://user-images.githubusercontent.com/95002315/162236576-16891ade-5656-47c2-820b-fe01a242ad34.png)


## Step 2 | Connecting using the key
I exported the key that was found in the /ssh folder and used it to connect to the remote machine. The connection was successful and now just needed to look for the flag. Using the ls command I noticed a file called flag.txt, theres a good change are flag is in there! Using the cat command I saw the contents and of course it was the flag.

![image](https://user-images.githubusercontent.com/95002315/162236605-b36c3853-903b-472d-b316-e2f6ff81988d.png)

Flag = picoCTF{k3y_5l3u7h_75b85d71}
