# 01 -- The Data Fragmentation Problem

---

## The Analogy

Imagine you have a filing cabinet at work, a shoebox of receipts at home, medical records at your doctor's office, a photo album on your phone, and a portfolio on a freelance platform. Each container uses its own filing system. None of them talk to each other. If you need to prove your identity to a new service, you start from scratch -- re-entering your name, re-uploading your photo, re-verifying your credentials.

Now imagine you want to move between virtual worlds. Your avatar, your preferences, your verified age, your purchased items -- none of it travels with you. You start over in every world.

This is the state of digital identity and portable state today.

---

## The Problem

Every pair of systems that needs to exchange user state builds a custom integration. Social profiles sit in one format. Device registrations sit in another. Privacy preferences are stored differently on every platform. Verified credentials use different schemas depending on who issued them.

Point-to-point integrations create a fragile web. Adding one new system means building N new integrations with every existing system. This approach does not scale.

Three things are missing:

1. **A shared document format.** There is no standard way to represent identity, consent, and credentials in a single portable document.

2. **Consent that travels.** When your data moves from Platform A to Platform B, your privacy preferences do not follow. Platform B has to guess -- or ignore -- what you allowed on Platform A.

3. **A lookup mechanism.** Even if a portable document existed, there is no standard way for a receiving system to find and retrieve it.

The result: engineering effort is duplicated across every integration, privacy is inconsistent across platforms, and true interoperability between systems remains out of reach.

---

*Next: [02 -- The Envelope](02-the-envelope.md) introduces the solution.*
