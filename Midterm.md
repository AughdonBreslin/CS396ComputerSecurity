# Midterm

4 questions; each question has 4 parts. Part 1 is short answer, parts 2 & 3 are multiple choice, Part 4 is True/False.

[toc]

## Lecture 1 Irrelevant

## Lecture 2 - CIA Triad

CIA triad

- Confidentiality
  - Asset is viewed only by authorized parties
- Integrity
  - Asset is modified only by authorized parties
- Accessibility
  - Asset can be used by any authorized parties

Secure Outsourced Computation

- Threats
  - Misconfigurations, erroneous failures, limited liability
  - Compromises, attacks, 

## Lecture 3 Irrelevant

## Lecture 4 - Vulnerability, Threat, Security Control

Defenders

- System owners seek to enforce one or more security properties or defeat certain attacks

Attackers

- External entitities seek to launch attacks that break a security property

Vulnerability - Threat - Control Paradigm

- Vulnerability
  - A weakness that could be exploited to cause harm

- Threat
  - A set of circumstances that could cause harm

- Security control
  - A mechanism that protects against harm


Difference between Vulnerability and Threat

- Threat is a person or event that has the potential to negatively impact a resource
- Vulnerability is that quality of a resource that allows the threat to be realized

## Lecture 5 - Threat v.s. Vulnerability, Symmetric Key

Threats

- Eavesdropping
  - Interception of information intended for someone else

- Alteration
  - Unauthorized modification of information

- Denial of Service
  - Interruption or degradation of data service

- Masquerading
  - Fabrication of information that is claimed to be from someone else

- Repudiation
  - Denial of a commitment or data receipt
    - Ex: Making a deal, then claiming it never happened


Vulnerabilities

- Insecure communication channel
- Software bugs
- Weak authentication

Security Controls

-   "Method - Opportunity - Motive" View
    -   Deny any of them and the attack will likely fail

-   HTTPS Protocol
-   RAID Technology
-   TOR Protocol

Symmetric Key Encryption

- Encryption is to protect Confidentiality and Integrity
- Schema
  - $m \in M$, (Gen, Enc, Dec) algos.
    - Gen, Enc are probabilistic, but Dec must be deterministic
    - Gen outputs a uniformly random key $k \in K$. 

  - Alice encrypts her message $m$ to ciphertext $c$, which is then sent.
  - Bob decrypts received ciphertext $c$ to original message $m$.
  - Eve can intercept $c$ but cannot learn $m$ from $c$.
  - Alice and Bob share a secret key $k$ from Gen that allows them to encrypt and decrypt.

- Kerckhoff's Principle: The cipher method must not be required to be secret, and it must be able to fall into the hands of the enemy without inconvenience.
  - Reasoning:
    - Due to security & correctness, Alice & Bob must share some secret info
    - If no shared key captures this secret info, it must be captured by Enc, Dec
    - But, keeping Enc, Dec secret is problematic
      - Harder to keep secret an algorithm than a short key
      - Harder to change an algorithm than a short key
      - Riskier to rely on custom/ad-hoc schemes than publicly scrutinized/standardized ones

Brute Force Attacks

- Generic Attack
  - Given a captured ciphertext $c$ and known key space $K$, $Dec$
  - Strategy is an exhaustive search
    - For all possible keys $k \in K$, determine if $Dec(c,k)$ is a likely plaintext $m$.
  - Requires some knowledge on the message space $M$.
    - i.e., structure of the plaintext (e.g. PDF file or email message)
- Countermeasure
  - key should be a random value from a sufficiently large key space $K$ to make exhaustive search attacks infeasible

## Lecture 6 - Classical Ciphers & Perfect Secrecy

Classical Ciphers

- Substitution Cipher
  - Obliterated by basic frequency analysis
- Caesar Cipher
  - Obliterated by brute force

Perfect Secrecy

- The adversary should not be able to learn **any additional** information on $m$.
  - We cannot hide prior knowledge about the message.

- A posteriori = A priori
  - Information after looking is the same as the information known before looking
  - $P(M=m|C=c)=P(M=m)$: Probability that $M=m$ given $C=c$ is the same as the probability that $M=m$.

- C is independent of M
  - $P(Enc_K(m)=c)=P(Enc_K(m')=c)$: The probability that $Enc_k(m)=c$ is the same as the probability that any other $Enc_k(m')=c$. 


## Lecture 7 - One Time Pad

One-Time Pad

- Strategy
  - Let $n$ = number of plaintext messages.
    Let $M$ = message space, with bit-strings of length $n$.
    Let $K$ = key space, with bit-strings of length $n$.
    - Note the key must be as long as the message!

  - Fix $n$ to be any positive integer; set $M=C=K=\{0,1\}^n$.
    - Gen: Choose $n$ bits uniformly at random $P(bit=1)=0.5$.
      - $Gen \rightarrow \{0,1\}^n$

    - Enc: Given an equal-length key and message, compute their bit-wise XOR.
      - $Enc(k,m)=Enc_k(m)=k \oplus m$

    - Dec: Compute the bit-wise XOR of the key and ciphertext
      - $Dec(k,m)=Dec_k(m)=k \oplus c$

  - This works because: $k \oplus c = k \oplus k \oplus m = 0 \oplus m = m$.

- Perfectly secure
  - C is independent of M due to Gen algorithm.

- Impractical
  1. The key has to be as long as the plaintext
  2. The key cannot be reused

## Lecture 8 - Formal Treatment

Formal Treatment in Modern Cryptography

- Problem is formulated in terms of
  1. Formal Definitions
     - Rigorous description of security problem (to be considered, designed, achieved)
     - Computing setting, underlying cryptographic scheme, desired properties
  2. Precise Assumptions
     - Precise description of all relevant problem components
     - Adversary, computational assumptions, computing setting
  3. Provable Security
     - Subject to above assumptions, scheme is proved to be secure according to above definitions.

Possible Eavesdropping Attacks

- Collection of ciphertexts (EAV)
  - *Plain* threat model

- Collection of plaintext/ciphertext pairs
  - Known Plaintext Attack (KPA)

- Collection of plaintext/ciphertext pairs for chosen plaintexts
  - Chosen Plaintext Attack (CPA)
  - *Advanced* Threat Model
- Collection of plaintext/ciphertext pairs for chosen ciphertexts
  - Chosen Ciphertext Attack (CCA)


Computational Security

- Difference between perfect secrecy and computational security
- Perfect Secrecy: Requires that
  - the ciphertext leaks absolutely no extra information about the plaintext
  - to adversaries of unlimited computational power
- Computational Security: A relaxed notion of security requires that
  - the ciphertext leaks a tiny amount of extra information about the plaintext
  - to adversaries with bounded computational power

Three Equivalent Looks of Perfect Secrecy

- a posteriori = a priori
- C is independent of M
- Indistinguishability

## Lecture 9 - PRGs and Stream/Block Ciphers

Pseudorandomness

- In perfectly secret cipher, ciphertext appears to be **truly random**.
- When security is computational, ciphertext appears to be **pseudorandom**.
  - It cannot be efficiently distinguished from truly random.


Pseudorandom Generators (PRGs)

- Input a seed $s \in \{0,1\}^t$, output $G(s) \ in \{0,1\}^{l(t)}$, where $l(t)$ is a polynomial and $\forall n,  l(n)>n$.
- PRG requires:
  - Expansion
  - Pseudorandomness

Pseudorandom Functions

- Block Ciphers
  - Want **random** mapping of n-bit inputs to n-bit outputs for $2^{n2^n}$ possible mappings.
  - Instead, we get a random key that selects a **random-enough** mapping with keyed function $F_k:\{0,1\}^n \rightarrow \{0,1\}^n$.

Modes of Operations -- high level and security aspect

- ECB - Electronic Code Book

  - Each plaintext string goes to a different block and gets encrypted with a key
  - Insecure, of only historic value
  - Deterministic
    - Produces the same ciphertext on the same plaintext (given the same key)
  - Not CPA or even EAV-secure

- CBC - Cipher Block Chaining
  - Previous block's ciphertext is "mixed" with current block's plaintext
    - Each plaintext block is encrypted as $C[i]=Enc_k(C[i-1] \oplus P[i])$.

    - Each ciphertext block is decrypted as $P[i]=C[i-1] \oplus Dec_k(C[i])$.

  - $C[0]$ is a random initialization vector transmitted separately

  - CPA-secure if $F_k$ is a permutation

- Chained CBC
  - Use last block ciphertext of current message as independent variable of next message

  - Saves bandwidth but not CPA-secure

- OFB - Output Feedback
  - No need for the message length to be a multiple of $n$
  - Resembles synchronized stream-cipher mode
  - CPA-secure if $F_k$ is a pseudorandom function

- CTR - Counter mode
  - No need for message length to be a multiple of $n$
  - Resembles synchronized stream-cipher mode
  - CPA-secure if $F_k$ is a pseudorandom function
  - No need for $F_k$ to be invertible
  - Parallelizable



Stream vs. Block Ciphers

- Advantages/Disadvantages
  |               | Stream                                                       | Block                                                      |
  | ------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
  | Advantages    | Speed of transformation<br />Low error propagation           | High diffusion<br />Immunity to insertion of symbol        |
  | Disadvantages | Low diffusion<br />Susceptibility to malicious insertions and modifications | Slowness of encryption<br />Padding<br />Error propagation |

Techniques used in practice for Symmetric Encryption

- Substitution
  - Exchanging one set of bits for another set
- Transposition
  - Rearranging the order of the ciphertext bits to break any regularities in the underlying plaintext
- Confusion
  - Enforcing complex functional relationship between the plaintext/key pair and the ciphertext
- Diffusion
  - Distributes information from single plaintext characters over entire ciphertext output

DES v.s. AES

- AES lets you choose a 128-bit, 192-bit, or 256-bit key, making it exponentially stronger than DES's 56-bit key
- They're both symmetric block ciphers
- DES uses 64-bit block sizes while AES uses 128-bit

## Lecture 10 - Message Authentication

Message Authentication

- to protect the integrity of the message
- Information has value, but only when it's correct
  - Altered data could be useless or harmful


Security Problems Studied by Modern Cryptography

Integrity of Communication/Computations

- Any unprotected system can't be trusted
- Prevention and Detection
  - Stopping messages from being altered, and
  - Detecting whether messages have been altered are both important

Message Authentication Codes (MACs)

- Communication over unprotected channel
- Solution Concept: Symmetric-key message authentication
  - Secretly annotate or "sign" message so that it is unforgeable while in transit
  - Alice tags her message $m$ with tag $t$, which is sent along with plaintext $m$
    - Tag $t$ is generated as such: $t \leftarrow Mac_k(m)$.
  - Bob verifies authenticity of received message using tag t
  - Mallory can manipulate m, t, but "cannot forge" a fake verifiable pair m',t'.
    - Verification Algorithm: $b = V_k(m,t)$
  - Alice and Bob share a secret key k that is used for both operations
- MAC is defined as:
  - A message space $M$, and
  - A triplet of algorithms $(Gen,Mac,Vrf)$.
    - Gen, Mac are probabilistic, Vrf is deterministic


MAC Security

- MAC is secure if any computationally bounded attacker wins the game only negligibly often.

Replay Attacks

- Real-life attacker
  - Aims to insert an invalid but verifiable message $m^*, t^*$ into stream of messages
    - Forged message could be:
      - New: Attacker wins!
      - previously observed: Replay attack

  - Launch a brute-force attack (given that $Mac_k(m) \rightarrow t$ is publicly known)
    - Given any observed pair $(m,t)$, exhaustively search key space to find the used key $k$.


MAC Constructions

- Fixed-length MAC
  - Direct application of a PRF for tagging
  - Otherwise, pretty limited applicability

- Domain extension for MACs
  - Straightforward secure extension of fix-length MAC, but
  - Inefficient

- CBC-MAC
  - Resembles CBC-mode encryption
  - Efficient
  - Can authenticate longer messages than basic PRF-based schemes


## Lecture 11 - Hash Functions

Hash Functions

- Maps arbitrarily long objects to fixed-length binary strings

- Core Security Property: Mapping avoids collisions
  - Collisions: Distinct objects that map to the same hash value
  - Collision-resistance

Design Framework

- Merkle-Damgard Design/Definition
  - Suppose that $h:\{0,1\}^{2n} \rightarrow \{0,1\}^n$ is a collision-resistant compression function. Consider the general hash function $H:M=\{x:|x|<2^n\}\rightarrow \{0,1\}^n$, defined as follows:
  - $H(x)$ is computed by applying $h()$ in a chained manner over $n$-bit message blocks.
    - Pad $x$ to define a number $B$ of message blocks $x_1,...,x_B$, with $|x_i|=n$
    - Set an extra, final message block $x_{B+1}$ as an $n$-bit encoding $L$ of $|x|$
    - Starting by initial digest $z_0=0^n$, output $H(x)=z_{B+1}$, where $z_i=h^s(z_{i-1}||x_i)$ 

  - Basically chain the output of one hash function as an input of another


Generic Attacks

- Brute-force attack
  - For each string $x$ in the domain:
    - Compute and record hash value $h(x)$
    - If $h(x)$ equals a previous recorded hash $h(y)$, where $x \ne y$, then halt and output collision on $x \ne y$

- Birthday Attack

  - Use a randomized search rather than an exhaustive search because we don't care what $x$ or $y$ are, just that they map to the same hash value
    - Birthday Paradox states (assuming uniform birthday distribution) "In any group of 23 people, there's a ~53% chance that two people in that group have the same birthday."
  - Which means that for large $m=2^n$ where m is the number of possible outputs based on $n$ bits, the average number of hash evaluations to find the first collision is $1.25\sqrt{m}$.

Applications of Hashing to Security

- MD5
  - Output 128 bits, which is now too small to feasibly prevent collision resistance.

- SHA1 - Secure Hash Algorithm
  - Output 160 bits, considered insecure for collision resistance

- SHA2-$n$
  - Outputs $n$ bits, no real security concerns yet

- SHA3
  - Completely new philosophy allows for sponge construction and unkeyed permutations

- Fairness
  - A general issue with concealing private data via hashing
    - Due to small search space, this protocol is not secure!
    - Forward search attack
  - Increase search space to prevent

Well-Known Hash Functions

- MD5, All the SHAs
  - Know the differences, approaches

- Current hash standards

## Lecture 12 - Public Key Certificate

From Symmetric to Asymmetric Message Authentication

- Secret-Key Message Auth (MAC)
  - Main Limitation: Session-specific keys
- Public-Key Message Auth (Digital Signature)
  - Main Flexibility: User-specific keys
  - Only messages signed by sender's SK can be verified by sender's PK

Public-Key Certificates

- A public key and an identity bound together
- Signed by Certificate Authority

Certificate Authority

- Person that users trust to securely bind identity to public keys
  - CA verifies identities before generating certificates
  - Secures binding via digital signatures

Certificate Hierarchy

- Trusted root certificate authorities sign certificates for lower-level CAs

NOTHING FROM HYBRID ENCRYPTION AND AFTER