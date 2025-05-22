# HILL CIPHER
HILL CIPHER
EX. NO: 3 AIM:
 

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

## PROGRAM 
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>
#define SIZE 3
int keyMatrix[SIZE][SIZE] = {
{2, 4, 5}, {9, 2, 1}, {3, 17, 7}
};
int inverseKeyMatrix[SIZE][SIZE] = {
{4, 9, 15}, {15, 17, 6}, {24, 0, 17}
};
void preprocessMessage(char *input, char *output) {
int len = 0;
for (int i = 0; input[i] != '\0'; i++) {
if (isalpha(input[i])) {
output[len++] = toupper(input[i]);
}
}
while (len % SIZE != 0) { // Pad with 'X'
output[len++] = 'X';
}
output[len] = '\0';
}
void encryptBlock(char *block, char *encrypted) {
int num[SIZE], result[SIZE];
for (int i = 0; i < SIZE; i++)
num[i] = block[i] - 'A';
for (int i = 0; i < SIZE; i++) {
result[i] = 0;
for (int j = 0; j < SIZE; j++) {
result[i] += keyMatrix[i][j] * num[j];
}
result[i] %= 26; // Mod 26
}
for (int i = 0; i < SIZE; i++)
encrypted[i] = result[i] + 'A';
}
void decryptBlock(char *block, char *decrypted) {
int num[SIZE], result[SIZE];
for (int i = 0; i < SIZE; i++)
num[i] = block[i] - 'A';
for (int i = 0; i < SIZE; i++) {
result[i] = 0;
for (int j = 0; j < SIZE; j++) {
result[i] += inverseKeyMatrix[i][j] * num[j];
}
result[i] %= 26; // Mod 26
}
for (int i = 0; i < SIZE; i++)
decrypted[i] = result[i] + 'A';
}
int main() {
char inputMessage[] = "Shubhavi";
char paddedMessage[100], encryptedMessage[100], decryptedMessage[100];
preprocessMessage(inputMessage, paddedMessage);
printf("Padded Message: %s\n", paddedMessage);
int len = strlen(paddedMessage);
for (int i = 0; i < len; i += SIZE) {
encryptBlock(&paddedMessage[i], &encryptedMessage[i]);
}
encryptedMessage[len] = '\0';
printf("Encrypted Message: %s\n", encryptedMessage);
for (int i = 0; i < len; i += SIZE) {
decryptBlock(&encryptedMessage[i], &decryptedMessage[i]);
}
decryptedMessage[len] = '\0';
printf("Decrypted Message: %s\n", decryptedMessage);
return 0;
}
```

## OUTPUT
![image](https://github.com/user-attachments/assets/aad3981c-5ab2-4c00-96ff-e637801c5a83)


## RESULT
The program is executed successfully.
