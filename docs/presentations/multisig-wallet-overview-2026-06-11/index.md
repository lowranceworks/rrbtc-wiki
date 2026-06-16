## Introduction

**Not your keys, not your coins.**

**Not your keys, not your coins.**

**Not your keys, not your coins.**

You've heard this enough times.

You've bought the cold storage hardware wallet.

You've generated a seed and stamped it into steel.

You've moved your Bitcoin off the custodian wallets hosted on Coinbase, Fidelity, RobinHood, etc..

Your Bitcoin is now safely stored away on your new cold storage wallet.

A device that has never connected to the internet.

A device that doesn't use the bluetooth or NFC protocols.

You're signing Bitcoin transactions in [air-gapped]() fashion.

There's just one problem, you now have a single point of failure.

```
    ┌─────────────────────────────────┐
    │         SINGLE POINT            │
    │         OF FAILURE              │
    │                                 │
    │   ┌───────────┐                 │
    │   │           │    Lost?        │
    │   │  1 Key    │──► Stolen?      │
    │   │           │    Damaged?     │
    │   │           │    Forgotten?   │
    │   └───────────┘                 │
    │         │                       │
    │         ▼                       │
    │   ╔═══════════╗                 │
    │   ║  ALL BTC  ║                 │
    │   ║   GONE    ║                 │
    │   ╚═══════════╝                 │
    └─────────────────────────────────┘
```

Enter MultiSig.

---

## What is MultiSig?

A Bitcoin wallet configuration that requires multiple private keys to authorize a transaction.

```
  SingleSig                          MultiSig (2-of-3)
  ─────────                          ─────────────────

  ┌─────┐                        ┌─────┐ ┌─────┐ ┌─────┐
  │Key 1│                        │Key 1│ │Key 2│ │Key 3│
  └──┬──┘                        └──┬──┘ └──┬──┘ └──┬──┘
     │                              │       │       │
     │                              └───┬───┘       │
     │                                  │   ┌───────┘
     ▼                                  ▼   ▼
  ╔══════╗                        ╔══════════════╗
  ║ SIGN ║                        ║ 2 of 3 SIGN  ║
  ╚══╤═══╝                        ╚══════╤═══════╝
     │                                   │
     ▼                                   ▼
  ┌──────────┐                    ┌──────────┐
  │    TX    │                    │    TX    │
  │ APPROVED │                    │ APPROVED │
  └──────────┘                    └──────────┘
```

Defined in [BIP-11 (2011)](https://github.com/bitcoin/bips/blob/master/bip-0011.mediawiki) and later improved with P2SH in [BIP-16](https://github.com/bitcoin/bips/blob/master/bip-0016.mediawiki).

---

## What does it look like?

| Config     | Who Uses It                            | Notes                                                       |
| ---------- | -------------------------------------- | ----------------------------------------------------------- |
| **2-of-2** | Partners, parent/child                 | Both keys required -- no redundancy                         |
| **2-of-3** | Individuals                            | By far the most popular; gold standard for personal custody |
| **3-of-5** | Businesses, high-net-worth individuals | Casa Premium, Unchained                                     |
| **4-of-7** | Corporate treasuries, institutions     | Less common but used                                        |
| **5-of-9** | Large institutions                     | Rare, high-security environments                            |

**The more signatures required, the more security you have -- but also more coordination overhead.**



---

## What's wrong with SingleSig?

Single point of failure.

One compromised seed phrase? Game over.

One key. One threat. Game over.

---

## Why would I want MultiSig?

Security is the obvious answer, but it's not the only one.

### Security

This reason alone is enough.

#### $5 Wrench Attack

A familiar concept in the Bitcoin community.

[A 12" Crescent wrench is now $25.](https://www.homedepot.com/p/Crescent-12-in-Chrome-Adjustable-Wrench-AC212VS/203161636) Even violence has inflated.

A thief invests $25 into a wrench, breaks into your home, threatens you, you hand over your Bitcoin.

Return on investment: considerable.

With SingleSig, that's the end of the story.

```
  $5 Wrench Attack vs. SingleSig
  ═══════════════════════════════

  Attacker                    You
  ┌──────┐    ┌────────┐    ┌──────┐
  │      │    │        │    │      │
  │  $$  │───►│ WRENCH │───►│  !!  │
  │      │    │        │    │      │
  └──────┘    └────────┘    └──┬───┘
                               │
                          "Here's my
                           seed phrase"
                               │
                               ▼
                         ╔═══════════╗
                         ║  ALL BTC  ║
                         ║   GONE    ║
                         ╚═══════════╝
```

### Game Theory (MultiSig Edition)

With a 3-of-5 MultiSig, the attacker's evening gets complicated:

1. Attacker gets your device. That's 1 of 5. They need 3.
2. Attacker has to call a friend. Friend has to break into another location.
3. That might trigger a security alarm. They might get shot trying.
4. Let's say they're successful. They now have 2 of 5. Still need 3.
5. Attacker calls another friend. Same scenario plays out.

More keys, more locations, more points of failure *for the attacker*.

```
  $5 Wrench Attack vs. 3-of-5 MultiSig
  ══════════════════════════════════════

  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐
  │ Key 1   │  │ Key 2   │  │ Key 3   │  │ Key 4   │  │ Key 5   │
  │ Your    │  │ Safety  │  │ Friend  │  │ Bank    │  │ Lawyer  │
  │ House   │  │ Deposit │  │ House   │  │ Vault   │  │ Office  │
  └────┬────┘  └────┬────┘  └────┬────┘  └────┬────┘  └────┬────┘
       │            │            │            │            │
       ▼            ▼            ▼            ▼            ▼
     GOT IT      NEED IT      NEED IT      NEED IT      NEED IT
       │            │            │            │            │
       │    ┌───────┘            │            │            │
       │    │  Break in #2       │            │            │
       │    │  at 2 AM?          │            │            │
       │    │  Alarm? Dog?       │            │            │
       │    │  Shotgun?          │            │            │
       │    ▼                    │            │            │
       │  MAYBE?                 │            │            │
       │    │    ┌───────────────┘            │            │
       │    │    │                            │            │
       ▼    ▼    ▼                            │            │
     ╔════════════════╗                       │            │
     ║  Attacker now  ║                       │            │
     ║  questioning   ║◄──────────────────────┘            │
     ║  life choices  ║◄───────────────────────────────────┘
     ╚════════════════╝
```

### Inheritance Planning

Your life savings should not have a single point of failure.

Consider mortality. Life isn't guaranteed tomorrow.

### Authorize Transactions with a Group

A great option for:

- Institutions
- Nonprofit Organizations
- LLCs
- DAOs and community treasuries

### Wealth Building Accountability

You generate 3 seeds across 3 devices.

You hold one device & seed.

A friend holds another device & seed.

Your brother holds the third device & seed.

If you want to spend your Bitcoin, you need at least one of them to co-sign. Built-in impulse control. Better than willpower.

```
  Accountability MultiSig (2-of-3)
  ═════════════════════════════════

  You: "I want to buy a boat"
       │
       ▼
  ┌──────────┐   "Are you sure?"   ┌──────────┐
  │   YOU    │───────────────────► │  FRIEND  │
  │  Key 1   │◄────────────────────│  Key 2   │
  └──────────┘   "...no"           └──────────┘
                                   ┌──────────┐
                                   │ BROTHER  │
                                   │  Key 3   │
                                   └──────────┘
                                   (not needed)

       ╔═══════════════════════════╗
       ║  Bitcoin: still stacking  ║
       ║  Boat: not purchased      ║
       ╚═══════════════════════════╝
```

---

## How do I get started?

### Bitkey

A product created by [Block, Inc.](https://block.xyz/) (Jack Dorsey's company, formerly Square).

2-of-3 MultiSig natively built-in out of the box. Phone + hardware device + Block's server.

```
  Bitkey 2-of-3 Setup
  ════════════════════

  ┌───────────┐   ┌───────────┐   ┌───────────┐
  │ ┌───────┐ │   │  ┌─────┐  │   │  ┌─────┐  │
  │ │       │ │   │  │     │  │   │  │     │  │
  │ │ Phone │ │   │  │ HW  │  │   │  │Block│  │
  │ │  App  │ │   │  │ Dev │  │   │  │ Svr │  │
  │ │       │ │   │  │     │  │   │  │     │  │
  │ └───────┘ │   │  └─────┘  │   │  └─────┘  │
  │  Key 1    │   │  Key 2    │   │  Key 3    │
  └─────┬─────┘   └─────┬─────┘   └───────────┘
        │               │
        └───────────┬───┘
             2 of 3 │
                    ▼
              ╔══════════╗
              ║ TX SENT  ║
              ╚══════════╝
```

[bitkey.world](https://bitkey.world/)

I can't personally recommend this wallet -- I've never used one. But they do offer MultiSig out of the box.

One "device" is software on your phone. One signer is your thumbprint. One key lives on Block's server.

Is this true MultiSig? It doesn't pass the $5 wrench attack.

### Build your own custom MultiSig Config

#### Create a custom MultiSig with collaborative custody

Costs money, typically a recurring annual subscription.

Solid options:

- [Unchained](https://www.unchained.com/vaults) (based in Austin, TX)
- [Nunchuk - Honey Badger wallet](https://nunchuk.io/blog/introducing-the-honey-badger-wallet) (based in Canada)

Recommended if you don't want to burden your family with technical hurdles. The custodian holds one key and provides recovery assistance.

The tradeoff is privacy and cost for convenience.

```
  Collaborative Custody (2-of-3)
  ══════════════════════════════

  ┌───────────────┐  ┌───────────────┐  ┌───────────────┐
  │     YOU       │  │     YOU       │  │   CUSTODIAN   │
  │   Device 1    │  │   Device 2    │  │  (Unchained/  │
  │   + Seed 1    │  │   + Seed 2    │  │   Nunchuk)    │
  │               │  │               │  │   + Seed 3    │
  │   [at home]   │  │  [off-site]   │  │   [their HQ]  │
  └───────┬───────┘  └───────┬───────┘  └───────┬───────┘
          │                  │                  │
          │    You sign      │                  │
          │◄─────────────────┤                  │
          │                  │                  │
          └────────┬─────────┘                  │
              2 of 3                            │
                   ▼                (only used  │
             ╔══════════╗          for recovery)│
             ║ TX SENT  ║◄─────── ─ ─ ─ ─ ─ ─ ─┘
             ╚══════════╝
```

Nunchuk does offer a non-KYC option.

#### Create a custom MultiSig without collaborative custody

The most self-sovereign option, but also the one most likely to get you locked out of your own Bitcoin.

Proceed with caution. Don't go beyond your technical knowledge. Practice on the Bitcoin Test network or small sums of sats.

Requires planning, documentation, and people you trust.

```
  DIY MultiSig (2-of-3) -- No Custodian
  ══════════════════════════════════════

  ┌───────────────┐  ┌───────────────┐  ┌───────────────┐
  │     YOU       │  │   TRUSTED     │  │   TRUSTED     │
  │   Device 1    │  │   PERSON A    │  │   PERSON B    │
  │   + Seed 1    │  │   Device 2    │  │   Device 3    │
  │               │  │   + Seed 2    │  │   + Seed 3    │
  │   [home]      │  │   [loc. 2]    │  │   [loc. 3]    │
  └───────────────┘  └───────────────┘  └───────────────┘

       ⚠ YOU are responsible for EVERYTHING ⚠

       • BSMS backup      • Seed backups
       • XPUB backups     • Recovery testing
       • Derivation paths • Key holder check-ins
```

---

## Technical Considerations with Managing a Custom MultiSig

```
  What You MUST Back Up
  ═════════════════════

  ┌─────────────────────────────────────────────┐
  │              BSMS FILE                      │
  │  ┌─────────────────────────────────────┐    │
  │  │  • XPUBs (all cosigner public keys) │    │
  │  │  • Derivation paths                 │    │
  │  │  • Quorum config (m-of-n)           │    │
  │  │  • Script type                      │    │
  │  └─────────────────────────────────────┘    │
  └──────────────────┬──────────────────────────┘
                     │
        ┌────────────┼────────────┐
        ▼            ▼            ▼
  ┌──────────┐ ┌──────────┐ ┌──────────┐
  │ Copy 1   │ │ Copy 2   │ │ Copy 3   │
  │ Home     │ │ Off-site │ │ Trusted  │
  │ Safe     │ │ Location │ │ Person   │
  └──────────┘ └──────────┘ └──────────┘

  ALSO save separately (redundancy is the point):
  ┌──────────┐ ┌──────────────────┐
  │  XPUBs   │ │ Derivation Paths │
  └──────────┘ └──────────────────┘
```

**Save multiple copies of your BSMS file.**

The [Bitcoin Secure Multisig Setup (BSMS)]() file contains everything needed to reconstruct your wallet: XPUBs, derivation paths, and the quorum configuration.

**Save your XPUBs.**

Yes, they're in the BSMS file. Save them separately anyway. Redundancy is the point.

**Save your derivation paths.**

Also in the BSMS file. Save them separately anyway.

**Practice restoring the wallet from the BSMS file.**

Before you need to.

**Practice signing a transaction with multiple devices.**

Before you need to.

**Routine checkups on people who hold your keys.**

"Hey, do you still have that manila envelope?"

"Where is it?"

- Biannual or annual checkups at minimum
- Verify physical possession, not just a "yeah I think so"

---

## Recommended Cold Storage Wallets for MultiSig

| Wallet | Manufacturer | Link |
|--------|-------------|------|
| SeedSigner | Open Source / DIY | [seedsigner.com](https://seedsigner.com/) |
| SeedSigner Plus | Open Source / DIY | [seedsigner.com](https://seedsigner.com/) |
| Jade | Blockstream | [blockstream.com/jade](https://blockstream.com/jade/) |
| Jade Plus | Blockstream | [blockstream.com/jade](https://blockstream.com/jade/) |
| COLDCARD Mk4 | Coinkite | [coldcard.com](https://coldcard.com/) |
| COLDCARD Mk5 | Coinkite | [coldcard.com](https://coldcard.com/) |
| COLDCARD Q | Coinkite | [coldcard.com/q](https://coldcard.com/q) |

---

## Risks with MultiSig

A common way people lose their Bitcoin is by doing something they don't understand. MultiSig adds complexity. Complexity is the enemy of execution.

```
  The MultiSig Tradeoff
  ═════════════════════

  Security ◄──────────────────────────► Complexity
  ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓░░░░░░░░░░░░░░░░░░░░░░░░░░

  SingleSig    2-of-3    3-of-5    5-of-9
  ┌──────┐   ┌──────┐   ┌──────┐   ┌──────┐
  │ Easy │   │ Good │   │ Hard │   │ Big  │
  │Risky │   │Sweet │   │ More │   │ BTC  │
  │      │   │ Spot │   │ Safe │   │      │
  └──────┘   └──────┘   └──────┘   └──────┘
     ▲            ▲
     │            │
  Most         Most people
  people       should be
  are here     here
```

What good is the scarcest money in the world if your heirs can't spend it?

Requires clear instructions, planning, technical confidence, or a trusted friend who actually knows what they're doing.

---

## Not ready for MultiSig?

Consider the top-of-the-line cold storage wallet: [ColdCard Q](https://coldcard.com/q).

Generate a seed and create a BIP-39 Passphrase.

Create "trick PINs" for duress scenarios:
- Direct the attacker to a "honeypot" wallet with a small balance
- Steers them away from your real stash

```
  ColdCard Q -- Trick PIN Strategy
  ═════════════════════════════════

  Attacker: "Give me your PIN"
                │
                ▼
  ┌──────────────────────────────┐
  │  You enter TRICK PIN: 1234   │
  └──────────────┬───────────────┘
                 │
                 ▼
  ┌──────────────────────────────┐
  │   HONEYPOT WALLET OPENS      │
  │                              │
  │   Balance: 0.005 BTC         │
  │                              │
  │   Attacker: "That's it?"     │
  │   You:     "Times are tough" │
  │   ¯\_(ツ)_/¯                 │
  └──────────────────────────────┘

  Meanwhile...
  ┌──────────────────────────────┐
  │   REAL WALLET (real PIN)     │
  │                              │
  │   Balance: XXXXXX BTC        │
  │                              │
  │   Status: SAFE               │
  └──────────────────────────────┘
```

---

## References

- [BTC Sessions - Simple BITCOIN INHERITANCE Planning with NUNCHUK Wallet](https://www.youtube.com/watch?v=kizqvBY4zPE&list=PLxdf8G0kzsUUqr4oVXRHL1L-iK1q9hCfq)

- [Unchained - MultiSig Documentation](https://unchained.com/features/vaults)

- [Nunchuk - Honey Badger Wallet](https://nunchuk.io/blog/introducing-the-honey-badger-wallet)
