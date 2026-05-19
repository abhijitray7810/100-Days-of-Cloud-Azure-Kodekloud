```bash
# Retrieve credentials if needed
showcreds

# Login to Azure
az login -u "kk_lab_user_main-a82d3c5c8b424587@azurefreekmlprod.onmicrosoft.com" -p 'g%d&s66p'

# Upload the file to the blob container
az storage blob upload \
  --account-name devopsst24418 \
  --container-name devops-blob-25287 \
  --name devops.txt \
  --file /tmp/devops.txt \
  --auth-mode login
```

To verify the upload:

```bash
az storage blob list \
  --account-name devopsst24418 \
  --container-name devops-blob-25287 \
  --auth-mode login \
  --output table
```
