# ver-anchors

**Public time witness for VER (Verifiable Evidence Record) checkpoints.**

This repository exists for one reason: so that anyone, at any time, can prove that a VER record existed no later than a given date — without trusting the institution that sealed it, and without trusting Tsum Intelligence.

## What is here

Once per UTC day, each institution running a VER sealer builds a Merkle tree over every record it sealed that day, signs the root, and commits the result here:

```
checkpoints/{tenant_key_id}/{YYYY-MM-DD}.json
```

Each file contains the canonical checkpoint object and its Ed25519 signature, exactly as defined in **VER Technical Specification v0.1, Section 10**:

```json
{
  "checkpoint": {
    "date": "2026-09-03",
    "leaf_count": 2,
    "leaf_hash_algorithm": "SHA-256",
    "root": "7573c9943750b7c8a9e7ffe9960f13aa349c5b7cc7ce02e81c11f47571935d21",
    "tenant_key_id": "21fe31dfa154a261626bf854046fd227",
    "ver_version": "0.1"
  },
  "checkpoint_signature": "1zT6fLq9T5toPqA5UfRgTE/R7OYpCOHMn/5+sPEW900Ze3CJX7H0BdAK+jH2pc71l6q7D80BgmYxRgoI/yoDBg=="
}
```

## Why a git repository

A commit has an authorship timestamp, a parent, and a hash. Rewriting history changes every subsequent commit hash, and this repository is public — anyone may clone it, and clones are independent witnesses. That makes the commit history a time anchor: a checkpoint committed on a given date cannot later be back-dated without the rewrite being visible to everyone who holds a clone.

This is anchor medium `git-public` in the specification. A second, independent medium (RFC 3161 timestamp authority) is recommended for records that will be produced in court, and required for `admissibility` and `neutral-adversarial` scrutiny regimes.

## What this repository does not contain

No records. No artifacts. No personal data. Only Merkle roots — 64-character hashes — and signatures over them. A root reveals nothing about the records beneath it except how many there were.

## How to verify a record against this repository

1. Obtain the VER export package (record + seal + checkpoint + inclusion proof).
2. Find `checkpoints/{tenant_key_id}/{date}.json` here, where `tenant_key_id` and `date` come from the package's checkpoint.
3. Confirm the checkpoint in the package matches the one committed here, byte for byte.
4. Note the commit's date. The record existed no later than that.
5. Run the open validator on the package. Step 23 verifies the checkpoint signature and walks the inclusion proof to the root.

The validator and specification are being prepared for publication under https://github.com/tsum-intelligence. This line will carry the link when they are public.

## Rules

- Files are added, never modified or deleted. If a checkpoint is wrong, a correction is a new file with a note, not an edit.
- One file per tenant per day. A day with zero records has no file.
- Commits are made by the sealer, not by hand.
- Nothing else goes in this repository, apart from this README and `SECURITY.md` (how to report a problem with the checkpoint or anchor mechanism). Neither is evidence; the `checkpoints/` tree is.

## Who operates this

Tsum Intelligence Pvt. Ltd., Kathmandu, as editor of the VER specification. The repository is held by the company's GitHub organisation, `tsum-intelligence`, not by any individual's account. The specification is published under CC BY 4.0; the reference validator under Apache 2.0. Tsum does not hold any tenant's signing key and cannot produce a checkpoint on a tenant's behalf.

---

*First commit: 8 September 2026. Transferred from a personal account to the `tsum-intelligence` organisation on 7 October 2026; the history is unchanged and the old address redirects. The repository is the evidence.*
