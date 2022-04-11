# ERC721AX

Bridging the optimality-gap in [ERC721A](https://github.com/chiru-labs/ERC721A) in a realistic minting setup.

Keeps variables such as `collectionSize` and `maxPerWallet` internally, so that we don't need an extra sload. Also keeps track of whether the next token data has already been set before, so that we don't have to check it (1 sload) on every transfer for all eternity.

Further optimization could be achieved by storing the number of minted nfts in a certain batch and then back-calculating if a certain tokenId is the last in the batch. I.e. if A mints 5 ids, `A 0 0 0 0` is stored. Now, if we transfer the last id in the batch, we know that the token following that one will have to be explicitly set, so we can skip an sload check.

[Gas snapshot](.gas-snapshot)

```
forge snapshot --match-contract GasTest
```
