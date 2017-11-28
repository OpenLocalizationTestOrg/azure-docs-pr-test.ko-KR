---
title: "클래식 Azure CLI aaaCreate 인터넷 연결 부하 분산 장치-| Microsoft Docs"
description: "인터넷 연결 부하 분산 장치에 사용 하 여 클래식 배포 모델 toocreate Azure CLI hello 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: e6070cbc574f74bca0cccb960ff192847d6511bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-cli"></a><span data-ttu-id="fc509-103">경우에 인터넷 연결 hello Azure CLI에에서 부하 분산 장치 (클래식)를 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="fc509-103">Get started creating an Internet facing load balancer (classic) in hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fc509-104">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="fc509-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="fc509-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc509-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="fc509-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fc509-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="fc509-107">Azure 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="fc509-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="fc509-108">Azure 리소스를 사용 하기 전에 Azure에 현재 두 가지 배포 모델에 중요 한 toounderstand: Azure 리소스 관리자 및 기본 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="fc509-109">Azure 리소스로 작업하기 전에 [배포 모델 및 도구](../azure-classic-rm.md) 를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="fc509-110">이 문서의 hello 위쪽 hello 탭을 클릭 하 여 다양 한 도구에 대 한 hello 설명서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="fc509-111">이 문서에서는 hello 클래식 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="fc509-112">수도 있습니다 [toocreate 인터넷 연결 로드 분산 장치는 Azure 리소스 관리자를 사용 하는 방법에 대해 알아봅니다](load-balancer-get-started-internet-arm-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a><span data-ttu-id="fc509-113">CLI를 사용하여 인터넷 연결 부하 분산 장치 만들기 단계별 지침</span><span class="sxs-lookup"><span data-stu-id="fc509-113">Step by step creating an Internet facing load balancer using CLI</span></span>

<span data-ttu-id="fc509-114">이 가이드에서는 toocreate는 인터넷 부하 분산 장치에 따라 방법 위의 hello 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-114">This guide shows how toocreate an Internet load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="fc509-115">Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-115">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="fc509-116">Hello 실행 **azure 구성 모드** 아래와 같이 명령 tooswitch tooclassic 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-116">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="fc509-117">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="fc509-117">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="fc509-118">끝점과 부하 분산 장치 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="fc509-118">Create endpoint and load balancer set</span></span>

<span data-ttu-id="fc509-119">"web2" 만들어진와 hello 시나리오에서는 가상 컴퓨터 "web1" hello를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-119">hello scenario assumes hello virtual machines "web1" and "web2" were created.</span></span>
<span data-ttu-id="fc509-120">이 가이드를 통해 공용 포트로 포트 80과 로컬 포트로 포트 80을 사용하여 부하 분산 장치 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-120">This guide will create a load balancer set using port 80 as public port and port 80 as local port.</span></span> <span data-ttu-id="fc509-121">프로브 포트는 포트 80에 구성도 하 고 명명 된 hello 부하 분산 장치 "lbset"를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-121">A probe port is also configured on port 80 and named hello load balancer set "lbset".</span></span>

### <a name="step-1"></a><span data-ttu-id="fc509-122">1단계</span><span class="sxs-lookup"><span data-stu-id="fc509-122">Step 1</span></span>

<span data-ttu-id="fc509-123">Hello 첫 번째 끝점을 만들고 부하 분산 장치를 사용 하 여 설정 `azure network vm endpoint create` "web1" 가상 컴퓨터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-123">Create hello first endpoint and load balancer set using `azure network vm endpoint create` for virtual machine "web1".</span></span>

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a><span data-ttu-id="fc509-124">2단계</span><span class="sxs-lookup"><span data-stu-id="fc509-124">Step 2</span></span>

<span data-ttu-id="fc509-125">두 번째 가상 컴퓨터 "web2" toohello 부하 분산 장치 집합을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-125">Add a second virtual machine "web2" toohello load balancer set.</span></span>

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a><span data-ttu-id="fc509-126">3단계</span><span class="sxs-lookup"><span data-stu-id="fc509-126">Step 3</span></span>

<span data-ttu-id="fc509-127">Hello 부하 분산 장치 사용 하 여 구성 확인 `azure vm show` 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-127">Verify hello load balancer configuration using `azure vm show` .</span></span>

```azurecli
azure vm show web1
```

<span data-ttu-id="fc509-128">hello 출력이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-128">hello output will be:</span></span>

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

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="fc509-129">가상 컴퓨터를 위한 원격 데스크톱 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="fc509-129">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="fc509-130">원격 데스크톱 끝점 tooforward 네트워크 트래픽을 사용 하 여 특정 가상 컴퓨터에 대 한 공용 포트 tooa 로컬 포트를 만들 수 있습니다 `azure vm endpoint create`합니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-130">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="fc509-131">부하 분산 장치에서 가상 컴퓨터 제거</span><span class="sxs-lookup"><span data-stu-id="fc509-131">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="fc509-132">Toodelete hello 연결 된 끝점 toohello hello 가상 컴퓨터에서 부하 분산 장치 집합을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-132">You have toodelete hello endpoint associated toohello load balancer set from hello virtual machine.</span></span> <span data-ttu-id="fc509-133">Hello 끝점 기능이 제거 되 면 hello 가상 컴퓨터 부하 분산 집합을 더 이상을 toohello 속하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-133">Once hello endpoint is removed, hello virtual machine doesn't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="fc509-134">위의 hello 예제를 사용 하 여 제거할 수 있습니다 "web1" 가상 컴퓨터에 대해 만든 hello 끝점 "lbset" hello 명령을 사용 하 여 부하 분산 장치에서 `azure vm endpoint delete`합니다.</span><span class="sxs-lookup"><span data-stu-id="fc509-134">Using hello example above, you can remove hello endpoint created for virtual machine "web1" from load balancer "lbset" using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> <span data-ttu-id="fc509-135">Hello 명령을 사용 하 여 더 많은 옵션 toomanage 끝점을 탐색할 수 있습니다.`azure vm endpoint --help`</span><span class="sxs-lookup"><span data-stu-id="fc509-135">You can explore more options toomanage endpoints using hello command `azure vm endpoint --help`</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc509-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fc509-136">Next steps</span></span>

[<span data-ttu-id="fc509-137">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="fc509-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="fc509-138">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="fc509-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="fc509-139">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="fc509-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
