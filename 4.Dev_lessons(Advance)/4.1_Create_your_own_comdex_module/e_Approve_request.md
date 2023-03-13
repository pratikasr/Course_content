## Approve a loan

In the loan approval process, another account can approve a loan request made by a borrower and agree to the terms proposed. This involves transferring the requested funds from the lender to the borrower.

For a loan to be eligible for approval, its status must be "requested," indicating that the borrower has requested a loan and is waiting for a lender to agree to the terms and provide the funds. Once a lender decides to approve the loan, they can transfer the funds to the borrower.

After loan approval, the loan status changes to "approved," indicating that the funds have been successfully transferred and the loan agreement is now in effect.


    func (k Keeper) Approve(ctx sdk.Context, loanID uint64, lender string) error {
        loan, found := k.GetLoan(ctx, loanID)
        if !found {
            return sdkerrors.Wrapf(sdkerrors.ErrKeyNotFound, "key %d doesn't exist for loanID", loanID)
        }
        if loan.State != "requested" {
            return sdkerrors.Wrapf(types.ErrWrongLoanState, "%v", loan.State)
        }

        pair, found := k.Asset.GetPair(ctx, loan.PairID)
        if !found {
            return assettypes.ErrorPairDoesNotExist
        }

        assetOut, found := k.Asset.GetAsset(ctx, pair.AssetOut)
        if !found {
            return assettypes.ErrorAssetDoesNotExist
        }

        lenderAddr, err := sdk.AccAddressFromBech32(lender)
        if err != nil {
            return err
        }

        borrowerAddr, err := sdk.AccAddressFromBech32(loan.Owner)
        if err != nil {
            return err
        }

        err = k.bankKeeper.SendCoinsFromAccountToModule(ctx, lenderAddr, types.ModuleName, sdk.NewCoins(sdk.NewCoin(assetOut.Denom, loan.AmountOut)))
        if err != nil {
            return err
        }

        err = k.bankKeeper.SendCoinsFromModuleToAccount(ctx, types.ModuleName, borrowerAddr, sdk.NewCoins(sdk.NewCoin(assetOut.Denom, loan.AmountOut)))
        if err != nil {
            return err
        }
        loan.Lender = lender
        loan.State = "approved"
        return nil
    }

