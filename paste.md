The "best" text encryption algorithm can depend on various factors, including the specific use case, security requirements, and performance considerations. However, some widely recognized and robust encryption algorithms include:

1. **AES (Advanced Encryption Standard)**: 
   - AES is a symmetric encryption algorithm that is widely used across the globe. It supports key sizes of 128, 192, and 256 bits, providing a high level of security. AES is efficient and suitable for encrypting large amounts of data.

2. **RSA (Rivest-Shamir-Adleman)**:
   - RSA is an asymmetric encryption algorithm that is commonly used for secure data transmission. It relies on the mathematical properties of large prime numbers. RSA is often used for encrypting small amounts of data, such as keys for symmetric encryption algorithms.

3. **ChaCha20**:
   - ChaCha20 is a stream cipher that is designed to be fast and secure. It is particularly effective in environments where performance is critical, such as mobile devices. It is often used in conjunction with the Poly1305 message authentication code (MAC) for authenticated encryption.

4. **Twofish**:
   - Twofish is a symmetric key block cipher that is known for its speed and flexibility. It supports key sizes up to 256 bits and is considered secure, although it is less commonly used than AES.

5. **Blowfish**:
   - Blowfish is another symmetric key block cipher that is known for its speed and effectiveness. It has a variable key length from 32 bits to 448 bits. While it is still secure, it has largely been replaced by AES in many applications.

6. **Elliptic Curve Cryptography (ECC)**:
   - ECC is a form of public key cryptography based on the algebraic structure of elliptic curves over finite fields. It offers similar security to RSA but with smaller key sizes, making it efficient for use in constrained environments.

When choosing an encryption algorithm, consider the following factors:

- **Security Level**: Ensure the algorithm is resistant to known attacks.
- **Performance**: Evaluate the speed and resource usage, especially for large datasets or constrained environments.
- **Compliance**: Check if the algorithm meets any regulatory or industry standards relevant to your application.
- **Ease of Implementation**: Consider the availability of libraries and support for the algorithm in your programming environment.

For most applications, AES is often recommended due to its balance of security and performance.