## Importing methods from the Bank keeper and Asset keeper

In the previous step you have created the `loan` module with `ignite scaffold module` using `--dep bank`. This command created a new module and added the `bank` keeper to the `loan` module, which allows you to add and use bank's keeper methods in loan's keeper methods.

We will also be importing asset module's function for getting assets and pairs.

    type BankKeeper interface {
        SpendableCoins(ctx sdk.Context, addr sdk.AccAddress) sdk.Coins
        SendCoinsFromAccountToModule(ctx sdk.Context, address sdk.AccAddress, name string, coins sdk.Coins) error
        SendCoinsFromModuleToAccount(ctx sdk.Context, name string, address sdk.AccAddress, coins sdk.Coins) error
        GetAllBalances(ctx sdk.Context, addr sdk.AccAddress) sdk.Coins
        SendCoinsFromModuleToModule(
            ctx sdk.Context, senderModule, recipientModule string, amt sdk.Coins,
        ) error
        SendCoins(ctx sdk.Context, fromAddr, toAddr sdk.AccAddress, amt sdk.Coins) error
        GetBalance(ctx sdk.Context, addr sdk.AccAddress, denom string) sdk.Coin
    }

    type AssetKeeper interface {
        GetAsset(ctx sdk.Context, id uint64) (assettypes.Asset, bool)
        GetPair(ctx sdk.Context, id uint64) (assettypes.Pair, bool)
        GetApp(ctx sdk.Context, id uint64) (assettypes.AppData, bool)
    }