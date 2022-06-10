# Install Red Hat Advanced Cluster Security for K8s in OpenShift

Deploy Red Hat Advanced Cluster Security for Kubernetes Demo ( Apps ) on OpenShift 4.x in a easy and automated way.

## 1. Prerequisites

### Ansible 2.9

- [Ansible Installation Guide](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- PyYAML
- python3-openshift
- python3-jmespath

### Define variables for your cluster

| Variable | Description |
| -------- | -------- |
| stackrox_central_admin_password    | RHACS - Central Admin Password     |
| ACTION    | create ( To install ) or destroy ( To uninstall )  |

## 2. Steps

### 2.1 Installing RHACS and Demo workloads

```bash
ansible-galaxy collection install kubernetes.core
git clone https://github.com/rh-mobb/rhacs-demo
cd rhacs-demo
```

You can use the **rhacs-install.yaml** as example, please change the credentials before running the playbook.

### 2.2 Example file rhacs-install.yaml

```bash
- hosts: localhost
  vars:
    stackrox_central_admin_password: stackrox
  roles:
  - ocp4_install_acs
  - ocp4_deploy_acs_demo_apps
```

### 2.3 Login to ocp using a Cluster-Admin user

```bash
oc login -u admin https://yourcluster:6443
```

### 2.4 Installing RHACS cluster and deploy Demo Apps

```bash
ansible-playbook rhacs-install.yaml
```

### Optional - Only install Demo Apps

```bash
ansible-playbook rhacs-demo.yaml
```
