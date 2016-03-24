# Openstack Deploy
Ansible playbooks to deploy a Openstack Liberty on Ubuntu 14.04

## Neutron specific config:
In order to make Neutron works you need to create manually some OVS bridges:

```
# ovs-vsctl add-br br-eth2
# ovs-vsctl add-br br-ex
```

Finally of you want access outside with you VM you need to add 1 nic and put it in the br-ex bridge:
```
# ovs-vsctl add-port br-ex eth1
```
## Cinder requirements:
For cinder, you need add a disk to the storage node.

## Example:
Deploy an All in One Openstack.
- Install the infra (Mysql, ntp...):
```
ansible-playbook -i hosts.aio --skip-tags multi-host -u root os-infra.yml
```
- Install Keystone:
```
ansible-playbook -i hosts.aio  -u root os-keystone.yml
```
- Install Glance:
```
ansible-playbook -i hosts.aio  -u root os-glance.yml
```
- Install nova:
```
ansible-playbook -i hosts.aio  -u root os-nova.yml
```
- Install Neutron:
```
ansible-playbook -i hosts.aio  -u root os-neutron.yml
```
**Warning: Don't forget to add the bridges.**
- Install Cinder:
```
ansible-playbook -i hosts.aio  -u root os-cinder.yml
```
- Install Horizon:
```
ansible-playbook -i hosts.aio  -u root os-horizon.yml
```
- Connect to the horizon web interface:
```
http://(your ip address)/horizon
```
Default admin credentials are admin/admin

Enjoy.
