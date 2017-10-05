---
title: "Azure App Service Environment 사용"
description: "Azure App Service Environment에서 앱을 작성, 게시 및 확장하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 279951d40b7780120d0b94e183f06e00ccece016
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-an-app-service-environment"></a><span data-ttu-id="feea2-103">App Service Environment 사용</span><span class="sxs-lookup"><span data-stu-id="feea2-103">Use an App Service environment</span></span> #

## <a name="overview"></a><span data-ttu-id="feea2-104">개요</span><span class="sxs-lookup"><span data-stu-id="feea2-104">Overview</span></span> ##

<span data-ttu-id="feea2-105">Azure App Service Environment는 Azure App Service를 고객의 Azure Virtual Network에 있는 서브넷에 배포한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-105">Azure App Service Environment is a deployment of Azure App Service into a subnet in a customer’s Azure virtual network.</span></span> <span data-ttu-id="feea2-106">ASE는 다음으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-106">It consists of:</span></span>

- <span data-ttu-id="feea2-107">**프런트 엔드**: 프런트 엔드는 ASE(App Service Environment)에서 HTTP/HTTPS가 종료되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-107">**Front ends**: The front ends are where HTTP/HTTPS terminates in an App Service environment (ASE).</span></span>
- <span data-ttu-id="feea2-108">**작업자**: 작업자는 앱을 호스트하는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-108">**Workers**: The workers are the resources that host your apps.</span></span>
- <span data-ttu-id="feea2-109">**데이터베이스**: 데이터베이스에는 환경을 정의하는 정보가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-109">**Database**: The database holds information that defines the environment.</span></span>
- <span data-ttu-id="feea2-110">**저장소**: 저장소는 고객이 게시한 앱을 호스트하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-110">**Storage**: The storage is used to host the customer-published apps.</span></span>

> [!NOTE]
> <span data-ttu-id="feea2-111">App Service Environment에는 두 가지 버전(ASEv1 및 ASEv2)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-111">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="feea2-112">ASEv1에서는 사용하려는 리소스를 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-112">In ASEv1, you must manage the resources before you can use them.</span></span> <span data-ttu-id="feea2-113">ASEv1을 구성하고 관리하는 방법을 알아보려면 [App Service Environment v1 구성][ConfigureASEv1]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="feea2-113">To learn how to configure and manage ASEv1, see [Configure an App Service environment v1][ConfigureASEv1].</span></span> <span data-ttu-id="feea2-114">이 문서의 나머지 부분에서는 ASEv2에 대해 중점적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-114">The rest of this article focuses on ASEv2.</span></span>
>
>

<span data-ttu-id="feea2-115">앱 액세스를 위한 외부 또는 내부 VIP로 ASE(ASEv1 및 ASEv2)를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-115">You can deploy an ASE (ASEv1 and ASEv2) with an external or internal VIP for app access.</span></span> <span data-ttu-id="feea2-116">외부 VIP를 사용하는 배포를 대개 외부 ASE라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-116">The deployment with an external VIP is commonly called an External ASE.</span></span> <span data-ttu-id="feea2-117">내부 버전은 내부 ILB(부하 분산 장치)를 사용하므로 ILB ASE라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-117">The internal version is called the ILB ASE because it uses an internal load balancer (ILB).</span></span> <span data-ttu-id="feea2-118">ILB ASE에 대해 자세히 알아보려면 [ILB ASE 만들기 및 사용][MakeILBASE]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="feea2-118">To learn more about the ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span>

## <a name="create-a-web-app-in-an-ase"></a><span data-ttu-id="feea2-119">ASE에서 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="feea2-119">Create a web app in an ASE</span></span> ##

<span data-ttu-id="feea2-120">ASE에서 웹앱을 만들려는 경우 일반적으로 웹앱을 만들 때 사용하는 것과 같은 프로세스를 사용합니다. 그러나 두 프로세스 간에는 몇 가지 세부적인 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-120">To create a web app in an ASE, you use the same process as when you create it normally, but with a few small differences.</span></span> <span data-ttu-id="feea2-121">새 App Service 계획을 만들 때는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-121">When you create a new App Service plan:</span></span>

- <span data-ttu-id="feea2-122">앱을 배포하기 위한 지리적 위치를 선택하는 대신 ASE를 위치로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-122">Instead of choosing a geographic location in which to deploy your app, you choose an ASE as your location.</span></span>
- <span data-ttu-id="feea2-123">ASE에서 만들어진 모든 App Service 계획은 격리 가격 책정 계층에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-123">All App Service plans created in an ASE must be in an Isolated pricing tier.</span></span>

<span data-ttu-id="feea2-124">ASE가 없는 경우 [App Service Environment 만들기][MakeExternalASE]의 지침에 따라 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-124">If you don't have an ASE, you can create one by following the instructions in [Create an App Service environment][MakeExternalASE].</span></span>

<span data-ttu-id="feea2-125">ASE에서 웹앱을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="feea2-125">To create a web app in an ASE:</span></span>

1. <span data-ttu-id="feea2-126">**새로 만들기**  > **웹 + 모바일** > **웹앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-126">Select **New** > **Web + Mobile** > **Web App**.</span></span>

2. <span data-ttu-id="feea2-127">웹앱의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-127">Enter a name for the web app.</span></span> <span data-ttu-id="feea2-128">ASE에서 이미 App Service 계획을 선택한 경우 앱의 도메인 이름에 ASE의 도메인 이름이 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-128">If you already selected an App Service plan in an ASE, the domain name for the app reflects the domain name of the ASE.</span></span>

    ![웹앱 이름 선택][1]

3. <span data-ttu-id="feea2-130">구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-130">Select a subscription.</span></span>

4. <span data-ttu-id="feea2-131">새 리소스 그룹의 이름을 입력하거나 **기존 항목 사용**을 선택하고 드롭다운 목록에서 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-131">Enter a name for a new resource group, or select **Use existing** and select one from the drop-down list.</span></span>

5. <span data-ttu-id="feea2-132">ASE에서 기존 App Service 계획을 선택하거나 다음 단계를 통해 새 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-132">Select an existing App Service plan in your ASE, or create a new one by following these steps:</span></span>

    <span data-ttu-id="feea2-133">a.</span><span class="sxs-lookup"><span data-stu-id="feea2-133">a.</span></span> <span data-ttu-id="feea2-134">**새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-134">Select **Create New**.</span></span>

    <span data-ttu-id="feea2-135">b.</span><span class="sxs-lookup"><span data-stu-id="feea2-135">b.</span></span> <span data-ttu-id="feea2-136">App Service 계획의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-136">Enter the name for your App Service plan.</span></span>

    <span data-ttu-id="feea2-137">c.</span><span class="sxs-lookup"><span data-stu-id="feea2-137">c.</span></span> <span data-ttu-id="feea2-138">**위치** 드롭다운 목록에서 해당 ASE를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-138">Select your ASE in the **Location** drop-down list.</span></span>

    <span data-ttu-id="feea2-139">d.</span><span class="sxs-lookup"><span data-stu-id="feea2-139">d.</span></span> <span data-ttu-id="feea2-140">**격리** 가격 책정 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-140">Select an **Isolated** pricing tier.</span></span> <span data-ttu-id="feea2-141">**선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-141">Select **Select**.</span></span>

    <span data-ttu-id="feea2-142">e.</span><span class="sxs-lookup"><span data-stu-id="feea2-142">e.</span></span> <span data-ttu-id="feea2-143">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-143">Select **OK**.</span></span>
    
    ![격리 가격 책정 계층][2]

6. <span data-ttu-id="feea2-145">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-145">Select **Create**.</span></span>

## <a name="how-scale-works"></a><span data-ttu-id="feea2-146">확장이 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="feea2-146">How scale works</span></span> ##

<span data-ttu-id="feea2-147">모든 App Service 앱은 App Service 계획에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-147">Every App Service app runs in an App Service plan.</span></span> <span data-ttu-id="feea2-148">컨테이너 모델 환경은 App Service 계획을 포함하고 App Service 계획은 앱을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-148">The container model is environments hold App Service plans, and App Service plans hold apps.</span></span> <span data-ttu-id="feea2-149">앱을 확장하면 App Service 계획이 확장되므로 같은 계획 내에 있는 모든 앱이 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-149">When you scale an app, you scale the App Service plan and thus scale all the apps in the same plan.</span></span>

<span data-ttu-id="feea2-150">ASEv2에서는 App Service 계획을 확장하면 필요한 인프라가 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-150">In ASEv2, when you scale an App Service plan, the needed infrastructure is automatically added.</span></span> <span data-ttu-id="feea2-151">인프라가 추가되는 동안 확장 작업의 시간이 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-151">There is a time delay to scale operations while the infrastructure is added.</span></span> <span data-ttu-id="feea2-152">반면 ASEv1에서는 App Service 계획을 만들거나 규모 확장하려면 필요한 인프라를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-152">In ASEv1, the needed infrastructure must be added before you can create or scale out your App Service plan.</span></span> 

<span data-ttu-id="feea2-153">다중 테넌트 App Service에서는 대개 확장이 즉시 수행됩니다. 확장을 지원하는 리소스 풀을 즉시 사용할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-153">In the multitenant App Service, scaling is usually immediate because a pool of resources is readily available to support it.</span></span> <span data-ttu-id="feea2-154">ASE에는 이러한 버퍼가 없으며 리소스는 필요 시에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-154">In an ASE, there is no such buffer, and resources are allocated upon need.</span></span>

<span data-ttu-id="feea2-155">ASE는 최대 100개의 인스턴스를 포함하도록 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-155">In an ASE, you can scale up to 100 instances.</span></span> <span data-ttu-id="feea2-156">이러한 100개의 인스턴스는 모두 하나의 App Service 계획에 있거나 여러 App Service 계획에 분산될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-156">Those 100 instances can be all in one single App Service plan or distributed across multiple App Service plans.</span></span>

## <a name="ip-addresses"></a><span data-ttu-id="feea2-157">IP 주소</span><span class="sxs-lookup"><span data-stu-id="feea2-157">IP addresses</span></span> ##

<span data-ttu-id="feea2-158">App Service에는 앱에 전용 IP 주소를 할당하는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-158">App Service has the ability to allocate a dedicated IP address to an app.</span></span> <span data-ttu-id="feea2-159">[Azure Web Apps에 기존 사용자 지정 SSL 인증서 바인딩][ConfigureSSL]에 설명된 대로 IP 기반 SSL을 구성하고 나면 이 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-159">This capability is available after you configure an IP-based SSL, as described in [Bind an existing custom SSL certificate to Azure web apps][ConfigureSSL].</span></span> <span data-ttu-id="feea2-160">그러나 ASE에는 중요한 예외 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-160">However, in an ASE, there is a notable exception.</span></span> <span data-ttu-id="feea2-161">즉, ILB ASE에서 IP 기반 SSL용으로 사용할 IP 주소를 더 추가할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-161">You can't add additional IP addresses to be used for an IP-based SSL in an ILB ASE.</span></span>

<span data-ttu-id="feea2-162">ASEv1에서는 IP 주소를 사용하기 전에 IP 주소를 리소스로 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-162">In ASEv1, you need to allocate the IP addresses as resources before you can use them.</span></span> <span data-ttu-id="feea2-163">ASEv2에서는 다중 테넌트 App Service에서와 마찬가지로 앱에서 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-163">In ASEv2, you use them from your app just as you do in the multitenant App Service.</span></span> <span data-ttu-id="feea2-164">ASEv2에는 항상 여분의 주소가 하나 있습니다(최대 IP 주소 30개).</span><span class="sxs-lookup"><span data-stu-id="feea2-164">There is always one spare address in ASEv2 up to 30 IP addresses.</span></span> <span data-ttu-id="feea2-165">IP 주소를 사용할 때마다 다른 주소가 추가되므로 주소 하나를 항상 즉시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-165">Each time you use one, another is added so that an address is always readily available for use.</span></span> <span data-ttu-id="feea2-166">다른 IP 주소를 할당할 때는 시간이 지연되므로, IP 주소를 연속해서 빠르게 추가할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-166">A time delay is required to allocate another IP address, which prevents adding IP addresses in quick succession.</span></span>

## <a name="front-end-scaling"></a><span data-ttu-id="feea2-167">프런트 엔드 확장</span><span class="sxs-lookup"><span data-stu-id="feea2-167">Front-end scaling</span></span> ##

<span data-ttu-id="feea2-168">ASEv2에서 App Service 계획을 규모 확장할 때는 이러한 계획을 지원하도록 작업자가 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-168">In ASEv2, when you scale out your App Service plans, workers are automatically added to support them.</span></span> <span data-ttu-id="feea2-169">모든 ASE는 프런트 엔드 2개를 포함하는 상태로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-169">Every ASE is created with two front ends.</span></span> <span data-ttu-id="feea2-170">또한 App Service 계획의 15개 인스턴스마다 프런트 엔드가 하나씩 생성되는 속도로 프런트 엔드가 자동으로 규모 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-170">In addition, the front ends automatically scale out at a rate of one front end for every 15 instances in your App Service plans.</span></span> <span data-ttu-id="feea2-171">예를 들어 인스턴스가 15개이면 프런트 엔드는 세 개입니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-171">For example, if you have 15 instances, then you have three front ends.</span></span> <span data-ttu-id="feea2-172">인스턴스 30개로 확장하면 프런트 엔드가 네 개 있는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-172">If you scale to 30 instances, then you have four front ends, and so on.</span></span>

<span data-ttu-id="feea2-173">대부분의 시나리오에서는 이 정도의 프런트 엔드만으로도 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-173">This number of front ends should be more than enough for most scenarios.</span></span> <span data-ttu-id="feea2-174">그러나 더 빠른 속도로 규모를 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-174">However, you can scale out at a faster rate.</span></span> <span data-ttu-id="feea2-175">인스턴스 5개마다 프런트 엔드가 하나씩 생성되도록 비율을 더 낮게 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-175">You can change the ratio to as low as one front end for every five instances.</span></span> <span data-ttu-id="feea2-176">비율 변경 시에는 요금이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-176">There is a charge for changing the ratio.</span></span> <span data-ttu-id="feea2-177">자세한 내용은 [Azure App Service 가격][Pricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="feea2-177">For more information, see [Azure App Service pricing][Pricing].</span></span>

<span data-ttu-id="feea2-178">프런트 엔드 리소스는 ASE의 HTTP/HTTPS 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-178">Front-end resources are the HTTP/HTTPS endpoint for the ASE.</span></span> <span data-ttu-id="feea2-179">기본 프런트 엔드 구성에서는 프런트 엔드당 메모리 사용량이 일관되게 약 60%입니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-179">With the default front-end configuration, memory usage per front end is consistently around 60 percent.</span></span> <span data-ttu-id="feea2-180">고객 작업은 프런트 엔드에서 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-180">Customer workloads don't run on a front end.</span></span> <span data-ttu-id="feea2-181">확장과 관련한 프런트 엔드의 주요 요인은 CPU입니다. CPU는 주로 HTTPS 트래픽에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-181">The key factor for a front end with respect to scale is the CPU, which is driven primarily by HTTPS traffic.</span></span>

## <a name="app-access"></a><span data-ttu-id="feea2-182">앱 액세스</span><span class="sxs-lookup"><span data-stu-id="feea2-182">App access</span></span> ##

<span data-ttu-id="feea2-183">외부 ASE에서는 앱을 만들 때 사용되는 도메인이 다중 테넌트 App Service와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-183">In an External ASE, the domain that's used when you create apps is different from the multitenant App Service.</span></span> <span data-ttu-id="feea2-184">이 도메인에는 ASE의 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-184">It includes the name of the ASE.</span></span> <span data-ttu-id="feea2-185">외부 ASE를 만드는 방법에 대한 자세한 내용은 [App Service Environment 만들기][MakeExternalASE]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="feea2-185">For more information on how to create an External ASE, see [Create an App Service environment][MakeExternalASE].</span></span> <span data-ttu-id="feea2-186">외부 ASE의 도메인 이름은 *.&lt;asename&gt;.p.azurewebsites.net*과 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-186">The domain name in an External ASE looks like *.&lt;asename&gt;.p.azurewebsites.net*.</span></span> <span data-ttu-id="feea2-187">예를 들어 ASE 이름이 _external-ase_이고 해당 ASE에서 _contoso_라는 앱을 호스트하는 경우 다음과 같은 URL에서 앱에 액세스하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-187">For example, if your ASE is named _external-ase_ and you host an app called _contoso_ in that ASE, you reach it at the following URLs:</span></span>

- <span data-ttu-id="feea2-188">contoso.external-ase.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="feea2-188">contoso.external-ase.p.azurewebsites.net</span></span>
- <span data-ttu-id="feea2-189">contoso.scm.external-ase.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="feea2-189">contoso.scm.external-ase.p.azurewebsites.net</span></span>

<span data-ttu-id="feea2-190">URL contoso.scm.external-ase.p.azurewebsites.net은 Kudu 콘솔에 액세스하거나 웹 배포를 사용하여 앱을 게시하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-190">The URL contoso.scm.external-ase.p.azurewebsites.net is used to access the Kudu console or for publishing your app by using web deploy.</span></span> <span data-ttu-id="feea2-191">Kudu 콘솔에 대한 자세한 내용은 [Azure App Service용 Kudu 콘솔][Kudu]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="feea2-191">For information on the Kudu console, see [Kudu console for Azure App Service][Kudu].</span></span> <span data-ttu-id="feea2-192">Kudu 콘솔은 디버깅, 파일 업로드, 파일 편집 등을 위한 웹 UI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-192">The Kudu console gives you a web UI for debugging, uploading files, editing files, and much more.</span></span>

<span data-ttu-id="feea2-193">ILB ASE에서는 배포 시간에 도메인을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-193">In an ILB ASE, you determine the domain at deployment time.</span></span> <span data-ttu-id="feea2-194">ILB ASE를 만드는 방법에 대한 자세한 내용은 [ILB ASE 만들기 및 사용][MakeILBASE]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="feea2-194">For more information on how to create an ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span> <span data-ttu-id="feea2-195">도메인 이름 _ilb-ase.info_를 지정하면 해당 ASE의 앱은 앱을 만드는 동안 해당 도메인을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-195">If you specify the domain name _ilb-ase.info_, the apps in that ASE use that domain during app creation.</span></span> <span data-ttu-id="feea2-196">이름이 _contoso_인 앱의 경우 URL은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-196">For the app named _contoso_, the URLs are:</span></span>

- <span data-ttu-id="feea2-197">contoso.ilb-ase.info</span><span class="sxs-lookup"><span data-stu-id="feea2-197">contoso.ilb-ase.info</span></span>
- <span data-ttu-id="feea2-198">contoso.scm.ilb-ase.info</span><span class="sxs-lookup"><span data-stu-id="feea2-198">contoso.scm.ilb-ase.info</span></span>

## <a name="publishing"></a><span data-ttu-id="feea2-199">게시</span><span class="sxs-lookup"><span data-stu-id="feea2-199">Publishing</span></span> ##

<span data-ttu-id="feea2-200">다중 테넌트 App Service와 마찬가지로 ASE에서는 다음을 사용하여 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-200">As with the multitenant App Service, in an ASE you can publish with:</span></span>

- <span data-ttu-id="feea2-201">웹 배포</span><span class="sxs-lookup"><span data-stu-id="feea2-201">Web deployment.</span></span>
- <span data-ttu-id="feea2-202">FTP</span><span class="sxs-lookup"><span data-stu-id="feea2-202">FTP.</span></span>
- <span data-ttu-id="feea2-203">연속 통합</span><span class="sxs-lookup"><span data-stu-id="feea2-203">Continuous integration.</span></span>
- <span data-ttu-id="feea2-204">Kudu 콘솔에서 끌어서 놓기</span><span class="sxs-lookup"><span data-stu-id="feea2-204">Drag and drop in the Kudu console.</span></span>
- <span data-ttu-id="feea2-205">IDE(예: Visual Studio, Eclipse 또는 IntelliJ IDEA)</span><span class="sxs-lookup"><span data-stu-id="feea2-205">An IDE, such as Visual Studio, Eclipse, or IntelliJ IDEA.</span></span>

<span data-ttu-id="feea2-206">외부 ASE에서는 이러한 게시 옵션이 모두 동일하게 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-206">With an External ASE, these publishing options all behave the same.</span></span> <span data-ttu-id="feea2-207">자세한 내용은 [Azure App Service의 배포][AppDeploy]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="feea2-207">For more information, see [Deployment in Azure App Service][AppDeploy].</span></span> 

<span data-ttu-id="feea2-208">게시에서 중요한 차이점은 ILB ASE와 관련된 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-208">The major difference with publishing is with respect to an ILB ASE.</span></span> <span data-ttu-id="feea2-209">ILB ASE에서 게시 끝점은 모두 ILB를 통해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-209">With an ILB ASE, the publishing endpoints are all available only through the ILB.</span></span> <span data-ttu-id="feea2-210">ILB는 Virtual Network의 ASE 서브넷에 있는 개인 IP에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-210">The ILB is on a private IP in the ASE subnet in the virtual network.</span></span> <span data-ttu-id="feea2-211">ILB에 대한 네트워크 액세스 권한이 없는 경우 해당 ASE에 앱을 게시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-211">If you don’t have network access to the ILB, you can't publish any apps on that ASE.</span></span> <span data-ttu-id="feea2-212">[ILB ASE 만들기 및 사용][MakeILBASE]에 설명된 것처럼 시스템에서 앱에 대한 DNS를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-212">As noted in [Create and use an ILB ASE][MakeILBASE], you need to configure DNS for the apps in the system.</span></span> <span data-ttu-id="feea2-213">여기에 SCM 끝점이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-213">That includes the SCM endpoint.</span></span> <span data-ttu-id="feea2-214">SCM 끝점이 올바르게 정의되어 있지 않으면 게시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-214">If they're not defined properly, you can't publish.</span></span> <span data-ttu-id="feea2-215">또한 직접 ILB에 게시하려면 IDE에 ILB에 대한 네트워크 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-215">Your IDEs also need to have network access to the ILB in order to publish directly to it.</span></span>

<span data-ttu-id="feea2-216">ILB ASE에서는 GitHub, Visual Studio Team Services 등의 인터넷 기반 CI 시스템이 작동하지 않습니다. 게시 끝점이 인터넷에 액세스할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-216">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because the publishing endpoint is not Internet accessible.</span></span> <span data-ttu-id="feea2-217">대신 끌어오기 모델을 사용하는 CI 시스템(예: Dropbox)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-217">Instead, you need to use a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="feea2-218">ILB ASE의 앱에 대한 게시 끝점에서는 ILB ASE가 만들어진 도메인을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-218">The publishing endpoints for apps in an ILB ASE use the domain that the ILB ASE was created with.</span></span> <span data-ttu-id="feea2-219">해당 도메인은 앱의 게시 프로필과 앱의 포털 블레이드(**개요** > **필수** 및 **속성**)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-219">You can see it in the app's publishing profile and in the app's portal blade (in **Overview** > **Essentials** and also in **Properties**).</span></span> 

## <a name="pricing"></a><span data-ttu-id="feea2-220">가격</span><span class="sxs-lookup"><span data-stu-id="feea2-220">Pricing</span></span> ##

<span data-ttu-id="feea2-221">가격 책정 SKU **격리**는 ASEv2에서만 사용하기 위해 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-221">The pricing SKU called **Isolated** was created for use only with ASEv2.</span></span> <span data-ttu-id="feea2-222">ASEv2에서 호스트되는 모든 App Service 계획에는 격리 가격 책정 SKU가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-222">All App Service plans that are hosted in ASEv2 are in the Isolated pricing SKU.</span></span> <span data-ttu-id="feea2-223">격리된 App Service 계획 요금은 지역마다 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-223">Isolated App Service plan rates can vary per region.</span></span> 

<span data-ttu-id="feea2-224">App Service 계획에 대한 가격 외에 ASE 자체에 대한 고정 요금이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-224">In addition to the price for your App Service plans, there is a flat rate for ASE itself.</span></span> <span data-ttu-id="feea2-225">고정 요금은 ASE 크기에 따라 변경되지 않으며, 15개의 모든 App Service 계획 인스턴스에 대해 1개의 추가 프런트 엔드에 대한 기본 크기 조정 요금으로 ASE 인프라 요금을 지불하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-225">The flat rate doesn't change with the size of your ASE and pays for the ASE infrastructure at a default scaling rate of 1 additional front-end for every 15 App Service plan instances.</span></span>  

<span data-ttu-id="feea2-226">15개의 모든 App Service 계획 인스턴스에 대해 프런트 엔드 1개의 기본 확장 비율이 충분히 빠르지 않을 경우 프런트 엔드가 추가되는 속도 또는 프런트 엔드의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-226">If the default scale rate of 1 front end for every 15 App Service plan instances is not fast enough, you can adjust the ratio at which front-ends are added or the size of the front-ends.</span></span>  <span data-ttu-id="feea2-227">이 비율 또는 크기를 조정할 경우 기본적으로 추가되지 않는 프런트 엔드 코어에 대해 비용을 지불하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-227">When you adjust the ratio or size, you pay for the front-end cores that would not be added by default.</span></span>  

<span data-ttu-id="feea2-228">예를 들어 확장 비율을 10으로 조정하면 App Service 계획에서 인스턴스 10개마다 프런트 엔드 하나가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-228">For example, if you adjust the scale ratio to 10, a front end is added for every 10 instances in your App Service plans.</span></span> <span data-ttu-id="feea2-229">고정 비용을 지불하는 경우에는 인스턴스 15개마다 프런트 엔드 하나가 추가되는 확장 비율이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-229">The flat fee covers a scale rate of one front end for every 15 instances.</span></span> <span data-ttu-id="feea2-230">확장 비율이 10인 경우에는 App Service 계획 인스턴스 10개에 대해 추가되는 세 번째 프런트 엔드의 요금을 지불하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-230">With a scale ratio of 10, you pay a fee for the third front end that's added for the 10 App Service plan instances.</span></span> <span data-ttu-id="feea2-231">인스턴스 수가 15개가 될 때는 요금을 지불하지 않아도 됩니다. 이 경우에는 프런트 엔드가 자동으로 추가되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-231">You don't need to pay for it when you reach 15 instances because it was added automatically.</span></span>

<span data-ttu-id="feea2-232">프런트 엔드의 크기를 2개 코어로 조절했으나 해당 비율을 조절하지 않은 경우 추가 코어에 대한 요금을 지불하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-232">If you adjusted the size of the front-ends to 2 cores but do not adjust the ratio then you pay for the extra cores.</span></span>  <span data-ttu-id="feea2-233">프런트 엔드 2개를 사용하여 ASE가 생성됩니다. 따라서 자동 크기 조정 임계값보다 낮더라도 해당 크기를 2 코어 프런트 엔드로 늘리면 2개의 추가 코어에 대해 요금을 지불하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-233">An ASE is created with 2 front-ends, so even below the automatic scaling threshold you would pay for 2 extra cores if you increased the size to 2 core front-ends.</span></span>

<span data-ttu-id="feea2-234">자세한 내용은 [Azure App Service 가격][Pricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="feea2-234">For more information, see [Azure App Service pricing][Pricing].</span></span>

## <a name="delete-an-ase"></a><span data-ttu-id="feea2-235">ASE 삭제</span><span class="sxs-lookup"><span data-stu-id="feea2-235">Delete an ASE</span></span> ##

<span data-ttu-id="feea2-236">ASE를 삭제하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-236">To delete an ASE:</span></span> 

1. <span data-ttu-id="feea2-237">**App Service Environment** 블레이드 위쪽의 **삭제**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-237">Use **Delete** at the top of the **App Service Environment** blade.</span></span> 

2. <span data-ttu-id="feea2-238">ASE의 이름을 입력하여 ASE 삭제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-238">Enter the name of your ASE to confirm that you want to delete it.</span></span> <span data-ttu-id="feea2-239">ASE를 삭제하면 해당 ASE 내의 콘텐츠도 모두 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="feea2-239">When you delete an ASE, you delete all of the content within it as well.</span></span> 

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
