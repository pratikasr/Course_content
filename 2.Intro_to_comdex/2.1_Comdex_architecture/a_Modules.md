## Asset

### Overview

The x/asset modules facilitate creating Apps, Assets, Pairs , ExtendedPairVault .

App: An app needs to be added via governance proposal for a specific protocol.All major functionality is driven at app level , providing an ecosystem from multiple apps to co-exist.

Asset: An asset to be used in the chain has to be added via governance proposal.An asset is a common entity and can be used globally by any app .i.e the app can control the use of any in their protocol but cannot control/stop other apps to use the same.

Pair: A pair is an ordered combination of 2 assets where first asset is an asset accepted as deposit by protocol and second asset is the one minted by protocol for the user.

ExtendedPair: ExtendedPair as the name suggests is an extension of a pair to be used by a specific app for vault creation containing key params for each Collateral - Borrow asset pair.

## Auction

### Overview

Auction module holds the key functionality for creating /managing auctions across all apps.  
The auction module has three distinct auction model

1.  Dutch Auction: Collateral auctions for the liquidated vaults take place via this mechanism.Bidders can bid for partial collateral at a price that keeps varying with auction duration starting with a high price and decreasing linearly.
2.  Surplus Auction Excess surplus of an asset (collector\_asset\_id in CollectorLookupTable in Collector module) is auctioned off for an increasing amount of secondary\_asset\_id .After the completed auction duration the excess surplus is sent to bidder with highest amount of secondary\_asset\_id bid.The amount of secondary\_asset\_id bid received is the burned via tokenmint module.
3.  Debt Auction(Reverse Auction): When protocol runs in debt for an asset\_id(collector\_asset\_id in CollectorLookupTable in Collector module) , the debt auction can be triggered to accumulate collector\_asset\_id for which bidders bids against decreasing amount of secondary\_asset\_id.Once auction duration is completed , the bidder with lowest bid for secondary\_asset\_id wins the bid and protocol mints the bid amount of secondary\_asset\_id for the winner.

## Bandoracle

### Overview

Bandoracle module fetches the prices of assets. A band packet is created containing the list of assets symbols for which price is to be fetched. Then the packet is relayed to the band chain (through a relayer), where the request is acknowledged, and the price is validated. Following this, the price is being sent to our chain through the packets using the same channel. After receiving the packets, the prices are mapped to the corresponding assets. The packets are relayed after every 20 blocks; hence prices are updated after every 20 blocks.

## Collector

### Overview

Collector module keeps track of protocol earning via penalty,opening/closing fee etc.Collector keeps track of app earning for each individual asset. Protocol can decide to use the excess fund for rewarding locker depositors or participate in surplus auction and can also participate in debt auction if protocol is deficit of funds for an asset and app.

## ESM

### Overview

Emergency Shutdown is triggered in the case of serious emergencies, such as long-term market irrationality, hacks, or security breaches.Emergency Shutdown stops and gracefully settles the Protocol.Emergency shutdown is triggered by the protocol’s holders by burning their governance token. Once the target amount is reached , users can trigger the ESM via tx command.

## Lend

### Overview

Lend module is used for collateralized lending-borrowing of assets on top of the comdex chain. Any user can deposit their IBC-Assets in a listed cPool and start earning interest on the lent asset. Similarly they can open a borrow position for the lent asset of different IBC-Asset. The module contains transactions to open/close/edit the Lend & Borrow position.  
If the user fails to maintain proper collateralization ratio, then his borrow position will be liquidated. After liquidation, creation of borrow position for the same pair is restricted and then liquidation and auction are handled by the respective modules.

## Liquidation

### Overview

Liquidation module handles the vaults that have been liquidated ( i.e collateralization ratio falls below the minimum collateralization ratio).A locked vault is created once a vault is liquidated and the vault owner will have no access to the vault to perform any action.  
Apps can decide to enable/disable liquidations for their apps through the governance proposal in smart contracts.

## Liquidity

### Overview

The liquidity module is responsible for all the AMM, OrderBook, and Farming Activities. This module implements all the basic features like PairCreation, PoolCreation, AddLiquidity(Deposit), RemoveLiquidity(withdraw), limitOrder, MarketOrder, CancelOrders, Farming, and Unfarming. Multiple applications (apps created using asset module) can leverage the functionality of this module.

## Locker

### Overview

Locker module enables the user to deposit a whitelisted asset for an app and earn rewards on it . The rewards comes from collector module and is distributed to the locker depositor per block basis for a fixed annual rate (locker\_saving\_rate , defined in collector lookup for an app\_id and asset\_id(collector\_asset\_id))

## Market

### Overview

Market module sets the price fetched by Bandoracle module into the market module. After the price being set all the modules fetch the price using this module.

## Tokenmint

### Overview

Tokenmint module lets apps create their own tokens with a genesis supply . An app that wished to create their own governance token can create the same via this module.Only one covernance token can exist for an app whereas multiple non governance token can exist for a app. Tokenmint is solely responsible for minting and burning these tokens.

## Vault

### Overview

The Vault module holds the functionality to create / manage the CDP vaults users .The CDP vault creates an asset by locking up another listed asset as collateral.

The prices of assets are tracked from oracles like Band Protocol.

A liquidation event is triggered when the collateralization ratio of the position falls below the minimum threshold value (Liquidation Ratio) for a cAsset.

Collateralization Ratio = (Value of collaterals locked up)/(Value of borrowed assets)

The Module also offers Stable Mint functionality which is a global common vault for all users where the users can deposit / withdraw collateral for a borrowed asset at 1 : 1 ratio.