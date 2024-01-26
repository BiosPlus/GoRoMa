---
layout: default
title: Secure Device Erasure
parent: macOS
---

# Secure Device Erasure
{: .no_toc }

Some words on secure device erasure. (A bit of an opinion piece)
{: .fs-6 .fw-300 }

---

## Understanding the T2 Chip in Mac Devices

Modern Mac devices, predominantly those released from 2018 onwards, incorporate a significant security feature: the T2 chip. This chip plays a role in data encryption and device security. Mainly:

- **Chip and Storage Pairing:** The T2 chip automatically encrypts files on the fly. This encryption is independent of whether FileVault2 is activated. The critical aspect of this setup is the unique pairing between the T2 chip and the device's storage unit, whether it's an M2 SSD or HDD. 
    - **Pairing Implication:** Due to this unique pairing, transferring a storage unit from one Mac to another is generally not feasible. Each T2 chip is unique, and a disk can only be decrypted by the T2 chip it was originally paired with. However, once a drive is wiped, it can be paired with a new T2 chip.

- **FileVault2 Encryption:** FileVault2 provides further encryption when activated. It relies on user-known passwords or smart cards for decryption during the boot process.

## The Appropriate Erasure Standard for Mac Devices

Given the encryption provided by the T2 chip and the supplemental second-pass encryption via FileVault2, the method of erasing data from Mac devices warrants reconsideration. Traditional approaches, such as the Department of Defense (DoD) standard involving three seperate passes of random data overwriting, is (in my opinion) unnecessary or even effective in this context. Instead, the NIST 800-88 approach of a single pass wipe is more than sufficient.

Conveniently, the built-in Disk Utility tool within macOS aligns with the NIST 800-88 standard. It performs a single pass wipe.

Don't bother wasting money on expensive software where the encryption standard established with the T2 and filevault does more than enough to scramble data in the first place.