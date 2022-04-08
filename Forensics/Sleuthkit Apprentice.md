# Forensics - Sleuthkit Apprentice
## Description 
Download this disk image and find the flag. Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.
-   [Download compressed disk image](https://artifacts.picoctf.net/c/332/disk.flag.img.gz)

## Provided Hints (0)
No hints are provided for this challenge

## Breaking it down
We are given a disk image and told to find the flag, the first thought I have is to use FTK imager and locate the flag file. This could take some time since I have no clues on which directory it is located it, so before uploading to FTK I could use a Linux tool to search for the file.

## Step 1 | Using fiwalk 
Before I upload the file to FTK imager I can use a tool such as fiwalk to find the file path to the flag. 

![image](https://user-images.githubusercontent.com/95002315/162501848-c71b83c8-ea4c-4605-b306-35b63a30ee33.png)

## Step 2 | FTK Imager Analysis
Since I now know the files location I can go to the directory and view the file. As you can see its out flag.

![image](https://user-images.githubusercontent.com/95002315/162501901-d054e51c-1148-4dee-9193-1cac5c2cf6c9.png)

Flag = picoCTF{by73_5urf3r_2f22df38} 
