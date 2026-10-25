# MemWallet

> **Deterministic cryptocurrency wallet generator for Bitcoin, Ethereum, Litecoin & Monero**  
> Like WarpWallet — but for altcoins.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live-brightgreen)](https://dvdbng.github.io/memwallet)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Live Demo](#live-demo)
- [How It Works](#how-it-works)
- [Algorithm](#algorithm)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Security Considerations](#security-considerations)
- [Contributing](#contributing)
- [Official Sources](#official-sources)
- [License](#license)
- [Acknowledgements](#acknowledgements)

---

## Overview

**MemWallet** is a fully client-side, deterministic cryptocurrency address generator. It derives public addresses and private keys from a human-memorable **passphrase** and an optional **salt** — no storage, no servers, no external assets required.

Originally inspired by [WarpWallet](https://keybase.io/warp/), MemWallet extends the same battle-tested algorithm to support **four major cryptocurrencies**:

| Cryptocurrency | Algorithm ID (`b`) |
|----------------|-------------------|
| Bitcoin        | `1`               |
| Litecoin       | `2`               |
| Ethereum       | `3`               |
| Monero         | `4`               |

> **No private keys are ever stored.**  
> If you remember your passphrase and salt, you can regenerate your wallet anytime, anywhere.

---

## Features

- 🔐 **Deterministic** — Same passphrase + salt always yields the same wallet.
- 🌐 **Multi-coin support** — Bitcoin, Ethereum, Litecoin, and Monero.
- 📴 **Fully offline** — No external assets; save the page and run it air-gapped.
- 🧂 **Optional salt** — Strengthen your wallet with an email, phone number, etc.
- ⚡ **Scrypt + PBKDF2** — Memory-hard and time-hard key derivation.
- 📱 **Responsive UI** — Clean, modern dark theme built with pure CSS.
- 🛡️ **Security-first** — No tracking, no analytics, no network calls.

---

## Live Demo

Try MemWallet instantly (no installation required):

👉 **[https://dvdbng.github.io/memwallet](https://dvdbng.github.io/memwallet)**

> ⚠️ For maximum security, download the page and run it on an **offline computer**.

---

## How It Works

1. Choose your cryptocurrency (Bitcoin, Ethereum, Litecoin, or Monero).
2. Enter a strong **passphrase** (e.g., 6–12 random words).
3. (Optional) Provide a **salt** — your email or phone number works well.
4. Click **Generate**.
5. MemWallet runs `scrypt` and `PBKDF2` locally in your browser and displays:
   - Public address
   - Private key
   - (For Monero) View key and Spend key

No data leaves your device.

---

## Algorithm

MemWallet uses the exact same derivation as WarpWallet for Bitcoin, with a coin-specific domain separator `b`:

| Step | Formula |
|------|---------|
| `b`  | `1` = Bitcoin, `2` = Litecoin, `3` = Ethereum, `4` = Monero |
| `seed₁` | `scrypt(key = passphrase ‖ b, salt = salt ‖ b, N = 2¹⁸, r = 8, p = 1, dkLen = 32)` |
| `seed₂` | `pbkdf2(key = passphrase ‖ (b+1), salt = salt ‖ (b+1), c = 2¹⁶, dkLen = 32, PRF = SHA256)` |
| `wallet` | `generate_wallet(seed = seed₁ ⊕ seed₂)` |

This dual-KDF approach makes brute-force attacks **memory-intensive** and **time-intensive**, offering far stronger protection than traditional brainwallets.

> For a detailed explanation, see the [original WarpWallet documentation](https://keybase.io/warp/).

---

## Getting Started

### Prerequisites

- A modern web browser (Chrome, Firefox, Safari, Edge).
- No Node.js, no build tools, no server required.

### Local Usage (Offline)

1. Clone the repository:
   ```bash
   git clone https://github.com/AbdallahP2P/memwallet.git
   cd memwallet
   
