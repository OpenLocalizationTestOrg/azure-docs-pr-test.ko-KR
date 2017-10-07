---
title: "Azure 앱 서비스 환경 aaaUse"
description: "Toocreate, 게시 하 고 앱에서 Azure 앱 서비스 환경 크기를 조정 하는 방법"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a22450c4-9b8b-41d4-9568-c4646f4cf66b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 30c89e384efc07c560254856c0ca7d4eb4b1f010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-app-service-environment"></a><span data-ttu-id="931b0-103">App Service Environment 사용</span><span class="sxs-lookup"><span data-stu-id="931b0-103">Use an App Service environment</span></span> #

## <a name="overview"></a><span data-ttu-id="931b0-104">개요</span><span class="sxs-lookup"><span data-stu-id="931b0-104">Overview</span></span> ##

<span data-ttu-id="931b0-105">Azure App Service Environment는 Azure App Service를 고객의 Azure Virtual Network에 있는 서브넷에 배포한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-105">Azure App Service Environment is a deployment of Azure App Service into a subnet in a customer’s Azure virtual network.</span></span> <span data-ttu-id="931b0-106">ASE는 다음으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-106">It consists of:</span></span>

- <span data-ttu-id="931b0-107">**프런트 엔드**: hello 프런트 엔드는 앱 서비스 환경 (ASE)에서 HTTP/HTTPS 종료 되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-107">**Front ends**: hello front ends are where HTTP/HTTPS terminates in an App Service environment (ASE).</span></span>
- <span data-ttu-id="931b0-108">**작업자**: hello 작업자는 앱을 호스트 하는 hello 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-108">**Workers**: hello workers are hello resources that host your apps.</span></span>
- <span data-ttu-id="931b0-109">**데이터베이스**: hello 데이터베이스 hello 환경을 정의 하는 정보를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-109">**Database**: hello database holds information that defines hello environment.</span></span>
- <span data-ttu-id="931b0-110">**저장소**: hello 저장소에 사용 되는 toohost hello 고객 게시 된 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-110">**Storage**: hello storage is used toohost hello customer-published apps.</span></span>

> [!NOTE]
> <span data-ttu-id="931b0-111">App Service Environment에는 두 가지 버전(ASEv1 및 ASEv2)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-111">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="931b0-112">ASEv1, 사용 하기 전에 hello 리소스를 관리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-112">In ASEv1, you must manage hello resources before you can use them.</span></span> <span data-ttu-id="931b0-113">toolearn 어떻게 tooconfigure ASEv1 관리, 참조 및 [앱 서비스 환경 v1 구성][ConfigureASEv1]합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-113">toolearn how tooconfigure and manage ASEv1, see [Configure an App Service environment v1][ConfigureASEv1].</span></span> <span data-ttu-id="931b0-114">이 문서의 나머지 부분 hello ASEv2에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-114">hello rest of this article focuses on ASEv2.</span></span>
>
>

<span data-ttu-id="931b0-115">앱 액세스를 위한 외부 또는 내부 VIP로 ASE(ASEv1 및 ASEv2)를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-115">You can deploy an ASE (ASEv1 and ASEv2) with an external or internal VIP for app access.</span></span> <span data-ttu-id="931b0-116">외부 VIP 사용 하는 hello 배포는 일반적으로 외부 ASE는 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-116">hello deployment with an external VIP is commonly called an External ASE.</span></span> <span data-ttu-id="931b0-117">내부 부하 분산 장치 ILB ()를 사용 하기 때문에 내부 버전 hello ILB ASE hello를 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-117">hello internal version is called hello ILB ASE because it uses an internal load balancer (ILB).</span></span> <span data-ttu-id="931b0-118">toolearn ILB ASE hello에 대 한 자세한 참조 [만들고 ILB ASE를 사용 하 여][MakeILBASE]합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-118">toolearn more about hello ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span>

## <a name="create-a-web-app-in-an-ase"></a><span data-ttu-id="931b0-119">ASE에서 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="931b0-119">Create a web app in an ASE</span></span> ##

<span data-ttu-id="931b0-120">toocreate ASE에 웹 앱을 사용 하면 동일한 프로세스 hello 작은 몇 가지 차이점이 있지만 만들 때 일반적으로.</span><span class="sxs-lookup"><span data-stu-id="931b0-120">toocreate a web app in an ASE, you use hello same process as when you create it normally, but with a few small differences.</span></span> <span data-ttu-id="931b0-121">새 App Service 계획을 만들 때는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-121">When you create a new App Service plan:</span></span>

- <span data-ttu-id="931b0-122">지리적 위치는 toodeploy에 앱을 선택 하는 대신 사용자의 위치를 ASE를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-122">Instead of choosing a geographic location in which toodeploy your app, you choose an ASE as your location.</span></span>
- <span data-ttu-id="931b0-123">ASE에서 만들어진 모든 App Service 계획은 격리 가격 책정 계층에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-123">All App Service plans created in an ASE must be in an Isolated pricing tier.</span></span>

<span data-ttu-id="931b0-124">ASE를 설정 하지 않은 경우 hello 지침에 따라 하나를 만들 수 있습니다 [앱 서비스 환경 만들기][MakeExternalASE]합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-124">If you don't have an ASE, you can create one by following hello instructions in [Create an App Service environment][MakeExternalASE].</span></span>

<span data-ttu-id="931b0-125">toocreate ASE에 웹 앱:</span><span class="sxs-lookup"><span data-stu-id="931b0-125">toocreate a web app in an ASE:</span></span>

1. <span data-ttu-id="931b0-126">**새로 만들기**  > **웹 + 모바일** > **웹앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-126">Select **New** > **Web + Mobile** > **Web App**.</span></span>

2. <span data-ttu-id="931b0-127">Hello 웹 앱에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-127">Enter a name for hello web app.</span></span> <span data-ttu-id="931b0-128">이미 ASE에 앱 서비스 계획을 선택 하는 경우 hello 앱에 대 한 도메인 이름을 hello hello ASE의 hello 도메인 이름을 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-128">If you already selected an App Service plan in an ASE, hello domain name for hello app reflects hello domain name of hello ASE.</span></span>

    ![웹앱 이름 선택][1]

3. <span data-ttu-id="931b0-130">구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-130">Select a subscription.</span></span>

4. <span data-ttu-id="931b0-131">새 리소스 그룹에 대 한 이름을 입력 하거나 선택 **기존 항목 사용** hello 드롭 다운 목록에서 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-131">Enter a name for a new resource group, or select **Use existing** and select one from hello drop-down list.</span></span>

5. <span data-ttu-id="931b0-132">ASE에서 기존 App Service 계획을 선택하거나 다음 단계를 통해 새 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-132">Select an existing App Service plan in your ASE, or create a new one by following these steps:</span></span>

    <span data-ttu-id="931b0-133">a.</span><span class="sxs-lookup"><span data-stu-id="931b0-133">a.</span></span> <span data-ttu-id="931b0-134">**새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-134">Select **Create New**.</span></span>

    <span data-ttu-id="931b0-135">b.</span><span class="sxs-lookup"><span data-stu-id="931b0-135">b.</span></span> <span data-ttu-id="931b0-136">앱 서비스 계획에 대 한 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-136">Enter hello name for your App Service plan.</span></span>

    <span data-ttu-id="931b0-137">c.</span><span class="sxs-lookup"><span data-stu-id="931b0-137">c.</span></span> <span data-ttu-id="931b0-138">Hello에 프로그램 ASE 선택 **위치** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-138">Select your ASE in hello **Location** drop-down list.</span></span>

    <span data-ttu-id="931b0-139">d.</span><span class="sxs-lookup"><span data-stu-id="931b0-139">d.</span></span> <span data-ttu-id="931b0-140">**격리** 가격 책정 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-140">Select an **Isolated** pricing tier.</span></span> <span data-ttu-id="931b0-141">**선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-141">Select **Select**.</span></span>

    <span data-ttu-id="931b0-142">e.</span><span class="sxs-lookup"><span data-stu-id="931b0-142">e.</span></span> <span data-ttu-id="931b0-143">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-143">Select **OK**.</span></span>
    
    ![격리 가격 책정 계층][2]

6. <span data-ttu-id="931b0-145">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-145">Select **Create**.</span></span>

## <a name="how-scale-works"></a><span data-ttu-id="931b0-146">확장이 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="931b0-146">How scale works</span></span> ##

<span data-ttu-id="931b0-147">모든 App Service 앱은 App Service 계획에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-147">Every App Service app runs in an App Service plan.</span></span> <span data-ttu-id="931b0-148">hello 컨테이너 모델은 환경 앱 서비스 계획을 보유 하 고 앱 서비스 계획을 응용 프로그램을 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-148">hello container model is environments hold App Service plans, and App Service plans hold apps.</span></span> <span data-ttu-id="931b0-149">Hello 앱 서비스 계획의 크기를 조정 하 고 따라서 hello 내에서 모든 hello 앱의 크기 조정 응용 프로그램 크기를 조정할 때 동일한 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-149">When you scale an app, you scale hello App Service plan and thus scale all hello apps in hello same plan.</span></span>

<span data-ttu-id="931b0-150">ASEv2, 앱 서비스 계획의 크기를 조정 하는 경우 필요한 hello 인프라 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-150">In ASEv2, when you scale an App Service plan, hello needed infrastructure is automatically added.</span></span> <span data-ttu-id="931b0-151">동안에 시간 지연이 tooscale 작업 hello 인프라가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-151">There is a time delay tooscale operations while hello infrastructure is added.</span></span> <span data-ttu-id="931b0-152">ASEv1, hello 필요한 인프라를 만들거나 앱 서비스 계획을 확장할 수 먼저 추가 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-152">In ASEv1, hello needed infrastructure must be added before you can create or scale out your App Service plan.</span></span> 

<span data-ttu-id="931b0-153">Hello 다중 테 넌 트 응용 프로그램 서비스를 크기 조정는 일반적으로 즉시 리소스 풀에 원활 하 게 사용 toosupport 이므로 것입니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-153">In hello multitenant App Service, scaling is usually immediate because a pool of resources is readily available toosupport it.</span></span> <span data-ttu-id="931b0-154">ASE에는 이러한 버퍼가 없으며 리소스는 필요 시에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-154">In an ASE, there is no such buffer, and resources are allocated upon need.</span></span>

<span data-ttu-id="931b0-155">ASE too100 인스턴스를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-155">In an ASE, you can scale up too100 instances.</span></span> <span data-ttu-id="931b0-156">이러한 100개의 인스턴스는 모두 하나의 App Service 계획에 있거나 여러 App Service 계획에 분산될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-156">Those 100 instances can be all in one single App Service plan or distributed across multiple App Service plans.</span></span>

## <a name="ip-addresses"></a><span data-ttu-id="931b0-157">IP 주소</span><span class="sxs-lookup"><span data-stu-id="931b0-157">IP addresses</span></span> ##

<span data-ttu-id="931b0-158">응용 프로그램 서비스는 hello 기능 tooallocate 전용된 IP 주소 tooan 앱을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-158">App Service has hello ability tooallocate a dedicated IP address tooan app.</span></span> <span data-ttu-id="931b0-159">이 기능을 사용할 수 있는 IP 기반 SSL을 구성한 후에 설명 된 대로 [는 기존 사용자 지정 SSL 인증서 tooAzure 웹 앱을 바인딩할][ConfigureSSL]합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-159">This capability is available after you configure an IP-based SSL, as described in [Bind an existing custom SSL certificate tooAzure web apps][ConfigureSSL].</span></span> <span data-ttu-id="931b0-160">그러나 ASE에는 중요한 예외 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-160">However, in an ASE, there is a notable exception.</span></span> <span data-ttu-id="931b0-161">IP를 추가할 수 없습니다 toobe ILB ASE에는 IP 기반 SSL에 사용 되는 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-161">You can't add additional IP addresses toobe used for an IP-based SSL in an ILB ASE.</span></span>

<span data-ttu-id="931b0-162">ASEv1에 있어야만 tooallocate hello IP 주소 리소스 그룹으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-162">In ASEv1, you need tooallocate hello IP addresses as resources before you can use them.</span></span> <span data-ttu-id="931b0-163">ASEv2를 사용 하 여 해당 앱에서 hello 다중 테 넌 트 응용 프로그램 서비스와 마찬가지로.</span><span class="sxs-lookup"><span data-stu-id="931b0-163">In ASEv2, you use them from your app just as you do in hello multitenant App Service.</span></span> <span data-ttu-id="931b0-164">항상 하나의 예비에 주소가 ASEv2 too30 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-164">There is always one spare address in ASEv2 up too30 IP addresses.</span></span> <span data-ttu-id="931b0-165">IP 주소를 사용할 때마다 다른 주소가 추가되므로 주소 하나를 항상 즉시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-165">Each time you use one, another is added so that an address is always readily available for use.</span></span> <span data-ttu-id="931b0-166">지연 시간은 한 번 필요한 tooallocate IP 추가 수행할 수 없습니다. 다른 IP 주소를 연속으로 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-166">A time delay is required tooallocate another IP address, which prevents adding IP addresses in quick succession.</span></span>

## <a name="front-end-scaling"></a><span data-ttu-id="931b0-167">프런트 엔드 확장</span><span class="sxs-lookup"><span data-stu-id="931b0-167">Front-end scaling</span></span> ##

<span data-ttu-id="931b0-168">ASEv2, 앱 서비스 계획을 확장할 때 작업자는 자동으로 추가 toosupport 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-168">In ASEv2, when you scale out your App Service plans, workers are automatically added toosupport them.</span></span> <span data-ttu-id="931b0-169">모든 ASE는 프런트 엔드 2개를 포함하는 상태로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-169">Every ASE is created with two front ends.</span></span> <span data-ttu-id="931b0-170">또한 hello 프런트 엔드 자동으로 확장 15 모든 인스턴스에 대 한 프런트 엔드를 한 개, 앱 서비스 계획에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-170">In addition, hello front ends automatically scale out at a rate of one front end for every 15 instances in your App Service plans.</span></span> <span data-ttu-id="931b0-171">예를 들어 인스턴스가 15개이면 프런트 엔드는 세 개입니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-171">For example, if you have 15 instances, then you have three front ends.</span></span> <span data-ttu-id="931b0-172">Too30 인스턴스를 크기를 조정 하는 경우 이름을 제공 해야 끝 앞 / 등 4 개.</span><span class="sxs-lookup"><span data-stu-id="931b0-172">If you scale too30 instances, then you have four front ends, and so on.</span></span>

<span data-ttu-id="931b0-173">대부분의 시나리오에서는 이 정도의 프런트 엔드만으로도 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-173">This number of front ends should be more than enough for most scenarios.</span></span> <span data-ttu-id="931b0-174">그러나 더 빠른 속도로 규모를 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-174">However, you can scale out at a faster rate.</span></span> <span data-ttu-id="931b0-175">5 개의 모든 인스턴스에 대 한 하나의 프런트 엔드 tooas 낮은 hello 비율을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-175">You can change hello ratio tooas low as one front end for every five instances.</span></span> <span data-ttu-id="931b0-176">Hello 비율을 변경 하는 데 대 한 요금이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-176">There is a charge for changing hello ratio.</span></span> <span data-ttu-id="931b0-177">자세한 내용은 [Azure App Service 가격][Pricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="931b0-177">For more information, see [Azure App Service pricing][Pricing].</span></span>

<span data-ttu-id="931b0-178">프런트 엔드 리소스가 ASE hello에 대 한 hello HTTP/HTTPS 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-178">Front-end resources are hello HTTP/HTTPS endpoint for hello ASE.</span></span> <span data-ttu-id="931b0-179">Hello 기본 프런트 엔드 구성에서 프런트 엔드 별로 메모리 사용량은 지속적으로 약 60%입니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-179">With hello default front-end configuration, memory usage per front end is consistently around 60 percent.</span></span> <span data-ttu-id="931b0-180">고객 작업은 프런트 엔드에서 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-180">Customer workloads don't run on a front end.</span></span> <span data-ttu-id="931b0-181">hello 존중 tooscale와 프런트 엔드에 대 한 중요 한 요소는 HTTPS 트래픽에 따라 주로 진행 hello CPU, 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-181">hello key factor for a front end with respect tooscale is hello CPU, which is driven primarily by HTTPS traffic.</span></span>

## <a name="app-access"></a><span data-ttu-id="931b0-182">앱 액세스</span><span class="sxs-lookup"><span data-stu-id="931b0-182">App access</span></span> ##

<span data-ttu-id="931b0-183">외부 ASE에 앱을 만들 때 사용 되는 hello 도메인은 hello 다중 테 넌 트 응용 프로그램 서비스와에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-183">In an External ASE, hello domain that's used when you create apps is different from hello multitenant App Service.</span></span> <span data-ttu-id="931b0-184">Hello ASE의 hello 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-184">It includes hello name of hello ASE.</span></span> <span data-ttu-id="931b0-185">방법에 대 한 자세한 내용은 외부 ASE toocreate 참조 [앱 서비스 환경 만들기][MakeExternalASE]합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-185">For more information on how toocreate an External ASE, see [Create an App Service environment][MakeExternalASE].</span></span> <span data-ttu-id="931b0-186">외부 ASE에 hello 도메인 이름 처럼 보이는 *.&lt; asename&gt;. p.azurewebsites.net*합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-186">hello domain name in an External ASE looks like *.&lt;asename&gt;.p.azurewebsites.net*.</span></span> <span data-ttu-id="931b0-187">예를 들어 프로그램 ASE 라는 _외부 ase_ 호출 응용 프로그램에 호스트할 _contoso_ 해당 ASE 있습니다 도달 hello 다음 Url에서:</span><span class="sxs-lookup"><span data-stu-id="931b0-187">For example, if your ASE is named _external-ase_ and you host an app called _contoso_ in that ASE, you reach it at hello following URLs:</span></span>

- <span data-ttu-id="931b0-188">contoso.external-ase.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="931b0-188">contoso.external-ase.p.azurewebsites.net</span></span>
- <span data-ttu-id="931b0-189">contoso.scm.external-ase.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="931b0-189">contoso.scm.external-ase.p.azurewebsites.net</span></span>

<span data-ttu-id="931b0-190">hello URL contoso.scm.external ase.p.azurewebsites.net는 사용 되는 tooaccess hello Kudu 콘솔 또는 웹 사용 하 여 응용 프로그램 게시에 대 한 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-190">hello URL contoso.scm.external-ase.p.azurewebsites.net is used tooaccess hello Kudu console or for publishing your app by using web deploy.</span></span> <span data-ttu-id="931b0-191">Hello Kudu 콘솔에 대 한 자세한 내용은 참조 [Azure 앱 서비스에 대 한 Kudu 콘솔][Kudu]합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-191">For information on hello Kudu console, see [Kudu console for Azure App Service][Kudu].</span></span> <span data-ttu-id="931b0-192">hello Kudu 콘솔 디버깅, 파일 업로드, 파일 및 더 많은 편집에 대 한 웹 UI를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-192">hello Kudu console gives you a web UI for debugging, uploading files, editing files, and much more.</span></span>

<span data-ttu-id="931b0-193">ILB ASE 배포 시 hello 도메인을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-193">In an ILB ASE, you determine hello domain at deployment time.</span></span> <span data-ttu-id="931b0-194">Toocreate 받는 ILB ASE를 확인 하려면 어떻게 해야 대 한 자세한 내용은 [만들고 ILB ASE를 사용 하 여][MakeILBASE]합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-194">For more information on how toocreate an ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span> <span data-ttu-id="931b0-195">Hello 도메인 이름을 지정 하는 경우 _ilb ase.info_, ASE 응용 프로그램 생성 하는 동안 해당 도메인을 사용 한다는 점에서 앱 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-195">If you specify hello domain name _ilb-ase.info_, hello apps in that ASE use that domain during app creation.</span></span> <span data-ttu-id="931b0-196">명명 된 hello 앱에 대 한 _contoso_, hello Url은:</span><span class="sxs-lookup"><span data-stu-id="931b0-196">For hello app named _contoso_, hello URLs are:</span></span>

- <span data-ttu-id="931b0-197">contoso.ilb-ase.info</span><span class="sxs-lookup"><span data-stu-id="931b0-197">contoso.ilb-ase.info</span></span>
- <span data-ttu-id="931b0-198">contoso.scm.ilb-ase.info</span><span class="sxs-lookup"><span data-stu-id="931b0-198">contoso.scm.ilb-ase.info</span></span>

## <a name="publishing"></a><span data-ttu-id="931b0-199">게시</span><span class="sxs-lookup"><span data-stu-id="931b0-199">Publishing</span></span> ##

<span data-ttu-id="931b0-200">Hello 다중 테 넌 트 응용 프로그램 서비스와 마찬가지로 ASE에으로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-200">As with hello multitenant App Service, in an ASE you can publish with:</span></span>

- <span data-ttu-id="931b0-201">웹 배포</span><span class="sxs-lookup"><span data-stu-id="931b0-201">Web deployment.</span></span>
- <span data-ttu-id="931b0-202">FTP</span><span class="sxs-lookup"><span data-stu-id="931b0-202">FTP.</span></span>
- <span data-ttu-id="931b0-203">연속 통합</span><span class="sxs-lookup"><span data-stu-id="931b0-203">Continuous integration.</span></span>
- <span data-ttu-id="931b0-204">끌어 놓은 hello Kudu 콘솔.</span><span class="sxs-lookup"><span data-stu-id="931b0-204">Drag and drop in hello Kudu console.</span></span>
- <span data-ttu-id="931b0-205">IDE(예: Visual Studio, Eclipse 또는 IntelliJ IDEA)</span><span class="sxs-lookup"><span data-stu-id="931b0-205">An IDE, such as Visual Studio, Eclipse, or IntelliJ IDEA.</span></span>

<span data-ttu-id="931b0-206">외부 ASE와 작동 하는 이러한 게시 옵션을 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-206">With an External ASE, these publishing options all behave hello same.</span></span> <span data-ttu-id="931b0-207">자세한 내용은 [Azure App Service의 배포][AppDeploy]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="931b0-207">For more information, see [Deployment in Azure App Service][AppDeploy].</span></span> 

<span data-ttu-id="931b0-208">게시와 hello 주요 다른 존중 tooan ILB ASE와입니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-208">hello major difference with publishing is with respect tooan ILB ASE.</span></span> <span data-ttu-id="931b0-209">ILB ASE 끝점을 게시 하는 hello을 hello ILB 사용할 때만 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-209">With an ILB ASE, hello publishing endpoints are all available only through hello ILB.</span></span> <span data-ttu-id="931b0-210">ILB hello hello 가상 네트워크의 hello ASE 서브넷의 개인 IP 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-210">hello ILB is on a private IP in hello ASE subnet in hello virtual network.</span></span> <span data-ttu-id="931b0-211">네트워크 액세스 toohello ILB를 설정 하지 않은 경우 해당 ASE에 있는 앱을 게시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-211">If you don’t have network access toohello ILB, you can't publish any apps on that ASE.</span></span> <span data-ttu-id="931b0-212">설명한 것 처럼 [만들고 ILB ASE를 사용 하 여][MakeILBASE], hello 시스템에 DNS tooconfigure hello 앱에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-212">As noted in [Create and use an ILB ASE][MakeILBASE], you need tooconfigure DNS for hello apps in hello system.</span></span> <span data-ttu-id="931b0-213">Hello SCM 끝점을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-213">That includes hello SCM endpoint.</span></span> <span data-ttu-id="931b0-214">SCM 끝점이 올바르게 정의되어 있지 않으면 게시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-214">If they're not defined properly, you can't publish.</span></span> <span data-ttu-id="931b0-215">프로그램 Ide 해야 toohave 네트워크 액세스 toohello ILB 순서 toopublish에서 직접 tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-215">Your IDEs also need toohave network access toohello ILB in order toopublish directly tooit.</span></span>

<span data-ttu-id="931b0-216">인터넷 기반 CI 시스템, GitHub 및 Visual Studio Team Services와 같은 hello 게시 끝점 인터넷에 액세스할 수 없기 때문에 ILB ASE를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-216">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because hello publishing endpoint is not Internet accessible.</span></span> <span data-ttu-id="931b0-217">대신, Dropbox 등의 끌어오기 모델을 사용 하는 CI 시스템 toouse를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-217">Instead, you need toouse a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="931b0-218">ILB ASE에 앱에 대 한 끝점 게시 hello hello 도메인 ILB ASE를 사용 하 여 만든 해당 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-218">hello publishing endpoints for apps in an ILB ASE use hello domain that hello ILB ASE was created with.</span></span> <span data-ttu-id="931b0-219">Hello 응용 프로그램의 포털 블레이드 및 hello 응용 프로그램의 게시 프로필에서 확인할 수 있습니다 (에서 **개요** > **Essentials** 와 **속성**).</span><span class="sxs-lookup"><span data-stu-id="931b0-219">You can see it in hello app's publishing profile and in hello app's portal blade (in **Overview** > **Essentials** and also in **Properties**).</span></span> 

## <a name="pricing"></a><span data-ttu-id="931b0-220">가격</span><span class="sxs-lookup"><span data-stu-id="931b0-220">Pricing</span></span> ##

<span data-ttu-id="931b0-221">호출 SKU 가격 hello **격리 됨** ASEv2 에서만 사용 하기 위해 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-221">hello pricing SKU called **Isolated** was created for use only with ASEv2.</span></span> <span data-ttu-id="931b0-222">앱 서비스 계획을 ASEv2에서 호스트 되는 모든 안녕 SKU 가격 격리 됨.</span><span class="sxs-lookup"><span data-stu-id="931b0-222">All App Service plans that are hosted in ASEv2 are in hello Isolated pricing SKU.</span></span> <span data-ttu-id="931b0-223">격리된 App Service 계획 요금은 지역마다 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-223">Isolated App Service plan rates can vary per region.</span></span> 

<span data-ttu-id="931b0-224">또한 toohello 가격에 대 한 앱 서비스 계획, ASE 자체에 대 한 플랫 주기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-224">In addition toohello price for your App Service plans, there is a flat rate for ASE itself.</span></span> <span data-ttu-id="931b0-225">hello 고정 프로그램 ASE hello 크기가 변경 되지 않습니다 및 hello ASE 인프라는 기본 추가 1의 속도 비율에 맞게 대금을 지급 한다는 15 모든 앱 서비스 계획 인스턴스에서 대 한 프런트 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-225">hello flat rate doesn't change with hello size of your ASE and pays for hello ASE infrastructure at a default scaling rate of 1 additional front-end for every 15 App Service plan instances.</span></span>  

<span data-ttu-id="931b0-226">모든 15 앱 서비스 계획 인스턴스 1 프런트 엔드의 hello 기본 배율 속도 만큼 빠르지 없으면 hello 비율 프런트 엔드를 추가 하거나 hello hello 프런트엔드의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-226">If hello default scale rate of 1 front end for every 15 App Service plan instances is not fast enough, you can adjust hello ratio at which front-ends are added or hello size of hello front-ends.</span></span>  <span data-ttu-id="931b0-227">Hello 비율 또는 크기를 조정 하면 기본적으로 추가 되지 hello 프런트 엔드 코어에 대 한 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-227">When you adjust hello ratio or size, you pay for hello front-end cores that would not be added by default.</span></span>  

<span data-ttu-id="931b0-228">예를 들어 hello 눈금 비율 too10 조정 하는 경우 프런트 엔드 인스턴스 모든 10에 대 한 앱 서비스 계획에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-228">For example, if you adjust hello scale ratio too10, a front end is added for every 10 instances in your App Service plans.</span></span> <span data-ttu-id="931b0-229">hello 요금 15 모든 인스턴스에 대 한 하나의 프런트 엔드의 배율 속도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-229">hello flat fee covers a scale rate of one front end for every 15 instances.</span></span> <span data-ttu-id="931b0-230">10의 배율 비율로, hello 세 번째 프런트 엔드를 앱 서비스 계획 인스턴스 10 hello에 대 한 추가 대 한 요금을 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-230">With a scale ratio of 10, you pay a fee for hello third front end that's added for hello 10 App Service plan instances.</span></span> <span data-ttu-id="931b0-231">15 인스턴스가 자동으로 추가 되었기 때문에 도달 하면에 대 한 toopay를 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-231">You don't need toopay for it when you reach 15 instances because it was added automatically.</span></span>

<span data-ttu-id="931b0-232">Hello 프런트 엔드가 too2 코어 hello 크기를 조정 하지만 다음에 대 한 지불 hello 비율을 조정 하지 마십시오 하는 경우 추가 코어를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-232">If you adjusted hello size of hello front-ends too2 cores but do not adjust hello ratio then you pay for hello extra cores.</span></span>  <span data-ttu-id="931b0-233">ASE 2 프런트 엔드, hello 크기 too2 코어 프런트 엔드를 증가 시킨 경우 추가 코어 2 개에 대해 지불할 hello 자동 크기 조정 임계값 보다도 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-233">An ASE is created with 2 front-ends, so even below hello automatic scaling threshold you would pay for 2 extra cores if you increased hello size too2 core front-ends.</span></span>

<span data-ttu-id="931b0-234">자세한 내용은 [Azure App Service 가격][Pricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="931b0-234">For more information, see [Azure App Service pricing][Pricing].</span></span>

## <a name="delete-an-ase"></a><span data-ttu-id="931b0-235">ASE 삭제</span><span class="sxs-lookup"><span data-stu-id="931b0-235">Delete an ASE</span></span> ##

<span data-ttu-id="931b0-236">ASE toodelete:</span><span class="sxs-lookup"><span data-stu-id="931b0-236">toodelete an ASE:</span></span> 

1. <span data-ttu-id="931b0-237">사용 하 여 **삭제** hello의 hello 위쪽 **앱 서비스 환경** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-237">Use **Delete** at hello top of hello **App Service Environment** blade.</span></span> 

2. <span data-ttu-id="931b0-238">원하는 toodelete 프로그램 ASE tooconfirm의 hello 이름을 입력 하기.</span><span class="sxs-lookup"><span data-stu-id="931b0-238">Enter hello name of your ASE tooconfirm that you want toodelete it.</span></span> <span data-ttu-id="931b0-239">ASE를 삭제 하면 콘텐츠의 hello 그 안에 모두 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="931b0-239">When you delete an ASE, you delete all of hello content within it as well.</span></span> 

    ![ASE 삭제][3]

<!--Image references-->
[1]: ./media/using_an_app_service_environment/usingase-appcreate.png
[2]: ./media/using_an_app_service_environment/usingase-pricingtiers.png
[3]: ./media/using_an_app_service_environment/usingase-delete.png


<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
