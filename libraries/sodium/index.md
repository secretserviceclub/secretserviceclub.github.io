# sodium
The popular salt-based cryptographic library from [libsodium](https://doc.libsodium.org/).\
Specializing in cryptographic practices for security various types of data.\
All data created by this library is formatted in hexadecimal for memory safety.

---
## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.random(min: number, max: number, alpha?: boolean): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.random(min: number, max: number, alpha?: boolean): string
</code>

- Creates a randomly generated string.
- If alpha is `true` then strings will be alphabets rather than hexadecimal.

---
### Hex
Hexadecimal (or "hex") is a base-16 number system commonly used to represent binary data in a compact form.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.hex.encode(input: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.hex.encode(input: string): string
</code>

- Converts data into it's hexadecimal form.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.hex.decode(input: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.hex.decode(input: string): string
</code>

- Converts hexadecimal formatted data into it's original data.

---
### Base64
Base64 is a method of encoding binary data into an ASCII string using a fixed-size alphabet, which makes it easier to transmit or store the data over media that are designed to deal with textual data.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.base64.encode(input: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.base64.encode(input: string): string
</code>

- Converts data into it's base64 form.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.base64.decode(input: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.base64.decode(input: string): string
</code>

- Converts base64 formatted data into it's original data.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.base64.xencode(input: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.base64.xencode(input: string): string
</code>

- Converts hexadecimal formatted data into it's base64 form.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.base64.xdecode(input: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.base64.xdecode(input: string): string
</code>

- Converts base64 formatted data into it's hexadecimal form.

---
### HASH
Cryptographic hash function that provides data integrity by creating a unique "fingerprint" of the input data.\
Not generally considered a cipher in the traditional sense, but rather a building block for various cryptographic protocols and algorithms.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.hash.enc256(input: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.hash.enc256(input: string): string
</code>

- Creates a SHA-256 block hash based on the input data.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.hash.enc512(input: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.hash.enc512(input: string): string
</code>

- Creates a SHA-512 block hash based on the input data.

---
### HMAC
HMAC (Hash-based Message Authentication Code) is a type of message authentication code that provides both authenticity and integrity by using a cryptographic hash function in combination with a secret key to produce a "tag" that verifies the message.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.hmac.key256(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.hmac.key256(): string
</code>

- Creates a HMAC-256 cipher key.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.hmac.enc256(input: string, key: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.hmac.enc256(input: string, key: string): string
</code>

- Creates a HMAC-256 block hash based on the input data.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.hmac.key512(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.hmac.key512(): string
</code>

- Creates a HMAC-512 cipher key.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.hmac.enc512(input: string, key: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.hmac.enc512(input: string, key: string): string
</code>

- Creates a HMAC-512 block hash based on the input data.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.hmac.key512256(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.hmac.key512256(): string
</code>

- Creates a HMAC-512256 cipher key.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.hmac.enc512256(input: string, key: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.hmac.enc512256(input: string, key: string): string
</code>

- Creates a HMAC-512256 block hash based on the input data.

---
### Signature
Digital signatures are used to provide authenticity and integrity of a cipher message.\
They use public-key cryptography and a hash function to create a unique digital signature that can be used to verify the authenticity and integrity of the message.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.signature.key(): string, string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.signature.key(): string, string
</code>

- Creates a two-pair signature key.
- Return in order of "Public Key" and "Secret Key".

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.signature.encode(input: string, sk: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.signature.encode(input: string, sk: string): string
</code>

- Encodes a message with the secret key.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.signature.decode(input: string, pk: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.signature.decode(input: string, pk: string): string
</code>

- Decodes a message with the public key.

---
### AEAD
Authenticated Encryption with Associated Data (AEAD) is a type of encryption algorithm that provides both confidentiality and authenticity for data.

#### ChaCha20Poly1305
An authenticated encryption algorithm that uses the ChaCha stream cipher for encryption and the Poly1305 message authentication code.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.chachapoly.nonce(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.chachapoly.nonce(): string
</code>

- Generates a nonce which is used in securing uniqueness.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.chachapoly.key(base?: string, salt?: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.chachapoly.key(base?: string, salt?: string): string
</code>

- Generates a key, providing a base acts as an offset, with providing a salt for greater resiliance.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.chachapoly.encrypt(input: string, key: string, nonce: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.chachapoly.encrypt(input: string, key: string, nonce: string): string
</code>

- Encrypts a messages based on the key and added nonce.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.chachapoly.decrypt(input: string, key: string, nonce: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.chachapoly.decrypt(input: string, key: string, nonce: string): string
</code>

- Decrypts a messages based on the key and added nonce.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.chachapoly.encode(input: string, key: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.chachapoly.encode(input: string, key: string): string
</code>

- Encrypts a message based on the key, this generates its own nonce internally.
- The nonce is applied to the start of the message.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.chachapoly.decode(input: string, key: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.chachapoly.decode(input: string, key: string): string
</code>

- Decrypts a message based on the key, this handles its own nonce internally.
- The nonce is applied to the start of the message.

#### GCM-256
A block cipher mode of operation called Galois/Counter Mode (GCM) that provides both confidentiality and authenticity, using a 256-bit key.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.gcm.nonce(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.gcm.nonce(): string
</code>

- Generates a nonce which is used in securing uniqueness.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.gcm.key(base?: string, salt?: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.gcm.key(base?: string, salt?: string): string
</code>

- Generates a key, providing a base acts as an offset, with providing a salt for greater resiliance.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.gcm.encrypt(input: string, key: string, nonce: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.gcm.encrypt(input: string, key: string, nonce: string): string
</code>

- Encrypts a messages based on the key and added nonce.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.gcm.decrypt(input: string, key: string, nonce: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.gcm.decrypt(input: string, key: string, nonce: string): string
</code>

- Decrypts a messages based on the key and added nonce.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.gcm.encode(input: string, key: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.gcm.encode(input: string, key: string): string
</code>

- Encrypts a message based on the key, this generates its own nonce internally.
- The nonce is applied to the start of the message.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.gcm.decode(input: string, key: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.gcm.decode(input: string, key: string): string
</code>

- Decrypts a message based on the key, this handles its own nonce internally.
- The nonce is applied to the start of the message.

#### AEGIS-256
A new authenticated encryption algorithm that is designed to be fast and secure, using a 256-bit key.\
For applications these might not be standardized yet.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.aegis.nonce(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.aegis.nonce(): string
</code>

- Generates a nonce which is used in securing uniqueness.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.aegis.key(base?: string, salt?: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.aegis.key(base?: string, salt?: string): string
</code>

- Generates a key, providing a base acts as an offset, with providing a salt for greater resiliance.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.aegis.encrypt(input: string, key: string, nonce: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.aegis.encrypt(input: string, key: string, nonce: string): string
</code>

- Encrypts a messages based on the key and added nonce.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.aegis.decrypt(input: string, key: string, nonce: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.aegis.decrypt(input: string, key: string, nonce: string): string
</code>

- Decrypts a messages based on the key and added nonce.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.aegis.encode(input: string, key: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.aegis.encode(input: string, key: string): string
</code>

- Encrypts a message based on the key, this generates its own nonce internally.
- The nonce is applied to the start of the message.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sodium.aead.aegis.decode(input: string, key: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sodium.aead.aegis.decode(input: string, key: string): string
</code>

- Decrypts a message based on the key, this handles its own nonce internally.
- The nonce is applied to the start of the message.

<div hidden>

```ts

```

</div>
