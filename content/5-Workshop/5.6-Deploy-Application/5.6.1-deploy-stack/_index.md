---
title : "Create application stack"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.6.1. </b> "
---

#### Goal

Deploy the main MedChain AI stack after pre-stack services are ready.

#### Method A - AWS Console

1. Open **CloudFormation**.
2. Create stack from the synthesized template if you deploy manually.
3. Enter stack name `MedChainAiLabStack`.
4. Wait for **CREATE_COMPLETE**.

![Stack complete](/images/5-Workshop/5.6-Deploy-Application/5.6.1-deploy-stack/stack.png)

#### Method B - Command / code deployment

```powershell
$env:ENABLE_API_ROUTES = "true"
$env:ENABLE_WEEK3_OPERATIONS = "true"
$env:RETAIN_DATA = "false"
$env:ENABLE_CLOUDFRONT = "true"
$env:USE_EXISTING_CLOUDFRONT = "false"
npx cdk synth $StackName --profile $Profile
npx cdk deploy $StackName --profile $Profile --require-approval never
```

#### Validation

CloudFormation stack status should be CREATE_COMPLETE and outputs should be available.

![Stack complete](/images/5-Workshop/5.6-Deploy-Application/5.6.1-deploy-stack/stack_1.png)
