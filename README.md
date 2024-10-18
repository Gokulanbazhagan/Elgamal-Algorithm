# Exp 12-IMPLEMENT ELGAMAL CRYPTOGRAPHY

## AIM:
To write a program to implement Elgamal Algorithm. ALGORITHM:
STEP-1: Input large prime number, base, and private key
STEP-2: Calculate the public key
STEP-3: Input message to encrypt
STEP-4: Input random ephemeral key
STEP-5: ElGamal
## PROGRAM:
```
#include <stdio.h>
#include <math.h>
#include <stdlib.h>

// Function to perform modular exponentiation: (base^exp) % mod
int mod_exp(int base, int exp, int mod) {
    int result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1) {
            result = (result * base) % mod;
        }
        exp = exp >> 1; // exp = exp / 2
        base = (base * base) % mod;
    }
    return result;
}

// Function to calculate GCD of two numbers
int gcd(int a, int b) {
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

int main() {
    int p, g, x; // p = large prime, g = primitive root, x = private key
    int h, y; // h = public key (h = g^x mod p), y = ephemeral key
    int message, k; // message to encrypt, k = random integer (ephemeral key)
    int c1, c2, decrypted_message; // Ciphertext components and decrypted message

    printf("\n\n *******Elgamal encryption and decryption*******\n");
    printf("\n DEVELOPED BY : DEVADARSHAN A S\n");
    printf(" REG NO : 212222110007\n\n");

    // Get the large prime number p, base g, and private key x
    printf("Enter a large prime number (p): ");
    scanf("%d", &p);
    printf("Enter a primitive root of p (g): ");
    scanf("%d", &g);
    printf("Enter the private key (x): ");
    scanf("%d", &x);

    // Calculate the public key h = (g^x) % p
    h = mod_exp(g, x, p);
    printf("Public key (h) = %d\n", h);

    // Get the message to encrypt
    printf("Enter the message to encrypt (as an integer less than p): ");
    scanf("%d", &message);

    // Generate the random ephemeral key k such that gcd(k, p-1) = 1
    do {
        printf("Enter the ephemeral key (k) such that gcd(k, p-1) = 1: ");
        scanf("%d", &k);
    } while (gcd(k, p - 1) != 1);

    // ElGamal encryption
    c1 = mod_exp(g, k, p); // c1 = (g^k) % p
    c2 = (message * mod_exp(h, k, p)) % p; // c2 = (message * h^k) % p
    printf("Ciphertext (c1, c2) = (%d, %d)\n", c1, c2);

    // ElGamal decryption
    int inverse = mod_exp(c1, p - 1 - x, p); // (c1^(p-1-x)) % p
    decrypted_message = (c2 * inverse) % p; // decrypted_message = (c2 * (c1^(p-1-x))) % p
    printf("Decrypted message = %d\n", decrypted_message);

    return 0;
}


```
## OUTPUT :
![Screenshot 2024-10-18 134300](https://github.com/user-attachments/assets/892a3acd-2dab-4e1e-bca1-13094690e861)



## RESULT :
Thus the Elgamal algorithm had been implemented successfully.
