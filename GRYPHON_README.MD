# Overview
This repository has been forked from https://github.com/wazuh/wazuh-ansible with the goal of addressing defects that
prevent the full breadth of configuration options for the Wazuh agent and manager roles.

A comparison of the current state of the fork against 4.13.1 of the upstream role is available at
https://github.com/gryphonai/wazuh-ansible/compare/v4.13.1...gryphonai:wazuh-ansible:kwl/main_fork_gryph-4_13_1

# Fork Strategy

This fork was created from https://github.com/wazuh/wazuh-ansible and then a branch was created from the upstream
tag 4.13.1. The branch where this README is found contains Gryphon initiated improvements (see below). 

# Full Ansible Galaxy Collection Support

NOTE: Two promising PRs have been submitted to formally add Galaxy Collection support to upstream
1. https://github.com/wazuh/wazuh-ansible/pull/1586
1. https://github.com/wazuh/wazuh-ansible/issues/1493

# New Features

These changes should be considered in a PR once the Galaxy role PR(s) mentioned above have been merged and ensure a
consistent directory structure


## GCP Pub/Sub (SIEM)

The following files have been modified to help enable GCP Pub/Sub Support as will be leveraged in SIEM agents.

| File                                                        | Purpose                                                          |
|-------------------------------------------------------------|------------------------------------------------------------------|
| roles/agent/defaults/main.yml                               | Defines a dictionary wazuh_agent_gcp_pubsub                      |
| roles/agent/templates/var-ossec-etc-ossec-agent.conf.j2     | Adds GCP Pub/Sub Ingestion logic                                 |
| roles/agent/tasks/Linux.yml                                 | adds support for GCP credentials to allow communication with GCP |
|                                                             |                                                                  |

# Fixes

These issues have PRs associated to them that, once merged, will remove the need to fork from the official wazuh role.

## PR topics under consideration as per current state of 4.13.1:


### ansible-wazuh-agent - force creation of local wazuh agent configuration files #1810

https://github.com/wazuh/wazuh-ansible/pull/1810

### Allow multiple api users to configured for ansible-wazuh-manager #1807

https://github.com/wazuh/wazuh-ansible/pull/1807

### Ansible-Wazuh-Manager: Correct mismatched closing tags in ossec config #1808

https://github.com/wazuh/wazuh-ansible/pull/1808

### Wwazuh-Indexer: Set index data path using the existing indexer_index_path var #1809

https://github.com/wazuh/wazuh-ansible/pull/1809

### Remove meta yamls that prevent indexer and agent role installation #1806

https://github.com/wazuh/wazuh-ansible/pull/1806