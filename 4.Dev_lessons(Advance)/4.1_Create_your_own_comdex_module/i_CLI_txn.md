## Creating Commands for Transaction

We first need to generate the .pb files for tx.proto and then define txn messages and msgserver methods.

    func txRequest() *cobra.Command {
        cmd := &cobra.Command{
            Use:   "request [app-id] [pair-id] [amountIn] [amountOut] [fee] [duration]",
            Short: "create a loan request",
            Args:  cobra.ExactArgs(6),
            RunE: func(cmd *cobra.Command, args []string) error {
                ctx, err := client.GetClientTxContext(cmd)
                if err != nil {
                    return err
                }

                appID, err := strconv.ParseUint(args[0], 10, 64)
                if err != nil {
                    return err
                }

                pairID, err := strconv.ParseUint(args[1], 10, 64)
                if err != nil {
                    return err
                }

                amountIn, ok := sdk.NewIntFromString(args[2])
                if !ok {
                    return err
                }

                amountOut, ok := sdk.NewIntFromString(args[3])
                if !ok {
                    return err
                }

                fee, ok := sdk.NewIntFromString(args[4])
                if !ok {
                    return err
                }

                duration, ok := sdk.NewIntFromString(args[5])
                if !ok {
                    return err
                }

                msg := types.NewMsgCreate(ctx.GetFromAddress().String(), appID, pairID, amountIn, amountOut, fee, duration.Int64())

                return tx.GenerateOrBroadcastTxCLI(ctx, cmd.Flags(), msg)
            },
        }

        flags.AddTxFlagsToCmd(cmd)
        return cmd
    }

    func txApprove() *cobra.Command {
        cmd := &cobra.Command{
            Use:   "approve [loan-id]",
            Short: "approve a loan request",
            Args:  cobra.ExactArgs(1),
            RunE: func(cmd *cobra.Command, args []string) error {
                ctx, err := client.GetClientTxContext(cmd)
                if err != nil {
                    return err
                }

                loanID, err := strconv.ParseUint(args[0], 10, 64)
                if err != nil {
                    return err
                }

                msg := types.NewMsgApprove(ctx.GetFromAddress().String(), loanID)

                return tx.GenerateOrBroadcastTxCLI(ctx, cmd.Flags(), msg)
            },
        }

        flags.AddTxFlagsToCmd(cmd)
        return cmd
    }

    func txRepay() *cobra.Command {
        cmd := &cobra.Command{
            Use:   "repay [loan-id]",
            Short: "repay a loan ",
            Args:  cobra.ExactArgs(1),
            RunE: func(cmd *cobra.Command, args []string) error {
                ctx, err := client.GetClientTxContext(cmd)
                if err != nil {
                    return err
                }

                loanID, err := strconv.ParseUint(args[0], 10, 64)
                if err != nil {
                    return err
                }

                msg := types.NewMsgRepay(ctx.GetFromAddress().String(), loanID)

                return tx.GenerateOrBroadcastTxCLI(ctx, cmd.Flags(), msg)
            },
        }

        flags.AddTxFlagsToCmd(cmd)
        return cmd
    }

    func txCancel() *cobra.Command {
        cmd := &cobra.Command{
            Use:   "cancel [loan-id]",
            Short: "Cancel a loan ",
            Args:  cobra.ExactArgs(1),
            RunE: func(cmd *cobra.Command, args []string) error {
                ctx, err := client.GetClientTxContext(cmd)
                if err != nil {
                    return err
                }

                loanID, err := strconv.ParseUint(args[0], 10, 64)
                if err != nil {
                    return err
                }

                msg := types.NewMsgCancel(ctx.GetFromAddress().String(), loanID)

                return tx.GenerateOrBroadcastTxCLI(ctx, cmd.Flags(), msg)
            },
        }

        flags.AddTxFlagsToCmd(cmd)
        return cmd
    }

Here are the msgserver methods:

    func NewMsgServerImpl(keeper Keeper) types.MsgServer {
        return &msgServer{Keeper: keeper}
    }

    var _ types.MsgServer = msgServer{}

    func (m msgServer) MsgCreate(goCtx context.Context, request *types.MsgCreateRequest) (*types.MsgCreateResponse, error) {
        ctx := sdk.UnwrapSDKContext(goCtx)
        err := m.Keeper.Request(ctx, request.AppId, request.PairId, request.GetFrom(), request.AmountIn, request.AmountOut, request.Fee, request.DurationDays)
        if err != nil {
            return nil, err
        }
        return &types.MsgCreateResponse{}, nil
    }

    func (m msgServer) MsgApprove(goCtx context.Context, request *types.MsgApproveRequest) (*types.MsgApproveResponse, error) {
        ctx := sdk.UnwrapSDKContext(goCtx)
        err := m.Keeper.Approve(ctx, request.LoanId, request.GetFrom())
        if err != nil {
            return nil, err
        }
        return &types.MsgApproveResponse{}, nil
    }

    func (m msgServer) MsgRepay(goCtx context.Context, request *types.MsgRepayRequest) (*types.MsgRepayResponse, error) {
        ctx := sdk.UnwrapSDKContext(goCtx)
        err := m.Keeper.Repay(ctx, request.LoanId)
        if err != nil {
            return nil, err
        }
        return &types.MsgRepayResponse{}, nil
    }

    func (m msgServer) MsgCancel(goCtx context.Context, request *types.MsgCancelRequest) (*types.MsgCancelResponse, error) {
        ctx := sdk.UnwrapSDKContext(goCtx)
        err := m.Keeper.Cancel(ctx, request.LoanId)
        if err != nil {
            return nil, err
        }
        return &types.MsgCancelResponse{}, nil
    }
