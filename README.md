# Solana Real-Time Indexer CLI

A command-line tool for indexing Solana blockchain data in real-time using Yellowstone gRPC. Monitor accounts, transactions, slots, blocks, and more with an interactive CLI.

## Demo
![Demo](https://github.com/akshaydhayal/Solana-Real-Time-Indexer/blob/main/solana-indexer-demo.gif)

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
cargo build

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

ACCOUNTS INDEXED DATA
```bash
================================================================================
📦 Update Type: ACCOUNT
🔍 Filters: client
⏰ Timestamp: 1765864485.079305
--------------------------------------------------------------------------------
  data: 736572756d03000000000000006ac4c3cefa9f19bf54c8dc0f5e4d1ceee5327d26482b29d2b13cbaa43447218d0100000000... (truncated, 776 chars)
  executable: false
  isStartup: false
  lamports: 5458084
  owner: srmqPvymJeFKQ4zGQed1GFppgkRHL9kaELCbyksJtPX
  pubkey: 8BnEgHoWFysVcuFFX7QztDmzuH8r5ZFvyP3sYwn1XTh6
  rentEpoch: 18446744073709551615
  slot: 387021217
  txnSignature: JcquUNVDznQcSpdjqrQuJsKK7z9g91oUuAfh9N8gdu3cNFqPzcoaLWgg6MQVD8KCeXrP1jUNDXFUNuc422K22Ki
  writeVersion: 1537985469364
================================================================================
```

TRANSACTION INDEXED DATA
```bash
================================================================================
📦 Update Type: TRANSACTION
🔍 Filters: client
⏰ Timestamp: 1765864231.708303
--------------------------------------------------------------------------------
  isVote: false
  signature: ZpXDocoYu7JVcFH2Frt9RXDMRqnVmeP3jaT6rrVEUR3Guf7aN5CQ4AeXQFVwFRKfghPqmFQccqBKVbS1ncQ4FmQ
  slot: 387020561
  tx: {"meta":{"computeUnitsConsumed":215648,"costUnits":223695,"err":null,"fee":12600,"innerInstructions":[{"index":2,"instructions":[{"accounts":[15],"data":"84eT","programIdIndex":17,"stackHeight":2},{"accounts":[0,2],"data":"11119os1e9qSs2u7TsThXqkBSRVFxhmYaFKFZ1waB2X7armDmvK3p5GmLdUxYdg3h7QSrL","programIdIndex":16,"stackHeight":2},{"accounts":[2],"data":"P","programIdIndex":17,"stackHeight":2},{"accounts":[2,15],"data":"6dpFtf6pzGuUucpTSMCu6WZineNWGPTS1UsheJNJLDuq9","programIdIndex":17,"stackHeight":2}]},{"index":5,"instructions":[{"accounts":[25,19],"data":"2BfZXS1GQrCLYKfSSHGxWziZfgGAyj1VLmdYHUPPEYjYeb","programIdIndex":26,"stackHeight":2},{"accounts":[2,15,5,0],"data":"jM4tinaZsVAC8","programIdIndex":17,"stackHeight":2},{"accounts":[6,21,4,3],"data":"hUPBxrDs8GrW9","programIdIndex":17,"stackHeight":2},{"accounts":[6,21,7,3],"data":"hqeZQ8AWk4Ajw","programIdIndex":17,"stackHeight":2},{"accounts":[23],"data":"9k6unfwB8yYie7YGjfXzMuTpZe6gCeJoVg85whcBhahnczSo8bw1af6Vw7SzHTEVzTi7xTpEz5Kb3h3p19TLLKJgPboUdEmLuiK91unHHkutPc1VEVBzUsX5CQCq4L1gvSZJtaxybyEyPymyCmNxBCVwpdjHv4xyNmdLzdKG3iVnfPJAVwqL6FhxrVXTyibtYRrfSnWQuhtvw8Jr71fmGMe2s2UMh8CMzZpsxzBjJAoggmqdkzDT4yYRpCMMaUYeNwfhtkDH8qULQVU6adq6pePQ9LeiYbD76gzpxvPAhgRyPm2LQiJJBug2SceYewcgmEFaoNmUBDsYFX5nZ6s8XTgJVsEbriXEbBVAgg1XPzh7C8A8Uofs9XJof6zjMZtVDD3DYMQ71jLjC4FrwQfmrhwNmTyDa18c39QT5aihWbF81L6yCB82BXDgCc5JTamCd43yiDvmwfgAoKSu9cSYXAwXHYT5PnYLomJYmqp7xdC3ELXi6dT8AWs","programIdIndex":19,"stackHeight":2}]},{"index":7,"instructions":[{"accounts":[15],"data":"84eT","programIdIndex":17,"stackHeight":2},{"accounts":[1,9],"data":"11119os1e9qSs2u7TsThXqkBSRVFxhmYaFKFZ1waB2X7armDmvK3p5GmLdUxYdg3h7QSrL","programIdIndex":16,"stackHeight":2},{"accounts":[9],"data":"P","programIdIndex":17,"stackHeight":2},{"accounts":[9,15],"data":"6Yy1beMYFs2nM4Ecb6EaEBhR9U3dqypygEmQXq7VFrVWP","programIdIndex":17,"stackHeight":2}]},{"index":8,"instructions":[{"accounts":[25,19],"data":"2BfZXS1GQrCLYKfSSHGxWziZfgGAyj1VLmdUZbmdNuVkKZ","programIdIndex":26,"stackHeight":2},{"accounts":[5,15,9,3],"data":"irbtQzPcJfLx8","programIdIndex":17,"stackHeight":2},{"accounts":[10,21,6,1],"data":"gBYAHu7yYcTim","programIdIndex":17,"stackHeight":2},{"accounts":[10,21,7,1],"data":"hkhJ4c1zPwmNd","programIdIndex":17,"stackHeight":2},{"accounts":[23],"data":"2R73ve6nZ42SoaP8dDaUWgTYxyQufgSWGZXgvdYEgYBZ1xFhgCRekBZBRdJvogTLwvcSVgU5W3b9bG4napEcLgZxJg4hxQtw8ya7kDAb2qfGLG9qpjVr7iRC8Q22789pq1QCsz6QMXQ2Wmsc4pdaNGoStqSkDfVZYe85iKBTzSN4MShf6aBDfLGLbudKJrU6A2Epq92ydsgrNJoRXchawRcMT3xwHGcwtRw9HiNWzWF9EXvoUcv4JQEnjmGmfFc2UidjGiwaEzAyJgUzqZrEVZbT8GUeAwrzbYgMByuGEaSYCgcQkpEYJENQ7tWwmQfpbDwUZED1CH4Wy34nMCaEQ1tYXsi2ueaKj5uyHEah9A2RRpoaAw7cRvNWRn446KEq8zkBScgJp7h3mSsfbbYJzNRp19d1WpYY8adp7X2gCpkGGwc4usBsdZZamGKBCbZFTn3onugJ7fWaPKUam66AdXRMXdyt8tAqvRLjo5Z3QHduY46ANjv8SgBemEtUFjQMXgEH2D5bNUD3QFtmZ4hp3Ss1ytwqMq5T1JQPG95DTrxxrAhog5NJtoqip","programIdIndex":19,"stackHeight":2}]}],"loadedAddresses":{"readonly":[],"writable":[]},"logMessages":["Program ComputeBudget111111111111111111111111111111 invoke [1]","Program ComputeBudget111111111111111111111111111111 success","Program ComputeBudget111111111111111111111111111111 invoke [1]","Program ComputeBudget111111111111111111111111111111 success","Program ATokenGPvbdGVxr1b2hvZbsiqW5xWH25efTNsLJA8knL invoke [1]","Program log: Create","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [2]","Program log: Instruction: GetAccountDataSize","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 1569 of 251333 compute units","Program return: TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA pQAAAAAAAAA=","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success","Program 11111111111111111111111111111111 invoke [2]","Program 11111111111111111111111111111111 success","Program log: Initialize the associated token account","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [2]","Program log: Instruction: InitializeImmutableOwner","Program log: Please upgrade to SPL Token 2022 for immutable owner support","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 1405 of 244746 compute units","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [2]","Program log: Instruction: InitializeAccount3","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 3158 of 240864 compute units","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success","Program ATokenGPvbdGVxr1b2hvZbsiqW5xWH25efTNsLJA8knL consumed 22277 of 259700 compute units","Program ATokenGPvbdGVxr1b2hvZbsiqW5xWH25efTNsLJA8knL success","Program 11111111111111111111111111111111 invoke [1]","Program 11111111111111111111111111111111 success","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [1]","Program log: Instruction: SyncNative","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 3045 of 237273 compute units","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success","Program pAMMBay6oceH9fJKBRHGP5D4bD4sWpmSwMn52FMfXEA invoke [1]","Program log: Instruction: Sell","Program pfeeUxB6jkeY1Hxd7CsFCAjcbHA9rWtchMGdZ6VojVZ invoke [2]","Program log: Instruction: GetFees","Program pfeeUxB6jkeY1Hxd7CsFCAjcbHA9rWtchMGdZ6VojVZ consumed 4274 of 199449 compute units","Program return: pfeeUxB6jkeY1Hxd7CsFCAjcbHA9rWtchMGdZ6VojVZ GQAAAAAAAAAFAAAAAAAAAAAAAAAAAAAA","Program pfeeUxB6jkeY1Hxd7CsFCAjcbHA9rWtchMGdZ6VojVZ success","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [2]","Program log: Instruction: TransferChecked","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 6238 of 191414 compute units","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [2]","Program log: Instruction: TransferChecked","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 6147 of 182303 compute units","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [2]","Program log: Instruction: TransferChecked","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 6147 of 173268 compute units","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success","Program data: Pi83CqUD3Com80BpAAAAAP7QNvYAAAAAT/4k/kQDAAD+0Db2AAAAAEoN5S9dAQAAJ+OZHfEAAAAo2y/EEDsDAJf/4DJJAwAAGQAAAAAAAACkAF4aAgAAAAUAAAAAAAAAiGasawAAAADz/oIYRwMAAGuY1qxGAwAAQAHbROi0MXn6smmsm6I3Hp3bVkpKLqEEm8a1fQhvjjn33RKqdgYezcHnStEVnkajod/QLZA960Lc2WG7PbECqESsorBnnuSzzwth/J0DeYiM3zepb1HfIweOQ6wLGH0TCUdO58m2ViZGFo6rZlatIk+b7mkbY24UvZ7T3Lthisn/g4OBi6j6KMPNO21ek/n6uPCXm8NyFazFskaHe6jDyYuxqr7UbrH65qTNdDODUUCmu4eFMEqRPh3CNgNBxNfAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA","Program pAMMBay6oceH9fJKBRHGP5D4bD4sWpmSwMn52FMfXEA invoke [2]","Program pAMMBay6oceH9fJKBRHGP5D4bD4sWpmSwMn52FMfXEA consumed 2036 of 160633 compute units","Program pAMMBay6oceH9fJKBRHGP5D4bD4sWpmSwMn52FMfXEA success","Program pAMMBay6oceH9fJKBRHGP5D4bD4sWpmSwMn52FMfXEA consumed 76869 of 234228 compute units","Program pAMMBay6oceH9fJKBRHGP5D4bD4sWpmSwMn52FMfXEA success","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [1]","Program log: Instruction: CloseAccount","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 2915 of 157359 compute units","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success","Program ATokenGPvbdGVxr1b2hvZbsiqW5xWH25efTNsLJA8knL invoke [1]","Program log: Create","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [2]","Program log: Instruction: GetAccountDataSize","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 1569 of 149077 compute units","Program return: TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA pQAAAAAAAAA=","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success","Program 11111111111111111111111111111111 invoke [2]","Program 11111111111111111111111111111111 success","Program log: Initialize the associated token account","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [2]","Program log: Instruction: InitializeImmutableOwner","Program log: Please upgrade to SPL Token 2022 for immutable owner support","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 1405 of 142490 compute units","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [2]","Program log: Instruction: InitializeAccount3","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 3158 of 138608 compute units","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success","Program ATokenGPvbdGVxr1b2hvZbsiqW5xWH25efTNsLJA8knL consumed 19277 of 154444 compute units","Program ATokenGPvbdGVxr1b2hvZbsiqW5xWH25efTNsLJA8knL success","Program pAMMBay6oceH9fJKBRHGP5D4bD4sWpmSwMn52FMfXEA invoke [1]","Program log: Instruction: Buy","Program pfeeUxB6jkeY1Hxd7CsFCAjcbHA9rWtchMGdZ6VojVZ invoke [2]","Program log: Instruction: GetFees","Program pfeeUxB6jkeY1Hxd7CsFCAjcbHA9rWtchMGdZ6VojVZ consumed 4274 of 90562 compute units","Program return: pfeeUxB6jkeY1Hxd7CsFCAjcbHA9rWtchMGdZ6VojVZ GQAAAAAAAAAFAAAAAAAAAAAAAAAAAAAA","Program pfeeUxB6jkeY1Hxd7CsFCAjcbHA9rWtchMGdZ6VojVZ success","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [2]","Program log: Instruction: TransferChecked","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 6238 of 82421 compute units","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [2]","Program log: Instruction: TransferChecked","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 6147 of 73383 compute units","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [2]","Program log: Instruction: TransferChecked","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 6147 of 64452 compute units","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success","Program data: Z/RSHyz1d3cm80BpAAAAANhBf74AAAAAf+TuhZcCAAAAAAAAAAAAAIrVU++dBAAAJbTQE/IAAAA13KyryTcDAIG/WkKKAgAAGQAAAAAAAACFdyqgAQAAAAUAAAAAAAAAgbE7UwAAAAAGN4XiiwIAAIfowDWMAgAAQAHbROi0MXn6smmsm6I3Hp3bVkpKLqEEm8a1fQhvjjmv0LQ8je7/812Hx3WzRYgBDvaR7fzI9k/gdepwvRbGIN3+FLWG3VS97+gZvBRviw4QBfcRi5271O20IBa5cKs5liP/4UM5f1+vCsRJ11BY+8vt63FmI1OgRB4x/jxdCrT/g4OBi6j6KMPNO21ek/n6uPCXm8NyFazFskaHe6jDyYuxqr7UbrH65qTNdDODUUCmu4eFMEqRPh3CNgNBxNfAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA2EF/vgAAAAADAAAAYnV5","Program pAMMBay6oceH9fJKBRHGP5D4bD4sWpmSwMn52FMfXEA invoke [2]","Program pAMMBay6oceH9fJKBRHGP5D4bD4sWpmSwMn52FMfXEA consumed 2036 of 51057 compute units","Program pAMMBay6oceH9fJKBRHGP5D4bD4sWpmSwMn52FMfXEA success","Program pAMMBay6oceH9fJKBRHGP5D4bD4sWpmSwMn52FMfXEA consumed 87900 of 135167 compute units","Program pAMMBay6oceH9fJKBRHGP5D4bD4sWpmSwMn52FMfXEA success","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [1]","Program log: Instruction: CloseAccount","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 2915 of 47267 compute units","Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success"],"postBalances":[23095533211,27426506932,0,2589120,2039280,1036520558653,2039280,2039280,2039280,0,2039280,25068917,1844400,1,3316541054,1258599172628,1,5315277768,0,1129860422,5359209,1461600,3185965552635,1002088,0,18374415,1159717],"postTokenBalances":[{"accountIndex":4,"mint":"Ejw8VHkEpehDMEYBroqhqWJdy7BFQhjig8AdNMjAgxUd","owner":"HgZDiuJBz4D5MLMvG3hm2bHQ9UvSyiAJmxXnoncWvmQB","programId":"TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA","uiTokenAmount":{"amount":"5101829465525","decimals":6,"uiAmount":5101829.465525,"uiAmountString":"5101829.465525"}},{"accountIndex":5,"mint":"So11111111111111111111111111111111111111112","owner":"5Jrjc6w2UEGxFYfnyvvX9VdEovXyJkCaXwFXo525za8x","programId":"TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA","uiTokenAmount":{"amount":"1036518519373","decimals":9,"uiAmount":1036.518519373,"uiAmountString":"1036.518519373"}},{"accountIndex":6,"mint":"Ejw8VHkEpehDMEYBroqhqWJdy7BFQhjig8AdNMjAgxUd","owner":"5Jrjc6w2UEGxFYfnyvvX9VdEovXyJkCaXwFXo525za8x","programId":"TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA","uiTokenAmount":{"amount":"908564062409531","decimals":6,"uiAmount":908564062.409531,"uiAmountString":"908564062.409531"}},{"accountIndex":7,"mint":"Ejw8VHkEpehDMEYBroqhqWJdy7BFQhjig8AdNMjAgxUd","owner":"JCRGumoE9Qi5BBgULTgdgTLjSgkCMSbF62ZZfGs84JeU","programId":"TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA","uiTokenAmount":{"amount":"7226065006695","decimals":6,"uiAmount":7226065.006695,"uiAmountString":"7226065.006695"}},{"accountIndex":8,"mint":"Ejw8VHkEpehDMEYBroqhqWJdy7BFQhjig8AdNMjAgxUd","owner":"8N3GDaZ2iwN65oxVatKTLPNooAVUJTbfiVJ1ahyqwjSk","programId":"TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA","uiTokenAmount":{"amount":"0","decimals":6,"uiAmount":0.0,"uiAmountString":"0"}},{"accountIndex":10,"mint":"Ejw8VHkEpehDMEYBroqhqWJdy7BFQhjig8AdNMjAgxUd","owner":"CqJviA1TaBWWnkX515NthiykyA42a5hyXrEgLXoSZM5R","programId":"TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA","uiTokenAmount":{"amount":"2275151113475","decimals":6,"uiAmount":2275151.113475,"uiAmountString":"2275151.113475"}}],"preBalances":[27226333393,24230495964,0,2589120,2039280,1035585782039,2039280,2039280,2039280,0,2039280,25068917,1844400,1,3316541054,1258599172628,1,5315277768,0,1129860422,5359209,1461600,3185965552635,1002088,0,18374415,1159717],"preTokenBalances":[{"accountIndex":4,"mint":"Ejw8VHkEpehDMEYBroqhqWJdy7BFQhjig8AdNMjAgxUd","owner":"HgZDiuJBz4D5MLMvG3hm2bHQ9UvSyiAJmxXnoncWvmQB","programId":"TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA","uiTokenAmount":{"amount":"1499747126602","decimals":6,"uiAmount":1499747.126602,"uiAmountString":"1499747.126602"}},{"accountIndex":5,"mint":"So11111111111111111111111111111111111111112","owner":"5Jrjc6w2UEGxFYfnyvvX9VdEovXyJkCaXwFXo525za8x","programId":"TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA","uiTokenAmount":{"amount":"1035583742759","decimals":9,"uiAmount":1035.583742759,"uiAmountString":"1035.583742759"}},{"accountIndex":6,"mint":"Ejw8VHkEpehDMEYBroqhqWJdy7BFQhjig8AdNMjAgxUd","owner":"5Jrjc6w2UEGxFYfnyvvX9VdEovXyJkCaXwFXo525za8x","programId":"TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA","uiTokenAmount":{"amount":"909368127118120","decimals":6,"uiAmount":909368127.11812,"uiAmountString":"909368127.11812"}},{"accountIndex":7,"mint":"Ejw8VHkEpehDMEYBroqhqWJdy7BFQhjig8AdNMjAgxUd","owner":"JCRGumoE9Qi5BBgULTgdgTLjSgkCMSbF62ZZfGs84JeU","programId":"TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA","uiTokenAmount":{"amount":"7222862125150","decimals":6,"uiAmount":7222862.12515,"uiAmountString":"7222862.12515"}},{"accountIndex":8,"mint":"Ejw8VHkEpehDMEYBroqhqWJdy7BFQhjig8AdNMjAgxUd","owner":"8N3GDaZ2iwN65oxVatKTLPNooAVUJTbfiVJ1ahyqwjSk","programId":"TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA","uiTokenAmount":{"amount":"0","decimals":6,"uiAmount":0.0,"uiAmountString":"0"}},{"accountIndex":10,"mint":"Ejw8VHkEpehDMEYBroqhqWJdy7BFQhjig8AdNMjAgxUd","owner":"CqJviA1TaBWWnkX515NthiykyA42a5hyXrEgLXoSZM5R","programId":"TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA","uiTokenAmount":{"amount":"5076371625354","decimals":6,"uiAmount":5076371.625354,"uiAmountString":"5076371.625354"}}],"rewards":[],"status":{"Ok":null}},"transaction":["AhxNWT7j1PcqXNZ6FF6N12maiftFRc5im9KOke8OOW8C+8e5lSLstiUonc4Hn+OdJNgZh55/rCVp+1ce7WzI2A8xZjzaxY0B3WzhSdBkFTvXNKypld99iB6uAJc5RayBrg5Jef7mcuJ0s4mNcNtoRmGQ6mVne0+yVvWzSCpYXWMCgAIADhv33RKqdgYezcHnStEVnkajod/QLZA960Lc2WG7PbECqK/QtDyN7v/zXYfHdbNFiAEO9pHt/Mj2T+B16nC9FsYgRKyisGee5LPPC2H8nQN5iIzfN6lvUd8jB45DrAsYfRNAAdtE6LQxefqyaaybojcendtWSkouoQSbxrV9CG+OOQlHTufJtlYmRhaOq2ZWrSJPm+5pG2NuFL2e09y7YYrJEYZohzFyFfRZO1/L9h3obN3AXNs6X870A7VjB3TwhJxYh+r56iOtEj3Kov5AWOknmxZq4T1C+yQRmnt3gIbQn4uxqr7UbrH65qTNdDODUUCmu4eFMEqRPh3CNgNBxNfA9IJ64SoQuZwBqpTXPKZa+358AqRvJdnqA32n+lN4C2Xd/hS1ht1Uve/oGbwUb4sOEAX3EYudu9TttCAWuXCrOZYj/+FDOX9frwrESddQWPvL7etxZiNToEQeMf48XQq0o9e7En5YrcEspo+DQ37C4cP5gg3pPlj5F4opGN2q97QkY/djpFrOgtSx9+ra1AW2lg8foIUeBj2MJUxAR48L1AMGRm/lIRcy/+ytunLDm+e8jOW7xfcSayxDmzpAAAAAjJclj04kifG7PRApFI4NgwtaE5na/xCEBI572Nvp+FkGm4hX/quBhPtof2NGGMA12sQ53BrrO1WYoPAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABt324ddloZPZy+FGzut5rBy0he1fWzeROoz1hX7/AKkK8cNDIYjKOmNRNaE6GJUazr0p5qwtrmf/2wbXQW5zKAwU3vyCXsZ2lCUIGLtlQGX0KY0xVtVxtNT4CQwY6ahjiQumRP4fVaoZ8RzS0uwU0yM7bgpL6u73K2mFjiHhcNbMJ4cqas+O9mpK184W48vyzxJbeiPfaCob4Cnj5ReiZv+Dg4GLqPoow807bV6T+fq48Jebw3IVrMWyRod7qMPJ5UpwlSiDn2HAubhgeYkcE5IW5Hpxti+3O+xyFpRYdF5tZZBDuqUqGBtYRCOejVQtH97c1oHOfnHQdSnayW4mrUEkbsx9eP6B5BdzpGllQZk3kjoHZEeX328+tRRCYBDLDDX/qQVajlaNqPe8B1YVJ0zxySykH0AAnFFqpBTCfHBHT+JAdocypSo5nd7dT28KEk55fGdrvliymESiiZ3DPQoNAAUCoPcDAA0ACQMQJwAAAAAAAA4GAAIADxARABADAAISDAIAAAD+0Db2AAAAABEBAgERExUDABQPFQIEBQYWBxEREA4XEwgYGRoYM+aFpAF/g63+0Db2AAAAAE/+JP5EAwAAEQMCAAABCQ4GAQkBDxARABMXAwEUDxUJCgUGFgcRERAOFxMIGAsMGRoZZgY9EgHa6+rYQX++AAAAAH/k7oWXAgAAABEDCQEBAQkA","base64"],"version":0}
================================================================================
```

BLOCKMETA INDEXED DATA
```bash
  ================================================================================
📦 Update Type: BLOCKMETA
🔍 Filters: client
⏰ Timestamp: 1765863842.956715
--------------------------------------------------------------------------------
  blockHeight: 365163407
  blockTime: 1765863841
  blockhash: DBCd8xsVQEHmUiQ37mWVMjarAbLTDj9fF1fRanJ6u5Tn
  entriesCount: 358
  executedTransactionCount: 1009
  parentBlockhash: C92pA8EtfQRjWo2cYHrym1ztpWSEWootjzAX8yNyWTkH
  parentSlot: 387019566
  rewards: {"num_partitions":null,"rewards":[{"commission":null,"lamports":12432005,"postBalance":13702275176,"pubkey":"radM7PKUpZwJ9bYPAJ7V8FXHeUmH1zim6iaXUKkftP9","rewardType":"Fee"}]}
  slot: 387019567
================================================================================
```

SLOT INDEXED DATA
```bash
================================================================================
📦 Update Type: SLOT
🔍 Filters: client
⏰ Timestamp: 1765863971.803431
--------------------------------------------------------------------------------
  deadError: null
  parent: 387019892
  slot: 387019893
  status: SLOT_PROCESSED
================================================================================
```
## Configuration

The `.env` file uses:
- `GRPC_ENDPOINT`: Solana gRPC endpoint URL
- `X_TOKEN`: Authentication token

**Note**: Default free endpoint works, but using your own endpoint in `.env` provides better performance and reliability.

