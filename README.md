# Cryptography---19CS412-classical-techqniques
# Caeser Cipher
## Date: 19.2.25
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
CaearCipher.
```
    #include <stdio.h>
    #include <string.h> 
    #include <ctype.h>
    
    int main() { 
    char plain[10], cipher[10];
    int key, i, length;
    printf("\n Enter the plain text:");
    scanf("%s", plain);
    printf("\n Enter the key value:");
    scanf("%d", &key);
    
    printf("\n \n \t PLAIN TEXT: %s", plain);
    printf("\n \n \t ENCRYPTED TEXT: ");
    
    length = strlen(plain);
    
    for (i = 0; i < length; i++) {
        cipher[i] = plain[i] + key;
        
        if (isupper(plain[i]) && (cipher[i] > 'Z'))
            cipher[i] = cipher[i] - 26;
            
        if (islower(plain[i]) && (cipher[i] > 'z'))
            cipher[i] = cipher[i] - 26;
            
        printf("%c", cipher[i]);
    }
    
    printf("\n \n \t AFTER DECRYPTION : ");
    
    for (i = 0; i < length; i++) {
        plain[i] = cipher[i] - key;
        
        if (isupper(cipher[i]) && (plain[i] < 'A'))
            plain[i] = plain[i] + 26;
            
        if (islower(cipher[i]) && (plain[i] < 'a'))
            plain[i] = plain[i] + 26;
            
        printf("%c", plain[i]);
    }
    
    return 0;
    }

```
# OUTPUT:
## Simulating Caesar Cipher
### Input : Anna University
### Encrypted Message : Dqqd Xqlyhuvlwb Decrypted Message : Anna University

# RESULT:
The program is executed successfully

---------------------------------

# PlayFair Cipher
## Date: 24.2.25
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
        #include <stdio.h>
        #include <string.h>
        #include <ctype.h>
        
        #define SIZE 30
        
        void formatText(char text[]) {
            int i, j = 0;
            for (i = 0; text[i]; i++)
                if (text[i] != ' ') text[j++] = tolower(text[i]);
            text[j] = '\0';
        }
        
        void generateKeyTable(char key[], char keyT[5][5]) {
            int used[26] = {0}, i, j, k = 0;
            for (i = 0; i < 5; i++)
                for (j = 0; j < 5; j++) {
                    while (key[k] && used[key[k] - 'a']) k++;
                    keyT[i][j] = key[k] ? key[k++] : (used[k] || k == 'j' - 'a' ? ++k, k + 'a' : k + 'a');
                    used[keyT[i][j] - 'a'] = 1;
                }
        }
        
        void findPositions(char keyT[5][5], char a, char b, int pos[]) {
            for (int i = 0; i < 5; i++)
                for (int j = 0; j < 5; j++)
                    if (keyT[i][j] == a) pos[0] = i, pos[1] = j;
                    else if (keyT[i][j] == b) pos[2] = i, pos[3] = j;
        }
        
        void encrypt(char text[], char keyT[5][5]) {
            int i, pos[4];
            for (i = 0; text[i] && text[i + 1]; i += 2) {
                findPositions(keyT, text[i], text[i + 1], pos);
                text[i] = pos[0] == pos[2] ? keyT[pos[0]][(pos[1] + 1) % 5] :
                         pos[1] == pos[3] ? keyT[(pos[0] + 1) % 5][pos[1]] : keyT[pos[0]][pos[3]];
                text[i + 1] = pos[0] == pos[2] ? keyT[pos[2]][(pos[3] + 1) % 5] :
                              pos[1] == pos[3] ? keyT[(pos[2] + 1) % 5][pos[3]] : keyT[pos[2]][pos[1]];
            }
        }
        
        int main() {
            char key[] = "monarchy", text[] = "instruments", keyT[5][5];
        
            formatText(text);
            if (strlen(text) % 2 != 0) strcat(text, "x"); // Append 'X' if odd length
        
            generateKeyTable(key, keyT);
            encrypt(text, keyT);
        
            printf("Encrypted: %s\n", text);
            return 0;
        }
```
# OUTPUT:
### Key text: Monarchy 
### Plain text: instruments 
### Cipher text: gatlmzclrqtx

## RESULT:
The program is executed successfully


---------------------------

# Hill Cipher
## Date: 26.2.25
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

    #include <stdio.h>
    #include <string.h>
    
    #define SIZE 2 
    
    void encrypt(char plaintext[], int key[SIZE][SIZE]) {
        int cipher[SIZE], i, j;
        char encryptedText[SIZE + 1];
    
        int textVector[SIZE] = {plaintext[0] - 'A', plaintext[1] - 'A'};
    
        for (i = 0; i < SIZE; i++) {
            cipher[i] = 0;
            for (j = 0; j < SIZE; j++)
                cipher[i] += key[i][j] * textVector[j];
            cipher[i] %= 26; // Mod 26 to keep within A-Z range
            encryptedText[i] = cipher[i] + 'A';
        }
        encryptedText[SIZE] = '\0';
    
        printf("Encrypted Text: %s\n", encryptedText);
    }
    
    int main() {
        int key[SIZE][SIZE] = { {3, 3}, {2, 5} }; 
        char plaintext[SIZE + 1] = "HI"; 
    
        printf("Plaintext: %s\n", plaintext);
        encrypt(plaintext, key);
    
        return 0;
    }
    ```


# OUTPUT:
### Simulating Hill Cipher
### Input Message : SecurityLaboratory
### Padded Message : SECURITYLABORATORY Encrypted Message : EACSDKLCAEFQDUKSXU Decrypted Message : SECURITYLABORATORY
## RESULT:
The program is executed successfully

-------------------------------------------------

# Vigenere Cipher
## Date: 3.3.25
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
    #include <stdio.h>
    #include <string.h>
    
    void encrypt(char text[], char key[]) {
        int i, textLen = strlen(text), keyLen = strlen(key);
        for (i = 0; i < textLen; i++)
            text[i] = ((text[i] - 'A') + (key[i % keyLen] - 'A')) % 26 + 'A';
        printf("Encrypted Text: %s\n", text);
    }
    
    int main() {
        char text[100], key[100];
    
        printf("Enter plaintext (UPPERCASE): ");
        scanf("%s", text);
    
        printf("Enter key (UPPERCASE): ");
        scanf("%s", key);
    
        encrypt(text, key);
    
        return 0;
    }
```
# OUTPUT:
### Simulating Vigenere Cipher
### Input Message : SecurityLaboratory
### Encrypted Message : NMIYEMKCNIQVVROWXC Decrypted Message : SECURITYLABORATORY
## RESULT:
The program is executed successfully

-----------------------------------------------------------------------

# Rail Fence Cipher
## Date: 5.3.25
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
```
    #include <stdio.h>
    #include <string.h>
    
    void encrypt(char text[]) {
        int i;
        for (i = 0; i < strlen(text); i += 2) // Print even index characters
            printf("%c", text[i]);
        for (i = 1; i < strlen(text); i += 2) // Print odd index characters
            printf("%c", text[i]);
        printf("\n");
    }
    
    int main() {
        char text[100];
        scanf("%s", text);
        encrypt(text);
        return 0;
    }
```

# OUTPUT:
### Enter a Secret Message wearediscovered
### Enter number of rails 2
### mwaeicvrderdsoee
# RESULT:
The program is executed successfully
