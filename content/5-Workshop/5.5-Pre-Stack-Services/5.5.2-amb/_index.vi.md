---
title : "Tạo AMB Ethereum node"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.5.2. </b> "
---

#### Mục tiêu

Tạo AMB Ethereum node thật trước khi bật blockchain ledger validation.

#### Cách A - AWS Console

1. Mở **Amazon Managed Blockchain**.
2. Chọn **Access Ethereum**.
3. Tạo dedicated Ethereum node.
4. Chờ trạng thái **Available**.
5. Copy HTTP endpoint.

![AMB Ethereum node](/images/5-Workshop/5.5-Pre-Stack-Services/5.5.2-amb/amb_1.png)
![AMB Ethereum node](/images/5-Workshop/5.5-Pre-Stack-Services/5.5.2-amb/amb_2.png)
![AMB Ethereum node](/images/5-Workshop/5.5-Pre-Stack-Services/5.5.2-amb/amb_3.png)
![AMB Ethereum node](/images/5-Workshop/5.5-Pre-Stack-Services/5.5.2-amb/amb_4.png)

#### Cách B - Lệnh / code deployment

```powershell
$env:AMB_ETHEREUM_ENDPOINT = "https://nd-xxxxx.ethereum.managedblockchain.ap-southeast-1.amazonaws.com/"
awscurl `
  --service managedblockchain `
  --region ap-southeast-1 `
  -X POST `
  -d {"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1} `
  "$env:AMB_ETHEREUM_ENDPOINT"
```

#### Kiểm tra

JSON-RPC response cần trả về block number result.
