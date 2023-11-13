# 🥶 Staking Support

Elixir can integrate your current staking platform so holders can benefit from their NFT when they stake. To support staking on your NFT Collection, you'll need to provide the support team with an API that provides the wallets and their staked NFTs following the format:

```javascript
[
   wallet_id1: [nft_id1, nft_id2, nft_id3...],
   wallet_id2: [nft_id1, nft_id2, nft_id3...],
   wallet_id3: [nft_id1, nft_id2, nft_id3...],
   ...
]
```

We wanted to be aligned with the ecosystem, and with this mind we implemented the standard settled by [Matrica](https://docs.matrica.io/guides/community-guide/staking-support), so you don't have to do things twice.
