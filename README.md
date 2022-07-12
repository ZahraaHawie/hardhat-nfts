# Hardhat NFT

## Overview

ERC20 is a technical standard for fungible tokens created using the Ethereum blockchain.

ERC721 is a standard for representing ownership of Non-Fungible Tokens (NFT) that is, where each token is unique.

The main difference between ERC721 & ERC20:

ERC20: Have a simple mapping between an address and how much the address holds.
mapping(address=>uint256) \_balances;

ERC721: ERC721 have unique tokenID, each tokenID has a unique owner.
mapping(uint256 => address) private \_owners; (from tokenId to OwnerAddress)

Each tokenID represents a unique asset, so since these are assets are unique and we want to show what they actually look like, we need to define those attributes of the object.

If it is a piece of art ---> We want a way to define what that art looks like.
If it is a character in a game ---> We need to define the character stats in the NFT

This where MetaData & TokenURI comes in.

If you know Ethereum.. You know that sometimes the gas prices gets pretty high, especially when it comes to storing a lot of space. So the question that comes to our mind, are they storing this images? Are these pieces on chain? Artists & ETH devs used to deploy images into ETH BC but it was so much expensive if you put all this art on chain.

So what they did, is that they put in the standard whats called the tokenURI. This is a universally unique indicator of what that asset or what that token looks like and what the attributes of the token are.

You can use something like a centralized API or IPFS to actually get this tokenURI.

Typical token URI has to return something in this format like this, where it has the name, the image, location, the description.

There is always talks between metadata offchain and metadata onchain.

Absolutely.. storing all your metadata offchain is cheaper and much easier so a lot of people will use something like IPFS (decentralized) but they also can use their own centralized API.

Most of NFT marketplaces can't and won't read off on chain attributes or on chain metadata, because they're so used to looking for the token URI.

Obviously, if you do off chain metadata, you can't do anything really cool or really interesting or have any gains with your NFT's. For example, if you wanted to create an on chain Pokemon game, all your attributes would need to be on chain in order for your Pokemon to interact with each other. Because if it was off chain, then that becomes a lot harder to cryptographically prove.

### Action Plan

If you are looking to render an image as NFT:

1. Add you image to IPFS
2. Add a metadata file pointing to that image file
3. Grab that tokenURI and set as your NFT (Add IPFS URI to your NFT URI)

#### What 3 contracts we will use in the Repo

3 Contracts:

1. Basic Nft using ERC721 standard

2. Random IPFS NFT: It is going to be random at creation time, this is going to give some true scarcity and some true randomness to our NFT. It's hosted on IPFS.
   (uses chainlinkvrf to generate randomness)

3. Dynamic SVG NFT: Hosted 100% on chain, Image gonna change based on some parameters.
   (uses price feeds to be duynamic)

-Pros: The data is on chain!
-Cons: Much more Expensive (We will use smaller images)

We are going to make this actually change based off some data on chain.

If the price of ETH is above X ---> Happy Face
If the price of ETH is below X ---> Frown Face
