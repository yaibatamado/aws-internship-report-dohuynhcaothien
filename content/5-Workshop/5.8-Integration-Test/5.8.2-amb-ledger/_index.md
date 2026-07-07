---
title : "Validate AMB ledger transaction"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.8.2. </b> "
---

#### Goal

Validate that the AMB node can respond and that the application can store ledger metadata.

#### Method A - AWS Console

1. Open the MedChain AI UI.
2. Complete a medical record action that writes ledger metadata.
3. Open CloudWatch logs for the ledger Lambda.
4. Confirm `payloadHash` and `transactionHash`.

#### Method B - Command / code deployment

```powershell
awscurl `
  --service managedblockchain `
  --region ap-southeast-1 `
  -X POST `
  -d {"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1} `
  "$env:AMB_ETHEREUM_ENDPOINT"
```

#### Validation

The result should show a block number or a transaction hash.
