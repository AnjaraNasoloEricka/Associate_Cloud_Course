# Security 

## Google Infrastructure Security 
Progressive Layers : 
1. **Hardware Infrastructure Layer** : comprises 3 key security features
    1. **Hardware design and provenance :** Both the server boards and the networking equipment in Google data centers are custom-designed by Google. Google also designs custom chips, including a hardware security chip that's currently being deployed on both servers and peripherals.
    2. **Secure Boot Stack :**
        - **Goal :** ensure that they are booting the correct software stack
        - **Examples :** cryptographic signatures over the BIOS, bootloader, kernel, and base operating system image.
    3. **Premises security :** : Access to these data centers is limited to only a very small number of Google employees.

2. **Service deployment layer** : 
    - **Key** : Encryption of inter-service communication
    - *Google’s services communicate with each other using RPC calls* (provides cryptographic privacy and integrity for remote procedure call (“RPC”) data on the network)

3. **User identity layer** : 
    - Users can also employ secondary factors when signing in, including devices based on the Universal 2nd Factor (U2F) open standard

4. **Storage services layer** : 
    - **Key** : encryption at rest security feature.

5. **Internet communication layer** : comprises 2 key security features
    - **Google Front End (GFE)** : 
        - ensures that  all TLS connections are ended using a public-private key pair and an X.509 certificate from a Certified Authority (CA), as well as following best practices such as supporting perfect forward secrecy.
        - applies protections against Denial of Service attacks.
    - **Denial of Service (DoS) protection** :
        - *Goal* : The sheer scale of its infrastructure enables Google to simply absorb many DoS attacks.
        - Google also has multi-tier, multi-layer DoS protections that further reduce the risk of any DoS impact on a service running behind a GFE.

6. **Google's Operational security layer** : comprises 4 key security features
    1. **Intrusion detection** : Rules and machine intelligence give Google’s operational security teams warnings of possible incidents.
    2. **Reducing insider risk** :
        - Google aggressively limits and actively monitors the activities of employees who have been granted administrative access to the infrastructure.
    3. **Employee U2F use** : To guard against phishing attacks against Google employees, employee accounts
    4. **Stringent software development practices** :
        - Google employs central source control and requires two-party review of new code.

> Link to learn more about Google’s technical-infrastructure security at : cloud.google.com/security/security-design.
