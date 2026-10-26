# HILL CIPHER EX. NO: 3 
## AIM:
 IMPLEMENTATION OF HILL CIPHER
 
## To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM :
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define MAXLEN 900

int keymat[3][3] = { { 1, 2, 1 }, { 2, 3, 2 }, { 2, 2, 1 } };
int invkeymat[3][3] = { { -1, 0, 1 }, { 2, -1, 0 }, { -2, 2, -1 } };
char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

/* Encrypt one block of 3 letters into out[0..2] */
void encode(char a, char b, char c, char *out)
{
    int x, y, z;
    int posa = a - 'A';
    int posb = b - 'A';
    int posc = c - 'A';

    x = posa * keymat[0][0] + posb * keymat[1][0] + posc * keymat[2][0];
    y = posa * keymat[0][1] + posb * keymat[1][1] + posc * keymat[2][1];
    z = posa * keymat[0][2] + posb * keymat[1][2] + posc * keymat[2][2];

    out[0] = key[((x % 26) + 26) % 26];
    out[1] = key[((y % 26) + 26) % 26];
    out[2] = key[((z % 26) + 26) % 26];
    out[3] = '\0';
}

/* Decrypt one block of 3 letters into out[0..2] */
void decode(char a, char b, char c, char *out)
{
    int x, y, z;
    int posa = a - 'A';
    int posb = b - 'A';
    int posc = c - 'A';

    x = posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * invkeymat[2][0];
    y = posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * invkeymat[2][1];
    z = posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * invkeymat[2][2];

    out[0] = key[((x % 26) + 26) % 26];
    out[1] = key[((y % 26) + 26) % 26];
    out[2] = key[((z % 26) + 26) % 26];
    out[3] = '\0';
}

int main(void)
{
    char input[MAXLEN];
    char msg[MAXLEN + 4];
    char enc[MAXLEN + 4] = "";
    char dec[MAXLEN + 4] = "";
    char block[4];
    int i, n, len = 0;

    printf("Simulation of Hill Cipher\n");
    printf("Enter the message: ");
    if (fgets(input, sizeof(input), stdin) == NULL) {
        printf("Failed to read message.\n");
        return 1;
    }

    /* Keep letters only, convert to uppercase */
    for (i = 0; input[i] != '\0'; i++) {
        if (isalpha((unsigned char)input[i])) {
            msg[len++] = (char)toupper((unsigned char)input[i]);
        }
    }
    msg[len] = '\0';

    if (len == 0) {
        printf("Message must contain at least one letter.\n");
        return 1;
    }

    printf("Input message : %s", input);
    if (strchr(input, '\n') == NULL) printf("\n");

    /* Pad with X to a multiple of 3 */
    n = len % 3;
    if (n != 0) {
        for (i = 0; i < 3 - n; i++) {
            msg[len++] = 'X';
        }
        msg[len] = '\0';
    }
    printf("Padded message : %s\n", msg);

    /* Encrypt */
    for (i = 0; i < len; i += 3) {
        encode(msg[i], msg[i + 1], msg[i + 2], block);
        strcat(enc, block);
    }
    printf("Encoded message : %s\n", enc);

    /* Decrypt */
    for (i = 0; i < len; i += 3) {
        decode(enc[i], enc[i + 1], enc[i + 2], block);
        strcat(dec, block);
    }
    printf("Decoded message : %s\n", dec);

    return 0;
}   
```

## OUTPUT:
<img width="1807" height="841" alt="image" src="https://github.com/user-attachments/assets/e75fa4bb-aac7-4222-8c84-4ffb8a81f871" />


## RESULT:
The program is executed successfully
