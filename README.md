# Blockchain Development - Leads Present - NFTs

## STEP 1: Generate images & metadata

1.1. Open a terminal and navigate to the `/backend` folder.

1.2. From the terminal run: 
```
npm install
```

1.3. Notice the `/backend/layers` folder holding the different traits and rarities of the final images.

1.4. Before we can generate the images and their respective metadata, we need to configure some things (this data will appear in the image metadata).

Open the `/backend/src/config.js` file, locate and configure the following variables:
 - `namePrefix` - try to enter a unique name for your collection
 - `description` - add a short description for your collection
 - `layerConfigurations.growEditionSizeTo` - the number of images and metadata to generate (keep this below 20 for speed considerations).
 - `extraMetadata.external_url` - link to an external website (optional)

1.5. Generate the collection images and metadata by executing the following command: 
```
npm run generate
```

1.6. Notice that in the `/backend/build` folder two new folders were created:
 - `images` - containing the images generated
 - `json` - containing the coresponding images metadata

1.7. Because we will launch our NFT's with a grand reveal, we will also have to create some generic image and metadata to keep the actual images secret until de reveal.

The generic image has already been uploaded for you [see it here](https://ipfs.io/ipfs/bafkreiev3mkvxoscza3c6ss7ilwqu3hf2vvz47o3hw3chqdyfmcyp4yo34).

Check the following settings from `/backend/src/config.js` if you wish to modify the generic data:
 - `GENERIC_TITLE` - the name of the collection (if you want it to differ from the actual contract name)
 - `GENERIC_DESCRIPTION` - a generic description for your collection
 - `GENERIC_IMAGE` - a generic image which will be displayed for all your items

When you are happy with the settings, we can create the generic metadata by executing the following command:

```
npm run create_generic
```

1.8. Notice that in the `/backend/build` folder a new folder was created:
 - `genericJson` - containing the generic metadata (without traits)


## STEP 2: Upload images and metadata to IPFS (descentralized storage)
2.1. First of all open the `.env` file and fill in your NFTPort API key.

2.2. Now lets upload the images to IPFS. To do this execute:
```
npm run upload_files
```

Notice that the metadata files (`file_url` & `image fields`) in the `backend/build/json` folder have been updated with the actual IPFS image address.

2.3. Now lets upload the metadata (real and generic) to IPFS. To do this execute:
```
npm run upload_metadata
```

2.4. Notice that in the `/backend/build` folder two new folders were created:
 - `ipfsMetas` - containing the actual metadata information
 - `ipfsMetasGeneric` - containing the generic metadata information


## STEP 3: Deploy de contract to the blockchain
3.1. First of all open the `/backend/src/config.js` file and provide values for the following fields:
 - `CONTRACT_NAME` - collection name (as shown on OpenSea)
 - `CONTRACT_SYMBOL` - a short acronim for your collection
 - `MINT_TO_ADDRESS` - enter your metamask wallet address
 - `ROYALTY_ADDRESS` - enter your metamask wallet address

**Important**: Double check these values for they cannot be updated later on!

3.2. Now we are ready to deploy the contract to the blockchain.
To do this execute the following command:
```
npm run deploy_contract
```

Notice that in the `/backend/build` a new folder was created:
 - `contract` - containing information about the deployment

Your contact is now being deployed on the blockchain. This can take some time.

3.3. After contact deployment is complete we can get our contract details using the following command:
```
npm run get_contract
```
If this operation succeeds you will see a new file in your `/backend/build/contact` folder called `_contract.json`.

**Important**: Open this file and locate the `contact_address` variable. Copy this value into the `/backend/src/config.js` and assign it to the `CONTRACT_ADDRESS` variable.


## STEP 4: Mint a few of your items and reveal them
4.1. In order to mint (create) one or more NFTs we have to run the following command:
```
npm run mint --start=1 --end=3
```
Notice that in the `/backend/build` a new folder was created:
 - `minted` - containing information about the minted NFTs

4.2. Now lets check to see how our collection looks on OpenSea.

- Go to [https://testnets.opensea.io/](https://testnets.opensea.io/) and connect connect your Metamask wallet (allow to change network to `Goerli test network`).
- Click on your profile icon (cyan circle) and go to `My Collections`.

Here you should find your minted items with their generic image.

4.3. In order to reveal the actual NFTs we have to run the following command:
```
npm run reveal --start=1 --end=3
```
Notice that in the `/backend/build` a new folder was created:
 - `revealed` - containing information about the revealed NFTs

 4.4. Go back to OpenSea, select one of your items and click on the `Refresh metadata` button. 

 After waiting a bit, you can realod the page. The item should be revealed now with the actual image.

 4.5. Check how your contract looks via the blockchain explorer:
 [https://goerli.etherscan.io/](https://goerli.etherscan.io/)


 #### 🎉🎉🎉 **CONGRADULATIONS!!! YOU JUST LAUNCHED YOUR FIRST NFT COLLECTION!** 🎉🎉🎉