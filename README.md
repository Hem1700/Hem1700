# Hem Parekh

**Security engineer focused on memory-safety and vulnerability research in large open-source codebases.**

I audit production C/C++ and systems code for memory-safety bugs — out-of-bounds reads, missing bounds checks, unchecked attacker-controlled indices — and report them through proper disclosure channels. My approach is methodical source auditing, sibling-pattern mining (finding where a guard exists in one function but is missing in its siblings), and ASan-backed proof-of-concepts.

🔗 Portfolio & writeups: **[hem1700.github.io](https://hem1700.github.io)**

## Security Research / Notable Findings

- **Linux kernel (ksmbd) — out-of-bounds read fix, applied.** Found and fixed an OOB read in `smb_check_perm_dacl()` (`fs/smb/server/smbacl.c`) in the in-kernel SMB server, reachable over the network by an unprivileged client. Root cause was a missing `num_subauth`/`ace_size` bounds check that the function's two siblings already had. Reproduced under AddressSanitizer; patch carries `Fixes:` and `Cc: stable@vger.kernel.org`, and the maintainer applied it to `ksmbd-for-next-next`. CVE candidate pending mainline/stable. — [patch on linux-cifs](https://lore.kernel.org/linux-cifs/20260602235646.23581-1-hemparekh1596@gmail.com/T/#u)

- **PyTorch — flatbuffer loader bounds check (open PR).** Identified an unchecked attacker-controlled index (`class_type`) used in `all_types_[class_index]` in the mobile flatbuffer loader, leading to an OOB read / SIGSEGV when loading a malformed model. Fix routes the lookup through the bounds-checked `getType()` + `TORCH_CHECK`. — [pytorch/pytorch#186672](https://github.com/pytorch/pytorch/pull/186672)

- **curl — URL-parser SSRF-filter bypass (responsibly disclosed, under review).** Reported a logic bug in `parse_authority()` where IPv4 normalization runs before host percent-decoding, so a single `%2e` in the host escapes IPv4 canonicalization while the resolver still connects to the intended address — making curl disagree with its own `no_proxy` matcher. Currently under review; no CVE claimed.

## Focus & tools

Memory-safety auditing · vulnerability research · responsible disclosure · C/C++ · Python · AddressSanitizer · Linux kernel internals · fuzzing

## Connect

[![LinkedIn](https://img.shields.io/badge/LinkedIn-%230077B5.svg?logo=linkedin&logoColor=white)](https://linkedin.com/in/hem-parekh-bb356b175)
