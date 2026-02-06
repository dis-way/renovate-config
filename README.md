# renovate-config
Default renovate config for the dis-way organization

## AKS version management

To have Renovate maintain the AKS version in your Terraform files, add the following comment above the variable default:

```hcl
# renovate: datasource=custom.azure-aks depName=azure-aks versioning=loose
default = "1.30"
```
