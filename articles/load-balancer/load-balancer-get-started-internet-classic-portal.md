---
title: "aaaCreate 인터넷 연결 부하 분산 장치-클래식 Azure 포털 | Microsoft Docs"
description: "인터넷 연결 부하 분산 장치에 사용 하 여 클래식 배포 모델 toocreate Azure 클래식 포털 hello 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a><span data-ttu-id="e4565-103">경우에 인터넷 연결 hello Azure 클래식 포털에서에서 부하 분산 장치 (클래식)를 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="e4565-103">Get started creating an Internet facing load balancer (classic) in hello Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4565-104">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="e4565-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="e4565-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4565-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="e4565-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e4565-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="e4565-107">Azure 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="e4565-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="e4565-108">Azure 리소스를 사용 하기 전에 Azure에 현재 두 가지 배포 모델에 중요 한 toounderstand: Azure 리소스 관리자 및 기본 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="e4565-109">Azure 리소스로 작업하기 전에 [배포 모델 및 도구](../azure-classic-rm.md) 를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="e4565-110">이 문서의 hello 위쪽 hello 탭을 클릭 하 여 다양 한 도구에 대 한 hello 설명서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="e4565-111">이 문서에서는 hello 클래식 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="e4565-112">수도 있습니다 [toocreate 인터넷 연결 로드 분산 장치는 Azure 리소스 관리자를 사용 하는 방법에 대해 알아봅니다](load-balancer-get-started-internet-arm-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="e4565-113">가상 컴퓨터에 대한 인터넷 연결 부하 분산 장치 설정</span><span class="sxs-lookup"><span data-stu-id="e4565-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="e4565-114">순서 tooload 분산할 네트워크 트래픽 hello 인터넷 hello 가상 컴퓨터 클라우드 서비스의 사이에서 부하 분산 된 집합을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-114">In order tooload balance network traffic from hello Internet across hello virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="e4565-115">이 절차에서는 hello 가상 컴퓨터를 이미 만들었다고 있고 이들이 모두 hello 내에서 동일한 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-115">This procedure assumes that you have already created hello virtual machines and that they are all within hello same cloud service.</span></span>

<span data-ttu-id="e4565-116">**가상 컴퓨터에 대 한 부하 분산 집합 tooconfigure**</span><span class="sxs-lookup"><span data-stu-id="e4565-116">**tooconfigure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="e4565-117">Hello Azure 클래식 포털에서에서 클릭 **가상 컴퓨터**, hello 부하 분산 집합에 가상 컴퓨터의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-117">In hello Azure classic portal, click **Virtual Machines**, and then click hello name of a virtual machine in hello load-balanced set.</span></span>
2. <span data-ttu-id="e4565-118">**끝점**을 클릭한 후 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="e4565-119">Hello에 **끝점 tooa 가상 컴퓨터 추가** 페이지 hello 오른쪽 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-119">On hello **Add an endpoint tooa virtual machine** page, click hello right arrow.</span></span>
4. <span data-ttu-id="e4565-120">Hello에 **hello 끝점의 hello 세부 정보 지정** 페이지:</span><span class="sxs-lookup"><span data-stu-id="e4565-120">On hello **Specify hello details of hello endpoint** page:</span></span>

   * <span data-ttu-id="e4565-121">**이름**, hello 끝점에 대 한 이름을 입력 하거나 일반 프로토콜에 대해 미리 정의 된 끝점의 hello 목록에서 hello 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-121">In **Name**, type a name for hello endpoint or select hello name from hello list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="e4565-122">**프로토콜**, 필요에 따라 TCP 또는 UDP 끝점의 hello 유형에 필요한 hello 프로토콜을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-122">In **Protocol**, select hello protocol required by hello type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="e4565-123">**공용 포트 및 개인 포트**, 원하는 가상 컴퓨터 toouse hello 필요에 따라 hello 포트 번호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-123">In **Public Port and Private Port**, type hello port numbers that you want hello virtual machine toouse, as needed.</span></span> <span data-ttu-id="e4565-124">응용 프로그램에 대 한 적절 한 방식으로 가상 컴퓨터 tooredirect 트래픽을 hello hello 개인 포트 및 방화벽 규칙을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-124">You can use hello private port and firewall rules on hello virtual machine tooredirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="e4565-125">hello 개인 포트는 hello 공용 포트와 동일한 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-125">hello private port can be hello same as hello public port.</span></span> <span data-ttu-id="e4565-126">예를 들어 웹 (HTTP) 트래픽에 대 한 끝점에 대 한 포트 80 tooboth hello 공용 및 개인 포트를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 tooboth hello public and private port.</span></span>

5. <span data-ttu-id="e4565-127">선택 **부하 분산 된 집합을 만들**, 다음 hello 오른쪽 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-127">Select **Create a load-balanced set**, and then click hello right arrow.</span></span>
6. <span data-ttu-id="e4565-128">Hello에 **hello 부하 분산 된 집합 구성** 페이지 hello 부하 분산 집합에 대 한 이름을 입력 한 다음 hello의 hello Azure 부하 분산 장치 프로브 동작 값을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-128">On hello **Configure hello load-balanced set** page, type a name for hello load-balanced set, and then assign hello values for probe behavior of hello Azure Load Balancer.</span></span> <span data-ttu-id="e4565-129">hello 부하 분산 집합의 hello 가상 컴퓨터는 사용할 수 있는 tooreceive 들어오는 트래픽을 hello 부하 분산 장치 프로브 toodetermine를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-129">hello Load Balancer uses probes toodetermine if hello virtual machines in hello load-balanced set are available tooreceive incoming traffic.</span></span>
7. <span data-ttu-id="e4565-130">Hello 확인 표시가 toocreate hello 부하 분산 끝점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-130">Click hello check mark toocreate hello load-balanced endpoint.</span></span> <span data-ttu-id="e4565-131">나타납니다 **예** hello에 **부하 분산 집합 이름이** hello 열 **끝점** hello 가상 컴퓨터에 대 한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-131">You will see **Yes** in hello **Load-balanced set name** column of hello **Endpoints** page for hello virtual machine.</span></span>
8. <span data-ttu-id="e4565-132">Hello 포털에서 클릭 **가상 컴퓨터**hello 부하 분산 된 집합에 추가 가상 컴퓨터의 hello 이름을 클릭 하 고 **끝점**, 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-132">In hello portal, click **Virtual Machines**, click hello name of an additional virtual machine in hello load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="e4565-133">Hello에 **끝점 tooa 가상 컴퓨터 추가** 페이지 **끝점 tooan 기존 부하 분산 집합을 추가**hello 부하 분산 된 집합의 hello 이름을 선택한 다음 hello 오른쪽 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-133">On hello **Add an endpoint tooa virtual machine** page, click **Add endpoint tooan existing load-balanced set**, select hello name of hello load-balanced set, and then click hello right arrow.</span></span>
10. <span data-ttu-id="e4565-134">Hello에 **hello 끝점의 hello 세부 정보 지정** 페이지 hello 끝점에 대 한 이름을 입력 한 다음 hello 확인 표시를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-134">On hello **Specify hello details of hello endpoint** page, type a name for hello endpoint, and then click hello check mark.</span></span>

<span data-ttu-id="e4565-135">Hello 추가 가상 컴퓨터의 hello 부하 분산 된 집합의 경우 8 ~ 10 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4565-135">For hello additional virtual machines in hello load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4565-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e4565-136">Next steps</span></span>

[<span data-ttu-id="e4565-137">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="e4565-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="e4565-138">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="e4565-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="e4565-139">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="e4565-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
