# number_cruncher
ansible role for system provisioning

## requirements

## variables
- fqdn_hostname: true
  - set fqdn_hostname to false to set the hostname as the hostname part only

## dependencies
requires the following role(s):
- [boot_loader](https://github.com/chomatz/boot_loader)
- [remote_management](https://github.com/chomatz/remote_management)
- [system_information](https://github.com/chomatz/system_information)
- [time_synchronization](https://github.com/chomatz/time_synchronization)

## examples
