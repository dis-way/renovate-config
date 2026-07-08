# renovate-config
Default renovate config for the dis-way organization

## Release age gating

Updates wait `minimumReleaseAge: 3 days` before a PR is created, as a supply-chain precaution.
The age check only applies when the datasource provides a release timestamp
(`minimumReleaseAgeBehaviour: timestamp-optional`). Renovate's `docker` datasource only provides
timestamps for Docker Hub, so images from other registries (ghcr.io, mcr.microsoft.com, quay.io, ...)
update as soon as Renovate sees them — without `timestamp-optional` they would instead wait forever
(the Renovate v42 default is `timestamp-required`).

First-party `ghcr.io/altinn/altinn-platform/**` images are additionally exempted from the cooldown
entirely, so they keep updating immediately even if Renovate learns to resolve timestamps for ghcr.io
in the future.

## AKS version management

To have Renovate maintain the AKS version in your Terraform files, add the following comment above the variable default:

```hcl
# renovate: datasource=custom.azure-aks depName=azure-aks versioning=loose
default = "1.30"
```
