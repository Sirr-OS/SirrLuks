# SirrLuks

SirrLuks is a minimal, interactive tool for changing the password of a LUKS-encrypted device.
It is designed to safely rotate LUKS passphrases by adding a new key first and only removing the old one after successful validation.

The tool is written entirely in Bash and relies on cryptsetup for all cryptographic operations.

---

## Purpose

The goal of SirrLuks is to provide a simple and controlled way to change the passphrase of a LUKS volume without risking data loss.

It follows the safest possible sequence:

1. Add a new LUKS key
2. Verify success
3. Remove the old LUKS key

If any step fails, the existing key remains valid.

---

## Features

* Interactive, password-hidden input
* Safe LUKS key rotation logic
* Prevents empty or mismatched passwords
* Uses cryptsetup batch mode
* No background services
* No configuration files
* Clear error handling

---

## Requirements

* Linux system using LUKS encryption
* Root privileges
* cryptsetup installed
* A valid block device configured in the script

By default, the target device is:

```
/dev/mmcblk2p2
```

This can be changed by editing the script.

---

## Usage

Run the tool as root:

```
sudo sirrluks
```

You will be prompted for:

* Current LUKS password
* New password
* Password confirmation

Passwords are never echoed to the terminal.

---

## Safety Notes

* The script adds the new LUKS key before removing the old one
* If adding the new key fails, no changes are made
* If removing the old key fails, the new key remains valid

This design minimizes the risk of locking yourself out of the encrypted device.

---

## Warnings

* This tool modifies encryption keys on disk
* Incorrect usage may cause permanent data loss
* Always ensure you know at least one valid LUKS password before proceeding
* Use only on devices you fully control

---

## Security Model

* No passwords are stored on disk
* Password variables are unset on exit
* cryptsetup is called using batch mode
* Requires direct root access

---

## Project Philosophy

* Minimal and auditable Bash code
* Explicit operations, no automation magic
* Fail fast on errors

---

## Author

Commander.Z3R0
