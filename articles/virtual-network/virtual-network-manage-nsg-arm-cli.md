---
title: "네트워크 보안 그룹 관리 - Azure CLI 2.0 | Microsoft Docs"
description: "Azure CLI(명령줄 인터페이스) 2.0을 사용하여 네트워크 보안 그룹을 관리하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed17d314-07e6-4c7f-bcf1-a8a2535d7c14
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 11ec0d3d9e33c06d4c0a164f7fba5dd5cca73872
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-the-azure-cli-20"></a><span data-ttu-id="83fb8-103">Azure CLI 2.0을 사용하여 네트워크 보안 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="83fb8-103">Manage network security groups using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="83fb8-104">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="83fb8-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="83fb8-105">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="83fb8-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) - 클래식 및 리소스 관리 배포 모델용 CLI</span><span class="sxs-lookup"><span data-stu-id="83fb8-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="83fb8-107">[Azure CLI 2.0](#View-existing-NSGs) - 리소스 관리 배포 모델용 차세대 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="83fb8-107">[Azure CLI 2.0](#View-existing-NSGs) - our next generation CLI for the resource management deployment model (this article)</span></span>


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="83fb8-108">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="83fb8-109">이 문서에서는 Resource Manager 배포 모델 사용을 설명하며 Microsoft에서는 대부분의 새로운 배포에 대해 클래식 배포 모델 대신 이 모델을 사용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a><span data-ttu-id="83fb8-110">필수 요소</span><span class="sxs-lookup"><span data-stu-id="83fb8-110">Prerequisite</span></span>
<span data-ttu-id="83fb8-111">아직 설치하지 않은 경우 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치 및 구성하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-111">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 


## <a name="view-existing-nsgs"></a><span data-ttu-id="83fb8-112">기존 NSG 보기</span><span class="sxs-lookup"><span data-stu-id="83fb8-112">View existing NSGs</span></span>
<span data-ttu-id="83fb8-113">특정 리소스 그룹에서 NSG 목록을 보려면 `-o table` 출력 형식으로 [az network nsg list](/cli/azure/network/nsg#list) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-113">To view the list of NSGs in a specific resource group, run the [az network nsg list](/cli/azure/network/nsg#list) command with a `-o table` output format:</span></span>

```azurecli
az network nsg list -g RG-NSG -o table
```

<span data-ttu-id="83fb8-114">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="83fb8-114">Expected output:</span></span>

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="83fb8-115">NSG에 대한 모든 규칙 나열</span><span class="sxs-lookup"><span data-stu-id="83fb8-115">List all rules for an NSG</span></span>
<span data-ttu-id="83fb8-116">**NSG-FrontEnd**라는 NSG 규칙을 보려면 [JMESPATH 쿼리 필터](/cli/azure/query-az-cli2) 및 `-o table` 출력 형식을 사용하여 [az network nsg show](/cli/azure/network/nsg#show) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-116">To view the rules of an NSG named **NSG-FrontEnd**, run the [az network nsg show](/cli/azure/network/nsg#show) command using a [JMESPATH query filter](/cli/azure/query-az-cli2) and the `-o table` output format:</span></span>

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

<span data-ttu-id="83fb8-117">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="83fb8-117">Expected output:</span></span>

    Name                           Desc                                                    Access    Direction    DestPortRange    DestAddrPrefix    SrcPortRange    SrcAddrPrefix
    -----------------------------  ------------------------------------------------------  --------  -----------  ---------------  ----------------  --------------  -----------------
    AllowVnetInBound               Allow inbound traffic from all VMs in VNET              Allow     Inbound      *                VirtualNetwork    *               VirtualNetwork
    AllowAzureLoadBalancerInBound  Allow inbound traffic from azure load balancer          Allow     Inbound      *                *                 *               AzureLoadBalancer
    DenyAllInBound                 Deny all inbound traffic                                Deny      Inbound      *                *                 *               *
    AllowVnetOutBound              Allow outbound traffic from all VMs to all VMs in VNET  Allow     Outbound     *                VirtualNetwork    *               VirtualNetwork
    AllowInternetOutBound          Allow outbound traffic from all VMs to Internet         Allow     Outbound     *                Internet          *               *
    DenyAllOutBound                Deny all outbound traffic                               Deny      Outbound     *                *                 *               *
    rdp-rule                                                                               Allow     Inbound      3389             *                 *               Internet
    web-rule                                                                               Allow     Inbound      80               *                 *               Internet
> [!NOTE]
> <span data-ttu-id="83fb8-118">[az network nsg rule list](/cli/azure/network/nsg/rule#list)를 사용하여 NSG에서 사용자 지정 규칙을 나열할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-118">You can also use [az network nsg rule list](/cli/azure/network/nsg/rule#list) to list only the custom rules from an NSG .</span></span>
>

## <a name="view-nsg-associations"></a><span data-ttu-id="83fb8-119">NSG 연결 보기</span><span class="sxs-lookup"><span data-stu-id="83fb8-119">View NSG associations</span></span>

<span data-ttu-id="83fb8-120">**NSG-FrontEnd** NSG가 연결된 리소스를 보려면 아래와 같이 `az network nsg show` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-120">To view what resources the **NSG-FrontEnd** NSG is associate with, run the `az network nsg show` command as shown below.</span></span> 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

<span data-ttu-id="83fb8-121">아래와 같이 **NetworkInterfaces** 및 **서브넷** 속성을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-121">Look for the **networkInterfaces** and **subnets** properties as shown below:</span></span>

```json
[
  [
    {
      "addressPrefix": null,
      "etag": null,
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
      "ipConfigurations": null,
      "name": null,
      "networkSecurityGroup": null,
      "provisioningState": null,
      "resourceGroup": "RG-NSG",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  null
]
```

<span data-ttu-id="83fb8-122">위의 예에서 NSG는 NIC(네트워크 인터페이스)에 연결되지 않고 **FrontEnd**라는 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-122">In the example above, the NSG is not associated to any network interfaces (NICs), and it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="add-a-rule"></a><span data-ttu-id="83fb8-123">규칙 추가</span><span class="sxs-lookup"><span data-stu-id="83fb8-123">Add a rule</span></span>
<span data-ttu-id="83fb8-124">컴퓨터에서 **NSG-FrontEnd** NSG에 포트 **443**에 대한 **인바운드** 트래픽을 허용하는 규칙을 추가하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-124">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, enter the following command:</span></span>

```azurecli
az network nsg rule create  \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd  \
--name allow-https \
--description "Allow access to port 443 for HTTPS" \
--access Allow \
--protocol Tcp  \
--direction Inbound \
--priority 102 \
--source-address-prefix "*"  \
--source-port-range "*"  \
--destination-address-prefix "*" \
--destination-port-range "443"
```

<span data-ttu-id="83fb8-125">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="83fb8-125">Expected output:</span></span>

```json
{
  "access": "Allow",
  "description": "Allow access to port 443 for HTTPS",
  "destinationAddressPrefix": "*",
  "destinationPortRange": "443",
  "direction": "Inbound",
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
  "name": "allow-https",
  "priority": 102,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

## <a name="change-a-rule"></a><span data-ttu-id="83fb8-126">규칙 변경</span><span class="sxs-lookup"><span data-stu-id="83fb8-126">Change a rule</span></span>
<span data-ttu-id="83fb8-127">**인터넷**에서만 인바운드 트래픽을 허용하도록 위에서 만든 규칙을 변경하려면 [az network nsg rule update](/cli/azure/network/nsg/rule#update) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-127">To change the rule created above to allow inbound traffic from the **Internet** only, run the [az network nsg rule update](/cli/azure/network/nsg/rule#update) command:</span></span>

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

<span data-ttu-id="83fb8-128">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="83fb8-128">Expected output:</span></span>

```json
{
"access": "Allow",
"description": "Allow access to port 443 for HTTPS",
"destinationAddressPrefix": "*",
"destinationPortRange": "443",
"direction": "Inbound",
"etag": "W/\"<guid>\"",
"id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
"name": "allow-https",
"priority": 102,
"protocol": "Tcp",
"provisioningState": "Succeeded",
"resourceGroup": "RG-NSG",
"sourceAddressPrefix": "Internet",
"sourcePortRange": "*"
}
```

## <a name="delete-a-rule"></a><span data-ttu-id="83fb8-129">규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="83fb8-129">Delete a rule</span></span>
<span data-ttu-id="83fb8-130">위에서 만든 규칙을 삭제하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-130">To delete the rule created above, run the following command:</span></span>

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="83fb8-131">NIC에 NSG 연결</span><span class="sxs-lookup"><span data-stu-id="83fb8-131">Associate an NSG to a NIC</span></span>
<span data-ttu-id="83fb8-132">**NSG-FrontEnd** NSG를 **TestNICWeb1** NIC에 연결하려면 [az network nic update](/cli/azure/network/nic#update) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-132">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, use the [az network nic update](/cli/azure/network/nic#update) command:</span></span>

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

<span data-ttu-id="83fb8-133">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="83fb8-133">Expected output:</span></span>

```json
{
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": [],
    "internalDnsNameLabel": null,
    "internalDomainNameSuffix": "k0wkaguidnqrh0ud.gx.internal.cloudapp.net",
    "internalFqdn": null
  },
  "enableAcceleratedNetworking": false,
  "enableIpForwarding": false,
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1",
  "ipConfigurations": [
    {
      "applicationGatewayBackendAddressPools": null,
      "etag": "W/\"<guid>\"",
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1",
      "loadBalancerBackendAddressPools": null,
      "loadBalancerInboundNatRules": null,
      "name": "ipconfig1",
      "primary": true,
      "privateIpAddress": "192.168.1.6",
      "privateIpAddressVersion": "IPv4",
      "privateIpAllocationMethod": "Static",
      "provisioningState": "Succeeded",
      "publicIpAddress": null,
      "resourceGroup": "RG-NSG",
      "subnet": {
        "addressPrefix": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
        "ipConfigurations": null,
        "name": null,
        "networkSecurityGroup": null,
        "provisioningState": null,
        "resourceGroup": "RG-NSG",
        "resourceNavigationLinks": null,
        "routeTable": null
      }
    }
  ],
  "location": "centralus",
  "macAddress": "00-0D-3A-91-A9-60",
  "name": "TestNICWeb1",
  "networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  },
  "primary": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "resourceGuid": "<guid>",
  "tags": {},
  "type": "Microsoft.Network/networkInterfaces",
  "virtualMachine": null
}
```

## <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="83fb8-134">NIC에서 NSG 분리</span><span class="sxs-lookup"><span data-stu-id="83fb8-134">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="83fb8-135">**TestNICWeb1** NIC에서 **NSG-FrontEnd** NSG의 연결을 해제하려면 [az network nsg rule update](/cli/azure/network/nsg/rule#update) 명령을 다시 실행하고 `--network-security-group` 인수를 빈 문자열(`""`)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-135">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, run the [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace the `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

<span data-ttu-id="83fb8-136">출력에서 `networkSecurityGroup` 키는 null로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-136">In the output, the `networkSecurityGroup` key is set to null.</span></span>

## <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="83fb8-137">서브넷에서 NSG 분리</span><span class="sxs-lookup"><span data-stu-id="83fb8-137">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="83fb8-138">**FrontEnd** 서브넷에서 **NSG-FrontEnd** NSG의 연결을 해제하려면 [az network nsg rule update](/cli/azure/network/nsg/rule#update) 명령을 다시 실행하고 `--network-security-group` 인수를 빈 문자열(`""`)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-138">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, again run the [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace the `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

<span data-ttu-id="83fb8-139">출력에서 `networkSecurityGroup` 키는 null로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-139">In the output, the `networkSecurityGroup` key is set to null.</span></span>

## <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="83fb8-140">서브넷에 NSG 연결</span><span class="sxs-lookup"><span data-stu-id="83fb8-140">Associate an NSG to a subnet</span></span>
<span data-ttu-id="83fb8-141">**NSG-FrontEnd** NSG를 **FrontEnd** 서브넷에 다시 연결하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-141">To associate the **NSG-FrontEnd** NSG to the **FrontEnd** subnet again, run the following command:</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

<span data-ttu-id="83fb8-142">출력에서 `networkSecurityGroup` 키는 다음 값에 유사한 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-142">In the output, the `networkSecurityGroup` key has something similar for the value:</span></span>

```json
"networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  }
  ```

## <a name="delete-an-nsg"></a><span data-ttu-id="83fb8-143">NSG 삭제</span><span class="sxs-lookup"><span data-stu-id="83fb8-143">Delete an NSG</span></span>
<span data-ttu-id="83fb8-144">리소스에 연결되지 않은 경우 NSG를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-144">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="83fb8-145">NSG를 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-145">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="83fb8-146">NSG에 연결된 리소스를 확인하려면 [NSG 연결 보기](#View-NSGs-associations)에서처럼 `azure network nsg show`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-146">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="83fb8-147">NSG가 NIC에 연결된 경우 각 NIC에 대한 [NIC에서 NSG 분리](#Dissociate-an-NSG-from-a-NIC)에서처럼 `azure network nic set`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-147">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="83fb8-148">NSG가 서브넷에 연결된 경우 각 서브넷에 대한 [서브넷에서 NSG 분리](#Dissociate-an-NSG-from-a-subnet)에서처럼 `azure network vnet subnet set`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-148">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="83fb8-149">NSG를 삭제하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="83fb8-149">To delete the NSG, run the following command:</span></span>

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a><span data-ttu-id="83fb8-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="83fb8-150">Next steps</span></span>
* <span data-ttu-id="83fb8-151">[로깅을 사용합니다](virtual-network-nsg-manage-log.md) .</span><span class="sxs-lookup"><span data-stu-id="83fb8-151">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

