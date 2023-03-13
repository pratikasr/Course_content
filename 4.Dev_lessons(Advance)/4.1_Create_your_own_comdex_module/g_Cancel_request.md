## Cancel a Loan

If you have created a loan as a borrower but have changed your mind and no longer want to proceed with it, you can choose to cancel the loan. However, this can only be done if the loan's current status is marked as "requested."

Once you cancel the loan, the collateral tokens that were being held as security for the loan will be transferred back to your account from the module account. As a result, you will regain possession of the collateral tokens you had initially provided as security for the loan.


    func (k Keeper) Cancel(ctx sdk.Context, loanID uint64) error {
        loan, found := k.GetLoan(ctx, loanID)
        if !found {
            return sdkerrors.Wrapf(sdkerrors.ErrKeyNotFound, "key %d doesn't exist for loanID", loanID)
        }
        if loan.State != "requested" {
            return sdkerrors.Wrapf(types.ErrWrongLoanState, "%v", loan.State)
        }

        borrowerAddr, err := sdk.AccAddressFromBech32(loan.Owner)
        if err != nil {
            return err
        }

        pair, found := k.Asset.GetPair(ctx, loan.PairID)
        if !found {
            return assettypes.ErrorPairDoesNotExist
        }

        assetIn, found := k.Asset.GetAsset(ctx, pair.AssetIn)
        if !found {
            return assettypes.ErrorAssetDoesNotExist
        }

        err = k.bankKeeper.SendCoinsFromModuleToAccount(ctx, types.ModuleName, borrowerAddr, sdk.NewCoins(sdk.NewCoin(assetIn.Denom, loan.AmountIn.Add(loan.Fee))))
        if err != nil {
            return err
        }
        k.DeleteLoan(ctx, loanID)

        return nil
    }
