# Security policy

This repository is the public time witness for VER (Verifiable Evidence Record) checkpoints. If you have found a way to make a non-conforming record verify, a conforming record fail, a producer report falsely, or a checkpoint be back-dated, we want to know before anyone else does.

**Reporting.** Email security@forenq.com. Include what you found, how to reproduce it, and what you think it could cause. Encrypted email is not required; if you prefer it, ask for our key.

**What we'll do.** Acknowledge within 48 hours. Investigate under the incident response procedure. Tell you what we found and when a fix will ship. Credit you by name in the release notes and the conformance suite's test that now covers it, unless you'd rather not be named.

**What's in scope.** The VER specification, the reference validator, the conformance suite, the sealer, the checkpoint and anchor mechanism, the key registry. Anything that touches what a stranger can verify offline.

**What we ask.** Give us a reasonable time to fix before publishing, thirty days for most things, longer if we tell you why. Don't access, alter, or exfiltrate any tenant's records while demonstrating a finding. Don't run tests against a production tenant's deployment; use the published test vectors.

**What we won't do.** We won't take legal action against research conducted in good faith under these terms. We won't ask you to sign anything to be credited.

---

Tsum Intelligence Pvt. Ltd., Kathmandu. This policy is the companion to the `security.txt` served at https://forenq.com/.well-known/security.txt.
