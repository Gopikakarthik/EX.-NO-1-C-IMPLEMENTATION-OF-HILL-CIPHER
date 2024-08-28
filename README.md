# EX.-NO-1-C-IMPLEMENTATION-OF-HILL-CIPHER

## AIM:
To write a C program to implement the hill cipher substitution techniques.

## ALGORITHM:

STEP-1: Read the plain text and key from the user.

STEP-2: Split the plain text into groups of length three.

STEP-3: Arrange the keyword in a 3*3 matrix.

STEP-4: Multiply the two matrices to obtain the cipher text of length three.

STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM: 

```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define SIZE 2  // Size of the key matrix (2x2)


int modInverse(int a, int m) {
    a = a % m;
    for (int x = 1; x < m; x++) {
        if ((a * x) % m == 1)
            return x;
    }
    return -1;
}


void multiply(int keyMatrix[SIZE][SIZE], int block[SIZE], int result[SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        result[i] = 0;
        for (int j = 0; j < SIZE; j++) {
            result[i] += keyMatrix[i][j] * block[j];
        }
        result[i] %= 26;
    }
}


void encrypt(char plaintext[], int keyMatrix[SIZE][SIZE], char ciphertext[]) {
    int block[SIZE], result[SIZE];
    int len = strlen(plaintext);
    int i, j;

    for (i = 0; i < len; i += SIZE) {
        for (j = 0; j < SIZE; j++) {
            block[j] = plaintext[i + j] - 'A';
        }
        multiply(keyMatrix, block, result);
        for (j = 0; j < SIZE; j++) {
            ciphertext[i + j] = result[j] + 'A';
        }
    }
    ciphertext[len] = '\0';
}

void prepareText(char plaintext[]) {
    int len = strlen(plaintext);
    int i;

    
    for (i = 0; i < len; i++) {
        plaintext[i] = toupper(plaintext[i]);
    }

    
    if (len % SIZE != 0) {
        for (i = len; i < len + SIZE - (len % SIZE); i++) {
            plaintext[i] = 'X';
        }
        plaintext[i] = '\0';
    }
}

int main() {
    char plaintext[100], ciphertext[100];
    int keyMatrix[SIZE][SIZE] = {{3, 3}, {2, 5}};  // Example key matrix (2x2)

    printf("Enter the plaintext (without spaces): ");
    scanf("%s", plaintext);

    prepareText(plaintext);
    encrypt(plaintext, keyMatrix, ciphertext);

    printf("Ciphertext: %s\n", ciphertext);

    return 0;
}

```
## OUTPUT:

![Screenshot 2024-08-28 161728](https://github.com/user-attachments/assets/00ca4dec-1c99-4f41-94e3-7982e97c385d)

## RESULT:
  Thus the hill cipher substitution technique had been implemented successfully.
