# hub-spoke-without-nva
Step by step to create Azure Hub-Spoke network topology without NVA (Network Virtual Appliance)

## Situation:
Azure documentation provides some information about creating Hub-Spoke network topology where Spoke vNets (Virtual Networks) can connect to each other without creating NVA (Network Virtual Appliance such as Azure Firewall or 3rd party Firewall).

## Objective:
To provide clear step-by-step guide to successfully create Hub-Spoke network topology using VPN Gateway as inter-vNet router.

## Step-by-step setup:
1. Create the vNets and subnets, in this case I created 1 Hub vNet and 2 Spoke vNets. For simplicity, use the same Azure region for all vNets. I use Australia East region.
- myHub vNet CIDR: 10.0.0.0/16, GatewaySubnet CIDR: 10.0.0.0/27
- Spoke1 vNet CIDR: 10.1.0.0/16, spoke1subnet CIDR: 10.1.0.0/24
- Spoke2 vNet CIDR: 10.2.0.0/16, spoke2subnet CIDR: 10.2.0.0/24

Important: 
* Subnet in Hub must be named [**GatewaySubnet**](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsub).
* If GatewaySubnet CIDR uses /28, it only supports Basic SKU for VPN Gateway. For other SKU (zonal and AZ redundant), GatewaySubnet CIDR must use /27 or larger subnet.
* Subnets in Spoke can be named something else as your preference.

Reference:
[How to create vNet and subnet](https://docs.microsoft.com/en-us/azure/virtual-network/quick-create-portal#create-a-virtual-network).

2. I'm using Azure Network Manager (currently in public preview) to simplify vNet peering creation.

- Create Network Manager: name mynetworkmanager, region Australia East, scope mysubscription, features both (Connectivity and Security admin)
- From mynetworkmanager Network groups pane, create Network groups - name: myspoke
- From myspoke Overview pane, Define Dynamic Membership - Name contains Spoke
- From mynetworkmanager Configurations pane, create Connectivity configuration - name: myanmhubspoke, Topology: Hub and spoke, Hub: myHub, Spoke network groups: myspoke
- From myanmhubspoke Overview pane, Deploy

Azure Network Manager will create necessary peerings: myHub to Spoke1, myHub to Spoke2, Spoke1 to myHub, and Spoke2 to myHub.

3. Create Virtual Network Gateway.

- Name: myhubvpngateway, Region: Australia East, Gateway type: VPN, VPN type: Route based, SKU: VpnGw1, Virtual network: myHub
- 
