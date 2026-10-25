<div align="center">

# ◈ MemWallet

**Deterministic cryptocurrency wallet generator for Bitcoin, Ethereum, Litecoin & Monero**

*Like WarpWallet — but for altcoins.*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Live Demo](https://img.shields.io/badge/Live%20Demo-online-brightgreen)](https://abdallahp2p.github.io/MemWallet/)
[![GitHub Pages](https://img.shields.io/badge/Hosted%20on-GitHub%20Pages-blue)](https://abdallahp2p.github.io/MemWallet/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/AbdallahP2P/MemWallet/pulls)

👉 **[🚀 Open MemWallet Live →](https://abdallahp2p.github.io/MemWallet/)**

</div>

---

## 📖 Table of Contents

- [Overview](#-overview)
- [Live Demo](#-live-demo)
- [Features](#-features)
- [How It Works](#-how-it-works)
- [Algorithm](#-algorithm)
- [Getting Started](#-getting-started)
- [Project Structure](#-project-structure)
- [Security Considerations](#-security-considerations)
- [Roadmap](#-roadmap)
- [Contributing](#-contributing)
- [Official Sources](#-official-sources)
- [License](#-license)
- [Acknowledgements](#-acknowledgements)

---

## 🌟 Overview

**MemWallet** is a **fully client-side, offline-capable, deterministic** cryptocurrency wallet generator. It derives public addresses and private keys from a human-memorable **passphrase** and an optional **salt** — no servers, no storage, no external assets.

This repository is a **professionally maintained fork and modernization** of the original [MemWallet](https://github.com/dvdbng/memwallet) by **David Bengoa**, which itself was inspired by [WarpWallet](https://keybase.io/warp/).

The goal of this fork is to:

- 🎨 **Redesign** the UI with a clean, modern, responsive dark theme.
- 🧹 **Restructure** the codebase for easier maintenance and future contributions.
- 🔧 **Fix** layout and compatibility bugs.
- 📚 **Document** the algorithm, security model, and usage thoroughly.

### Supported Cryptocurrencies

| Cryptocurrency | Algorithm ID (`b`) | Status |
|----------------|:------------------:|:------:|
| **Bitcoin**    | `1`                | ✅     |
| **Litecoin**   | `2`                | ✅     |
| **Ethereum**   | `3`                | ✅     |
| **Monero**     | `4`                | ✅     |

> **No private keys are ever stored.**  
> If you remember your passphrase and salt, you can regenerate your wallet anytime, anywhere.

---

## 🔗 Live Demo

The official hosted version of **this fork** is available at:

### 👉 [https://abdallahp2p.github.io/MemWallet/](https://abdallahp2p.github.io/MemWallet/)

> ⚠️ For maximum security, download the page and run it on an **offline computer** (air-gapped).

---

## ✨ Features

- 🔐 **Deterministic** — Same passphrase + salt always produces the same wallet.
- 🌐 **Multi-coin support** — Bitcoin, Ethereum, Litecoin, and Monero.
- 📴 **Fully offline** — No external assets; save the page and run it air-gapped.
- 🧂 **Optional salt** — Strengthen your wallet with an email, phone number, or phrase.
- ⚡ **Scrypt + PBKDF2** — Memory-hard and time-hard key derivation.
- 🎨 **Modern UI** — Clean, responsive dark theme built with pure CSS variables.
- 📱 **Mobile-friendly** — Fully responsive layout for all screen sizes.
- 🛡️ **Security-first** — No tracking, no analytics, no network calls.
- 🧾 **Auditable** — JavaScript left un-minified for offline review.

---

## ⚙️ How It Works

1. **Choose** your cryptocurrency (Bitcoin, Ethereum, Litecoin, or Monero).
2. **Enter** a strong passphrase (e.g., 6–12 random words from [Diceware](https://www.eff.org/dice)).
3. *(Optional)* Provide a **salt** — your email or phone number works well.
4. **Click Generate.**
5. MemWallet runs `scrypt` and `PBKDF2` locally in your browser and displays:
   - ✅ Public address
   - 🔑 Private key
   - 👁️ *(Monero only)* View key and Spend key

**No data leaves your device.** All computation happens in your browser.

---

## 🧮 Algorithm

MemWallet uses the exact same derivation as WarpWallet for Bitcoin, with a coin-specific domain separator `b`:

| Step | Formula |
|------|---------|
| `b`  | `1` = Bitcoin, `2` = Litecoin, `3` = Ethereum, `4` = Monero |
| `seed₁` | `scrypt(key = passphrase ‖ b, salt = salt ‖ b, N = 2¹⁸, r = 8, p = 1, dkLen = 32)` |
| `seed₂` | `pbkdf2(key = passphrase ‖ (b+1), salt = salt ‖ (b+1), c = 2¹⁶, dkLen = 32, PRF = SHA256)` |
| `wallet` | `generate_wallet(seed = seed₁ ⊕ seed₂)` |

This dual-KDF approach makes brute-force attacks **memory-intensive** and **time-intensive**, offering far stronger protection than traditional brainwallets.

> 📖 For a detailed explanation, see the [original WarpWallet documentation](https://keybase.io/warp/).

---

## 🚀 Getting Started

### Prerequisites

- A modern web browser (Chrome, Firefox, Safari, Edge).
- **No Node.js, no build tools, no server required.**

### Local Usage (Offline)

```bash
# 1. Clone this fork
git clone https://github.com/AbdallahP2P/MemWallet.git
cd MemWallet

# 2. Open in your browser
# (Linux/macOS)
open index.html
# (Windows)
start index.html
# (or just double-click index.html in your file explorer)
