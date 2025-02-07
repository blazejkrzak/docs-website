erc725.js - v0.5.7 / [Exports](modules.md)

# ERC725.js

This library allows for interfacing with ERC725Y compliant contract on an EVM using the [ERC725YJSONSchema](https://github.com/lukso-network/LIPs/blob/master/LSPs/LSP-2-ERC725YJSONSchema.md).

For more information see [Documentation](https://docs.lukso.tech/).

*This package is currently in early stages of development, use only for testing or experimentation purposes*

## Installation

```shell script
$ npm install erc725.js
```

```js
import ERC725 from "erc725.js";
// Or alternately the named export in cases where it
// assists with integration into node modules or commonjs.
import { ERC725 } from "erc725.js";
```

## Example Instantiation

```js
import ERC725 from 'erc725.js';
import Web3 from 'web3';

// Part of LSP3-UniversalProfile Schema
// https://github.com/lukso-network/LIPs/blob/master/LSPs/LSP-3-UniversalProfile.md
const schema = [
  {
    name: "SupportedStandards:ERC725Account",
    key: "0xeafec4d89fa9619884b6b89135626455000000000000000000000000afdeb5d6",
    keyType: "Mapping",
    valueContent: "0xafdeb5d6",
    valueType: "bytes",
  },
  {
    name: "LSP3Profile",
    key: "0x5ef83ad9559033e6e941db7d7c495acdce616347d28e90c7ce47cbfcfcad3bc5",
    keyType: "Singleton",
    valueContent: "JSONURL",
    valueType: "bytes",
  },
  {
    name: "LSP1UniversalReceiverDelegate",
    key: "0x0cfc51aec37c55a4d0b1a65c6255c4bf2fbdf6277f3cc0730c45b828b6db8b47",
    keyType: "Singleton",
    valueContent: "Address",
    valueType: "address",
  },
];

const addresss = "0x0c03fba782b07bcf810deb3b7f0595024a444f4e";
const provider = new Web3.providers.HttpProvider("https://rpc.l14.lukso.network");
const config = {
  ipfsGateway: 'https://ipfs.lukso.network/ipfs/'
}

const erc725 = new ERC725(schema, address, provider, config);
```

## Usage

```js
await erc725.getOwner();
// > '0x28D25E70819140daF65b724158D00c373D1a18ee'

await erc725.getData("SupportedStandards:ERC725Account");
// > '0xafdeb5d6'

await erc725.getData("LSP3Profile");
/* >
{
    url: 'ipfs://QmXybv2LdJWscy1C6yRKUjvnaj6aqKktZX4g4xmz2nyYj2',
    hash: '0xb4f9d72e83bbe7e250ed9ec80332c493b7b3d73e0d72f7b2c7ab01c39216eb1a',
    hashFunction: 'keccak256(utf8)'
}
*/

await erc725.fetchData("LSP3Profile"); // downloads and verifies the linked JSON
/* > 
{
    LSP3Profile: {
        name: 'frozeman',
        description: 'The inventor of ERC725 and ERC20...',
        links: [
            { title: 'Twitter', url: 'https://twitter.com/feindura' },
            { title: 'lukso.network', url: 'https://lukso.network' }
        ],
        ...
    }
}
*/
```

## Testing

```shell script
$ npm test
```
