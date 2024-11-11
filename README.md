# EX-NO-2-B-COLUMN TRANSFORMATION CIPHER

## AIM:
  To write a C program to implement the rail fence transposition technique.
  
## ALGORITHM:

STEP-1: Read the Plain text.

STEP-2: Arrange the plain text in row columnar matrix format.

STEP-3: Now read the keyword depending on the number of columns of the plain text.

STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.

STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

## PROGRAM:
```
#include <stdio.h>
#include <string.h>

void cipher(int i, int r);
int findMin();
void makeArray(int col, int row);

char arr[22][22], darr[22][22], emessage[111], retmessage[111], key[55];
char temp[55], temp2[55];
int k = 0;

int main() {
    char message[111];
    int i, j, klen, emlen, flag = 0;
    int r, c, index, rows;

    printf("Enter the key:\n");
    scanf("%s", key);
    
    printf("\nEnter the message to be ciphered:\n");
    getchar(); // To consume newline left by scanf
    fgets(message, sizeof(message), stdin);
    message[strcspn(message, "\n")] = '\0'; // Remove newline character from fgets

    strcpy(temp, key);
    klen = strlen(key);
    k = 0;

    // Fill the array with the message
    for (i = 0; ; i++) {
        if (flag == 1) break;
        for (j = 0; j < klen; j++) {
            if (message[k] == '\0') {
                flag = 1;
                arr[i][j] = '-';
            } else {
                arr[i][j] = message[k++];
            }
        }
    }

    r = i;
    c = j;

    // Print the filled array
    for (i = 0; i < r; i++) {
        for (j = 0; j < c; j++) {
            printf("%c ", arr[i][j]);
        }
        printf("\n");
    }

    // Encryption process
    k = 0;
    for (i = 0; i < klen; i++) {
        index = findMin();
        cipher(index, r);
    }
    emessage[k] = '\0';

    printf("\nEncrypted message is:\n");
    printf("%s\n\n", emessage);

    // Decryption process
    emlen = strlen(emessage);
    strcpy(temp, key);
    rows = emlen / klen;

    j = 0;
    for (i = 0, k = 1; emessage[i] != '\0'; i++, k++) {
        temp2[j++] = emessage[i];
        if ((k % rows) == 0) {
            temp2[j] = '\0';
            index = findMin();
            makeArray(index, rows);
            j = 0;
        }
    }

    printf("\nArray Retrieved is:\n");
    k = 0;
    for (i = 0; i < r; i++) {
        for (j = 0; j < c; j++) {
            printf("%c ", darr[i][j]);
            retmessage[k++] = darr[i][j];
        }
        printf("\n");
    }

    retmessage[k] = '\0';
    printf("\nMessage retrieved is:\n");
    printf("%s\n", retmessage);

    return 0;
}

void cipher(int i, int r) {
    int j;
    for (j = 0; j < r; j++) {
        emessage[k++] = arr[j][i];
    }
}

void makeArray(int col, int row) {
    int i;
    for (i = 0; i < row; i++) {
        darr[i][col] = temp2[i];
    }
}

int findMin() {
    int j, min, index;
    min = temp[0];
    index = 0;
    for (j = 0; temp[j] != '\0'; j++) {
        if (temp[j] < min) {
            min = temp[j];
            index = j;
        }
    }
    temp[index] = 123; // Mark character as used
    return index;
}
```
## OUTPUT:
![Screenshot 2024-11-09 103120](https://github.com/user-attachments/assets/6619a0e6-b3f9-4814-82e6-63f1beec9b33)


## RESULT:
Thus the rail fence cipher using row column transformation technique is executed and implemented.
