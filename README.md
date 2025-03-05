# aws-cf-deploy

## Find existing OIDC provider ARN:

```bash
aws iam list-open-id-connect-providers --query 'OpenIDConnectProviderList[?contains(Arn, `token.actions.githubusercontent.com`)].Arn' --output text
```

## Deploy the GitHub OIDC Role

```bash
aws cloudformation deploy \
  --template-file cloudformation/github-oidc-role.yml \
  --stack-name github-oidc-role \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameter-overrides \
    CreateOIDCProvider=false \
    ExistingOIDCProviderArn=<existing-oidc-provider-arn>
```

## Get GitHub OIDC Role ARN

```bash
aws cloudformation describe-stacks \
  --stack-name github-oidc-role \
  --query 'Stacks[0].Outputs[?OutputKey==`RoleARN`].OutputValue' \
  --output text
```
