# Hem Parekh

```text
$ whoami
hem parekh — security engineer · memory-safety & vulnerability research

$ cat ~/.signature
"The bug is rarely that nobody wrote the check.
 It's that someone wrote it everywhere except here."
```

I read production C/C++ and systems code looking for the one path that drifted from its safe siblings — missing bounds checks, unchecked attacker-controlled indices, out-of-bounds reads — then prove it with a sanitizer and ship the fix upstream.

## Findings ledger

| Target | Bug class | Where | Status |
| --- | --- | --- | --- |
| **Linux kernel** · ksmbd | OOB read | `smb_check_perm_dacl()` — `fs/smb/server/smbacl.c` | **Applied** to `ksmbd-for-next-next`, `Cc: stable` · [patch](https://lore.kernel.org/linux-cifs/20260602235646.23581-1-hemparekh1596@gmail.com/T/#u) |
| **PyTorch** | OOB read → SIGSEGV | unchecked `class_type` index, mobile flatbuffer loader | Open PR · [#186672](https://github.com/pytorch/pytorch/pull/186672) |
| **curl** | SSRF-filter bypass | `parse_authority()` — normalize-before-decode (`%2e`) | Responsibly disclosed, under review |

## How I work

```text
read the code  →  diff a function against its siblings & git history
              →  hypothesize the missing invariant
              →  confirm with ASan / KASAN
              →  upstream patch + responsible disclosure
```

No exotic tooling — careful reading, sibling-pattern mining, and a sanitizer that turns a hunch into a named, reproducible bug.

## Stack

`C` · `C++` · `Python` · AddressSanitizer / KASAN · Linux kernel internals · fuzzing · responsible disclosure

## Elsewhere

**Portfolio & writeups →** [hem1700.github.io](https://hem1700.github.io)  ·  [LinkedIn](https://linkedin.com/in/hem-parekh-bb356b175)
