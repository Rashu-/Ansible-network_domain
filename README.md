# Network Domain Settings

Ansible role which defines domain servers and global domain settings for networking devices. 

The configuration of the role is done in such a way that it should not be necessary to modify the role.
All settings can configured by changing role parameters or by declaring new config as variable.
See the examples below for details.

Please report any issues or send PR.

## Examples

```yaml
---

- name: Example of how to add a domain server
  hosts: switches
  vars:
    domain_servers:
      srv1:
        - ip: 1.1.1.1
  roles:
    - Ansible-network_domain

- name: Example of how to add a couple domain servers in different vrfs
  hosts: switches
  vars:
    domain_servers:
      srv1:
        - ip: 1.1.1.1
          vrf: mgmt
      srv2:
        - ip: 8.8.8.8
          vrf: prod
  roles:
    - Ansible-network_domain

- name: Example of how to configure domain settings in different vrfs
  hosts: switches
  vars:
    system_domain_global:  
      domain_lookup: true               # by default it is false - disabled
      domain_name:                      # domain name suffix for this node
        - vrf: management 				# vrf for this name server
          name: oob.com
        - vrf: 							# don't add any value to be added to the default vrf
          name: abc.com
      domain_search:                    # domain suffix to search when performing DNS resolution
        - vrf: management 				
          name: oob.com
        - vrf: 							
          name: abc.com
  roles:
    - Ansible-network_domain
```

## Role variables

```yaml
# Define the domain global vars to be configured ( see README for examples)
system_domain_global: { }

# Define the dns servers to be used ( see README for examples)
domain_servers: { }
```


## License

Apache


## Author

Dan Murarasu
