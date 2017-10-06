---
title: "aaaCreate Azure CLI 2.0 hello로 Linux 환경 | Microsoft Docs"
description: "Hello Azure CLI 2.0을 사용 하 여 접지 hello 모두에서 저장소, Linux VM, 가상 네트워크 및 서브넷, 부하 분산 장치, NIC를, 공용 IP 및 네트워크 보안 그룹을 만듭니다."
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
ms.openlocfilehash: 7287ea178e76001b84dade628ead04a59dc27f40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="d5109-103">Hello Azure CLI가 있는 완벽 한 Linux 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="d5109-103">Create a complete Linux virtual machine with hello Azure CLI</span></span>
<span data-ttu-id="d5109-104">모든 필수 리소스를 지 원하는 기본 값 toocreate를 사용 하는 단일 Azure CLI 명령을 사용할 수 있습니다, tooquickly Azure에서 가상 컴퓨터 (VM)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-104">tooquickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values toocreate any required supporting resources.</span></span> <span data-ttu-id="d5109-105">가상 네트워크, 공용 IP 주소 및 네트워크 보안 그룹 규칙 등의 리소스는 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="d5109-106">프로덕션 환경에서 사용자 환경의 자세한 컨트롤에 대 한 사용, 이러한 리소스 보다 앞선 시간을 만들고 Vm toothem 추가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs toothem.</span></span> <span data-ttu-id="d5109-107">이 문서 어떻게 toocreate VM 및 각 hello 하나씩 지원 리소스에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-107">This article guides you through how toocreate a VM and each of hello supporting resources one by one.</span></span>

<span data-ttu-id="d5109-108">Hello 최신 설치 되어 있는지 확인 [Azure CLI 2.0](/cli/azure/install-az-cli2) 에 있는 계정입니다. 기록 된 tooan Azure 및 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-108">Make sure that you have installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged tooan Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="d5109-109">Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-109">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="d5109-110">예제 매개 변수 이름에는 *myResourceGroup*, *myVnet*, *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="d5109-111">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="d5109-111">Create resource group</span></span>
<span data-ttu-id="d5109-112">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="d5109-113">리소스 그룹은 가상 컴퓨터와 지원하는 가상 네트워크 리소스에 앞서 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="d5109-114">Hello 리소스 그룹을 만들 [az 그룹 만들기](/cli/azure/group#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-114">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d5109-115">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치:</span><span class="sxs-lookup"><span data-stu-id="d5109-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="d5109-116">기본적으로 Azure CLI 명령을 hello 출력은 JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="d5109-116">By default, hello output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="d5109-117">예를 들어 사용 toochange hello 기본 출력 tooa 목록 또는 테이블을 [az 구성-출력](/cli/azure/#configure)합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-117">toochange hello default output tooa list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="d5109-118">추가할 수도 있습니다 `--output` tooany 명령을 한 번에 대 한 출력 형식으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-118">You can also add `--output` tooany command for a one time change in output format.</span></span> <span data-ttu-id="d5109-119">hello 다음 예제에서는 hello JSON 출력을에서 보여 줍니다 hello `az group create` 명령:</span><span class="sxs-lookup"><span data-stu-id="d5109-119">hello following example shows hello JSON output from hello `az group create` command:</span></span>

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

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="d5109-120">가상 네트워크 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="d5109-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="d5109-121">그런 다음 Azure에서 가상 네트워크를 만드는 경우 및 toowhich의 서브넷을 Vm을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-121">Next you create a virtual network in Azure and a subnet in toowhich you can create your VMs.</span></span> <span data-ttu-id="d5109-122">사용 하 여 [az 네트워크 vnet 만들기](/cli/azure/network/vnet#create) toocreate 이라는 가상 네트워크 *myVnet* hello로 *192.168.0.0/16* 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-122">Use [az network vnet create](/cli/azure/network/vnet#create) toocreate a virtual network named *myVnet* with hello *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="d5109-123">이라는 서브넷을 추가할 수도 *mySubnet* hello 주소 접두사와 *192.168.1.0/24*:</span><span class="sxs-lookup"><span data-stu-id="d5109-123">You also add a subnet named *mySubnet* with hello address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="d5109-124">hello 출력 hello 서브넷을 hello 가상 네트워크 내에 만들어진 논리적으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-124">hello output shows hello subnet as logically created inside hello virtual network:</span></span>

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


## <a name="create-a-public-ip-address"></a><span data-ttu-id="d5109-125">공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="d5109-125">Create a public IP address</span></span>
<span data-ttu-id="d5109-126">이제 [az network public-ip create](/cli/azure/network/public-ip#create)를 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="d5109-127">이 공용 IP 주소가 있습니다 tooconnect tooyour를 Vm hello 인터넷에서에서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-127">This public IP address enables you tooconnect tooyour VMs from hello Internet.</span></span> <span data-ttu-id="d5109-128">Hello로 명명 된 DNS 항목 hello 기본 주소는 동적도 생성 `--domain-name-label` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-128">Because hello default address is dynamic, we also create a named DNS entry with hello `--domain-name-label` option.</span></span> <span data-ttu-id="d5109-129">hello 다음 예제에서는 명명 된 공용 IP *myPublicIP* 의 hello DNS 이름을 가진 *mypublicdns*합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-129">hello following example creates a public IP named *myPublicIP* with hello DNS name of *mypublicdns*.</span></span> <span data-ttu-id="d5109-130">Hello DNS 이름은 고유 해야 하기 때문에 고유한 DNS 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-130">Because hello DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="d5109-131">출력:</span><span class="sxs-lookup"><span data-stu-id="d5109-131">Output:</span></span>

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


## <a name="create-a-network-security-group"></a><span data-ttu-id="d5109-132">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="d5109-132">Create a network security group</span></span>
<span data-ttu-id="d5109-133">toocontrol hello 트래픽 흐름을 Vm에 내부 및 외부 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-133">toocontrol hello flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="d5109-134">네트워크 보안 그룹에 적용 된 tooa NIC 또는 서브넷 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-134">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="d5109-135">hello 다음 예제에서는 [az 네트워크 nsg 만들기](/cli/azure/network/nsg#create) 네트워크 보안 그룹 이라는 toocreate *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="d5109-135">hello following example uses [az network nsg create](/cli/azure/network/nsg#create) toocreate a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="d5109-136">Hello 특정 트래픽을 허용 하거나 거부 하는 규칙을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-136">You define rules that allow or deny hello specific traffic.</span></span> <span data-ttu-id="d5109-137">tooallow 22 (toosupport SSH) 포트에서 인바운드 연결 네트워크 보안 그룹을 hello에 대 한 인바운드 규칙을 만듭니다 [az 네트워크 nsg 규칙 만들기](/cli/azure/network/nsg/rule#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-137">tooallow inbound connections on port 22 (toosupport SSH), create an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="d5109-138">hello 다음 규칙을 만드는 예제는 명명 된 *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="d5109-138">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

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

<span data-ttu-id="d5109-139">tooallow 다른 네트워크 보안 그룹 규칙을 추가 하는 포트 80 (toosupport 웹 트래픽)에 대 한 인바운드 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-139">tooallow inbound connections on port 80 (toosupport web traffic), add another network security group rule.</span></span> <span data-ttu-id="d5109-140">hello 다음 규칙을 만드는 예제는 명명 된 *myNetworkSecurityGroupRuleHTTP*:</span><span class="sxs-lookup"><span data-stu-id="d5109-140">hello following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

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

<span data-ttu-id="d5109-141">Hello 네트워크 보안 그룹 및 규칙을 검사 하 여 [az 네트워크 nsg 쇼](/cli/azure/network/nsg#show):</span><span class="sxs-lookup"><span data-stu-id="d5109-141">Examine hello network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="d5109-142">출력:</span><span class="sxs-lookup"><span data-stu-id="d5109-142">Output:</span></span>

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
      "description": "Allow outbound traffic from all VMs tooall VMs in VNET",
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
      "description": "Allow outbound traffic from all VMs tooInternet",
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

## <a name="create-a-virtual-nic"></a><span data-ttu-id="d5109-143">가상 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="d5109-143">Create a virtual NIC</span></span>
<span data-ttu-id="d5109-144">가상 네트워크 인터페이스 카드 (Nic)은 tootheir 사용 규칙을 적용할 수 있으므로 프로그래밍 방식으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="d5109-145">2개 이상 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-145">You can also have more than one.</span></span> <span data-ttu-id="d5109-146">Hello 다음과에서 [az 네트워크 nic 만들](/cli/azure/network/nic#create) 명령, 명명 된 NIC를 만들고 *myNic* hello 네트워크 보안 그룹에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-146">In hello following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with hello network security group.</span></span> <span data-ttu-id="d5109-147">공용 IP 주소를 hello *myPublicIP* hello 가상 NIC.과 관련 되어</span><span class="sxs-lookup"><span data-stu-id="d5109-147">hello public IP address *myPublicIP* is also associated with hello virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="d5109-148">출력:</span><span class="sxs-lookup"><span data-stu-id="d5109-148">Output:</span></span>

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


## <a name="create-an-availability-set"></a><span data-ttu-id="d5109-149">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="d5109-149">Create an availability set</span></span>
<span data-ttu-id="d5109-150">가용성 집합은 장애 도메인 및 업데이트 도메인에 걸쳐 VM을 분산하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="d5109-151">모범 사례 toouse 가용성 집합 toomake는만 하나의 VM 지금 바로 만들 경우에 해당 hello 향후에 더 쉽게 tooexpand 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-151">Even though you only create one VM right now, it's best practice toouse availability sets toomake it easier tooexpand in hello future.</span></span> 

<span data-ttu-id="d5109-152">장애 도메인은 공통의 전원 및 네트워크 스위치를 공유하는 가상 컴퓨터 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="d5109-153">기본적으로 가용성 집합 내에서 구성 된 가상 컴퓨터를 hello toothree 오류 도메인을 걸쳐 분리 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-153">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="d5109-154">이러한 장애 도메인 중 하나에서 발생한 하드웨어 문제가 앱을 실행 중인 모든 VM에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="d5109-155">업데이트 도메인 hello에서 다시 부팅 해야 하는 기본 실제 하드웨어와 가상 컴퓨터 그룹을 나타내는 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="d5109-156">계획 된 유지 관리 하는 동안 업데이트 도메인 재부팅 됩니다 hello 순서 순차적, 않을 수 있지만 한 번에 하나의 업데이트 도메인을 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-156">During planned maintenance, hello order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="d5109-157">Azure 자동으로 Vm hello 장애 도메인과 업데이트 도메인에 걸쳐 때 배포 가용성 집합에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-157">Azure automatically distributes VMs across hello fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="d5109-158">자세한 내용은 참조 [Vm의 가용성을 hello 관리](manage-availability.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-158">For more information, see [managing hello availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="d5109-159">[az vm availability-set create](/cli/azure/vm/availability-set#create)를 사용하여 VM에 대한 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="d5109-160">hello 다음 예제에서는 가용성 명명 된 집합 *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="d5109-160">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="d5109-161">출력 메모 오류 도메인 hello 하 고 도메인을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-161">hello output notes fault domains and update domains:</span></span>

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


## <a name="create-hello-linux-vms"></a><span data-ttu-id="d5109-162">Hello Linux Vm 만들기</span><span class="sxs-lookup"><span data-stu-id="d5109-162">Create hello Linux VMs</span></span>
<span data-ttu-id="d5109-163">Hello 네트워크 리소스 toosupport를 인터넷에서 액세스할 수 있는 Vm 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-163">You've created hello network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="d5109-164">이제 VM을 만들어 SSH 키로 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="d5109-165">이 예에서 여기 toocreate Ubuntu VM hello에 따라 가장 최근의 LTS 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-165">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="d5109-166">[Azure VM 이미지 찾기](cli-ps-findimage.md)에서 설명한 대로 [az vm image list](/cli/azure/vm/image#list)를 통해 추가적인 이미지를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="d5109-167">또한 인증을 위해 SSH 키 toouse를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-167">We also specify an SSH key toouse for authentication.</span></span> <span data-ttu-id="d5109-168">SSH 공개 키 쌍이 없는 경우 다음을 할 수 있습니다 [만들](mac-create-ssh-keys.md) hello를 사용 하 여 또는 `--generate-ssh-keys` 매개 변수 toocreate ç 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use hello `--generate-ssh-keys` parameter toocreate them for you.</span></span> <span data-ttu-id="d5109-169">키 쌍이 있으면 이 매개 변수는 `~/.ssh`의 기존 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="d5109-170">모든 리소스와 정보를 hello 함께 전환 하 여 hello VM 만들기 [az vm 만들기](/cli/azure/vm#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-170">Create hello VM by bringing all our resources and information together with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="d5109-171">hello 다음 예제에서는 V *myVM*:</span><span class="sxs-lookup"><span data-stu-id="d5109-171">hello following example creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="d5109-172">Hello 공용 IP 주소를 만들 때 제공한 DNS 항목 hello로 SSH tooyour VM입니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-172">SSH tooyour VM with hello DNS entry you provided when you created hello public IP address.</span></span> <span data-ttu-id="d5109-173">이 `fqdn` VM을 만드는 것 만큼 hello 출력에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-173">This `fqdn` is shown in hello output as you create your VM:</span></span>

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

<span data-ttu-id="d5109-174">출력:</span><span class="sxs-lookup"><span data-stu-id="d5109-174">Output:</span></span>

```bash
hello authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

toorun a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

<span data-ttu-id="d5109-175">NGINX를 설치 하 고 hello 트래픽 흐름 toohello VM을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-175">You can install NGINX and see hello traffic flow toohello VM.</span></span> <span data-ttu-id="d5109-176">다음과 같이 NGINX를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="d5109-177">toosee hello 기본 NGINX 사이트 작업에서 웹 브라우저를 열고에 FQDN을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-177">toosee hello default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![VM의 기본 NGINX 사이트](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="d5109-179">템플릿으로 내보내기</span><span class="sxs-lookup"><span data-stu-id="d5109-179">Export as a template</span></span>
<span data-ttu-id="d5109-180">이제 toocreate hello로 추가 개발 환경을 원하는 경우 동일한 매개 변수 또는 일치 하는 프로덕션 환경?</span><span class="sxs-lookup"><span data-stu-id="d5109-180">What if you now want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="d5109-181">리소스 관리자는 사용자 환경에 대 한 모든 hello 매개 변수를 정의 하는 JSON 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-181">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="d5109-182">이 JSON 템플릿을 참조하여 전체 환경을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="d5109-183">할 수 있습니다 [JSON 서식 파일을 수동으로 빌드할](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 기존 환경 toocreate hello JSON 템플릿을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you.</span></span> <span data-ttu-id="d5109-184">사용 하 여 [az 그룹 내보내기](/cli/azure/group#export) tooexport 리소스 그룹 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-184">Use [az group export](/cli/azure/group#export) tooexport your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="d5109-185">이 명령은 만듭니다 hello `myResourceGroup.json` 현재 작업 디렉터리에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-185">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="d5109-186">이 템플릿에서 환경을 만들 때 모든 hello 리소스 이름을 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-186">When you create an environment from this template, you are prompted for all hello resource names.</span></span> <span data-ttu-id="d5109-187">Hello를 추가 하 여 템플릿 파일에 이러한 이름을 채울 수 있습니다 `--include-parameter-default-value` 매개 변수 toohello `az group export` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-187">You can populate these names in your template file by adding hello `--include-parameter-default-value` parameter toohello `az group export` command.</span></span> <span data-ttu-id="d5109-188">JSON 템플릿 toospecify hello 리소스 이름의 편집 또는 [parameters.json 파일을 만들](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello 리소스 이름을 지정 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-188">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="d5109-189">서식 파일을 사용 하 여 환경 toocreate [az 그룹 배포 만들기](/cli/azure/group/deployment#create) 다음과 같습니다:</span><span class="sxs-lookup"><span data-stu-id="d5109-189">toocreate an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="d5109-190">Tooread 경우가 [방법에 대 한 자세한 템플릿에서 toodeploy](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-190">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d5109-191">Tooincrementally 업데이트 환경 hello 매개 변수 파일을 사용 하 고 단일 저장소 위치에서 서식 파일에 액세스 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-191">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5109-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d5109-192">Next steps</span></span>
<span data-ttu-id="d5109-193">이제 준비 toobegin 여러 네트워킹 구성 요소 및 Vm을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-193">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="d5109-194">여기 도입 hello 핵심 구성 요소를 사용 하 여이 샘플 환경 toobuild 응용 프로그램에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5109-194">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
