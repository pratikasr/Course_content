## Create a loan Request

The `Request` keeper method that will be called whenever a user requests a loan. `Request` creates a new loan with the provided data, sends the collateral from the borrower's account to a module account, and saves the loan to the blockchain's store.

    func (k Keeper) Request(ctx sdk.Context, appID, pairID uint64, owner string, amtIn, amtOut, fee sdk.Int, duration int64) error {
        loanID := k.GetLoanID(ctx)
        loan := types.Loan{
            Id:           loanID + 1,
            AppId:        appID,
            PairID:       pairID,
            Owner:        owner,
            AmountIn:     amtIn,
            AmountOut:    amtOut,
            Fee:          fee,
            CreatedAt:    ctx.BlockTime(),
            DurationDays: duration,
            Lender:       "",
            State:        "requested",
        }
        addr, err := sdk.AccAddressFromBech32(owner)
        if err != nil {
            return err
        }
        pair, found := k.Asset.GetPair(ctx, pairID)
        if !found {
            return assettypes.ErrorPairDoesNotExist
        }
        assetIn, found := k.Asset.GetAsset(ctx, pair.AssetIn)
        if !found {
            return assettypes.ErrorAssetDoesNotExist
        }

        err = k.bankKeeper.SendCoinsFromAccountToModule(ctx, addr, types.ModuleName, sdk.NewCoins(sdk.NewCoin(assetIn.Denom, amtIn.Add(fee))))
        if err != nil {
            return err
        }
        k.SetLoanID(ctx, loan.Id)
        k.SetLoan(ctx, loan)
        return nil
    }

## Basic message validation

When a loan is created, a certain message input validation is required. You want to throw error messages in case the end user tries impossible inputs.

    func (msg *MsgCreateRequest) ValidateBasic() error {
        _, err := sdk.AccAddressFromBech32(msg.GetFrom())
        if err != nil {
            return err
        }
        if msg.AppId == 0 {
            return fmt.Errorf("app id should not be 0: %d ", msg.AppId)
        }
        if msg.AmountIn.IsNegative() || msg.AmountIn.IsZero() {
            return fmt.Errorf("invalid coin amount: %s < 0", msg.AmountIn)
        }
        if msg.AmountOut.IsNegative() || msg.AmountOut.IsZero() {
            return fmt.Errorf("invalid coin amount: %s < 0", msg.AmountOut)
        }
        if msg.PairId == 0 {
            return fmt.Errorf("pair id should not be 0: %d ", msg.PairId)
        }

        return nil
    }