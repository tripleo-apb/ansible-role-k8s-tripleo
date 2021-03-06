# ansible-role-k8s-tripleo

You can call this module directly:

```
- name: Test hieradata
  parse_tripleo_hiera:
    hieradata:
      glance::api::v1: True
    schema:
      glance::api::v1: DEFAULT.enable_glance_v1
  register: result


- name: Check values
  fail:
    msg: "DEFAULT not in conf_dict"
  when:
    - not result.conf_dict['DEFAULT']
    - not result.conf_dict['DEFAULT']['enable_glance_v1']
```

Or just include the role:

```
- name: Test include role
  include_role:
    name: 'ansible-role-k8s-tripleo'
  vars:
    hieradata:
      glance::api::v1: True
    schema:
      glance::api::v1: DEFAULT.enable_glance_v1
    fact_variable: 'glance_config'


- name: Check fact glance_config
  fail:
    msg: "glance_config not set"
  when:
    - not glance_config
```
