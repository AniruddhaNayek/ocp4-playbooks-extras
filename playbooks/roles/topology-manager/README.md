Validate Topology Manger
========================

This playbook validates the Topology Manager for which it covers the following use cases:

* Validate Pod Alignment with CPU requests and Topology Manager policy set to Best Effort
* Validate Pod Alignment with CPU requests and Topology Manager policy set to Restricted
* Validate Pod Alignment with CPU requests and Topology Manager policy set to None

Note: For use cases related to single numa-node policy those need to be validated manually

Pre-requisite & Requirements
----------------------------

- The cluster is in a known good state, without any errors.
- Setting up CPU manager in the cluster
- Label the worker-1 node while setting up CPU manager
- First manually complete the use case for single-numa-node to analyze the partion & CPU memory for the above use cases ( *Validate Pod Alignment with CPU requests and Topology Manager Single-numa-node policy* )

Role Variables
--------------

| Variable         | Required | Comments                                        |
| ---------------- | -------- | ----------------------------------------------- |
| topology_enabled | no       | Set it to true to run this playbook.            |
| besteffort_cpuv1 | yes      | Request desired no. of CPUs for the first pod.  |
| besteffort_cpuv2 | yes      | Request desired no. of CPUs for the second pod. |
| restricted_cpuv1 | yes      | Request desired no. of CPUs for the first pod.  |
| restricted_cpuv2 | yes      | Request desired no. of CPUs for the second pod. |
| none_cpuv1       | yes      | Request desired no. of CPUs for the first pod.  |
| none_cpuv2       | yes      | Request desired no. of CPUs for the second pod. |

Example Playbook
----------------

```
- name: Validate topology manager on Power
  hosts: bastion
  roles:
  - topology-manager
```

Steps to run playbook
---------------------

- Copy `ocp4-playbooks-extras/examples/inventory` file to the home or working directory and modify it to add a remote host
- Copy the `ocp4-playbooks-extras/examples/topology_vars.yaml` to the home or working directory and set the role variables for `roles/topology-manager` with the custom inputs.
- To execute the playbook run the below sample command

Sample Command
--------------

ansible-playbook -i inventory -e @topology_vars.yaml ~/ocp4-playbooks-extras/playbooks/topology-manager.yml

License
-------

See LICENCE.txt

Author Information
------------------

aniruddha.nayek@ibm.com

