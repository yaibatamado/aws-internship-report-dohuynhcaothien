---
title : "Create AMB Ethereum node"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.5.2. </b> "
---

#### Goal

Create a real AMB Ethereum node before enabling blockchain ledger validation.

#### Method A - AWS Console

1. Open **Amazon Managed Blockchain**.
2. Choose **Access Ethereum**.
3. Create a dedicated Ethereum node.
4. Wait until status is **Available**.
5. Copy the HTTP endpoint.

![AMB Ethereum node](/images/5-Workshop/5.5-Pre-Stack-Services/5.5.2-amb/amb_1.png)
![AMB Ethereum node](/images/5-Workshop/5.5-Pre-Stack-Services/5.5.2-amb/amb_2.png)
![AMB Ethereum node](/images/5-Workshop/5.5-Pre-Stack-Services/5.5.2-amb/amb_3.png)
![AMB Ethereum node](/images/5-Workshop/5.5-Pre-Stack-Services/5.5.2-amb/amb_4.png)

#### Method B - Command / code deployment

```powershell
$env:AMB_ETHEREUM_ENDPOINT = "https://nd-xxxxx.ethereum.managedblockchain.ap-southeast-1.amazonaws.com/"
awscurl `
  --service managedblockchain `
  --region ap-southeast-1 `
  -X POST `
  -d {"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1} `
  "$env:AMB_ETHEREUM_ENDPOINT"
```

#### Validation

The JSON-RPC response should return a block number result.
