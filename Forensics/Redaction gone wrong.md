# Forensics - Redaction gone wrong

## Description

Now you DON’T see me. This [report](https://artifacts.picoctf.net/c/264/Financial_Report_for_ABC_Labs.pdf) has some critical data in it, some of which have been redacted correctly, while some were not. Can you find an important key that was not redacted properly?

## Provided Hints (1)

How can you be sure of the redaction?

## Breaking it down

The challenge provides us with a pdf file which on the surface appears to have some redacted information. We need to find a way to extract the redacted information as its likely our flag is hidden within.

PIC OF REDACTED

## Step 1 | CTRL + A, C, and V

Some text visible on the document says, "Just painted over in MS word", this lead me to trying a CTRL + A to select all text and copying it with CTRL + C and pasting it all into a text file with CTRL + V. Below you will see the outputted text, seems we have extracted the flag pretty easily.

PIC OF FLAG

Flag = picoCTF{C4n_Y0u_S33_m3_fully}