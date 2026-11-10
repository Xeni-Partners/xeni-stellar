# Xeni on Stellar

Migrating Xeni's agentic travel-payment stack from **USDC on Hedera** to **USDC on Stellar**, and moving the full 450,000+ wallet base to production. Travelers pay for bookings in USDC from their own non-custodial wallet — first by authorizing a chosen deal, then fully autonomously against a signed intent (target price, dates, star rating, distance from a landmark) — and Xeni settles suppliers in USDC on the same network.

Proposed to the **Stellar Community Fund** (Integration Track).

## Why Stellar

Every mechanism Xeni hand-built on Hedera has a native Stellar counterpart, so the migration leans on the platform instead of fighting it:

| Built on Hedera | Native Stellar primitive |
|---|---|
| Agent as named fee-payer (user pays no gas token) | Fee-bump transactions |
| Single on-chain `user→agent` allowance | Soroban SEP-41 `approve` / `transfer_from` |
| Planned agent payment rail (x402) | Built-on-Stellar x402 Facilitator |
| Creating 450k+ accounts | Sponsored reserves |

## Documents

- **[Technical Architecture Document](docs/Technical-Architecture-Document.pdf)** — what exists today (Hedera), the primitive-by-primitive mapping to Stellar, the target two-seam design (a Stellar MCP replacing the Hedera H-MCP for agent payments; a XeniPay chains adapter replacing Hedera HTS for settlement), the architecture diagram, and an end-to-end sub-system sequence.
- **[Project Plan](docs/Project-Plan.pdf)** — delivery staged across three Integration-Track tranches.

## Delivery at a glance

| Tranche | Milestone | Duration | Network |
|---|---|---|---|
| 1 | Interactive flow — build + test | 5 weeks | testnet |
| 2 | Autonomous intent-based flow — build + test | 3 weeks | testnet |
| 3 | Migrate 450,000+ wallets + production rollout | 4 weeks | mainnet |

## Core invariants

- The agent **never holds user funds** — USDC stays in the traveler's wallet until the treasury transfer.
- The user **never pays the gas token** — the agent account is the named fee-payer.
- Agent spend is **bounded by a signed allowance**, enforced server-side.
- Every payment and refund is **audited**, and the money path is idempotent (no double-pay).

## Branches

- `develop` — integration (default)
- `master` — release

---

*Not affiliated with or endorsed by the Stellar Development Foundation.*
