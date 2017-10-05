---
title: "Azure App Service Environment에서 내부 부하 분산 장치 만들기 및 사용"
description: "인터넷에 연결되지 않은 Azure App Service Environment를 만들고 사용하는 방법에 대한 세부 정보"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: e7f85aaf2d940f114248d5925a1e97fe0f6bda6c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="0208c-103">App Service Environment에서 내부 부하 분산 장치 만들기 및 사용</span><span class="sxs-lookup"><span data-stu-id="0208c-103">Create and use an internal load balancer with an App Service environment</span></span> #

 <span data-ttu-id="0208c-104">Azure App Service Environment는 Azure App Service를 Azure VNet(Virtual Network)의 서브넷에 배포한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="0208c-105">ASE(App Service Environment)에는 두 가지 배포 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-105">There are two ways to deploy an App Service environment (ASE):</span></span> 

- <span data-ttu-id="0208c-106">외부 ASE라고도 하는 외부 IP 주소의 VIP 사용</span><span class="sxs-lookup"><span data-stu-id="0208c-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="0208c-107">내부 끝점이 ILB(내부 부하 분산 장치)이기 때문에 ILB ASE라고도 하는 내부 IP 주소의 VIP 사용</span><span class="sxs-lookup"><span data-stu-id="0208c-107">With a VIP on an internal IP address, often called an ILB ASE because the internal endpoint is an internal load balancer (ILB).</span></span> 

<span data-ttu-id="0208c-108">이 문서에서는 ILB ASE를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-108">This article shows you how to create an ILB ASE.</span></span> <span data-ttu-id="0208c-109">ASE의 개요는 [App Service Environment에 대한 소개][Intro]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0208c-109">For an overview on the ASE, see [Introduction to App Service environments][Intro].</span></span> <span data-ttu-id="0208c-110">외부 ASE를 만드는 방법을 알아보려면 [외부 ASE 만들기][MakeExternalASE]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0208c-110">To learn how to create an External ASE, see [Create an External ASE][MakeExternalASE].</span></span>

## <a name="overview"></a><span data-ttu-id="0208c-111">개요</span><span class="sxs-lookup"><span data-stu-id="0208c-111">Overview</span></span> ##

<span data-ttu-id="0208c-112">VNet의 인터넷 액세스 가능 끝점 또는 IP 주소를 사용하여 ASE를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-112">You can deploy an ASE with an internet-accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="0208c-113">IP 주소를 VNet 주소로 설정하려면 ASE는 ILB를 사용하여 배포되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-113">To set the IP address to a VNet address, the ASE must be deployed with an ILB.</span></span> <span data-ttu-id="0208c-114">ILB를 사용하여 ASE를 배포하는 경우 다음과 같은 항목을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-114">When you deploy your ASE with an ILB, you must provide:</span></span>

-   <span data-ttu-id="0208c-115">앱을 만들 때 사용하는 고유한 도메인</span><span class="sxs-lookup"><span data-stu-id="0208c-115">Your own domain that you use when you create your apps.</span></span>
-   <span data-ttu-id="0208c-116">HTTPS에 사용되는 인증서</span><span class="sxs-lookup"><span data-stu-id="0208c-116">The certificate used for HTTPS.</span></span>
-   <span data-ttu-id="0208c-117">도메인에 대한 DNS 관리</span><span class="sxs-lookup"><span data-stu-id="0208c-117">DNS management for your domain.</span></span>

<span data-ttu-id="0208c-118">결과적으로 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-118">In return, you can do things such as:</span></span>

-   <span data-ttu-id="0208c-119">사이트 간 또는 Azure ExpressRoute VPN을 통해 액세스하는 클라우드에서 인트라넷 응용 프로그램을 안전하게 호스트</span><span class="sxs-lookup"><span data-stu-id="0208c-119">Host intranet applications securely in the cloud, which you access through a site-to-site or Azure ExpressRoute VPN.</span></span>
-   <span data-ttu-id="0208c-120">공용 DNS 서버에 나열되지 않은 클라우드에 앱 호스트</span><span class="sxs-lookup"><span data-stu-id="0208c-120">Host apps in the cloud that aren't listed in public DNS servers.</span></span>
-   <span data-ttu-id="0208c-121">프런트 엔드 앱이 안전하게 통합될 수 있는 인터넷 격리 백 엔드 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="0208c-121">Create internet-isolated back-end apps, which your front-end apps can securely integrate with.</span></span>

### <a name="disabled-functionality"></a><span data-ttu-id="0208c-122">사용되지 않도록 설정된 기능</span><span class="sxs-lookup"><span data-stu-id="0208c-122">Disabled functionality</span></span> ###

<span data-ttu-id="0208c-123">ILB ASE를 사용하는 경우 수행할 수 없는 작업도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-123">There are some things that you can't do when you use an ILB ASE:</span></span>

-   <span data-ttu-id="0208c-124">IP 기반 SSL 사용</span><span class="sxs-lookup"><span data-stu-id="0208c-124">Use IP-based SSL.</span></span>
-   <span data-ttu-id="0208c-125">특정 앱에 IP 주소 할당</span><span class="sxs-lookup"><span data-stu-id="0208c-125">Assign IP addresses to specific apps.</span></span>
-   <span data-ttu-id="0208c-126">Azure Portal을 통해 앱에서 인증서 구매 및 사용</span><span class="sxs-lookup"><span data-stu-id="0208c-126">Buy and use a certificate with an app through the Azure portal.</span></span> <span data-ttu-id="0208c-127">직접 인증 기관에서 직접 인증서를 가져와서 앱에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-127">You can obtain certificates directly from a certificate authority and use them with your apps.</span></span> <span data-ttu-id="0208c-128">Azure Portal을 통해 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-128">You can't obtain them through the Azure portal.</span></span>

## <a name="create-an-ilb-ase"></a><span data-ttu-id="0208c-129">ILB ASE 만들기</span><span class="sxs-lookup"><span data-stu-id="0208c-129">Create an ILB ASE</span></span> ##

<span data-ttu-id="0208c-130">ILB ASE를 만들려면</span><span class="sxs-lookup"><span data-stu-id="0208c-130">To create an ILB ASE:</span></span>

1. <span data-ttu-id="0208c-131">Azure Portal에서 **새로 만들기** > **웹 + 모바일** > **App Service Environment**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-131">In the Azure portal, select **New** > **Web + Mobile** > **App Service Environment**.</span></span>

2. <span data-ttu-id="0208c-132">사용 중인 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-132">Select your subscription.</span></span>

3. <span data-ttu-id="0208c-133">리소스 그룹을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-133">Select or create a resource group.</span></span>

4. <span data-ttu-id="0208c-134">VNet을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-134">Select or create a VNet.</span></span>

5. <span data-ttu-id="0208c-135">기존 VNet을 선택한 경우 ASE를 보유하는 서브넷을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-135">If you select an existing VNet, you need to create a subnet to hold the ASE.</span></span> <span data-ttu-id="0208c-136">ASE의 향후 증가에 맞게 충분히 큰 서브넷 크기를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-136">Make sure to set a subnet size large enough to accommodate any future growth of your ASE.</span></span> <span data-ttu-id="0208c-137">`/25` 크기를 사용하는 것이 좋습니다. 그러면 128개의 주소가 있고 최대 크기의 ASE를 다룰 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-137">We recommend a size of `/25`, which has 128 addresses and can handle a maximum-sized ASE.</span></span> <span data-ttu-id="0208c-138">선택할 수 있는 최소 크기는 `/28`입니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-138">The minimum size you can select is a `/28`.</span></span> <span data-ttu-id="0208c-139">인프라에서 요구하면 이 크기는 최대 11개의 인스턴스로 확장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-139">After infrastructure needs, this size can be scaled to a maximum of 11 instances.</span></span>

    * <span data-ttu-id="0208c-140">App Service 계획에서 기본 최대 100개를 초과합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-140">Go beyond the default maximum of 100 instances in your App Service plans.</span></span>

    * <span data-ttu-id="0208c-141">더 신속한 프런트 엔드 확장으로 100개 가까이 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-141">Scale near 100 but with more rapid front-end scaling.</span></span>

6. <span data-ttu-id="0208c-142">**Virtual Network/위치** > **Virtual Network 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-142">Select **Virtual Network/Location** > **Virtual Network Configuration**.</span></span> <span data-ttu-id="0208c-143">**VIP 형식**을 **내부**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-143">Set the **VIP Type** to **Internal**.</span></span>

7. <span data-ttu-id="0208c-144">도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-144">Enter a domain name.</span></span> <span data-ttu-id="0208c-145">이 도메인은 이 ASE에서 만든 앱에 사용되는 하위 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-145">This domain is the one used for apps created in this ASE.</span></span> <span data-ttu-id="0208c-146">몇 가지 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-146">There are some restrictions.</span></span> <span data-ttu-id="0208c-147">다음 항목을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-147">It can't be:</span></span>

    * <span data-ttu-id="0208c-148">net</span><span class="sxs-lookup"><span data-stu-id="0208c-148">net</span></span>   

    * <span data-ttu-id="0208c-149">azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="0208c-149">azurewebsites.net</span></span>

    * <span data-ttu-id="0208c-150">p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="0208c-150">p.azurewebsites.net</span></span>

    * <span data-ttu-id="0208c-151">&lt;asename&gt;.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="0208c-151">&lt;asename&gt;.p.azurewebsites.net</span></span>

   <span data-ttu-id="0208c-152">앱의 사용자 지정 도메인 이름 및 ASE에서 사용하는 도메인 이름은 겹칠 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-152">The custom domain name used for apps and the domain name used by your ASE can't overlap.</span></span> <span data-ttu-id="0208c-153">_contoso.com_이라는 도메인 이름의 ILB ASE의 경우 앱에 다음과 비슷한 사용자 지정 도메인 이름을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-153">For an ILB ASE with the domain name _contoso.com_, you can't use custom domain names for your apps like:</span></span>

    * <span data-ttu-id="0208c-154">www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="0208c-154">www.contoso.com</span></span>

    * <span data-ttu-id="0208c-155">abcd.def.contoso.com</span><span class="sxs-lookup"><span data-stu-id="0208c-155">abcd.def.contoso.com</span></span>

    * <span data-ttu-id="0208c-156">abcd.contoso.com</span><span class="sxs-lookup"><span data-stu-id="0208c-156">abcd.contoso.com</span></span>

   <span data-ttu-id="0208c-157">앱의 사용자 지정 도메인 이름을 알고 있는 경우 해당 사용자 지정 도메인 이름과 충돌하지 않는 ILB ASE의 도메인을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-157">If you know the custom domain names for your apps, choose a domain for the ILB ASE that won’t have a conflict with those custom domain names.</span></span> <span data-ttu-id="0208c-158">이 예제에서는 *.contoso.com*으로 끝나는 사용자 지정 도메인 이름과 충돌하지 않는 *contoso-internal.com*과 같은 이름을 ASE의 도메인에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-158">In this example, you can use something like *contoso-internal.com* for the domain of your ASE because that won't conflict with custom domain names that end in *.contoso.com*.</span></span>

8. <span data-ttu-id="0208c-159">**확인**을 선택하고 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-159">Select **OK**, and then select **Create**.</span></span>

    ![ASE 만들기][1]

<span data-ttu-id="0208c-161">**Virtual Network** 블레이드에는 **Virtual Network 구성** 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-161">On the **Virtual Network** blade, there is a **Virtual Network Configuration** option.</span></span> <span data-ttu-id="0208c-162">이 옵션을 사용하여 외부 VIP 또는 내부 VIP를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-162">You can use it to select an External VIP or an Internal VIP.</span></span> <span data-ttu-id="0208c-163">기본값은 **외부**입니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-163">The default is **External**.</span></span> <span data-ttu-id="0208c-164">**외부**를 선택한 경우 ASE는 인터넷 액세스 가능 VIP를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-164">If you select **External**, your ASE uses an internet-accessible VIP.</span></span> <span data-ttu-id="0208c-165">**내부**를 선택하는 경우 ASE가 VNet 내의 IP 주소에 있는 ILB로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-165">If you select **Internal**, your ASE is configured with an ILB on an IP address within your VNet.</span></span>

<span data-ttu-id="0208c-166">**내부**를 선택한 후에 ASE에 더 많은 IP 주소를 추가하는 기능이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-166">After you select **Internal**, the ability to add more IP addresses to your ASE is removed.</span></span> <span data-ttu-id="0208c-167">대신 ASE의 도메인을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-167">Instead, you need to provide the domain of the ASE.</span></span> <span data-ttu-id="0208c-168">외부 VIP가 있는 ASE에서 ASE의 이름은 해당 ASE에서 만든 앱에 대한 도메인에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-168">In an ASE with an External VIP, the name of the ASE is used in the domain for apps created in that ASE.</span></span>

<span data-ttu-id="0208c-169">**VIP 형식**을 **내부**로 설정한 경우 ASE 이름은 해당 ASE의 도메인에서 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-169">If you set **VIP Type** to **Internal**, your ASE name is not used in the domain for the ASE.</span></span> <span data-ttu-id="0208c-170">도메인을 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-170">You specify the domain explicitly.</span></span> <span data-ttu-id="0208c-171">도메인이 *contoso.corp.net*이고 해당 ASE에서 *timereporting*이라는 앱을 만들었으면 해당 앱의 URL은 timereporting.contoso.corp.net이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-171">If your domain is *contoso.corp.net* and you create an app in that ASE named *timereporting*, the URL for that app is timereporting.contoso.corp.net.</span></span>


## <a name="create-an-app-in-an-ilb-ase"></a><span data-ttu-id="0208c-172">ILB ASE에 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="0208c-172">Create an app in an ILB ASE</span></span> ##

<span data-ttu-id="0208c-173">일반적으로 ASE에서 앱을 만드는 것과 동일한 방식으로 ILB ASE에서 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-173">You create an app in an ILB ASE in the same way that you create an app in an ASE normally.</span></span>

1. <span data-ttu-id="0208c-174">Azure Portal에서 **새로 만들기** > **웹 + 모바일** > **웹**을 선택하거나 **모바일** 또는 **API App**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-174">In the Azure portal, select **New** > **Web + Mobile** > **Web** or **Mobile** or **API App**.</span></span>

2. <span data-ttu-id="0208c-175">앱의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-175">Enter the name of the app.</span></span>

3. <span data-ttu-id="0208c-176">구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-176">Select the subscription.</span></span>

4. <span data-ttu-id="0208c-177">리소스 그룹을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-177">Select or create a resource group.</span></span>

5. <span data-ttu-id="0208c-178">App Service 계획을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-178">Select or create an App Service plan.</span></span> <span data-ttu-id="0208c-179">새 App Service 계획을 만들려는 경우 ASE를 위치로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-179">If you want to create a new App Service plan, select your ASE as the location.</span></span> <span data-ttu-id="0208c-180">App Service 계획을 만들려는 작업자 풀을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-180">Select the worker pool where you want your App Service plan to be created.</span></span> <span data-ttu-id="0208c-181">App Service 계획을 만들 때 위치 및 작업자 풀로 ASE를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-181">When you create the App Service plan, select your ASE as the location and the worker pool.</span></span> <span data-ttu-id="0208c-182">앱의 이름을 지정하면 앱 이름 아래의 도메인을 ASE에 대한 도메인으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-182">When you specify the name of the app, the domain under your app name is replaced by the domain for your ASE.</span></span>

6. <span data-ttu-id="0208c-183">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-183">Select **Create**.</span></span> <span data-ttu-id="0208c-184">앱을 대시보드에 표시하려면 **대시보드에 고정** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-184">If you want the app to appear on your dashboard, select the **Pin to dashboard** check box.</span></span>

    ![App Service 계획 생성][2]

    <span data-ttu-id="0208c-186">**앱** 이름 아래에서 도메인 이름이 ASE의 도메인을 반영하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-186">Under **App name**, the domain name is updated to reflect the domain of your ASE.</span></span>

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="0208c-187">ILB ASE 생성 후 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="0208c-187">Post-ILB ASE creation validation</span></span> ##

<span data-ttu-id="0208c-188">ILB ASE는 비 ILB ASE와는 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-188">An ILB ASE is slightly different than the non-ILB ASE.</span></span> <span data-ttu-id="0208c-189">이미 설명한 대로 고유의 DNS을 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-189">As already noted, you need to manage your own DNS.</span></span> <span data-ttu-id="0208c-190">또한 HTTPS 연결에 고유한 인증서를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-190">You also have to provide your own certificate for HTTPS connections.</span></span>

<span data-ttu-id="0208c-191">ASE를 만든 후에 도메인 이름은 지정된 도메인을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-191">After you create your ASE, the domain name shows the domain you specified.</span></span> <span data-ttu-id="0208c-192">**ILB 인증서**라는 **설정** 메뉴에서 새 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-192">A new item appears in the **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="0208c-193">ILB ASE 도메인을 지정하지 않는 인증서로 ASE가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-193">The ASE is created with a certificate that doesn't specify the ILB ASE domain.</span></span> <span data-ttu-id="0208c-194">해당 인증서로 ASE를 사용하는 경우 브라우저에서 올바르지 않음을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-194">If you use the ASE with that certificate, your browser tells you that it's invalid.</span></span> <span data-ttu-id="0208c-195">이 인증서를 사용하면 쉽게 HTTPS를 테스트할 수 있지만 ILB ASE 도메인에 연결된 고유한 인증서를 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-195">This certificate makes it easier to test HTTPS, but you need to upload your own certificate that's tied to your ILB ASE domain.</span></span> <span data-ttu-id="0208c-196">인증서가 자체 서명되었는지 인증 기관에서 얻었는지에 관계없이 이 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-196">This step is necessary regardless of whether your certificate is self-signed or acquired from a certificate authority.</span></span>

![ILB ASE 도메인 이름][3]

<span data-ttu-id="0208c-198">ILB ASE에는 유효한 SSL 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-198">Your ILB ASE needs a valid SSL certificate.</span></span> <span data-ttu-id="0208c-199">내부 인증 기관을 사용하거나, 외부 발급자로부터 인증서를 구입하거나, 자체 서명된 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-199">Use internal certificate authorities, purchase a certificate from an external issuer, or use a self-signed certificate.</span></span> <span data-ttu-id="0208c-200">SSL 인증서의 소스에 관계 없이 다음과 같은 인증서 특성을 올바르게 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-200">Regardless of the source of the SSL certificate, the following certificate attributes need to be configured properly:</span></span>

* <span data-ttu-id="0208c-201">**주체**: 이 특성은 *.your-root-domain-here로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-201">**Subject**: This attribute must be set to *.your-root-domain-here.</span></span>
* <span data-ttu-id="0208c-202">**주체 대체 이름**: 이 특성에는 **.your-root-domain-here* 및 **.scm.your-root-domain-here* 둘 다 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-202">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here* and **.scm.your-root-domain-here*.</span></span> <span data-ttu-id="0208c-203">각 앱과 연결된 SCM/Kudu 사이트에 대한 SSL 연결은 *your-app-name.scm.your-root-domain-here* 양식의 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-203">SSL connections to the SCM/Kudu site associated with each app use an address of the form *your-app-name.scm.your-root-domain-here*.</span></span>

<span data-ttu-id="0208c-204">SSL 인증서를 .pfx 파일로 변환/저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-204">Convert/save the SSL certificate as a .pfx file.</span></span> <span data-ttu-id="0208c-205">.pfx 파일에는 모든 중간 인증서와 루트 인증서가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-205">The .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="0208c-206">암호로 인증서를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-206">Secure it with a password.</span></span>

<span data-ttu-id="0208c-207">자체 서명된 인증서를 만들려는 경우 여기에서 PowerShell 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-207">If you want to create a self-signed certificate, you can use the PowerShell commands here.</span></span> <span data-ttu-id="0208c-208">*internal.contoso.com* 대신 ILB ASE 도메인 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-208">Be sure to use your ILB ASE domain name instead of *internal.contoso.com*:</span></span> 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

<span data-ttu-id="0208c-209">다음과 같은 PowerShell 명령이 생성한 인증서는 브라우저의 신뢰 체인에 있는 인증 기관에서 만들어지지 않았기 때문에 브라우저에서 플래그 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-209">The certificate that these PowerShell commands generate is flagged by browsers because the certificate wasn't created by a certificate authority that's in your browser's chain of trust.</span></span> <span data-ttu-id="0208c-210">브라우저에서 신뢰하는 인증서를 가져오려면 브라우저의 신뢰 체인에 있는 상용 인증 기관으로부터 확보합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-210">To get a certificate that your browser trusts, procure it from a commercial certificate authority in your browser's chain of trust.</span></span> 

![ILB 인증서 설정][4]

<span data-ttu-id="0208c-212">고유한 인증서를 업로드하고 액세스를 테스트하려면:</span><span class="sxs-lookup"><span data-stu-id="0208c-212">To upload your own certificates and test access:</span></span>

1. <span data-ttu-id="0208c-213">ASE를 만든 후에 ASE UI로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-213">After the ASE is created, go to the ASE UI.</span></span> <span data-ttu-id="0208c-214">**ASE** > **설정** > **ILB 인증서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-214">Select **ASE** > **Settings** > **ILB Certificate**.</span></span>

2. <span data-ttu-id="0208c-215">ILB 인증서를 설정하려면 인증서 pfx 파일을 선택하고 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-215">To set the ILB certificate, select the certificate .pfx file and enter the password.</span></span> <span data-ttu-id="0208c-216">이 단계를 처리하는 데 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-216">This step takes some time to process.</span></span> <span data-ttu-id="0208c-217">업로드 작업이 진행 중이라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-217">A message appears stating that an upload operation is in progress.</span></span>

3. <span data-ttu-id="0208c-218">ASE에 ILB 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-218">Get the ILB address for your ASE.</span></span> <span data-ttu-id="0208c-219">**ASE** > **속성** > **가상 IP 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-219">Select **ASE** > **Properties** > **Virtual IP Address**.</span></span>

4. <span data-ttu-id="0208c-220">ASE를 만든 후에 해당 ASE에서 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-220">Create a web app in your ASE after the ASE is created.</span></span>

5. <span data-ttu-id="0208c-221">VM이 VNet에 없는 경우 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-221">Create a VM if you don't have one in that VNet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0208c-222">실패하거나 문제를 일으키기 때문에 이 VM를 ASE와 동일한 서브넷에 만들려고 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-222">Don't try to create this VM in the same subnet as the ASE because it will fail or cause problems.</span></span>
    >
    >

6. <span data-ttu-id="0208c-223">ASE 도메인에 DNS를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-223">Set the DNS for your ASE domain.</span></span> <span data-ttu-id="0208c-224">DNS에 있는 도메인에서 와일드 카드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-224">You can use a wildcard with your domain in your DNS.</span></span> <span data-ttu-id="0208c-225">몇 가지 간단한 테스트를 수행하려면 VIP IP 주소에 웹앱 이름을 설정하도록 VM에 대한 호스트 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-225">To do some simple tests, edit the hosts file on your VM to set the web app name to the VIP IP address:</span></span>

    <span data-ttu-id="0208c-226">a.</span><span class="sxs-lookup"><span data-stu-id="0208c-226">a.</span></span> <span data-ttu-id="0208c-227">ASE의 도메인 이름이 _.ilbase.com_이고 _mytestapp_이라는 웹앱을 만든 경우 _mytestapp.ilbase.com_으로 주소가 지정됩니다. 그런 다음 _mytestapp.ilbase.com_을 설정하여 ILB 주소로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-227">If your ASE has the domain name _.ilbase.com_ and you create the web app named _mytestapp_, it's addressed at _mytestapp.ilbase.com_. You then set _mytestapp.ilbase.com_ to resolve to the ILB address.</span></span> <span data-ttu-id="0208c-228">(Windows에서 호스트 파일은 _C:\Windows\System32\drivers\etc\_에 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="0208c-228">(On Windows, the hosts file is at _C:\Windows\System32\drivers\etc\_.)</span></span>

    <span data-ttu-id="0208c-229">b.</span><span class="sxs-lookup"><span data-stu-id="0208c-229">b.</span></span> <span data-ttu-id="0208c-230">웹 배포 게시를 테스트하거나 고급 콘솔에 액세스하려면 _mytestapp.scm.ilbase.com_의 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-230">To test web deployment publishing or access to the advanced console, create a record for _mytestapp.scm.ilbase.com_.</span></span>

7. <span data-ttu-id="0208c-231">해당 VM에서 브라우저를 사용하고 http://mytestapp.ilbase.com으로 이동합니다. (또는 도메인에서 웹앱 이름으로 이동합니다.)</span><span class="sxs-lookup"><span data-stu-id="0208c-231">Use a browser on that VM and go to http://mytestapp.ilbase.com. (Or go to whatever your web app name is with your domain.)</span></span>

8. <span data-ttu-id="0208c-232">해당 VM에서 브라우저를 사용하고 https://mytestapp.ilbase.com으로 이동합니다. 자체 서명된 인증서를 사용하는 경우 보안 부족에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-232">Use a browser on that VM and go to https://mytestapp.ilbase.com. If you use a self-signed certificate, accept the lack of security.</span></span>

    <span data-ttu-id="0208c-233">ILB의 IP 주소가 **IP 주소**에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-233">The IP address for your ILB is listed under **IP addresses**.</span></span> <span data-ttu-id="0208c-234">이 목록에는 외부 VIP 및 인바운드 관리 트래픽에 사용하는 IP 주소도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-234">This list also has the IP addresses used by the external VIP and for inbound management traffic.</span></span>

    ![ILB IP 주소][5]

### <a name="web-jobs-functions-and-the-ilb-ase"></a><span data-ttu-id="0208c-236">웹 작업, 함수 및 ILB ASE</span><span class="sxs-lookup"><span data-stu-id="0208c-236">Web jobs, Functions and the ILB ASE</span></span>

<span data-ttu-id="0208c-237">함수 및 웹 작업 모두 ILB ASE에서 지원되지만 포털에서 작동되려면 네트워크를 통해 SCM 사이트에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-237">Both Functions and web jobs are supported on an ILB ASE but for the portal to work with them, you must have network access to the SCM site.</span></span>  <span data-ttu-id="0208c-238">즉, 가상 네트워크에 있거나 가상 네트워크에 연결된 호스트에 브라우저가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-238">This means your browser must either be on a host that is either in or connected to the virtual network.</span></span>  

<span data-ttu-id="0208c-239">ILB ASE에서 Azure Functions를 사용할 경우 다음과 같은 오류 메시지가 발생할 수 있습니다. "함수를 지금 바로 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-239">When you use Azure Functions on an ILB ASE, you might get an error message that says "We are not able to retrieve your functions right now.</span></span> <span data-ttu-id="0208c-240">나중에 다시 시도하십시오."</span><span class="sxs-lookup"><span data-stu-id="0208c-240">Please try again later."</span></span> <span data-ttu-id="0208c-241">이 오류는 Functions UI가 HTTPS를 통해 SCM 사이트를 사용하며 루트 인증서가 브라우저의 신뢰 체인에 없기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-241">This error occurs because the Functions UI leverages the SCM site over HTTPS and the root certificate is not in the browser chain of trust.</span></span> <span data-ttu-id="0208c-242">웹 작업에도 비슷한 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-242">Web jobs has a similar problem.</span></span> <span data-ttu-id="0208c-243">이 문제를 방지하기 위해 다음 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-243">To avoid this problem you can do one of the following:</span></span>

- <span data-ttu-id="0208c-244">신뢰할 수 있는 인증서 저장소에 인증서를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-244">Add the certificate to your trusted certificate store.</span></span> <span data-ttu-id="0208c-245">그러면 Edge 및 Internet Explorer가 차단 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-245">This unblocks Edge and Internet Explorer.</span></span>
- <span data-ttu-id="0208c-246">Chrome을 사용하고 먼저 SCM 사이트로 이동한 후 신뢰할 수 없는 인증서를 수락한 다음 포털로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-246">Use Chrome and go to the SCM site first, accept the untrusted certificate and then go to the portal.</span></span>
- <span data-ttu-id="0208c-247">브라우저의 신뢰 체인에 있는 상용 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-247">Use a commercial certificate that is in your browser chain of trust.</span></span>  <span data-ttu-id="0208c-248">이것이 최상의 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-248">This is the best option.</span></span>  

## <a name="dns-configuration"></a><span data-ttu-id="0208c-249">DNS 구성</span><span class="sxs-lookup"><span data-stu-id="0208c-249">DNS configuration</span></span> ##

<span data-ttu-id="0208c-250">외부 VIP를 사용하는 경우 DNS가 Azure에서 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-250">When you use an External VIP, the DNS is managed by Azure.</span></span> <span data-ttu-id="0208c-251">ASE에서 만든 모든 앱은 공용 DNS에 해당하는 Azure DNS에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-251">Any app created in your ASE is automatically added to Azure DNS, which is a public DNS.</span></span> <span data-ttu-id="0208c-252">ILB ASE에서 자체 DNS를 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-252">In an ILB ASE, you must manage your own DNS.</span></span> <span data-ttu-id="0208c-253">_contoso.net_과 지정된 도메인의 경우 다음에 대해 ILB 주소를 가리키는 DNS에서 DNS A 레코드를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-253">For a given domain such as _contoso.net_, you need to create DNS A records in your DNS that point to your ILB address for:</span></span>

- <span data-ttu-id="0208c-254">*.contoso.net</span><span class="sxs-lookup"><span data-stu-id="0208c-254">*.contoso.net</span></span>
- <span data-ttu-id="0208c-255">*.scm.contoso.net</span><span class="sxs-lookup"><span data-stu-id="0208c-255">*.scm.contoso.net</span></span>

<span data-ttu-id="0208c-256">ILB ASE 도메인이 해당 ASE 외부에서 여러 작업에 사용되는 경우 앱 이름 기준으로 DNS에서 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-256">If your ILB ASE domain is used for multiple things outside this ASE, you might need to manage DNS on a per-app-name basis.</span></span> <span data-ttu-id="0208c-257">이 방법은 새 앱을 만들 때 각 앱 이름을 DNS에 추가해야 하기 때문에 더 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-257">This method is challenging because you need to add each new app name into your DNS when you create it.</span></span> <span data-ttu-id="0208c-258">이러한 이유로 전용 도메인을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-258">For this reason, we recommend that you use a dedicated domain.</span></span>

## <a name="publish-with-an-ilb-ase"></a><span data-ttu-id="0208c-259">ILB ASE로 게시</span><span class="sxs-lookup"><span data-stu-id="0208c-259">Publish with an ILB ASE</span></span> ##

<span data-ttu-id="0208c-260">만든 모든 앱에는 두 개의 끝점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-260">For every app that's created, there are two endpoints.</span></span> <span data-ttu-id="0208c-261">ILB ASE에는 *&lt;앱 이름>.&lt;ILB ASE 도메인>*과 *&lt;앱 이름>.scm.&lt; ILB ASE 도메인>*이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-261">In an ILB ASE, you have *&lt;app name>.&lt;ILB ASE Domain>* and *&lt;app name>.scm.&lt;ILB ASE Domain>*.</span></span> 

<span data-ttu-id="0208c-262">SCM 사이트 이름은 Azure Portal 내에서 **고급 포털**이라고 하는 Kudu 콘솔로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-262">The SCM site name takes you to the Kudu console, called the **Advanced portal**, within the Azure portal.</span></span> <span data-ttu-id="0208c-263">Kudu 콘솔을 통해 환경 변수를 확인하고, 디스크를 탐색하고, 콘솔을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-263">The Kudu console lets you view environment variables, explore the disk, use a console, and much more.</span></span> <span data-ttu-id="0208c-264">자세한 내용은 [Azure App Service의 Kudu 콘솔][Kudu]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0208c-264">For more information, see [Kudu console for Azure App Service][Kudu].</span></span> 

<span data-ttu-id="0208c-265">다중 테넌트 App Service 및 외부 ASE에는 Azure Portal과 Kudu 콘솔 간의 Single Sign-On이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-265">In the multitenant App Service and in an External ASE, there's single sign-on between the Azure portal and the Kudu console.</span></span> <span data-ttu-id="0208c-266">그러나 ILB ASE의 경우 게시 자격 증명을 사용하여 Kudu 콘솔에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-266">For the ILB ASE, however, you need to use your publishing credentials to sign into the Kudu console.</span></span>

<span data-ttu-id="0208c-267">ILB ASE에서는 GitHub, Visual Studio Team Services 등의 인터넷 기반 CI 시스템이 작동하지 않습니다. 게시 끝점이 인터넷에 액세스할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-267">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because the publishing endpoint isn't internet accessible.</span></span> <span data-ttu-id="0208c-268">대신 끌어오기 모델을 사용하는 CI 시스템(예: Dropbox)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-268">Instead, you need to use a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="0208c-269">ILB ASE의 앱에 대한 게시 끝점에서는 ILB ASE가 만들어진 도메인을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-269">The publishing endpoints for apps in an ILB ASE use the domain that the ILB ASE was created with.</span></span> <span data-ttu-id="0208c-270">이 도메인은 앱의 게시 프로필과 앱의 포털 블레이드(**개요** > **Essentials** 및 **속성**)에서 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-270">This domain appears in the app's publishing profile and in the app's portal blade (**Overview** > **Essentials** and also **Properties**).</span></span> <span data-ttu-id="0208c-271">하위 도메인이 *contoso.net*인 ILB ASE 및 *mytest*라는 앱이 있는 경우 FTP에 *mytest.contoso.net*을 사용하고 웹 배포에 *mytest.scm.contoso.net*을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-271">If you have an ILB ASE with the subdomain *contoso.net* and an app named *mytest*, use *mytest.contoso.net* for FTP and *mytest.scm.contoso.net* for web deployment.</span></span>

## <a name="couple-an-ilb-ase-with-a-waf-device"></a><span data-ttu-id="0208c-272">WAF 장치로 ILB ASE 연결</span><span class="sxs-lookup"><span data-stu-id="0208c-272">Couple an ILB ASE with a WAF device</span></span> ##

<span data-ttu-id="0208c-273">Azure App Service는 시스템을 보호하는 많은 보안 조치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-273">Azure App Service provides many security measures that protect the system.</span></span> <span data-ttu-id="0208c-274">앱이 해킹되었는지를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-274">They also help to determine whether an app was hacked.</span></span> <span data-ttu-id="0208c-275">웹 응용 프로그램을 보호하기 위해 WAF(웹 응용 프로그램 방화벽)를 사용하여 Azure App Service와 같은 호스팅 플랫폼을 결합해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-275">The best protection for a web application is to couple a hosting platform, such as Azure App Service, with a web application firewall (WAF).</span></span> <span data-ttu-id="0208c-276">ILB ASE에 네트워크 격리 응용 프로그램 끝점이 있기 때문에 사용하기에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-276">Because the ILB ASE has a network-isolated application endpoint, it's appropriate for such a use.</span></span>

<span data-ttu-id="0208c-277">WAF 장치를 사용하여 ILB ASE를 구성하는 방법에 대한 자세한 내용은 [App Service Environment를 사용하여 웹 응용 프로그램 방화벽 구성][ASEWAF]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0208c-277">To learn more about how to configure your ILB ASE with a WAF device, see [Configure a web application firewall with your App Service environment][ASEWAF].</span></span> <span data-ttu-id="0208c-278">이 문서에서는 ASE를 사용하여 Barracuda 가상 어플라이언스를 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-278">This article shows how to use a Barracuda virtual appliance with your ASE.</span></span> <span data-ttu-id="0208c-279">다른 방법은 Azure Application Gateway를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-279">Another option is to use Azure Application Gateway.</span></span> <span data-ttu-id="0208c-280">Application Gateway는 이후에 배치할 모든 응용 프로그램을 보호하기 위해 OWASP 핵심 규칙을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-280">Application Gateway uses the OWASP core rules to secure any applications placed behind it.</span></span> <span data-ttu-id="0208c-281">Application Gateway에 대한 자세한 내용은 [Azure 웹 응용 프로그램 방화벽 소개][AppGW]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0208c-281">For more information about Application Gateway, see [Introduction to the Azure web application firewall][AppGW].</span></span>

## <a name="get-started"></a><span data-ttu-id="0208c-282">시작</span><span class="sxs-lookup"><span data-stu-id="0208c-282">Get started</span></span> ##

<span data-ttu-id="0208c-283">ASE에 대한 모든 문서와 지침은 [App Service Environment의 추가 정보][ASEReadme]에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0208c-283">All articles and how-to instructions for ASEs are available in the [README for App Service environments][ASEReadme].</span></span>

* <span data-ttu-id="0208c-284">ASE를 시작하려면 [App Service Environment 소개][Intro]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0208c-284">To get started with ASEs, see [Introduction to App Service environments][Intro].</span></span>
* <span data-ttu-id="0208c-285">Azure App Service 플랫폼에 대한 자세한 내용은 [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0208c-285">For more information about the Azure App Service platform, see [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span></span>
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

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
