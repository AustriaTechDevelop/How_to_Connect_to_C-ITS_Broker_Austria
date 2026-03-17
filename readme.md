## C-ITS Broker Austria — How to Connect

This document explains the technical details for external organisations connecting to the C-ITS Broker Austria.

---

### Broker Connection Details

| | |
|---|---|
| **Endpoint** | `amqps://amqp.croads-broker.at:5671` |
| **Target address** (C-Roads messages) | `croads`, `testing` |

---

## Client Certificate Request

Before connecting, you need a client certificate to authenticate your AMQP client. Request one by emailing **c-itsbrokerat@austriatech.at** with the following information:

---

### Required Information in Your Request

1. **PKCS#10 Certificate Signing Request** — see instructions below
3. **Contact person name** for the respective client(s)
4. **Client role** — see role descriptions below
5. **Publisher ID** *(publishing clients only)* — obtainable via Austrian Standards
6. **Authorization confirmation** *(contractors only)* — a confirmation from the contracting party stating you are authorized to act on their behalf, along with their Publisher ID

---

### Roles

| Role | Description |
|---|---|
| **subscription-only** | Can receive messages from the broker. Any messages sent for publishing will be rejected. |
| **pub-sub** | Can receive and publish messages. Published messages must pass validation of the ITS message's secured GeoNetworking header. *(Guest role)* |
| **trusted-pub-sub** | Can receive and publish messages. Messages are published immediately without validation. *(For cities or regional C-ITS actors with active C-ITS stations generating regular messages)* |

---

### Generating a Certificate Signing Request (CSR) with OpenSSL

**Step 1 — Generate a new key pair:**
```bash
openssl ecparam -out c-roads-client.key -name prime256v1 -genkey
```

**Step 2 — Generate the CSR:**
```bash
openssl req -new -key c-roads-client.key -out c-roads-client.csr
```

Attach the resulting `c-roads-client.csr` file to your certificate request email.

### Subscription Client
For subscribing to the C-ITS Broker Austria, AustriaTech provides a public client. It enables subscription using Apache Qpid Proton and is available on GitHub:

`https://github.com/AustriaTechDevelop/C-ITS-Broker-Austria-Subscription-Client`


