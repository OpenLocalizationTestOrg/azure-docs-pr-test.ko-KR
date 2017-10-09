---
title: "aaaAvailability 및 Azure 리소스 관리자 템플릿을 배율이 | Microsoft Docs"
description: "Azure 가상 컴퓨터 DotNet Core 자습서"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8fcfea79-f017-4658-8c51-74242fcfb7f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6f830ca0a64e6b65859312bdf31dc0af59e2b978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="c26fb-103">Linux VM용 Azure Resource Manager 템플릿의 가용성 및 크기 조정</span><span class="sxs-lookup"><span data-stu-id="c26fb-103">Availability and scale in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="c26fb-104">가용성과 규모 toouptime / hello 기능 toomeet 요구를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c26fb-104">Availability and scale refer toouptime and hello ability toomeet demand.</span></span> <span data-ttu-id="c26fb-105">응용 프로그램 hello 시간의 99.9%를 차지 수 있어야 할 경우 여러 개의 동시 계산 리소스를 허용 하는 아키텍처 toohave가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-105">If an application must be up 99.9% of hello time, it needs toohave an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="c26fb-106">예를 들어, 단일 웹 사이트를 설치 하는 대신 가용성의 높은 수준의 구성 hello 앞에 기술 분산 동일 사이트의 여러 인스턴스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of hello same site, with balancing technology in front of them.</span></span> <span data-ttu-id="c26fb-107">이 구성에서는 hello 응용 프로그램의 한 인스턴스를 중지할 수 유지 관리를 위해 남은 hello toofunction를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-107">In this configuration, one instance of hello application can be taken down for maintenance, while hello remaining continue toofunction.</span></span> <span data-ttu-id="c26fb-108">눈금 hello에 다른 손 tooan 응용 프로그램에서 기능 tooserve 요구를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-108">Scale on hello other hand refers tooan applications ability tooserve demand.</span></span> <span data-ttu-id="c26fb-109">부하 분산 된 응용 프로그램을 추가 하거나 hello 풀에서 인스턴스를 제거 하더라도 응용 프로그램 tooscale toomeet 요구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-109">With a load balanced application, adding or removing instances from hello pool allows an application tooscale toomeet demand.</span></span>

<span data-ttu-id="c26fb-110">이 문서 가용성과 규모에 대 한 hello Music Store 샘플 배포는 구성 하는 방법에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-110">This document details how hello Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="c26fb-111">모든 종속성 및 고유한 구성이 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="c26fb-112">Hello 최상의 경험에 대 한 미리 hello 솔루션 tooyour Azure 구독 및 Azure 리소스 관리자 템플릿 hello와 함께 작업의 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-112">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="c26fb-113">hello 완전 한 템플릿 여기 – 있습니다 [ubuntu 음악 스토어 배포](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-113">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="availability-set"></a><span data-ttu-id="c26fb-114">가용성 집합</span><span class="sxs-lookup"><span data-stu-id="c26fb-114">Availability Set</span></span>
<span data-ttu-id="c26fb-115">가용성 집합은 여러 물리적 호스트 및 기타 인프라 구성 요소(예: 전원 공급 장치 및 물리적 네트워킹 하드웨어)에 Azure 가상 컴퓨터를 논리적으로 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="c26fb-116">가용성 집합은 유지 관리, 장치 오류 또는 기타 가동 중단 시간 동안 모든 가상 컴퓨터가 영향을 받지는 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="c26fb-117">가용성 집합 tooan Azure 리소스 관리자 템플릿 hello Visual Studio 새 리소스 추가 마법사를 사용 하 여 서식 파일에 유효한 JSON을 삽입 또는 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-117">An Availability Set can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="c26fb-118">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [가용성 집합](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387)합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-118">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "avalibility-set"
  },
  "properties": {
    "platformUpdateDomainCount": 5,
    "platformFaultDomainCount": 3
  }
}
```

<span data-ttu-id="c26fb-119">가용성 집합은 가상 컴퓨터 리소스의 속성으로 선언됩니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="c26fb-120">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [가상 컴퓨터와 연결 가용성 집합](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313)합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-120">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="c26fb-121">hello 가용성 hello Azure 포털에서에서와 같이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-121">hello availability set as seen from hello Azure portal.</span></span> <span data-ttu-id="c26fb-122">각 가상 컴퓨터 및 hello 구성에 대 한 세부 정보는 여기에서 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-122">Each virtual machine and details about hello configuration are detailed here.</span></span>

![가용성 집합](./media/dotnet-core-4-availability-scale/aset.png)

<span data-ttu-id="c26fb-124">가용성 집합에 대한 자세한 내용은 [가상 컴퓨터의 가용성 관리](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c26fb-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="c26fb-125">네트워크 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="c26fb-125">Network Load Balancer</span></span>
<span data-ttu-id="c26fb-126">가용성 집합에는 응용 프로그램에 대 한 내결함성을 제공, 반면 부하 분산 장치 하면 hello 응용 프로그램의 여러 인스턴스에서 사용할 수는 단일 네트워크 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of hello application available on a single network address.</span></span> <span data-ttu-id="c26fb-127">응용 프로그램의 여러 인스턴스를 호스팅할 수 있습니다 tooa 부하 분산 장치를 연결 된 각 많은 가상 컴퓨터에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-127">Multiple instances of an application can be hosted on many virtual machines, each one connected tooa load balancer.</span></span> <span data-ttu-id="c26fb-128">Hello 응용 프로그램에 액세스 하는 대로 hello 부하 분산 장치 경로 hello 연결 된 멤버에서 들어오는 요청을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-128">As hello application is accessed, hello load balancer routes hello incoming request across hello attached members.</span></span> <span data-ttu-id="c26fb-129">부하 분산 장치 또는 hello Visual Studio 새 리소스 추가 마법사를 사용 하 여 추가할 수 올바르게 삽입 하 여 JSON 리소스 hello Azure 리소스 관리자 템플릿으로 서식이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-129">A Load Balancer can be added using hello Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into hello Azure Resource Manager template.</span></span>

<span data-ttu-id="c26fb-130">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [네트워크 부하 분산 장치](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208)합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-front"
  },
  ........<truncated>
}
```

<span data-ttu-id="c26fb-131">Hello 샘플 응용 프로그램에 노출 된 toohello 이므로 공용 IP 주소를 사용 하 여 인터넷을이 주소는 부하 분산 장치 hello와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-131">Because hello sample application is exposed toohello internet with a public IP address, this address is associated with hello load balancer.</span></span> 

<span data-ttu-id="c26fb-132">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [공용 IP 주소와 네트워크 부하 분산 장치 연결](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221)합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-132">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="c26fb-133">Hello Azure 포털에서에서 hello 네트워크 부하 분산 장치 개요 표시 hello 공용 IP 주소와 hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-133">From hello Azure portal, hello network load balancer overview shows hello association with hello public IP address.</span></span>

![네트워크 부하 분산 장치](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="c26fb-135">부하 분산 장치 규칙</span><span class="sxs-lookup"><span data-stu-id="c26fb-135">Load Balancer Rule</span></span>
<span data-ttu-id="c26fb-136">부하 분산 장치를 사용 하 여 의도 한 hello 리소스 간에 트래픽 균형 방법을 제어 하는 규칙이 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-136">When using a load balancer, rules are configured that control how traffic is balanced across hello intended resources.</span></span> <span data-ttu-id="c26fb-137">Hello 예제 음악 스토어 응용 프로그램으로 트래픽 hello 공용 IP 주소의 포트 80에서 도착 하 고 모든 가상 컴퓨터의 포트 80에 분산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-137">With hello sample Music Store application, traffic arrives on port 80 of hello public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="c26fb-138">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [부하 분산 장치 규칙](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270)합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-138">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span>

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

<span data-ttu-id="c26fb-139">수준의 hello 네트워크 부하 분산 장치 규칙 hello 포털에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-139">A view of hello network load balancer rule from hello portal.</span></span>

![네트워크 부하 분산 장치 규칙](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="c26fb-141">부하 분산 장치 검색</span><span class="sxs-lookup"><span data-stu-id="c26fb-141">Load Balancer Probe</span></span>
<span data-ttu-id="c26fb-142">부하 분산 장치 hello도 필요 toomonitor 각 가상 컴퓨터 요청은 toorunning 시스템만을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-142">hello load balancer also needs toomonitor each virtual machine so that requests are served only toorunning systems.</span></span> <span data-ttu-id="c26fb-143">이 모니터링은 미리 정의된 포트를 지속적으로 검색하여 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="c26fb-144">hello Music Store 배포가 구성 된 tooprobe 포트 80에 모든 포함 된 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-144">hello Music Store deployment is configured tooprobe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="c26fb-145">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [부하 분산 장치 검색](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257)합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-145">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span></span>

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

<span data-ttu-id="c26fb-146">부하 분산 장치 프로브 hello hello Azure 포털에서에서 본 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-146">hello load balancer probe seen from hello Azure portal.</span></span>

![네트워크 부하 분산 장치 검색](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="c26fb-148">인바운드 NAT 규칙</span><span class="sxs-lookup"><span data-stu-id="c26fb-148">Inbound NAT Rules</span></span>
<span data-ttu-id="c26fb-149">규칙 toobe 필요한 부하 분산 장치를 사용할 때 비 부하 분산 된 액세스 tooeach 가상 컴퓨터를 제공 하는 위치에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-149">When using a Load Balancer, rules need toobe put into place that provide non-load balanced access tooeach Virtual Machine.</span></span> <span data-ttu-id="c26fb-150">예를 들어 각 가상 컴퓨터에 대한 SSH 연결을 만들 때 이 트래픽의 부하가 분산되지 않아야 하며, 미리 결정된 경로가 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-150">For instance, when creating an SSH connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="c26fb-151">미리 결정된 경로는 인바운드 NAT 규칙 리소스를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-151">pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="c26fb-152">이 리소스를 사용 하 여 인바운드 통신 매핑된 tooindividual 가상 컴퓨터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-152">Using this resource, inbound communication can be mapped tooindividual Virtual Machines.</span></span> 

<span data-ttu-id="c26fb-153">음악 스토어 응용 프로그램 hello로 매핑된 tooport 22 각 가상 컴퓨터에 SSH 액세스를 위한가 5000에서 시작 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-153">With hello Music Store application, a port starting at 5000 is mapped tooport 22 on each Virtual Machine for SSH access.</span></span> <span data-ttu-id="c26fb-154">hello `copyindex()` 함수는 사용 되는 tooincrement hello 수신 포트, 5001이 고 포트가 들어오는 받는 두 번째 가상 컴퓨터를 hello 등, 세 번째 5002 hello 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-154">hello `copyindex()` function is used tooincrement hello incoming port, such that hello second Virtual Machine receives an incoming port of 5001, hello third 5002, and so on.</span></span> 

<span data-ttu-id="c26fb-155">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [인바운드 NAT 규칙](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270)합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-155">Follow this link toosee hello JSON sample within hello Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'SSH-VM', copyIndex())]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "location": "[resourceGroup().location]",
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
    "backendPort": 22,
    "enableFloatingIP": false
  }
}
```

<span data-ttu-id="c26fb-156">Azure 포털에서 본 것된 hello로 인바운드 NAT 규칙을 한 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-156">One example inbound NAT rule as seen in hello Azure portal.</span></span> <span data-ttu-id="c26fb-157">SSH NAT 규칙 hello 배포의 각 가상 컴퓨터에 대해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-157">An SSH NAT rule is created for each virtual machine in hello deployment.</span></span>

![인바운드 NAT 규칙](./media/dotnet-core-4-availability-scale/natrule.png)

<span data-ttu-id="c26fb-159">Hello Azure 네트워크 부하 분산 장치에 대 한 자세한 내용은 참조 하십시오. [부하 Azure 인프라 서비스에 대 한 분산](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-159">For in-depth information on hello Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="c26fb-160">여러 VM 배포</span><span class="sxs-lookup"><span data-stu-id="c26fb-160">Deploy multiple VMs</span></span>
<span data-ttu-id="c26fb-161">마지막으로,에서 가용성 집합 또는 부하 분산 장치 tooeffectively 함수를 여러 가상 컴퓨터가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-161">Finally, for an Availability Set or Load Balancer tooeffectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="c26fb-162">Hello Azure 리소스 관리자 템플릿 복사 기능을 사용 하 여 여러 Vm은 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-162">Multiple VMs can be deployed using hello Azure Resource Manager template copy function.</span></span> <span data-ttu-id="c26fb-163">Hello 복사 기능을 사용 하 여, 없습니다. 필요한 toodefine 한정 된 수의 가상 컴퓨터 대신이 값 수 동적으로 제공할 수 hello 시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-163">Using hello copy function, it is not necessary toodefine a finite number of Virtual Machines, rather this value can be dynamically provided at hello time of deployment.</span></span> <span data-ttu-id="c26fb-164">hello 복사 기능 인스턴스 toocreated 및 hello 적절 한 수의 가상 컴퓨터와 연결 된 리소스를 배포 하는 핸들의 hello 번호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-164">hello copy function consumes hello number of instances toocreated and handles deploying hello proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="c26fb-165">Hello 음악 스토어 샘플 템플릿은 인스턴스 수는 수행 하는 매개 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-165">In hello Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="c26fb-166">가상 컴퓨터 및 관련된 리소스를 만들 때이 수가 hello 템플릿 전체에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-166">This number is used throughout hello template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
}
```

<span data-ttu-id="c26fb-167">Hello 가상 컴퓨터 리소스, hello 복사 루프는 이름이 지정 되며 있으며 toocontrol hello 매수 결과 사용 하는 hello 수가 인스턴스 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-167">On hello Virtual Machine resource, hello copy loop is given a name and hello number of instances parameter used toocontrol hello number of resulting copies.</span></span>

<span data-ttu-id="c26fb-168">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [가상 컴퓨터 복사 기능](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300)합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-168">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span></span> 

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Compute/virtualMachines",
"name": "[concat(variables('vmName'),copyindex())]",
"location": "[resourceGroup().location]",
"copy": {
  "name": "virtualMachineLoop",
  "count": "[parameters('numberOfInstances')]"
}
```

<span data-ttu-id="c26fb-169">hello 복사 기능의 현재 반복 hello hello로 액세스할 수 `copyIndex()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-169">hello current iteration of hello copy function can be accessed with hello `copyIndex()` function.</span></span> <span data-ttu-id="c26fb-170">hello 복사 인덱스 함수 hello 값 tooname 사용 되는 가상 컴퓨터 및 기타 리소스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-170">hello value of hello copy index function can be used tooname virtual machines and other resources.</span></span> <span data-ttu-id="c26fb-171">예를 들어 가상 컴퓨터의 두 인스턴스가 배포된 경우 둘 다 이름이 달라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="c26fb-172">hello `copyIndex()` hello 가상 컴퓨터의 부분 이름을 toocreate 고유 이름으로 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-172">hello `copyIndex()` function can be used as part of hello virtual machine name toocreate a unique name.</span></span> <span data-ttu-id="c26fb-173">Hello의 예로 `copyindex()` hello 가상 컴퓨터 리소스에서에서 목적으로 이름 지정에 사용 되는 함수를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-173">An example of hello `copyindex()` function used for naming purposes can be seen in hello Virtual Machine resource.</span></span> <span data-ttu-id="c26fb-174">여기서 hello 컴퓨터 이름은 hello의 연결을 `vmName` 매개 변수 및 hello `copyIndex()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-174">Here, hello computer name is a concatenation of hello `vmName` parameter, and hello `copyIndex()` function.</span></span> 

<span data-ttu-id="c26fb-175">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [복사 인덱스 기능](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319)합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-175">Follow this link toosee hello JSON sample within hello Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span></span> 

```json
"osProfile": {
  "computerName": "[concat(parameters('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "linuxConfiguration": {
    "disablePasswordAuthentication": "true",
    "ssh": {
      "publicKeys": [
        {
          "path": "[variables('sshKeyPath')]",
          "keyData": "[parameters('sshKeyData')]"
        }
      ]
    }
  }
}
```

<span data-ttu-id="c26fb-176">hello `copyIndex` 함수가 hello Music Store 예제 서식 파일에서 여러 번 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-176">hello `copyIndex` function is used several times in hello Music Store sample template.</span></span> <span data-ttu-id="c26fb-177">리소스 및 함수를 사용 하 여 `copyIndex` 어느 것에 특정 tooa hello 가상 컴퓨터 네트워크 인터페이스, 부하 분산 장치 규칙 등의 단일 인스턴스를 포함 하 고 모든 기능에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-177">Resources and functions utilizing `copyIndex` include anything specific tooa single instance of hello virtual machine such as network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="c26fb-178">Hello 복사 기능에 대 한 자세한 내용은 참조 하십시오. [Azure 리소스 관리자 리소스의 여러 인스턴스를 만들](../../resource-group-create-multiple.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c26fb-178">For more information on hello copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="c26fb-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c26fb-179">Next step</span></span>
<hr>

[<span data-ttu-id="c26fb-180">4단계 - Azure Resource Manager 템플릿을 사용한 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="c26fb-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

