---
title: "Azure Resource Manager 템플릿의 가용성 및 크기 조정 | Microsoft Docs"
description: "Azure 가상 컴퓨터 DotNet Core 자습서"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 494724b5-06af-4dea-a774-ba580cf27527
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c351950fa3fc1023e339c0dc63b034c5e0d910f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="e0f7b-103">Windows VM용 Azure Resource Manager 템플릿의 가용성 및 크기 조정</span><span class="sxs-lookup"><span data-stu-id="e0f7b-103">Availability and scale in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="e0f7b-104">가용성 및 크기 조정은 가동 시간 및 요구를 충족하는 능력을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-104">Availability and scale refer to uptime and the ability to meet demand.</span></span> <span data-ttu-id="e0f7b-105">응용 프로그램의 가동 시간이 99.9% 이상이어야 하면 여러 개의 동시 계산 리소스를 허용하는 아키텍처가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-105">If an application must be up 99.9% of the time, it needs to have an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="e0f7b-106">예를 들어 단일 웹 사이트를 유지하지 않고, 가용성 수준이 좀 더 높은 구성에 동일한 사이트의 여러 인스턴스를 포함하고 부하 분산 기술을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of the same site, with balancing technology in front of them.</span></span> <span data-ttu-id="e0f7b-107">이 구성에서 응용 프로그램의 인스턴스 하나를 유지 관리에 사용하고 나머지는 계속 작동되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-107">In this configuration, one instance of the application can be taken down for maintenance, while the remaining continue to function.</span></span> <span data-ttu-id="e0f7b-108">크기 조정은 요구를 처리하는 응용 프로그램의 능력을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-108">Scale on the other hand refers to an applications ability to serve demand.</span></span> <span data-ttu-id="e0f7b-109">부하 분산된 응용 프로그램을 사용하여 풀에서 인스턴스를 추가하거나 제거하면 수요에 맞게 크기를 응용 프로그램 규모를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-109">With a load balanced application, adding or removing instances from the pool allows an application to scale to meet demand.</span></span>

<span data-ttu-id="e0f7b-110">이 문서에서는 가용성 및 크기 조정을 위해 Music Store 샘플 배포를 구성하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-110">This document details how the Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="e0f7b-111">모든 종속성 및 고유한 구성이 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="e0f7b-112">최상의 환경을 위해서는 솔루션 인스턴스를 Azure 구독에 미리 배포하고 Azure Resource Manager 템플릿을 따라 작업하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-112">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="e0f7b-113">전체 템플릿은 [Windows의 Music Store 배포](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-113">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="availability-set"></a><span data-ttu-id="e0f7b-114">가용성 집합</span><span class="sxs-lookup"><span data-stu-id="e0f7b-114">Availability Set</span></span>
<span data-ttu-id="e0f7b-115">가용성 집합은 여러 물리적 호스트 및 기타 인프라 구성 요소(예: 전원 공급 장치 및 물리적 네트워킹 하드웨어)에 Azure 가상 컴퓨터를 논리적으로 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="e0f7b-116">가용성 집합은 유지 관리, 장치 오류 또는 기타 가동 중단 시간 동안 모든 가상 컴퓨터가 영향을 받지는 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="e0f7b-117">Visual Studio 새 리소스 추가 마법사를 사용하거나 템플릿에 유효한 JSON을 삽입하여 Azure Resource Manager 템플릿에 가용성 집합을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-117">An Availability Set can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="e0f7b-118">[가용성 집합](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-118">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "availability-set"
  },
  "properties": {
  }
}
```

<span data-ttu-id="e0f7b-119">가용성 집합은 가상 컴퓨터 리소스의 속성으로 선언됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="e0f7b-120">[가상 컴퓨터와 가용성 집합 연결](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-120">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="e0f7b-121">Azure Portal의 가용성 집합.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-121">The availability set as seen from the Azure portal.</span></span> <span data-ttu-id="e0f7b-122">각 가상 컴퓨터 및 구성 방법에 대한 세부 정보가 여기에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-122">Each virtual machine and details about the configuration are detailed here.</span></span>

![가용성 집합](./media/dotnet-core-4-availability-scale/ase-win.png)

<span data-ttu-id="e0f7b-124">가용성 집합에 대한 자세한 내용은 [가상 컴퓨터의 가용성 관리](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="e0f7b-125">네트워크 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="e0f7b-125">Network Load Balancer</span></span>
<span data-ttu-id="e0f7b-126">가용성 집합은 응용 프로그램 내결함성을 제공하지만 부하 분산 장치는 단일 네트워크 주소에서 응용 프로그램의 여러 인스턴스를 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of the application available on a single network address.</span></span> <span data-ttu-id="e0f7b-127">응용 프로그램의 여러 인스턴스를 각각 하나의 부하 분산 장치에 연결된 여러 가상 컴퓨터에서 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-127">Multiple instances of an application can be hosted on many virtual machines, each one connected to a load balancer.</span></span> <span data-ttu-id="e0f7b-128">응용 프로그램에 액세스하면 부하 분산 장치는 들어오는 요청을 연결된 멤버 간에 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-128">As the application is accessed, the load balancer routes the incoming request across the attached members.</span></span> <span data-ttu-id="e0f7b-129">Visual Studio 새 리소스 추가 마법사를 사용하거나 적절한 형식의 JSON 리소스를 삽입하여 Azure Resource Manager 템플릿에 부하 분산 장치를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-129">A Load Balancer can be added using the Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into the Azure Resource Manager template.</span></span>

<span data-ttu-id="e0f7b-130">[네트워크 부하 분산 장치](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-130">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer"
  },
  ........<truncated>
}
```

<span data-ttu-id="e0f7b-131">샘플 응용 프로그램이 공용 IP 주소를 사용하여 인터넷에 노출되므로 이 주소는 부하 분산 장치에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-131">Because the sample application is exposed to the internet with a public IP address, this address is associated with the load balancer.</span></span> 

<span data-ttu-id="e0f7b-132">[네트워크 부하 부산 장치와 공용 IP 주소 연결](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-132">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

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

<span data-ttu-id="e0f7b-133">Azure Portal의 네트워크 부하 분산 장치 개요에 공용 IP 주소와의 연결 관계가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-133">From the Azure portal, the network load balancer overview shows the association with the public IP address.</span></span>

![네트워크 부하 분산 장치](./media/dotnet-core-4-availability-scale/nlb-win.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="e0f7b-135">부하 분산 장치 규칙</span><span class="sxs-lookup"><span data-stu-id="e0f7b-135">Load Balancer Rule</span></span>
<span data-ttu-id="e0f7b-136">부하 분산 장치를 사용하면 계획된 리소스 간에 트래픽이 분산되는 방식을 제어하는 규칙이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-136">When using a load balancer, rules are configured that control how traffic is balanced across the intended resources.</span></span> <span data-ttu-id="e0f7b-137">샘플 Music Store 응용 프로그램을 사용할 경우 트래픽은 공용 IP 주소의 포트 80에 도착하고 모든 가상 컴퓨터의 포트 80에 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-137">With the sample Music Store application, traffic arrives on port 80 of the public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="e0f7b-138">[부하 분산 장치 규칙](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-138">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).</span></span>

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

<span data-ttu-id="e0f7b-139">포털의 네트워크 부하 분산 장치 규칙 보기.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-139">A view of the network load balancer rule from the portal.</span></span>

![네트워크 부하 분산 장치 규칙](./media/dotnet-core-4-availability-scale/lbrule-win.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="e0f7b-141">부하 분산 장치 검색</span><span class="sxs-lookup"><span data-stu-id="e0f7b-141">Load Balancer Probe</span></span>
<span data-ttu-id="e0f7b-142">부하 분산 장치는 요청이 실행 중인 시스템에만 제공되도록 각 가상 컴퓨터를 모니터링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-142">The load balancer also needs to monitor each virtual machine so that requests are served only to running systems.</span></span> <span data-ttu-id="e0f7b-143">이 모니터링은 미리 정의된 포트를 지속적으로 검색하여 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="e0f7b-144">Music Store 배포는 포함된 모든 가상 컴퓨터에서 포트 80을 검색하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-144">The Music Store deployment is configured to probe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="e0f7b-145">[부하 분산 장치 검색](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-145">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).</span></span>

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

<span data-ttu-id="e0f7b-146">Azure Portal에서 살펴본 부하 분산 장치 검색.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-146">The load balancer probe seen from the Azure portal.</span></span>

![네트워크 부하 분산 장치 검색](./media/dotnet-core-4-availability-scale/lbprobe-win.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="e0f7b-148">인바운드 NAT 규칙</span><span class="sxs-lookup"><span data-stu-id="e0f7b-148">Inbound NAT Rules</span></span>
<span data-ttu-id="e0f7b-149">부하 분산 장치를 사용할 때 각 가상 컴퓨터에 부하가 분산되지 않은 액세스를 제공하는 규칙을 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-149">When using a Load Balancer, rules need to be put into place that provide non-load balanced access to each Virtual Machine.</span></span> <span data-ttu-id="e0f7b-150">예를 들어 각 가상 컴퓨터에 대한 RDP 연결을 만들 때 이 트래픽의 부하가 분산되지 않아야 하며, 미리 결정된 경로가 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-150">For instance, when creating an RDP connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="e0f7b-151">미리 결정된 경로는 인바운드 NAT 규칙 리소스를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-151">Pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="e0f7b-152">이 리소스를 사용하면 인바운드 통신을 개별 가상 컴퓨터에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-152">Using this resource, inbound communication can be mapped to individual Virtual Machines.</span></span> 

<span data-ttu-id="e0f7b-153">Music Store 응용 프로그램을 사용할 경우 5000에서 시작하는 포트가 RDP 액세스를 위해 각 가상 컴퓨터의 포트 3389에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-153">With the Music Store application, a port starting at 5000 is mapped to port 3389 on each Virtual Machine for RDP access.</span></span> <span data-ttu-id="e0f7b-154">`copyindex()` 함수는 두 번째 가상 컴퓨터가 들어오는 포트 5001을 수신하고, 세 번째가 5002를 수신하는 방식으로 계속되도록 들어오는 포트를 증가시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-154">The `copyindex()` function is used to increment the incoming port, such that the second Virtual Machine receives an incoming port of 5001, the third 5002, and so on.</span></span>

<span data-ttu-id="e0f7b-155">[인바운드 NAT 규칙](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-155">Follow this link to see the JSON sample within the Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'RDP-VM', copyIndex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 3389,
    "enableFloatingIP": false
  }
}
```

<span data-ttu-id="e0f7b-156">Azure Portal의 예제 인바운드 NAT 규칙.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-156">One example inbound NAT rule as seen in the Azure portal.</span></span> <span data-ttu-id="e0f7b-157">배포의 각 가상 컴퓨터에 대해 RDP NAT 규칙이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-157">An RDP NAT rule is created for each virtual machine in the deployment.</span></span>

![인바운드 NAT 규칙](./media/dotnet-core-4-availability-scale/natrule-win.png)

<span data-ttu-id="e0f7b-159">Azure 네트워크 부하 분산 장치에 대한 자세한 내용은 [Azure 인프라 서비스를 위한 부하 분산](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-159">For in-depth information on the Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="e0f7b-160">여러 VM 배포</span><span class="sxs-lookup"><span data-stu-id="e0f7b-160">Deploy multiple VMs</span></span>
<span data-ttu-id="e0f7b-161">마지막으로 가용성 집합 또는 부하 분산 장치가 효과적으로 작동하려면 여러 개의 가상 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-161">Finally, for an Availability Set or Load Balancer to effectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="e0f7b-162">Azure Resource Manager 템플릿 copy 함수를 사용하여 여러 VM을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-162">Multiple VMs can be deployed using the Azure Resource Manager template copy function.</span></span> <span data-ttu-id="e0f7b-163">copy 함수를 사용할 때 정해진 수의 가상 컴퓨터를 정의할 필요는 없습니다. 배포 시에 이 값이 동적으로 제공될 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-163">Using the copy function, it is not necessary to define a finite number of Virtual Machines, rather this value can be dynamically provided at the time of deployment.</span></span> <span data-ttu-id="e0f7b-164">copy 함수는 만들 인스턴스 수를 사용하고, 적절한 수의 가상 컴퓨터 및 관련 리소스의 배포를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-164">The copy function consumes the number of instances to be created and handles deploying the proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="e0f7b-165">Music Store 샘플 템플릿에서 인스턴스 수를 사용하는 매개 변수가 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-165">In the Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="e0f7b-166">가상 컴퓨터 및 관련 리소스를 만들 때 템플릿 전체에서 이 수가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-166">This number is used throughout the template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 2,
  "metadata": {
    "description": "Number of VM instances to be created behind load balancer."
  }
},
```

<span data-ttu-id="e0f7b-167">가상 컴퓨터 리소스에서 복사 루프에 이름이 지정되며, 결과 사본 수를 제어하는 데 인스턴스 수 매개 변수가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-167">On the Virtual Machine resource, the copy loop is given a name and the number of instances parameter used to control the number of resulting copies.</span></span>

<span data-ttu-id="e0f7b-168">[가상 컴퓨터 Copy 함수](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-168">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  }
```

<span data-ttu-id="e0f7b-169">현재 반복되는 copy 함수 항목에는 `copyIndex()` 함수를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-169">The current iteration of the copy function can be accessed with the `copyIndex()` function.</span></span> <span data-ttu-id="e0f7b-170">copy index 함수 값은 가상 컴퓨터 및 기타 리소스를 명명하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-170">The value of the copy index function can be used to name virtual machines and other resources.</span></span> <span data-ttu-id="e0f7b-171">예를 들어 가상 컴퓨터의 두 인스턴스가 배포된 경우 둘 다 이름이 달라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="e0f7b-172">`copyIndex()` 함수는 고유한 이름을 만들기 위해 가상 컴퓨터 이름의 일부로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-172">The `copyIndex()` function can be used as part of the virtual machine name to create a unique name.</span></span> <span data-ttu-id="e0f7b-173">명명을 위해 사용되는 `copyindex()` 함수의 예제는 가상 컴퓨터 리소스에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-173">An example of the `copyindex()` function used for naming purposes can be seen in the Virtual Machine resource.</span></span> <span data-ttu-id="e0f7b-174">여기서 컴퓨터 이름은 `vmName` 매개 변수와 `copyIndex()` 함수를 연결해서 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-174">Here, the computer name is a concatenation of the `vmName` parameter, and the `copyIndex()` function.</span></span> 

<span data-ttu-id="e0f7b-175">[Copy Index 함수](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-175">Follow this link to see the JSON sample within the Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309).</span></span> 

```json
"osProfile": {
  "computerName": "[concat(variables('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "adminPassword": "[parameters('adminPassword')]"
}
```

<span data-ttu-id="e0f7b-176">`copyIndex` 함수는 Music Store 샘플 템플릿에서 여러 번 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-176">The `copyIndex` function is used several times in the Music Store sample template.</span></span> <span data-ttu-id="e0f7b-177">`copyIndex` 를 활용하는 리소스 및 함수에는 네트워크 인터페이스, 부하 분산 장치 규칙 등, 가상 컴퓨터의 단일 인스턴스에 국한되는 항목이 포함되며, 모두가 함수에 따라 좌우됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-177">Resources and functions utilizing `copyIndex` include anything specific to a single instance of the virtual machine such and network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="e0f7b-178">copy 함수에 대한 자세한 내용은 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](../../resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0f7b-178">For more information on the copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="e0f7b-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0f7b-179">Next step</span></span>
<hr>

[<span data-ttu-id="e0f7b-180">4단계 - Azure Resource Manager 템플릿을 사용한 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="e0f7b-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

