[**Current Version:** 4.0](README.md)

# Network Information

To learn about a network, an **HTTPS POST** request to `/protocols/network_information` is used.

Server must not expect any data to be in body for this request.

Example Response Client Must Expect:

```json
{
  "@context": "https://theprotocols.org/ns/4.0/Network.jsonld",
  "@id": "theprotocols://{network}/network/about",
  "@version": "4.0",
  "authorizationUrl": "", // Authorization URL
  "help": "", // Username of the account users must contact for help
  "os": { // Information about OS of the server of the network
    "arch": "", // Architecture of OS (look below)
    "family": "", // OS Family (all lowercase, no space)
    "name": "", // OS Name (possible shortest legal name for OS)
    "version": "" // OS Version
  },
  "rules": {
    "newAccountsAllowed": true // If network allows creating new accounts
  },
  "software": {
    "build": 1, // Build number of the server software
    "channel": "", // Release channel of the server software (look below)
    "name": "", // Name of the server software
    "version": "" // Version of the server software
  },
  "subscriptionPlans": [
    {
      "name": "", // Name for the free plan
      "storage": 0, // Storage limit for free plan users
    },
    {
      "name": "", // Name for cheapest plan
      "storage": 0, // Storage limit for free plan users
    },
    ...
    {
      "name": "", // Name for the most expensive plan
      "storage": 0, // Storage limit for free plan users
    }
  ]
}
```

> **Architecture of OS must be any of these:** i386, i486, i586, i686, amd64, arm, armhf, armel, arm64, riscv32, riscv64, ppc, ppc64, ppc64le, mips, mipsel, mips64, mips64el, sparc, sparc64, s390, s390x, loongarch64, alpha, hppa, m68k, sh4, ia64, nios2, arc, xtensa, microblaze

> **Software channel must be any of these:** development, alpha, beta, silver, gold.
