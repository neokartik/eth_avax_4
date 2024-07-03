## DegenToken: Your Programmable Reward System

### Introduction

DegenToken is a robust Solidity contract designed to facilitate the creation and management of a reward system within your application or game. This token provides users with an engaging way to earn, redeem, and manage their rewards. With an emphasis on clarity, security, and flexibility, DegenToken empowers developers to build dynamic reward experiences.

### Key Features

#### Minting: Owners can mint Degen tokens to distribute as rewards to users.
#### Burning: Users can burn their Degen tokens to interact with the system (e.g., redeem items).
#### Transferring: Users can easily transfer Degen tokens between each other.
#### Redeeming: Users can exchange their Degen tokens for pre-defined items within the system.
#### Security: The contract leverages the battle-tested OpenZeppelin libraries for verified functionality and robust security measures.
#### Transparency: The contract offers clear visibility into user balances, redeemed items, and token ownership.

### Getting Started

## Deployment: Compile and deploy the DegenToken contract on your chosen blockchain platform (e.g., Ethereum, Binance Smart Chain).
## Integration: Integrate the contract with your frontend application using tools like Web3.js or Ethers.js to interact with its functions.
Contract Breakdown

## Ownership: The Ownable contract from OpenZeppelin ensures only the contract owner can mint Degen tokens.
Token Management: The ERC20, ERC20Burnable, and ERC20Votes contracts from OpenZeppelin provide core functionality for token creation, burning, and potential future voting mechanisms.
Item Management:
itemPrices mapping: Stores prices associated with different items (e.g., itemPrices[1] might hold the price for item 1).
redeemedItems mapping: Tracks items redeemed by each user (address is the key, array of item IDs is the value).
## Events:
## DegenMinted: Emitted when Degen tokens are minted for an account.
ItemRedeemed: Emitted when a user redeems an item using Degen tokens.
## Functions:
 mintDegen(address account, uint256 amount): Allows the owner to mint tokens and credit them to an account.
 getDegenBalance(): Returns the user's current Degen token balance.
 transferTokens(address recipient, uint256 amount): Enables users to transfer Degen tokens to other accounts.
 burnDegen(address account, uint256 amount): Allows users to burn Degen tokens, potentially for interacting with the system.
 exploreItems(): Provides information about available items (names and prices).
 redeemItem(uint256 choice): Users can exchange Degen tokens for items based on their choices.
 getRedeemedItems(address account): Returns a list of item IDs redeemed by a specific user.

## Some Main functions:

function exploreItems() public pure returns (string[] memory) {
        string[] memory items = new string[](3);
        items[0] = "1. Digital Assets - 100 Tokens";
        items[1] = "2. NFTs - 50 Tokens";
        items[2] = "3. FRX Tokens - 20 Tokens";
        return items;
    }

    function redeemItem(uint256 choice) external payable {
        require(choice > 0 && choice <= 3, "Invalid choice"); 
        uint256 itemPrice = itemPrices[choice];
        require(itemPrice > 0, "Invalid choice");

        require(balanceOf(msg.sender) >= itemPrice, "Insufficient balance");

        _transfer(msg.sender, owner(), itemPrice);
        redeemedItems[msg.sender].push(choice);

        emit ItemRedeemed(msg.sender, choice);
    }

## Authors
Kartik 

## License
This project is licensed under the MIT License - see the LICENSE.md file for details
