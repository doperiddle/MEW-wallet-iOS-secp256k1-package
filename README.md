# MEW-wallet-iOS-secp256k1-package

A Swift Package Manager wrapper for the [secp256k1](https://github.com/MyEtherWallet/MEW-wallet-iOS-secp256k1) C library, optimized for use in iOS and macOS applications.

## Overview

This package provides a convenient way to integrate the high-performance secp256k1 elliptic-curve cryptography library into Swift projects via Swift Package Manager. It is used by [MyEtherWallet](https://github.com/MyEtherWallet) to support Ethereum key management and cryptographic operations on Apple platforms.

## Features

- **ECDSA signing and verification** — Sign messages and verify signatures using the secp256k1 curve.
- **Key generation** — Generate secret and public key pairs.
- **Key serialization/parsing** — Serialize and parse secret keys, public keys, and signatures.
- **Public key recovery** — Recover a public key from a signature (via the optional recovery module).
- **ECDH key exchange** — Perform Elliptic-curve Diffie-Hellman key agreement (via the optional ECDH module).
- **Constant-time operations** — Signing and public key generation are designed to be free of timing side-channels.
- **Derandomized ECDSA** — Signatures use RFC 6979 for deterministic nonce generation.

## Requirements

- Swift 5.2 or later
- iOS 10.0+ / macOS 10.12+
- Xcode 11.4+

## Installation

### Swift Package Manager

Add this package as a dependency in your `Package.swift`:

```swift
dependencies: [
    .package(url: "https://github.com/doperiddle/MEW-wallet-iOS-secp256k1-package.git", from: "1.0.0")
]
```

Then add `"MEW-wallet-iOS-secp256k1-package"` to your target's dependencies:

```swift
targets: [
    .target(
        name: "YourTarget",
        dependencies: ["MEW-wallet-iOS-secp256k1-package"]
    )
]
```

In Xcode, you can add the package via **File → Add Packages…** and enter the repository URL.

## Usage

Import the module in your Swift file:

```swift
import MEW_wallet_iOS_secp256k1_package
```

The package exposes the secp256k1 C API directly. Refer to the [secp256k1 header](Sources/MEW-wallet-iOS-secp256k1/include/secp256k1.h) and the module headers for `secp256k1_ecdh.h` and `secp256k1_recovery.h` for the full API surface.

### Example: Verifying a context is created

```swift
import MEW_wallet_iOS_secp256k1_package

// Create a secp256k1 context for signing and verification
let context = secp256k1_context_create(UInt32(SECP256K1_CONTEXT_SIGN | SECP256K1_CONTEXT_VERIFY))
defer { secp256k1_context_destroy(context) }
```

## License

This package wraps the [libsecp256k1](https://github.com/MyEtherWallet/MEW-wallet-iOS-secp256k1) library, which is distributed under the MIT license. See the library's [COPYING](Sources/MEW-wallet-iOS-secp256k1/COPYING) file for details.
