## EX. NO: 1 : IMPLEMENTATION OF CAESAR CIPHER
 

## AIM:

To implement the simple substitution technique named Caesar cipher using C language.

## DESCRIPTION:

To encrypt a message with a Caesar cipher, each letter in the message is changed using a simple rule: shift by three. Each letter is replaced by the letter three letters ahead in the alphabet. A becomes D, B becomes E, and so on. For the last letters, we can think of the
alphabet as a circle and "wrap around". W becomes Z, X becomes A, Y bec mes B, and Z
becomes C. To change a message back, each letter is replaced by the one three before it.

## EXAMPLE:



![image](https://github.com/Hemamanigandan/CNS/assets/149653568/eb9c6c43-8c80-4cdd-b9d4-91705a311c79)


## ALGORITHM:

### STEP-1: Read the plain text from the user.
### STEP-2: Read the key value from the user.
### STEP-3: If the key is positive then encrypt the text by adding the key with each character in the plain text.
### STEP-4: Else subtract the key from the plain text.
### STEP-5: Display the cipher text obtained above.


PROGRAM :-
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>
#define MAX_LENGTH 1000

void caesarCipher(char text[], int key) {
    int i;
    char ch;
    
    for (i = 0; text[i] != '\0'; i++) {
        ch = text[i];
        if (isalpha(ch)) {
           if (isupper(ch)) {
               if (key >= 0) {
                    text[i] = ((ch - 'A' + key) % 26) + 'A';
                } else {
                    text[i] = ((ch - 'A' + key + 26) % 26) + 'A';
                }
            }
            else {
                if (key >= 0) {
                    text[i] = ((ch - 'a' + key) % 26) + 'a';
                } else {
                    text[i] = ((ch - 'a' + key + 26) % 26) + 'a';
                }
            }
        }
    }
}

void encrypt(char text[], int key) {
    caesarCipher(text, key);
}

void decrypt(char text[], int key) {
    caesarCipher(text, -key);
}

int main() {
    char plainText[MAX_LENGTH];
    char cipherText[MAX_LENGTH];
    char decryptedText[MAX_LENGTH];
    int key;
    int choice;
    
    printf("Choose operation:\n");
    printf("1. Encrypt a message\n");
    printf("2. Decrypt a message\n");
    printf("3. Encrypt then decrypt (demo)\n");
    printf("Enter your choice (1-3): ");
    scanf("%d", &choice);
    getchar(); // consume newline after scanf
    
    printf("\nEnter the text: ");
    fgets(plainText, sizeof(plainText), stdin);
    plainText[strcspn(plainText, "\n")] = '\0';
    
    printf("Enter the key value (integer): ");
    if (scanf("%d", &key) != 1) {
        printf("Invalid key! Please enter an integer.\n");
        return 1;
    }
    
    strcpy(cipherText, plainText);
    
    switch(choice) {
        case 1:
            // ENCRYPTION
            encrypt(cipherText, key);
            printf("Original text: %s\n", plainText);
            printf("Encrypted text: %s\n", cipherText);
            printf("Key used: %d\n", key);
            break;
            
        case 2:
            decrypt(cipherText, key);
            printf("Cipher text: %s\n", plainText);
            printf("Decrypted text: %s\n", cipherText);
            printf("Key used: %d\n", key);
            break;
            
        case 3:
         
            strcpy(decryptedText, cipherText);
            
            encrypt(cipherText, key);
            decrypt(decryptedText, -key); 
            
            
            printf("Original text:  %s\n", plainText);
            printf("Encrypted text: %s\n", cipherText);
            
            
            strcpy(decryptedText, cipherText);
            decrypt(decryptedText, key);
            printf("Decrypted text: %s\n", decryptedText);
            printf("Key used: %d\n", key);
            

            if (strcmp(plainText, decryptedText) == 0) {
                printf("\n✓ SUCCESS: Decryption restored original text!\n");
            } else {
                printf("\n✗ ERROR: Decryption failed!\n");
            }
            break;
            
        default:
            printf("Invalid choice!\n");
            return 1;
    }
    return 0;
}
```
OUTPUT :-
<img width="1634" height="893" alt="image" src="https://github.com/user-attachments/assets/daa23671-a605-403b-9a96-f778491f672b" />
