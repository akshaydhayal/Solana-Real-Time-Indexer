# Solana Real-Time Indexer CLI

A command-line tool for indexing Solana blockchain data in real-time using Yellowstone gRPC. Monitor accounts, transactions, slots, blocks, and more with an interactive CLI.

## Features

- 🔄 Real-time indexing of accounts, transactions, slots, blocks, entries, and block metadata
- 🔍 Query commands: get latest blockhash, block height, slot, validate blockhashes
- ⚡ Commitment levels: Processed, Confirmed, or Finalized
- 🎨 Interactive hierarchical menu with all options visible
- ⚙️ `.env` configuration for endpoint (default free endpoint included)
- 📈 Pretty formatted output with clear field separation

## What It Does

Connects to Solana gRPC (Yellowstone) to:
- Subscribe to real-time updates (accounts, transactions, slots, blocks)
- Query blockchain info (slot, block height, blockhash validation)
- Monitor specific accounts/transactions with filters
- Index data at your chosen commitment level

## Quick Start

### Prerequisites
- Rust (latest stable)

### Installation & Run

```bash
# Build
cargo build --release

# Run interactively (recommended)
cargo run --bin client
```

### Configuration

Edit `.env` file:
```env
# Default free endpoint (already configured)
GRPC_ENDPOINT=https://solana-rpc.parafi.tech:10443
X_TOKEN=10443

# 💡 Tip: Use your own endpoint for faster response!
# GRPC_ENDPOINT=https://your-endpoint.com:443
# X_TOKEN=your-token
```

## Usage

### Interactive Mode

1. **Main Menu**: Select what to index/query
   - 📊 Index Data → Accounts, Transactions, Slots, Blocks, Entries, Block Meta
   - 🔍 Query Commands → Get blockhash, slot, block height, validate blockhash
   - ❤️ Health Check

2. **Commitment Level**: Choose Processed/Confirmed/Finalized

3. **Configure**: Endpoint/token auto-loaded from `.env`

### Examples

**Index Accounts:**
```bash
cargo run --bin client
# Select: Index Data → Accounts → Choose commitment → Enter pubkey(s)
```

**Query Latest Blockhash:**
```bash
cargo run --bin client
# Select: Query Commands → Get Latest Blockhash → Choose commitment
```

**Command-Line (Non-Interactive):**
```bash
# Subscribe to accounts
cargo run --bin client -- subscribe --accounts --accounts-account <Pubkey>

# Get latest blockhash
cargo run --bin client -- get-latest-blockhash

# Health check
cargo run --bin client -- health-check
```

## Output

All updates show:
- Clear separators between responses
- Each field on a new line
- Formatted timestamps
- Truncated long data for readability

## Configuration

The `.env` file uses:
- `GRPC_ENDPOINT`: Solana gRPC endpoint URL
- `X_TOKEN`: Authentication token

**Note**: Default free endpoint works, but using your own endpoint in `.env` provides better performance and reliability.

