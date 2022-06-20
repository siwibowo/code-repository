# hub-spoke-without-nva
Step by step to create Azure Hub-Spoke network topology without NVA (Network Virtual Appliance)

## Situation:
Azure documentation provides some information about creating Hub-Spoke network topology where Spoke vNets (Virtual Networks) can connect to each other without creating NVA (Network Virtual Appliance such as Azure Firewall or 3rd party Firewall).

## Objective:
To provide clear step-by-step guide to successfully create Hub-Spoke network topology using VPN Gateway as inter-vNet router.

## Step-by-step setup:
1. Create the vNets and subnets, in this case I created 1 Hub vNet and 2 Spoke vNets. For simplicity, use the same Azure region for all vNets. I use Australia East region.
- Hub vNet CIDR: 10.0.0.0/16, GatewaySubnet CIDR: 10.0.0.0/28
- Spoke1 vNet CIDR: 10.1.0.0/16, spoke1subnet CIDR: 10.1.0.0/24
- Spoke2 vNet CIDR: 10.2.0.0/16, spoke2subnet CIDR: 10.2.0.0/24

Important: 
* Subnet in Hub must be named [**GatewaySubnet**](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsub).
* Subnets in Spoke can be named something else as your preference.

Reference:
[How to create vNet and subnet](https://docs.microsoft.com/en-us/azure/virtual-network/quick-create-portal#create-a-virtual-network).
