---
sidebar_position: 2
sidebar_label: How to mint a Basic NFT on-chain
---

# How to mint a Basic NFT on-chain

## Prerequisites

Before getting started, make sure you have the following ready:

1. Create a [Ternoa account](/for-developers/get-started/create-account) with [Alphanet CAPS](/for-developers/get-started/create-account#step-2-get-some-free-test-caps-tokens)
2. Install and set up your editor of choice (we will use Visual Studio Code [VSC] in this tutorial)
3. Install [NodeJS v.14+](https://nodejs.org/en/download/) & NPM
4. [Install & initialize Ternoa-JS](/for-developers/get-started/install-ternoa-js)

## Minting a Basic NFT on-chain using Ternoa-JS

To create an NFT on the Ternoa chain, Ternoa-JS provides you with a `createNft` helper to do so. It returns an object promise containing the `NFTCreatedEvent` returned by the Ternoa blockchain.

Replace _IPFS_CID_ in the following code snippet with your CID hash previously generated in ["How to prepare Basic NFT assets"](/for-developers/guides/NFT/basic-NFT/prepare-assets):

```typescript showLineNumbers
import { createNft, getKeyringFromSeed, WaitUntil } from "ternoa-js";

const mintNFT = async () => {
	try {
		const keyring = await getKeyringFromSeed("//TernoaTestAccount");
		const nftData = await createNft(
			"IPFS_CID",
			0,
			undefined,
			false,
			keyring,
			WaitUntil.BlockInclusion
		);
		console.log("The on-chain NFT id is: ", nftData.nftId);
	} catch (e) {
		console.error(e);
	}
};
```

:::info

Use your own account by updating the `//TernoaTestAccount` with your account seed when retrieving the keyring from the example below.

:::

Here are detailed the `createNft` helper parameters:

```markdown
`offchainData`: a string that can be IPFS CID hash that points to a JSON file, a plain text, a small JSON string, or a link to either a static or a dynamic file.
`royalty`: a number (in percentage between 0 and 100) to set the royalties taken by the owner for each NFT sale.
`collectionId`: an optional parameter. If you want your NFT to belong to a collection, add the collection id here otherwise keep it undefined.
`isSoulbound`: (boolean): when set to true, the NFT will be a soulbound NFT. The default is false.
`keyring`: the provided keyring (containing the address) will be used to sign the transaction and pay the execution fee.
`waitUntil`: WaitUntil defines at which point we want to get the results of the transaction execution: BlockInclusion or BlockFinalization.
```

The response returned includes all the information below according to the parameters provided when creating the NFT. Note that `MintFee` refers to the fee paid to mint the NFT in Big Number format (`MintFeeRounded` is the humanized format, easier and more friendly to use).

```markdown
`nftId`: ID of the NFT.
`owner`: The owner of the NFT.
`offchainData`: The off-chain data provided for the NFT.
`royalty`: The royalty fee set for the NFT.
`collectionId`: The ID of the collection, the NFT belongs to.
`isSoulbound`: True if the NFT is soulbound. False if the NFT is not soulbound.
`mintFee`: Minting fee for the NFT. Big Number format
`mintFeeRounded`: Minting fee for the NFT. Basic number format.
```

## Next

The next step will be getting the NFT data from the Ternoa Indexer using the NFT id just generated. Keep it and continue on the ["How to retrieve a Basic NFT"](/for-developers/guides/NFT/basic-NFT/get-NFT) guide.

## Support

If you face any trouble, feel free to reach out to our community engineers in our [Discord](https://discord.gg/fUmBkPpnRu).
