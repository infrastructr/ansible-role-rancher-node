[![Build Status](https://travis-ci.org/infrastructr/ansible-role-rancher-node.svg?branch=master)](https://travis-ci.org/infrastructr/ansible-role-rancher-node)
[![Ansible Galaxy](https://img.shields.io/badge/role-infrastructr.rancher_node-blue.svg)](https://galaxy.ansible.com/infrastructr/rancher_node/)
[![GitHub tag (latest by date)](https://img.shields.io/github/v/tag/infrastructr/ansible-role-rancher)](https://galaxy.ansible.com/infrastructr/rancher_node)
[![Ansible Galaxy Downloads](https://img.shields.io/ansible/role/d/48976.svg?color=blue)](https://galaxy.ansible.com/infrastructr/rancher_node/)

# Ansible Role: Rancher Node

An Ansible Role that manages setup and configuration of an [Rancher](https://rancher.com/docs/rancher/v2.x/en/installation/) nodes.

## Role Variables

Available variables listed below, along with default values (see `defaults/main.yml`):

    rancher_node_master_api_token: "{{ rancher_api_token }}"
    
Rancher master API token.

    rancher_node_cluster_id: "{{ rancher_cluster_id }}"
    
Rancher cluster ID.

    rancher_node_master_group: paas_master

Inventory group for the Rancher master hosts.
    
    rancher_node_master_host: "{{ hostvars[groups[rancher_master_group][0]]['ansible_host'] }}"
    
Rancher API host.    
    
    rancher_node_master_url: "https://{{ rancher_node_master_host }}"
    
Rancher API URL.    
    
    rancher_node_validate_certs: no
  
Enable/disable SSL certificate validation when communicating with the Rancher API.

    rancher_node_retries: 10
    
Number of retries for long-running operations.

    rancher_node_delay: 30

Number of seconds as delay between retries for long-running operations.

    rancher_node_address: ''
    
Node address.    
    
    rancher_node_internal_address: ''

## Dependencies

- [geerlingguy.pip](https://galaxy.ansible.com/geerlingguy/pip)
- [geerlingguy.docker](https://galaxy.ansible.com/geerlingguy/docker)

## Example Playbook

    - hosts: all
      vars:
        pip_package: python3-pip
        pip_install_packages:
          - name: docker    
      roles:
        - geerlingguy.pip
        - geerlingguy.docker
        
    - hosts: paas_master
      roles:
        - infrastructr.rancher_master
        - infrastructr.rancher_cluster

    - hosts: paas_node
      roles:
        - infrastructr.rancher_node
        
## Development

Use [docker-molecule](https://github.com/infrastructr/docker-molecule) following the instructions to run [Molecule](https://molecule.readthedocs.io/en/stable/)
or install [Molecule](https://molecule.readthedocs.io/en/stable/) locally (not recommended, version conflicts might appear).

Provide Hetzner Cloud token:

    export HCLOUD_TOKEN=123abc456efg

Use following to run tests:

    molecule test --all

## Maintainers

- [build-failure](https://github.com/build-failure)

## License

See the [LICENSE.md](LICENSE.md) file for details.

## Author Information

This role was created in 2020 by [infrastructr](https://github.com/infrastructr) team.
