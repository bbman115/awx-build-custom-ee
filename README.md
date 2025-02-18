# awx-build-custom-ee
Short project to know how to create a basic AWX Execution Environment custom image based on Centos:stream9

## Requirements
### Linux Host
- It has to have access to https://quay.io/repository/ansible/awx-ee?tab=tags&tag=latest in order to use the base EE from RedHat quay.io.
- It has to have access to a private registry to push/pull images (i.e. setup a private Docker registry on your own or use GitHub/GitLab container registry, Sonatype Nexus etc...).
- Packages `ansible-builder` and `docker` must be installed.

### Execution Environment information
- You have to know :
    - which ansible collections you need
    - which python lib you need. 
    - which CentOS 'OS packages' you need.
    - which ansible-core version you want to working with.

## Step-by-step
1) Add ansible collections you need into `requirements.yml`.
2) Add python libraries you need into `requirements.txt`.
3) If needed, you can add some 'OS' packages into `bindep.txt`.
4) If needed, you can set some append/prepend instructions in `execution-environment.yml` or change base_image name to use a different CentOS image for instance.
4) Run `ansible-builder build -v3 -t your-registry.com/path-to-image/your-image-name:X.Y.Z`.

In this example :
- requirements.txt will be used to install
  - hvac & requests python module
- requirements.yml will be used to install 
  - community.hashi_vault & community.zabbix ansible collections.
- bindep.txt will be used to install 'OS' packages that I need.


## Sources
Ansible Execution Environment Definition
https://ansible.readthedocs.io/projects/builder/en/stable/definition/#execution-environment-definition 

Ansible Release Schedule
https://docs.ansible.com/ansible/latest/reference_appendices/release_and_maintenance.html#release-schedule

