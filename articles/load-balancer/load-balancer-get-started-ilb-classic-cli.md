---
title: "내부 부하 분산 장치 만들기 - Azure CLI 클래식 | Microsoft Docs"
description: "Azure CLI를 사용하여 클래식 배포 모델에서 내부 부하 분산 장치를 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: d24b95f75b5ffd1116b07cf9f8bac33767a9c835
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-the-azure-cli"></a><span data-ttu-id="c0b8f-103">Azure CLI를 사용하여 내부 부하 분산 장치(클래식) 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="c0b8f-103">Get started creating an internal load balancer (classic) using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0b8f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0b8f-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="c0b8f-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c0b8f-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="c0b8f-106">Cloud services</span><span class="sxs-lookup"><span data-stu-id="c0b8f-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="c0b8f-107">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="c0b8f-108">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="c0b8f-109">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="c0b8f-110">[Resource Manager 모델을 사용하여 이러한 단계를 수행하는](load-balancer-get-started-ilb-arm-cli.md) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="to-create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="c0b8f-111">가상 컴퓨터에 대한 내부 부하 분산 장치 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="c0b8f-111">To create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="c0b8f-112">내부 부하 분산 장치 집합과 이 집합으로 해당 트래픽을 전송할 서버를 만들려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-112">To create an internal load balancer set and the servers that will send their traffic to it, you must do the following:</span></span>

1. <span data-ttu-id="c0b8f-113">부하 분산 집합의 서버 간에 부하가 분산될 들어오는 트래픽의 끝점이 되는 내부 부하 분산의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-113">Create an instance of Internal Load Balancing that will be the endpoint of incoming traffic to be load balanced across the servers of a load-balanced set.</span></span>
2. <span data-ttu-id="c0b8f-114">들어오는 트래픽을 수신할 가상 컴퓨터에 해당하는 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-114">Add endpoints corresponding to the virtual machines that will be receiving the incoming traffic.</span></span>
3. <span data-ttu-id="c0b8f-115">부하가 분산될 트래픽을 전송하는 서버가 해당 트래픽을 내부 부하 분산 인스턴스의 VIP(가상 IP) 주소로 전송하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-115">Configure the servers that will be sending the traffic to be load balanced to send their traffic to the virtual IP (VIP) address of the Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="c0b8f-116">CLI를 사용하여 내부 부하 분산 장치 만들기 단계별 지침</span><span class="sxs-lookup"><span data-stu-id="c0b8f-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="c0b8f-117">이 가이드에서는 위의 시나리오에 따라 내부 부하 분산 장치를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-117">This guide shows how to create an internal load balancer based on the scenario above.</span></span>

1. <span data-ttu-id="c0b8f-118">Azure CLI를 처음 사용하는 경우 [Azure CLI 설치 및 구성](../cli-install-nodejs.md) 을 참조하고 Azure 계정 및 구독을 선택하는 부분까지 관련 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-118">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="c0b8f-119">아래와 같이 **azure config mode** 명령을 실행하여 클래식 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-119">Run the **azure config mode** command to switch to classic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="c0b8f-120">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="c0b8f-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="c0b8f-121">끝점과 부하 분산 장치 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="c0b8f-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="c0b8f-122">시나리오는 "mytestcloud"라는 클라우드 서비스에 가상 컴퓨터 "DB1" 및 "DB2"가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-122">The scenario assumes the virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="c0b8f-123">두 가상 컴퓨터는 서브넷 "subnet-1"과 함께 내 "testvnet"이라는 가상 네트워크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="c0b8f-124">이 가이드를 통해 개인 포트로 포트 1433과 로컬 포트로 포트 1433을 사용하여 내부 부하 분산 장치 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="c0b8f-125">이는 일반적인 시나리오로, 백 엔드의 SQL 가상 컴퓨터는 데이터베이스 서버가 공용 IP 주소를 사용하여 직접 노출되지 않는다는 것을 보장하기 위해 내부 부하 분산 장치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-125">This is a common scenario where you have SQL virtual machines on the back end using an internal load balancer to guarantee the database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="c0b8f-126">1단계</span><span class="sxs-lookup"><span data-stu-id="c0b8f-126">Step 1</span></span>

<span data-ttu-id="c0b8f-127">`azure network service internal-load-balancer add`를 사용하여 내부 부하 분산 장치 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="c0b8f-128">자세한 내용은 `azure service internal-load-balancer --help` 를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="c0b8f-129">`azure service internal-load-balancer list` *클라우드 서비스 이름*명령을 사용하여 내부 부하 분산 장치 속성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-129">You can check the internal load balancer properties using the command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="c0b8f-130">다음은 출력의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-130">Here follows an example of the output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="c0b8f-131">2단계</span><span class="sxs-lookup"><span data-stu-id="c0b8f-131">Step 2</span></span>

<span data-ttu-id="c0b8f-132">첫 번째 끝점을 추가할 때 내부 부하 분산 장치 집합을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-132">You configure the internal load balancer set when you add the first endpoint.</span></span> <span data-ttu-id="c0b8f-133">이 단계에서 끝점, 가상 컴퓨터 및 프로브 포트를 내부 부하 분산 장치 집합에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-133">You will associate the endpoint, virtual machine and probe port to the internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="c0b8f-134">3단계</span><span class="sxs-lookup"><span data-stu-id="c0b8f-134">Step 3</span></span>

<span data-ttu-id="c0b8f-135">`azure vm show` *가상 컴퓨터 이름*</span><span class="sxs-lookup"><span data-stu-id="c0b8f-135">Verify the load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="c0b8f-136">다음과 같이 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-136">The output will be:</span></span>

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

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="c0b8f-137">가상 컴퓨터를 위한 원격 데스크톱 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="c0b8f-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="c0b8f-138">`azure vm endpoint create`을 사용하여 특정 가상 컴퓨터의 공용 포트에서 로컬 포트로 네트워크 트래픽을 전달하는 원격 데스크톱 끝점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-138">You can create a remote desktop endpoint to forward network traffic from a public port to a local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="c0b8f-139">부하 분산 장치에서 가상 컴퓨터 제거</span><span class="sxs-lookup"><span data-stu-id="c0b8f-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="c0b8f-140">연결된 된 끝점을 삭제하여 내부 부하 분산 장치 집합에서 가상 컴퓨터를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-140">You can remove a virtual machine from an internal load balancer set by deleting the associated endpoint.</span></span> <span data-ttu-id="c0b8f-141">끝점이 제거되면 가상 컴퓨터는 더 이상 부하 분산 장치 집합에 속하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-141">Once the endpoint is removed, the virtual machine won't belong to the load balancer set anymore.</span></span>

<span data-ttu-id="c0b8f-142">위의 예제를 통해 명령 `azure vm endpoint delete`를 사용하여 내부 부하 분산 장치 "lbset"에서 가상 컴퓨터 "DB1"을 위해 만들어진 끝점을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-142">Using the example above, you can remove the endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using the command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="c0b8f-143">자세한 내용은 `azure vm endpoint --help` 를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="c0b8f-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0b8f-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c0b8f-144">Next steps</span></span>

[<span data-ttu-id="c0b8f-145">원본 IP 선호도를 사용하여 부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="c0b8f-145">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="c0b8f-146">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="c0b8f-146">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
