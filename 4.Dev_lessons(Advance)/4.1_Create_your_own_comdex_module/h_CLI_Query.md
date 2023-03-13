## Creating Commands for Query

We first need to create proto for Query and then generate the .pb files for the same.

Here is the proto file we created.

    syntax = "proto3";
    package comdex.loan.v1beta1;

    import "gogoproto/gogo.proto";
    import "google/api/annotations.proto";
    import "cosmos/base/query/v1beta1/pagination.proto";
    import "comdex/loan/v1beta1/params.proto";
    import "comdex/loan/v1beta1/loan.proto";

    option go_package = "github.com/comdex-official/comdex/x/loan/types";

    service Query {
    rpc Params(QueryParamsRequest) returns (QueryParamsResponse) {
        option (google.api.http).get = "/comdex-official/comdex/loan/params";
    }
    rpc QueryLoan(QueryLoanRequest) returns (QueryLoanResponse) {
        option (google.api.http).get = "/comdex/lend/v1beta1/loans/{id}";
    }
    }

    message QueryParamsRequest {}

    message QueryParamsResponse {
    Params params = 1 [(gogoproto.nullable) = false];
    }

    message QueryLoanRequest {
    uint64 id = 1;
    }

    message QueryLoanResponse {
    Loan loan = 1
    [(gogoproto.nullable) = false, (gogoproto.moretags) = "yaml:\"loan\""];
    }

After generating the .pb files we need to create the query commands.

Here is the query command which we created.

    func queryLoan() *cobra.Command {
        cmd := &cobra.Command{
            Use:   "loan [id]",
            Short: "Query a loan position",
            Args:  cobra.ExactArgs(1),
            RunE: func(cmd *cobra.Command, args []string) error {
                ctx, err := client.GetClientQueryContext(cmd)
                if err != nil {
                    return err
                }

                id, err := strconv.ParseUint(args[0], 10, 64)
                if err != nil {
                    return err
                }

                queryClient := types.NewQueryClient(ctx)

                res, err := queryClient.QueryLoan(
                    context.Background(),
                    &types.QueryLoanRequest{
                        Id: id,
                    },
                )
                if err != nil {
                    return err
                }

                return ctx.PrintProto(res)
            },
        }

        flags.AddQueryFlagsToCmd(cmd)

        return cmd
    }

We also need to define queryserver methods:

    func queryLoan() *cobra.Command {
        cmd := &cobra.Command{
            Use:   "loan [id]",
            Short: "Query a loan position",
            Args:  cobra.ExactArgs(1),
            RunE: func(cmd *cobra.Command, args []string) error {
                ctx, err := client.GetClientQueryContext(cmd)
                if err != nil {
                    return err
                }

                id, err := strconv.ParseUint(args[0], 10, 64)
                if err != nil {
                    return err
                }

                queryClient := types.NewQueryClient(ctx)

                res, err := queryClient.QueryLoan(
                    context.Background(),
                    &types.QueryLoanRequest{
                        Id: id,
                    },
                )
                if err != nil {
                    return err
                }

                return ctx.PrintProto(res)
            },
        }

        flags.AddQueryFlagsToCmd(cmd)

        return cmd
    }

Our query for a loan using loanID is ready to use.
