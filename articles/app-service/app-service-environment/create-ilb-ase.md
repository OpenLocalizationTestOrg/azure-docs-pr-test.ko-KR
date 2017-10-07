---
title: "aaaCreate 및 Azure 앱 서비스 환경에는 내부 부하 분산 장치 사용"
description: "자세한 방법은 toocreate 인터넷 격리 Azure 앱 서비스 환경 사용"
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
ms.openlocfilehash: d019ca6f231c3acfdab4cd380db375a076802f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="69f70-103">App Service Environment에서 내부 부하 분산 장치 만들기 및 사용</span><span class="sxs-lookup"><span data-stu-id="69f70-103">Create and use an internal load balancer with an App Service environment</span></span> #

 <span data-ttu-id="69f70-104">Azure App Service Environment는 Azure App Service를 Azure VNet(Virtual Network)의 서브넷에 배포한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="69f70-105">앱 서비스 환경 (ASE)는 두 가지 방법으로 toodeploy:</span><span class="sxs-lookup"><span data-stu-id="69f70-105">There are two ways toodeploy an App Service environment (ASE):</span></span> 

- <span data-ttu-id="69f70-106">외부 ASE라고도 하는 외부 IP 주소의 VIP 사용</span><span class="sxs-lookup"><span data-stu-id="69f70-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="69f70-107">내부 IP 주소에 VIP와 ILB ASE 때문에 라고도 hello 내부 끝점은 내부 부하 분산 장치 (ILB).</span><span class="sxs-lookup"><span data-stu-id="69f70-107">With a VIP on an internal IP address, often called an ILB ASE because hello internal endpoint is an internal load balancer (ILB).</span></span> 

<span data-ttu-id="69f70-108">이 문서에서는 ILB ASE toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-108">This article shows you how toocreate an ILB ASE.</span></span> <span data-ttu-id="69f70-109">ASE hello에 대 한 개요를 참조 하세요. [소개 tooApp 서비스 환경][Intro]합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-109">For an overview on hello ASE, see [Introduction tooApp Service environments][Intro].</span></span> <span data-ttu-id="69f70-110">toocreate 외부 ASE를 확인 하려면 어떻게 toolearn [외부 ASE 만들][MakeExternalASE]합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-110">toolearn how toocreate an External ASE, see [Create an External ASE][MakeExternalASE].</span></span>

## <a name="overview"></a><span data-ttu-id="69f70-111">개요</span><span class="sxs-lookup"><span data-stu-id="69f70-111">Overview</span></span> ##

<span data-ttu-id="69f70-112">VNet의 인터넷 액세스 가능 끝점 또는 IP 주소를 사용하여 ASE를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-112">You can deploy an ASE with an internet-accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="69f70-113">tooset hello IP 주소 tooa VNet 주소, hello ASE 받는 ILB 함께 배포 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-113">tooset hello IP address tooa VNet address, hello ASE must be deployed with an ILB.</span></span> <span data-ttu-id="69f70-114">ILB를 사용하여 ASE를 배포하는 경우 다음과 같은 항목을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-114">When you deploy your ASE with an ILB, you must provide:</span></span>

-   <span data-ttu-id="69f70-115">앱을 만들 때 사용하는 고유한 도메인</span><span class="sxs-lookup"><span data-stu-id="69f70-115">Your own domain that you use when you create your apps.</span></span>
-   <span data-ttu-id="69f70-116">HTTPS에 사용 되는 hello 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-116">hello certificate used for HTTPS.</span></span>
-   <span data-ttu-id="69f70-117">도메인에 대한 DNS 관리</span><span class="sxs-lookup"><span data-stu-id="69f70-117">DNS management for your domain.</span></span>

<span data-ttu-id="69f70-118">결과적으로 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-118">In return, you can do things such as:</span></span>

-   <span data-ttu-id="69f70-119">사이트 간 또는 Azure ExpressRoute VPN을 통해 액세스 하는 hello 클라우드에 안전 하 게 인트라넷 응용 프로그램을 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-119">Host intranet applications securely in hello cloud, which you access through a site-to-site or Azure ExpressRoute VPN.</span></span>
-   <span data-ttu-id="69f70-120">공용 DNS 서버에는 없지만 hello 클라우드에서 호스트 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-120">Host apps in hello cloud that aren't listed in public DNS servers.</span></span>
-   <span data-ttu-id="69f70-121">프런트 엔드 앱이 안전하게 통합될 수 있는 인터넷 격리 백 엔드 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="69f70-121">Create internet-isolated back-end apps, which your front-end apps can securely integrate with.</span></span>

### <a name="disabled-functionality"></a><span data-ttu-id="69f70-122">사용되지 않도록 설정된 기능</span><span class="sxs-lookup"><span data-stu-id="69f70-122">Disabled functionality</span></span> ###

<span data-ttu-id="69f70-123">ILB ASE를 사용하는 경우 수행할 수 없는 작업도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-123">There are some things that you can't do when you use an ILB ASE:</span></span>

-   <span data-ttu-id="69f70-124">IP 기반 SSL 사용</span><span class="sxs-lookup"><span data-stu-id="69f70-124">Use IP-based SSL.</span></span>
-   <span data-ttu-id="69f70-125">Toospecific 앱 IP 주소를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-125">Assign IP addresses toospecific apps.</span></span>
-   <span data-ttu-id="69f70-126">구입 하 고 hello Azure 포털을 통해 응용 프로그램과 함께 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-126">Buy and use a certificate with an app through hello Azure portal.</span></span> <span data-ttu-id="69f70-127">직접 인증 기관에서 직접 인증서를 가져와서 앱에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-127">You can obtain certificates directly from a certificate authority and use them with your apps.</span></span> <span data-ttu-id="69f70-128">Hello Azure 포털을 통해 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-128">You can't obtain them through hello Azure portal.</span></span>

## <a name="create-an-ilb-ase"></a><span data-ttu-id="69f70-129">ILB ASE 만들기</span><span class="sxs-lookup"><span data-stu-id="69f70-129">Create an ILB ASE</span></span> ##

<span data-ttu-id="69f70-130">ILB ASE toocreate:</span><span class="sxs-lookup"><span data-stu-id="69f70-130">toocreate an ILB ASE:</span></span>

1. <span data-ttu-id="69f70-131">Hello Azure 포털에서에서 선택 **새로** > **웹 + 모바일** > **앱 서비스 환경**합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-131">In hello Azure portal, select **New** > **Web + Mobile** > **App Service Environment**.</span></span>

2. <span data-ttu-id="69f70-132">사용 중인 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-132">Select your subscription.</span></span>

3. <span data-ttu-id="69f70-133">리소스 그룹을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-133">Select or create a resource group.</span></span>

4. <span data-ttu-id="69f70-134">VNet을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-134">Select or create a VNet.</span></span>

5. <span data-ttu-id="69f70-135">기존 VNet을 선택한 경우 toocreate 서브넷 toohold hello ASE 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-135">If you select an existing VNet, you need toocreate a subnet toohold hello ASE.</span></span> <span data-ttu-id="69f70-136">Tooset 서브넷 크기 충분히 큰 tooaccommodate 향후 성장에 ASE에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-136">Make sure tooset a subnet size large enough tooaccommodate any future growth of your ASE.</span></span> <span data-ttu-id="69f70-137">`/25` 크기를 사용하는 것이 좋습니다. 그러면 128개의 주소가 있고 최대 크기의 ASE를 다룰 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-137">We recommend a size of `/25`, which has 128 addresses and can handle a maximum-sized ASE.</span></span> <span data-ttu-id="69f70-138">hello 최소 크기를 선택할 수 있습니다는 `/28`합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-138">hello minimum size you can select is a `/28`.</span></span> <span data-ttu-id="69f70-139">인프라 요구, 후이 크기에는 크기 조정 된 tooa 최대 11 인스턴스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-139">After infrastructure needs, this size can be scaled tooa maximum of 11 instances.</span></span>

    * <span data-ttu-id="69f70-140">앱 서비스 계획에 hello 기본 최대 100 개를 초과 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-140">Go beyond hello default maximum of 100 instances in your App Service plans.</span></span>

    * <span data-ttu-id="69f70-141">더 신속한 프런트 엔드 확장으로 100개 가까이 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-141">Scale near 100 but with more rapid front-end scaling.</span></span>

6. <span data-ttu-id="69f70-142">**Virtual Network/위치** > **Virtual Network 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-142">Select **Virtual Network/Location** > **Virtual Network Configuration**.</span></span> <span data-ttu-id="69f70-143">집합 hello **VIP 유형** 너무**내부**합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-143">Set hello **VIP Type** too**Internal**.</span></span>

7. <span data-ttu-id="69f70-144">도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-144">Enter a domain name.</span></span> <span data-ttu-id="69f70-145">이 도메인은 hello이이 ASE에서 만든 앱에 사용 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-145">This domain is hello one used for apps created in this ASE.</span></span> <span data-ttu-id="69f70-146">몇 가지 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-146">There are some restrictions.</span></span> <span data-ttu-id="69f70-147">다음 항목을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-147">It can't be:</span></span>

    * <span data-ttu-id="69f70-148">net</span><span class="sxs-lookup"><span data-stu-id="69f70-148">net</span></span>   

    * <span data-ttu-id="69f70-149">azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="69f70-149">azurewebsites.net</span></span>

    * <span data-ttu-id="69f70-150">p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="69f70-150">p.azurewebsites.net</span></span>

    * <span data-ttu-id="69f70-151">&lt;asename&gt;.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="69f70-151">&lt;asename&gt;.p.azurewebsites.net</span></span>

   <span data-ttu-id="69f70-152">앱에 대 한 hello 사용자 지정 도메인 이름을 사용 하 고 프로그램 ASE 사용 하는 hello 도메인 이름을 겹칠 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-152">hello custom domain name used for apps and hello domain name used by your ASE can't overlap.</span></span> <span data-ttu-id="69f70-153">Hello 도메인 이름의 ILB ASE에 대 한 _contoso.com_, 같은 앱에 대 한 사용자 지정 도메인 이름을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-153">For an ILB ASE with hello domain name _contoso.com_, you can't use custom domain names for your apps like:</span></span>

    * <span data-ttu-id="69f70-154">www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="69f70-154">www.contoso.com</span></span>

    * <span data-ttu-id="69f70-155">abcd.def.contoso.com</span><span class="sxs-lookup"><span data-stu-id="69f70-155">abcd.def.contoso.com</span></span>

    * <span data-ttu-id="69f70-156">abcd.contoso.com</span><span class="sxs-lookup"><span data-stu-id="69f70-156">abcd.contoso.com</span></span>

   <span data-ttu-id="69f70-157">앱에 대 한 사용자 지정 도메인 이름을 hello를 알고 있는 경우 해당 사용자 지정 도메인 이름으로 충돌을 잊은 ILB ASE hello에 대 한 도메인을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-157">If you know hello custom domain names for your apps, choose a domain for hello ILB ASE that won’t have a conflict with those custom domain names.</span></span> <span data-ttu-id="69f70-158">이 예제에서는 다음과 같이 사용할 수 있습니다 *contoso internal.com* 프로그램 ASE의 hello 도메인에 대 한 사용자 지정 도메인 이름으로 끝나는와 충돌 하지 않음 하 때문에 *. contoso.com*합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-158">In this example, you can use something like *contoso-internal.com* for hello domain of your ASE because that won't conflict with custom domain names that end in *.contoso.com*.</span></span>

8. <span data-ttu-id="69f70-159">**확인**을 선택하고 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-159">Select **OK**, and then select **Create**.</span></span>

    ![ASE 만들기][1]

<span data-ttu-id="69f70-161">Hello에 **가상 네트워크** 블레이드에서는 **가상 네트워크 구성** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-161">On hello **Virtual Network** blade, there is a **Virtual Network Configuration** option.</span></span> <span data-ttu-id="69f70-162">외부 VIP 또는 내부 VIP tooselect을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-162">You can use it tooselect an External VIP or an Internal VIP.</span></span> <span data-ttu-id="69f70-163">hello 기본값은 **외부**합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-163">hello default is **External**.</span></span> <span data-ttu-id="69f70-164">**외부**를 선택한 경우 ASE는 인터넷 액세스 가능 VIP를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-164">If you select **External**, your ASE uses an internet-accessible VIP.</span></span> <span data-ttu-id="69f70-165">**내부**를 선택하는 경우 ASE가 VNet 내의 IP 주소에 있는 ILB로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-165">If you select **Internal**, your ASE is configured with an ILB on an IP address within your VNet.</span></span>

<span data-ttu-id="69f70-166">선택한 후 **내부**, hello 기능 tooadd IP 주소가 많을 수록 tooyour ASE 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-166">After you select **Internal**, hello ability tooadd more IP addresses tooyour ASE is removed.</span></span> <span data-ttu-id="69f70-167">대신, tooprovide hello 도메인의 hello ASE 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-167">Instead, you need tooprovide hello domain of hello ASE.</span></span> <span data-ttu-id="69f70-168">Hello 이름 ASE 해당 ASE에서 만든 앱에 대 한 hello 도메인에서 사용 되는 hello의 외부 VIP와 ASE에.</span><span class="sxs-lookup"><span data-stu-id="69f70-168">In an ASE with an External VIP, hello name of hello ASE is used in hello domain for apps created in that ASE.</span></span>

<span data-ttu-id="69f70-169">설정한 경우 **VIP 유형** 너무**내부**, ASE 이름 ASE hello에 대 한 hello 도메인에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-169">If you set **VIP Type** too**Internal**, your ASE name is not used in hello domain for hello ASE.</span></span> <span data-ttu-id="69f70-170">Hello 도메인을 명시적으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-170">You specify hello domain explicitly.</span></span> <span data-ttu-id="69f70-171">도메인 이름은 경우 *contoso.corp.net* ASE 라는 한다는 점에서 응용 프로그램을 만들면 *timereporting*, 이러한 앱은 timereporting.contoso.corp.net URL hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-171">If your domain is *contoso.corp.net* and you create an app in that ASE named *timereporting*, hello URL for that app is timereporting.contoso.corp.net.</span></span>


## <a name="create-an-app-in-an-ilb-ase"></a><span data-ttu-id="69f70-172">ILB ASE에 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="69f70-172">Create an app in an ILB ASE</span></span> ##

<span data-ttu-id="69f70-173">Hello에 ILB ASE에 앱을 만드는 응용 프로그램 ASE에 정상적으로 만들 때 동일한 방법으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-173">You create an app in an ILB ASE in hello same way that you create an app in an ASE normally.</span></span>

1. <span data-ttu-id="69f70-174">Hello Azure 포털에서에서 선택 **새로** > **웹 + 모바일** > **웹** 또는 **모바일** 또는  **API 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-174">In hello Azure portal, select **New** > **Web + Mobile** > **Web** or **Mobile** or **API App**.</span></span>

2. <span data-ttu-id="69f70-175">Hello hello 앱 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-175">Enter hello name of hello app.</span></span>

3. <span data-ttu-id="69f70-176">Hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-176">Select hello subscription.</span></span>

4. <span data-ttu-id="69f70-177">리소스 그룹을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-177">Select or create a resource group.</span></span>

5. <span data-ttu-id="69f70-178">App Service 계획을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-178">Select or create an App Service plan.</span></span> <span data-ttu-id="69f70-179">Toocreate 새 앱 서비스 계획 hello 위치로 프로그램 ASE를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-179">If you want toocreate a new App Service plan, select your ASE as hello location.</span></span> <span data-ttu-id="69f70-180">생성 하 여 앱 서비스 계획 toobe 저장할 hello 작업자 풀을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-180">Select hello worker pool where you want your App Service plan toobe created.</span></span> <span data-ttu-id="69f70-181">Hello 앱 서비스 계획을 만들 때 hello 위치와 hello 작업자 풀 프로그램 ASE를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-181">When you create hello App Service plan, select your ASE as hello location and hello worker pool.</span></span> <span data-ttu-id="69f70-182">Hello 응용 프로그램의 hello 이름을 지정 하면 응용 프로그램 이름 아래에 hello 도메인 프로그램 ASE에 대 한 hello 도메인으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-182">When you specify hello name of hello app, hello domain under your app name is replaced by hello domain for your ASE.</span></span>

6. <span data-ttu-id="69f70-183">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-183">Select **Create**.</span></span> <span data-ttu-id="69f70-184">대시보드 hello 앱 tooappear 하려는 경우 선택 된 **Pin toodashboard** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-184">If you want hello app tooappear on your dashboard, select the **Pin toodashboard** check box.</span></span>

    ![App Service 계획 생성][2]

    <span data-ttu-id="69f70-186">아래 **응용 프로그램 이름**, hello 도메인 이름은 프로그램 ASE의 업데이트 된 tooreflect hello 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-186">Under **App name**, hello domain name is updated tooreflect hello domain of your ASE.</span></span>

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="69f70-187">ILB ASE 생성 후 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="69f70-187">Post-ILB ASE creation validation</span></span> ##

<span data-ttu-id="69f70-188">ILB ASE 약간 다른 경우 보다 hello 비-ILB ASE</span><span class="sxs-lookup"><span data-stu-id="69f70-188">An ILB ASE is slightly different than hello non-ILB ASE.</span></span> <span data-ttu-id="69f70-189">이미 설명한 것 처럼 필요한 toomanage 사용자 고유의 DNS 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-189">As already noted, you need toomanage your own DNS.</span></span> <span data-ttu-id="69f70-190">또한 있습니다 tooprovide HTTPS 연결에 대 한 고유한 인증서.</span><span class="sxs-lookup"><span data-stu-id="69f70-190">You also have tooprovide your own certificate for HTTPS connections.</span></span>

<span data-ttu-id="69f70-191">프로그램 ASE를 만든 후 hello 도메인 이름에 지정 된 hello 도메인을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-191">After you create your ASE, hello domain name shows hello domain you specified.</span></span> <span data-ttu-id="69f70-192">**ILB 인증서**라는 **설정** 메뉴에서 새 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-192">A new item appears in the **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="69f70-193">hello ASE hello ILB ASE 도메인을 지정 하지 않으면 인증서로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-193">hello ASE is created with a certificate that doesn't specify hello ILB ASE domain.</span></span> <span data-ttu-id="69f70-194">해당 인증서로 hello ASE를 사용 하는 경우 브라우저 올바르지 않음을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-194">If you use hello ASE with that certificate, your browser tells you that it's invalid.</span></span> <span data-ttu-id="69f70-195">이 인증서 하면 보다 쉽게 tootest HTTPS 하지만 tooupload 동률된 tooyour ILB ASE 도메인인 사용자 고유의 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-195">This certificate makes it easier tootest HTTPS, but you need tooupload your own certificate that's tied tooyour ILB ASE domain.</span></span> <span data-ttu-id="69f70-196">인증서가 자체 서명되었는지 인증 기관에서 얻었는지에 관계없이 이 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-196">This step is necessary regardless of whether your certificate is self-signed or acquired from a certificate authority.</span></span>

![ILB ASE 도메인 이름][3]

<span data-ttu-id="69f70-198">ILB ASE에는 유효한 SSL 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-198">Your ILB ASE needs a valid SSL certificate.</span></span> <span data-ttu-id="69f70-199">내부 인증 기관을 사용하거나, 외부 발급자로부터 인증서를 구입하거나, 자체 서명된 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-199">Use internal certificate authorities, purchase a certificate from an external issuer, or use a self-signed certificate.</span></span> <span data-ttu-id="69f70-200">Hello SSL 인증서의 hello 소스에 관계 없이 hello 다음 인증서 특성 필요 toobe 올바르게 구성.</span><span class="sxs-lookup"><span data-stu-id="69f70-200">Regardless of hello source of hello SSL certificate, hello following certificate attributes need toobe configured properly:</span></span>

* <span data-ttu-id="69f70-201">**제목**:이 속성은 루트 도메인 여기 too*.your 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-201">**Subject**: This attribute must be set too*.your-root-domain-here.</span></span>
* <span data-ttu-id="69f70-202">**주체 대체 이름**: 이 특성에는 **.your-root-domain-here* 및 **.scm.your-root-domain-here* 둘 다 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-202">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here* and **.scm.your-root-domain-here*.</span></span> <span data-ttu-id="69f70-203">Hello 폼의 주소를 사용 하는 SSL 연결 toohello 각 앱과 연결 된 SCM/Kudu 사이트 *your-app-name.scm.your-root-domain-here*합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-203">SSL connections toohello SCM/Kudu site associated with each app use an address of hello form *your-app-name.scm.your-root-domain-here*.</span></span>

<span data-ttu-id="69f70-204">.Pfx 파일로 hello SSL 인증서를 convert/저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-204">Convert/save hello SSL certificate as a .pfx file.</span></span> <span data-ttu-id="69f70-205">hello.pfx 파일 모든 중간 포함 하 고 루트 인증서 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-205">hello .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="69f70-206">암호로 인증서를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-206">Secure it with a password.</span></span>

<span data-ttu-id="69f70-207">Toocreate 자체 서명 된 인증서를 사용 하도록 하려는 경우 여기 hello PowerShell 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-207">If you want toocreate a self-signed certificate, you can use hello PowerShell commands here.</span></span> <span data-ttu-id="69f70-208">대신 ILB ASE 도메인 이름을 있는지 toouse 수 *internal.contoso.com*:</span><span class="sxs-lookup"><span data-stu-id="69f70-208">Be sure toouse your ILB ASE domain name instead of *internal.contoso.com*:</span></span> 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

<span data-ttu-id="69f70-209">hello 인증서 브라우저의 신뢰 체인에 있는 인증 기관에서 만들어지지 않았으면 다음 PowerShell 명령을 생성 하는 hello 인증서 브라우저에서 플래그가 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-209">hello certificate that these PowerShell commands generate is flagged by browsers because hello certificate wasn't created by a certificate authority that's in your browser's chain of trust.</span></span> <span data-ttu-id="69f70-210">tooget 브라우저에서 신뢰 하는 인증서를 브라우저의 신뢰 체인의 상용 인증 기관에서 것을 확보 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-210">tooget a certificate that your browser trusts, procure it from a commercial certificate authority in your browser's chain of trust.</span></span> 

![ILB 인증서 설정][4]

<span data-ttu-id="69f70-212">tooupload 사용자 고유의 인증서 및 액세스 테스트:</span><span class="sxs-lookup"><span data-stu-id="69f70-212">tooupload your own certificates and test access:</span></span>

1. <span data-ttu-id="69f70-213">Hello ASE를 만든 후 toohello ASE UI를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-213">After hello ASE is created, go toohello ASE UI.</span></span> <span data-ttu-id="69f70-214">**ASE** > **설정** > **ILB 인증서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-214">Select **ASE** > **Settings** > **ILB Certificate**.</span></span>

2. <span data-ttu-id="69f70-215">tooset hello ILB 인증서 hello 인증서.pfx 파일을 선택 하 고 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-215">tooset hello ILB certificate, select hello certificate .pfx file and enter hello password.</span></span> <span data-ttu-id="69f70-216">이 단계에서는 일부 시간 tooprocess 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-216">This step takes some time tooprocess.</span></span> <span data-ttu-id="69f70-217">업로드 작업이 진행 중이라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-217">A message appears stating that an upload operation is in progress.</span></span>

3. <span data-ttu-id="69f70-218">프로그램 ASE를 hello ILB 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-218">Get hello ILB address for your ASE.</span></span> <span data-ttu-id="69f70-219">**ASE** > **속성** > **가상 IP 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-219">Select **ASE** > **Properties** > **Virtual IP Address**.</span></span>

4. <span data-ttu-id="69f70-220">Hello ASE 만들어진 후 프로그램 ASE에 웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-220">Create a web app in your ASE after hello ASE is created.</span></span>

5. <span data-ttu-id="69f70-221">VM이 VNet에 없는 경우 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-221">Create a VM if you don't have one in that VNet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="69f70-222">이 VM에 toocreate 마세요 실패 하거나 문제를 일으킬 됩니다 때문에 ASE hello 처럼 동일한 서브넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-222">Don't try toocreate this VM in hello same subnet as hello ASE because it will fail or cause problems.</span></span>
    >
    >

6. <span data-ttu-id="69f70-223">ASE 도메인에 대 한 hello DNS를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-223">Set hello DNS for your ASE domain.</span></span> <span data-ttu-id="69f70-224">DNS에 있는 도메인에서 와일드 카드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-224">You can use a wildcard with your domain in your DNS.</span></span> <span data-ttu-id="69f70-225">toodo 몇 가지 간단한 테스트, 프로그램 VM tooset hello 웹 응용 프로그램 이름 toohello VIP IP 주소에서 hello 호스트 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-225">toodo some simple tests, edit hello hosts file on your VM tooset hello web app name toohello VIP IP address:</span></span>

    <span data-ttu-id="69f70-226">a.</span><span class="sxs-lookup"><span data-stu-id="69f70-226">a.</span></span> <span data-ttu-id="69f70-227">프로그램 ASE hello 도메인 이름이 있으면 _. ilbase.com_ 라는 hello 웹 앱을 만들고 _mytestapp_에서 문제가 해결 되 _mytestapp.ilbase.com_합니다. 다음 설정 _mytestapp.ilbase.com_ tooresolve toohello ILB 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-227">If your ASE has hello domain name _.ilbase.com_ and you create hello web app named _mytestapp_, it's addressed at _mytestapp.ilbase.com_. You then set _mytestapp.ilbase.com_ tooresolve toohello ILB address.</span></span> <span data-ttu-id="69f70-228">(_C:\Windows\System32\drivers\etc에 hello 호스트 파일은 windows에서\_.)</span><span class="sxs-lookup"><span data-stu-id="69f70-228">(On Windows, hello hosts file is at _C:\Windows\System32\drivers\etc\_.)</span></span>

    <span data-ttu-id="69f70-229">b.</span><span class="sxs-lookup"><span data-stu-id="69f70-229">b.</span></span> <span data-ttu-id="69f70-230">tootest 웹 배포 게시 또는 액세스 toohello 고급 콘솔에 대 한 레코드를 만듭니다. _mytestapp.scm.ilbase.com_합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-230">tootest web deployment publishing or access toohello advanced console, create a record for _mytestapp.scm.ilbase.com_.</span></span>

7. <span data-ttu-id="69f70-231">해당 VM에서 브라우저를 사용하고 http://mytestapp.ilbase.com으로 이동합니다. (또는 웹 응용 프로그램 이름 도메인은 toowhatever 이동 합니다.)</span><span class="sxs-lookup"><span data-stu-id="69f70-231">Use a browser on that VM and go to http://mytestapp.ilbase.com. (Or go toowhatever your web app name is with your domain.)</span></span>

8. <span data-ttu-id="69f70-232">해당 VM에서 브라우저를 사용하고 https://mytestapp.ilbase.com으로 이동합니다. 자체 서명 된 인증서를 사용 하는 경우 보안 hello 부족을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-232">Use a browser on that VM and go to https://mytestapp.ilbase.com. If you use a self-signed certificate, accept hello lack of security.</span></span>

    <span data-ttu-id="69f70-233">프로그램 ilb hello IP 주소 아래에 있는지 **IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-233">hello IP address for your ILB is listed under **IP addresses**.</span></span> <span data-ttu-id="69f70-234">이 목록에는 다음과 같은 hello 외부 VIP와 인바운드 관리 트래픽에 사용 하는 hello IP 주소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-234">This list also has hello IP addresses used by hello external VIP and for inbound management traffic.</span></span>

    ![ILB IP 주소][5]

### <a name="web-jobs-functions-and-hello-ilb-ase"></a><span data-ttu-id="69f70-236">웹 작업, 함수 및 ILB ASE hello</span><span class="sxs-lookup"><span data-stu-id="69f70-236">Web jobs, Functions and hello ILB ASE</span></span>

<span data-ttu-id="69f70-237">ILB ASE 함수와 웹 작업이 둘 다가 지원 되지만 포털 toowork 사람과 hello에 대 한 네트워크 액세스 toohello SCM 사이트 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-237">Both Functions and web jobs are supported on an ILB ASE but for hello portal toowork with them, you must have network access toohello SCM site.</span></span>  <span data-ttu-id="69f70-238">즉, 또는 중 toohello 가상 네트워크를 연결 하는 호스트의 브라우저 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-238">This means your browser must either be on a host that is either in or connected toohello virtual network.</span></span>  

<span data-ttu-id="69f70-239">ILB ASE에 Azure 함수를 사용할 때 "는 함수를 지금 바로 수 tooretrieve 라는 오류 메시지가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-239">When you use Azure Functions on an ILB ASE, you might get an error message that says "We are not able tooretrieve your functions right now.</span></span> <span data-ttu-id="69f70-240">나중에 다시 시도하십시오."</span><span class="sxs-lookup"><span data-stu-id="69f70-240">Please try again later."</span></span> <span data-ttu-id="69f70-241">이 오류는 hello 함수 UI hello SCM 사이트를 활용 하 여 HTTPS를 통해 hello 루트 인증서 신뢰의 hello 브라우저 체인에 없기 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-241">This error occurs because hello Functions UI leverages hello SCM site over HTTPS and hello root certificate is not in hello browser chain of trust.</span></span> <span data-ttu-id="69f70-242">웹 작업에도 비슷한 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-242">Web jobs has a similar problem.</span></span> <span data-ttu-id="69f70-243">tooavoid이이 문제를 hello 다음 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-243">tooavoid this problem you can do one of hello following:</span></span>

- <span data-ttu-id="69f70-244">Hello 인증서 tooyour 신뢰할 수 있는 인증서 저장소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-244">Add hello certificate tooyour trusted certificate store.</span></span> <span data-ttu-id="69f70-245">그러면 Edge 및 Internet Explorer가 차단 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-245">This unblocks Edge and Internet Explorer.</span></span>
- <span data-ttu-id="69f70-246">Chrome을 사용 하 여 및 toohello SCM 사이트를 먼저 이동, hello 신뢰할 수 없는 인증서를 수락 하 고 toohello 포털 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-246">Use Chrome and go toohello SCM site first, accept hello untrusted certificate and then go toohello portal.</span></span>
- <span data-ttu-id="69f70-247">브라우저의 신뢰 체인에 있는 상용 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-247">Use a commercial certificate that is in your browser chain of trust.</span></span>  <span data-ttu-id="69f70-248">Hello 최상의 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-248">This is hello best option.</span></span>  

## <a name="dns-configuration"></a><span data-ttu-id="69f70-249">DNS 구성</span><span class="sxs-lookup"><span data-stu-id="69f70-249">DNS configuration</span></span> ##

<span data-ttu-id="69f70-250">외부 VIP를 사용 하면 Azure hello DNS을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-250">When you use an External VIP, hello DNS is managed by Azure.</span></span> <span data-ttu-id="69f70-251">프로그램 ASE에서 만든 모든 앱은 자동으로 tooAzure DNS은 추가 공용 DNS 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-251">Any app created in your ASE is automatically added tooAzure DNS, which is a public DNS.</span></span> <span data-ttu-id="69f70-252">ILB ASE에서 자체 DNS를 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-252">In an ILB ASE, you must manage your own DNS.</span></span> <span data-ttu-id="69f70-253">와 같은 지정된 된 도메인에 대 한 _contoso.net_, 해당 포인트 tooyour ILB 주소를 DNS에 DNS A 레코드 toocreate 필요:</span><span class="sxs-lookup"><span data-stu-id="69f70-253">For a given domain such as _contoso.net_, you need toocreate DNS A records in your DNS that point tooyour ILB address for:</span></span>

- <span data-ttu-id="69f70-254">*.contoso.net</span><span class="sxs-lookup"><span data-stu-id="69f70-254">*.contoso.net</span></span>
- <span data-ttu-id="69f70-255">*.scm.contoso.net</span><span class="sxs-lookup"><span data-stu-id="69f70-255">*.scm.contoso.net</span></span>

<span data-ttu-id="69f70-256">ILB ASE 도메인이이 ASE 밖의 여러 작업을 위한 사용 하는 경우 응용 프로그램 이름으로 DNS toomanage를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-256">If your ILB ASE domain is used for multiple things outside this ASE, you might need toomanage DNS on a per-app-name basis.</span></span> <span data-ttu-id="69f70-257">이 메서드는 것은 어려울 해야 하기 때문에 tooadd 각 새로운 앱 이름에 DNS를 만들 경우.</span><span class="sxs-lookup"><span data-stu-id="69f70-257">This method is challenging because you need tooadd each new app name into your DNS when you create it.</span></span> <span data-ttu-id="69f70-258">이러한 이유로 전용 도메인을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-258">For this reason, we recommend that you use a dedicated domain.</span></span>

## <a name="publish-with-an-ilb-ase"></a><span data-ttu-id="69f70-259">ILB ASE로 게시</span><span class="sxs-lookup"><span data-stu-id="69f70-259">Publish with an ILB ASE</span></span> ##

<span data-ttu-id="69f70-260">만든 모든 앱에는 두 개의 끝점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-260">For every app that's created, there are two endpoints.</span></span> <span data-ttu-id="69f70-261">ILB ASE에는 *&lt;앱 이름>.&lt;ILB ASE 도메인>*과 *&lt;앱 이름>.scm.&lt; ILB ASE 도메인>*이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-261">In an ILB ASE, you have *&lt;app name>.&lt;ILB ASE Domain>* and *&lt;app name>.scm.&lt;ILB ASE Domain>*.</span></span> 

<span data-ttu-id="69f70-262">hello SCM 사이트 이름이 사용 toohello Kudu 콘솔 hello **고급 포털**내에서 Azure 포털 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-262">hello SCM site name takes you toohello Kudu console, called hello **Advanced portal**, within hello Azure portal.</span></span> <span data-ttu-id="69f70-263">hello Kudu 콘솔을 사용 하 여 hello 디스크를 탐색, 콘솔과 더 많은 사용 하 여 환경 변수를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-263">hello Kudu console lets you view environment variables, explore hello disk, use a console, and much more.</span></span> <span data-ttu-id="69f70-264">자세한 내용은 [Azure App Service의 Kudu 콘솔][Kudu]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69f70-264">For more information, see [Kudu console for Azure App Service][Kudu].</span></span> 

<span data-ttu-id="69f70-265">Hello 다중 테 넌 트 응용 프로그램 서비스 및 외부 ASE single sign on hello Azure 포털 및 hello Kudu 콘솔 간의 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-265">In hello multitenant App Service and in an External ASE, there's single sign-on between hello Azure portal and hello Kudu console.</span></span> <span data-ttu-id="69f70-266">그러나 ILB ASE hello에 대 한 해야 toouse 프로그램 게시 자격 증명 toosign hello Kudu 콘솔에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-266">For hello ILB ASE, however, you need toouse your publishing credentials toosign into hello Kudu console.</span></span>

<span data-ttu-id="69f70-267">인터넷 기반 CI 시스템, GitHub 및 Visual Studio Team Services와 같은 hello 게시 끝점을 인터넷에 액세스할 수 있는 되어 ILB ASE를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-267">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because hello publishing endpoint isn't internet accessible.</span></span> <span data-ttu-id="69f70-268">대신, Dropbox 등의 끌어오기 모델을 사용 하는 CI 시스템 toouse를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-268">Instead, you need toouse a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="69f70-269">ILB ASE에 앱에 대 한 끝점 게시 hello hello 도메인 ILB ASE를 사용 하 여 만든 해당 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-269">hello publishing endpoints for apps in an ILB ASE use hello domain that hello ILB ASE was created with.</span></span> <span data-ttu-id="69f70-270">이 도메인 hello 응용 프로그램의 포털 블레이드 및 hello 응용 프로그램의 게시 프로필에 표시 (**개요** > **Essentials** 그리고 **속성**).</span><span class="sxs-lookup"><span data-stu-id="69f70-270">This domain appears in hello app's publishing profile and in hello app's portal blade (**Overview** > **Essentials** and also **Properties**).</span></span> <span data-ttu-id="69f70-271">ILB ASE hello 하위 도메인으로 설정한 경우 *contoso.net* 및 앱 *mytest*를 사용 하 여 *mytest.contoso.net* FTP에 대 한 및 *mytest.scm.contoso.net*  웹 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-271">If you have an ILB ASE with hello subdomain *contoso.net* and an app named *mytest*, use *mytest.contoso.net* for FTP and *mytest.scm.contoso.net* for web deployment.</span></span>

## <a name="couple-an-ilb-ase-with-a-waf-device"></a><span data-ttu-id="69f70-272">WAF 장치로 ILB ASE 연결</span><span class="sxs-lookup"><span data-stu-id="69f70-272">Couple an ILB ASE with a WAF device</span></span> ##

<span data-ttu-id="69f70-273">Azure 앱 서비스는 hello 시스템을 보호 하는 많은 보안 조치를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-273">Azure App Service provides many security measures that protect hello system.</span></span> <span data-ttu-id="69f70-274">또한 응용 프로그램 해킹 된 여부 toodetermine를 지원할 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-274">They also help toodetermine whether an app was hacked.</span></span> <span data-ttu-id="69f70-275">웹 응용 프로그램에 대 한 최상의 보호 hello toocouple 호스팅 같은 플랫폼 Azure 앱 서비스 웹 응용 프로그램 방화벽 (WAF)입니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-275">hello best protection for a web application is toocouple a hosting platform, such as Azure App Service, with a web application firewall (WAF).</span></span> <span data-ttu-id="69f70-276">ILB ASE hello 네트워크 격리 된 응용 프로그램 끝점을 사용 하므로는 이러한 사용에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-276">Because hello ILB ASE has a network-isolated application endpoint, it's appropriate for such a use.</span></span>

<span data-ttu-id="69f70-277">toolearn tooconfigure WAF 장치와 프로그램 ILB ASE 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 [앱 서비스 환경으로 웹 응용 프로그램 방화벽을 구성][ASEWAF]합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-277">toolearn more about how tooconfigure your ILB ASE with a WAF device, see [Configure a web application firewall with your App Service environment][ASEWAF].</span></span> <span data-ttu-id="69f70-278">이 문서에서는 어떻게 toouse 프로그램 ASE와 Barracuda 가상 어플라이언스 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-278">This article shows how toouse a Barracuda virtual appliance with your ASE.</span></span> <span data-ttu-id="69f70-279">또 다른 옵션은 Azure 응용 프로그램 게이트웨이 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-279">Another option is toouse Azure Application Gateway.</span></span> <span data-ttu-id="69f70-280">응용 프로그램 게이트웨이 hello OWASP 코어 규칙 toosecure 뒤 배치 모든 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-280">Application Gateway uses hello OWASP core rules toosecure any applications placed behind it.</span></span> <span data-ttu-id="69f70-281">응용 프로그램 게이트웨이에 대 한 자세한 내용은 참조 [소개 toohello Azure 웹 응용 프로그램 방화벽][AppGW]합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-281">For more information about Application Gateway, see [Introduction toohello Azure web application firewall][AppGW].</span></span>

## <a name="get-started"></a><span data-ttu-id="69f70-282">시작</span><span class="sxs-lookup"><span data-stu-id="69f70-282">Get started</span></span> ##

<span data-ttu-id="69f70-283">사용할 수 있는 모든 문서 및 방법 tooinstructions ASEs에 대 한는 [앱 서비스 환경에 대 한 추가 정보][ASEReadme]합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-283">All articles and how-tooinstructions for ASEs are available in the [README for App Service environments][ASEReadme].</span></span>

* <span data-ttu-id="69f70-284">ASEs, 시작 tooget 참조 [소개 tooApp 서비스 환경][Intro]합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-284">tooget started with ASEs, see [Introduction tooApp Service environments][Intro].</span></span>
* <span data-ttu-id="69f70-285">Azure 앱 서비스 플랫폼 hello에 대 한 자세한 내용은 참조 [Azure 앱 서비스](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/)합니다.</span><span class="sxs-lookup"><span data-stu-id="69f70-285">For more information about hello Azure App Service platform, see [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span></span>
 
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
