---
title: "Windows VM용 Azure 템플릿의 액세스 및 보안 | Microsoft Docs"
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
ms.openlocfilehash: ad1b5c4763cf56f681a50bb1bccc825311bbfdf5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="fb39c-103">Windows VM용 Azure Resource Manager 템플릿의 액세스 및 보안</span><span class="sxs-lookup"><span data-stu-id="fb39c-103">Access and security in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="fb39c-104">Azure에 호스트되는 응용 프로그램은 인터넷 또는 Azure와의 VPN/Express 경로 연결을 통해 액세스되어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-104">Applications hosted in Azure likely need to be access over the internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="fb39c-105">Music Store 응용 프로그램 샘플을 사용할 경우 공용 IP 주소를 통해 인터넷에서 해당 웹 사이트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-105">With the Music Store application sample, the web site is made available on the internet with a public IP address.</span></span> <span data-ttu-id="fb39c-106">액세스가 설정되면 응용 프로그램에 대한 연결 및 가상 컴퓨터 리소스에 대한 액세스가 자체적으로 보호되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-106">With access established, connections to the application and access to the virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="fb39c-107">이 액세스 보안은 네트워크 보안 그룹을 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="fb39c-108">이 문서에서는 샘플 Azure Resource Manager 템플릿에서 Music Store 응용 프로그램의 보안을 유지하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-108">This document details how the Music Store application is secured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="fb39c-109">모든 종속성 및 고유한 구성이 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="fb39c-110">최상의 환경을 위해서는 솔루션 인스턴스를 Azure 구독에 미리 배포하고 Azure Resource Manager 템플릿을 따라 작업하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="fb39c-111">전체 템플릿은 [Windows의 Music Store 배포](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-111">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="public-ip-address"></a><span data-ttu-id="fb39c-112">공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="fb39c-112">Public IP Address</span></span>
<span data-ttu-id="fb39c-113">Azure 리소스에 대한 공용 액세스를 제공하려면 공용 IP 주소 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-113">To provide public access to an Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="fb39c-114">정적 또는 동적 IP 주소로 공용 IP 주소를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="fb39c-115">동적 주소가 사용되고 가상 컴퓨터를 중지된 후 할당 취소되면 해당 주소가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-115">If a dynamic address is used, and the virtual machine is stopped and deallocated, the addresses is removed.</span></span> <span data-ttu-id="fb39c-116">컴퓨터 다시 시작되면 다른 공용 IP 주소를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-116">When the machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="fb39c-117">IP 주소가 변경되지 않게 하려면 예약된 IP 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-117">To prevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="fb39c-118">Visual Studio 새 리소스 추가 마법사를 사용하거나 템플릿에 유효한 JSON을 삽입하여 Azure Resource Manager 템플릿에 공용 IP 주소를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-118">A Public IP Address can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="fb39c-119">[공용 IP 주소](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-119">Follow this link to see the JSON sample within the Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span></span>

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

<span data-ttu-id="fb39c-120">공용 IP 주소를 가상 네트워크 어댑터 또는 부하 분산 장치에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="fb39c-121">이 예제에서는 Music Store 웹 사이트 부하가 여러 가상 컴퓨터에서 분산되기 때문에 공용 IP 주소가 부하 분산 장치에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-121">In this example, because the Music Store website is load balanced across several virtual machines, the Public IP Address is attached to the Load Balancer.</span></span>

<span data-ttu-id="fb39c-122">[공용 IP 주소와 부하 부산 장치 연결](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-122">Follow this link to see the JSON sample within the Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

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

<span data-ttu-id="fb39c-123">Azure Portal에 표시된 공용 IP 주소.</span><span class="sxs-lookup"><span data-stu-id="fb39c-123">The public IP Address as seen from the Azure portal.</span></span> <span data-ttu-id="fb39c-124">공용 IP 주소가 가상 컴퓨터가 아닌 부하 분산 장치에 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-124">Notice that the public IP address is associated to a load balancer and not a virtual machine.</span></span> <span data-ttu-id="fb39c-125">네트워크 부하 분산 장치는 이 시리즈의 다음 문서에 자세히 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-125">Network load balancers are detailed in the next document of this series.</span></span>

![공용 IP 주소](./media/dotnet-core-3-access-security/pubip-win.png)

<span data-ttu-id="fb39c-127">Azure 공용 IP 주소에 대한 자세한 내용은 [Azure의 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb39c-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="fb39c-128">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="fb39c-128">Network Security Group</span></span>
<span data-ttu-id="fb39c-129">Azure 리소스에 대한 액세스가 설정되면 이 액세스를 제한해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-129">Once access has been established to Azure resources, this access should be limited.</span></span> <span data-ttu-id="fb39c-130">Azure 가상 컴퓨터의 경우 네트워크 보안 그룹을 사용하여 보안 액세스가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="fb39c-131">Music Store 응용 프로그램 샘플을 사용하면 가상 컴퓨터에 대한 모든 액세스가 제한됩니다. 단 http 액세스를 위한 포트 80과 RDP 액세스를 위한 포트 3389는 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-131">With the Music Store application sample, all access to the virtual machine is restricted except for over port 80 for http access, and port 3389 for RDP access.</span></span> <span data-ttu-id="fb39c-132">Visual Studio 새 리소스 추가 마법사를 사용하거나 템플릿에 유효한 JSON을 삽입하여 Azure Resource Manager 템플릿에 네트워크 보안 그룹을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-132">A Network Security Group can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="fb39c-133">[네트워크 보안 그룹](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-133">Follow this link to see the JSON sample within the Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span></span>

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

<span data-ttu-id="fb39c-134">이 예제에서 네트워크 보안 그룹은 가상 네트워크 리소스에 선언된 서브넷 개체와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-134">In this example, the network security group is associate with the subnet object declared in the Virtual Network resource.</span></span> 

<span data-ttu-id="fb39c-135">[네트워크 보안 그룹과 가상 네트워크의 연결](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-135">Follow this link to see the JSON sample within the Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span></span>

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

<span data-ttu-id="fb39c-136">Azure Portal의 네트워크 보안 그룹은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-136">Here is what the network security group looks like from the Azure portal.</span></span> <span data-ttu-id="fb39c-137">NSG는 서브넷 및/또는 네트워크 인터페이스와 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="fb39c-138">이 경우 NSG는 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-138">In this case, the NSG is associated to a subnet.</span></span> <span data-ttu-id="fb39c-139">이 구성에서 인바운드 규칙이 서브넷에 연결된 모든 가상 컴퓨터에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb39c-139">In this configuration, the inbound rules apply to all virtual machines connected to the subnet.</span></span>

![네트워크 보안 그룹](./media/dotnet-core-3-access-security/nsg-win.png)

<span data-ttu-id="fb39c-141">네트워크 보안 그룹에 대한 자세한 내용은 [네트워크 보안 그룹이란?](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb39c-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="fb39c-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fb39c-142">Next step</span></span>
<hr>

[<span data-ttu-id="fb39c-143">3단계 - Azure Resource Manager 템플릿의 가용성 및 크기 조정</span><span class="sxs-lookup"><span data-stu-id="fb39c-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

