# MerkleTree WhiteList NFT

![68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f7468756d622f392f39352f486173685f547265652e7376672f3139323070782d486173685f547265652e7376672e706e67](https://user-images.githubusercontent.com/102038261/223790581-5f432975-4bdf-485b-8480-d5c6d5ad6ade.png)

Simple implementation of a Merkle Tree Whitelist for an NFT smart contract.


---

### Libraries used to generate the Merkle tree and verify a wallet is inside of the Merkle tree with the proof:

- keccak256

```
npm i keccak256
```

- MerkleTreejs

```
npm i merkletreejs
```
⬇ <a href="https://github.com/CristianRicharte6/MerkleTree-WhiteList-NFT/blob/main/merkleTree.js" target="_blank">merkleTree.js</a> ⬇

```javascript
const { MerkleTree } = require("merkletreejs");
const keccak256 = require("keccak256");
const wallet = keccak256("0x5B38Da6a701c568545dCfcB03FcB875f56beddC4");

const leaves = [
  "0x5B38Da6a701c568545dCfcB03FcB875f56beddC4",
  "0x70997970C51812dc3A010C7d01b50e0d17dc79C8",
  "0x03C6FcED478cBbC9a4FAB34eF9f40767739D1Ff7",
  "0x70997970C51812dc3A010C7d01b50e0d17dc79C8",
  "0x03C6FcED478cBbC9a4FAB34eF9f40767739D1Ff7",
];

// Create Root.
const tree = new MerkleTree(leaves, keccak256, {
  /** If set to `true`, the leaves will hashed using the set hashing algorithms. */
  hashLeaves: true,
  /** If set to `true`, the hashing pairs will be sorted. */
  sortPairs: true,
});

// Get root hash of the tree.
const root = tree.getHexRoot();

// Get Proof from the root hash.
const proof = tree.getHexProof(wallet);

//Solidity needs it to have " double quotes" instead of `single quotes`
const merkleProof = [
  "0x9da258265696d227eef589fd6cd14671a82aa2963ec2214eb048fca5441c4a7e",
  "0xcf1af5889bea11e72fa5ccf227f07abc63b97b8f599e45dff51bb45c16a680bd",
  "0xbedabe7d0bfc2ec1d2a619d63dff4699d816c857675c1cd6ce376dd39ab5d092",
  "0x1c6df1b72628f8ee596a55eaa3078be04c45ce70bd92b04a719c065f92165690",
  "0x42d2024a9a9eb2572b5985038caf67e7af6228905cef6f38fe929b40f5c73d46",
];

module.exports = { merkleProof, root, wallet };
```
----------------
## Development

Install dependencies

```
npm install
```

Test the contract by passing an address in the Whitelist and an addres not in the Whitelist
```
npx hardhat test
```
