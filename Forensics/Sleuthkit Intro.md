# Forensics - Sleuthkit Intro
## Description
Download the disk image and use `mmls` on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag. Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.
-   [Download disk image](https://artifacts.picoctf.net/c/114/disk.img.gz)
-   Access checker program: `nc saturn.picoctf.net 52279`

## Provided Hints (0)
No hints are provided for this challenge

## Breaking it down
As with any challenge involving a disk image we must first download the image and in this case also decompress it with gunzip. We are told to use mmls to find the size of a Linux partition and check the answer using a remote checking service. IT can be assumed once we answer correctly that we will be given the flag.

## Step 1 | Using mmls to find Linux partition
The mmls command can be used to show the parition table on this disk image. Simply run the following command `mmls disk.img`. You will see in the output below the Linuix partition is seen and we can see the following information such as the partition starts at 0000002048 and ends at 0000204799, and a length of 0000202752. 
PIC OF OUTPUT

## Step 2 | Checking our answer
Connecting to the remote checking service via netcat we are prompted for the size of the Linux partition which we noted down as 0000202752. Once we enter that information we are given the flag.


Flag = picoCTF{mm15_f7w!}