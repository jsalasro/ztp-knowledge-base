# cfg_base_mano

This repository contains the configuration for MANO clusters in kustomize format in order to be applied either manually or through GitOps tools.

## Overview

The base repository defines all the ACM policies and required resources to setup. Among them:

- **Placement** for the `mano-clusters`.
- **ClusterSetBinding** for the `mano-clusters`
- Different **PolicySet** and associated **PolicySetBindings** to group related configurations.
- **Policies** to configure OCP as defined on the HLD.
- **Policies** to deploy the Operators (see operators versioning).
- **Policies** to configure internal storage.
- **Policies** to create the required instances from the different applications.

> **NOTE**: this configuration expects the ClusterSet `mano-clusters` to exist, and in order to apply the policies to the hub cluster, the `local-cluster` must belong to it.

### Operators versioning

This repo is aimed to be used as Configutation As Code for the Mano cluster and for that, a configuration file `operators-version.cgf` is used to set the desired version of the installed operators.

## Usage

The aim of this content is to be used through an application of an **ArgoCD** instance. Nevertheless, it can be manually applied:

```
# clone the git repository and change path to it
# login to the target cluster where ACM is running
oc kustomize base | oc apply -f -
```

