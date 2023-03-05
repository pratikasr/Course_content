## Build dApp on comdex

### Introduction

A CDP based dApp on the Comdex chain can be built in go with a series of below mentioned steps . The generic modules of the Comdex chain enable different dapps to co-exist, having their individual specific functionalities.

## Using generic modules

Here are the list of generic modules that all dApps can utilise :

1.  Asset: Manages all asset(s) , pair(s) , extended pair(s) and app(s)
2.  Vault: Base module for managing CDP (Collateralized Debt Position).
3.  Collector: Manages Protocol collection for dApps
4.  Locker: Manages asset deposits for dApps
5.  Auction: Manages auction for liquidated vaults for dApps
6.  Tokenmint: Allows dApps to mint their custom tokens (assets).
7.  Rewards: Manages internal and external rewards for dApps.
8.  Liquidity: Manages the logic for Dex.

## Steps to Launch a dApp

### 1\. Register an application(app)

Asset module is responsible for maintaining different apps on the chain.A proposal must be raised to register an app on the comdex chain which once passed will be used to communicate with all module functionality independently.

Proposal Msg:

comdex tx gov submit-proposal add-app <app\_name> <app\_shortname> <min\_gov\_deposit> <governance\_voting\_period(in sec)>

### 2\. Whitelist an Asset

As a next step , a new asset can be whitelisted via asset module, which once done can be used by any dApp in the Comdex chain.

Proposal Msg:

comdex tx gov submit-proposal add-assets <asset\_name> <denom> <gov\_time\_in\_sec> <decimal> <is\_on\_chain> <asset\_out\_oracle\_price>

### 3\. Create an Asset pair

Asset module can now be leveraged to create an asset pair that can be used by the vault module to create a vault from the pair

Proposal:

comdex tx gov submit-proposal add-pairs \[asset-in\] \[asset-out\]

### 4\. Map an Asset for App

Any dApp that wishes to generate its own token can do so via the tokenmint module . The module can mint several new custom tokens for the dApp out of which at only one asset can be the governance token for the dapp.

Proposal:

comdex tx gov submit-proposal add-asset-in-app --add-asset-mapping-file assetmap.json

assetmap.json

{
 "app\_id" : 
 "asset\_id" :,
 "genesis\_supply" : ,
 "is\_gov\_token" : , 
 "recipient" :  ,
 "title" :  ,
 "description" : ,
 "deposit" :
}

### Mint the Custom Tokens

Once the above proposals are passed , the designated recipient can call the tx command to mint the genesis supply to its respective account (only once).

Tx Msg:

comdex tx tokenmint tokenmint \[app\_id\] \[asset\_id\]

### Governance

All dApps can use a single existing governance contract with their designated governance token assigned through the tokenmint module above.

Below mentioned are the list of proposals that can be raised via contracts for a specific dApp

#### 1\. Create extended pair vault :

Description: Its an asset pair extension comprising specific vault properties like minimum collateralization ratio , fee on vault creation or opening etc.

Msg Struct:

`{"msg\_add\_extended\_pairs\_vault":{
                  "app\_id":,
                  "pair\_id":,
                  "stability\_fee":,
                  "closing\_fee": ,
                  "liquidation\_penalty": ,
                  "draw\_down\_fee": ,
                  "is\_vault\_active":,
                  "debt\_ceiling": ,
                  "debt\_floor":,
                  "is\_stable\_mint\_vault": ,
                  "min\_cr":,
                  "pair\_name" : ,
                  "asset\_out\_oracle\_price":,
                  "asset\_out\_price":,
                  "min\_usd\_value\_left": }
                  }`

#### 2\. Initialise collector data

Description: A collector can contain protocol earning. Each collected asset for an app is tracked by the collector. The proposal signals to add collector asset i.e the accumulated asset for an app with a secondary asset that takes part in a surplus or debt auction is the app is enables for the same.It also has the locker\_saving\_rate that distributes rewards to locker depositors for collector asset in the same app on a per-block basis based on the locker\_saving\_rate defined in the proposal.

Msg Struct:

{"msg\_set\_collector\_lookup\_table":{"app\_id" :,
          "collector\_asset\_id" :,
          "secondary\_asset\_id" :,
          "surplus\_threshold" :,
          "debt\_threshold":,
          "locker\_saving\_rate":,
          "lot\_size":,
          "bid\_factor":,
            "debt\_lot\_size":}}

#### 3\. Whitelist Asset for locker

Description: This proposal signals to set the asset\_id eligible for locker functionalities for the given app\_id .Locker creation, withdrawal or deposit can then be performed.

Msg Struct:

{"msg\_white\_list\_asset\_locker":{"app\_id":,
"asset\_id":}}

#### 4\. Activate App for Locker rewards for Specific Asset/s

Description: This Proposals signals to make all lockers eligible for the given asset\_id and app\_id to receive locker rewards based on the locker\_saving\_rate defined in the collector lookup for the asset\_id and app\_id.

Msg Struct:

{"msg\_whitelist\_app\_id\_locker\_rewards":{"app\_id":,
       "asset\_id":}}

#### 5\. Activate App for vault stability fee accrual (across all vault type)

Description: The proposals triggers the fee accrual for all existing vaults under an app\_id.

Msg Struct:

{"msg\_whitelist\_app\_id\_vault\_interest":{"app\_id":1}}

#### 6\. WhiteList App Id for Liquidation

Description: The proposal sets all vaults eligible for liquidation for a given app\_id.

Msg Struct:

{"msg\_whitelist\_app\_id\_liquidation":{"app\_id":1}}

#### 7\. Set Auction Mapping Eligibility for Asset (Surplus and Debt Auction)

Description: Its an asset pair extension comprising specific vault properties like minimum collateralization ratio , fee on vault creation or opening etc.

Msg Struct:

{"msg\_set\_auction\_mapping\_for\_app":{"app\_id" :,
    "asset\_id" :,
    "is\_surplus\_auction" :,
    "is\_debt\_auction":,
    "asset\_out\_oracle\_price":,
    "asset\_out\_price":
    }}

#### 8\. Update Collector Lookup for an asset

Description: Its an asset pair extension comprising specific vault properties like minimum collateralization ratio , fee on vault creation or opening etc.

Msg Struct:

{"msg\_update\_collector\_lookup\_table":{"app\_id":,
  ,"asset\_id":
    ,"lsr":
    ,"debt\_threshold":
    ,"surplus\_threshold":
    ,"lot\_size": ,
    "debt\_lot\_size":,
    "bid\_factor":}}

#### 9\. Update Extended Pair Vault data

Description: Its an asset pair extension comprising specific vault properties like minimum collateralization ratio , fee on vault creation or opening etc.

Msg Struct:

{"msg\_update\_pairs\_vault":{"app\_id" :,
    "ext\_pair\_id" :,
    "stability\_fee" : ,
    "closing\_fee":"0.0",
    "liquidation\_penalty": ,
    "draw\_down\_fee": ,
    "min\_cr": ,
    "debt\_ceiling": ,
    "debt\_floor": ,
    "min\_usd\_value\_left": }}

#### 10\. Deactivate Asset for locker rewards

Description: Its an asset pair extension comprising specific vault properties like minimum collateralization ratio , fee on vault creation or opening etc.

Msg Struct:

{"msg\_remove\_whitelist\_asset\_locker":{"app\_id":
      ,"asset\_id":}}

#### 11\. Deactivate Stability Fee accruel for all vaults across App

Description: Its an asset pair extension comprising specific vault properties like minimum collateralization ratio , fee on vault creation or opening etc.

Msg Struct:

{"msg\_remove\_whitelist\_app\_id\_vault\_interest":{"app\_id":}}

#### 12\. Remove Whitelist App\_id for liquidation

Description: Its an asset pair extension comprising specific vault properties like minimum collateralization ratio , fee on vault creation or opening etc.

Msg Struct:

{"msg\_remove\_whitelist\_app\_id\_liquidation":{"app\_id":}}

#### 13\. Set/update ESM params

Description: Its an asset pair extension comprising specific vault properties like minimum collateralization ratio , fee on vault creation or opening etc.

Msg Struct:

"msg\_add\_e\_s\_m\_trigger\_params":{"app\_id":,
  "target\_value":{"amount":, "denom":},
      "cool\_off\_period":}}

#### 14\. Set/Update auction params

Description: Its an asset pair extension comprising specific vault properties like minimum collateralization ratio , fee on vault creation or opening etc.

Msg Struct:

 {"msg\_add\_auction\_params":{"app\_id": ,
      "auction\_duration\_seconds":,
      "buffer":,
      "cusp":,
      "step":,
      "price\_function\_type":,
      "surplus\_id":,
      "debt\_id":,
      "dutch\_id":,
      "bid\_duration\_seconds":}}