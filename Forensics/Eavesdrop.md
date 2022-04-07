# Forensics - Eavesdrop
## Description
Download this packet capture and find the flag.
-   [Download packet capture](https://artifacts.picoctf.net/c/360/capture.flag.pcap)

## Provided Hints (1)
All we know is that this packet capture includes a chat conversation and a file transfer.

## Breaking it down
We know that somewhere in the provided pcap file we will find a chat conversation and a file transfer. It can be assumed the file transfer is our flag and the chat conversation may give us more clues on how to decrypt it.

## Step 1 | Follow tcp stream of packet 31
Looking at the packets we first see some DHCP and ARP packets which realistically wouldn't give us much information on how to find the flag. Using Wireshark to follow the tcp stream of a packet such as packet 31 presents us with the chat log. This chat conversation tells us the port the file was sent over and the command needed to decrypt it.
PICTURE OF CHAT 
![[Pasted image 20220407105236.png]]

## Step 2 | Filtering traffic to see the file transfer
The chat conversation provided us with a port number in which the flag was transferred on. We can filter by tcp port in Wireshark to view all traffic on port number 9002. Then when we follow the tcp stream of those packets and we can see an encrypted value.
PICTURE OF VALUE
![[Pasted image 20220407105934.png]]

## Step 3 | Exporting packet bytes
Now that we can see the encrypted, looking back at the conversation we need to run the following command: sudo openssl des3 -d -salt -in file.des3 -out file.txt -k supersecretpassword123. Looking at the command I can see this encrypted value needs to be in a .des3 file. So in Wireshark I opened the packet and exported the packet bytes as file.des3.
PICTURE OF EXPORTING PACKET BYTES
![[Pasted image 20220407110422.png]]

## Step 4 | Decrypting the flag
Now that I have the file.des3 command on my system, I can run the openssl command we saw in the chat conversation and it should leave us with a file.txt which contains the decrypted flag.
PICTURE OF DECRYPT
![[Pasted image 20220407110610.png]]     

Flag = picoCTF{nc_73115_411_0ee7267a}