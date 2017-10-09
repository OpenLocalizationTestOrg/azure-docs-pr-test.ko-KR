---
title: "클래식 Azure CLI aaaCreate는 내부 부하 분산 장치-| Microsoft Docs"
description: "Hello 클래식 배포 모델에서 사용 하 여 내부 부하 분산 장치 toocreate Azure CLI hello 하는 방법을 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: becbbbde-a118-4269-9444-d3153f00bf34
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: ef29dfda5f7a75a411bbabe8b688a31c6bf81113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a><span data-ttu-id="da9ba-103">내부 부하 분산 장치 (클래식) hello Azure CLI를 사용 하 여 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="da9ba-103">Get started creating an internal load balancer (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="da9ba-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="da9ba-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="da9ba-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="da9ba-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="da9ba-106">Cloud services</span><span class="sxs-lookup"><span data-stu-id="da9ba-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="da9ba-107">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="da9ba-108">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="da9ba-109">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="da9ba-110">너무 방법에 대해 알아봅니다[hello 리소스 관리자 모델을 사용 하 여 이러한 단계를 수행](load-balancer-get-started-ilb-arm-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="da9ba-111">toocreate는 내부 부하 분산 장치 가상 컴퓨터에 대 한 설정</span><span class="sxs-lookup"><span data-stu-id="da9ba-111">toocreate an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="da9ba-112">수행 해야 합니다는 내부 부하 분산 장치 설정 하 고 해당 트래픽 tooit 보낼 서버 hello toocreate, hello 다음:</span><span class="sxs-lookup"><span data-stu-id="da9ba-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you must do hello following:</span></span>

1. <span data-ttu-id="da9ba-113">내부 부하 분산의 부하 분산 된 집합의 hello 서버에 걸쳐 분산 된 들어오는 트래픽 toobe 부하의 hello 끝점 수 있는 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="da9ba-114">Hello 들어오는 트래픽을 받게 되 toohello 가상 컴퓨터를 해당 끝점을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="da9ba-115">송신할 hello 트래픽 toobe 부하 분산 된 toosend 해당 트래픽을 toohello 가상 IP (VIP) 인스턴스의 주소 hello 내부 부하 분산 하는 hello 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="da9ba-116">CLI를 사용하여 내부 부하 분산 장치 만들기 단계별 지침</span><span class="sxs-lookup"><span data-stu-id="da9ba-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="da9ba-117">이 가이드에서는 toocreate는 내부 부하 분산 장치에 따라 방법 위의 hello 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-117">This guide shows how toocreate an internal load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="da9ba-118">Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-118">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="da9ba-119">Hello 실행 **azure 구성 모드** 아래와 같이 명령 tooswitch tooclassic 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-119">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="da9ba-120">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="da9ba-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="da9ba-121">끝점과 부하 분산 장치 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="da9ba-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="da9ba-122">hello 시나리오 hello에서에서 가상 컴퓨터 "DB1" 및 "DB2" "mytestcloud" 이라는 클라우드 서비스를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-122">hello scenario assumes hello virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="da9ba-123">두 가상 컴퓨터는 서브넷 "subnet-1"과 함께 내 "testvnet"이라는 가상 네트워크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="da9ba-124">이 가이드를 통해 개인 포트로 포트 1433과 로컬 포트로 포트 1433을 사용하여 내부 부하 분산 장치 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="da9ba-125">SQL 가상 컴퓨터는 내부 부하 분산 장치 tooguarantee hello 데이터베이스 서버 공용 IP 주소를 사용 하 여 직접 노출 되지 않습니다 hello 백 엔드 사용에 있는 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-125">This is a common scenario where you have SQL virtual machines on hello back end using an internal load balancer tooguarantee hello database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="da9ba-126">1단계</span><span class="sxs-lookup"><span data-stu-id="da9ba-126">Step 1</span></span>

<span data-ttu-id="da9ba-127">`azure network service internal-load-balancer add`를 사용하여 내부 부하 분산 장치 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="da9ba-128">자세한 내용은 `azure service internal-load-balancer --help` 를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="da9ba-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="da9ba-129">Hello 명령을 사용 하 여 hello 내부 부하 분산 장치 속성을 확인할 수 있습니다 `azure service internal-load-balancer list` *클라우드 서비스 이름*합니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-129">You can check hello internal load balancer properties using hello command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="da9ba-130">여기 hello 출력의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-130">Here follows an example of hello output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="da9ba-131">2단계</span><span class="sxs-lookup"><span data-stu-id="da9ba-131">Step 2</span></span>

<span data-ttu-id="da9ba-132">Hello 첫 번째 끝점을 추가할 때 설정 하는 hello 내부 부하 분산 장치를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-132">You configure hello internal load balancer set when you add hello first endpoint.</span></span> <span data-ttu-id="da9ba-133">Hello 끝점, 가상 컴퓨터 및 프로브 포트 toohello 내부 부하 분산 집합에이 단계를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-133">You will associate hello endpoint, virtual machine and probe port toohello internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="da9ba-134">3단계</span><span class="sxs-lookup"><span data-stu-id="da9ba-134">Step 3</span></span>

<span data-ttu-id="da9ba-135">Hello 부하 분산 장치 사용 하 여 구성 확인 `azure vm show` *가상 컴퓨터 이름*</span><span class="sxs-lookup"><span data-stu-id="da9ba-135">Verify hello load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="da9ba-136">hello 출력이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-136">hello output will be:</span></span>

    azure vm show DB1
    info:    Executing command vm show
    + Getting virtual machines
    data:    DNSName "mytestcloud.cloudapp.net"
    data:    Location "East US 2"
    data:    VMName "DB1"
    data:    IPAddress "192.168.2.4"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "db1-DB1-0-201511120457370846"
    data:    OSDisk mediaLink "https://XXXX.blob.core.windows.net/vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "137.116.64.107"
    data:    VirtualIPAddresses 0 name "db1ContractContract"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    VirtualIPAddresses 1 address "192.168.2.7"
    data:    VirtualIPAddresses 1 name "ilbset"
    data:    Network Endpoints 0 localPort 5986
    data:    Network Endpoints 0 name "PowerShell"
    data:    Network Endpoints 0 port 5986
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 3389
    data:    Network Endpoints 1 name "Remote Desktop"
    data:    Network Endpoints 1 port 60173
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 1433
    data:    Network Endpoints 2 name "tcp-1433-1433"
    data:    Network Endpoints 2 port 1433
    data:    Network Endpoints 2 loadBalancerProbe port 1433
    data:    Network Endpoints 2 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 2 loadBalancerProbe intervalInSeconds 300
    data:    Network Endpoints 2 loadBalancerProbe timeoutInSeconds 600
    data:    Network Endpoints 2 protocol "tcp"
    data:    Network Endpoints 2 virtualIPAddress "192.168.2.7"
    data:    Network Endpoints 2 enableDirectServerReturn false
    data:    Network Endpoints 2 loadBalancerName "ilbset"
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="da9ba-137">가상 컴퓨터를 위한 원격 데스크톱 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="da9ba-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="da9ba-138">원격 데스크톱 끝점 tooforward 네트워크 트래픽을 사용 하 여 특정 가상 컴퓨터에 대 한 공용 포트 tooa 로컬 포트를 만들 수 있습니다 `azure vm endpoint create`합니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-138">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="da9ba-139">부하 분산 장치에서 가상 컴퓨터 제거</span><span class="sxs-lookup"><span data-stu-id="da9ba-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="da9ba-140">연결 된 hello 끝점을 삭제 하 여 설정 하는 내부 부하 분산 장치에서 가상 컴퓨터를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-140">You can remove a virtual machine from an internal load balancer set by deleting hello associated endpoint.</span></span> <span data-ttu-id="da9ba-141">Hello 끝점 기능이 제거 되 면 hello 가상 컴퓨터가 부하 분산 집합을 더 이상을 toohello 속해 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-141">Once hello endpoint is removed, hello virtual machine won't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="da9ba-142">위의 hello 예제를 사용 하 여에서 제거할 수 있습니다 "DB1" 가상 컴퓨터에 대해 만든 hello 끝점 내부 부하 분산 장치 "ilbset" hello 명령을 사용 하 여 `azure vm endpoint delete`합니다.</span><span class="sxs-lookup"><span data-stu-id="da9ba-142">Using hello example above, you can remove hello endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="da9ba-143">자세한 내용은 `azure vm endpoint --help` 를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="da9ba-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da9ba-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da9ba-144">Next steps</span></span>

[<span data-ttu-id="da9ba-145">원본 IP 선호도를 사용하여 부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="da9ba-145">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="da9ba-146">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="da9ba-146">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
