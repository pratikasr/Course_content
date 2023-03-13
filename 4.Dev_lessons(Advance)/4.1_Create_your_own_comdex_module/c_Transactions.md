## Transaction Messages

Here are the list of txn messages defined in tx.proto of the loan module. We will be using these transaction to create, approve, repay and cancel a loan.


    message MsgCreateRequest {
    string from = 1 [(gogoproto.moretags) = "yaml:\"from\""];
    uint64 app_id = 2 [(gogoproto.moretags) = "yaml:\"app_id\""];
    uint64 pair_id = 3 [
        (gogoproto.moretags) = "yaml:\"pair_id\""
    ];
    string amount_in = 4 [
        (gogoproto.customtype) = "github.com/cosmos/cosmos-sdk/types.Int",
        (gogoproto.moretags) = "yaml:\"amount_in\"",
        (gogoproto.nullable) = false
    ];
    string amount_out = 5 [
        (gogoproto.customtype) = "github.com/cosmos/cosmos-sdk/types.Int",
        (gogoproto.moretags) = "yaml:\"amount_out\"",
        (gogoproto.nullable) = false
    ];
    string fee = 6 [
        (gogoproto.customtype) = "github.com/cosmos/cosmos-sdk/types.Int",
        (gogoproto.moretags) = "yaml:\"fee\"",
        (gogoproto.nullable) = false
    ];
    int64 duration_days = 7 [
        (gogoproto.moretags) = "yaml:\"duration_days\""
    ];
    }

    message MsgCreateResponse {}

    message MsgApproveRequest {
    string from = 1 [(gogoproto.moretags) = "yaml:\"from\""];
    uint64 loan_id = 2 [(gogoproto.moretags) = "yaml:\"loan_id\""];
    }

    message MsgApproveResponse {}

    message MsgRepayRequest {
    string from = 1 [(gogoproto.moretags) = "yaml:\"from\""];
    uint64 loan_id = 2 [(gogoproto.moretags) = "yaml:\"loan_id\""];
    }

    message MsgRepayResponse {}

    message MsgCancelRequest {
    string from = 1 [(gogoproto.moretags) = "yaml:\"from\""];
    uint64 loan_id = 2 [(gogoproto.moretags) = "yaml:\"loan_id\""];
    }

    message MsgCancelResponse {}


    service Msg {
    rpc MsgCreate(MsgCreateRequest) returns (MsgCreateResponse);
    rpc MsgApprove(MsgApproveRequest) returns (MsgApproveResponse);
    rpc MsgRepay(MsgRepayRequest) returns (MsgRepayResponse);
    rpc MsgCancel(MsgCancelRequest) returns (MsgCancelResponse);
    }
