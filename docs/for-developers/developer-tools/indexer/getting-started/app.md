---
sidebar_position: 2
--- 

# DApp

## USE IT IN YOUR DAPP

Here we'll see the simplest example to request indexer data from a node application.
We'll use the simple request used in the playground section.

### First of all, in a new folder, create 2 files:

``` json title="package.json" showLineNumbers
{
  "name": "indexer-request-sample",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "type": "module",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "graphql-request": "^5.0.0"
  }
}
```


```javascript title="index.js" showLineNumbers
import { request } from "graphql-request"

const getLastListedNFTs = async () => {
	const gqlQuery = `{
	  nftEntities(
		first: 10, 
		offset: 0, 
		orderBy: TIMESTAMP_LISTED_DESC
	  ) {
		totalCount
		nodes {
			nftId
			owner
			creator
			collectionId
			offchainData
    	}
	  }
	}`
	const response = await request("https://indexer-alphanet.ternoa.dev/", gqlQuery)
	if (response.nftEntities){
		console.log("Total count", response.nftEntities.totalCount)
		response.nftEntities.nodes.forEach(x => console.log(x))
	}
}

getLastListedNFTs()
```

Now open a terminal in this folder and run the following commands:
```bash
npm install
node index.js
```