# Cryptography Riddles

Below are a series of fun and challenging cryptography riddles that incorporate classic rhymes and encryption methods. The riddles will take you through different types of ciphers, hashes, and steganography. Have fun solving them!

### Riddle 1: Caesar Cipher

> **Roses are Red Violets are Blue,**
> **Caesar would be 8 is your first clue.**
> **Decrypt ********************************`ozcjmz`******************************** and enter it below,**
> **and maybe a key then might just show.**

Hint: Apply Caesar Cipher shifting the text by 8 positions backward to decrypt.

**How to Solve:**

1. Write down the alphabet.
2. Find each letter of the encrypted text (`ozcjmz`).
3. Shift each letter 8 positions backward in the alphabet:
   - `o` -> `g`
   - `z` -> `r`
   - `c` -> `u`
   - `j` -> `b`
   - `m` -> `e`
   - `z` -> `r`
4. The decrypted message is: **gruber**

---

### Riddle 2: Binary Message

> **Humpty Dumpty Sat on the Wall, Humpty Dumpty had a great Fall,**\
> **All the king's Horses and all the Kings Men couldn't decode this message for him:**
>
> `01000111 01100101 01101110 01100101 01110010 01101111`

Convert the binary code to text using ASCII to find the hidden message.

**How to Solve:**

1. Split the binary string into 8-bit chunks.
2. Convert each chunk to its corresponding ASCII character:
   - `01000111` -> `G`
   - `01100101` -> `e`
   - `01101110` -> `n`
   - `01101110` -> `n`
   - `01100101` -> `e`
   - `01110010` -> `r`
   - `01101111` -> `o`
3. The decrypted message is: **Gennero**

---

### Riddle 3: AES Encrypted Text

> **I'm a little Cipher, short and sweet.**
> **Here is my vector, and also my key.**
> **When I get all steamed up, hear me shout!**
> **Just use OpenSSL to figure me out.**

**Cipher Text:** `4qMOIvwEGXzvkMvRE2bNbg==`

**Key:** `5284A3B154D99487D9D8D8508461A478C7BEB67081A64AD9A15147906E8E8564`

**IV (Initialization Vector):** `1907C5E255F7FC9A6B47B0E789847AED`

**OpenSSL Options:**

- `-pbkdf2`
- `-nosalt`
- `-aes-256-cbc`
- `base64`

**How to Decrypt:**
To decrypt the AES encrypted text using OpenSSL, use the following command:

```
echo "4qMOIvwEGXzvkMvRE2bNbg==" | openssl enc -aes-256-cbc -d -a -nosalt -pbkdf2 -K 5284A3B154D99487D9D8D8508461A478C7BEB67081A64AD9A15147906E8E8564 -iv 1907C5E255F7FC9A6B47B0E789847AED
```

**Solution:** `takagi`

<img width="1278" alt="Screenshot 2024-11-05 at 16 43 03" src="https://github.com/user-attachments/assets/c2627ebb-aa7b-4418-8f03-28384f50093d">

---

### Riddle 4: Jack and Jill's Key Exchange

Question 1:&#x20;

> **Jack and Jill went up a Hill to use their public Keys.**\
> **Jack had 2, and Jill did too to exchange their messages with ease.**
>
> What would Jack use to send an encrypted message to Jill?

**Options:**

- Jack's Public Key
- Jack's Private Key
- Jill's Public Key
- Jill's Private Key

**Answer:** Jack would use **Jill's Public Key** to encrypt the message, which only Jill could decrypt with her private key. This represents the fundamental concept of asymmetric encryption used in public key cryptography.

**Question 2:** What would Jill use to decrypt Jack's message?

**Options:**

- Jack's Public Key
- Jack's Private Key
- Jill's Public Key
- Jill's Private Key

**Answer:** Jill would use **Jill's Private Key** to decrypt Jack's message.

**Question 3:** Jack and Jill invited Bob, Alice, Tim, and Peter along to exchange some messages. How many keys would they all need for asymmetric vs symmetric encryption?

**Options:**

- 12 Asymmetric and 15 Symmetric
- 15 Asymmetric and 12 Symmetric
- 6 Asymmetric and 15 Symmetric
- 10 Asymmetric and 15 Symmetric
- 12 Asymmetric and 30 Symmetric

**Answer:** They would need **12 Asymmetric and 15 Symmetric** keys.

**Question 4:** Tim just sent an encrypted message to one of his friends, which of the following keys did he likely use to encrypt the message?

**Options:**

- Tim's Public Key
- Alice's Public Key
- Bob's Private Key
- Peter's Private Key
- Tim's Private Key

**Answer:** Tim likely used **Alice's Public Key** to encrypt the message.

---

### Riddle 5: MD5 Hash

> **Hey diddle diddle, the cat and the fiddle,**\
> **The cow jumped over the moon.**\
> **The little dog laughed when it found this MD5 hash,**\
> **And the dish ran away with the spoon!**
>
> **HASH:** `3b75cdd826a16f5bba0076690f644dc7`

&#x20;Passwords: `3b75cdd826a16f5bba0076690f644dc7:argyle`

<img width="732" alt="Screenshot 2024-11-05 at 16 37 54" src="https://github.com/user-attachments/assets/5ee8c17e-adb0-499f-a5a0-80f950297003">


---

### Riddle 6: Steganography with Mary

> **Mary had a secret code,**\
> **Hidden in a photo,**\
> **And everywhere that photo went,**\
> **The code was sure to go.**
>
> **She wrote the passphrase on the book, to access the code**\
> **You just need to use some stego tricks and the secret will be showed.**

Use `steghide` with the passphrase to extract the hidden text from `mary-lamb.jpg`.

**Command Example:**

```
  steghide extract -sf mary-lamb.jpg -p "ABC"
```

The hidden message inside the file is **mcclane**.

![mary-lamb](https://github.com/user-attachments/assets/3f3b3915-87d8-4847-aafb-e3143b277b13)
<img width="1154" alt="Screenshot 2024-11-05 at 15 39 28" src="https://github.com/user-attachments/assets/de0e0ad6-6381-47a6-a10a-ac966d5e8449">


---


