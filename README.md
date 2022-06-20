# hub-spoke-without-nva
Step by step to create Azure Hub-Spoke network topology without NVA (Network Virtual Appliance)

## Situation:
Azure documentation provides some information about creating Hub-Spoke network topology where Spoke vNets (Virtual Networks) can connect to each other without creating NVA (Network Virtual Appliance such as Azure Firewall or 3rd party Firewall).

## Objective:
To provide clear step-by-step guide to successfully create Hub-Spoke network topology using VPN Gateway as inter-vnet router.

## Step-by-step setup:
1. Create the vNets, in this case I created 1 Hub vNet and 2 Spoke vNets.
* Hub vNet CIDR: 10.0.0.0/16
* Spoke1 vNet CIDR: 10.1.0.0/16
* Spoke2 vNet CIDR: 10.2.0.0/16

2. Create subnets, GatewaySubnet in Hub and one subnet for VM (Virtual Machine) in each of the Spoke.
* Hub GatewaySubnet CIDR: 10.0.0.0/28
* Spoke1 spoke1subnet CIDR: 10.1.0.0/24
* Spoke1 spoke2subnet CIDR: 10.2.0.0/24

