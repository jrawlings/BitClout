> These docs are a Work-In-Progress, and are entirely created by the BitClout community.

# BitClout API

## Reference 
- The BitClout API has multiple base URL's available for use. They are:
  - https://api.bitclout.blue/api/v1
  - https://api.bitclout.green/api/v1
  - https://api.bitclout.com/api/v1
    > Note: This base url is protected by cloudflare, and will be unusable for most endpoints.
    
- These Base URL's do not work for all endpoints. You should use the base specified in the endpoint documentation.
  
## Endpoints

## Getting Transactions

#### Request
\* = Requiered
| Property  | Value                               |
|-----------|-------------------------------------|
| *Endpoint       | `https://api.bitclout.green/api/v1/transaction-info`       |
| *Headers    | `content-type: application/json`            |
| *Body       | `{"PublicKeyBase58Check":"<PUBLIC_KEY>"}`


#### Response 
<pre>
{
  "Error": String,
  <a href="https://github.com/HPaulson/BitClout-API-Docs/#transaction">"Transactions"</a>: [
    {
      "TransactionIDBase58Check": String,
      "RawTransactionHex": String,
      <a href="https://github.com/HPaulson/BitClout-API-Docs/#input">"Inputs"</a>: [
        {
          "TransactionIDBase58Check": String,
          "Index": Integer
        }
      ]
     <a href="https://github.com/HPaulson/BitClout-API-Docs/#output">"Outputs"</a>: [
        {
          "PublicKeyBase58Check": String,
          "AmountNanos": Integer
     ]
     "SignatureHex": String,
     "TransactionType": <a href="https://github.com/HPaulson/BitClout-API-Docs/#txntype">TransactionType</a>
     "BlockHashHex": String,
     <a href="https://github.com/HPaulson/BitClout-API-Docs/#output">"TransactionMetadata"</a>: {
        "BlockHashHex": String,
        "TxnIndexInBlock": String,
        "TxnType": <a href="https://github.com/HPaulson/BitClout-API-Docs/#txntype">TransactionType</a>,
        "TransactorPublicKeyBase58Check": String,
        "AffectedPublicKeys": [
          {
            "PublicKeyBase58Check": String,
            "Metadata": <a href="https://github.com/HPaulson/BitClout-API-Docs/#affectedpublickey-metadata">PublicKeyType</a>,
          }
        ],
        <a href="https://github.com/HPaulson/BitClout-API-Docs/#basictransfertxindexmetadata">"BasicTransferTxindexMetadata"</a>: {
          "TotalInputNanos": Integer,
          "TotalOutputNanos" Integer,
          "FeeNanos": Integer,
          "UtxoOpsDump": String
        },
        <a href="https://github.com/HPaulson/BitClout-API-Docs/#bitcoinexchangetxindexmetadata">"BitcoinExchangeTxindexMetadata"</a>: {
          < UNKNOWN >
        },
        <a href="https://github.com/HPaulson/BitClout-API-Docs/#creatorcointxindexmetadata">"CreatorCoinTxindexMetadata"</a>: {
          "OperationType": "buy" | "sell",
          "BitCloutToSellNanos": Integer,
          "CreatorCoinToSellNanos": Integer,
          "BitCloutToAddNanos": Integer
         },
        <a href="https://github.com/HPaulson/BitClout-API-Docs/#updateprofiletxindexmetadata">"UpdateProfileTxindexMetadata"</a>: {
          "ProfilePublicKeyBase58Check": String,
          "NewUsername": String,
          "NewDescription": String,
          "NewProfilePic": String,
          "NewCreatorBasisPoints": Integer,
          "NewStakeMultipleBasisPoints": Integer,
          "IsHidden": Boolean
        },
        <a href="https://github.com/HPaulson/BitClout-API-Docs/#submitposttxindexmetadata">"SubmitPostTxindexMetadata"</a>: {
          "PostHashBeingModifiedHex": String,
          "ParentPostHashHex": String,
          <a href="https://github.com/HPaulson/BitClout-API-Docs/#liketxindexmetadata">"LikeTxindexMetadata"</a>: {
            "IsUnlike": Boolean,
            "PostHashHex": String
          },
          <a href="https://github.com/HPaulson/BitClout-API-Docs/#followtxindexmetadata">"FollowTxindexMetadata"</a>: {
            "IsUnfollow": Boolean
          },
          <a href="https://github.com/HPaulson/BitClout-API-Docs/#privatemessagetxindexmetadata">"PrivateMessageTxindexMetadata"</a>: {
            < UNKNOWN TYPES >
          },
          <a href="https://github.com/HPaulson/BitClout-API-Docs/#swapidentitytxindexmetadata">"SwapIdentityTxindexMetadata"</a>: {
            < UNKNOWN TYPES >
          }
        }
      }
    }
  ],
  "BalanceNanos": Integer
}
</pre>
---

## Types

## TxnType
| Type  | Description                               |
|-----------|-------------------------------------|
| "BASIC_TRANSFER"       | Transfer of BitClout       |
| "UPDATE_PROFILE"    | Profile Update (Name, Bio, etc)            |
| "FOLLOW"       | Follow (Or unfollow) a user |
| "CREATOR_COIN"       | Purchase (Or sell) a creator coin |
| "SUBMIT_POST"       | Create (Or hide) post  |
| "LIKE"       | Like (Or unlike) post |
| "BLOCK_REWARD" | Reward for mining a block |

## AffectedPublicKey Metadata
| Type  | Description                               |
|-----------|-------------------------------------|
| "BasicTransferOutput"       | Public key of user who engaged in an action       |
| "ProfilePublicKeyBase58Check"    | ???            |
| "FollowedPublicKeyBase58Check"       | Public key of the user who recived a follow (Or unfollow) |
| "CreatorPublicKey"       | Public key of creator who's coin was purchased (Or sold) |
| "PosterPublicKeyBase58Check"       | Public key the a liked post author  |

## Transaction
| Type  | Description                               |
|-----------|-------------------------------------|
| "TransactionIDBase58Check"       | Transaction ID in Base 58      |
| "RawTransactionHex"    | Raw Hex Transaction ID            |
| "Inputs"       | Array of Transaction Inputs |
| "Outputs"       | Arrat of Transaction Outputs |
| "SignatureHex"       | Transaction Signature in Hex  |
| "TransactionMetadata"       | Transaction Meta Data  |

## Input
| Type  | Description                               |
|-----------|-------------------------------------|
| "TransactionIDBase58Check"       | Transaction ID in Base 58      |
| "Index"       | < UNKNOWN >      |

## Output
| Type  | Description                               |
|-----------|-------------------------------------|
| "PublicKeyBase58Check"       | Author's Pulic Key in Base 58      |
| "AmountNanos"       | < UNKNOWN >      |

## TransactionMetadata
| Type  | Description                               |
|-----------|-------------------------------------|
| "BlockHashHex"       | Transaction's block in hex |
| "TxnIndexInBlock"       | Transaction's index in it's block      |
| "TxnType"       | Transaction Type      |
| "AffectedPublicKeys"       | Array of users affected by the transaction      |
| "BasicTransferTxindexMetadata"       | Nano metadata
| "BitcoinExchangeTxindexMetadata"       | Bitcoin exchange metadata      |
| "CreatorCoinTxindexMetadata"       | Creator Coin transaction metadata      |
| "UpdateProfileTxindexMetadata"       | Profile Update meta data      |
| "SubmitPostTxindexMetadata"       | Created (Or hidden) post's metadata      |
| "LikeTxindexMetadata"       | Meta data of liked (Or unliked) post      |
| "FollowTxindexMetadata"       | Meta data of follow (Or Unfollow)      |
| "SwapIdentityTxindexMetadata"       | < UNKNOWN >      |

## BasicTransferTxindexMetadata
| Type  | Description                               |
|-----------|-------------------------------------|
| "TotalInputNanos"       | Nano's inputed into the transaction |
| "TotalOutputNanos"       | Nano's outputted into the transaction |
| "FeeNanos"       | Nano fee paid for the transaction (Input - Output) |
| "UtxoOpsDump"       | < UNKNOWN > |

## BitcoinExchangeTxindexMetadata
| Type  | Description                               |
|-----------|-------------------------------------|
| "< UNKNOWN TYPES >"       | < UNKNOWN > |

## CreatorCoinTxindexMetadata
| Type  | Description                               |
|-----------|-------------------------------------|
| "OperationType"       | Transaction Type, `"buy"` or `"sell"` |
| "BitCloutToSellNanos"       | BitClout paid for creator coin |
| "CreatorCoinToSellNanos"       | Creator Coin sold for BitClout |
| "BitCloutToAddNanos"       | < UNKNOWN > |

## UpdateProfileTxindexMetadata
| Type  | Description                               |
|-----------|-------------------------------------|
| "ProfilePublicKeyBase58Check"       | User's public key in Base 58 |
| "NewUsername"       | User's new username |
| "NewDescription"       | User's new bio |
| "NewProfilePic"       | User's new profile image |
| "NewCreatorBasisPoints"       | < UNKNOWN > |
| "NewStakeMultipleBasisPoints"       | < UNKNOWN > |
| "IsHidden"       | < UNKNOWN > |

## SubmitPostTxindexMetadata
| Type  | Description                               |
|-----------|-------------------------------------|
| "PostHashBeingModifiedHex"       | Transaction ID of the modified post |
| "ParentPostHashHex"       | Transaction ID of the parent post (When the modified post is a reply) |

## LikeTxindexMetadata
| Type  | Description                               |
|-----------|-------------------------------------|
| "IsUnlike"       | Whether the transaction was an unlike (rather than a like) |
| "PostHashHex"       | Transaction ID of the liked post |

## FollowTxindexMetadata
| Type  | Description                               |
|-----------|-------------------------------------|
| "IsUnfollow"       | Whether the transaction was an unfollow (rather than a follow) |

## PrivateMessageTxindexMetadata
| Type  | Description                               |
|-----------|-------------------------------------|
| "< UNKNOWN TYPES >"       | < UNKNOWN > |

## SwapIdentityTxindexMetadata
| Type  | Description                               |
|-----------|-------------------------------------|
| "< UNKNOWN TYPES >"       | < UNKNOWN > |

