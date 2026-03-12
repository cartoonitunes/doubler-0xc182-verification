# Doubler (0xc182) Verification

Byte-for-byte verification of a **Doubler** pyramid scheme contract deployed on Ethereum mainnet.

| Field | Value |
|-------|-------|
| Contract | [`0xc1824278b767d9efb304c63128b1a92babc3fa4b`](https://etherscan.io/address/0xc1824278b767d9efb304c63128b1a92babc3fa4b) |
| Block | 1,028,387 |
| Date | February 19, 2016 |
| Deployer | `0x4f691fb14282fd40517511b47d33fed39dbd6a69` |
| Compiler | soljson v0.2.1+commit.91a6b35f (emscripten) |
| Optimizer | Enabled |
| Runtime | 1,137 bytes (exact match) |
| Creation | 1,183 bytes |
| Balance | ~28 ETH (locked forever) |

## What Is This?

A Ponzi/pyramid scheme from early Ethereum. New participants call `enter()` with at least 1 ETH. The contract takes a 10% fee and queues them for a 2x payout funded by later entrants. The owner can drain accumulated fees via `collectFees()`.

28 ETH remain locked in the contract, belonging to participants who entered too late to ever be paid out.

## How It Works

1. `enter()` -- Join with at least 1 ETH
2. First participant's entire deposit goes to fees (no one above to pay)
3. Subsequent deposits: 10% to fees, 90% to balance
4. When balance exceeds 2x the next-in-line participant's deposit, they receive 180% (2x minus the 10% fee already taken)
5. `collectFees()` -- Owner withdraws accumulated fees
6. `setOwner(address)` -- Transfer ownership

## Verification

```bash
./verify.sh
```

Requires Node.js. Downloads the solc binary automatically.

## Notes

This is a different deployment than the [Doubler at 0x2ff2a65b](https://etherscan.io/address/0x2ff2a65b0a324c04747bfdc63f4bf525d43e5c62) (block 883,117), which used the native C++ solc v0.2.0 compiler. This contract uses the emscripten (JavaScript) build of soljson v0.2.1, producing different bytecode from the same source pattern.

The "Doubler" template was one of the most commonly deployed contract patterns in early Ethereum, with dozens of variants across 2015-2016.

## Part Of

- [awesome-ethereum-proofs](https://github.com/cartoonitunes/awesome-ethereum-proofs)
- [EthereumHistory.com](https://ethereumhistory.com)
