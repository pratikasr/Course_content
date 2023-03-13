## Repay a loan

The RepayLoan function is in charge of managing the repayment of a loan by transferring the borrowed funds, as well as any agreed-upon fees, from the borrower to the lender. Additionally, the collateral that was provided as part of the loan agreement will be released from the escrow account and returned to the borrower.

There are certain conditions that must be met before the RepayLoan function can be called. Firstly, the borrower of the loan must sign the transaction, ensuring that only the borrower can initiate the repayment process. Secondly, the loan must be in an approved status, indicating that it has been approved and is ready for repayment.

To implement the RepayLoan function, we must first ensure that these conditions have been met before proceeding with the repayment process. Once the necessary checks have been performed, the function can proceed with transferring the funds and releasing the collateral from the escrow account.

    func (k Keeper) Repay(ctx sdk.Context, loanID uint64) error {
        loan, found := k.GetLoan(ctx, loanID)
        if !found {
            return sdkerrors.Wrapf(sdkerrors.ErrKeyNotFound, "key %d doesn't exist for loanID", loanID)
        }
        if loan.State != "approved" {
            return sdkerrors.Wrapf(types.ErrWrongLoanState, "%v", loan.State)
        }

        pair, found := k.Asset.GetPair(ctx, loan.PairID)
        if !found {
            return assettypes.ErrorPairDoesNotExist
        }

        assetIn, found := k.Asset.GetAsset(ctx, pair.AssetIn)
        if !found {
            return assettypes.ErrorAssetDoesNotExist
        }

        assetOut, found := k.Asset.GetAsset(ctx, pair.AssetOut)
        if !found {
            return assettypes.ErrorAssetDoesNotExist
        }

        lenderAddr, err := sdk.AccAddressFromBech32(loan.Lender)
        if err != nil {
            return err
        }

        borrowerAddr, err := sdk.AccAddressFromBech32(loan.Owner)
        if err != nil {
            return err
        }

        err = k.bankKeeper.SendCoinsFromAccountToModule(ctx, borrowerAddr, types.ModuleName, sdk.NewCoins(sdk.NewCoin(assetOut.Denom, loan.AmountOut)))
        if err != nil {
            return err
        }

        err = k.bankKeeper.SendCoinsFromModuleToAccount(ctx, types.ModuleName, lenderAddr, sdk.NewCoins(sdk.NewCoin(assetOut.Denom, loan.AmountOut), sdk.NewCoin(assetIn.Denom, loan.Fee)))
        if err != nil {
            return err
        }

        err = k.bankKeeper.SendCoinsFromModuleToAccount(ctx, types.ModuleName, borrowerAddr, sdk.NewCoins(sdk.NewCoin(assetIn.Denom, loan.AmountIn)))
        if err != nil {
            return err
        }

        k.DeleteLoan(ctx, loanID)

        return nil
    }
