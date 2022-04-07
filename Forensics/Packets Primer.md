# Forensic - Packets Primer
## Description 
Download the packet capture file and use packet analysis software to find the flag.
-   [Download packet capture](https://artifacts.picoctf.net/c/201/network-dump.flag.pcap)

## Provided Hints (1)
Wireshark, if you can install and use it, is probably the most beginner friendly packet analysis software product.

## Breaking it down
The challenge requires us to analyze a packet capture and find the flag using a packet analysis software. First software that comes to mind is Wireshark as it is free, easy to install, and easy to use.

## Step 1 | Opening pcap file in Wireshark
Once the packet capture was opened in the packet analysis software of choice (Wireshark) I could see a total of 9 packets. Packets 6-9 are all ARP packets which most likely wont contain a flag and the rest are TCP packets. Out of the two protocols it is more likely to find the flag in the TPC packets so we should investigate those.
PICTURE OF CAPTURE

## Step 2 | Follow the TCP stream and find the flag
Since we narrowed it down to the TCP packets that most likely will contain the flag we can follow the tcp stream of one of the packets and click through until we find something interesting. Doing so we find the flag in plain text!
PICTURE OF FLAG

Flag = picoCTF{p4ck37_5h4rk_01b0a0d6}