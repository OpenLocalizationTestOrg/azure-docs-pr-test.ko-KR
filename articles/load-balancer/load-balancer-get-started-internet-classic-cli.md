---
title: "인터넷 연결 부하 분산 장치 만들기 - Azure CLI 클래식 | Microsoft Docs"
description: "Azure CLI를 사용하여 클래식 배포 모델에서 인터넷 연결 부하 분산 장치를 만드는 방법에 대해 알아봅니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: e433a824-4a8a-44d2-8765-a74f52d4e584
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: da3a908f17ff5c6d3923549a884ecc0a13cb8e9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-the-azure-cli"></a><span data-ttu-id="f2f89-103">Azure CLI에서 인터넷 연결 부하 분산 장치(클래식) 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="f2f89-103">Get started creating an Internet facing load balancer (classic) in the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2f89-104">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="f2f89-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="f2f89-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2f89-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="f2f89-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f2f89-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="f2f89-107">Azure 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="f2f89-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="f2f89-108">Azure 리소스로 작업하기 전에 Azure에는 현재 Azure Resource Manager와 클래식 모드의 두 가지 배포 모델이 있다는 것을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="f2f89-109">Azure 리소스로 작업하기 전에 [배포 모델 및 도구](../azure-classic-rm.md) 를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="f2f89-110">이 문서의 윗부분에 있는 탭을 클릭하여 다양한 도구에 대한 설명서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="f2f89-111">이 문서에서는 클래식 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="f2f89-112">또한 [Azure 리소스 관리자를 사용하여 인터넷 연결 부하 분산 장치를 만드는 방법을 배울 수 있습니다](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f2f89-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a><span data-ttu-id="f2f89-113">CLI를 사용하여 인터넷 연결 부하 분산 장치 만들기 단계별 지침</span><span class="sxs-lookup"><span data-stu-id="f2f89-113">Step by step creating an Internet facing load balancer using CLI</span></span>

<span data-ttu-id="f2f89-114">이 가이드에서는 위의 시나리오에 따라 인터넷 부하 분산 장치를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-114">This guide shows how to create an Internet load balancer based on the scenario above.</span></span>

1. <span data-ttu-id="f2f89-115">Azure CLI를 처음 사용하는 경우 [Azure CLI 설치 및 구성](../cli-install-nodejs.md) 을 참조하고 Azure 계정 및 구독을 선택하는 부분까지 관련 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-115">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="f2f89-116">아래와 같이 **azure config mode** 명령을 실행하여 클래식 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-116">Run the **azure config mode** command to switch to classic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="f2f89-117">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="f2f89-117">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="f2f89-118">끝점과 부하 분산 장치 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="f2f89-118">Create endpoint and load balancer set</span></span>

<span data-ttu-id="f2f89-119">시나리오는 가상 컴퓨터 "web1" 및 "web2"가 만들어졌다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-119">The scenario assumes the virtual machines "web1" and "web2" were created.</span></span>
<span data-ttu-id="f2f89-120">이 가이드를 통해 공용 포트로 포트 80과 로컬 포트로 포트 80을 사용하여 부하 분산 장치 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-120">This guide will create a load balancer set using port 80 as public port and port 80 as local port.</span></span> <span data-ttu-id="f2f89-121">또한 프로브 포트가 포트 80에 구성되고 부하 분산 장치 집합을 "lbset"로 지명합니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-121">A probe port is also configured on port 80 and named the load balancer set "lbset".</span></span>

### <a name="step-1"></a><span data-ttu-id="f2f89-122">1단계</span><span class="sxs-lookup"><span data-stu-id="f2f89-122">Step 1</span></span>

<span data-ttu-id="f2f89-123">가상 컴퓨터 "web1"을 위해 `azure network vm endpoint create` 을 사용하여 첫 번째 끝점과 부하 분산 장치 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-123">Create the first endpoint and load balancer set using `azure network vm endpoint create` for virtual machine "web1".</span></span>

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a><span data-ttu-id="f2f89-124">2단계</span><span class="sxs-lookup"><span data-stu-id="f2f89-124">Step 2</span></span>

<span data-ttu-id="f2f89-125">두 번째 가상 컴퓨터 "web2"를 부하 분산 장치 집합에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-125">Add a second virtual machine "web2" to the load balancer set.</span></span>

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a><span data-ttu-id="f2f89-126">3단계</span><span class="sxs-lookup"><span data-stu-id="f2f89-126">Step 3</span></span>

<span data-ttu-id="f2f89-127">`azure vm show` 를 사용하여 부하 분산 장치 구성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-127">Verify the load balancer configuration using `azure vm show` .</span></span>

```azurecli
azure vm show web1
```

<span data-ttu-id="f2f89-128">다음과 같이 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-128">The output will be:</span></span>

    data:    DNSName "contoso.cloudapp.net"
    data:    Location "East US"
    data:    VMName "web1"
    data:    IPAddress "10.0.0.5"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-2015
    6-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "joaoma-1-web1-0-201509251804250879"
    data:    OSDisk mediaLink "https://XXXXXXXXXXXXXXX.blob.core.windows.
    /vhds/joaomatest-web1-2015-09-25.vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Se
    r-2012-R2-20150916-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "XXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 name "XXXXXXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    Network Endpoints 0 loadBalancedEndpointSetName "lbset"
    data:    Network Endpoints 0 localPort 80
    data:    Network Endpoints 0 name "tcp-80-80"
    data:    Network Endpoints 0 port 80
    data:    Network Endpoints 0 loadBalancerProbe port 80
    data:    Network Endpoints 0 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 0 loadBalancerProbe intervalInSeconds 15
    data:    Network Endpoints 0 loadBalancerProbe timeoutInSeconds 31
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 5986
    data:    Network Endpoints 1 name "PowerShell"
    data:    Network Endpoints 1 port 5986
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 3389
    data:    Network Endpoints 2 name "Remote Desktop"
    data:    Network Endpoints 2 port 58081
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="f2f89-129">가상 컴퓨터를 위한 원격 데스크톱 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="f2f89-129">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="f2f89-130">`azure vm endpoint create`을 사용하여 특정 가상 컴퓨터의 공용 포트에서 로컬 포트로 네트워크 트래픽을 전달하는 원격 데스크톱 끝점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-130">You can create a remote desktop endpoint to forward network traffic from a public port to a local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="f2f89-131">부하 분산 장치에서 가상 컴퓨터 제거</span><span class="sxs-lookup"><span data-stu-id="f2f89-131">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="f2f89-132">가상 컴퓨터에서 부하 분산 장치 집합에 연결된 끝점을 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-132">You have to delete the endpoint associated to the load balancer set from the virtual machine.</span></span> <span data-ttu-id="f2f89-133">끝점이 제거되면 가상 컴퓨터는 더 이상 부하 분산 장치 집합에 속하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-133">Once the endpoint is removed, the virtual machine doesn't belong to the load balancer set anymore.</span></span>

<span data-ttu-id="f2f89-134">위의 예제를 통해 명령 `azure vm endpoint delete`를 사용하여 부하 분산 장치 "lbset"에서 가상 컴퓨터 "web1"을 위해 만들어진 끝점을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-134">Using the example above, you can remove the endpoint created for virtual machine "web1" from load balancer "lbset" using the command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> <span data-ttu-id="f2f89-135">명령 `azure vm endpoint --help`를 사용하여 끝점을 관리하는 더 많은 옵션을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2f89-135">You can explore more options to manage endpoints using the command `azure vm endpoint --help`</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2f89-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f2f89-136">Next steps</span></span>

[<span data-ttu-id="f2f89-137">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="f2f89-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="f2f89-138">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="f2f89-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="f2f89-139">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="f2f89-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
