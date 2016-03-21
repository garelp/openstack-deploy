# Openstack Deploy
Ansible playbooks to deploy a Openstack Liberty on Ubuntu 14.04

## Neutron specific conig:
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
1. Install the infra (Mysql, ntp...):
```
ansible-playbook -i hosts.aio --skip-tags multi-host -u root os-infra.yml
```
2. Install Keystone:
```
ansible-playbook -i hosts.aio  -u root os-keystone.yml
```
3. Install Glance:
```
ansible-playbook -i hosts.aio  -u root os-glance.yml
```
4. Install nova:
```
ansible-playbook -i hosts.aio  -u root os-nova.yml
```
5. Install Neutron:
```
ansible-playbook -i hosts.aio  -u root os-keystone.yml
```
**Warning: Don't forget to add the bridges.**
6. Install Cinder:
```
ansible-playbook -i hosts.aio  -u root os-cinder.yml
```
7. Install Horizon:
```
ansible-playbook -i hosts.aio  -u root os-horizon.yml
```
8. Connect to the horizon web interface:
```
http://(your ip address)/horizon
```
Default admin credentials are admin/admin

Enjoy.
