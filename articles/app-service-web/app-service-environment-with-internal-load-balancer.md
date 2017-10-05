---
title: "App Service Environment에서 내부 부하 분산 장치 생성 및 사용 | Microsoft Docs"
description: "ILB를 사용하여 ASE 만들기 및 사용"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: ad9a1e00-d5e5-413e-be47-e21e5b285dbf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 9e5a40f18eb9eaf60579af21afc6f05c2d87f4c1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="using-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="7ed5b-103">앱 서비스 환경에서 내부 부하 분산 장치 사용</span><span class="sxs-lookup"><span data-stu-id="7ed5b-103">Using an Internal Load Balancer with an App Service Environment</span></span>

> [!NOTE] 
> <span data-ttu-id="7ed5b-104">이 문서는 ASE(App Service Environment) v1에 관한 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-104">This article is about the App Service Environment v1.</span></span> <span data-ttu-id="7ed5b-105">사용하기가 더 쉽고 더 강력한 인프라에서 실행되는 최신 버전의 App Service Environment가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-105">There is a newer version of the App Service Environment that is easier to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="7ed5b-106">새 버전에 대한 자세한 내용은 [App Service Environment 소개](../app-service/app-service-environment/intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-106">To learn more about the new version start with the [Introduction to the App Service Environment](../app-service/app-service-environment/intro.md).</span></span>
>

<span data-ttu-id="7ed5b-107">ASE(App Service Environment) 기능은 다중 테넌트 증명(stamp)에서 사용할 수 없는 향상된 구성 기능을 제공하는 Azure App Service의 프리미엄 서비스 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-107">The App Service Environment (ASE) feature is a Premium service option of Azure App Service that delivers an enhanced configuration capability that is not available in the multi-tenant stamps.</span></span> <span data-ttu-id="7ed5b-108">ASE 기능은 기본적으로 Azure 가상 네트워크(VNet)에 Azure 앱 서비스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-108">The ASE feature essentially deploys the Azure App Service in your Azure Virtual Network(VNet).</span></span> <span data-ttu-id="7ed5b-109">App Service 환경에서 제공되는 기능에 대한 자세한 내용은 [App Service 환경 정의][WhatisASE] 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-109">To gain a greater understanding of the capabilities offered by App Service Environments read the [What is an App Service Environment][WhatisASE] documentation.</span></span> <span data-ttu-id="7ed5b-110">VNet에서 작업할 때의 이점을 잘 모르는 경우 [Azure Virtual Network FAQ][virtualnetwork]를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-110">If you don't know the benefits of operating in a VNet read the [Azure Virtual Network FAQ][virtualnetwork].</span></span> 

## <a name="overview"></a><span data-ttu-id="7ed5b-111">개요</span><span class="sxs-lookup"><span data-stu-id="7ed5b-111">Overview</span></span>
<span data-ttu-id="7ed5b-112">ASE는 VNet의 인터넷 액세스 가능 끝점 또는 IP 주소를 사용하여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-112">An ASE can be deployed with an internet accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="7ed5b-113">IP 주소를 VNet 주소로 설정하기 위해서는 ILB(내부 부하 분산 장치)를 사용하여 ASE를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-113">In order to set the IP address to a VNet address you need to deploy your ASE with an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="7ed5b-114">ASE가 ILB로 구성된 경우 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-114">When your ASE is configured with an ILB you provide:</span></span>

* <span data-ttu-id="7ed5b-115">고유한 도메인 또는 하위 도메인.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-115">your own domain or subdomain.</span></span> <span data-ttu-id="7ed5b-116">작업을 용이하게 하기 위해 이 문서에서는 하위 도메인을 가정하지만, 두 가지 모두 구성 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-116">To make it easy, this document assumes subdomain but you can configure it either way.</span></span> 
* <span data-ttu-id="7ed5b-117">HTTPS에 사용되는 인증서</span><span class="sxs-lookup"><span data-stu-id="7ed5b-117">the certificate used for HTTPS</span></span>
* <span data-ttu-id="7ed5b-118">하위 도메인에 대한 DNS 관리</span><span class="sxs-lookup"><span data-stu-id="7ed5b-118">DNS management for your subdomain.</span></span> 

<span data-ttu-id="7ed5b-119">결과적으로 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-119">In return, you can do things such as:</span></span>

* <span data-ttu-id="7ed5b-120">사이트 간 또는 Express 경로 VPN을 통해 액세스하는 클라우드에서 인트라넷 응용 프로그램(예: LOB(기간 업무) 응용 프로그램)을 안전하게 호스트</span><span class="sxs-lookup"><span data-stu-id="7ed5b-120">host intranet applications, like line of business applications, securely in the cloud which you access through a Site to Site or ExpressRoute VPN</span></span>
* <span data-ttu-id="7ed5b-121">공용 DNS 서버에 나열되지 않은 클라우드에 앱 호스트</span><span class="sxs-lookup"><span data-stu-id="7ed5b-121">host apps in the cloud that are not listed in public DNS servers</span></span>
* <span data-ttu-id="7ed5b-122">프런트 엔드 앱이 안전하게 통합될 수 있는 인터넷 격리 백 엔드 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="7ed5b-122">create internet isolated backend apps which your front end apps can securely integrate with</span></span>

#### <a name="disabled-functionality"></a><span data-ttu-id="7ed5b-123">사용되지 않도록 설정된 기능</span><span class="sxs-lookup"><span data-stu-id="7ed5b-123">Disabled functionality</span></span>
<span data-ttu-id="7ed5b-124">ILB ASE를 사용하는 경우 수행할 수 없는 작업도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-124">There are some things that you cannot do when using an ILB ASE.</span></span> <span data-ttu-id="7ed5b-125">여기에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-125">Those things include:</span></span>

* <span data-ttu-id="7ed5b-126">IPSSL 사용</span><span class="sxs-lookup"><span data-stu-id="7ed5b-126">using IPSSL</span></span>
* <span data-ttu-id="7ed5b-127">특정 앱에 IP 주소 할당</span><span class="sxs-lookup"><span data-stu-id="7ed5b-127">assigning IP addresses to specific apps</span></span>
* <span data-ttu-id="7ed5b-128">포털을 통해 인증서를 구매하여 앱에 사용</span><span class="sxs-lookup"><span data-stu-id="7ed5b-128">buying and using a certificate with an app through the portal.</span></span> <span data-ttu-id="7ed5b-129">물론 Azure 포털을 통해서가 아니라 인증 기관에서 직접 인증서를 구한 후 앱에 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-129">You can of course still obtain certificates directly with a Certificate Authority and use it with your apps, just not through the Azure portal.</span></span>

## <a name="creating-an-ilb-ase"></a><span data-ttu-id="7ed5b-130">ILB ASE 만들기</span><span class="sxs-lookup"><span data-stu-id="7ed5b-130">Creating an ILB ASE</span></span>
<span data-ttu-id="7ed5b-131">ILB ASE를 만드는 과정은 일반적으로 ASE를 만드는 과정과 크게 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-131">Creating an ILB ASE is not much different from creating an ASE normally.</span></span> <span data-ttu-id="7ed5b-132">ASE를 만드는 방법에 대한 자세한 내용은 [App Service 환경을 만드는 방법][HowtoCreateASE]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-132">For a deeper discussion on creating an ASE read [How to Create an App Service Environment][HowtoCreateASE].</span></span> <span data-ttu-id="7ed5b-133">ILB ASE를 만드는 프로세스를 ASE 생성 중에 VNet을 만드는 경우와 기존 VNet을 선택하는 경우에서 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-133">The process to create an ILB ASE is the same between creating a VNet during ASE creation or selecting a pre-existing VNet.</span></span> <span data-ttu-id="7ed5b-134">ILB ASE를 만들려면</span><span class="sxs-lookup"><span data-stu-id="7ed5b-134">To create an ILB ASE:</span></span> 

1. <span data-ttu-id="7ed5b-135">Azure Portal에서 **새로 만들기 > 웹 + 모바일 > App Service 환경** 선택</span><span class="sxs-lookup"><span data-stu-id="7ed5b-135">In the Azure portal select **New -> Web + Mobile -> App Service Environment**</span></span>
2. <span data-ttu-id="7ed5b-136">구독 선택</span><span class="sxs-lookup"><span data-stu-id="7ed5b-136">Select your subscription</span></span>
3. <span data-ttu-id="7ed5b-137">리소스 그룹 선택 또는 만들기</span><span class="sxs-lookup"><span data-stu-id="7ed5b-137">Select or create a resource group</span></span>
4. <span data-ttu-id="7ed5b-138">VNet 선택 또는 만들기</span><span class="sxs-lookup"><span data-stu-id="7ed5b-138">Select or create a VNet</span></span>
5. <span data-ttu-id="7ed5b-139">VNet을 선택하는 경우 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="7ed5b-139">Create a subnet if selecting a VNet</span></span>
6. <span data-ttu-id="7ed5b-140">**가상 네트워크/위치 -> VNet 구성**을 선택하고 VIP 유형을 내부로 설정</span><span class="sxs-lookup"><span data-stu-id="7ed5b-140">Select **Virtual Network/Location -> VNet Configuration** and set the VIP Type to Internal</span></span>
7. <span data-ttu-id="7ed5b-141">하위 도메인 이름(이 ASE에서 만든 앱에 사용되는 하위 도메인) 제공</span><span class="sxs-lookup"><span data-stu-id="7ed5b-141">Provide subdomain name (this will be the subdomain used for apps created in this ASE)</span></span>
8. <span data-ttu-id="7ed5b-142">확인 및 만들기를 차례로 선택</span><span class="sxs-lookup"><span data-stu-id="7ed5b-142">Select Ok and then Create</span></span>

![][1]

<span data-ttu-id="7ed5b-143">가상 네트워크 블레이드 내에는 VNet 구성 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-143">Within the Virtual Network blade there is a VNet Configuration option.</span></span> <span data-ttu-id="7ed5b-144">여기서 외부 VIP 또는 내부 VIP 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-144">This lets you select between an External VIP or Internal VIP.</span></span> <span data-ttu-id="7ed5b-145">기본값은 외부입니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-145">The default is External.</span></span> <span data-ttu-id="7ed5b-146">외부로 설정하기로 선택한 경우 ASE는 인터넷 액세스 가능 VIP를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-146">If you have it set to External then your ASE will use an internet accessible VIP.</span></span> <span data-ttu-id="7ed5b-147">내부를 선택하는 경우 ASE가 VNet 내의 IP 주소에 있는 ILB로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-147">If you select Internal, your ASE will be configured with an ILB on an IP address within your VNet.</span></span> 

<span data-ttu-id="7ed5b-148">내부를 선택하면 ASE에 더 많은 IP 주소를 추가하는 기능이 제거되고, 대신 ASE의 하위 도메인을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-148">After selecting Internal, the ability to add more IP addresses to your ASE is removed and instead you need to provide the subdomain of the ASE.</span></span> <span data-ttu-id="7ed5b-149">외부 VIP가 있는 ASE에서 ASE의 이름은 해당 ASE에서 만든 앱에 대한 하위 도메인에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-149">In an ASE with an External VIP the name of the ASE is used in the subdomain for apps created in that ASE.</span></span> <span data-ttu-id="7ed5b-150">ASE가 ***contosotest***로 지칭되고 해당 ASE의 앱이 ***mytest***로 지칭되면 하위 도메인 형식은 ***contosotest.p.azurewebsites.net***이고 해당 앱의 URL은 ***mytest.contosotest.p.azurewebsites.net***이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-150">If your ASE was called ***contosotest*** and your app in that ASE was called ***mytest*** then the subdomain would be of the format ***contosotest.p.azurewebsites.net*** and the URL for that app would be ***mytest.contosotest.p.azurewebsites.net***.</span></span> <span data-ttu-id="7ed5b-151">VIP 유형을 내부로 설정한 경우 ASE 이름은 해당 ASE의 하위 도메인에서 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-151">If you set the VIP Type to Internal, your ASE name is not used in the subdomain for the ASE.</span></span> <span data-ttu-id="7ed5b-152">하위 도메인을 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-152">You specify the subdomain explicitly.</span></span> <span data-ttu-id="7ed5b-153">하위 도메인이 ***contoso.corp.net***이고 해당 ASE에서 ***timereporting***이라는 앱을 만들었으면 해당 앱의 URL은 ***timereporting.contoso.corp.net***이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-153">If your subdomain was ***contoso.corp.net*** and you made an app in that ASE named ***timereporting*** then the URL for that app would be ***timereporting.contoso.corp.net***.</span></span>

## <a name="apps-in-an-ilb-ase"></a><span data-ttu-id="7ed5b-154">ILB ASE의 앱</span><span class="sxs-lookup"><span data-stu-id="7ed5b-154">Apps in an ILB ASE</span></span>
<span data-ttu-id="7ed5b-155">ILB ASE에서 앱을 만드는 과정은 일반적으로 ASE에서 앱을 만드는 과정과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-155">Creating an app in an ILB ASE is the same as creating an app in an ASE normally.</span></span> 

1. <span data-ttu-id="7ed5b-156">Azure Portal에서 **새로 만들기 -> 웹 + 모바일 > 웹**을 선택하거나 **모바일** 또는 **API App**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-156">In the Azure portal select **New -> Web + Mobile -> Web** or **Mobile** or **API App**</span></span>
2. <span data-ttu-id="7ed5b-157">앱 이름 입력</span><span class="sxs-lookup"><span data-stu-id="7ed5b-157">Enter name of app</span></span>
3. <span data-ttu-id="7ed5b-158">구독 선택</span><span class="sxs-lookup"><span data-stu-id="7ed5b-158">Select subscription</span></span>
4. <span data-ttu-id="7ed5b-159">리소스 그룹 선택 또는 만들기</span><span class="sxs-lookup"><span data-stu-id="7ed5b-159">Select or create resource group</span></span>
5. <span data-ttu-id="7ed5b-160">ASP(앱 서비스 계획) 선택 또는 만들기.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-160">Select or create App Service Plan(ASP).</span></span> <span data-ttu-id="7ed5b-161">새 ASE를 만드는 경우 위치로 ASE를 선택하고 ASP를 생성할 작업자 풀을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-161">If creating a new ASP then select your ASE as the location and select the worker pool you want your ASP to be created in.</span></span> <span data-ttu-id="7ed5b-162">ASP를 만들 때 위치 및 작업자 풀로 ASE를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-162">When you create the ASP you select your ASE as the location and the worker pool.</span></span> <span data-ttu-id="7ed5b-163">앱의 이름을 지정하면 앱 이름 아래의 하위 도메인이 ASE에 대한 하위 도메인으로 바뀌는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-163">When you specify the name of the app you will see that the subdomain under your app name is replaced by the subdomain for your ASE.</span></span> 
6. <span data-ttu-id="7ed5b-164">만들기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-164">Select Create.</span></span> <span data-ttu-id="7ed5b-165">앱을 대시보드에 표시하려면 **대시보드에 고정** 확인란을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-165">You should select the **Pin to dashboard** checkbox if you want the app to show up on your dashboard.</span></span> 

![][2]

<span data-ttu-id="7ed5b-166">앱 이름 아래의 하위 도메인 이름이 ASE의 하위 도메인을 반영하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-166">Under the app name the subdomain name gets updated to reflect the subdomain of your ASE.</span></span> 

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="7ed5b-167">ILB ASE 만들기 유효성 검사 게시</span><span class="sxs-lookup"><span data-stu-id="7ed5b-167">Post ILB ASE creation validation</span></span>
<span data-ttu-id="7ed5b-168">ILB ASE는 비 ILB ASE와는 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-168">An ILB ASE is slightly different than the non-ILB ASE.</span></span> <span data-ttu-id="7ed5b-169">앞서 명시한 것처럼 사용자 고유의 DNS를 관리해야 하므로 HTTPS 연결에 대 한 사용자 고유의 인증서를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-169">As already noted you need to manage your own DNS and you also have to provide your own certificate for HTTPS connections.</span></span> 

<span data-ttu-id="7ed5b-170">ASE를 만든 후에는 해당 하위 도메인이 사용자가 지정한 하위 도메인을 표시하며, **설정** 메뉴에는 **ILB 인증서**라는 새 항목이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-170">After you create your ASE you will notice that the subdomain shows the subdomain you specified and there is a new item in the **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="7ed5b-171">ASE는 HTTPS를 쉽게 테스트하는 자체 서명된 인증서로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-171">The ASE is created with a self-signed certificate which makes it easier to test HTTPS.</span></span> <span data-ttu-id="7ed5b-172">포털에서는 HTTPS에 고유한 인증서를 제공해야 한다고 지시할 수 있지만 이로 인해 하위 도메인으로 사용하는 인증서를 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-172">The portal will tell you that you need to provide your own certificate for HTTPS but this is to drive you to have a certificate that goes with your subdomain.</span></span> 

![][3]

<span data-ttu-id="7ed5b-173">인증서 만드는 방법을 잘 모르고 시험적으로 수행해보려는 경우 IIS MMC 콘솔 응용 프로그램을 사용하여 자체 서명된 인증서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-173">If you are simply trying things out and don't know how to create a certificate, you can use the IIS MMC console application to create a self signed certificate.</span></span> <span data-ttu-id="7ed5b-174">이 인증서가 생성되면 .pfx 파일로 내보낸 다음 ILB 인증서 UI에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-174">Once it is created you can export it as a .pfx file and then upload it in the ILB Certificate UI.</span></span> <span data-ttu-id="7ed5b-175">자체 서명된 인증서로 보안이 유지된 사이트에 액세스하면 인증서 유효성을 검사할 수 없으므로 액세스하려는 사이트가 안전하지 않다는 경고가 브라우저에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-175">When you access a site secured with a self-signed certificate, your browser will give you a warning that the site you are accessing is not secure due to the inability to validate the certificate.</span></span> <span data-ttu-id="7ed5b-176">해당 경고가 발생하지 않도록 하려면 하위 도메인과 일치하고, 브라우저에서 인식할 수 있는 신뢰 체인을 포함하는 적절히 서명된 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-176">If you want to avoid that warning you need a properly signed certificate that matches your subdomain and has a chain of trust that is recognized by your browser.</span></span>

![][6]

<span data-ttu-id="7ed5b-177">고유한 인증서를 사용하여 흐름을 시도하고 ASE에 대한 HTTP 및 HTTPS 액세스를 테스트하려면:</span><span class="sxs-lookup"><span data-stu-id="7ed5b-177">If you want to try the flow with your own certificates and test both HTTP and HTTPS access to your ASE:</span></span>

1. <span data-ttu-id="7ed5b-178">ASE를 만든 후에 ASE UI, **ASE -> 설정 -> ILB 인증서**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-178">Go to ASE UI after ASE is created **ASE -> Settings -> ILB Certificates**</span></span>
2. <span data-ttu-id="7ed5b-179">인증서 pfx 파일을 선택하여 ILB 인증서를 설정하고 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-179">Set ILB certificate by selecting certificate pfx file and provide password.</span></span> <span data-ttu-id="7ed5b-180">이 단계를 처리하는 데 잠시 시간이 소요되며, 크기 조정 작업이 진행 중이라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-180">This step takes a little while to process and the message that a scaling operation is in progress will be shown.</span></span>
3. <span data-ttu-id="7ed5b-181">ASE의 ILB 주소를 가져옵니다(**ASE -> 속성 -> 가상 IP 주소**).</span><span class="sxs-lookup"><span data-stu-id="7ed5b-181">Get the ILB address for your ASE (**ASE -> Properties -> Virtual IP Address**)</span></span>
4. <span data-ttu-id="7ed5b-182">ASE를 만든 후에 ASE에서 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-182">Create a web app in ASE after creation</span></span> 
5. <span data-ttu-id="7ed5b-183">해당 VNET에 없는 경우 VM을 만듭니다(ASE가 있는 동일한 서브넷이 아니거나 연결이 끊긴 경우).</span><span class="sxs-lookup"><span data-stu-id="7ed5b-183">Create a VM if you don't have one in that VNET (Not in the same subnet as the ASE or things break)</span></span>
6. <span data-ttu-id="7ed5b-184">하위 도메인에 대한 DNS를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-184">Set DNS for your subdomain.</span></span> <span data-ttu-id="7ed5b-185">DNS에 하위 도메인과 와일드카드를 사용할 수도 있고, 몇 가지 간단한 테스트를 수행하려는 경우 VM의 호스트 파일을 편집하여 웹앱 이름을 VIP IP 주소로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-185">You can use a wildcard with your subdomain in your DNS or if you want to do some simple tests, edit the hosts file on your VM to set web app name to VIP IP address.</span></span> <span data-ttu-id="7ed5b-186">ASE에 .ilbase.com이라는 하위 도메인이 있고 웹앱 mytestapp을 만들었으면 mytestapp.ilbase.com에서 주소가 지정되고 해당 사항이 호스트 파일에 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-186">If your ASE had the subdomain name .ilbase.com and you made the web app mytestapp so that it would be addressed at mytestapp.ilbase.com then set that in your hosts file.</span></span> <span data-ttu-id="7ed5b-187">(Windows에서 호스트 파일은 C:\Windows\System32\drivers\etc\에 있음)</span><span class="sxs-lookup"><span data-stu-id="7ed5b-187">(On Windows the hosts file is at C:\Windows\System32\drivers\etc\ )</span></span>
7. <span data-ttu-id="7ed5b-188">해당 VM의 브라우저를 사용하여 http://mytestapp.ilbase.com (또는 하위 도메인이 포함된 웹앱 이름)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-188">Use a browser on that VM and go to http://mytestapp.ilbase.com (or whatever your web app name is with your subdomain)</span></span>
8. <span data-ttu-id="7ed5b-189">해당 VM에서 브라우저를 사용하여 https://mytestapp.ilbase.com으로 이동합니다. 자체 서명된 인증서를 사용하는 경우 보안이 부족함에 동의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-189">Use a browser on that VM and go to https://mytestapp.ilbase.com You will have to accept the lack of security if using a self-signed certificate.</span></span> 

<span data-ttu-id="7ed5b-190">ILB에 대한 IP 주소는 속성에 가상 IP 주소로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-190">The IP address for your ILB is listed in your Properties as the Virtual IP Address</span></span>

![][4]

## <a name="using-an-ilb-ase"></a><span data-ttu-id="7ed5b-191">ILB ASE 사용</span><span class="sxs-lookup"><span data-stu-id="7ed5b-191">Using an ILB ASE</span></span>
#### <a name="network-security-groups"></a><span data-ttu-id="7ed5b-192">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="7ed5b-192">Network Security Groups</span></span>
<span data-ttu-id="7ed5b-193">ILB ASE에서는 앱에 액세스할 수 없고 인터넷에서 해당 앱도 알 수 없을 때 네트워크 격리를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-193">An ILB ASE enables network isolation for your apps as the apps are not accessible or even known by the internet.</span></span> <span data-ttu-id="7ed5b-194">이러한 기능은 LOB(기간 업무) 응용 프로그램과 같은 인트라넷 사이트를 호스트하는 데 아주 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-194">This is excellent for hosting intranet sites such as line of business applications.</span></span> <span data-ttu-id="7ed5b-195">액세스를 좀 더 제한해야 할 경우, NSG(네트워크 보안 그룹)를 사용하여 네트워크 수준에서 액세스를 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-195">When you need to restrict access even further you can still use Network Security Groups(NSGs) to control access at the network level.</span></span> 

<span data-ttu-id="7ed5b-196">NSG를 사용하여 액세스를 좀 더 제한하려는 경우 ASE의 작동에 필요한 통신이 끊어지지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-196">If you wish to use NSGs to further restrict access then you need to make sure you do not break the communication that the ASE needs in order to operate.</span></span> <span data-ttu-id="7ed5b-197">HTTP/HTTPS 액세스가 ASE에 사용되는 ILB를 통해서만 진행되더라도 ASE에는 VNet 외부의 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-197">Even though the HTTP/HTTPS access is only through the ILB used by the ASE the ASE still depends on resource outside of the VNet.</span></span> <span data-ttu-id="7ed5b-198">여전히 필요한 네트워크 액세스를 확인하려면 [App Service 환경에 대한 인바운드 트래픽 제어][ControlInbound] 및 [ExpressRoute를 사용하는 App Service 환경에 대한 네트워크 구성 세부 정보][ExpressRoute]에 대한 문서에서 해당 정보를 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-198">To see what network access is still required look at the information in the document on [Controlling Inbound Traffic to an App Service Environment][ControlInbound] and the document on [Network Configuration Details for App Service Environments with ExpressRoute][ExpressRoute].</span></span> 

<span data-ttu-id="7ed5b-199">ASE를 구성하려면 Azure에서 ASE 관리를 위해 사용하는 IP 주소를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-199">To configure your NSGs you need to know the IP address that is used by Azure to manage your ASE.</span></span> <span data-ttu-id="7ed5b-200">인터넷 요청도 수행하는 경우 해당 IP 주소는 ASE의 아웃바운드 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-200">That IP address is also the outbound IP address from your ASE if it makes internet requests.</span></span> <span data-ttu-id="7ed5b-201">ASE에 대한 아웃바운드 IP 주소는 ASE 수명 동안 정적 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-201">The outbound IP address for your ASE will remain static for the life of your ASE.</span></span> <span data-ttu-id="7ed5b-202">ASE를 삭제하고 다시 만들면 새 IP 주소를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-202">If you delete and recreate your ASE, you will get a new IP address.</span></span> <span data-ttu-id="7ed5b-203">이 IP 주소를 찾으려면 **설정 -> 속성**으로 이동한 후 **아웃바운드 IP 주소**를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-203">To find this IP address go to **Settings -> Properties** and find the **Outbound IP Address**.</span></span> 

![][5]

#### <a name="general-ilb-ase-management"></a><span data-ttu-id="7ed5b-204">일반 ILB ASE 관리</span><span class="sxs-lookup"><span data-stu-id="7ed5b-204">General ILB ASE management</span></span>
<span data-ttu-id="7ed5b-205">대체적으로 ILB ASE 관리는 일반적인 ASE 관리와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-205">Managing an ILB ASE is largely the same as managing an ASE normally.</span></span> <span data-ttu-id="7ed5b-206">추가 ASP 인스턴스를 호스트하려면 작업자 풀을 확장해야 하고, 증가하는 HTTP/HTTPS 트래픽 양을 처리하려면 프런트 엔드 서버를 확장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-206">You need to scale up your worker pools to host more ASP instances and scale up your Front End servers to handle increased amounts of HTTP/HTTPS traffic.</span></span> <span data-ttu-id="7ed5b-207">ASE의 구성 관리에 대한 일반적인 내용을 보려면 [App Service 환경 구성][ASEConfig] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-207">For general information on managing the configuration of an ASE, read the document on [Configuring an App Service Environment][ASEConfig].</span></span> 

<span data-ttu-id="7ed5b-208">추가 관리 항목은 인증서 관리 및 DNS 관리입니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-208">The additional management items are certificate management and DNS management.</span></span> <span data-ttu-id="7ed5b-209">ILB ASE를 만든 후에 HTTPS에 사용되는 인증서를 구하여 업로드하고 만료되기 전에 교체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-209">You need to obtain and upload the certificate used for HTTPS after ILB ASE creation and replace it before it expires.</span></span> <span data-ttu-id="7ed5b-210">Azure는 기본 도메인을 소유하므로 ASE에 대한 인증서에 외부 VIP를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-210">Because Azure owns the base domain we can provide certificates for ASEs with an External VIP.</span></span> <span data-ttu-id="7ed5b-211">ILB ASE에 사용되는 하위 도메인에는 제한이 없으므로 HTTPS에 대한 자체 인증서를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-211">Since the subdomain used by an ILB ASE can be anything, you need to provide your own certificate for HTTPS.</span></span> 

#### <a name="dns-configuration"></a><span data-ttu-id="7ed5b-212">DNS 구성</span><span class="sxs-lookup"><span data-stu-id="7ed5b-212">DNS Configuration</span></span>
<span data-ttu-id="7ed5b-213">외부 VIP를 사용하는 경우 DNS가 Azure에서 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-213">When using an External VIP the DNS is managed by Azure.</span></span> <span data-ttu-id="7ed5b-214">ASE에서 만든 모든 앱은 공용 DNS에 해당하는 Azure DNS에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-214">Any app created in your ASE is automatically added to Azure DNS which is a public DNS.</span></span> <span data-ttu-id="7ed5b-215">ILB ASE에서 자체 DNS를 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-215">In an ILB ASE you have to manage your own DNS.</span></span> <span data-ttu-id="7ed5b-216">contoso.corp.net과 같은 특정 하위 도메인의 경우 다음에 대해 ILB 주소를 가리키는 DNS A 레코드를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-216">For a given subdomain such as contoso.corp.net you need to create DNS A records that point to your ILB address for:</span></span>

    * 
    <span data-ttu-id="7ed5b-217">*.scm ftp 게시</span><span class="sxs-lookup"><span data-stu-id="7ed5b-217">*.scm ftp publish</span></span> 


## <a name="getting-started"></a><span data-ttu-id="7ed5b-218">시작</span><span class="sxs-lookup"><span data-stu-id="7ed5b-218">Getting started</span></span>
<span data-ttu-id="7ed5b-219">앱 서비스 환경에 대한 모든 문서와 지침은 [응용 프로그램 서비스 환경의 추가 정보](../app-service/app-service-app-service-environments-readme.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-219">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="7ed5b-220">App Service 환경을 시작하려면 [App Service 환경 소개][WhatisASE]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-220">To get started with App Service Environments, see [Introduction to App Service Environments][WhatisASE]</span></span>

<span data-ttu-id="7ed5b-221">Azure App Service 플랫폼에 대한 자세한 내용은 [Azure App Service][AzureAppService]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ed5b-221">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createilbase.png
[2]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createapp.png
[3]: ./media/app-service-environment-with-internal-load-balancer/ilbase-newase.png
[4]: ./media/app-service-environment-with-internal-load-balancer/ilbase-vip.png
[5]: ./media/app-service-environment-with-internal-load-balancer/ilbase-externalvip.png
[6]: ./media/app-service-environment-with-internal-load-balancer/ilbase-ilbcertificate.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[vnetnsgs]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
