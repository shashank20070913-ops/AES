# EX-8-ADVANCED-ENCRYPTION-STANDARD ALGORITHM
# Aim:
To use Advanced Encryption Standard (AES) Algorithm for a practical application like URL Encryption.

# ALGORITHM:
AES is based on a design principle known as a substitution–permutation.
AES does not use a Feistel network like DES, it uses variant of Rijndael.
It has a fixed block size of 128 bits, and a key size of 128, 192, or 256 bits.
AES operates on a 4 × 4 column-major order array of bytes, termed the state
# PROGRAM:

#include <stdio.h>
#include <string.h>
#include <openssl/evp.h>

int main() {
    unsigned char key[16] = "1234567890123456";
    unsigned char iv[16] = "abcdefghijklmnop";

    unsigned char plaintext[] = "https://example.com";

    unsigned char ciphertext[128];
    unsigned char decryptedtext[128];

    int len, ciphertext_len;
    int decrypted_len;

    EVP_CIPHER_CTX *ctx;

    // AES Encryption
    ctx = EVP_CIPHER_CTX_new();

    EVP_EncryptInit_ex(ctx, EVP_aes_128_cbc(),
                       NULL, key, iv);

    EVP_EncryptUpdate(ctx, ciphertext, &len,
                      plaintext, strlen((char *)plaintext));

    ciphertext_len = len;

    EVP_EncryptFinal_ex(ctx, ciphertext + len, &len);

    ciphertext_len += len;

    EVP_CIPHER_CTX_free(ctx);

    // Display encrypted text
    printf("Original URL: %s\n", plaintext);

    printf("Encrypted URL: ");

    for (int i = 0; i < ciphertext_len; i++) {
        printf("%02X", ciphertext[i]);
    }

    printf("\n");

    // AES Decryption
    ctx = EVP_CIPHER_CTX_new();

    EVP_DecryptInit_ex(ctx, EVP_aes_128_cbc(),
                       NULL, key, iv);

    EVP_DecryptUpdate(ctx, decryptedtext, &len,
                      ciphertext, ciphertext_len);

    decrypted_len = len;

    EVP_DecryptFinal_ex(ctx, decryptedtext + len, &len);

    decrypted_len += len;

    decryptedtext[decrypted_len] = '\0';

    EVP_CIPHER_CTX_free(ctx);

    printf("Decrypted URL: %s\n", decryptedtext);

    return 0;
}

# OUTPUT:
<img width="405" height="137" alt="image" src="https://github.com/user-attachments/assets/47df01eb-e5de-4661-9cfb-1fa48bbefd83" />



# RESULT:


