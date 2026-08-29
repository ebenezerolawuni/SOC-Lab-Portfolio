# Registry Integrity Investigation — Rule 750

## Overview

This investigation analysed a Windows registry modification detected by Wazuh Syscheck.

The objective was to determine what registry value had changed, identify the program associated with the value, and assess whether the modification represented malicious persistence or legitimate software activity.

---

## Detection

**Rule ID:** 750

**Description:** Registry Value Integrity Checksum Changed

**Severity:** Level 5

**Timestamp:** August 29, 2026 — 11:53:59

---

## Initial Evidence

```text
Registry Path:
HKEY_LOCAL_MACHINE\Software\Microsoft\Active Setup\Installed Components\{9459C573-B17A-45AE-9F64-1857B5D58CEE}

Value Name:
StubPath

Value Type:
REG_SZ

Event:
modified
```

The integrity information showed that the registry value had changed:

```text
Size:
172 bytes → 171 bytes

MD5:
67054272a426952990f4166f1edb9267
→
e9c4334fd08ae99786b7f81698d68615

SHA256:
c031d61a5033834e7117c16599e1f996b30ae1ac9fae1d46dd5a6a28567b0862
→
36d4ef588c401516aad771d76548128f15a3dc32faafbdfd525bf33d16d56066
```

The change in multiple integrity hashes confirmed that the registry value's contents had changed.

---

## Investigation

Because the affected value was `StubPath`, further investigation was required to determine exactly what command was configured.

The registry value was retrieved from the Windows endpoint using PowerShell.

The resulting value was:

```text
"C:\Program Files (x86)\Microsoft\Edge\Application\152.0.4191.53\Installer\setup.exe"
--configure-user-settings
--verbose-logging
--system-level
--msedge
--channel=stable
```

---

## Analysis

The registry entry pointed to:

```text
C:\Program Files (x86)\Microsoft\Edge\
```

The executable was:

`setup.exe`

The command-line parameters were associated with Microsoft Edge configuration:

* `--configure-user-settings`
* `--verbose-logging`
* `--system-level`
* `--msedge`
* `--channel=stable`

The executable was located within the expected Microsoft Edge installation directory under `Program Files (x86)`.

The evidence therefore indicated legitimate Microsoft Edge installation or configuration activity rather than an unknown executable or suspicious persistence mechanism.

---

## Persistence Consideration

Active Setup can be used by legitimate software to perform configuration actions when users log on.

However, the same type of registry mechanism could potentially be abused by an attacker for persistence.

Therefore, the important investigative question was not simply:

> "Was an Active Setup registry value modified?"

The more useful question was:

> "What does the modified value actually execute?"

In this case, the answer was a Microsoft Edge installer/configuration executable located in an expected software installation directory.

---

## Classification

**🟢 Benign / Expected Activity**

---

## Key SOC Lessons

1. Registry integrity alerts should be investigated rather than automatically classified as malicious.
2. Hash changes confirm that a registry value changed, but they do not establish malicious intent.
3. `StubPath` values should be examined to determine what executable or command they reference.
4. Legitimate software can modify registry values during installation or configuration.
5. File location is important when assessing the legitimacy of an executable.
6. Active Setup can have legitimate uses but should still be investigated when unexpected modifications occur.
7. The actual contents of a registry value provide more useful evidence than the alert title alone.

---

## Analyst Conclusion

Wazuh Rule 750 correctly detected a modification to an Active Setup `StubPath` registry value. Further investigation revealed that the value referenced the Microsoft Edge `setup.exe` executable within the expected installation directory and contained parameters consistent with Edge configuration activity. Based on the available evidence, the modification was assessed as benign and expected rather than malicious persistence.
