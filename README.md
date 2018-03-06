## Azure

### Prerequisites

```bash
LOCATION=eastus
RESOURCEGROUP=changeme
```

### Login

```bash
az login
```

### Create resource group and deployment

```bash
az group create --location "$LOCATION" --name "$RESOURCEGROUP"
az group deployment create --resource-group "$RESOURCEGROUP" \
    --template-file azuredeploy.json \
    --parameters @azuredeploy.parameters.json \
    --parameters adminPublicKey="$(cat ~/.ssh/id_rsa.pub)"
```

### Check where to ssh

```bash
az group deployment show --resource-group "$RESOURCEGROUP" --name azuredeploy --query properties.outputs
ssh cloud-user@W.X.Y.Z
sudo -i
logout
logout
```

### Tear it down
```bash
az group delete --name "$RESOURCEGROUP" # --yes
```
