# Final Review

only multiple choice and true false

### Lecture 12/13 - Public Key Cryptography

Benefits of Public Key Cryptography:

- No need to securely share secret keys.
- User specific keys provide more flexibility than session specific keys (which are used in secret key encryption).

Limitations of Symmetric Key Encryption

- Session specific keys means a new key is needed for every session, rather than per user.
- For every session, a secret key must be securely distributed between parties.
  - A secure channel must be established every session

Symmetric Crypto vs. Asymmetric Crypto

- Symmetric Crypto
  - Key Management
    - Less scalable and riskier
  - Assumptions
    - Secret and authentic communication
    - Secure storage
  - Primitives
    - Generic assumptions
    - More efficient in practice
- Asymmetric Crypto
  - Key Management
    - More scalable and simpler
  - Assumptions
    - Authenticity (PKI)
    - Secure storage
  - Primitives
    - Math assumptions
    - Less efficient in practice (2-3 o.o.m)

Secret-Key vs. Public-Key Encryption

|                   | Secret Key (Symmetric)                                       | Public Key (Asymmetric)                                      |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Number of Keys    | 1                                                            | 2                                                            |
| Key Size (bits)   | 56-112 (DES), 128-256 (AES)                                  | Unlimited, typically no less than 256; 1000 to 2000 currently considered desirable for most uses |
| Protection of Key | Must be kept secret                                          | One key must be kept secret; the other can be freely exposed |
| Best Uses         | Cryptographic workhorse. Secrecy and integrity of data, from single characters to blocks of data, messages, and files | Key exchange, authentication, signing                        |
| Key Distribution  | Must be out-of-band (Authentication that requires the communication channels used to authenticate a users to be separate from the channel used to sign in or do transactions) | Public keys can be used to distribute other keys             |
| Speed             | Fast                                                         | Slow, typically by a factor of up to 10,000 times slower than symmetric algorithms |

Digital Certificates

- A certificate is a public key and an identity bound together in a document signed by a Certificate Authority (CA). A CA is an entity that users trust to securely bind identities to public keys. A CA verifies identities before generating certificates for these identities.

Hybrid Encryption

- "Reduces" secret key cryptography to public key cryptography. Hybrid encryption performs better than block-based public key CPA-encryption.
- Main Idea
  - Apply PK encryption to a random key $k$, then use $k$ for secret encryption of message $m$.
    - Sender generates a fresh session-specific secret key $k$ and learns receiver's public key $R_{pk}$.
    - Session key $k$ is sent to receiver under key $R_{pk}$.
    - Session key $k$ is employed to run symmetric-key crypto.

Discrete Log Problem

- For groups of specific structure, solving the discrete log problem is infeasible. Any efficient algorithm finds discrete logs negligibly often ($P=2^{\frac{-t}2}$, where $t$ is the length of the prime generated), so brute force attacks operate in $O(2^{\frac{-t}2})$.

### Lecture 14 - System Security

Authentication vs Authorization

- Authentication: Proving who user claims to be
  - Authentication $\ne$ Identification
  - Authentication and Identification through username and password provide unilateral authentication
- Authorization: Enforcing the access control (eligibility)
  - Checking the user's privileges.
  - Determines whether a user should be able to access certain information

- Hashing passwords is not enough, user specific salting is usually added to slow down dictionary attacks. Hashing a password multiple times is another method to slow down dictionary attacks.

Authentication Through Biometrics

1. Identification: 1:n comparison, i.e. identify user from a database of $n$ persons
2. Verification: 1:1 comparison, i.e. check whether there is a match for a given user

Authentication Through Tokens

1. Physical tokens like a key card or ID tags can be lost or stolen.
2. Can be combined with password (something you know) to create 2 factor authentication (or multi factor authentication)

Methods

- Something user *knows*, *is*, or *has*

Countermeasures

- User specific salt
- Biometric Identification

Access Control (AC)

![image-20221216170109501](C:\Users\aughb\AppData\Roaming\Typora\typora-user-images\image-20221216170109501.png)

- Reference monitor
  - Verifies the identity of the principal making the request, and decides whether access is granted or denied

- Must distinguish between the three concepts:
  - User: A user is a person who interacts with a computer system or application.
    - Users can be classified into different categories, such as end users, who are the individuals who directly use the system or application, and system administrators, who are responsible for managing and maintaining the system or application.
  - Principal: An entity that can be authenticated and authorized to perform certain actions within a system.
    - A principal can be a user, a group of users, or a computer process.
  - Subject: An entity that can perform actions within a system or application.
    - Subjects are often associated with access control and security, and can include users, processes, or other entities that are authorized to perform certain actions within the system.

### Lecture 15 - Legal & Ethical Issues

Copyright

- Designed to protect the expression of ideas.
- It gives the author the exclusive right to make copies of the expression and sell them to the public.

Patent

- Designed to protect inventions, tangible items, or ways to make them.
- Patents were intended to apply to the results of STE rather than arts and writing.

Trade secret

- Information that gives one company or organization a competitive advantage over others.

Comparing Copyrights, Patents, and Trade Secrets

|                              | Copyright                                                | Patent                                        | Trade Secret                      |
| ---------------------------- | -------------------------------------------------------- | --------------------------------------------- | --------------------------------- |
| Protects                     | Expression of idea, not idea itself                      | Invention: The way something works            | A secret, competitive advantage   |
| Protected Object Made Public | Yes; intention is to promote publication                 | Design filed at Patent Office                 | No                                |
| Requirement to Distribute    | Yes                                                      | No                                            | No                                |
| Ease of Filing               | Very easy, do-it-yourself                                | Very complicated; specialist lawyer suggested | No filing                         |
| Duration                     | Varies by country; Approximately 75-100 years is typical | 19 years                                      | Indefinite                        |
| Legal Protection             | Sue if unauthorized copy sold                            | Sue if invention copied                       | Sue if secret improperly obtained |



Computer Crime

- Hard to prosecute due to: lack of domain understanding by courts, lack of physical evidence, complexity of cases, the victim (e.g. banks) may choose not to prosecute in order to not lose trust of their customers

Compare Law and Ethics

| Law                                                 | Ethics                                                       |
| --------------------------------------------------- | ------------------------------------------------------------ |
| Described by formal, written documents              | Described by unwritten principles                            |
| Interpreted by courts                               | Interpreted by each individual                               |
| Established by legislatures representing all people | Presented by philosophers, religions, professional groups    |
| Applied to everyone                                 | Chosen personally                                            |
| Priority determined by courts if two laws conflict  | Priority determined by an individual if two principles conflict |
| "Right" arbitrated finally by court                 | Not arbitrated externally                                    |
| Enforced by police and courts                       | Enforced by intangibles such as principles and beliefs       |

### Lecture 16 - Network Security (FOCUS)

Network Security

- Distributed Denial of Service Attack (DDoS)
  - Targets availability by denying users access to authorized data or services that should be available to them
  - May breach integrity and confidentiality as services/data are modified or accessed by an unauthorized party
- DYN Distributed Denial of Service Attack (DYN DDoS)
  - Only targets availability by crashing the primary server of DNS through sending gibberish queries that are guaranteed to not be cached by a secondary DNS server
- Domain Name Service (DNS)
  - Resolves domain names to IP addresses
  - All CIA Triad Properties are relevant:
    - Confidentiality
      - Must protect database entries that are not queried, or else and attacker may find out the structure of a target organization (e.g. zone enumeration attack)
    - Integrity
      - Must critically be trustworthy, or else connections to malicious sites may occur (e.g. DNS-spoofing attacks).
    - Availability
      - Must critically be available at all times, or else it won't always be guaranteed that your browser can connect to sites.
- DNS/IP Spoofing
  - An attacker poses as the DNS server in order to redirect the user to malicious sites

DNSSEC

- DNSSEC solved IP spoofing
- Security extensions of DNS protocol to to protect integrity of DNS data
- Each DNS entry is pre-signed by primary name server. This extension solves DNS Spoofing.

NSEC

- NSEC solved proof for denial of existence
- Lexicographically ordered and then each pair of neighboring existing domain names is pre-signed by the primary name server. Non-existing names are provided by providing this pair "containing" missed query names. This protocol however, leaks information about other domain names, and is therefore still vulnerable to zone enumeration attacks. Eventually this problem is solved in NSEC3 and NSEC5. 

How is Service Denied in a DDoS Attack

- Flooding, Application Based, Disabled Communications, Hardware/software failure

Cloud Computing

- Software as a Service (SaaS)
  - The cloud provider gives the customer access to applications running in the cloud
- Platform as a Service (PaaS)
  - The customer has their own applications, but the cloud provides the language and tools for running them
- Infrastructure as a Service (IaaS)
  - The cloud provider offers processing, storage, networks, and other computing resources that enable customers to run any kind of software.

Cloud Based Security Benefits

- Geographic Diversity
  - Many cloud providers run data centers in disparate geographic locations and mirror data across locations, providing protection from natural and other local disasters.

- Platform and Infrastructure Diversity
  - Different platforms and infrastructures mean different bugs and vulnerabilities, which makes a single attack or error less likely to bring a system down.

- Using cloud services as part of a larger system is a good way to diversify your technological stack.

Cloud-based Security Functions

- Email filtering
  - Since email is already hopping through a variety of SMTP servers, adding a cloud-based email filter is as simple as adding another hop

- DDoS Protection
  - Cloud based DDoS protection services update your DNS records to insert their servers as proxies in front of yours. They maintain sufficient bandwidth to handle the flood of attack traffic.

- Network monitoring
  - Cloud-based solutions can help customers deal with steep hardware requirements and can provide monitoring and incident response

### Lecture 17 - Software Security

Buffer Overflow

- Based on programmers' oversights (or programming language vulnerabilities)\
- Exploited by attackers inputting more data than expected (overflowing the buffer (roll credits))
- In the best case scenario, this can result in unauthorized access or privilege escalation that allows the attacker to run maliciously written code at a higher privilege level.

Attack Structure 

1. write malicious code
2. inject the malicious code into the memory of the target program
3. jump to and execute the malicious code

"Nopsled" Technique

- The use of many "no-operation" commands, carefully interleaved with a number of "relative jump" commands, so that a wider range of guessed values, injected as the return address of the function call in which the buffer overflow occurred, can lead to a successful execution of the injected malicious code.

Mediation

- Verifying that the subject is authorized to perform the operation on an object.
- When mediation is incomplete, unauthorized parties may be able to perform operations on objects they should not have access to.

Race Condition

- Threads; give one slot to two different people

Malware

- Programs planted by an agent with malicious intent to cause unanticipated or undesired effects

  | Code Type                                     | Characteristics                                              |
  | --------------------------------------------- | ------------------------------------------------------------ |
  | Virus                                         | Code that causes malicious behavior and propagates copies of itself to other programs |
  | Trojan Horse                                  | Code that contains, unexpected, undocumented, additional functionality |
  | Worm                                          | Code that propagates copies of itself through a network; impact is usually degraded performance |
  | Rabbit                                        | Code that replicates without limit to exhaust resources      |
  | Logic bomb                                    | Code that triggers action when a predetermined condition occurs |
  | Time bomb                                     | Code that triggers action when a predetermined time occurs   |
  | Dropper                                       | Transfer agent code only to drop other malicious code, such as virus or Trojan horse |
  | Hostile mobile code agent                     | Code communicated and semi-autonomously by programs transmitted through the web |
  | Script attack, JavaScript, active code attack | Malicious code communicated in JavaScript, ActiveX, or another scripting language, downloaded as part of displaying a web page. |

### Lecture 18 - Database Security

Database Security

- Databases store data and provide information to their users. It is important to ensure users update or retrieve information in a reliable and controlled manner.

CIA Properties

- Confidentiality
  - Protect sensitive data and disallow unauthorized leakage of information
- Integrity
  - Ensure data integrity and guarantee correctness/consistency of authorized operations
- Availability
  - Allow database access and ensure authorized access at all times

Confidentiality & Integrity Requirements

- Physical/logical/element Integrity
  - Ensure reliability, protect against failure, updates don't change DB schema, elementary data are inserted with correct/accurate values
- Data/privacy Protection
  - Protect against unauthorized disclosure of information and server breaches

SQL Injection

- An SQL injection attack involves placing SQL statements in the user input. When done to unsanitized inputs the attacker can execute SQL instructions from the input in the form
- How to use query to inject code
  - SELECT * FROM Users WHERE user='\$username' AND pwd='\$password'
  - SELECT * FROM Users WHERE user='M' OR '1=1' AND pwd='M' OR '1=1'

- Use to bypass authentication
  - Solution is to filter out single quote characters in the input


### Lab 10

Q1: A certain type of computer misuse that is against the law was detected coming from Bob's password-protected account. Without any further evidence, is Bob liable or not, and why?

- Yes. The computing system cannot distinguish between possible impersonation or delegation.

Q2: A password is a secret that can both be refreshed and shared: Users can change their passwords or willingly give them to friends or family, if needed. How does user authentication based on fingerprints compare with user authentication using the RSA token, with respect to the ability of the users to refresh or share their underlying secrets? You may assume that the RSA token produces new pseudorandom token codes by repeatedly applying SHA2 over the current token code, starting with an initial secret token code, or secret seed, that i hard coded in the token and also known to the user at the time of registration.

- Neither token codes nor fingerprints can be refreshed but they can both be shared. Fingerprints, at least theoretically, assuming some highly sophisticated technology.

Q3: How does fingerprint-based biometric authentication compare with password-based authentication with respect to the ability of users to refresh or share their underlying secrets?

- Passwords can be both refreshed and shared, but fingerprints can neither be refreshed nor shared

Q4: What motivated the design of public-key encryption and digital signatures?

- The need to increase the flexibility of a multi-user cryptographic system with respect to its key-management; instead of relying on session-specific shared secret keys, the use of user-specific public-key pairs removed the need for out-of-band secret communication in order to distribute shared secret keys.

Q5: What best describes the term "digital certificate"?

- Digital certificates constitute the prevalent way with which we implement a public-key infrastructure, wherein users' public keys are verified to be the currently correct/valid ones via a chain of verified signatures while using minimal trust assumptions about certain users' public keys (Certificate Authorities).

Q6: What is a consequence of encrypting files prior to their upload to a cloud-storage provider that employs deduplication?

- Depending on the type of the encryption, it may negate any storage benefits due to deduplication.

Q7: How does protocol DNSSEC compare to ordinary DNS?

- DNSSEC has all DNS records individually signed by a corresponding authoritative DNS server (a TLD server responsible for a top-level domain zone), thus tolerating IP spoofing attacks.

Q8: How does protocol NSEC compare to protocol DNSSEC?

- NSEC provides verifiable answers also for queried domain names that do not resolve to any IP addresses.

Q9: Stevens has recently updated its user-authentication system by adopting the use of Honeywords and a remote, cloud-based, server as HoneyChecker. Due to a large-scale DDoS attack against the cloud provider hosting the HoneyChecker, Stevens operates for an entire weekend without access to this server. What best describes the security of Stevens' authentication system during this period?

- The security of the system is reduced, falling back to the levels provided by the system prior to the adoption of Honeywords, because theft of password files can no longer be detected. This is why Honeywords strictly improve security.

Q10: Which of the following can be patented?

- A new encryption scheme that I have invented and that I presented at a conference sometime within the last 12 months.

Q11: A new product makes use of "security by obscurity" in combining and parameterizing standard security practices that are widely used in the industry. What legal protection can be used by the company offering this product?

- To treat the secret combination and parameterization as trade secret.

Q12: What are the three requirements, in principle, that a patent application should satisfy in order to be approved by a Patent Office?

- The disclosed invention should be about a technical idea that 1) solves a problem, 2) is novel, or equivalently "not obvious to those skilled in art," and 3) can be implemented.

Q13: After uploading your presentation slides of your final project for CS396 on the course web page, you decide that the main technical idea in your project -- namely that in order to protect against SQL injections attacks, the reference monitor of a DBMS system should employ Honeywords for user authentications and MAC for access-control management -- can be the basis of very promising startup. Which existing legal protection(s) you can use to ensure that only you will financially benefit by commercializing this idea?

- No legal protection can be applied for your idea.

Q14: "A research paper is submitted to a top security conference for publication. The paper presents results on a new powerful theoretical attack against a wide range of location-based services. To demonstrate its efficacy and practicality, the authors report on a real-world and fully-developed version of the attack, orchestrated against the popular mobile application Waze, which provides users with real-time map routes and driving conditions. It is shown that, because Waze does not support any authenticated roadmap queries, it is possible to reroute users to fake (maliciously or randomly crafted) routes and notify them on fake (non-existing) road conditions. This actual attack was performed in a highly-controlled low-risk environment, in a rural area in upstate NY during the 48-hour span of a weekend, with a users body of only 100. Prior to the submission of the paper to the conference, the authors contacted Waze to inform them about the specific attack and the security issues their application has, and they are currently working with the Waze security personnel to add any necessary safeguards." As a member of the Program Committee of the conference, which factors should you primarily consider in making an accept/reject decision?

- Scientific merits and ethical considerations. Any type of research should constitute a scientifically solid contribution that is performed in an ethical manner, especially when it involves a real-world attack; here, independently of the merits of the results, the method used for demonstrating the attack is clearly unethical (and dangerous at least).

Q15: In one CS396 lab, you need to perform some web search in one of the provided computer desktops. When you start working on the computer, you realize that your classmate Alice from the previous lab session is still logged in her Gmail account, as the web browser opens at a tab where you can see her emails. What is the most ethical thing to do?

- You should immediately logout of her Gmail account reboot the machine to re-launch the Web browser application.

Q16: 

```
/* stack.c */
#include <stdlib.h>

int func(char *str) {
	char buffer[12];
	strcpy(buffer, str);
	return 1;
}
```

What describes the security of running the above program?

- The program allows for buffer overflows, which can be exploited, by a malicious attacker to compromise the host machine.

Q17: What is the main challenge of the attacker in a successful buffer-overflow attack?

- To overwrite the program counter with the address of the malicious code.

Q18: In a buffer-overflow attack, what is the most challenging phase for the attacker who has already identified that a target server runs software with a buffer-overflow vulnerability?

- To ensure that the injected malicious code will eventually run.

Q19: In a buffer-overflow attack, what is the most challenging phase for the attacker and why?

- To ensure that the injected malicious code will eventually run. Indeed, the attacker cannot know with certainty the absolute memory locations of the injected overflowed data; this is where the attacker needs lots of trial and error and "nopsled" techniques.

### Reference Material

Q1: Which of the following are true about public-key cryptography?

- Public-key cryptography significantly improves scalability with respect to the management of secret keys in a multi-user cryptographic system, by eliminating the need for securely distributing secret keys to other users under the weaker (and more realistic to achieve) assumption that public keys become publicly available in a secure way.
- Although significantly slower compared to symmetric-key encryption, in practice, public-key encryption can be efficiently used in what is referred to as hybrid encryption. In particular, a client application may securely establish a session key with a remote server by first generating a key for a cipher, then sending this key encrypted using RSA, under the server's public key, and having a subsequent transmissions encrypted fast via this cipher.

Q2: When you see a little lock icon in the top left corner of your web browser, after you have successfully submitted your password and logged in to the bank account, which of the following are true?

- A secure connection has been established: 
  - By running HTTPS over TLS, all transmissions sent and received during your login session cannot be read or maliciously altered.
- Mutual authentication has been achieved using passwords and digital certificates: 
  - The bank server has verified that you are the user you claim you are, and your browser has verified that the server is the machine serving your bank.

Q3: Which of the following constitute real-world applications of collision-resistant cryptographic hashing?

- Data deduplication
  - i.e., using the digests of uploaded files as unique identities to avoid storing the same files more than once.
- Blockchain technologies
  - i.e., using collision puzzles to achieve consensus over the immutable state of a set of posted transactions.

Q4: Which of the CIA security properties become relevant to the security of the Domain Name System (DNS)?

- All three: Confidentiality, Integrity, and Availability

Q5: Which of the following statements are true about the DNS security extension protocols?

- NSEC complements DNSSEC by authenticating also "negative" or "miss" answers to DNS queries, i.e., on domain names that do not exist in the system.
- Zone-enumeration attacks are possible in NSEC due to the type of proofs provided to users while querying non-existing domain names.
- NSEC5 removes any zone-enumerations vulnerabilities that exist in NSEC3, by applying, exactly as in NSEC3, collision-resistant cryptographic hashing, but now implemented via a hash function that is not publicly computable, yet it is publicly verifiable.
- DNSSEC prevents against IP spoofing by individually signing DNS entries, i.e., pairs of domain names and a IP address they resolve to.

Q6: Which of the following are true with respect to buffer overflow attacks?

- A challenge that the attacker needs to overcome is translating a meaningful malicious code, written in the programming language in which the target program is implemented, typically C/C++, into low-level ASSEMBLY code that is specific to the computer architecture where the target program runs. Even a few lines of malware require sophisticated programming skills to translate into ASSEMBLY code that can run successfully.
- The "nopsled" technique involves the use of many "no-operation" commands, carefully interleaved with a number of "relative jump" commands, so that a wider range of guessed values, injected as the return address of the function call in which the buffer overflow occurred, can lead to a successful execution of the injected malicious code.

Q7: Stevens has recently updated its user-authentication system by adopting the use of Honeywords and a remote, cloud-based, server as HoneyChecker. Which of the following are true regarding the security of the new user-authentication system?

- As long as an attacker does not succeed in compromising both the authentication server at Stevens and the HoneyChecker, the security of the new system is strictly better, because user impersonation due to stolen password files now can be, in principle, detected.
- To achieve stronger security and eliminate false compromise alerts, honeywords, i.e., the decoy passwords of each user, should be as close as possible to the user's real password subject to the restriction that they pairwise differ by at least 2-3 characters.

Q8: Which of the following are countermeasures for hardening password security?

- Hashing passwords iteratively many times.
- Maintaining fake passwords, a.k.a. Honeywords, in a two-server password authentication architecture.
- Hashing passwords with user-specific salts.

Q9: Which of the following intellectual properties provide legal protections for the expression of ideas or technical ideas?

- Copyright
- Patents

Q10: Which of the following are true, considering the differences between law and ethics with respect to our judgement in making security related decisions?

- Laws dictate avoiding certain behaviors in a well-documented manner, whereas ethics involve behaving based on unwritten principles.
- Courts decide on conflicting laws or clarify unclear laws, more or less consistently, whereas ethical issues must be identified, analyzed and prioritized by individuals, based on their moral principles, beliefs and qualities like integrity, kindness etc.

---

Drink water :)