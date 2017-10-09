---
title: "Azure 클라우드 서비스에 대 한 부하 분산 장치는 인터넷 연결 aaaCreate | Microsoft Docs"
description: "인터넷 연결 toocreate 분산 장치 클라우드 서비스에 대 한 클래식 배포 모델에 로드 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 0bb16f96-56a6-429f-88f5-0de2d0136756
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d93cf76d417cbfc744cf07ba48c43a63cc14df69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a><span data-ttu-id="72c52-103">클라우드 서비스를 위한 인터넷 연결 부하 분산 장치 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="72c52-103">Get started creating an Internet facing load balancer for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="72c52-104">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="72c52-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="72c52-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72c52-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="72c52-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="72c52-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="72c52-107">Azure 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="72c52-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="72c52-108">Azure 리소스를 사용 하기 전에 Azure에 현재 두 가지 배포 모델에 중요 한 toounderstand: Azure 리소스 관리자 및 기본 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="72c52-109">Azure 리소스로 작업하기 전에 [배포 모델 및 도구](../azure-classic-rm.md) 를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="72c52-110">이 문서의 hello 위쪽 hello 탭을 클릭 하 여 다양 한 도구에 대 한 hello 설명서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="72c52-111">이 문서에서는 hello 클래식 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="72c52-112">수도 있습니다 [toocreate 인터넷 연결 로드 분산 장치는 Azure 리소스 관리자를 사용 하는 방법에 대해 알아봅니다](load-balancer-get-started-internet-arm-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

<span data-ttu-id="72c52-113">클라우드 서비스는 자동으로 부하 분산 장치 구성 및 hello 서비스 모델을 통해 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-113">Cloud services are automatically configured with a load balancer and can be customized via hello service model.</span></span>

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a><span data-ttu-id="72c52-114">Hello 서비스 정의 파일을 사용 하 여 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="72c52-114">Create a load balancer using hello service definition file</span></span>

<span data-ttu-id="72c52-115">클라우드 서비스에 대 한.NET 2.5 tooupdate hello Azure SDK를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-115">You can leverage hello Azure SDK for .NET 2.5 tooupdate your cloud service.</span></span> <span data-ttu-id="72c52-116">클라우드 서비스에 대 한 끝점 설정 hello 내용이 [서비스 정의](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-116">Endpoint settings for cloud services are made in hello [service definition](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef file.</span></span>

<span data-ttu-id="72c52-117">hello 다음 예제는 클라우드 배포에 대 한 servicedefinition.csdef 파일은 구성 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="72c52-117">hello following example shows how a servicedefinition.csdef file for a cloud deployment is configured:</span></span>

<span data-ttu-id="72c52-118">클라우드 배포에서 생성 된 hello.csdef 파일에 대 한 hello 조각 검사 hello 구성 된 외부 끝점이 toouse 포트 HTTP 포트 10000, 10001, 및 10002에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-118">Checking hello snippet for hello .csdef file generated by a cloud deployment, you can see hello external endpoint configured toouse ports HTTP on port 10000, 10001, and 10002.</span></span>

```xml
<ServiceDefinition name=“Tenant“>
    <WorkerRole name=“FERole” vmsize=“Small“>
<Endpoints>
    <InputEndpoint name=“FE_External_Http” protocol=“http” port=“10000“ />
    <InputEndpoint name=“FE_External_Tcp“  protocol=“tcp“  port=“10001“ />
    <InputEndpoint name=“FE_External_Udp“  protocol=“udp“  port=“10002“ />

    <InputEndpointname=“HTTP_Probe” protocol=“http” port=“80” loadBalancerProbe=“MyProbe“ />

    <InstanceInputEndpoint name=“InstanceEP” protocol=“tcp” localPort=“80“>
        <AllocatePublicPortFrom>
            <FixedPortRange min=“10110” max=“10120“  />
        </AllocatePublicPortFrom>
    </InstanceInputEndpoint>
    <InternalEndpoint name=“FE_InternalEP_Tcp” protocol=“tcp“ />
</Endpoints>
    </WorkerRole>
</ServiceDefinition>
```

## <a name="check-load-balancer-health-status-for-cloud-services"></a><span data-ttu-id="72c52-119">클라우드 서비스에 대한 부하 분산 장치 상태 확인</span><span class="sxs-lookup"><span data-stu-id="72c52-119">Check load balancer health status for cloud services</span></span>

<span data-ttu-id="72c52-120">hello 다음은 상태 검색의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-120">hello following is an example of a health probe:</span></span>

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

<span data-ttu-id="72c52-121">hello 부하 분산 장치 결합 하 여 hello 끝점의 hello 정보와 hello 프로브 toocreate의 hello 정보 hello 형식의 URL `http://{DIP of VM}:80/Probe.aspx` hello 서비스의 hello 상태를 사용 하는 tooquery 일 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-121">hello load balancer combines hello information of hello endpoint and hello information of hello probe toocreate a URL in hello form of `http://{DIP of VM}:80/Probe.aspx` that can be used tooquery hello health of hello service.</span></span>

<span data-ttu-id="72c52-122">hello 서비스에서 검색 주기 프로브 hello에서 동일한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-122">hello service detects periodic probes from hello same IP address.</span></span> <span data-ttu-id="72c52-123">Hello 가상 컴퓨터가 실행 되 고 hello 노드의 hello 호스트에서 들어오는 hello 상태 프로브 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-123">This is hello health probe request coming from hello host of hello node where hello virtual machine is running.</span></span> <span data-ttu-id="72c52-124">hello 서비스는 hello 부하 분산 장치 tooassume hello 서비스가 정상 임을 대 한 HTTP 200 상태 코드로 toorespond에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-124">hello service has toorespond with a HTTP 200 status code for hello load balancer tooassume that hello service is healthy.</span></span> <span data-ttu-id="72c52-125">다른 모든 HTTP 상태는 hello 순환 순서에서 가상 컴퓨터는 직접 (예: 503) 코드.</span><span class="sxs-lookup"><span data-stu-id="72c52-125">Any other HTTP status code (for example 503) directly takes hello virtual machine out of rotation.</span></span>

<span data-ttu-id="72c52-126">또한 hello 프로브 정의 hello hello 프로브 빈도 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-126">hello probe definition also controls hello frequency of hello probe.</span></span> <span data-ttu-id="72c52-127">경우에 위의 hello 부하 분산 장치는 hello 끝점 마다 5 초를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-127">In our case above, hello load balancer is probing hello endpoint every 5 secs.</span></span> <span data-ttu-id="72c52-128">No로 대답 양의 10 초 (두 개의 프로브 간격) 동안 수신 되 면 hello 프로브 다운 가정 하 고 hello 가상 컴퓨터 순환 순서에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-128">If no positive answer is received for 10 secs (two probe intervals), hello probe is assumed down, and hello virtual machine is taken out of rotation.</span></span> <span data-ttu-id="72c52-129">마찬가지로, 회전 hello 서비스는 양의 응답을 받을 경우 hello 서비스 다시 배치는 toorotation 바로 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-129">Similarly, if hello service is out of rotation and a positive answer is received, hello service is put back toorotation right away.</span></span> <span data-ttu-id="72c52-130">Hello 서비스는 변동이 간의 정상 및 비정상을 하는 경우 hello 부하 분산 장치 프로브 수에 대 한 정상까지 hello 서비스 백 toorotation toodelay hello 다시 도입을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-130">If hello service is fluctuating between healthy and unhealthy, hello load balancer can decide toodelay hello re-introduction of hello service back toorotation until it has been healthy for a number of probes.</span></span>

<span data-ttu-id="72c52-131">Hello에 대 한 hello 서비스 정의 스키마를 확인 [상태 프로브](https://msdn.microsoft.com/library/azure/jj151530.aspx) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c52-131">Check hello service definition schema for hello [health probe](https://msdn.microsoft.com/library/azure/jj151530.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72c52-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="72c52-132">Next steps</span></span>

[<span data-ttu-id="72c52-133">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="72c52-133">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="72c52-134">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="72c52-134">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="72c52-135">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="72c52-135">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

