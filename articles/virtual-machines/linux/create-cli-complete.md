---
title: "Azure CLI 2.0에서 Linux 환경 만들기 | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 저장소, Linux VM, 가상 네트워크 및 서브넷, 부하 분산 장치, NIC, 공용 IP, 네트워크 보안 그룹을 모두 처음부터 새로 만듭니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: e5c4785428b2150e951923e98079e00808a82d87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="a722c-103">Azure CLI를 사용하여 완전한 Linux 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="a722c-103">Create a complete Linux virtual machine with the Azure CLI</span></span>
<span data-ttu-id="a722c-104">Azure에서 가상 컴퓨터(VM)를 신속하게 만들려면 기본 값을 사용하여 모든 필요한 지원 리소스를 생성하는 단일 Azure CLI 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-104">To quickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values to create any required supporting resources.</span></span> <span data-ttu-id="a722c-105">가상 네트워크, 공용 IP 주소 및 네트워크 보안 그룹 규칙 등의 리소스는 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="a722c-106">프로덕션 환경에서의 더 높은 제어를 위해 미리 이 리소스를 만들어 VM을 여기에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs to them.</span></span> <span data-ttu-id="a722c-107">이 문서에서는 VM을 만들고 지원 리소스를 하나씩 만드는 방법을 안내합니다. </span><span class="sxs-lookup"><span data-stu-id="a722c-107">This article guides you through how to create a VM and each of the supporting resources one by one.</span></span>

<span data-ttu-id="a722c-108">최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치했고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-108">Make sure that you have installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged to an Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="a722c-109">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-109">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="a722c-110">예제 매개 변수 이름에는 *myResourceGroup*, *myVnet*, *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="a722c-111">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="a722c-111">Create resource group</span></span>
<span data-ttu-id="a722c-112">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="a722c-113">리소스 그룹은 가상 컴퓨터와 지원하는 가상 네트워크 리소스에 앞서 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="a722c-114">[az group create](/cli/azure/group#create)을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-114">Create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="a722c-115">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="a722c-116">기본적으로 Azure CLI 명령의 출력은 JSON(JavaScript Object Notation)으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-116">By default, the output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="a722c-117">기본 출력을 목록이나 테이블로 변경하려면 [az configure --output](/cli/azure/#configure)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-117">To change the default output to a list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="a722c-118">출력 형식을 1번 변경하기 위해 명령에 `--output`을 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-118">You can also add `--output` to any command for a one time change in output format.</span></span> <span data-ttu-id="a722c-119">다음 예제에서는 `az group create` 명령에서의 JSON 출력을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-119">The following example shows the JSON output from the `az group create` command:</span></span>

```json                       
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "location": "eastus",
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="a722c-120">가상 네트워크 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="a722c-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="a722c-121">다음에는 Azure에서 실행되는 가상 네트워크와, VM을 만들 수 있는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-121">Next you create a virtual network in Azure and a subnet in to which you can create your VMs.</span></span> <span data-ttu-id="a722c-122">[az network vnet create](/cli/azure/network/vnet#create)를 사용하여 이름이 *myVnet*이고 주소 접두사가 *192.168.0.0/16*인 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-122">Use [az network vnet create](/cli/azure/network/vnet#create) to create a virtual network named *myVnet* with the *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="a722c-123">주소 접두사로 *192.168.1.0/24*를 사용하는 *mySubnet*이라는 서브넷도 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-123">You also add a subnet named *mySubnet* with the address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="a722c-124">출력에는 가상 네트워크 내에 논리적으로 만들어진 서브넷이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-124">The output shows the subnet as logically created inside the virtual network:</span></span>

```json
{
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "location": "eastus",
  "name": "myVnet",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "ed62fd03-e9de-430b-84df-8a3b87cacdbb",
  "subnets": [
    {
      "addressPrefix": "192.168.1.0/24",
      "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
      "ipConfigurations": null,
      "name": "mySubnet",
      "networkSecurityGroup": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  "tags": {},
  "type": "Microsoft.Network/virtualNetworks",
  "virtualNetworkPeerings": null
}
```


## <a name="create-a-public-ip-address"></a><span data-ttu-id="a722c-125">공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="a722c-125">Create a public IP address</span></span>
<span data-ttu-id="a722c-126">이제 [az network public-ip create](/cli/azure/network/public-ip#create)를 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="a722c-127">이 공용 IP 주소를 사용하면 인터넷에서 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-127">This public IP address enables you to connect to your VMs from the Internet.</span></span> <span data-ttu-id="a722c-128">기본 주소가 동적이므로 `--domain-name-label` 옵션으로 명명된 DNS 항목도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-128">Because the default address is dynamic, we also create a named DNS entry with the `--domain-name-label` option.</span></span> <span data-ttu-id="a722c-129">다음 예제는 *mypublicdns*라는 DNS 이름으로 *myPublicIP*라는 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-129">The following example creates a public IP named *myPublicIP* with the DNS name of *mypublicdns*.</span></span> <span data-ttu-id="a722c-130">DNS 이름은 고유해야 하므로 자체 DNS 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-130">Because the DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="a722c-131">출력:</span><span class="sxs-lookup"><span data-stu-id="a722c-131">Output:</span></span>

```json
{
  "publicIp": {
    "dnsSettings": {
      "domainNameLabel": "mypublicdns",
      "fqdn": "mypublicdns.eastus.cloudapp.azure.com",
      "reverseFqdn": null
    },
    "etag": "W/\"2632aa72-3d2d-4529-b38e-b622b4202925\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "idleTimeoutInMinutes": 4,
    "ipAddress": null,
    "ipConfiguration": null,
    "location": "eastus",
    "name": "myPublicIP",
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Dynamic",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "4c65de38-71f5-4684-be10-75e605b3e41f",
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses"
  }
}
```


## <a name="create-a-network-security-group"></a><span data-ttu-id="a722c-132">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="a722c-132">Create a network security group</span></span>
<span data-ttu-id="a722c-133">VM 내/외부 네트워크 트래픽의 흐름을 제어하기 위해 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-133">To control the flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="a722c-134">네트워크 보안 그룹은 NIC 또는 서브넷에 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-134">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="a722c-135">다음 예제에서는 [az network nsg create](/cli/azure/network/nsg#create)를 사용하여 *myNetworkSecurityGroup*이라는 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-135">The following example uses [az network nsg create](/cli/azure/network/nsg#create) to create a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="a722c-136">특정 트래픽을 허용하거나 거부하는 규칙을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-136">You define rules that allow or deny the specific traffic.</span></span> <span data-ttu-id="a722c-137">[az network nsg rule create](/cli/azure/network/nsg/rule#create)를 사용하여 포트 22에서 모든 인바운드 연결을 허용하는 네트워크 보안 그룹의 인바운드 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-137">To allow inbound connections on port 22 (to support SSH), create an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="a722c-138">다음 예제에서는 *myNetworkSecurityGroupRuleSSH*이라는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-138">The following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 22 \
    --access allow
```

<span data-ttu-id="a722c-139">포트 80에서 인바운드 연결을 허용하기 위해(웹 트래픽 지원) 다른 네트워크 보안 그룹 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-139">To allow inbound connections on port 80 (to support web traffic), add another network security group rule.</span></span> <span data-ttu-id="a722c-140">다음 예제에서는 *myNetworkSecurityGroupRuleHTTP*라는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-140">The following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleWeb \
    --protocol tcp \
    --priority 1001 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="a722c-141">[az network nsg show](/cli/azure/network/nsg#show)를 사용하여 네트워크 보안 그룹 및 규칙을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-141">Examine the network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="a722c-142">출력:</span><span class="sxs-lookup"><span data-stu-id="a722c-142">Output:</span></span>

```json
{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowAzureLoadBalancerInBou
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs to all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs to Internet",
      "destinationAddressPrefix": "Internet",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
  "location": "eastus",
  "name": "myNetworkSecurityGroup",
  "networkInterfaces": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "47a9964e-23a3-438a-a726-8d60ebbb1c3c",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "22",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleSSH",
      "name": "myNetworkSecurityGroupRuleSSH",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "80",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleWeb",
      "name": "myNetworkSecurityGroupRuleWeb",
      "priority": 1001,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "subnets": null,
  "tags": null,
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## <a name="create-a-virtual-nic"></a><span data-ttu-id="a722c-143">가상 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="a722c-143">Create a virtual NIC</span></span>
<span data-ttu-id="a722c-144">가상 네트워크 인터페이스 카드(NIC)는 사용할 때 규칙을 적용할 수 있으므로 프로그래밍 방식으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="a722c-145">2개 이상 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-145">You can also have more than one.</span></span> <span data-ttu-id="a722c-146">다음 [az network nic create](/cli/azure/network/nic#create) 명령에서 이름이 *myNic*인 NIC를 만들어 네트워크 보안 그룹과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-146">In the following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with the network security group.</span></span> <span data-ttu-id="a722c-147">공용 IP 주소 *myPublicIP*도 가상 NIC에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-147">The public IP address *myPublicIP* is also associated with the virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="a722c-148">출력:</span><span class="sxs-lookup"><span data-stu-id="a722c-148">Output:</span></span>

```json
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "brqlt10lvoxedgkeuomc4pm5tb.bx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": false,
    "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": null,
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "192.168.1.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "provisioningState": "Succeeded",
        "publicIpAddress": {
          "dnsSettings": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
          "idleTimeoutInMinutes": null,
          "ipAddress": null,
          "ipConfiguration": null,
          "location": null,
          "name": null,
          "provisioningState": null,
          "publicIpAddressVersion": null,
          "publicIpAllocationMethod": null,
          "resourceGroup": "myResourceGroup",
          "resourceGuid": null,
          "tags": null,
          "type": null
        },
        "resourceGroup": "myResourceGroup",
        "subnet": {
          "addressPrefix": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
          "ipConfigurations": null,
          "name": null,
          "networkSecurityGroup": null,
          "provisioningState": null,
          "resourceGroup": "myResourceGroup",
          "resourceNavigationLinks": null,
          "routeTable": null
        }
      }
    ],
    "location": "eastus",
    "macAddress": null,
    "name": "myNic",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "myResourceGroup",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "primary": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "b3dbaa0e-2cf2-43be-a814-5cc49fea3304",
    "tags": null,
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null
  }
}
```


## <a name="create-an-availability-set"></a><span data-ttu-id="a722c-149">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="a722c-149">Create an availability set</span></span>
<span data-ttu-id="a722c-150">가용성 집합은 장애 도메인 및 업데이트 도메인에 걸쳐 VM을 분산하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="a722c-151">당장은 하나의 VM만 만든다 하더라도 향후 확장하기 쉽게 가용성 집합을 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-151">Even though you only create one VM right now, it's best practice to use availability sets to make it easier to expand in the future.</span></span> 

<span data-ttu-id="a722c-152">장애 도메인은 공통의 전원 및 네트워크 스위치를 공유하는 가상 컴퓨터 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="a722c-153">기본적으로 가용성 집합 안에 구성된 가상 컴퓨터는 최대 3개의 장애 도메인에 분산되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-153">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="a722c-154">이러한 장애 도메인 중 하나에서 발생한 하드웨어 문제가 앱을 실행 중인 모든 VM에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="a722c-155">업데이트 도메인은 동시에 다시 부팅할 수 있는 가상 컴퓨터 그룹과 기본 물리적 하드웨어를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="a722c-156">계획된 유지 보수 중에 업데이트 도메인의 재부팅 순서는 순차적으로 진행되지 않을 수 있으며, 한 번에 하나의 업데이트 도메인만 재부팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-156">During planned maintenance, the order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="a722c-157">Azure는 가용성 집합에 VM을 배치할 때 VM을 전체 장애 및 업데이트 도메인에 자동으로 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-157">Azure automatically distributes VMs across the fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="a722c-158">자세한 내용은 [VM의 가용성 관리](manage-availability.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a722c-158">For more information, see [managing the availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="a722c-159">[az vm availability-set create](/cli/azure/vm/availability-set#create)를 사용하여 VM에 대한 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="a722c-160">다음 예제는 *myAvailabilitySet*이라는 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-160">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="a722c-161">출력에서 장애 도메인과 업데이트 도메인을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-161">The output notes fault domains and update domains:</span></span>

```json
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet",
  "location": "eastus",
  "managed": null,
  "name": "myAvailabilitySet",
  "platformFaultDomainCount": 2,
  "platformUpdateDomainCount": 5,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": null,
    "managed": true,
    "tier": null
  },
  "statuses": null,
  "tags": {},
  "type": "Microsoft.Compute/availabilitySets",
  "virtualMachines": []
}
```


## <a name="create-the-linux-vms"></a><span data-ttu-id="a722c-162">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="a722c-162">Create the Linux VMs</span></span>
<span data-ttu-id="a722c-163">인터넷에서 액세스 가능한 VM을 지원하기 위해 네트워크 리소스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-163">You've created the network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="a722c-164">이제 VM을 만들어 SSH 키로 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="a722c-165">이 예에서는 가장 최근의 LTS를 기반으로 Ubuntu VM을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-165">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="a722c-166">[Azure VM 이미지 찾기](cli-ps-findimage.md)에서 설명한 대로 [az vm image list](/cli/azure/vm/image#list)를 통해 추가적인 이미지를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="a722c-167">인증에 사용할 SSH 키도 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-167">We also specify an SSH key to use for authentication.</span></span> <span data-ttu-id="a722c-168">SSH 공개 키 쌍이 없는 경우 [만들거나 ](mac-create-ssh-keys.md) `--generate-ssh-keys` 매개 변수를 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use the `--generate-ssh-keys` parameter to create them for you.</span></span> <span data-ttu-id="a722c-169">키 쌍이 있으면 이 매개 변수는 `~/.ssh`의 기존 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="a722c-170">[az vm create](/cli/azure/vm#create) 명령으로 모든 리소스 및 정보를 결합하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-170">Create the VM by bringing all our resources and information together with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="a722c-171">다음 예제에서는 *myVM*이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-171">The following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --availability-set myAvailabilitySet \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="a722c-172">공용 IP 주소를 만들 때 제공한 DNS 항목이 있는 VM에 대한 SSH.</span><span class="sxs-lookup"><span data-stu-id="a722c-172">SSH to your VM with the DNS entry you provided when you created the public IP address.</span></span> <span data-ttu-id="a722c-173">이 `fqdn`은 VM을 만들 때 출력에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-173">This `fqdn` is shown in the output as you create your VM:</span></span>

```json
{
  "fqdns": "mypublicdns.eastus.cloudapp.azure.com",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-13-71-C8",
  "powerState": "VM running",
  "privateIpAddress": "192.168.1.5",
  "publicIpAddress": "13.90.94.252",
  "resourceGroup": "myResourceGroup"
}
```

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="a722c-174">출력:</span><span class="sxs-lookup"><span data-stu-id="a722c-174">Output:</span></span>

```bash
The authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

<span data-ttu-id="a722c-175">NGINX를 설치하고 VM에 대한 트래픽 흐름을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-175">You can install NGINX and see the traffic flow to the VM.</span></span> <span data-ttu-id="a722c-176">다음과 같이 NGINX를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="a722c-177">작동 중인 기본 NGINX 사이트를 확인하려면 웹 브라우저를 열고 FQDN을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-177">To see the default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![VM의 기본 NGINX 사이트](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="a722c-179">템플릿으로 내보내기</span><span class="sxs-lookup"><span data-stu-id="a722c-179">Export as a template</span></span>
<span data-ttu-id="a722c-180">동일한 매개 변수를 사용하여 추가 개발 환경을 만들려고 하거나 일치하는 프로덕션 환경을 만들려면 어떻게 해야 할까요?</span><span class="sxs-lookup"><span data-stu-id="a722c-180">What if you now want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="a722c-181">Resource Manager는 사용자 환경에 대한 모든 매개 변수를 정의하는 JSON 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-181">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="a722c-182">이 JSON 템플릿을 참조하여 전체 환경을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="a722c-183">[JSON 템플릿을 수동으로 빌드](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)하거나 기존 환경을 내보내 JSON 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you.</span></span> <span data-ttu-id="a722c-184">다음과 같이 [az group export](/cli/azure/group#export)를 사용하여 리소스 그룹을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-184">Use [az group export](/cli/azure/group#export) to export your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="a722c-185">이 명령을 실행하면 `myResourceGroup.json` 파일이 현재 작업 디렉터리에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-185">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="a722c-186">이 템플릿에서 환경을 만들면 모든 리소스 이름을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-186">When you create an environment from this template, you are prompted for all the resource names.</span></span> <span data-ttu-id="a722c-187">`az group export` 명령에 `--include-parameter-default-value` 매개 변수를 추가하여 템플릿 파일에 이러한 이름을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-187">You can populate these names in your template file by adding the `--include-parameter-default-value` parameter to the `az group export` command.</span></span> <span data-ttu-id="a722c-188">JSON 템플릿을 편집하여 리소스 이름을 지정하거나 리소스 이름을 지정하는 [parameters.json 파일을 만듭니다](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="a722c-188">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="a722c-189">템플릿에서 환경을 만들려면 다음과 같이 [az group deployment create](/cli/azure/group/deployment#create)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-189">To create an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="a722c-190">[템플릿에서 배포하는 방법에 대해 자세히 읽어볼 수 있습니다](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a722c-190">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="a722c-191">환경을 점진적으로 업데이트하고, 매개 변수 파일을 사용하고, 단일 저장소 위치에서 템플릿에 액세스하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-191">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a722c-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a722c-192">Next steps</span></span>
<span data-ttu-id="a722c-193">이제 여러 네트워킹 구성 요소 및 VM을 사용할 준비가 되셨습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-193">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="a722c-194">이 샘플 환경에 사용하여 여기에 소개된 핵심 구성 요소로 응용 프로그램을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a722c-194">You can use this sample environment to build out your application by using the core components introduced here.</span></span>
