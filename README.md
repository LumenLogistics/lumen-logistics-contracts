# OrbitHaul Smart Contracts 🛰️📦
> **Soroban smart contracts powering immutable logistics tracking and automated settlements for OrbitHaul.**

This repository contains the core on-chain logic for the OrbitHaul platform. Written in Rust and deployed on the Stellar network via Soroban, these contracts handle the secure escrow of funds, tokenized shipment creation, and automated payouts triggered by verified supply chain milestones.

---

## ✨ Features

*   **Automated Escrow:** Securely lock funds upon shipment creation and automatically release them to carriers upon successful delivery verification.
*   **Immutable Milestone Tracking:** Record transit events (e.g., picked up, at customs, delivered) directly on-chain for tamper-proof visibility.
*   **Role-Based Access Control:** Strict authorization checks to ensure only assigned shippers, carriers, and receivers can update shipment statuses.
*   **Stellar Network Integration:** Optimized for low fees and high throughput using the Soroban environment.

## 🛠 Tech Stack

*   **Language:** Rust
*   **Smart Contract Environment:** Soroban (Stellar)
*   **Testing:** Rust native test framework `#[cfg(test)]`

## 🚀 Getting Started

### Prerequisites

To build and test the contracts locally, you will need to set up your Rust and Soroban development environment:

1.  **Install Rust:**
    ```bash
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    ```

2.  **Add the WebAssembly target:**
    ```bash
    rustup target add wasm32-unknown-unknown
    ```

3.  **Install the Soroban CLI:**
    ```bash
    cargo install --locked soroban-cli
    ```

### Building the Contracts

To compile the smart contracts into WebAssembly (`.wasm`) binaries optimized for deployment:

```bash
cargo build --target wasm32-unknown-unknown --release
```

To optimize the build further for deployment (minimizing the `.wasm` file size):

```bash
soroban contract optimize --wasm target/wasm32-unknown-unknown/release/orbithaul_contracts.wasm
```

### Running Tests

Run the native Rust test suite to ensure all escrow and milestone logic is functioning correctly before deployment:

```bash
cargo test
```

## 📦 Deployment

You can deploy the optimized `.wasm` file to the Stellar Testnet using the Soroban CLI.

1. Generate a Testnet identity (if you don't have one):

```bash
soroban config identity generate admin
soroban config network add --global testnet \
  --rpc-url https://soroban-testnet.stellar.org:443 \
  --network-passphrase "Test SDF Network ; September 2015"
```

2. Deploy the contract:

```bash
soroban contract deploy \
  --wasm target/wasm32-unknown-unknown/release/orbithaul_contracts.wasm \
  --source admin \
  --network testnet
```

> Make sure to save the outputted Contract ID to use in the OrbitHaul frontend and backend services!

## 🏗 Repository Structure

```
├── Cargo.toml          # Rust dependencies and workspace configuration
├── src/
│   ├── lib.rs          # Contract entry point and public interface
│   ├── escrow.rs       # Logic for locking and releasing funds
│   ├── storage.rs      # Data structures for state management
│   ├── events.rs       # Contract event emissions for the indexer
│   └── test.rs         # Unit and integration tests
└── README.md           # Project documentation
```

## 🤝 Contributing

Contributions make the open-source community an amazing place to learn, inspire, and create. Any contributions you make are greatly appreciated.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/SmartEscrow`)
3. Commit your Changes (`git commit -m 'Add SmartEscrow feature'`)
4. Push to the Branch (`git push origin feature/SmartEscrow`)
5. Open a Pull Request

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.
