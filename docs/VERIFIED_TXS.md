# Verified Transactions

All transactions on Solana devnet. Click to verify on Explorer.

---

## Program & Token

| Item | Address | Explorer |
|------|---------|----------|
| Program | `2R6Lus9psfB2dREDuC79ayfwd4peVfqG3Q42ca2iFhNV` | [View](https://solscan.io/account/2R6Lus9psfB2dREDuC79ayfwd4peVfqG3Q42ca2iFhNV?cluster=devnet) |
| IDL Account | `FDnuHMzje5EsyWqJUiTScbUJwBfQUgmD5B6VKG1qC5xS` | [View](https://solscan.io/account/FDnuHMzje5EsyWqJUiTScbUJwBfQUgmD5B6VKG1qC5xS?cluster=devnet) |
| PDOX Token | `4ckvALSiB6Hii7iVY9Dt6LRM5i7xocBZ9yr3YGNtVRwF` | [View](https://solscan.io/token/4ckvALSiB6Hii7iVY9Dt6LRM5i7xocBZ9yr3YGNtVRwF?cluster=devnet) |

---

## Settlement Transactions

### Batch Netting Settlement

```
TX: 5b1MtoyP1BRVn7SgfQtKCTyHDE1mfFD4k1oC8DtJmjnexrSWaBRvxJ1HgP6GYFYwZmzoVNpfwW2cVuLF1HVo9YJo
```

[View on Explorer](https://explorer.solana.com/tx/5b1MtoyP1BRVn7SgfQtKCTyHDE1mfFD4k1oC8DtJmjnexrSWaBRvxJ1HgP6GYFYwZmzoVNpfwW2cVuLF1HVo9YJo?cluster=devnet)

**What it proves:**
- `settle_net_batch` instruction executed successfully
- Program ID matches our deployed program
- Batch ID incremented (replay protection)
- Cash deltas applied

---

### Anonymous Payment

```
TX: 32YDUGw5kSsMSJ8KvdAwaAAKxJEA3YLnN8dvjx5DCb6cy49xXPa4NkpAeE5K7y3LDogyiFxSBDBgHcwkhGsxeTvh
```

[View on Explorer](https://explorer.solana.com/tx/32YDUGw5kSsMSJ8KvdAwaAAKxJEA3YLnN8dvjx5DCb6cy49xXPa4NkpAeE5K7y3LDogyiFxSBDBgHcwkhGsxeTvh?cluster=devnet)

**What it proves:**
- Payment routed through vault
- Sender and receiver don't directly transact
- Vault acts as intermediary

---

### Token Transfer (PDOX)

```
TX: 4LaL3ctzQYWuRGBUDWnL2TuMdeDJh2iEYWB6PgAJh3GzNhvrouKdcBg1ed3Gafd8euXcyibBrnPg4euacouEcjLC
```

[View on Explorer](https://explorer.solana.com/tx/4LaL3ctzQYWuRGBUDWnL2TuMdeDJh2iEYWB6PgAJh3GzNhvrouKdcBg1ed3Gafd8euXcyibBrnPg4euacouEcjLC?cluster=devnet)

**What it proves:**
- Token-2022 transfer works
- Transfer fee collected automatically
- Integration functional

---

### Temporal Paradox (Multi-layer)

```
TX: 45FZorwpTQgJuTS4dmpQE2GnGeaQChbiiUTx8odBRKRjfkMwzC9wZbjkbQJVuTj1SMK9hnBZLDNwt3BLxMezffa
```

[View on Explorer](https://explorer.solana.com/tx/45FZorwpTQgJuTS4dmpQE2GnGeaQChbiiUTx8odBRKRjfkMwzC9wZbjkbQJVuTj1SMK9hnBZLDNwt3BLxMezffa?cluster=devnet)

**What it proves:**
- Multi-layer anonymity path works
- 10-layer Hydra shard scatter tested
- Settlement completes successfully

---

## Test Results Summary

| Test | Target | Actual | Status | TX |
|------|--------|--------|--------|-----|
| Batch settlement | Success | Success | ✓ PASS | 5b1Mtoy... |
| Anonymous payment | A→B hidden | A→B hidden | ✓ PASS | 32YDUGw... |
| Token transfer | 3% fee | 3% fee | ✓ PASS | 4LaL3ct... |
| Replay protection | Reject dupe | Rejected | ✓ PASS | N/A |
| Cash conservation | sum=0 | sum=0 | ✓ PASS | N/A |
| Multi-layer anon | 10 layers | 10 layers | ✓ PASS | 45FZorw... |

---

## Merkle Roots

From actual batches:

| Batch | Intents | Root |
|-------|---------|------|
| Test 1 | 1,000 | `94164fb6fdbf78ecf19d8fd496e376567fdc82c488bff2e667754777793f9958` |

Verify at [TestLabs](https://labsx402.github.io/test/docs/test.html)

---

## How to Verify

### 1. Check Program Exists

```bash
solana program show 2R6Lus9psfB2dREDuC79ayfwd4peVfqG3Q42ca2iFhNV --url devnet
```

Expected output includes:
- `Program Id: 2R6Lus9psfB2dREDuC79ayfwd4peVfqG3Q42ca2iFhNV`
- `Executable: true`

### 1b. Fetch IDL (Anchor)

```bash
anchor idl fetch 2R6Lus9psfB2dREDuC79ayfwd4peVfqG3Q42ca2iFhNV --provider.cluster devnet
```

### 2. Check Token Exists

```bash
spl-token display 4ckvALSiB6Hii7iVY9Dt6LRM5i7xocBZ9yr3YGNtVRwF --url devnet
```

### 3. Verify TX on Explorer

1. Click any TX link above
2. Check "Result: Success"
3. Check "Program" matches our Program ID
4. Check instruction name matches claim

### 4. Verify Merkle Root

1. Go to [TestLabs](https://labsx402.github.io/test/docs/test.html)
2. Upload same intents JSON
3. Computed root must match

---

## Chain of Custody

All TXs signed by deployer wallet:
```
4VFatZLVLcVkmpJeNgwNffw3gzyCMAZeQ6jcSADGz5Tz
```

GlobalConfig authority (can submit batches):
```
Controlled by deployer during devnet testing
```

---

## Timestamps

| Event | Approximate Date |
|-------|------------------|
| Token minted (PDOX) | Nov 29, 2025 |
| Program v2.0.2 deployed | Nov 30, 2025 |
| IDL uploaded | Nov 30, 2025 |
| Stack overflow fixes | Nov 30, 2025 |

*Exact timestamps visible in Explorer TX details*

---

## Deploy Info (v2.0.2)

```
Program ID: 2R6Lus9psfB2dREDuC79ayfwd4peVfqG3Q42ca2iFhNV
IDL Account: FDnuHMzje5EsyWqJUiTScbUJwBfQUgmD5B6VKG1qC5xS
Deploy TX: 22nA19rTqfatoNCvMWR3vUf44u7yQc4jsYcCoG47eXEcGP8wQsGAEpL4KQq6cF6kEP387XEX8iJKuE1xX7FgRvAK
Deployer: 3XBBYhqcV5fdF1j8Bs97wcAbj9AYEeVHcxZipaFcefr3
```

---

## Updates

This document updated when new verified tests are run.

Last update: 2025-11-30

