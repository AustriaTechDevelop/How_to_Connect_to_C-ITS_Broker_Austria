![alt text](https://github.com/AustriaTechDevelop/How_to_Connect/blob/main/img/Logo.png?raw=true)
## C-ITS Broker Austria - How to Connect

This document explains the technical details for external organisations connecting to the C-ITS Broker Austria.

---

### Broker Connection Details

| | |
|---|---|
| **URL** | `amqps://amqp.croads-broker.at:5671` |
| **Topics** | `croads`, `testing` |

---

## Client Certificate Request

Before connecting, you need a client certificate to authenticate your AMQP client. Request one by emailing **c-itsbrokerat@austriatech.at** with the following information:

---

### Required Information for Your Request

1. **PKCS#10 Certificate Signing Request**: see instructions below
2. **Client role**: see role descriptions below
3. **Contact person name** for the respective client
4. **Publisher ID**: obtainable via Austrian Standards *(publishing clients only)*
5. **Authorization confirmation**: a confirmation from the contracting party stating you are authorized to act on their behalf, along with their Publisher ID *(contractors only)*

---

### Roles

| Role | Description |
|---|---|
| **subscription-only** | Client can receive messages from the broker. Any message sent to the broker by the client for publishing will be rejected. |
| **pub-sub** | Client can receive and publish messages on the C-ITS Broker Austria. Any messages sent to the broker by the client for publishing will be published if a validation of the ITS message’s secured GeoNetworking header returns successfully *(Guest role)*. |
| **trusted-pub-sub** | client can receive and publish messages on the C-ITS Broker Austria. Messages sent to the broker by the client will be published immediately without any validation of the message body *(This client request is for a city or a regional C-ITS actor with active C-ITS stations generating regular messages)* |

---

### Generating a Certificate Signing Request (CSR) with OpenSSL

**Step 1 - Generate a new key pair:**
```bash
openssl ecparam -out c-roads-client.key -name prime256v1 -genkey
```

**Step 2 - Generate the CSR:**
```bash
openssl req -new -key c-roads-client.key -out c-roads-client.csr
```
> [!IMPORTANT]
> Do not set a ```challengePassword``` when generating the CSR

Attach the resulting `c-roads-client.csr` file to your certificate request email.

### Subscription Client
For subscribing to the C-ITS Broker Austria, AustriaTech provides a client using Apache Qpid Proton, available on GitHub:
`https://github.com/AustriaTechDevelop/C-ITS-Broker-Austria-Subscription-Client`


