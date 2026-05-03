# Password-Manager-using-Cpp
A Self made C++ Project using greeksforgreeks learning.

-------

<div align="center">

# 🔐 Secure Password Manager

### A Military-Grade Encrypted Password Vault Built in C++

[![Language](https://img.shields.io/badge/Language-C%2B%2B17-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)](https://isocpp.org/)
[![Security](https://img.shields.io/badge/Security-Multi--Layer%20Encryption-red?style=for-the-badge&logo=shield&logoColor=white)](https://github.com/)
[![Platform](https://img.shields.io/badge/Platform-Cross--Platform-brightgreen?style=for-the-badge&logo=linux&logoColor=white)](https://www.onlinegdb.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)
[![Build](https://img.shields.io/badge/Build-Passing-success?style=for-the-badge&logo=github-actions&logoColor=white)](https://github.com/)
[![Standard](https://img.shields.io/badge/Standard-C%2B%2B17-blue?style=for-the-badge)](https://en.cppreference.com/w/cpp/17)

<br/>

*A complete, security-focused password management system featuring multi-layer encryption, PBKDF-lite key derivation, master password authentication with lockout, Binary Search Tree indexing, password strength analysis, and a rich terminal interface — all in a single compilable C++ file.*

<br/>


<p align="center">
  <a href="https://drive.google.com/file/d/1eGLz7qSRhOHhmsdCkgPkr_HXq7dX6vS1/view?usp=sharing" target="_blank">
    <img src="https://img.shields.io/badge/📄%20View-Project%20File-FF6F00?style=for-the-badge&logo=google-drive&logoColor=white" />
  </a>
</p>



```
  ╔══════════════════════════════════════════════╗
  ║   🔐  SECURE PASSWORD MANAGER               ║
  ║       Encryption  •  Storage  •  Safety      ║
  ╚══════════════════════════════════════════════╝
```

</div>

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Security Model](#-security-model)
- [Features](#-features)
- [Architecture & Tech Stack](#-architecture--tech-stack)
- [Encryption Deep Dive](#-encryption-deep-dive)
- [Data Structures & Algorithms](#-data-structures--algorithms)
- [Project Structure](#-project-structure)
- [Class Design (OOP)](#-class-design-oop)
- [Menu Options](#-menu-options)
- [File Storage Format](#-file-storage-format)
- [How to Run](#-how-to-run)
- [Sample Walkthrough](#-sample-walkthrough)
- [Edge Cases Handled](#-edge-cases-handled)
- [Security Considerations](#-security-considerations)
- [Future Enhancements](#-future-enhancements)

---

## 🌟 Overview

The **Secure Password Manager** is a fully featured, encrypted credential vault built entirely in **C++17**. It allows users to securely store, retrieve, generate, and audit passwords for any number of websites, applications, or services. All stored data is protected by a multi-layer encryption scheme derived from a single **master password** — meaning only the correct master password can decrypt and reveal any stored credential.

> **Design Goal:** Demonstrate real-world cryptography principles (key derivation, layered encryption, one-way hashing) combined with advanced C++ concepts (BST indexing, OOP, terminal UI) in a portable, single-file application.

### Why This Matters

| Without Password Manager | With This Password Manager |
|---|---|
| Reusing weak passwords everywhere | Unique strong password per site |
| Passwords stored in plain text files | All credentials encrypted at rest |
| No way to audit password health | Built-in strength auditing |
| Manual password creation | Cryptographically random generation |
| No access control | Master password + 3-attempt lockout |

---

## 🛡️ Security Model

```
┌─────────────────────────────────────────────────────────────────┐
│                      SECURITY LAYERS                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   User Input (Master Password)                                   │
│          │                                                       │
│          ▼                                                       │
│   ┌─────────────────────────────────┐                           │
│   │  PBKDF-lite Key Derivation      │  10,000–50,000 iterations │
│   │  password + random salt → key   │  64-byte derived key      │
│   └─────────────────────────────────┘                           │
│          │                      │                                │
│          ▼                      ▼                                │
│   ┌────────────┐        ┌──────────────────┐                    │
│   │  One-Way   │        │  Session Key     │                    │
│   │  Hash      │        │  (in memory)     │                    │
│   │  → .meta   │        │  cleared on lock │                    │
│   └────────────┘        └──────────────────┘                    │
│                                  │                               │
│                                  ▼                               │
│                    ┌──────────────────────────┐                  │
│                    │  3-Layer Encryption       │                  │
│                    │  Layer 1: XOR cipher      │                  │
│                    │  Layer 2: Caesar rotation │                  │
│                    │  Layer 3: Block reversal  │                  │
│                    │  Output:  Base64 encoded  │                  │
│                    └──────────────────────────┘                  │
│                                  │                               │
│                                  ▼                               │
│                         Encrypted .vault file                    │
└─────────────────────────────────────────────────────────────────┘
```

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔐 **Master Password Auth** | Single master password unlocks the entire vault |
| 🚫 **Brute-force Lockout** | Account locks after 3 failed login attempts |
| 🔑 **Session Key Management** | Encryption key lives only in RAM; wiped on lock/exit |
| 🧅 **Multi-layer Encryption** | XOR → Caesar rotation → block reversal → Base64 |
| 🧂 **Random Salt + PBKDF** | 32-byte random salt; 50,000-iteration key stretching |
| 🌳 **BST Title Index** | Binary Search Tree for fast credential lookup by title |
| 🔍 **Multi-mode Search** | By Title (BST), Category, Favorites, or ID |
| ✏️ **Full CRUD** | Add, View, Update, Delete password entries |
| 👁️ **Reveal with Re-auth** | Requires master password confirmation before showing any credential |
| 🎲 **Password Generator** | Configurable length, charset, generates 5 options simultaneously |
| 📊 **Strength Analyzer** | Real-time scoring with color-coded bar (WEAK / FAIR / GOOD / STRONG) |
| 🔍 **Security Audit** | Scans all entries and flags weak passwords |
| 🔄 **Master Password Change** | Re-encrypts every entry with new key atomically |
| ⭐ **Favorites** | Mark and filter favorite credentials |
| 📤 **Encrypted Export** | Backup export — passwords remain encrypted in output |
| 🔒 **Lock Vault** | Instant session lock; session key cleared from memory |
| 🏷️ **Categories** | Work / Personal / Banking / Social / Shopping / Other |

---

## 🏗️ Architecture & Tech Stack

```
┌────────────────────────────────────────────────────────────────────┐
│                   PASSWORD MANAGER APPLICATION                      │
├───────────────┬───────────────┬───────────────┬────────────────────┤
│  Crypto Layer │   OOP Layer   │   DSA Layer   │    UI/IO Layer     │
│               │               │               │                    │
│ • CryptoEngine│ • PasswordMgr │ • TitleIndex  │ • ANSI colors      │
│ • PBKDF-lite  │ • SecureStore │  (BST)        │ • Hidden input     │
│ • XOR cipher  │ • PasswordEnt │ • std::sort   │ • Unicode boxes    │
│ • Caesar rot  │ • BSTNode     │ • Strength    │ • Strength bars    │
│ • Block flip  │               │   Scoring     │ • Masked display   │
│ • Base64      │               │               │                    │
└───────────────┴───────────────┴───────────────┴────────────────────┘
```

### Technology Breakdown

| Technology | Implementation Details |
|---|---|
| **C++17** | Modern STL, structured bindings, range algorithms |
| **Encryption / Decryption** | 3-layer cipher: XOR → Caesar byte rotation → 8-byte block reversal → Base64 output |
| **Key Derivation (PBKDF-lite)** | 10,000 iterations for session key; 50,000 for master hash; 32-byte random salt; 64-byte output |
| **Master Password Auth** | One-way hash in `.meta`; session key in RAM only; 3-attempt lockout with progressive delay |
| **BST (Binary Search Tree)** | Custom BST indexes entry titles for O(log n) average-case insert and traversal |
| **Secure Storage** | Two-file system: `.vault` (encrypted entries) + `.meta` (salt + hash only) |
| **OOP & Encapsulation** | `CryptoEngine`, `PasswordManager`, `SecureStorage`, `TitleIndex`, `PasswordEntry` with single responsibility |
| **Sorting Algorithms** | `std::sort` with lambda comparators for title/category sorted display |
| **Password Strength Scoring** | Multi-factor 9-point scale across length + charset diversity with ANSI color output |
| **Terminal GUI** | ANSI escape codes, Unicode box-drawing, `termios`/`_getch` masked input, visual progress bars |

---

## 🔒 Encryption Deep Dive

### Key Derivation Function (PBKDF-lite)

The master password is **never stored directly**. Instead it is processed through a custom key derivation function:

```
MasterPassword + RandomSalt (32 bytes)
         │
         ▼
    Combined String
         │
         ▼  ×50,000 iterations (for hash) / ×10,000 (for session key)
    Mixing Loop:
        key[i] = ((key[i] × 31 + key[i+1]) XOR (iter×7+i)) & 0xFF
        key[i] XOR= key[i+7]
         │
         ▼
    64-byte derived key / one-way hash
```

| Parameter | Value |
|---|---|
| Salt length | 32 bytes (cryptographically random) |
| Key length | 64 bytes |
| Hash iterations | 50,000 |
| Session key iterations | 10,000 |
| Algorithm | Custom iterative mixing (XOR + multiply + rotate) |

### 3-Layer Encryption Pipeline

```
Plaintext Password
      │
      ▼  Layer 1 — XOR Cipher
      │  cipher[i] ^= key[i % 64]
      │
      ▼  Layer 2 — Caesar Byte Rotation
      │  cipher[i] = (cipher[i] + key[(i×3) % 64]) & 0xFF
      │
      ▼  Layer 3 — Block Reversal
      │  reverse every 8-byte block independently
      │
      ▼  Base64 Encoding
      │  ensure printable ASCII output safe for file storage
      │
  Ciphertext (stored in .vault)
```

Decryption applies all steps in exact reverse order:

```
Ciphertext → Base64 Decode → Undo Block Reversal
          → Undo Caesar Rotation → Undo XOR → Plaintext
```

### Two-File Security Split

```
my_vault.meta                        my_vault.vault
──────────────────────               ───────────────────────────────────────
RandomSalt (32 bytes)                1|Gmail|user@gmail.com|aGVsbG8=...|...
MasterPasswordHash (128 hex chars)   2|GitHub|johndoe|dGVzdA==...|...
                                     3|Netflix|john@mail.com|eW91cg==...|...

↑ Used ONLY for login verification    ↑ All passwords encrypted with session key
↑ Cannot decrypt vault entries         ↑ Useless without the session key
```

> **Key Insight:** Even if both files are stolen, an attacker cannot decrypt vault entries without brute-forcing the master password through the PBKDF-lite function — which costs significant compute time per attempt.

---

## 🧩 Data Structures & Algorithms

### 1. Binary Search Tree (TitleIndex)

The BST indexes every entry title in lowercase for fast lookup:

```
              netflix
             /       \
          github    spotify
          /    \       \
       amazon  gmail  youtube
```

| Operation | Complexity |
|---|---|
| Insert title | O(log n) average |
| Substring search | O(n) — full traversal for partial match |
| Rebuild on update/delete | O(n log n) |

### 2. Password Strength Scoring Algorithm

A 9-point weighted scoring system:

```
Score Factors:
  +1  length ≥ 8
  +1  length ≥ 12
  +1  length ≥ 16
  +1  contains uppercase (A-Z)
  +1  contains lowercase (a-z)
  +1  contains digits (0-9)
  +2  contains special characters (!@#$...)
  ─────────────────────────────────────────
  Max Score: 9

Thresholds:
  0–2  →  WEAK   (red)
  3–4  →  FAIR   (yellow)
  5–6  →  GOOD   (cyan)
  7–9  →  STRONG (green)
```

Visual output:
```
  Strength : STRONG (score: 7/9)
  [███████░░]
```

### 3. Password Generator Algorithm

| Property | Value |
|---|---|
| RNG Engine | `std::mt19937` seeded by `std::random_device` |
| Charset | lowercase + optional upper / digits / special |
| Options shown | 5 independent passwords per generation call |
| Min/Max length | 8 – 64 characters |

---

## 📁 Project Structure

```
password-manager/
│
├── password_manager.cpp      # Complete single-file application
│
├── my_vault.vault            # Auto-generated — encrypted entries
│                             # id|title|username|encPwd|url|category|notes|created|updated|fav
│
├── my_vault.meta             # Auto-generated — authentication data only
│                             # Line 1: random salt (32 chars)
│                             # Line 2: one-way master password hash (128 hex chars)
│
└── README.md                 # This file
```

> ⚠️ **Never share `my_vault.meta` or `my_vault.vault`.** Together with a guessed master password they could expose your credentials.

---

## 🎨 Class Design (OOP)

### Class Hierarchy & Responsibilities

```
┌───────────────────────────────────────────────────────────┐
│                  CryptoEngine              [static]        │
│  + deriveKey(pwd, salt, iters) → vector<uint8_t>          │
│  + hashPassword(pwd, salt) → string  [50k iterations]     │
│  + generateSalt(len) → string        [random_device]      │
│  + encrypt(plaintext, key) → string  [3-layer + Base64]   │
│  + decrypt(encoded, key) → string    [exact reverse]      │
└───────────────────────────────────────────────────────────┘
          ▲ used by
┌───────────────────────────────────────────────────────────┐
│                     PasswordEntry                          │
│  + id, title, username, encPassword, url                  │
│  + category, notes, createdAt, updatedAt: string          │
│  + isFavorite: bool                                       │
│  + displayMasked()     [password shown as ********]       │
│  + displayRevealed()   [decrypted password shown]         │
└───────────────────────────────────────────────────────────┘
          ▲
┌───────────────────────────────────────────────────────────┐
│                  TitleIndex  (BST)                         │
│  - root: BSTNode*                                         │
│  + insert(title, id)                                      │
│  + search(keyword) → vector<int>   [returns entry IDs]    │
│  + clear()                                                │
└───────────────────────────────────────────────────────────┘
          ▲
┌───────────────────────────────────────────────────────────┐
│                    SecureStorage                           │
│  - dataFile (.vault)    metaFile (.meta)                  │
│  + metaExists() → bool                                    │
│  + saveMeta(salt, hash)                                   │
│  + loadMeta() → pair<string, string>                      │
│  + saveEntries(vector<PasswordEntry>)                     │
│  + loadEntries() → vector<PasswordEntry>                  │
└───────────────────────────────────────────────────────────┘
          ▲
┌───────────────────────────────────────────────────────────┐
│               PasswordManager          [Core Orchestrator] │
│  - entries: vector<PasswordEntry>                         │
│  - bstIndex: TitleIndex                                   │
│  - storage: SecureStorage                                 │
│  - sessionKey: vector<uint8_t>  [cleared on lock]         │
│  - failedAttempts: int                                    │
│  + isFirstRun(), setupMaster(), login(), lock()           │
│  + changeMaster(old, new)  [re-encrypts all entries]      │
│  + addEntry(), deleteEntry(), updateEntry()               │
│  + revealPassword(id) → string  [decrypts on demand]      │
│  + searchByTitle(), searchByCategory(), getFavorites()    │
│  + auditPasswords() → vector<pair<Entry, Strength>>       │
│  + exportVault(filename)                                  │
└───────────────────────────────────────────────────────────┘
```

### Design Patterns Applied

| Pattern | Where Used |
|---|---|
| **Façade** | `PasswordManager` hides crypto + BST + storage complexity |
| **Static Factory** | `CryptoEngine` — stateless pure functions |
| **RAII** | `sessionKey.clear()` in `lock()` ensures no key lingers |
| **Single Responsibility** | Each class owns exactly one concern |
| **Guard Clause** | Every menu action validates preconditions, returns early on failure |
| **Separation of Concerns** | Auth, encryption, storage, and UI fully decoupled |

---

## 📋 Menu Options

```
  ┌────────────────────────────────────────────┐
  │             VAULT MENU                     │
  ├────────────────────────────────────────────┤
  │  1.  Add New Entry                         │
  │  2.  View All Entries                      │
  │  3.  Search Entries                        │
  │  4.  Reveal / View Password                │
  │  5.  Update Entry                          │
  │  6.  Delete Entry                          │
  │  7.  Password Generator                    │
  │  8.  Security Audit (Weak Passwords)       │
  │  9.  Statistics                            │
  │  10. Change Master Password                │
  │  11. Export Encrypted Backup               │
  │  12. Lock Vault                            │
  │  0.  Exit                                  │
  └────────────────────────────────────────────┘
  Vault: 12 entries  |  Status: 🔓 UNLOCKED
```

### Detailed Option Guide

#### `1` — Add New Entry
Prompts for: **Title**, **Username**, **Password** (manual or generated), **URL**, **Category**, **Notes**, **Favorite flag**
- Choose between **manual entry** (hidden input, no echo) or **auto-generate**
- Generated passwords display immediately with live strength bar
- Manually entered passwords confirmed via re-entry
- Password encrypted with session key before storage; saved to `.vault` immediately

#### `2` — View All Entries
Displays a **tabular list** of all entries sorted alphabetically by title. All passwords shown as `********` — never revealed in list view.

```
  ID    Title                 Username              Category     Fav
  ────────────────────────────────────────────────────────────────────
  3     GitHub                johndoe               Work
  1     Gmail                 user@gmail.com         Personal    ⭐
  4     Netflix               john@mail.com          Personal
```

#### `3` — Search Entries
Four modes: **By Title** (BST substring), **By Category** (exact filter), **By Favorites** (starred only), **By ID** (direct lookup)

#### `4` — Reveal / View Password
- Requires **re-entering the master password** before any credential is shown
- Displays full entry details including decrypted password
- Password strength bar shown alongside revealed credential

#### `5` — Update Entry
- Shows current values in `[current value]` format
- **Leave any field blank** to keep the existing value
- New password re-encrypted with session key; BST rebuilt; vault saved

#### `6` — Delete Entry
- Previews the full entry (masked) before deletion
- Requires typing **`yes`** exactly to confirm

#### `7` — Password Generator (Standalone)
- Configure: length (8–64), uppercase, digits, special characters
- Generates and displays **5 independent passwords** simultaneously

```
  1) K#9mLpQr@Xt2wYbN
  2) vH7$nJcRzA4kMoWe
  3) Bq3&fDsUiG8xTyPl
  4) mN5!hEoVjC6rKwZa
  5) Xp2@dLbMuF9yRtSk
```

#### `8` — Security Audit
- Decrypts and scores **every stored password** silently
- Lists all entries scoring WEAK or FAIR with color-coded labels

```
  ⚠  3 weak password(s) found:

  ID:2  Facebook   (WEAK)
  ID:7  Twitter    (FAIR)
  ID:9  OldEmail   (WEAK)

  Consider updating these passwords.
```

#### `9` — Statistics
Displays total entries count and per-category breakdown.

#### `10` — Change Master Password
- Verifies current master password; analyses new password strength
- **Atomically re-encrypts all entries** with new derived key
- New salt generated; `.meta` updated; `.vault` rewritten

#### `11` — Export Encrypted Backup
- Writes all entries to a `.txt` file — **passwords remain encrypted**
- Includes generation timestamp and entry count header
- Safe to store on cloud — no plaintext leakage

#### `12` — Lock Vault
- **Immediately wipes session key** from RAM
- Clears all in-memory entry data
- Returns to login screen; re-enter master password to unlock

---

## 💾 File Storage Format

### `.vault` — Encrypted Entries

```
id|title|username|encryptedPassword|url|category|notes|createdAt|updatedAt|isFavorite
```

Example content:
```
1|Gmail|user@gmail.com|aGVsbG8gd29ybGQ=...|https://gmail.com|Personal||2025-08-14 10:30|2025-08-14 10:30|1
2|GitHub|johndoe|dGVzdCBwYXNz...|https://github.com|Work|Dev account|2025-08-14 10:31|2025-08-14 10:31|0
```

> The `encryptedPassword` field is Base64-encoded ciphertext — meaningless without the session key.

### `.meta` — Authentication Data

```
<random_salt_32_chars>
<master_password_hash_128_hex_chars>
```

Example:
```
aB3kP9mNxQrZ7yWvUoLsEjFdCgHtIiMp
a3f2d1e4b5c6...8f9e0d1c2b3a4f5e6d7c8b9a0f1e2d3c4b5a6f7e8d9c0b1a2f3e4d5c6b7a8f9
```

### Storage Properties

| Property | Detail |
|---|---|
| **Entry format** | Pipe-delimited (`\|`) flat file |
| **Password field** | Always stored encrypted (Base64 ciphertext) |
| **Auth file** | Salt + one-way hash only — cannot decrypt vault |
| **Write policy** | Write-through on every mutation |
| **Corruption handling** | Malformed lines skipped silently on load |
| **Backup safety** | Exports keep passwords encrypted — safe for cloud |

---

## ▶️ How to Run

### Option A — GDB Online Compiler (Quick Start)

1. Go to **[https://www.onlinegdb.com](https://www.onlinegdb.com)**
2. Set language to **C++17**
3. Paste full contents of `password_manager.cpp`
4. Click **▶ Run**
5. On first launch, create your master password
6. Use the numbered menu to manage credentials

> ⚠️ Hidden password input (no-echo) may show characters in some online terminals. All logic still works correctly. File persistence between sessions is limited on online compilers.

---

### Option B — Local Compilation (Linux / macOS)

```bash
git clone https://github.com/yourusername/password-manager-cpp.git
cd password-manager-cpp

g++ -std=c++17 -o password_manager password_manager.cpp

./password_manager
```

### Option C — Local Compilation (Windows)

```cmd
g++ -std=c++17 -o password_manager.exe password_manager.cpp
password_manager.exe
```

### Option D — Using Makefile

```makefile
CXX      = g++
CXXFLAGS = -std=c++17 -Wall -O2
TARGET   = password_manager
SRC      = password_manager.cpp

all: $(TARGET)

$(TARGET): $(SRC)
	$(CXX) $(CXXFLAGS) -o $(TARGET) $(SRC)

clean:
	rm -f $(TARGET) *.vault *.meta *.txt
```

```bash
make
./password_manager
```

### Compiler Requirements

| Requirement | Minimum |
|---|---|
| **g++** | 7.0+ |
| **C++ Standard** | C++17 |
| **OS** | Windows / Linux / macOS / Online |
| **Dependencies** | None — standard library only |

---

## 🧪 Sample Walkthrough

```
# 1. First launch — create master password
./password_manager

  Welcome! First time setup.
Create master password : [hidden input]
Confirm master password: [hidden input]

  Strength : STRONG (score: 8/9)
  [████████░]
  ✓ Master password set. Vault initialized.

# 2. Login
Master Password: [hidden]
  Authenticating...
  ✓ Access granted!

# 3. Add a new entry (option 1)
Enter choice: 1
  Title/Site : Gmail
  Username   : user@gmail.com
  Password options: 1) Manual  2) Generate
  Choose: 2
  Length: 16

  Generated: K#9mLpQr@Xt2wYbN
  Strength : STRONG (score: 8/9)
  [████████░]

  Category : 2 (Personal)
  Favorite?: y
  ✓ Entry added and encrypted successfully!

# 4. Reveal a password (option 4)
Enter choice: 4
  Entry ID: 1
  🔐 Re-authentication required.
  Enter master password: [hidden]

  │  Password : K#9mLpQr@Xt2wYbN       │

# 5. Security audit (option 8)
Enter choice: 8
  Scanning for weak passwords...
  ✅ All passwords are strong! Great job.
```

---

## 🛡️ Edge Cases Handled

| Edge Case | Handling |
|---|---|
| **Empty title / password** | Validated before insertion; rejected with message |
| **Master password mismatch on setup** | Re-prompts until both entries match |
| **Wrong master password on login** | Decrement attempts; lock after 3 failures |
| **Vault locked after 3 attempts** | Prints lockout message; further input rejected |
| **Invalid ID for reveal/update/delete** | Returns "entry not found" gracefully |
| **Blank field on update** | Keeps existing value — no accidental overwrites |
| **Corrupt `.vault` line** | Wrapped in `try-catch`; malformed lines silently skipped |
| **`.meta` file missing** | `isFirstRun()` triggers first-time setup |
| **Non-integer ID input** | `try-catch` on `stoi`; re-prompts until valid |
| **Weak master password on setup** | Warns; asks explicit confirmation to proceed |
| **BST stale after update/delete** | Full BST rebuilt from vector after every structural change |
| **Session key after lock** | `sessionKey.clear()` + `entries.clear()` — nothing lingers |
| **Re-encrypt on password change** | All entries decrypted with old key, re-encrypted with new atomically |
| **Export file creation failure** | `try-catch` with user-facing error message |

---

## 🔬 Security Considerations

### What This Implementation Provides

- ✅ Passwords never stored in plaintext
- ✅ Master password never stored — only one-way hash
- ✅ Random per-vault salt prevents rainbow table attacks
- ✅ Key stretching (PBKDF-lite) increases brute-force cost
- ✅ Session key held only in RAM, wiped on lock
- ✅ Brute-force lockout after 3 failed attempts
- ✅ Re-authentication required before any password reveal
- ✅ Encrypted export — no accidental plaintext leakage
- ✅ Two-file split — `.meta` cannot decrypt `.vault` alone

### Known Limitations (Academic Project)

- ⚠️ The 3-layer cipher is **custom, not AES** — for production use, replace with OpenSSL AES-256-GCM
- ⚠️ PBKDF-lite is not PBKDF2/bcrypt/Argon2 — production systems should use one of these
- ⚠️ The session key is held in `std::vector<uint8_t>` — production would use `mlock()` / `SecureZeroMemory()`
- ⚠️ No integrity check (HMAC/MAC) on the vault file — tampering detectable but not authenticated

> **Note:** This project is designed to demonstrate cryptographic concepts in C++. For storing real production passwords, use established tools like [KeePass](https://keepass.info/), [Bitwarden](https://bitwarden.com/), or [1Password](https://1password.com/).

---

## 🚀 Future Enhancements

- [ ] **AES-256-GCM encryption** — replace custom cipher with OpenSSL AES
- [ ] **Argon2id key derivation** — memory-hard KDF for stronger brute-force resistance
- [ ] **HMAC integrity check** — detect vault file tampering
- [ ] **GUI Frontend** — Qt or wxWidgets graphical interface
- [ ] **TOTP / 2FA support** — store and generate time-based OTP codes
- [ ] **Password history** — track previous passwords per entry
- [ ] **Breach detection** — check via HaveIBeenPwned API (k-anonymity model)
- [ ] **Import from other managers** — parse KeePass XML, Bitwarden JSON
- [ ] **Clipboard integration** — copy password with auto-clear after 30s
- [ ] **Multiple vaults** — separate vaults for personal / work / family

---

## 📜 License

```
MIT License — Copyright (c) 2025

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
```

---

## 🙏 Acknowledgements

- **C++ Standard Library** — `<random>`, `<fstream>`, `<algorithm>` for core functionality
- **termios / conio.h** — platform-specific hidden password input
- **ISO C++17** — modern language features enabling clean expressive code
- **GDB Online** — browser-based compilation and testing platform
- **Cryptography Engineering** (Ferguson, Schneier, Kohno) — conceptual inspiration for layered cipher design

---

<div align="center">

**Built with 🔐 and C++17**

[![C++](https://img.shields.io/badge/C%2B%2B-17-00599C?style=flat-square&logo=cplusplus)](https://isocpp.org/)
[![Encryption](https://img.shields.io/badge/Encryption-Multi--Layer-red?style=flat-square)](https://en.wikipedia.org/wiki/Cipher)
[![BST](https://img.shields.io/badge/Index-BST-orange?style=flat-square)](https://en.wikipedia.org/wiki/Binary_search_tree)
[![PBKDF](https://img.shields.io/badge/KDF-PBKDF--lite-purple?style=flat-square)](https://en.wikipedia.org/wiki/PBKDF2)
[![No Dependencies](https://img.shields.io/badge/Dependencies-None-brightgreen?style=flat-square)](https://github.com/)

*⭐ Star this repo if you found it helpful!*

</div>
