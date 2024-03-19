 ## IMPLEMENTATION OF RSA
 # AIM :
 To write a C program to implement the RSA encryption algorithm.

## ALGORITHM:
STEP-1: Select two co-prime numbers as p and q.

STEP-2: Compute n as the product of p and q.

STEP-3: Compute (p-1)*(q-1) and store it in z.

STEP-4: Select a random prime number e that is less than that of z.

STEP-5: Compute the private key, d as e *
mod-1
(z).

STEP-6: The cipher text is computed as messagee *

STEP-7: Decryption is done as cipherdmod n.

## PROGRAM:
```
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

int gcd(int a, int b) {
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

void generateRSAKeys(int *n, int *e, int *d) {
    int p, q;
    printf("Enter two prime numbers: ");
    scanf("%d %d", &p, &q);

    *n = p * q;

    int phi = (p - 1) * (q - 1);


    *e = 5;

    *d = 0;
    while ((*d * *e) % phi != 1) {
        (*d)++;
    }
}

int modExp(int base, int exponent, int modulus) {
    int result = 1;
    while (exponent > 0) {
        if (exponent % 2 == 1) {
            result = (result * base) % modulus;
        }
        base = (base * base) % modulus;
        exponent /= 2;
    }
    return result;
}

int encrypt(int message, int publicKey, int modulus) {
    return modExp(message, publicKey, modulus);
}

int decrypt(int ciphertext, int privateKey, int modulus) {
    return modExp(ciphertext, privateKey, modulus);
}

int main() {
    int n, e, d;
    int plaintext;

    printf("Enter plaintext: ");
    scanf("%d", &plaintext);

    generateRSAKeys(&n, &e, &d);

    printf("Original message: %d\n", plaintext);

    int ciphertext = encrypt(plaintext, e, n);
    printf("Encrypted message: %d\n", ciphertext);

    int decryptedMessage = decrypt(ciphertext, d, n);
    printf("Decrypted message: %d\n", decryptedMessage);

    return 0;
}


```
## OUTPUT:
![image](https://github.com/Jeevapriya14/19CS412---CRYPTOGRAPHY---ADVANCED-ENCRYPTION/assets/121003043/80717dd0-fb33-4121-8985-e2c289a138b0)


## RESULT :

Thus the C program to implement RSA encryption technique had been
implemented successfully





## IMPLEMENTATION OF DIFFIE HELLMAN KEY EXCHANGE ALGORITHM

## AIM:

To implement the Diffie-Hellman Key Exchange algorithm using C language.


## ALGORITHM:

STEP-1: Both Alice and Bob shares the same public keys g and p.

STEP-2: Alice selects a random public key a.

STEP-3: Alice computes his secret key A as g
a mod p.

STEP-4: Then Alice sends A to Bob.


STEP-5: Similarly Bob also selects a public key b and computes his secret
key as B and sends the same back to Alice.


STEP-6: Now both of them compute their common secret key as the other
one’s secret key power of a mod p.

## PROGRAM: 

```

#include <stdio.h>
#include <math.h>

int power(int a, int b, int mod) {
    int result = 1;
    a = a % mod;
    while (b > 0) {
        if (b & 1)
            result = (result * a) % mod;
        b = b >> 1;
        a = (a * a) % mod;
    }
    return result;
}

void diffieHellman(int prime, int root) {
    int privateKeyA, privateKeyB;
    int publicKeyA, publicKeyB;
    int secretKeyA, secretKeyB;

    printf("Enter private key for user A: ");
    scanf("%d", &privateKeyA);
    printf("Enter private key for user B: ");
    scanf("%d", &privateKeyB);

    
    publicKeyA = power(root, privateKeyA, prime);
    publicKeyB = power(root, privateKeyB, prime);

    secretKeyA = power(publicKeyB, privateKeyA, prime);
    secretKeyB = power(publicKeyA, privateKeyB, prime);

    printf("Shared secret key computed by user A: %d\n", secretKeyA);
    printf("Shared secret key computed by user B: %d\n", secretKeyB);
}

int main() {
    int prime, root;

    printf("Enter prime number: ");
    scanf("%d", &prime);
    printf("Enter primitive root: ");
    scanf("%d", &root);

    diffieHellman(prime, root);

    return 0;
}
```
## OUTPUT:

![image](https://github.com/Jeevapriya14/19CS412---CRYPTOGRAPHY---ADVANCED-ENCRYPTION/assets/121003043/dff27e07-c1aa-45c8-8067-ec4b98eb59c5)


## RESULT: 

Thus the Diffie-Hellman key exchange algorithm had been successfully
implemented using C.





## IMPLEMENTATION OF DES ALGORITHM

## AIM:
To write a program to implement Data Encryption Standard (DES)

## ALGORITHM :

STEP-1: Read the 64-bit plain text.

STEP-2: Split it into two 32-bit blocks and store it in two different arrays.

STEP-3: Perform XOR operation between these two arrays.

STEP-4: The output obtained is stored as the second 32-bit sequence and the
original second 32-bit sequence forms the first part.

STEP-5: Thus the encrypted 64-bit cipher text is obtained in this way. Repeat the
same process for the remaining plain text characters.

### PROGRAM :

```
from cryptography.fernet import Fernet
message = input()
key = Fernet.generate_key()
fernet = Fernet(key)
encMessage = fernet.encrypt(message.encode())
print("original string: ", message)
print("encrypted string: ", encMessage)

decMessage = fernet.decrypt(encMessage).decode()
 
print("decrypted string: ", decMessage)
```
## OUTPUT:

![313462233-65fe4c9f-bfce-429c-af2d-7fb78287041d](https://github.com/Jeevapriya14/19CS412---CRYPTOGRAPHY---ADVANCED-ENCRYPTION/assets/121003043/c925d67a-caa6-4090-9a6b-54905507e01e)

## RESULT:

Thus the data encryption standard algorithm had been implemented
successfully.

