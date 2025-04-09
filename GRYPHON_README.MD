This repository has been forked from https://github.com/wazuh/wazuh-ansible with the major goal of adding full support 
for Ansible Galaxy installation.

A comparison of the current state of the fork against 4.11.2 of the upstream role is available at
https://github.com/wazuh/wazuh-ansible/compare/v4.11.2...gryphonai:wazuh-ansible:kwl/gdo-1489-wazuh-upgrade

Additionally, this fork corrects minor defects (to be submitted to upstream), and adds GCP Pub/Sub support via ansible 
(to be submitted to upstream)

- [Ansible Galaxy Support](#ansible-galaxy-support)
- [New Features](#new-features)
- [Fixes](#fixes)

# Ansible Galaxy Support

The files galaxy.yml and meta/runtime.yml have been added to our fork to support galaxy ansible installation through 
requirements.txt (devenv layer performs installation of roles)  

Additionally, a `repos_var_path` variable has been introduced and added to multiple role../defaults/main.yml in order
to support changing the path to where vars files are located (as necessary in the refactor effort to support 
ansible galaxy)

NOTE: Two promising PRs have been submitted to formally add Galaxy support to upstream
1. https://github.com/wazuh/wazuh-ansible/pull/1586
1. https://github.com/wazuh/wazuh-ansible/issues/1493 (appears to be all but ready for inclusion in 5.0.0 release?)

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

These changes should be considered in a PR once the Galaxy role PR(s) mentioned above have been merged and ensure a
consistent directory structure

## Improperly closed xml tags

Modified `roles/manager/templates/var-ossec-etc-ossec-server.conf.j2` to ensure tags are closed properly

## Make indexer index path a parameter instead of hard-coded

The following files have been modified to ensure that the indexer index paths can be specific as opposed to hard coded
- roles/indexer/templates/opensearch.yml.j2
- roles/indexer/tasks/main.yml

## Overwrite default files

The file `roles/agent/tasks/Linux.yml` has been changed to include `force: true` in the ansible task to ensure that
the default files that are created upon package installation can be overwritten by Ansible

## Install APT packages with Ansible native functions

The file `roles/dashboard/tasks/Debian.yml` has been updated to install APT repo keys using built in `apt_key`
ansible functions as opposed to native commands that call curl, gpg import, etc...