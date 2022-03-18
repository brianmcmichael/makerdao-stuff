# Verification of VoteDelegate Contracts

To become a Recognized or Shadow Delegate for MakerDAO, a delegate must create a new VoteDelegate contract.

These contracts are created on-chain, and if done via the VoteDelegateFactory they are not verified by default on Etherscan.

Here we will demosnstrate how to Etherscan verify an unverified [VoteDelegate](https://github.com/makerdao/vote-delegate) contract.

To demonstrate this procedure we'll be verifying the ACREInvest VoteDelegate as our [example](https://etherscan.io/address/0x4d3ac33ab1dd7b0f352b8e590fe8b62c4c39ead5#code).

### Gathering Info

There are two ways to discover the delegate's contract address.

* The first option is to inspect the "Internal Transactions" of the creation tx to discover the contract address.

[img]

* Alternatively, a link to the contract address is provided on the delegate information page.

[img]

Save this address, as well as the address of the deployer, for future reference. In this case, the deployer is registered via ENS as acreinvest.eth. You'll need to translate this back to it's ethereum address via a reverse resolution service like [Etherscan](https://etherscan.io/enslookup), ENS, or it can be found in the URL of the delegate's deployer page on the Maker Portal.

[img]

In this case, `acreinvest.eth` resolves to `0x5b9c98e8a3d9db6cd4b4b4c1f92d0a551d06f00d`, so we'll save that for later.

### Verifying the Contract

On the VoteDelegate page on Etherscan, click the "Contract" tab in the information panel, then the "Verify and Publish" option.

[img]

If the VoteDelegate was deployed by the factory, the settings will be standardized for each contract. Fill out the fields as displayed below.

[img]

* Contract address: the VoteDelegate address (pre-filled)
* Compiler Type: **Solidity (Single File)**
* Compiler Version: **v0.6.12+commit.27d51765**
* Open Source License Type: 13) **GNU Affero General Public License (GNU AGPLv3)**

Click "Continue"

#### Adding the code

The next page requests the source code to be verified and several additional options.

[img]

The Contract Address should already be filled in, as well as the Compiler version, which was provided on the previous page. The VoteDelegate was deployed with Optimizations, so you will need to select "Yes" from the dropdown.

* Contract Address: the VoteDelegate address (pre-filled)
* Compiler: v0.6.12+commit.27d51765 (pre-filled)
* Optimization: **Yes**

You will then need to provide the source code for the contract. This code must match the original code from the deployed  You can obtain this code from another deployed contract, or use the code provided on [IPFS](https://ipfs.io/ipfs/QmbXLZwVUS5Q3fQYdA6JYzu4rFQWZUcDw1nDVKCaKXpMDr)

* Enter the Solidity Contract Code below: \[Copy and Paste the contract code\]

#### Recreating the Constructor Arguments

The trickiest part of verifying a VoteDelegate contract is the creation of the Constructor arguments. You will need to ABI encode three contract addresses into a format that matches the parameters received when the contract was deployed. The simplest way to do this is to use a tool like [abi.hashex.org](https://abi.hashex.org/)

At abi.hashex.org, scroll down to the option to enter your parameters manually. You'll need to click the "Add argument" button three times, and select "Address" as the Argument type. Fill in the boxes as follows:

* Argument 1: **`0x0a3f6849f78076aefadf113f5bed87720274ddc0`**
* Argument 2: **`0xd3a9fe267852281a1e6307a1c37cdfd76d39b133`**
* Argument 3: **\[The Delagate Address (saved above)\]**

Where the first Argument is the ds-chief contract, the second argument is the address of the polling contract, and the third argument is the address that deployed the VoteDelegate contract. When you're done, it should look like the this:

[img]

Copy the data provided in the box and paste this back into the field labelled "Constructor Arguments ABI-encoded (for contracts that were created with constructor parameters)

[img]

You can leave the boxes in "Contract Library Address" and "Misc. Settings" alone.

Fulfil the requirements of the Captcha and click the "Verify and Publish" button.

### Verified!

If the steps have completed successfully, you'll see a screen similar to the following.

[img]

A thumbs-up emoji and the green success message mean your contract has been successfully verified on Etherscan!

If you get a failure message, you'll need to start over and try again, or you can feel free to reach out to a member of the Protocol Engineering team on MakerDAO's Discord chat for assistance.
