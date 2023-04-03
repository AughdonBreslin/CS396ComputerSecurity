# CS396: Security, Privacy and Society (Fall 2022)

## Homework #2, November 29, 2022

### Aughdon Breslin and Harshdeep Aujla

#### Instructions

Please carefully read the following guidelines on how to complete and submit your solutions.

1. The homework is due on Wednesday, December 9, 2022, at 11:59pm. Starting early always helps!
2. Solutions are accepted only via Canvas, where all relevant files should be submitted as a single .zip archive. This should include your typed answers as a .pdf file and the source code of any programming possibly used in your solutions.
3. If asked, you should be able to explain details in your source code (e.g., related to the design of your program and its implementation).
4. You are bound by the Stevens Honor System. For Homework #2, you may work either by yourself or in pairs—in this case, your team names should appear clearly on your hand-in, and 2 same hand-ins are required. Any collaboration beyond this is not allowed. You may use any sources related to course materials, but information from external sources must be properly cited. Your submission acknowledges that you have abided by this policy.

#### Problem 1: Domain-extension MAC implementation (40%)

Given the provided support code in Java, implement a secure secret-key message authentication code that employs only a block cipher (and no other cryptographic primitive) to authenticate messages of any size in a bandwidth-efficient manner. In particular, as specified in the provided instructions:

1. Implement the mac() and verify() methods. (20%)

   - **Attached.**
2. Demonstrate that they are correct by providing the MAC tag (in hexidecimal) of the specified default message using the specified default key. (10%)

   - Given the key "CS-306_Test_Key" and the message "This is a test message.  There are many like it but this one is mine.", the resulting tag is "**29BA1525FA2E2E390574CEAB96BF3F3F**".
3. Explain which algorithm you implemented and why, and what are the domain-extension features of your algorithm in relation to its security. (10%)
   - Hint: Does your implementation securely handle messages of fixed size, messages of any size, or messages of any fixed size?

   - We implemented the **CBC-MAC algorithm** by iteratively creating a BLOCK_SIZE padded message block, XOR'ing it with the previous block's output as the tag, and then encrypting the block with the key until we finished the message. We used this because Cipher-Block Chaining is CPA-secure, so CBC-MAC will be **secure for fixed-length messages**. However, it is **not secure by itself for variable-length messages**, so a single key should only be used for messages of a fixed and known length. One solution to extend the domain to make it secure for variable-length messages would be to include the length of the message in the first block. The domain-extension features of this algorithm include the consecutive use of blocks, which protects against reorder, mix-and-match, or truncate attacks since the order of the message is built into the algorithm.

#### Problem 2: Data outsourcing & public-key infrastructure (30%)

To protect the secrecy of communications amongst its members, Stevens makes use of public-key encryption: Each student, faculty or staff member with Stevens UID $i$, name $n_i$ and public-key pair $(sk_i , pk_i)$, has their public key registered with a trusted certification authority ($CA$), e.g., Symantec. For efficiency reasons, the $CA$ makes the directory $D = \{(i, n_i, pk_i)|i ∈ CS396\}$ of all such public keys available for users to query via an online service at Stevens that is administered by Mallory.

Specifically (see also Figure 1):

- The CA provides Mallory with the public-key directory $D$ along with a certificate $C$, or signed digest, that is the Merkle-tree digest of the directory signed by the $CA$.
- To send a new encrypted message to Bob, Alice asks Mallory for his public key (even if Alice had recently sent encrypted messages to Bob, as public keys may be refreshed or revoked).
- Along with Bob’s public-key record $(i_B,$ Bob$, pk_B)$ in $D$, Mallory provides Alice with the current certificate $C$ and a Merkle-tree proof (i.e., hash values) corresponding to Bob’s record.
- After any change in the members of Stevens community (e.g., students joining/graduation, new hires, etc.) or any update on users’ key pairs, the $CA$ provides Mallory with the newly updated directory $D'$ and its corresponding new certificate $C'$.

1. Suppose that Cindy manages to get access to Bob’s laptop and steal its secret key $sk_B$. After Bob becomes suspicious of this, he registers a new public-key pair with the $CA$. How can Cindy collaborate with Mallory in order for Cindy to be able to decrypt all subsequent encrypted messages that are sent to Bob over an insecure channel controlled by Cindy, without anyone ever becoming suspicious about this? What two named attacks are used in this case? (15%)
   - As the question suggests, Cindy was successful in getting access to Bob’s laptop and figured out Bob’s private key that he uses to decrypt messages sent to him. Cindy can launch a series of two attacks to help her decrypt all messages sent to Bob without anyone becoming suspicious of it. The combination of two attacks that Cindy can launch are a **replay attack and a man-in-the-middle attack**. To successfully achieve this task, Cindy will have to intercept all communication coming to Bob and all queries going to Mallory. First, Cindy will need to make sure she gets Bob’s public key (the one that is associated with the private key she stole) from Mallory. She will have to keep this information safe and not lose track of it. Whenever someone tries to get Bob’s new public key from Mallory, Cindy can capture that request and send it to Mallory herself. Mallory will send Bob’s new public key to Cindy (An important step). Cindy then, instead of sending Bob’s new public key, sends everyone the old public key of bob, which is associated with the private key she stole. Now the sender will encrypt their message to bob using his old public key. Cindy then captures this message, decrypt it with the stolen private key, reads it, or copies it and encrypts it again, but this time, she encrypts the message with the new public key she got from Mallory. This message will go to Bob, and he can simply decrypt it with his new private key, and he will never know the message was compromised in transit.  
2. Describe and justify, an efficient and secure countermeasure to the above threat. You may assume that no public key will be updated twice within the same day, and that the $CA$ processes such updates in batch by reporting new directory states $(D' , C')$ only every 24 hours. (15%)
   - Even if Mallory updates the directory every 24 hours, Cindy can keep launching her combination of attacks and continue reading messages sent to Bob unless Mallory implements more security features. One major implementation that can cause Cindy to not be able to decrypt Bob’s messages is the implementation of **signed time stamps on the certificates**. The whole reason why Cindy is successful in doing what she is doing she because none of the requests or messages have any time stamp feature. The sender can never verify whether the public key they receive is up-to-date or not. Time stamps can allow these senders to see when the message was generated and whether it is authentic. Any message that has a timestamp that was stamped with significantly past time should automatically be rejected and flag something.

#### Problem 3: On the RSA cryptosystem (40%)

1. Given the support code in Python that was provided in Lab#8 (ran on November 10), implement all RSA-related algorithms. Namely, submit the completed skeleton code for Lab#8, including:
   - The algorithms that you worked (or started working) on during the Lab#8 (methods modexp, RSA enc and RSA dec); (15%)
   - The RSA key-generation algorithm (method keygen). (15%)
     - **Attached.**
2. The RSA cryptosystem relies on modular exponentiations, as its core operations.
   - How are such operations realized more efficiently in practice? (5%)
     - Modular exponentiations are realized more efficiently in practice by substituting out the power for its equivalent binary representation. For example, if the exponent was $5^{117}$, we could instead calculate the result of $5^{64+32+16+4+1}\mod19$. This is faster because each power of two can be found by multiplying two of the previous powers of two mod 19 together. For example, $5^{64}\mod19=(5^{32}\mod19)*(5^{32}\mod19)$, $5^{32}\mod19 = (5^{16}\mod19)*(5^{16}\mod19)$, and so on. To get the final answer, we only need to multiply at most $\lg(n)$ terms together to get the result of $b^n\mod{m}$.
   - Would you recommend choosing a small public exponent (e.g., e = 3, 5 or 7) so that at least message encryption and signature verification become much faster, and why? (5%)
     - Yes. Choosing a small public exponent for RSA encryption and verification is not known to create any weakness as long as the public exponent is correct in that it is relatively prime to p-1 for all primes p which divide the modulus, however it does risk weakness given other security mistakes such as not using any padding for encryption and encrypting the exact same message with multiple distinct public keys. Small public key exponents promote efficiency for public-key operations, and while having a small private exponent could lead to susceptibility against key-recovery attacks, improper padding is the main security concern. Small exponents may only be riskier to use because the negative effects of other implementation errors such as improper padding can be larger.

