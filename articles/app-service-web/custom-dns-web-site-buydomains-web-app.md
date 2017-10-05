---
title: "Azure Web Apps에 대한 사용자 지정 도메인 이름 구입"
description: "Azure App Service에서 웹 앱으로 사용자 지정 도메인 이름을 구입하는 방법에 대해 알아봅니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 3cb22b935624041ab51e64028a1b668fd694f9b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="9730a-103">Azure Web Apps에 대한 사용자 지정 도메인 이름 구입</span><span class="sxs-lookup"><span data-stu-id="9730a-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="9730a-104">App Service 도메인(미리 보기)은 Azure에서 직접 관리되는 최상위 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="9730a-105">이 도메인을 통해 [Azure Web Apps](app-service-web-overview.md)에 대한 사용자 지정 도메인을 쉽게 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-105">They make it easy to manage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="9730a-106">이 자습서에서는 App Service 도메인을 구입하고 DNS 이름을 Azure Web Apps에 할당하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-106">This tutorial shows you how to buy an App Service domain and assign DNS names to Azure Web Apps.</span></span>

<span data-ttu-id="9730a-107">이 문서는 Azure App Service(Web Apps, API Apps, Mobile Apps, Logic Apps)에 관한 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="9730a-108">Azure VM 또는 Azure Storage의 경우 [Azure VM 또는 Azure Storage에 App Service 도메인 할당](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9730a-108">For Azure VM or Azure Storage, see [Assign App Service domain to Azure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="9730a-109">Cloud Services의 경우 [Azure 클라우드 서비스에 대한 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9730a-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9730a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9730a-110">Prerequisites</span></span>

<span data-ttu-id="9730a-111">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-111">To complete this tutorial:</span></span>

* <span data-ttu-id="9730a-112">[App Service 앱을 만들거나](/azure/app-service/) 다른 자습서를 위해 만든 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-the-app"></a><span data-ttu-id="9730a-113">앱 준비</span><span class="sxs-lookup"><span data-stu-id="9730a-113">Prepare the app</span></span>

<span data-ttu-id="9730a-114">Azure Web Apps에서 사용자 지정 도메인을 사용하려면 웹앱의 [App Service 계획](https://azure.microsoft.com/pricing/details/app-service/)이 유료 계층(**공유**, **기본**, **표준** 또는 **프리미엄**)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-114">To use custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="9730a-115">이 단계에서는 웹앱이 지원되는 가격 책정 계층에 있음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-115">In this step, you make sure that the web app is in the supported pricing tier.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="9730a-116">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="9730a-116">Sign in to Azure</span></span>

<span data-ttu-id="9730a-117">[클래식 포털](https://portal.azure.com)을 열고 Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-117">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="9730a-118">Azure Portal에서 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-118">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="9730a-119">왼쪽 메뉴에서 **App Services**를 선택한 다음 앱 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-119">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![Azure 앱에 대한 포털 탐색](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="9730a-121">App Service 앱의 관리 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-121">You see the management page of the App Service app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="9730a-122">가격 책정 계층 확인</span><span class="sxs-lookup"><span data-stu-id="9730a-122">Check the pricing tier</span></span>

<span data-ttu-id="9730a-123">앱 페이지의 왼쪽 탐색 영역에서 **설정** 섹션으로 스크롤하고 **강화(App Service 계획)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-123">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![강화 메뉴](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="9730a-125">앱의 현재 계층은 파란색 테두리로 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-125">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="9730a-126">앱이 **무료** 계층에 속해 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-126">Check to make sure that the app is not in the **Free** tier.</span></span> <span data-ttu-id="9730a-127">사용자 지정 DNS는 **무료** 계층에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-127">Custom DNS is not supported in the **Free** tier.</span></span> 

![가격 책정 계층 확인](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="9730a-129">App Service 계획이 **평가판** 계층이 아닌 경우 **가격 책정 계층 선택** 페이지를 닫고 [도메인 구입](#buy-the-domain)으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-129">If the App Service plan is not **Free**, close the **Choose your pricing tier** page and skip to [Buy the domain](#buy-the-domain).</span></span>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="9730a-130">강화 - App Service 계획</span><span class="sxs-lookup"><span data-stu-id="9730a-130">Scale up the App Service plan</span></span>

<span data-ttu-id="9730a-131">무료가 아닌 계층(**공유**, **기본**, **표준** 또는 **프리미엄**) 중에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-131">Select any of the non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="9730a-132">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-132">Click **Select**.</span></span>

![가격 책정 계층 확인](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="9730a-134">다음 알림이 표시되면 강화 작업이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-134">When you see the following notification, the scale operation is complete.</span></span>

![크기 조정 작업 확인](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-the-domain"></a><span data-ttu-id="9730a-136">도메인 구입</span><span class="sxs-lookup"><span data-stu-id="9730a-136">Buy the domain</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="9730a-137">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="9730a-137">Sign in to Azure</span></span>
<span data-ttu-id="9730a-138">[클래식 포털](https://portal.azure.com/)을 열고 Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-138">Open the [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="9730a-139">도메인 구입 시작</span><span class="sxs-lookup"><span data-stu-id="9730a-139">Launch Buy domains</span></span>
<span data-ttu-id="9730a-140">**Web Apps** 탭에서 웹앱의 이름을 클릭하고 **설정**을 선택한 다음 **사용자 지정 도메인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-140">In the **Web Apps** tab, click the name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="9730a-141">**사용자 지정 도메인** 페이지에서 **도메인 구입**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-141">In the **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-the-domain-purchase"></a><span data-ttu-id="9730a-142">도메인 구매 구성</span><span class="sxs-lookup"><span data-stu-id="9730a-142">Configure the domain purchase</span></span>

<span data-ttu-id="9730a-143">**App Service 도메인** 페이지의 **도메인 검색** 상자에 구입할 도메인 이름을 입력하고 `Enter`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-143">In the **App Service Domain** page, in the **Search for domain** box, type the domain name you want to buy and type `Enter`.</span></span> <span data-ttu-id="9730a-144">사용 가능한 도메인이 텍스트 상자 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-144">The suggested available domains are shown just below the text box.</span></span> <span data-ttu-id="9730a-145">구입하려는 도메인을 하나 이상 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-145">Select one or more domains you want to buy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="9730a-146">**연락처 정보**를 클릭하고 도메인의 연락처 정보 양식을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-146">Click the **Contact Information** and fill out the domain's contact information form.</span></span> <span data-ttu-id="9730a-147">완료한 후 **확인**을 클릭하면 App Service 도메인 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-147">When finished, click **OK** to return to the App Service Domain page.</span></span>
   
<span data-ttu-id="9730a-148">모든 필수 필드를 가능한 한 정확하게 기입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="9730a-149">잘못된 연락처 정보 데이터로 인해 도메인을 구입하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-149">Incorrect data for contact information can result in failure to purchase domains.</span></span> 

<span data-ttu-id="9730a-150">그런 다음 도메인에 대해 원하는 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-150">Next, select the desired options for your domain.</span></span> <span data-ttu-id="9730a-151">설명은 다음 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9730a-151">See the following table for explanations:</span></span>

| <span data-ttu-id="9730a-152">설정</span><span class="sxs-lookup"><span data-stu-id="9730a-152">Setting</span></span> | <span data-ttu-id="9730a-153">제안 값</span><span class="sxs-lookup"><span data-stu-id="9730a-153">Suggested Value</span></span> | <span data-ttu-id="9730a-154">설명</span><span class="sxs-lookup"><span data-stu-id="9730a-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="9730a-155">자동 갱신</span><span class="sxs-lookup"><span data-stu-id="9730a-155">Auto renew</span></span> | <span data-ttu-id="9730a-156">**사용**</span><span class="sxs-lookup"><span data-stu-id="9730a-156">**Enable**</span></span> | <span data-ttu-id="9730a-157">매년 App Service 도메인을 자동으로 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="9730a-158">갱신 시 신용 카드로 동일한 구매 가격이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-158">Your credit card is charged the same purchase price at the time of renewal.</span></span> |
|<span data-ttu-id="9730a-159">개인 정보 보호</span><span class="sxs-lookup"><span data-stu-id="9730a-159">Privacy protection</span></span> | <span data-ttu-id="9730a-160">사용</span><span class="sxs-lookup"><span data-stu-id="9730a-160">Enable</span></span> | <span data-ttu-id="9730a-161">_평가판_ 구매 가격에 포함된 "개인 정보 보호"에 참여합니다(_.co.in_, _.co.uk_ 등과 같이 레지스트리가 개인 정보 보호를 지원하지 않는 최상위 도메인은 제외).</span><span class="sxs-lookup"><span data-stu-id="9730a-161">Opt in to "Privacy protection", which is included in the purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="9730a-162">기본 호스트 이름 할당</span><span class="sxs-lookup"><span data-stu-id="9730a-162">Assign default hostnames</span></span> | <span data-ttu-id="9730a-163">**www** 및 **@**</span><span class="sxs-lookup"><span data-stu-id="9730a-163">**www** and **@**</span></span> | <span data-ttu-id="9730a-164">필요한 경우 원하는 호스트 이름 바인딩을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-164">Select the desired hostname bindings, if desired.</span></span> <span data-ttu-id="9730a-165">도메인 구매 작업이 완료되면 선택한 호스트 이름에서 웹앱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-165">When the domain purchase operation is complete, your web app can be accessed at the selected hostnames.</span></span> <span data-ttu-id="9730a-166">웹앱이 [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) 뒤에 있는 경우 Traffic Manager는 A 레코드를 지원하지 않으므로 루트 도메인을 할당하는 옵션이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-166">If the web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see the option to assign the root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="9730a-167">도메인 구매가 완료된 후 호스트 이름 할당을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-167">You can make changes to the hostname assignments after the domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="9730a-168">조건에 동의하고 구매</span><span class="sxs-lookup"><span data-stu-id="9730a-168">Accept terms and purchase</span></span>

<span data-ttu-id="9730a-169">**약관**을 클릭하여 조건 및 요금을 검토한 후 **구입**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-169">Click **Legal Terms** to review the terms and the charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="9730a-170">App Service 도메인은 도메인을 호스트하는 데 Azure DNS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-170">App Service Domains use Azure DNS to host the domains.</span></span> <span data-ttu-id="9730a-171">도메인 등록 요금 외에도 Azure DNS에 대한 사용 요금이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-171">In addition to the domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="9730a-172">자세한 내용은 [Azure DNS 가격 책정](https://azure.microsoft.com/pricing/details/dns/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9730a-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="9730a-173">**App Service 도메인** 페이지로 돌아가서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-173">Back in the **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="9730a-174">작업이 진행되는 동안 다음과 같은 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-174">While the operation is in progress, you see the following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-the-hostnames"></a><span data-ttu-id="9730a-175">호스트 이름 테스트</span><span class="sxs-lookup"><span data-stu-id="9730a-175">Test the hostnames</span></span>

<span data-ttu-id="9730a-176">웹앱에 기본 호스트 이름을 할당한 경우 선택한 각 호스트 이름에 대해 성공 알림도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-176">If you have assigned default hostnames to your web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="9730a-177">선택한 호스트 이름이 **호스트 이름** 섹션의 **사용자 지정 도메인** 페이지에도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-177">You also see the selected hostnames in the **Custom domains** page, in the **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="9730a-178">호스트 이름을 테스트하려면 브라우저에서 나열된 호스트 이름으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-178">To test the hostnames, navigate to the listed hostnames in the browser.</span></span> <span data-ttu-id="9730a-179">이전 스크린샷의 예에서 _kontoso.net_ 및 _www.kontoso.net_으로 이동해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-179">In the example in the preceding screenshot, try navigating to _kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-to-web-app"></a><span data-ttu-id="9730a-180">웹앱에 호스트 이름 할당</span><span class="sxs-lookup"><span data-stu-id="9730a-180">Assign hostnames to web app</span></span>

<span data-ttu-id="9730a-181">구매 과정에서 웹앱에 기본 호스트 이름을 하나 이상 할당하지 않도록 선택한 경우 또는 나열되지 않은 호스트 이름을 할당해야 하는 경우 언제든지 호스트 이름을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-181">If you choose not to assign one or more default hostnames to your web app during the purchase process, or if you need to assign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="9730a-182">App Service 도메인에서 다른 웹앱으로 호스트 이름을 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-182">You can also assign hostnames in the App Service Domain to any other web app.</span></span> <span data-ttu-id="9730a-183">이 단계는 App Service 도메인 및 웹앱이 동일한 구독에 속하는지 여부에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-183">The steps depend on whether the App Service Domain and the web app belong to the same subscription.</span></span>

- <span data-ttu-id="9730a-184">다른 구독: App Service 도메인에서 외부에서 구매한 도메인과 같은 웹앱으로 사용자 지정 DNS 레코드를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-184">Different subscription: Map custom DNS records from the App Service Domain to the web app like an externally purchased domain.</span></span> <span data-ttu-id="9730a-185">사용자 지정 DNS 이름을 App Service 도메인에 추가하는 방법에 대한 자세한 내용은 [사용자 지정 DNS 레코드 관리](#custom)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9730a-185">For information on adding custom DNS names to an App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="9730a-186">외부에서 구매한 도메인을 웹앱에 매핑하려면 [Azure Web Apps에 기존 사용자 지정 DNS 이름 매핑](app-service-web-tutorial-custom-domain.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9730a-186">To map an external purchased domain to a web app, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="9730a-187">같은 구독: 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-187">Same subscription: Use the following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="9730a-188">호스트 이름 추가 시작</span><span class="sxs-lookup"><span data-stu-id="9730a-188">Launch add hostname</span></span>
<span data-ttu-id="9730a-189">**App Services** 페이지에서 호스트 이름을 할당할 웹앱 이름을 선택하고 **설정**, **사용자 지정 도메인**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-189">In the **App Services** page, select the name of your web app that you want to assign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="9730a-190">구매한 도메인이 **App Service 도메인** 섹션에 나열되는지 확인하되, 선택하지는 마세요.</span><span class="sxs-lookup"><span data-stu-id="9730a-190">Make sure that your purchased domain is listed in the **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="9730a-191">같은 구독에 있는 모든 App Service 도메인은 웹앱의 **사용자 지정 도메인** 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-191">All App Service Domains in the same subscription are shown in the web app's **Custom domains** page.</span></span> <span data-ttu-id="9730a-192">도메인이 웹앱의 구독에 있지만 웹앱의 **사용자 지정 도메인** 페이지에서 볼 수 없는 경우 **사용자 지정 도메인** 페이지를 다시 열거나 웹 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-192">If your domain is in the web app's subscription, but you cannot see it in the web app's **Custom domains** page, try reopening the **Custom domains** page or refresh the webpage.</span></span> <span data-ttu-id="9730a-193">또한 Azure Portal의 맨 위에서 진행 상황 또는 생성 실패에 대한 알림 벨을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-193">Also, check the notification bell at the top of the Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="9730a-194">**호스트 이름 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="9730a-195">호스트 이름 구성</span><span class="sxs-lookup"><span data-stu-id="9730a-195">Configure hostname</span></span>
<span data-ttu-id="9730a-196">**호스트 이름 추가** 대화 상자에서 App Service 도메인 또는 하위 도메인의 정규화된 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-196">In the **Add hostname** dialog, type the fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="9730a-197">예:</span><span class="sxs-lookup"><span data-stu-id="9730a-197">For example:</span></span>

- <span data-ttu-id="9730a-198">kontoso.net</span><span class="sxs-lookup"><span data-stu-id="9730a-198">kontoso.net</span></span>
- <span data-ttu-id="9730a-199">www.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="9730a-199">www.kontoso.net</span></span>
- <span data-ttu-id="9730a-200">abc.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="9730a-200">abc.kontoso.net</span></span>

<span data-ttu-id="9730a-201">완료되면 **유효성 검사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-201">When finished, select **Validate**.</span></span> <span data-ttu-id="9730a-202">호스트 이름 레코드 형식이 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-202">The hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="9730a-203">**호스트 이름 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-203">Select **Add hostname**.</span></span>

<span data-ttu-id="9730a-204">작업이 완료되면 할당된 호스트 이름에 대해 성공 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-204">When the operation is complete, you see a success notification for the assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="9730a-205">호스트 이름 추가 닫기</span><span class="sxs-lookup"><span data-stu-id="9730a-205">Close add hostname</span></span>
<span data-ttu-id="9730a-206">**호스트 이름 추가** 페이지에서 원하는 대로, 웹앱에 다른 호스트 이름을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-206">In the **Add hostname** page, assign any other hostname to your web app, as desired.</span></span> <span data-ttu-id="9730a-207">완료되면 **호스트 이름 추가** 페이지를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-207">When finished, close the **Add hostname** page.</span></span>

<span data-ttu-id="9730a-208">이제 **사용자 지정 도메인** 페이지에 새로 할당된 호스트 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-208">You should now see the newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-the-hostnames"></a><span data-ttu-id="9730a-209">호스트 이름 테스트</span><span class="sxs-lookup"><span data-stu-id="9730a-209">Test the hostnames</span></span>

<span data-ttu-id="9730a-210">브라우저에서 나열된 호스트 이름으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-210">Navigate to the listed hostnames in the browser.</span></span> <span data-ttu-id="9730a-211">이전 스크린샷의 예에서 _abc.kontoso.net_으로 이동해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-211">In the example in the preceding screenshot, try navigating to _abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="9730a-212">사용자 지정 DNS 레코드 관리</span><span class="sxs-lookup"><span data-stu-id="9730a-212">Manage custom DNS records</span></span>

<span data-ttu-id="9730a-213">Azure에서 App Service 도메인에 대한 DNS 레코드는 [Azure DNS](https://azure.microsoft.com/services/dns/)를 사용하여 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="9730a-214">외부에서 구매한 도메인처럼 DNS 레코드를 추가, 제거 및 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="9730a-215">App Service 도메인 열기</span><span class="sxs-lookup"><span data-stu-id="9730a-215">Open App Service Domain</span></span>

<span data-ttu-id="9730a-216">Azure Portal의 왼쪽 메뉴에서 **추가 서비스** > **App Service 도메인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-216">In the Azure portal, from the left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="9730a-217">관리할 도메인을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-217">Select the domain to manage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="9730a-218">DNS 영역 액세스</span><span class="sxs-lookup"><span data-stu-id="9730a-218">Access DNS zone</span></span>

<span data-ttu-id="9730a-219">도메인의 왼쪽 메뉴에서 **DNS 영역**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-219">In the domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="9730a-220">이 작업으로 Azure DNS에서 App Service 도메인의 [DNS 영역](../dns/dns-zones-records.md) 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-220">This action opens the [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="9730a-221">DNS 레코드를 편집하는 방법에 대한 자세한 내용은 [Azure Portal에서 DNS 영역을 관리하는 방법](../dns/dns-operations-dnszones-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9730a-221">For information on how to edit DNS records, see [How to manage DNS Zones in the Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="9730a-222">구매 취소(도메인 삭제)</span><span class="sxs-lookup"><span data-stu-id="9730a-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="9730a-223">App Service 도메인을 구매한 후 5일 이내에 구매를 취소하고 전액 환불 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-223">After you purchase the App Service Domain, you have five days to cancel your purchase for a full refund.</span></span> <span data-ttu-id="9730a-224">5일이 지나면 App Service 도메인을 삭제할 수 있지만 환불은 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-224">After five days, you can delete the App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="9730a-225">App Service 도메인 열기</span><span class="sxs-lookup"><span data-stu-id="9730a-225">Open App Service Domain</span></span>

<span data-ttu-id="9730a-226">Azure Portal의 왼쪽 메뉴에서 **추가 서비스** > **App Service 도메인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-226">In the Azure portal, from the left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="9730a-227">취소 또는 삭제할 도메인을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-227">Select the domain to you want to cancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="9730a-228">호스트 이름 바인딩 삭제</span><span class="sxs-lookup"><span data-stu-id="9730a-228">Delete hostname bindings</span></span>

<span data-ttu-id="9730a-229">도메인의 왼쪽 메뉴에서 **호스트 이름 바인딩**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-229">In the domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="9730a-230">모든 Azure 서비스의 호스트 이름 바인딩이 여기에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-230">The hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="9730a-231">모든 호스트 이름 바인딩이 삭제되어야 App Service 도메인을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-231">You cannot delete the App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="9730a-232">**...** > **삭제**를 선택하여 각 호스트 이름 바인딩을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="9730a-233">모든 바인딩을 삭제한 후 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-233">After all the bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="9730a-234">취소 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="9730a-234">Cancel or delete</span></span>

<span data-ttu-id="9730a-235">도메인의 왼쪽 메뉴에서 **개요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-235">In the domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="9730a-236">구매한 도메인에 대한 취소 기간이 경과되지 않은 경우 **구매 취소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-236">If the cancellation period on the purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="9730a-237">그렇지 않으면 **삭제** 단추가 대신 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="9730a-238">환불하지 않고 도메인을 삭제하려면 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-238">To delete the domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="9730a-239">**확인**을 선택하여 작업을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-239">Select **OK** to confirm the operation.</span></span> <span data-ttu-id="9730a-240">계속하지 않으려면 확인 대화 상자 외부의 아무 곳이나 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-240">If you don't want to proceed, click anywhere outside of the confirmation dialog.</span></span>

<span data-ttu-id="9730a-241">작업이 완료되면 구독에서 도메인이 해제되어 누구든지 다시 구매할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9730a-241">After the operation is complete, the domain is released from your subscription and available for anyone to purchase again.</span></span> 
