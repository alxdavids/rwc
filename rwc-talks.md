#RWC talks

## DAY 1

### Software engineering and OpenSSL -- Rich Salz

- OpenSSL pre-heartbleed
- The community was under-developed and under-funded (< $2000)
- Code-base was archaic and hard to understand/contribute to
- Releases and design procedures were not coherent
- Number of commits was low and essentially restricted to very small group of individuals
- Heartbleed lead to increase funding
- Afterwards community decided to meet and define coding standards
- Procedure for addressing failures was designed
- Emphasis placed on designing community
- Faced several severe CVEs since but have _almost_ always managed to address in appropriate manner

### Project Wycheproof -- Thai Duong

- Unit tests of crypto libraries 
- Unveiled critical bugs in some libraries
- Requests to help develop the testing suite for extra libraries e.g. Go.

### X.509 in Practice -- L Jean Camp

- Analysing the state of certificates after the heartbleed vulnerability
- 90% of certificates revoked only after 2 years
-- Probably down to expiration rather than action
- Some funny/worrying statistics
-- People changed certificates but used the same old keys
-- Numerous certificates were downgraded (e.g. SHA256 --> SHA-1, SHA-1 --> MD5)
-- MD5 was still being seen in 2014 despite popular belief
- Prediction
-- It will be years before SHA-1 is phased out
- Notable for Q&A session that lead to 

### Cryptanalysis of go-jose -- Quan Nguyen

- (simplified, can't really remember that well)
- Library for interacting with RFCs for JWK/JWT/JWS
- There was a problem with the signature for JWTs also signing the header field
-- This allowed redefining the header and payload fields along with the public JWK
- There was a problem with allowing multiple signing objects
-- One success appeared to suggest that verifying was successful even if some of the signatures failed

### NSEC5 -- Sharon Goldberg

- DNS servers return IP addresses for queried domain names
- Sometimes it is necessary for a DNS server to prove that it does not have a record for the given query
-- Malicious DNS servers may want to pretend that it doesn't have a record for a domain name
- Previous solutions require that the server presents a viable range showing that the domain does not exist
-- otherwise it would exist in that range
- These solutions can be used to enumerate all DNS records on that server though (even if hashing was used)
- NSEC5 is a new solution that provably avoids enumeration attacks
-- Also improves on previous NSEC3 solution by avoiding (what?)
- Requires online computation by DNS server so not as efficient as earlier solutions but provides trade-off

### Cryptographically securing NTP

- NTP is used by clients to synchronise clocks with a server
- Currently there is no cryptographic enforcement of integrity 
-- The clients just take what is given to them
-- Allows a malicious server to alter the client's clock
-- This can cause significant failures, especially in time-sensitive situations
- The work is called NTS and it competes with the Roughtime solution proposed by Adam Langley
- There was a part of the NTS design that effectively required anonymous authentication
- May be possible to incorporate the blind signature design proposed by Cloudflare for the internet challenge bypass tool

### Levchin Prize -- Winners: Joan Daemen, Signal creators (Moxie Marlinspike, Trevor Perrin)

- Joan Daemen is known as one of the creators of both Rijndael and Keccak (AES and SHA-3 standards).
- Moxie and Trevor are the key developers in the Signal messaging protocol that is used by over a billion people worldwide
- Moxie spoke about pioneering technology developers as the "agents of history", rather than being the creators
-- I agreed with this
-- Technology progresses regardless of the actors involved
-- Drew comparisons with the way that Soviet leaders acknowledged applause -- contrasting with the way that fascist figureheads accepted it

### Security assessment of White-box crypto -- Joppe Bos

- Showing the white-box crypto is hard to achieve
- for example, easy to distinguish implementations of DES/AES (does this fit into security requirement?)
- More notable for Q&A for the inquiry into moral implications of work

### NIST PQ challenge - Rene Peralta

- The NIST challenge has been officially announced

### CRYSTAL - Tancrede Lepoint

- Cryptographic suite for lattice-based constructions
- NIST PQ submission 
- Module lattices used for operations
- Comparison to NewHope, NTRUPrime, Frodo?

### Frodo - Valeria Nikolaenko

- Key Change based on LWE rather than RLWE (NewHope)
- Communication is increased since matrices are sent instead of cyclotomic ring elements
- Computation time also has slight increase in overhead
- Represents security trade-off
-- LWE security much better understood 

### Supersingular Isogeny DH - Michael Naehrig

- Don't understand elliptic curves or isogenies
- Communication much better than lattice-based proposals
- Computation times very high (almost impractical)

## DAY 2

### High-throughput, secure 3-party computation -- Yehuda Lindell

- Adapts secret-sharing based techniques for new 3-party computation protocol
- Semi-honest version allows for > 7 billion AND gates per second
- Malicious protocol > 1 billion AND gates
-- How many AES computations?
- By far the fastest 3PC implementation so far

### MPC at Google -- Ben Kreuter

- Google are interested in practical methods for exploring MPC
- Not so interested in general methods
- One important use case is private set intersection
- Uses AHE for performing PSI
-- This is not a new method, seems wrong to compare against garbled circuits etc
- Maybe there is something here for my own work

### E2E in Messenger -- Jon Millican

- Talk describing the design decisions behind the Messenger E2E 
- Went for one device per chat as with other protocols
- Interesting concept known as message franking
-- Provides stamp of authenticity of messages without reading content
- Criticisms of solution due to not providing E2E by default
- Also concerns over how metadata is handled

### Snapchat (Memories) -- Moti Yung

- Memories for your eyes only
-- Videos/pictures stored in the cloud 
-- Password protected, if password is lost then so are the memories
- Can't remember the protocol in particular

### DMCA -- Mich Stoltz

- Research that displays faults in encryption schemes can be declared unlawful under the DMCA
-- Can be interpreted as breaking into encryption and thus as illegal activity
- Case brought forward by Matthew Green and others to challenge interpretation of law
-- Inhibits the ability of groups to conduct thorough research into 
- The EFF are aiding the case and have been attempting to get the law changed for some time


### Proof of Signal protocol -- Luke Garratt

- No previous analysis
- Provable guarantees can help
- Theoretical analysis
- Proof is long but not necessarily complex (apparently)
- Analyse with respect to forward secrecy and post-compromise security
- Euro S&P

### 0-RTT Key Exchange with Full Forward Secrecy - Felix Gunther

- Don't have to wait for a round trip before data can be sent (client -> server?)
- Establishes the key in the first message (maybe it needs pre-existing key material?)
- Explicit goal in QUIC and TLS1.3
- Replay attacks of first message is partially unavoidable
- no forward secrecy (considered inherent)
-- this is shown to be false in this work (impossibility wasn't already proven?)