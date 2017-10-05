---
title: "Azure Cloud Services에 대한 내부 부하 분산 장치 만들기 | Microsoft Docs"
description: "클래식 배포 모델에서 PowerShell을 사용하여 내부 부하 분산 장치를 만드는 방법에 대해 알아봅니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 8dbc951416d577fa7f534c2eab1605c6bee61fce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a><span data-ttu-id="31fcc-103">클라우드 서비스를 위한 내부 부하 분산 장치(클래식) 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="31fcc-103">Get started creating an internal load balancer (classic) for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="31fcc-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31fcc-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="31fcc-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="31fcc-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="31fcc-106">Cloud services</span><span class="sxs-lookup"><span data-stu-id="31fcc-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> <span data-ttu-id="31fcc-107">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="31fcc-108">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="31fcc-109">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="31fcc-110">[Resource Manager 모델을 사용하여 이러한 단계를 수행하는](load-balancer-get-started-ilb-arm-ps.md) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

## <a name="configure-internal-load-balancer-for-cloud-services"></a><span data-ttu-id="31fcc-111">클라우드 서비스에 대한 내부 부하 분산 장치 구성하기</span><span class="sxs-lookup"><span data-stu-id="31fcc-111">Configure internal load balancer for cloud services</span></span>

<span data-ttu-id="31fcc-112">내부 부하 분산 장치는 가상 컴퓨터 및 클라우드 서비스를 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-112">Internal load balancer is supported for both virtual machines and cloud services.</span></span> <span data-ttu-id="31fcc-113">지역 가상 네트워크 외부에 있는 클라우드 서비스에 생성된 내부 부하 분산 장치 끝점은 해당 클라우드 서비스 내에서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-113">An internal load balancer endpoint created in a cloud service that is outside a regional virtual network will be accessible only within the cloud service.</span></span>

<span data-ttu-id="31fcc-114">아래 샘플에 나와 있는 것처럼 클라우드 서비스에서 첫 번째 배포를 만드는 동안 내부 부하 분산 장치 구성을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-114">The internal load balancer configuration has to be set during the creation of the first deployment in the cloud service, as shown in the sample below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31fcc-115">아래 단계를 실행하려면 클라우드 배포를 위해 가상 네트워크를 반드시 미리 만들어 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-115">A prerequisite to run the steps below is to have a virtual network already created for the cloud deployment.</span></span> <span data-ttu-id="31fcc-116">내부 부하 분산을 만들려면 가상 네트워크 이름 및 서브넷 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-116">You will need the virtual network name and subnet name to create the Internal Load Balancing.</span></span>

### <a name="step-1"></a><span data-ttu-id="31fcc-117">1단계</span><span class="sxs-lookup"><span data-stu-id="31fcc-117">Step 1</span></span>

<span data-ttu-id="31fcc-118">Visual Studio에서 클라우드 배포용 서비스 구성 파일(.cscfg)을 열고 다음 섹션을 추가하여 네트워크 구성을 위해 마지막 "`</Role>`" 항목 아래에 내부 부하 분산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-118">Open the service configuration file (.cscfg) for your cloud deployment in Visual Studio and add the following section to create the Internal Load Balancing under the last "`</Role>`" item for the network configuration.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of the load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="31fcc-119">어떻게 표시되는지 나타내기 위해 네트워크 구성 파일에 대한 값을 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-119">Let's add the values for the network configuration file to show how it will look.</span></span> <span data-ttu-id="31fcc-120">예제에서는 test_subnet이라는 10.0.0.0/24 서브넷과 10.0.0.4 고정 IP를 사용하는 "test_vnet"이라는 VNet을 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-120">In the example, assume you created a VNet called "test_vnet" with a subnet 10.0.0.0/24 called test_subnet and a static IP 10.0.0.4.</span></span> <span data-ttu-id="31fcc-121">부하 분산 장치의 이름은 testLB입니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-121">The load balancer will be named testLB.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="31fcc-122">부하 분산 장치 스키마에 대한 자세한 내용은 [부하 분산 장치 추가](https://msdn.microsoft.com/library/azure/dn722411.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31fcc-122">For more information about the load balancer schema, see [Add load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span></span>

### <a name="step-2"></a><span data-ttu-id="31fcc-123">2단계</span><span class="sxs-lookup"><span data-stu-id="31fcc-123">Step 2</span></span>

<span data-ttu-id="31fcc-124">내부 부하 분산에 끝점을 추가하려면 서비스 정의(.csdef) 파일을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-124">Change the service definition (.csdef) file to add endpoints to the Internal Load Balancing.</span></span> <span data-ttu-id="31fcc-125">역할 인스턴스가 만들어지는 순간 서비스 정의 파일이 내부 부하 분산에 역할 인스턴스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-125">The moment a role instance is created, the service definition file will add the role instances to the Internal Load Balancing.</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="31fcc-126">위의 예제에서 나온 동일한 값을 따라 서비스 정의 파일에 값을 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-126">Following the same values from the example above, let's add the values to the service definition file.</span></span>

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="31fcc-127">들어오는 요청의 경우 포트 80을 사용하는 testLB 부하 분산 장치를 통해 네트워크 트래픽 부하가 분산되며 포트 80의 작업자 역할 인스턴스에도 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="31fcc-127">The network traffic will be load balanced using the testLB load balancer using port 80 for incoming requests, sending to worker role instances also on port 80.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31fcc-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31fcc-128">Next steps</span></span>

[<span data-ttu-id="31fcc-129">원본 IP 선호도를 사용하여 부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="31fcc-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="31fcc-130">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="31fcc-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

