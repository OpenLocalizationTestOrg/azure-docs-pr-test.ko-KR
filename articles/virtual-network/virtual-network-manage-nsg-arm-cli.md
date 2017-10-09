---
title: "aaaManage 네트워크 보안 그룹-Azure CLI 2.0 | Microsoft Docs"
description: "Toomanage 네트워크 보안 그룹을 사용 하 여 Azure CLI (명령줄 인터페이스) 2.0 hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: a3036b465e1e4049cba00e5e13ce1b479a2301d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="cfc63-103">Hello Azure CLI 2.0을 사용 하 여 네트워크 보안 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="cfc63-103">Manage network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="cfc63-104">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="cfc63-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="cfc63-105">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="cfc63-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – hello 클래식 및 리소스 관리 배포 모델에 대 한 우리의 CLI</span><span class="sxs-lookup"><span data-stu-id="cfc63-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="cfc63-107">[Azure CLI 2.0](#View-existing-NSGs) -우리의 차세대 CLI hello 리소스 관리 배포 모델 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="cfc63-107">[Azure CLI 2.0](#View-existing-NSGs) - our next generation CLI for hello resource management deployment model (this article)</span></span>


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="cfc63-108">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cfc63-109">이 문서에서는 Microsoft hello 클래식 배포 모델 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a><span data-ttu-id="cfc63-110">필수 요소</span><span class="sxs-lookup"><span data-stu-id="cfc63-110">Prerequisite</span></span>
<span data-ttu-id="cfc63-111">하지 않은 아직 설치 하 고 최신 hello 구성 [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 


## <a name="view-existing-nsgs"></a><span data-ttu-id="cfc63-112">기존 NSG 보기</span><span class="sxs-lookup"><span data-stu-id="cfc63-112">View existing NSGs</span></span>
<span data-ttu-id="cfc63-113">Nsg hello 실행은 특정 리소스 그룹의 tooview hello 목록 [az 네트워크 nsg 목록](/cli/azure/network/nsg#list) 명령에 `-o table` 출력 형식:</span><span class="sxs-lookup"><span data-stu-id="cfc63-113">tooview hello list of NSGs in a specific resource group, run hello [az network nsg list](/cli/azure/network/nsg#list) command with a `-o table` output format:</span></span>

```azurecli
az network nsg list -g RG-NSG -o table
```

<span data-ttu-id="cfc63-114">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="cfc63-114">Expected output:</span></span>

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="cfc63-115">NSG에 대한 모든 규칙 나열</span><span class="sxs-lookup"><span data-stu-id="cfc63-115">List all rules for an NSG</span></span>
<span data-ttu-id="cfc63-116">명명 된 NSG의 tooview hello 규칙 **NSG 프런트 엔드**실행 hello [az 네트워크 nsg 표시](/cli/azure/network/nsg#show) 명령을 사용 하는 [JMESPATH 쿼리 필터](/cli/azure/query-az-cli2) 및 hello `-o table` 출력 형식:</span><span class="sxs-lookup"><span data-stu-id="cfc63-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello [az network nsg show](/cli/azure/network/nsg#show) command using a [JMESPATH query filter](/cli/azure/query-az-cli2) and hello `-o table` output format:</span></span>

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

<span data-ttu-id="cfc63-117">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="cfc63-117">Expected output:</span></span>

    Name                           Desc                                                    Access    Direction    DestPortRange    DestAddrPrefix    SrcPortRange    SrcAddrPrefix
    -----------------------------  ------------------------------------------------------  --------  -----------  ---------------  ----------------  --------------  -----------------
    AllowVnetInBound               Allow inbound traffic from all VMs in VNET              Allow     Inbound      *                VirtualNetwork    *               VirtualNetwork
    AllowAzureLoadBalancerInBound  Allow inbound traffic from azure load balancer          Allow     Inbound      *                *                 *               AzureLoadBalancer
    DenyAllInBound                 Deny all inbound traffic                                Deny      Inbound      *                *                 *               *
    AllowVnetOutBound              Allow outbound traffic from all VMs tooall VMs in VNET  Allow     Outbound     *                VirtualNetwork    *               VirtualNetwork
    AllowInternetOutBound          Allow outbound traffic from all VMs tooInternet         Allow     Outbound     *                Internet          *               *
    DenyAllOutBound                Deny all outbound traffic                               Deny      Outbound     *                *                 *               *
    rdp-rule                                                                               Allow     Inbound      3389             *                 *               Internet
    web-rule                                                                               Allow     Inbound      80               *                 *               Internet
> [!NOTE]
> <span data-ttu-id="cfc63-118">사용할 수도 있습니다 [az 네트워크 nsg 규칙 목록](/cli/azure/network/nsg/rule#list) NSG에서 toolist 제공 하는 hello만 사용자 지정 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-118">You can also use [az network nsg rule list](/cli/azure/network/nsg/rule#list) toolist only hello custom rules from an NSG .</span></span>
>

## <a name="view-nsg-associations"></a><span data-ttu-id="cfc63-119">NSG 연결 보기</span><span class="sxs-lookup"><span data-stu-id="cfc63-119">View NSG associations</span></span>

<span data-ttu-id="cfc63-120">tooview 어떤 리소스 hello **NSG 프런트 엔드** NSG는 연결 된를 실행 하는 hello `az network nsg show` 아래와 같이 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `az network nsg show` command as shown below.</span></span> 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

<span data-ttu-id="cfc63-121">Hello에 대 한 확인 **networkInterfaces** 및 **서브넷** 아래와 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="cfc63-121">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

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

<span data-ttu-id="cfc63-122">NSG가 hello tooany Nic (네트워크 인터페이스), 연결 된 위의 hello 예제 이며 라는 관련된 tooa 서브넷 **프런트 엔드**합니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-122">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="add-a-rule"></a><span data-ttu-id="cfc63-123">규칙 추가</span><span class="sxs-lookup"><span data-stu-id="cfc63-123">Add a rule</span></span>
<span data-ttu-id="cfc63-124">tooadd 허용 하는 규칙 **인바운드** 트래픽 tooport **443** 모든 컴퓨터 toohello에서 **NSG 프런트 엔드** NSG를 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
az network nsg rule create  \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd  \
--name allow-https \
--description "Allow access tooport 443 for HTTPS" \
--access Allow \
--protocol Tcp  \
--direction Inbound \
--priority 102 \
--source-address-prefix "*"  \
--source-port-range "*"  \
--destination-address-prefix "*" \
--destination-port-range "443"
```

<span data-ttu-id="cfc63-125">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="cfc63-125">Expected output:</span></span>

```json
{
  "access": "Allow",
  "description": "Allow access tooport 443 for HTTPS",
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

## <a name="change-a-rule"></a><span data-ttu-id="cfc63-126">규칙 변경</span><span class="sxs-lookup"><span data-stu-id="cfc63-126">Change a rule</span></span>
<span data-ttu-id="cfc63-127">tooallow 위에서 만든 toochange hello 규칙 hello에서 트래픽 인바운드 **인터넷** hello에만, 실행 [az 네트워크 nsg 규칙 업데이트](/cli/azure/network/nsg/rule#update) 명령:</span><span class="sxs-lookup"><span data-stu-id="cfc63-127">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command:</span></span>

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

<span data-ttu-id="cfc63-128">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="cfc63-128">Expected output:</span></span>

```json
{
"access": "Allow",
"description": "Allow access tooport 443 for HTTPS",
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

## <a name="delete-a-rule"></a><span data-ttu-id="cfc63-129">규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="cfc63-129">Delete a rule</span></span>
<span data-ttu-id="cfc63-130">위에서 만든 toodelete hello 규칙은 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-130">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="cfc63-131">NSG tooa NIC에 연결</span><span class="sxs-lookup"><span data-stu-id="cfc63-131">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="cfc63-132">tooassociate hello **NSG 프런트 엔드** NSG toohello **TestNICWeb1** NIC를 사용 하 여 hello [az 네트워크 nic 업데이트](/cli/azure/network/nic#update) 명령:</span><span class="sxs-lookup"><span data-stu-id="cfc63-132">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, use hello [az network nic update](/cli/azure/network/nic#update) command:</span></span>

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

<span data-ttu-id="cfc63-133">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="cfc63-133">Expected output:</span></span>

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

## <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="cfc63-134">NIC에서 NSG 분리</span><span class="sxs-lookup"><span data-stu-id="cfc63-134">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="cfc63-135">toodissociate hello **NSG 프런트 엔드** hello에서 NSG **TestNICWeb1** hello 실행 NIC [az 네트워크 nsg 규칙 업데이트](/cli/azure/network/nsg/rule#update) 명령을 다시 있지만 hello 대체할 `--network-security-group` 인수는 빈 문자열 (`""`).</span><span class="sxs-lookup"><span data-stu-id="cfc63-135">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

<span data-ttu-id="cfc63-136">Hello 출력에 hello `networkSecurityGroup` toonull 키가 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-136">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="cfc63-137">서브넷에서 NSG 분리</span><span class="sxs-lookup"><span data-stu-id="cfc63-137">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="cfc63-138">toodissociate hello **NSG 프런트 엔드** hello에서 NSG **프런트 엔드** 서브넷을 다시 실행 하는 hello [az 네트워크 nsg 규칙 업데이트](/cli/azure/network/nsg/rule#update) 명령을 다시 있지만 hello 대체할 `--network-security-group` 인수는 빈 문자열 (`""`).</span><span class="sxs-lookup"><span data-stu-id="cfc63-138">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, again run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

<span data-ttu-id="cfc63-139">Hello 출력에 hello `networkSecurityGroup` toonull 키가 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-139">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="cfc63-140">NSG tooa 서브넷 연결</span><span class="sxs-lookup"><span data-stu-id="cfc63-140">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="cfc63-141">tooassociate hello **NSG 프런트 엔드** NSG toohello **프런트 엔드** 서브넷에 hello 다음 명령을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-141">tooassociate hello **NSG-FrontEnd** NSG toohello **FrontEnd** subnet again, run hello following command:</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

<span data-ttu-id="cfc63-142">Hello 출력에 hello `networkSecurityGroup` 비슷한 hello 값에 대 한 키에:</span><span class="sxs-lookup"><span data-stu-id="cfc63-142">In hello output, hello `networkSecurityGroup` key has something similar for hello value:</span></span>

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

## <a name="delete-an-nsg"></a><span data-ttu-id="cfc63-143">NSG 삭제</span><span class="sxs-lookup"><span data-stu-id="cfc63-143">Delete an NSG</span></span>
<span data-ttu-id="cfc63-144">NSG tooany 리소스를 연결 되지 않은 경우에 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-144">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="cfc63-145">NSG를 toodelete는 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-145">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="cfc63-146">toocheck hello 리소스 관련 tooan NSG를 hello 실행 `azure network nsg show` 에서처럼 [보기 Nsg 연결](#View-NSGs-associations)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-146">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="cfc63-147">Hello NSG 연결된 tooany Nic 이면 hello 실행 `azure network nic set` 에서처럼 [NIC에서 NSG를 분리](#Dissociate-an-NSG-from-a-NIC) 각 NIC.에 대 한</span><span class="sxs-lookup"><span data-stu-id="cfc63-147">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="cfc63-148">Hello NSG 연결된 tooany 서브넷 이면 hello 실행 `azure network vnet subnet set` 에서처럼 [서브넷에서 NSG를 분리](#Dissociate-an-NSG-from-a-subnet) 각 서브넷에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-148">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="cfc63-149">toodelete hello NSG hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfc63-149">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a><span data-ttu-id="cfc63-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cfc63-150">Next steps</span></span>
* <span data-ttu-id="cfc63-151">[로깅을 사용합니다](virtual-network-nsg-manage-log.md) .</span><span class="sxs-lookup"><span data-stu-id="cfc63-151">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

