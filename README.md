# Hill Cipher
Hill Cipher using with different key values


#REG NO:212222230158
NAME:thamizh selvan

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
#include <stdio.h>
#include <string.h>

int main() {
    unsigned int a[3][3] = {{6, 24, 1}, {13, 16, 10}, {20, 17, 15}};
    unsigned int b[3][3] = {{8, 5, 10}, {21, 8, 21}, {21, 12, 8}};
    int i, j, t = 0;
    unsigned int c[3], d[3];
    char msg[4], key[4];

    printf("Enter plain text (3 letters): ");
    scanf("%3s", msg);

    if (strlen(msg) != 3) {
        printf("Error: The plain text must be exactly 3 letters.\n");
        return 1;
    }

    printf("Enter key (3 letters): ");
    scanf("%3s", key);

    if (strlen(key) != 3) {
        printf("Error: The key must be exactly 3 letters.\n");
        return 1;
    }

    printf("Plain text numeric values: ");
    for (i = 0; i < 3; i++) {
        c[i] = msg[i] - 'A';
        printf("%d ", c[i]);
    }

    printf("\nKey numeric values: ");
    for (i = 0; i < 3; i++) {
        d[i] = key[i] - 'A';
        printf("%d ", d[i]);
    }

    for (i = 0; i < 3; i++) {
        t = 0;
        for (j = 0; j < 3; j++) {
            t += a[i][j] * c[j];
        }
        d[i] = t % 26;
    }

    printf("\nEncrypted Cipher Text: ");
    for (i = 0; i < 3; i++) {
        printf("%c", d[i] + 'A');
    }

    for (i = 0; i < 3; i++) {
        t = 0;
        for (j = 0; j < 3; j++) {
            t += b[i][j] * d[j];
        }
        c[i] = t % 26;
    }

    printf("\nDecrypted Cipher Text: ");
    for (i = 0; i < 3; i++) {
        printf("%c", c[i] + 'A');
    }

    getchar();
    return 0;
}






```

## OUTPUT:

![image](https://github.com/user-attachments/assets/aaa9125b-6c06-4f2e-bba8-f2a605ff98c7)


## RESULT:
The program is executed successfully
