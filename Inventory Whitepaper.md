# Inventory Whitepaper

This white paper for the NFT Inventory system is a draft and is currently in progress. 
# Abstract

Web3 gaming presents a paradigm shift in how players interact with in-game assets. This whitepaper delves into the current state of web3 gaming inventories and proposes a standardized approach to manage and use these assets.

The proposed Inventory system is a smart contract that allows game designers to define inventories for the characters in their web3 games. This allows players to equip items to their character NFTs and rewards and game items to be given directly to a character NFT, rather than to a player wallet. Unlike previous protocols that have allowed an NFT to own other tokens, the Inventory system specifies the purpose each token is being used for in the contract by allowing game designers to define specific inventory slots. As a result, the Inventory contract provides fully on-chain information about the game state, including what items a character has equipped and how those items can interact with the game.

# Motivation
## Why is it important to equip items to character NFTs, rather than sending them to player wallets?

Imagine that you are creating an on-chain fantasy RPG featuring a dwarf named Borri Barrowsbane.  

![borri_barrowsbane](https://static.greatwyrm.xyz/act1/characters/borri_barrowsbane.png) 

As Borri explores the gameworld, he finds some leather, iron, and wood and uses them to craft a battle axe. He uses the battle axe to slay a wyvern. 

Killing the wyvern earns Borri three experience points (XP), which unlocks new game content and allows him to level up his skills. 

The crafting resources (leather, iron, wood), the battle axe, and the XP can all be represented as tokens in the game. 

Borri burns the resources tokens to mint an item token (the axe) and collects three reward tokens (the XP). 

But where do these tokens go, and how do they interact with the Borri NFT, or with other items in the game?

### Old solution: Player wallets

Web3 games often place a lot of emphasis on player accounts. Character NFTs (ERC-721 tokens), items, XP, and rewards (ERC-721 or ERC-1155 tokens) can be sent straight to the player’s wallet. From there, the player can use them in the game, sell them, or trade them.

There are a couple of problems with this approach. For one thing, it blurs the line between a character’s progress and the player’s progress. If the three XP that Borri earned above go to the player’s wallet—i.e., if they aren’t directly associated with the Borri NFT—several potential problems arise:

1. Borri’s game progress doesn’t impact the value of the Borri NFT, because character NFTs and XP tokens must be traded separately.

⠀
2. A player could create a number of characters, earn a few XP with each through easy feats, and transfer them all to a single character NFT to level up that character quickly without having to face any difficult challenges.

⠀
3. A game that relies on XP or a similar counter to unlock new character abilities and storylines has no way to distinguish between several characters owned by the same player. This makes it difficult if players want to have more than one character playing the game. Any XP that any character accrues goes into a common wallet, which provides no data about how they can be used, and by whom. The same holds for weapons, unique quest items, influence points, guild badges, etc. All character NFTs associated with the relevant player wallet will have equal access to these items, making the items useless as a way to track any particular character’s progress through the game. 

⠀
Associating in-game items with player wallets also creates situations in which it is easy to circumvent the logic of the game’s narrative. For example:

4. Imagine that Borri crafts his battle axe while exploring the Eastern Mountains. The battle axe goes to the player’s wallet. The player then decides to give the battle axe to another character who is exploring the Great Western Forest, a character who has never crossed paths with Borri in the game. The second character uses the buff provided by the battle axe to fight a werebear and level up. In this case, the weapon, and the advantage that it provides, are transferred from one character to another without explanation of how this could happen in game. Borri doesn’t have to sell the spear at a market, or trade it to the other character directly, for it to change hands.

⠀
While game developers may come up with ways to work around some of these difficulties, the bottom line is that assigning in-game assets to player wallets rather than to specific character NFTs leads to a dearth of data about how and by which characters the assets should be used in-game and makes it difficult to use game progress or leveling to raise the value of an NFT. 

### New solution: NFT Inventory

Using the Inventory system to instead assign the XP and battle axe tokens directly to Borri solves the problems outlined above. 

1. By using the Inventory system to give the XP directly to the Borri NFT, Borri can be traded or sold with his XP equipped. This means that his game progress adds to the value of the character, as his leveling, and the skills and abilities it unlocks, transfer with him to the new owner. 

⠀
2. In fact, the game designer can choose to make certain items, such as XP, persistent, meaning that the player cannot unequip them. Making XP persistent ensures that it cannot be transferred from one character to another. This allows XP to function as a permanent record of a character’s progress and leveling. It also prevents the leveling shortcut described above, in which a player combines the XP from a number of low-level characters to create a single high-level character. 

⠀
3. Equipping items to a specific character’s NFT-based inventory makes it clear which character owns and is using which item and how many XP (or other points and achievements) each character has accrued. 

⠀
4. Equipping specific items to specific characters provides data and restrictions that make it easier to align gameplay with the logic of the game world, as well. If the battle axe is equipped to Borri, and Borri is in the Eastern Mountains, it is now easy to limit the group of characters that can use or trade for the battle axe to characters in the same area of the map. Similarly, if Borri’s friend in the Great Western Forest finds a rare mushroom there, she must travel to the nearest apothecary to sell it. The player can’t simply have a third character, who happens to already be in an apothecary’s shop, sell the item. The XP she earns for foraging, and the money she earns from the sale, will go to her, and Borri won’t have access to them. Once more, the availability of information about which character possesses which items allows the game designers to restrict potential uses of the items to those which fit the logic of the narrative. Additionally, it makes XP, quest items, and other tokens useful as a way to track a specific character’s progress and achievements. 

Note: In this section, we are discussing a very obvious use case for the Inventory System: tracking the items in a characters’ possession. For examples of other uses, see ~[below](https://docs.google.com/document/d/1hIE_7ZhMDHHJCkfSznUfwGPRkaexTD-KfZlElaRmwtA/edit%23heading=h.p65yffk7dfd1)~.


## Background: Hasn’t this been done before?

The Inventory System is not the only protocol in existence that allows an NFT to own another token. Most notably, token bound accounts, as described in ~[EIP-6551](https://eips.ethereum.org/EIPS/eip-6551)~, “allow NFTs to own assets and interact with applications.” By assigning an Ethereum account to an NFT, EIP-6551 allows that NFT to act as a wallet or folder that contains other on-chain assets.  Token bound accounts have proven themselves to be useful in a great variety of scenarios. However, precisely because they are designed for general use, they are not an ideal tool from the perspective of game design. 

The Inventory System, created specifically for web3 games, is better suited to game development for two key reasons:

1. Tokenbound accounts only specify ownership. The Inventory System specifies how a particular item is being used in the game contract. This makes the Inventory System a source of fully on-chain information about the game state in a way that token bound accounts cannot match. 
2. Anyone in the world can send tokens to an NFT’s tokenbound account. This means that you could send rival players unwanted items, including inferior versions of tools or heavy items in games with an inventory weight limit. You could also simply spam garbage tokens to an NFT’s token bound account. If the way that a game picks up token ownership for an NFT from its tokenbound account is not bounded, this could overwhelm the game's crawling infrastructure and would affect player experience.The Inventory System prevents these vulnerabilities by giving players exclusive control over equipping and unequipping items to/from a character’s inventory.

⠀
### Why should an Inventory contract specify more than ownership?

This chart compares the benefits that the Inventory System and token bound accounts offer to game designers. It is clear from the comparison that, while both options are preferable to sending in-game items to a player’s wallet, the Inventory System provides designers and players with more control, more on-chain information, and more options for customizing the inventory to suit the needs of the game.  	         **Benefits for Game Design: NFT Inventory vs Token Bound Accounts**
| **Lets users...**                                            | **Inventory** | **Token Bound** |
|--------------------------------------------------------------|:-------------:|:---------------:|
| Have characters (versus players) own the tokens representing their items, ranks, etc. | ✔             | ✔               |
| Sell items along with character NFTs                         | ✔             | ✔               |
| Add value to their NFTs based on in-game achievements        | ✔             | ✔               |
| Designate ownership                                          | ✔             | ✔               |
| Designate inventory slots                                    | ✔             |                 |
| Designate which items can be equipped in a slot              | ✔             |                 |
| Equip/unequip items                                          | ✔             |                 |
| Have sole control over equipping items to their characters   | ✔             |                 |
| Designate slots as persistent (permanent effects)            | ✔             |                 |
| Create fully on-chain metadata                               | ✔             |                 |
---

# Design (EIP)
This section explains the features of the Inventory contract in the format of an EIP. (Currently, these are section descriptions from ~[https://eips.ethereum.org/EIPS/eip-1](https://eips.ethereum.org/EIPS/eip-1)~ waiting to be replaced with our text.)

## Abstract
The NFT Inventory System is a smart contract that game designers can use to define inventories for the characters (ERC721 tokens) in their web3 games.  When an item is equipped to an NFT, ownership of that item is transferred to the Inventory contract.

Administrators can define the inventory slots that an NFT collection (ERC721 contract) admits. They can specify which items (ERC20 tokens, ERC721 tokens, ERC1155 tokens) are equippable in each slot and whether or not a slot is persistent (i.e., whether or not the NFT owners may unequip items from that slot). NFT owners can equip and unequip valid items to/from non-persistent (‘unequippable’) inventory slots. 

## Motivation
(For now, see the problem section above.)

~[ERC-6551](https://eips.ethereum.org/EIPS/eip-6551%23motivation)~ includes this in its motivation section: 
>*The pattern defined in this proposal does not require any changes to existing NFT smart contracts. It is also compatible out of the box with nearly all existing infrastructure that supports Ethereum accounts, from on-chain protocols to off-chain indexers. Token bound accounts are compatible with every existing on-chain asset standard, and can be extended to support new asset standards created in the future.*

It also includes notable use cases, which in our whitepaper might fit better elsewhere.

## Specification
> The technical specification should describe the syntax and semantics of any new feature. The specification should be detailed enough to allow competing, interoperable implementations for any of the current Ethereum platforms (besu, erigon, ethereumjs, go-ethereum, nethermind, or others).

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “NOT RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in RFC 2119 and RFC 8174.

The Inventory interface contract (IInventory.sol) is written in Solidity, as are all of the code blocks in the “Specification” section of this document. 

In the “Reference Implementations” section below, we provide two reference implementations for this contract: a standalone implementation and an EIP-2535-compatible (Diamond proxy facet) implementation. 

The following are the key features of the Inventory contract:

### Inventory Storage
Here are the structures of an inventory slot and an equipped item as defined in the Inventory contract (IInventory.sol).

#### Inventory slot
 `Slot` represents a single slot in an inventory. 

```
struct Slot {
    string SlotURI;
    bool SlotIsPersistent;
}
```

#### Equipped item
`EquippedItem` represents an item equipped in a specific inventory slot for a specific ERC721 token.

```
struct EquippedItem {
    uint256 ItemType;
    address ItemAddress;
    uint256 ItemTokenId;
    uint256 Amount;
}
```


### Functions

The Inventory contract (IInventory.sol) defines the following 13* functions. Four are admin-only, meaning that only the contract administrator (the game developer) can use them. The rest are open to all users (and thus to all players of the game).

#### Admin-only functions
These functions let the contract administrator (the game developer) designate the inventory slots for a particular inventory contract. The admin can create slots, designate persistent slots (slots from which players may not unequip items, such as slots for rank and leveling tokens like XP), and specify which items may be equipped to each slot. 

**To create a new inventory slot,** use the `createSlot` function and specify the following parameters: 

* `persistent` A boolean indicating if the slot is unequippable (true) or not (false). (If a slot is persistent, it means that players cannot unequip items from that slot.)
* `slotURI` A string representing the slot URI.

```
function createSlot(
        bool persistent,
        string memory slotURI
    ) external returns (uint256);

```


**To set the URI of a new inventory slot,** use the function `setSlotURI` Specify the following parameters:

* `newSlotURI` A string representing the URI of new slot.
* `slotID` 

```
function setSlotURI(string memory newSlotURI, uint256 slotId) external;
```


**To designate an inventory slot as persistent** or not persistent, use the function `setSlotPersistent`. (If a slot is persistent, it means that players cannot unequip items from that slot.)

```
 function setSlotPersistent(uint256 slotId, bool persistent) external;
```


To designate that an item may be equipped to a particular inventory slot, use the function `markItemAsEquippableInSlot` and specify the slot ID of the slot it may be equipped in, the item type, the item address, the item’s Pool ID, and the maximum number of that item that can be equipped in the indicated slot. Specify the following parameters:

* `slot` The slot ID (?)
* `itemType` The type of item (ERC20, ERC721, or ERC1155)
* `itemAddress` The item’s contract address
* `itemPoolId` The item pool ID.
* `maxAmount` The maximum number of that item that can be equipped in the designated slot.

```
function markItemAsEquippableInSlot(
        uint256 slot,
        uint256 itemType,
        address itemAddress,
        uint256 itemPoolId,
        uint256 maxAmount
    ) external;
```



#### Other functions
These functions are available to all users of the contract (players as well as game designers).

##### Interacting with a character’s inventory

**View the contract address of a character NFT:** ` subject` lets users view the ERC721 contract address for an NFT for which an inventory has been created. (Note: This function will be removed to allow for multi-tenant support for multiple ERC721 contracts on a single inventory.)
```
function subject() external view returns (address) {
        return contractERC721Address;
```


**To see how many slots there are in a particular inventory,** use the function `numSlots` . (Please help with the wording here, with regard to multi-tenant functionality. How should we talk about the inventory created for a specific ERC721 versus the ‘version’ of the inventory contract used by multiple ERC721s in the same game?)

```
function numSlots() external view returns (uint256);
```

**To see all of the items in a character’s inventory,** use the function `getAllEquippedItems`. Specify the ID of the character’s ERC721 contract.

```
function getAllEquippedItems(
        uint256 subjectTokenId
    ) external view returns (LibInventory.EquippedItem[] memory items);
```


##### Interacting with a particular inventory slot

**To view information about a particular inventory slot,** including the slot URI and whether or not the slot is persistent, use `getSlotByID` . Specify the slot ID for the inventory slot in question.

```
function getSlotById(
        uint256 slotId
    ) external view returns (LibInventory.Slot memory slots);

```


**To find the slot URI for a particular inventory slot,** use the function `getSlotURI`  and specify the slot ID.

```
function getSlotURI(uint256 slotId) external view returns (string memory);
```


**To see whether or not a particular inventory slot is persistent,** use the function `slotIsPersistent`  and specify the slot ID. (Persistent means that players cannot unequip items from that slot.)

```
 function slotIsPersistent(uint256 slotId) external view returns (bool);
```


**To discover the maximum number of items** of a given type that can be equipped in a particular slot in a character’s inventory, use the function `maxAmountOfItemInSlot`  and specify the following parameters: 

* `slot` The slot ID (?)
* `itemType` The type of item (ERC20, ERC721, or ERC1155)
* `itemAddress` The item’s contract address
* `itemPoolId` The item pool ID.
* `maxAmount` The maximum number of that item that can be equipped in the designated slot.

```
function maxAmountOfItemInSlot(
        uint256 slot,
        uint256 itemType,
        address itemAddress,
        uint256 itemPoolId
    ) external view returns (uint256);
```


##### Equipping and unequipping items

**Equip an item** to a particular slot in a character’s inventory with the `equip` function.  You will need to specify:

* `subjectTokenId` The token ID of the subject (character) NFT.
* `slot`The slot ID.
* `itemType` The type of item (ERC20, ERC721, or ERC1155).
* `itemAddress` The item’s contract address.
* `itemTokenId` The item's token ID.
* `amount` How many of the item to equip (relevant for ERC20 and ERC1155 tokens).

```
function equip(
        uint256 subjectTokenId,
        uint256 slot,
        uint256 itemType,
        address itemAddress,
        uint256 itemTokenId,
        uint256 amount
    ) external;
```


**To show the item that is currently quipped in a particular slot** in a character’s inventory, use the function `getEquippedItem`. Specify the token ID of the subject (character) NFT and the slot ID. 

```
function getEquippedItem(
        uint256 subjectTokenId,
        uint256 slot
    ) external view returns (LibInventory.EquippedItem memory item);
```


**Unequip (remove) items from a particular inventory slot** using the `_unequip`  function. Users can unequip a single item, multiple items, or all items from the slot in question, depending on the value they specify for the Boolean variable unequipAll. If unequipAll has the value >0, users will be prompted to specify how many items they would like to unequip.

```
function _unequip(uint256 subjectTokenId, uint256 slot, bool unequipAll, uint256 amount) public nonReentrant {
        require(!unequipAll || amount == 0, "Inventory._unequip: Set amount to 0 if you are unequipping all instances of the item in that slot");

        require(
            unequipAll || amount > 0,
            "Inventory._unequip: Since you are not unequipping all instances of the item in that slot, you must specify how many instances you want to unequip"
        );

        require(slotData[slot].SlotIsPersistent, "Inventory._unequip: That slot is not persistent");

  LibInventory.EquippedItem storage existingItem = equippedItems[contractERC721Address][subjectTokenId][slot];

        if (unequipAll) {
            amount = existingItem.Amount;
        }

        require(amount <= existingItem.Amount, "Inventory._unequip: Attempting to unequip too many items from the slot");

        if (existingItem.ItemType == 20) {
            IERC20 erc20Contract = IERC20(existingItem.ItemAddress);
            bool transferSuccess = erc20Contract.transfer(_msgSender(), amount);
            require(transferSuccess, "Inventory._unequip: Error unequipping ERC20 item - transfer was unsuccessful");
        } else if (existingItem.ItemType == 721 && amount > 0) {
            IERC721 erc721Contract = IERC721(existingItem.ItemAddress);
            erc721Contract.safeTransferFrom(address(this), _msgSender(), existingItem.ItemTokenId);
        } else if (existingItem.ItemType == 1155) {
            IERC1155 erc1155Contract = IERC1155(existingItem.ItemAddress);
            erc1155Contract.safeTransferFrom(address(this), _msgSender(), existingItem.ItemTokenId, amount, "");
        }

        emit ItemUnequipped(subjectTokenId, slot, existingItem.ItemType, existingItem.ItemAddress, existingItem.ItemTokenId, amount, _msgSender());

        existingItem.Amount -= amount;
        if (existingItem.Amount == 0) {
            delete equippedItems[contractERC721Address][subjectTokenId][slot];
        }
    }

```
      

You can also **equip multiple items to a character’s inventory at once** using the `equipBatch` function. Specify the token ID of the subject (character) token, the IDs of the slots to which items are being equipped (you must provide a slot ID for each item), and type, address, token ID, and amount for each item being equipped. 

```
function equipBatch(uint256 subjectTokenId, uint256[] memory slots, LibInventory.EquippedItem[] memory items) external nonReentrant {
        require(items.length > 0, "Inventory.batchEquip: Must equip at least one item");
        require(slots.length == items.length, "Inventory.batchEquip: Must provide a slot for each item");

        for (uint256 i = 0; i < items.length; i++) {
            equip(subjectTokenId, slots[i], items[i].ItemType, items[i].ItemAddress, items[i].ItemTokenId, items[i].Amount);
```


## Rationale
>The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work, e.g. how the feature is supported in other languages. The rationale should discuss important objections or concerns raised during discussion around the EIP.

## Backwards Compatibility (optional)
>All EIPs that introduce backwards incompatibilities must include a section describing these incompatibilities and their consequences. The EIP must explain how the author proposes to deal with these incompatibilities. This section may be omitted if the proposal does not introduce any backwards incompatibilities, but this section must be included if backward incompatibilities exist.

This is what the ~[ERC-6551](https://eips.ethereum.org/EIPS/eip-6551%23specification)~ Backwards Compatibility section looks like: 

>*This proposal seeks to be maximally backwards compatible with existing non-fungible token contracts. As such, it does not extend the ERC-721 standard.*

>*Additionally, this proposal does not require the registry to perform an ERC-165 interface check for ERC-721 compatibility prior to account creation. This maximizes compatibility with non-fungible token contracts that pre-date the ERC-721 standard (such as CryptoKitties) or only implement a subset of the ERC-721 interface (such as ENS NameWrapper names). It also allows the system described in this proposal to be used with semi-fungible or fungible tokens, although these use cases are outside the scope of the proposal.*

>*Smart contract authors may optionally choose to enforce interface detection for ERC-721 in their account implementations.*
 
## Test Cases (optional)
>Test cases for an implementation are mandatory for EIPs that are affecting consensus changes. Tests should either be inlined in the EIP as data (such as input/expected output pairs, or included in ../assets/eip-###/<filename>. This section may be omitted for non-Core proposals.

## Reference Implementations
* Standalone version
* EIP-2535-compatible version

## Security Considerations
>All EIPs must contain a section that discusses the security implications/considerations relevant to the proposed change. Include information that might be important for security discussions, surfaces risks and can be used throughout the life-cycle of the proposal. E.g. include security-relevant design decisions, concerns, important discussions, implementation-specific guidance and pitfalls, an outline of threats and risks and how they are being addressed. EIP submissions missing the “Security Considerations” section will be rejected. An EIP cannot proceed to status “Final” without a Security Considerations discussion deemed sufficient by the reviewers.

Should this go here? (From ~[github](https://github.com/lootledger/inventory/blob/main/contracts/libraries/LibInventory.sol)~):

> NOTE: We have added the subject contract address as the first mapping key as a defense against future modifications which may allow administrators to modify the subject contract address. If such a modification were made, it could make it possible for a bad actor administrator to change the address of the subject token to the address to an ERC721 contract they control and drain all items from every subject token's inventory. If this contract is deployed as a Diamond proxy, the owner of the Diamond can pretty much do whatever they want in any case, but adding the subject contract address as a key protects users of non-Diamond deployments even under small variants of the current implementation. It also offers *some* protection to users of Diamond deployments of the Inventory.

* Should we discuss only allowing the NFT owners to equip items in this section?
* We could talk about where items go when they are unequipped.
* What else should this section cover?

## Copyright Waiver
Copyright and related rights waived via ~[CC0](https://github.com/lootledger/inventory/blob/4d3c9619c6d521b999b3af5e6d1b4135d346a2c7/LICENSE)~.

--- 
# Examples of Use
Crypto Guilds: Community engagement
Bag: Creating a catch-all slot
Lands
# Conclusion 
# Calls to action
# References
~[https://www.notion.so/Inventory-User-Guide-5e4b62fa0d6748deb7d3ef77d4aeda21](https://www.notion.so/Inventory-User-Guide-5e4b62fa0d6748deb7d3ef77d4aeda21)~
~[Inventory Working Group](https://docs.google.com/document/d/14lbSZRSya7QL9B2Pie_bQXFMjb5kFF-op8dPwUrMTxw/edit)~
~[An Inventory system for web3 games](https://docs.google.com/document/d/1Oa9I9b7t46_ngYp-Pady5XKEDW8M2NE9rI0GBRACZBI/edit%23heading=h.w09oin6cubga)~
~[NFT Inventory](https://docs.google.com/document/d/1H-idKMa5hwTVb8suCszdVR4J-39xLiAPDQJqWqFCkLk/edit)~
