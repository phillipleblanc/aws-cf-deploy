# aws-cf-deploy


## Deploy the GitHub OIDC Role

```bash
aws cloudformation deploy \
  --template-file cloudformation/github-oidc-role.yml \
  --stack-name github-oidc-role \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameter-overrides \
    CreateOIDCProvider=false
```
