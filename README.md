# Ex-4 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.<br>
STEP-2: Arrange the plain text in row columnar matrix format.<br>
STEP-3: Now read the keyword depending on the number of columns of the plain text.<br>
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.<br>
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.<br>

# PROGRAM
```
#include <stdio.h>
#include <string.h>

void encrypt(char text[], int key, char cipher[]) {
    int len = strlen(text);
    char rail[key][len];

    // Fill matrix with '\n'
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            rail[i][j] = '\n';

    int row = 0, dir = 1;

    // Place characters in zigzag
    for (int i = 0; i < len; i++) {
        rail[row][i] = text[i];

        if (row == 0)
            dir = 1;
        else if (row == key - 1)
            dir = -1;

        row += dir;
    }

    // Read row by row
    int index = 0;
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] != '\n')
                cipher[index++] = rail[i][j];

    cipher[index] = '\0';
}

void decrypt(char cipher[], int key, char text[]) {
    int len = strlen(cipher);
    char rail[key][len];

    // Fill matrix with '\n'
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            rail[i][j] = '\n';

    // Mark zigzag path
    int row = 0, dir = 1;
    for (int i = 0; i < len; i++) {
        rail[row][i] = '*';

        if (row == 0)
            dir = 1;
        else if (row == key - 1)
            dir = -1;

        row += dir;
    }

    // Fill marked positions with cipher text
    int index = 0;
    for (int i = 0; i < key; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] == '*' && index < len)
                rail[i][j] = cipher[index++];

    // Read zigzag to get original text
    row = 0;
    dir = 1;
    index = 0;

    for (int i = 0; i < len; i++) {
        text[index++] = rail[row][i];

        if (row == 0)
            dir = 1;
        else if (row == key - 1)
            dir = -1;

        row += dir;
    }

    text[index] = '\0';
}

int main() {
    char plaintext[100], ciphertext[100], decrypted[100];
    int key;
    printf("Rail Fence Technique\n");
    printf("Enter Plaintext: ");
    scanf("%s", plaintext);

    printf("Enter Key (Number of Rails): ");
    scanf("%d", &key);

    encrypt(plaintext, key, ciphertext);
    decrypt(ciphertext, key, decrypted);
    
    printf("\nEncrypted Text : %s", ciphertext);
    printf("\nDecrypted Text : %s\n", decrypted);

    return 0;
}
```
# OUTPUT
<img width="1918" height="912" alt="Screenshot 2026-07-25 094943" src="https://github.com/user-attachments/assets/f6f9d7d4-8af3-4fd3-a837-fd941c4b20af" />

# RESULT
Rail fence transposition technique has been successsfully implemented and executed using C program.
