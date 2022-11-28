# Ansible Automation Platform using ServiceNow Inventory Plugin

## Create a new credential type 

Administration > Credential Types

- name: ServiceNow credentials

Input configuration:

```yaml
fields:
  - id: SN_USERNAME
    type: string
    label: Username
  - id: SN_PASSWORD
    type: string
    label: Password
    secret: true
  - id: SN_HOST
    type: string
    label: Snow Instance
required:
  - SN_USERNAME
  - SN_PASSWORD
  - SN_HOST
```

Injector configuration:

```yaml
env:
  SN_HOST: '{{ SN_HOST }}'
  SN_PASSWORD: '{{ SN_PASSWORD }}'
  SN_USERNAME: '{{ SN_USERNAME }}'
```

## Create a project

Resource > Projects

- name: ServiceNow inventory
- source control type: Git
- source control URL: https://github.com/sebw/AAP-servicenow-cmdb
- tick update revision on launch

Save and sync.

## Create ServiceNow credentials

- name: ServiceNow credentials
- Credential type: Servicenow credentials
- username: XYZ
- password: XYZ
- Snow instance: devXYZABC

## Create an inventory.

Add an inventory source.

- name: ServiceNow inventory source
- Source: sourced from a project
- Credentials: ServiceNow credentials
- project: ServiceNow inventory
- Inventory file: `/`
- overwrite
- update on launch

Sync.

You should see your hosts and groups.

## More info

https://www.ansible.com/blog/using-an-inventory-plugin-from-a-collection-in-ansible-tower
