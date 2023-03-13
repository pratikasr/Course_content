## Creating a structure of the application

To create a structure for a blockchain application that enables users to lend and borrow digital assets from each other, use the Ignite CLI to generate the necessary code.

Create a module with a dependency on the standard Cosmos SDK `bank` module by running the following command:

    ignite scaffold module loan --dep bank

Now, we will create our proto:

    message Loan {
    uint64 id = 1 ;
    uint64 app_id = 2
    [(gogoproto.customname) = "AppId",
        (gogoproto.moretags) = "yaml:\"app_id\""];

    uint64 pair_id = 3 [
        (gogoproto.customname) = "PairID",
        (gogoproto.moretags) = "yaml:\"pair_id\""];

    string owner = 4 [(gogoproto.moretags) = "yaml:\"owner\""];
    string amount_in = 5 [
        (gogoproto.customtype) = "github.com/cosmos/cosmos-sdk/types.Int",
        (gogoproto.moretags) = "yaml:\"amount_in\"",
        (gogoproto.nullable) = false
    ];
    string amount_out = 6 [
        (gogoproto.customtype) = "github.com/cosmos/cosmos-sdk/types.Int",
        (gogoproto.moretags) = "yaml:\"amount_out\"",
        (gogoproto.nullable) = false
    ];
    string fee = 7 [
        (gogoproto.customtype) = "github.com/cosmos/cosmos-sdk/types.Int",
        (gogoproto.moretags) = "yaml:\"fee\"",
        (gogoproto.nullable) = false
    ];
    google.protobuf.Timestamp created_at = 8 [
        (gogoproto.nullable) = false,
        (gogoproto.stdtime) = true,
        (gogoproto.moretags) = "yaml:\"created_at\""
    ];
    int64 duration_days = 9 [
        (gogoproto.moretags) = "yaml:\"duration_days\""
    ];
    string lender = 10 [(gogoproto.moretags) = "yaml:\"owner\""];
    string state = 11 [(gogoproto.moretags) = "yaml:\"state\""];
    }

Here, is the basic struct of our loan which any user can request.