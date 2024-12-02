#include <stdio.h>
#include <string.h>
#include <ctype.h>

// Function prototypes
void encrypt(char text[], int shift);
void decrypt(char text[], int shift);

int main() {
    char text[100];
    int shift, choice;

    printf("Simple Encryption and Decryption Program\n");
    printf("1. Encrypt\n");
    printf("2. Decrypt\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);

    printf("Enter the text: ");
    getchar(); // To consume the newline character
    fgets(text, sizeof(text), stdin);
    text[strcspn(text, "\n")] = 0; // Remove newline character from input

    printf("Enter the shift value (1-25): ");
    scanf("%d", &shift);

    // Handle the choice
    if (choice == 1) {
        encrypt(text, shift);
    } else if (choice == 2) {
        decrypt(text, shift);
    } else {
        printf("Invalid choice!\n");
    }

    return 0;
}

// Function to encrypt the text
void encrypt(char text[], int shift) {
    for (int i = 0; text[i] != '\0'; i++) {
        if (isalpha(text[i])) {
            char base = isupper(text[i]) ? 'A' : 'a';
            text[i] = (text[i] - base + shift) % 26 + base; // Shift and wrap around
        }
    }
    printf("Encrypted Text: %s\n", text);
}

// Function to decrypt the text
void decrypt(char text[], int shift) {
    for (int i = 0; text[i] != '\0'; i++) {
        if (isalpha(text[i])) {
            char base = isupper(text[i]) ? 'A' : 'a';
            text[i] = (text[i] - base - shift + 26) % 26 + base; // Reverse shift and wrap around
        }
    }
    printf("Decrypted Text: %s\n", text);
}
