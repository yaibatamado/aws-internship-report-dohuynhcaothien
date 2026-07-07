---
title : "Kiểm tra AMB ledger transaction"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.8.2. </b> "
---

#### Mục tiêu

Kiểm tra AMB node phản hồi được và ứng dụng lưu được ledger metadata.

#### Cách A - AWS Console

1. Mở giao diện MedChain AI.
2. Hoàn thành thao tác hồ sơ bệnh án có ghi ledger metadata.
3. Mở CloudWatch logs của ledger Lambda.
4. Kiểm tra `payloadHash` và `transactionHash`.

#### Cách B - Lệnh / code deployment

```powershell
awscurl `
  --service managedblockchain `
  --region ap-southeast-1 `
  -X POST `
  -d {"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1} `
  "$env:AMB_ETHEREUM_ENDPOINT"
```

#### Kiểm tra

Kết quả cần hiển thị block number hoặc transaction hash.
