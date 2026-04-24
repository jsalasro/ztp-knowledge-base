# ABI

Installing OCP4 on Baremetal nodes using Agent-Based Installer.

## Prerequisites

- RPMs:
  - nmstate
- Openshift-install version according to the cluster version intended for installation.
- Ansible collections:
  - requirements.yaml:

    ```
    ---
    collections:
      - community.general
      - name: kubernetes.core
        version: 6.2.0
      - name: redhat.openshift
        version: 5.0.0
      - name: redhat.satellite
        version: 5.7.0
      - name: redhat.satellite_operations
        version: 3.0.0
    ...
    ```
	
- Python modules:
  - kubernetes
  - openshift
  - jmespath

## How this repository works

Expect to find 3 folders: ansible, inventory and quay-mirroring.

### ansible

All the required playbooks to install OpenShift following the ABI process is stored here.

### ansible/templates

Ansible templates: ABI agent-config and install-confg templates and CRs definitions.

### quay-mirroring

All related scripts to be used for mirroring from CSZ to private quay registry deployed on OpenShift.

### Inventory

All the playbooks use the same inventory, this inventory has to be properly modified for each enviroment.

## How to run the deploy and configuration of the cluster

The ansible/deploy_cluster.yaml playbook is in charge of invoking other playbooks that installs the cluster following the ABI procedure, booting the ISO in the ILOs, waiting for cluster to be installed and configuring validated patterns onboarding.

It is actually possible to run all the playbooks in the same execution:

```
$ ansible-playbook -i inventory/inventory-{{ environment }}.yaml -e @inventory/vault-{{ environment }} ansible/deploy_cluster.yaml -J
```

If running the hashicorp_secrets playbook make sure the appropiate python interpreter is selected:

```
$ ansible-playbook -i inventory/inventory-{{ environment }}.yaml -e @inventory/vault-{{ environment }}  -e ansible_python_interpreter=/usr/bin/python3.11 ansible/vso_onboarding.yaml -J
```

### Check how OpenShift install is progressing

```
$ openshift-install --dir <install_directory> agent wait-for install-complete --log-level=debug
```

## Authors
Paulo Pacifico <ppacific@redhat.com>
Juan Carlos Tovar <jtovarro@redhat.com>
