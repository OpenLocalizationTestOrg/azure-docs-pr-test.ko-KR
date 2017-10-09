---
title: "aaaAccess Windows Vm에 대 한 Azure 템플릿에서 및 보안 | Microsoft Docs"
description: "Azure 가상 컴퓨터 DotNet Core 자습서"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4b8227ae745b3b0a22d136e98d18479f8b1504c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="72438-103">Windows VM용 Azure Resource Manager 템플릿의 액세스 및 보안</span><span class="sxs-lookup"><span data-stu-id="72438-103">Access and security in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="72438-104">응용 프로그램에서 Azure 할 가능성이 toobe 액세스를 통해 호스트 되 hello 인터넷 또는 VPN / azure Express 경로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="72438-104">Applications hosted in Azure likely need toobe access over hello internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="72438-105">Hello 음악 스토어 응용 프로그램 샘플에서와 hello 웹 사이트에서 사용할 수는 공용 IP 주소로 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="72438-105">With hello Music Store application sample, hello web site is made available on hello internet with a public IP address.</span></span> <span data-ttu-id="72438-106">설정에 연결 된 연결 toohello 응용 프로그램 리소스를 액세스할 toohello 가상 컴퓨터 자체를 보호 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72438-106">With access established, connections toohello application and access toohello virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="72438-107">이 액세스 보안은 네트워크 보안 그룹을 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="72438-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="72438-108">이 문서에 hello 샘플 Azure 리소스 관리자 템플릿 hello 음악 스토어 응용 프로그램 보호 되는 방식을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="72438-108">This document details how hello Music Store application is secured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="72438-109">모든 종속성 및 고유한 구성이 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="72438-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="72438-110">Hello 최상의 경험에 대 한 미리 hello 솔루션 tooyour Azure 구독 및 Azure 리소스 관리자 템플릿 hello와 함께 작업의 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="72438-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="72438-111">hello 완전 한 템플릿 여기 – 있습니다 [Windows에서 음악 스토어 배포](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)합니다.</span><span class="sxs-lookup"><span data-stu-id="72438-111">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="public-ip-address"></a><span data-ttu-id="72438-112">공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="72438-112">Public IP Address</span></span>
<span data-ttu-id="72438-113">tooprovide 공용 액세스 tooan Azure 리소스, 공용 IP 주소 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72438-113">tooprovide public access tooan Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="72438-114">정적 또는 동적 IP 주소로 공용 IP 주소를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72438-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="72438-115">동적 주소를 사용 하 고 hello 가상 컴퓨터를 중지 하 고 할당 취소 hello 주소 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72438-115">If a dynamic address is used, and hello virtual machine is stopped and deallocated, hello addresses is removed.</span></span> <span data-ttu-id="72438-116">Hello 컴퓨터 다시 시작 되 면 다른 공용 IP 주소를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72438-116">When hello machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="72438-117">가 변경할 tooprevent는 IP 주소, 예약된 된 IP 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72438-117">tooprevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="72438-118">공용 IP 주소는 Visual Studio 새 리소스 추가 마법사, hello를 사용 하 여 tooan Azure 리소스 관리자 템플릿을 추가할 수 있습니다 또는 서식 파일에 유효한 JSON을 삽입 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="72438-118">A Public IP Address can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="72438-119">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [공용 IP 주소](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110)합니다.</span><span class="sxs-lookup"><span data-stu-id="72438-119">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

<span data-ttu-id="72438-120">공용 IP 주소를 가상 네트워크 어댑터 또는 부하 분산 장치에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72438-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="72438-121">이 예제에서는 hello 음악 스토어 웹 사이트는 여러 가상 컴퓨터에서 부하 분산 때문에 hello 공용 IP 주소에는 연결 된 toohello 부하 분산 장치는 합니다.</span><span class="sxs-lookup"><span data-stu-id="72438-121">In this example, because hello Music Store website is load balanced across several virtual machines, hello Public IP Address is attached toohello Load Balancer.</span></span>

<span data-ttu-id="72438-122">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [부하 분산 된 공용 IP 주소 연결](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211)합니다.</span><span class="sxs-lookup"><span data-stu-id="72438-122">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="72438-123">hello와 공용 IP 주소에서에서 본 hello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="72438-123">hello public IP Address as seen from hello Azure portal.</span></span> <span data-ttu-id="72438-124">관련된 tooa 부하 분산 장치 및 가상 컴퓨터가 아닌 hello 공용 IP 주소 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="72438-124">Notice that hello public IP address is associated tooa load balancer and not a virtual machine.</span></span> <span data-ttu-id="72438-125">네트워크 부하 분산 장치 hello이이 시리즈의 다음 문서에 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="72438-125">Network load balancers are detailed in hello next document of this series.</span></span>

![공용 IP 주소](./media/dotnet-core-3-access-security/pubip-win.png)

<span data-ttu-id="72438-127">Azure 공용 IP 주소에 대한 자세한 내용은 [Azure의 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="72438-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="72438-128">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="72438-128">Network Security Group</span></span>
<span data-ttu-id="72438-129">액세스에 설정 된 tooAzure 리소스를 수행한 후에이 액세스 제한 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72438-129">Once access has been established tooAzure resources, this access should be limited.</span></span> <span data-ttu-id="72438-130">Azure 가상 컴퓨터의 경우 네트워크 보안 그룹을 사용하여 보안 액세스가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="72438-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="72438-131">Hello 음악 스토어 응용 프로그램 샘플에서와 모든 액세스 toohello 가상 컴퓨터는 http 액세스에 대 한 포트 80 및 포트 3389 RDP 액세스를 통해 제외 하 고 제한.</span><span class="sxs-lookup"><span data-stu-id="72438-131">With hello Music Store application sample, all access toohello virtual machine is restricted except for over port 80 for http access, and port 3389 for RDP access.</span></span> <span data-ttu-id="72438-132">네트워크 보안 그룹은 Visual Studio 새 리소스 추가 마법사, hello를 사용 하 여 tooan Azure 리소스 관리자 템플릿을 추가할 수 있습니다 또는 서식 파일에 유효한 JSON을 삽입 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="72438-132">A Network Security Group can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="72438-133">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [네트워크 보안 그룹](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57)합니다.</span><span class="sxs-lookup"><span data-stu-id="72438-133">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
},
```

<span data-ttu-id="72438-134">이 예제에서는 hello 네트워크 보안 그룹 hello 가상 네트워크 리소스에 선언 된 hello 서브넷 개체와 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72438-134">In this example, hello network security group is associate with hello subnet object declared in hello Virtual Network resource.</span></span> 

<span data-ttu-id="72438-135">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [가상 네트워크와 네트워크 보안 그룹 연결이](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143)합니다.</span><span class="sxs-lookup"><span data-stu-id="72438-135">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span></span>

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
]
```

<span data-ttu-id="72438-136">다음은 어떤 hello 네트워크 보안 그룹 모양 hello에서 Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="72438-136">Here is what hello network security group looks like from hello Azure portal.</span></span> <span data-ttu-id="72438-137">NSG는 서브넷 및/또는 네트워크 인터페이스와 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72438-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="72438-138">이 경우 hello NSG에는 관련된 tooa 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="72438-138">In this case, hello NSG is associated tooa subnet.</span></span> <span data-ttu-id="72438-139">이 구성에서는 hello 인바운드 규칙을 적용 tooall 연결 된 가상 컴퓨터 toohello 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="72438-139">In this configuration, hello inbound rules apply tooall virtual machines connected toohello subnet.</span></span>

![네트워크 보안 그룹](./media/dotnet-core-3-access-security/nsg-win.png)

<span data-ttu-id="72438-141">네트워크 보안 그룹에 대한 자세한 내용은 [네트워크 보안 그룹이란?](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="72438-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="72438-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="72438-142">Next step</span></span>
<hr>

[<span data-ttu-id="72438-143">3단계 - Azure Resource Manager 템플릿의 가용성 및 크기 조정</span><span class="sxs-lookup"><span data-stu-id="72438-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

