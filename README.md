# Cryptography---19CS412-classical-techqniques
# Caeser Cipher
Caeser Cipher using with different key values

# AIM:

To encrypt and decrypt the given message by using Ceaser Cipher encryption algorithm.


## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

1.	In Ceaser Cipher each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet.
2.	For example, with a left shift of 3, D would be replaced by A, E would become B, and so on.
3.	The encryption can also be represented using modular arithmetic by first transforming the letters into numbers, according to the   
    scheme, A = 0, B = 1, Z = 25.
4.	Encryption of a letter x by a shift n can be described mathematically as,
                       En(x) = (x + n) mod26
5.	Decryption is performed similarly,
                       Dn (x)=(x - n) mod26


## PROGRAM:
PROGRAM:
```
def caesar_encrypt(text, key):
    encrypted_text = ""
    for char in text:
        if 'A' <= char <= 'Z':
            encrypted_text += chr(((ord(char) - ord('A') + key) % 26 + 26) % 26 + ord('A'))
        elif 'a' <= char <= 'z':
            encrypted_text += chr(((ord(char) - ord('a') + key) % 26 + 26) % 26 + ord('a'))
        else:
            encrypted_text += char  # Keep non-alphabetic characters unchanged
    return encrypted_text

def caesar_decrypt(text, key):
    return caesar_encrypt(text, -key)  # Decryption is just encryption with a negative key

def main():
    message = input("Enter the message to encrypt: ")
    key = int(input("Enter the Caesar Cipher key (an integer): "))
    
    encrypted_message = caesar_encrypt(message, key)
    print(f"Encrypted Message: {encrypted_message}")
    
    decrypted_message = caesar_decrypt(encrypted_message, key)
    print(f"Decrypted Message: {decrypted_message}")

if __name__ == "__main__":
    main()
```

## OUTPUT:
![image](https://github.com/user-attachments/assets/6c0d27fd-94eb-4705-97cf-62c3689da3c7)


## RESULT:
The program is executed successfully

---------------------------------

# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.

 
## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

ALGORITHM DESCRIPTION:
The Playfair cipher uses a 5 by 5 table containing a key word or phrase. To generate the key table, first fill the spaces in the table with the letters of the keyword, then fill the remaining spaces with the rest of the letters of the alphabet in order (usually omitting "Q" to reduce the alphabet to fit; other versions put both "I" and "J" in the same space). The key can be written in the top rows of the table, from left to right, or in some other pattern, such as a spiral beginning in the upper-left-hand corner and ending in the centre.
The keyword together with the conventions for filling in the 5 by 5 table constitutes the cipher key. To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. Then apply the following 4 rules, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter. Encrypt the new pair and continue. Some   
   variants of Playfair use "Q" instead of "X", but any letter, itself uncommon as a repeated pair, will do.
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively (wrapping 
   around to the left side of the row if a letter in the original pair was on the right side of the row).
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively (wrapping around 
   to the top side of the column if a letter in the original pair was on the bottom side of the column).
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of 
   corners of the rectangle defined by the original pair. The order is important – the first letter of the encrypted pair is the one that 
    lies on the same row as the first letter of the plaintext pair.
To decrypt, use the INVERSE (opposite) of the last 3 rules, and the 1st as-is (dropping any extra "X"s, or "Q"s that do not make sense in the final message when finished).


## PROGRAM:
```
import re

def prepare_text(text):
    text = re.sub(r'[^a-zA-Z]', '', text).lower().replace('j', 'i')
    if len(text) % 2 != 0:
        text += 'z'
    return text

def create_key_square(key):
    key = ''.join(dict.fromkeys(key.replace('j', 'i') + "abcdefghiklmnopqrstuvwxyz"))
    return [list(key[i:i+5]) for i in range(0, 25, 5)]

def find_positions(key_square, char):
    for i, row in enumerate(key_square):
        if char in row:
            return i, row.index(char)

def playfair_cipher(text, key, encrypt=True):
    key_square = create_key_square(key)
    text = prepare_text(text)
    result = ""
    shift = 1 if encrypt else -1
    
    for i in range(0, len(text), 2):
        a, b = text[i], text[i+1]
        r1, c1 = find_positions(key_square, a)
        r2, c2 = find_positions(key_square, b)
        
        if r1 == r2:
            result += key_square[r1][(c1 + shift) % 5] + key_square[r2][(c2 + shift) % 5]
        elif c1 == c2:
            result += key_square[(r1 + shift) % 5][c1] + key_square[(r2 + shift) % 5][c2]
        else:
            result += key_square[r1][c2] + key_square[r2][c1]
    
    return result

def main():
    key = "priya"
    plaintext = "saveetha"
    ciphertext = playfair_cipher(plaintext, key, encrypt=True)
    decrypted_text = playfair_cipher(ciphertext, key, encrypt=False)
    
    print(f"Key: {key}")
    print(f"Plaintext: {plaintext}")
    print(f"Ciphertext: {ciphertext}")
    print(f"Decrypted Text: {decrypted_text}")

if __name__ == "__main__":
    main()
# Online Python compiler (interpreter) to run Python online.
# Write Python 3 code in this online editor and run it.
print("Try programiz.pro")
```

## OUTPUT:
Output:
Key text: priya Plain text: saveetha Cipher text: gatlmzclrqtx
![image](https://github.com/user-attachments/assets/aa07e60b-224b-4391-81d0-2af0c30bc132)

## RESULT:
The program is executed successfully


---------------------------

# Hill Cipher
Hill Cipher using with different key values

# AIM:

To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

### Step 1:

Design of Hill Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
The Hill cipher is a substitution cipher invented by Lester S. Hill in 1929. Each letter is represented by a number modulo 26. To encrypt a message, each block of n letters is multiplied by an invertible n × n matrix, again modulus 26.
To decrypt the message, each block is multiplied by the inverse of the matrix used for encryption. The matrix used for encryption is the cipher key, and it should be chosen randomly from the set of invertible n × n matrices (modulo 26).
The cipher can, be adapted to an alphabet with any number of letters. All arithmetic just needs to be done modulo the number of letters instead of modulo 26.


## PROGRAM:
```
import numpy as np

def mod_inverse(matrix, mod=26):
    det = int(round(np.linalg.det(matrix)))
    det_inv = pow(det, -1, mod)
    adj = np.round(det * np.linalg.inv(matrix)).astype(int) % mod
    return (det_inv * adj) % mod

def text_to_numbers(text):
    return [ord(c) - ord('A') for c in text]

def numbers_to_text(numbers):
    return ''.join(chr(n % 26 + ord('A')) for n in numbers)

def hill_cipher(text, key, encrypt=True):
    text = text.upper()
    while len(text) % 3 != 0:
        text += 'X'
    matrix = np.array(key)
    if not encrypt:
        matrix = mod_inverse(matrix)
    text_numbers = text_to_numbers(text)
    result = []
    for i in range(0, len(text_numbers), 3):
        block = np.array(text_numbers[i:i+3])
        encoded_block = np.dot(matrix, block) % 26
        result.extend(encoded_block)
    return numbers_to_text(result)

def main():
    key = [[1, 2, 1], [2, 3, 2], [2, 2, 1]]
    message = "priya"
    encrypted = hill_cipher(message, key, encrypt=True)
    decrypted = hill_cipher(encrypted, key, encrypt=False)
    print(f"Original: {message}")
    print(f"Encrypted: {encrypted}")
    print(f"Decrypted: {decrypted}")

if __name__ == "__main__":
    main()
```

## OUTPUT:
![image](https://github.com/user-attachments/assets/35f18f5f-fd25-4812-82fa-d6d3353cc55b)

## RESULT:
The program is executed successfully

-------------------------------------------------

# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:

To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:

### Step 1:

Design of Vigenere Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
The Vigenere cipher is a method of encrypting alphabetic text by using a series of different Caesar ciphers based on the letters of a keyword. It is a simple form of polyalphabetic substitution.To encrypt, a table of alphabets can be used, termed a Vigenere square, or Vigenere table. It consists of the alphabet written out 26 times in different rows, each alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses a different alphabet from one of the rows used. The alphabet at each point depends on a repeating keyword.



## PROGRAM:
```

```
## OUTPUT:
OUTPUT :

Simulating Vigenere Cipher


Input Message : SecurityLaboratory
Encrypted Message : NMIYEMKCNIQVVROWXC Decrypted Message : SECURITYLABORATORY
## RESULT:
The program is executed successfully

-----------------------------------------------------------------------

# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
In the rail fence cipher, the plaintext is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

## PROGRAM:

PROGRAM:
#include<stdio.h> #include<string.h> #include<stdlib.h> main()
{
int i,j,len,rails,count,code[100][1000]; char str[1000];
printf("Enter a Secret Message\n"); gets(str);
len=strlen(str);
printf("Enter number of rails\n"); scanf("%d",&rails); for(i=0;i<rails;i++)
{
for(j=0;j<len;j++)
{
code[i][j]=0;
}
}
count=0; j=0;
while(j<len)
{
if(count%2==0)
{
for(i=0;i<rails;i++)
{
//strcpy(code[i][j],str[j]);
code[i][j]=(int)str[j]; j++;
}

}
else
{
 
for(i=rails-2;i>0;i--)
{
code[i][j]=(int)str[j]; j++;
}
}

count++;
}

for(i=0;i<rails;i++)
{
for(j=0;j<len;j++)
{
if(code[i][j]!=0) printf("%c",code[i][j]);
}
}
printf("\n");
}
## OUTPUT:
OUTPUT:
Enter a Secret Message wearediscovered
Enter number of rails 2
waeicvrderdsoee
## RESULT:
The program is executed successfully
