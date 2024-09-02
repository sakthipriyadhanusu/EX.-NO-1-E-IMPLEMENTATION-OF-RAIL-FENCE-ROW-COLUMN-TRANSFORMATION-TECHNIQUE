# EX.-NO-1-E-IMPLEMENTATION-OF-RAIL-FENCE-ROW-COLUMN-TRANSFORMATION-TECHNIQUE

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
# Rail Fence Cipher Encryption and Decryption
def encrypt(text, key):
	rail = [['\n' for i in range(len(text))] for j in range(key)]
	dir_down = False
	row, col = 0, 0
	
	for i in range(len(text)):
		if (row == 0) or (row == key - 1):
			dir_down = not dir_down
		rail[row][col] = text[i]
		col += 1
		if dir_down:
			row += 1
		else:
			row -= 1
	result = []
	for i in range(key):
		for j in range(len(text)):
			if rail[i][j] != '\n':
				result.append(rail[i][j])
	return("" . join(result))

def decrypt(cipher, key):
	rail = [['\n' for i in range(len(cipher))] for j in range(key)]
	dir_down = None
	row, col = 0, 0
	for i in range(len(cipher)):
		if row == 0:
			dir_down = True
		if row == key - 1:
			dir_down = False
		rail[row][col] = '*'
		col += 1
		if dir_down:
			row += 1
		else:
			row -= 1
	index = 0
	for i in range(key):
		for j in range(len(cipher)):
			if ((rail[i][j] == '*') and
			(index < len(cipher))):
				rail[i][j] = cipher[index]
				index += 1
	result = []
	row, col = 0, 0
	for i in range(len(cipher)):
		if row == 0:
			dir_down = True
		if row == key-1:
			dir_down = False
		if (rail[row][col] != '*'):
			result.append(rail[row][col])
			col += 1
		if dir_down:
			row += 1
		else:
			row -= 1
	return("".join(result))

#MAIN
print("RAIL FENCE CIPHER: \n")
text = 'ENTERPRISE'
key=3
print("The Original Text: ",text)
e = encrypt(text, key)
d = decrypt(e, key)
print("CipherText: ",e)
print("Decrypted Text: ",d)
```

## OUTPUT:
![Screenshot 2024-09-02 134648](https://github.com/user-attachments/assets/5645ffc8-f7a6-42bb-8ef3-4e47365faac6)

## RESULT:
  Thus the rail fence algorithm had been executed successfully.
