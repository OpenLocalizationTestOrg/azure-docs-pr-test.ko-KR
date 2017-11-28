---
title: "Azure 웹 앱에 대 한 사용자 지정 도메인 이름 aaaBuy"
description: "Azure 앱 서비스의 웹 앱과 toobuy 사용자 지정 도메인 이름을 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="f20ff-103">Azure Web Apps에 대한 사용자 지정 도메인 이름 구입</span><span class="sxs-lookup"><span data-stu-id="f20ff-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="f20ff-104">App Service 도메인(미리 보기)은 Azure에서 직접 관리되는 최상위 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="f20ff-105">쉽게 toomanage 사용자 지정 도메인에 게 [Azure 웹 앱](app-service-web-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-105">They make it easy toomanage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="f20ff-106">이 자습서 toobuy 앱 서비스 도메인 및 DNS 할당 tooAzure 웹 응용 프로그램 이름을 지정 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-106">This tutorial shows you how toobuy an App Service domain and assign DNS names tooAzure Web Apps.</span></span>

<span data-ttu-id="f20ff-107">이 문서는 Azure App Service(Web Apps, API Apps, Mobile Apps, Logic Apps)에 관한 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="f20ff-108">Azure VM 또는 Azure 저장소에 대 한 참조 [할당 앱 서비스 도메인 tooAzure VM 또는 Azure 저장소](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-108">For Azure VM or Azure Storage, see [Assign App Service domain tooAzure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="f20ff-109">Cloud Services의 경우 [Azure 클라우드 서비스에 대한 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f20ff-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f20ff-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f20ff-110">Prerequisites</span></span>

<span data-ttu-id="f20ff-111">toocomplete이이 자습서:</span><span class="sxs-lookup"><span data-stu-id="f20ff-111">toocomplete this tutorial:</span></span>

* <span data-ttu-id="f20ff-112">[App Service 앱을 만들거나](/azure/app-service/) 다른 자습서를 위해 만든 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-hello-app"></a><span data-ttu-id="f20ff-113">Hello 앱 준비</span><span class="sxs-lookup"><span data-stu-id="f20ff-113">Prepare hello app</span></span>

<span data-ttu-id="f20ff-114">Azure 웹 앱에서 웹 앱의 사용자 지정 도메인 toouse [앱 서비스 계획](https://azure.microsoft.com/pricing/details/app-service/) 유료 계층 이어야 합니다 (**Shared**, **기본**, **표준**, 또는 **프리미엄**).</span><span class="sxs-lookup"><span data-stu-id="f20ff-114">toouse custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="f20ff-115">이 단계에서는 있습니다 지원 되는지 확인 해당 hello 웹 앱 hello에 가격 책정 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-115">In this step, you make sure that hello web app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="f20ff-116">TooAzure에 로그인</span><span class="sxs-lookup"><span data-stu-id="f20ff-116">Sign in tooAzure</span></span>

<span data-ttu-id="f20ff-117">열기 hello [Azure 포털](https://portal.azure.com) Azure 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-117">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="f20ff-118">Hello Azure 포털에서에서 toohello 응용 프로그램 이동</span><span class="sxs-lookup"><span data-stu-id="f20ff-118">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="f20ff-119">Hello 왼쪽된 메뉴에서 선택 **응용 프로그램 서비스**, hello 응용 프로그램의 hello 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-119">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="f20ff-121">Hello 앱 서비스 앱의 관리 페이지가 hello 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-121">You see hello management page of hello App Service app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="f20ff-122">가격 책정 계층 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-122">Check hello pricing tier</span></span>

<span data-ttu-id="f20ff-123">왼쪽 탐색 hello 응용 프로그램 페이지의 hello, toohello 스크롤하여 **설정** 선택한 섹션 **(앱 서비스 계획) 수직**합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-123">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![강화 메뉴](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="f20ff-125">hello 응용 프로그램의 현재 계층에 파란색 테두리가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-125">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="f20ff-126">Toomake hello 앱 hello 중이 아닌지 확인 **무료** 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-126">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="f20ff-127">사용자 지정 DNS hello에서 지원 되지 않습니다 **무료** 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-127">Custom DNS is not supported in hello **Free** tier.</span></span> 

![가격 책정 계층 확인](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="f20ff-129">Hello 앱 서비스 계획이 없는 경우 **무료**닫기, hello **가격 책정 계층 선택** 페이지 및 너무 건너뛸[구입 hello 도메인](#buy-the-domain)합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-129">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Buy hello domain](#buy-the-domain).</span></span>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="f20ff-130">앱 서비스 계획 hello 수직 확장</span><span class="sxs-lookup"><span data-stu-id="f20ff-130">Scale up hello App Service plan</span></span>

<span data-ttu-id="f20ff-131">Hello 이미 계층 중 하나를 선택 (**Shared**, **기본**, **표준**, 또는 **프리미엄**).</span><span class="sxs-lookup"><span data-stu-id="f20ff-131">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="f20ff-132">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-132">Click **Select**.</span></span>

![가격 책정 계층 확인](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="f20ff-134">Hello 알림을 다음 표시 되 면 hello 크기 조정 작업이 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-134">When you see hello following notification, hello scale operation is complete.</span></span>

![크기 조정 작업 확인](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a><span data-ttu-id="f20ff-136">Hello 도메인 구입</span><span class="sxs-lookup"><span data-stu-id="f20ff-136">Buy hello domain</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="f20ff-137">TooAzure에 로그인</span><span class="sxs-lookup"><span data-stu-id="f20ff-137">Sign in tooAzure</span></span>
<span data-ttu-id="f20ff-138">열기 hello [Azure 포털](https://portal.azure.com/) Azure 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-138">Open hello [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="f20ff-139">도메인 구입 시작</span><span class="sxs-lookup"><span data-stu-id="f20ff-139">Launch Buy domains</span></span>
<span data-ttu-id="f20ff-140">Hello에 **웹 앱** 탭을 선택 하면 웹 앱의 hello 이름을 클릭 **설정**를 선택한 후 **사용자 지정 도메인이**</span><span class="sxs-lookup"><span data-stu-id="f20ff-140">In hello **Web Apps** tab, click hello name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="f20ff-141">Hello에 **사용자 지정 도메인** 페이지 **도메인을 구입**합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-141">In hello **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a><span data-ttu-id="f20ff-142">Hello 도메인 구매를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-142">Configure hello domain purchase</span></span>

<span data-ttu-id="f20ff-143">Hello에 **응용 프로그램 서비스 도메인** 페이지 hello **도메인에 대 한 검색** 상자 toobuy 유형과 원하는 hello 도메인 이름을 입력 합니다 `Enter`합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-143">In hello **App Service Domain** page, in hello **Search for domain** box, type hello domain name you want toobuy and type `Enter`.</span></span> <span data-ttu-id="f20ff-144">hello 제안 된 사용 가능한 도메인 아래에 표시 됩니다 바로 hello 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-144">hello suggested available domains are shown just below hello text box.</span></span> <span data-ttu-id="f20ff-145">Toobuy 원하는 하나 이상의 도메인을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-145">Select one or more domains you want toobuy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="f20ff-146">Hello 클릭 **연락처 정보** hello 도메인의 연락처 정보 양식을 작성 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-146">Click hello **Contact Information** and fill out hello domain's contact information form.</span></span> <span data-ttu-id="f20ff-147">완료 되 면 클릭 **확인** tooreturn toohello 응용 프로그램 서비스 도메인 페이지.</span><span class="sxs-lookup"><span data-stu-id="f20ff-147">When finished, click **OK** tooreturn toohello App Service Domain page.</span></span>
   
<span data-ttu-id="f20ff-148">모든 필수 필드를 가능한 한 정확하게 기입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="f20ff-149">연락처 정보에 대 한 잘못 된 데이터는 오류 toopurchase 도메인에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-149">Incorrect data for contact information can result in failure toopurchase domains.</span></span> 

<span data-ttu-id="f20ff-150">그런 다음 도메인에 대 한 hello 원하는 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-150">Next, select hello desired options for your domain.</span></span> <span data-ttu-id="f20ff-151">다음 표에서 설명 하는 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f20ff-151">See hello following table for explanations:</span></span>

| <span data-ttu-id="f20ff-152">설정</span><span class="sxs-lookup"><span data-stu-id="f20ff-152">Setting</span></span> | <span data-ttu-id="f20ff-153">제안 값</span><span class="sxs-lookup"><span data-stu-id="f20ff-153">Suggested Value</span></span> | <span data-ttu-id="f20ff-154">설명</span><span class="sxs-lookup"><span data-stu-id="f20ff-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="f20ff-155">자동 갱신</span><span class="sxs-lookup"><span data-stu-id="f20ff-155">Auto renew</span></span> | <span data-ttu-id="f20ff-156">**사용**</span><span class="sxs-lookup"><span data-stu-id="f20ff-156">**Enable**</span></span> | <span data-ttu-id="f20ff-157">매년 App Service 도메인을 자동으로 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="f20ff-158">신용 카드 청구 동일한 구매 가격의 갱신 hello 시 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-158">Your credit card is charged hello same purchase price at hello time of renewal.</span></span> |
|<span data-ttu-id="f20ff-159">개인 정보 보호</span><span class="sxs-lookup"><span data-stu-id="f20ff-159">Privacy protection</span></span> | <span data-ttu-id="f20ff-160">사용</span><span class="sxs-lookup"><span data-stu-id="f20ff-160">Enable</span></span> | <span data-ttu-id="f20ff-161">너무 옵트인 hello 구매 가격에 포함 된 "개인 정보 보호" _무료로_ (레지스트리가 개인 정보 보호와 같은 지원 하지 않습니다는 최상위 도메인을 제외한 _. co.in_, _합니다. co.uk_등).</span><span class="sxs-lookup"><span data-stu-id="f20ff-161">Opt in too"Privacy protection", which is included in hello purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="f20ff-162">기본 호스트 이름 할당</span><span class="sxs-lookup"><span data-stu-id="f20ff-162">Assign default hostnames</span></span> | <span data-ttu-id="f20ff-163">**www** 및 **@**</span><span class="sxs-lookup"><span data-stu-id="f20ff-163">**www** and **@**</span></span> | <span data-ttu-id="f20ff-164">Select hello 원하는 경우 호스트 이름 바인딩을 원하는입니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-164">Select hello desired hostname bindings, if desired.</span></span> <span data-ttu-id="f20ff-165">Hello 도메인 구매 작업이 완료 되 면 웹 앱 선택 hello 호스트 이름에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-165">When hello domain purchase operation is complete, your web app can be accessed at hello selected hostnames.</span></span> <span data-ttu-id="f20ff-166">Hello 웹 응용 프로그램 뒤에 있는 경우 [Azure 트래픽 관리자](https://azure.microsoft.com/services/traffic-manager/), hello 옵션 tooassign hello 루트 도메인에 표시 되지 않으면 (@), 트래픽 관리자가 A 레코드를 지원 하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-166">If hello web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see hello option tooassign hello root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="f20ff-167">Hello 도메인 구매를 완료 후 toohello 호스트 이름을 할당 변경 내용을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-167">You can make changes toohello hostname assignments after hello domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="f20ff-168">조건에 동의하고 구매</span><span class="sxs-lookup"><span data-stu-id="f20ff-168">Accept terms and purchase</span></span>

<span data-ttu-id="f20ff-169">클릭 **약관** tooreview hello 용어 및 hello 요금이 클릭 **구입**합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-169">Click **Legal Terms** tooreview hello terms and hello charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="f20ff-170">Azure DNS toohost hello 도메인을 사용 하는 응용 프로그램 서비스 도메인.</span><span class="sxs-lookup"><span data-stu-id="f20ff-170">App Service Domains use Azure DNS toohost hello domains.</span></span> <span data-ttu-id="f20ff-171">Toohello 도메인 등록 요금 뿐만 아니라 Azure DNS에 대 한 사용 요금이 부과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-171">In addition toohello domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="f20ff-172">자세한 내용은 [Azure DNS 가격 책정](https://azure.microsoft.com/pricing/details/dns/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f20ff-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="f20ff-173">Hello에 다시 **응용 프로그램 서비스 도메인** 페이지 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-173">Back in hello **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="f20ff-174">Hello 작업이 진행 중에서 상태인 동안 다음 알림 hello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-174">While hello operation is in progress, you see hello following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="f20ff-175">테스트 hello 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="f20ff-175">Test hello hostnames</span></span>

<span data-ttu-id="f20ff-176">기본 호스트 이름을 tooyour 웹 앱에 할당 한 경우 선택한 각 호스트 이름에 대 한 성공 알림을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-176">If you have assigned default hostnames tooyour web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="f20ff-177">Hello에 선택한 hello 호스트 이름이 표시 **사용자 지정 도메인** 페이지 hello **Hostnames** 섹션.</span><span class="sxs-lookup"><span data-stu-id="f20ff-177">You also see hello selected hostnames in hello **Custom domains** page, in hello **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="f20ff-178">tootest hello 호스트 이름, hello 브라우저에서 toohello 나열 된 호스트를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-178">tootest hello hostnames, navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="f20ff-179">Too_kontoso.net_를 이동해 보십시오 스크린 샷, 앞의 hello hello 예제 및 _www.kontoso.net_합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-179">In hello example in hello preceding screenshot, try navigating too_kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-tooweb-app"></a><span data-ttu-id="f20ff-180">호스트 이름을 tooweb 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="f20ff-180">Assign hostnames tooweb app</span></span>

<span data-ttu-id="f20ff-181">하나 tooassign 하지 않으려는 hello 동안 보다 많은 기본 호스트 이름 tooyour 웹 앱 프로세스를 구입 하거나 나열 되지 tooassign 호스트 이름을 사용 해야 할 경우, 언제 든 지 한 호스트 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-181">If you choose not tooassign one or more default hostnames tooyour web app during hello purchase process, or if you need tooassign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="f20ff-182">또한 응용 프로그램 서비스 도메인 tooany hello에에서 호스트 이름이 다른 웹 앱을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-182">You can also assign hostnames in hello App Service Domain tooany other web app.</span></span> <span data-ttu-id="f20ff-183">hello 단계에 따라 응용 프로그램 서비스 도메인 hello 및 hello 웹 앱 toohello 속한 여부 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-183">hello steps depend on whether hello App Service Domain and hello web app belong toohello same subscription.</span></span>

- <span data-ttu-id="f20ff-184">다른 구독: hello 응용 프로그램 서비스 도메인 toohello 웹 응용 프로그램 외부에서 구매한 도메인에서 사용자 지정 DNS 레코드를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-184">Different subscription: Map custom DNS records from hello App Service Domain toohello web app like an externally purchased domain.</span></span> <span data-ttu-id="f20ff-185">추가 사용자 지정 dns 정보 tooan 응용 프로그램 서비스 도메인 이름, 참조 [사용자 지정 DNS 레코드 관리](#custom)합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-185">For information on adding custom DNS names tooan App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="f20ff-186">toomap 외부 구매한 도메인 tooa 웹 응용 프로그램 참조 [는 기존 사용자 지정 DNS 이름 tooAzure 웹 응용 프로그램을 매핑할](app-service-web-tutorial-custom-domain.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-186">toomap an external purchased domain tooa web app, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="f20ff-187">동일한 구독: 사용 하 여 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-187">Same subscription: Use hello following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="f20ff-188">호스트 이름 추가 시작</span><span class="sxs-lookup"><span data-stu-id="f20ff-188">Launch add hostname</span></span>
<span data-ttu-id="f20ff-189">Hello에 **응용 프로그램 서비스** 페이지, tooassign 호스트 이름, 선택 하려는 웹 앱 이름 선택 hello **설정**를 선택한 후 **사용자 지정 도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-189">In hello **App Services** page, select hello name of your web app that you want tooassign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="f20ff-190">도메인을 구입한 hello에 나열 되어 있는지 확인 **응용 프로그램 서비스 도메인** 섹션 하지만 선택 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="f20ff-190">Make sure that your purchased domain is listed in hello **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="f20ff-191">동일한 구독 hello 웹 앱에 표시 된 hello에서 모든 응용 프로그램 서비스 도메인 **사용자 지정 도메인** 페이지.</span><span class="sxs-lookup"><span data-stu-id="f20ff-191">All App Service Domains in hello same subscription are shown in hello web app's **Custom domains** page.</span></span> <span data-ttu-id="f20ff-192">도메인은 hello 웹 앱 구독에 있지만 hello 웹 앱에서 볼 수 없는 경우 **사용자 지정 도메인** 페이지, hello를 다시 열어 보십시오 **사용자 지정 도메인** 페이지 또는 hello 웹 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-192">If your domain is in hello web app's subscription, but you cannot see it in hello web app's **Custom domains** page, try reopening hello **Custom domains** page or refresh hello webpage.</span></span> <span data-ttu-id="f20ff-193">또한, 진행률 또는 생성 실패에 대 한 hello 위쪽 hello Azure 포털의 알림 벨 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-193">Also, check hello notification bell at hello top of hello Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="f20ff-194">**호스트 이름 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="f20ff-195">호스트 이름 구성</span><span class="sxs-lookup"><span data-stu-id="f20ff-195">Configure hostname</span></span>
<span data-ttu-id="f20ff-196">Hello에 **호스트 이름 추가** 대화 상자에서 응용 프로그램 서비스 도메인 또는 모든 하위 도메인의 형식 hello 정규화 된 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-196">In hello **Add hostname** dialog, type hello fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="f20ff-197">예:</span><span class="sxs-lookup"><span data-stu-id="f20ff-197">For example:</span></span>

- <span data-ttu-id="f20ff-198">kontoso.net</span><span class="sxs-lookup"><span data-stu-id="f20ff-198">kontoso.net</span></span>
- <span data-ttu-id="f20ff-199">www.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="f20ff-199">www.kontoso.net</span></span>
- <span data-ttu-id="f20ff-200">abc.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="f20ff-200">abc.kontoso.net</span></span>

<span data-ttu-id="f20ff-201">완료되면 **유효성 검사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-201">When finished, select **Validate**.</span></span> <span data-ttu-id="f20ff-202">hello hostname 레코드 종류 자동으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-202">hello hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="f20ff-203">**호스트 이름 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-203">Select **Add hostname**.</span></span>

<span data-ttu-id="f20ff-204">Hello 작업이 완료 되 면 호스트 이름을 할당 하는 hello에 대 한 성공 알림을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-204">When hello operation is complete, you see a success notification for hello assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="f20ff-205">호스트 이름 추가 닫기</span><span class="sxs-lookup"><span data-stu-id="f20ff-205">Close add hostname</span></span>
<span data-ttu-id="f20ff-206">Hello에 **호스트 이름 추가** 페이지에서 다른 호스트 이름 tooyour 웹 앱을 원하는 대로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-206">In hello **Add hostname** page, assign any other hostname tooyour web app, as desired.</span></span> <span data-ttu-id="f20ff-207">완료 되 면 닫습니다 hello **호스트 이름 추가** 페이지.</span><span class="sxs-lookup"><span data-stu-id="f20ff-207">When finished, close hello **Add hostname** page.</span></span>

<span data-ttu-id="f20ff-208">이제 응용 프로그램에서 새로 할당 된 hello hostname(s) 표시 **사용자 지정 도메인** 페이지.</span><span class="sxs-lookup"><span data-stu-id="f20ff-208">You should now see hello newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="f20ff-209">테스트 hello 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="f20ff-209">Test hello hostnames</span></span>

<span data-ttu-id="f20ff-210">Hello 브라우저에서 toohello 나열 된 호스트를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-210">Navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="f20ff-211">Hello 스크린 샷 앞에 hello 예에서 too_abc.kontoso.net_ 탐색 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f20ff-211">In hello example in hello preceding screenshot, try navigating too_abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="f20ff-212">사용자 지정 DNS 레코드 관리</span><span class="sxs-lookup"><span data-stu-id="f20ff-212">Manage custom DNS records</span></span>

<span data-ttu-id="f20ff-213">Azure에서 App Service 도메인에 대한 DNS 레코드는 [Azure DNS](https://azure.microsoft.com/services/dns/)를 사용하여 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="f20ff-214">외부에서 구매한 도메인처럼 DNS 레코드를 추가, 제거 및 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="f20ff-215">App Service 도메인 열기</span><span class="sxs-lookup"><span data-stu-id="f20ff-215">Open App Service Domain</span></span>

<span data-ttu-id="f20ff-216">Hello hello 왼쪽된 메뉴에서 Azure 포털에서에서 선택 **더 서비스** > **응용 프로그램 서비스 도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-216">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="f20ff-217">Hello 도메인 toomanage를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-217">Select hello domain toomanage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="f20ff-218">DNS 영역 액세스</span><span class="sxs-lookup"><span data-stu-id="f20ff-218">Access DNS zone</span></span>

<span data-ttu-id="f20ff-219">Hello 도메인의 왼쪽된 메뉴에서 선택 **DNS 영역**합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-219">In hello domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="f20ff-220">Hello 열립니다 [DNS 영역](../dns/dns-zones-records.md) Azure DNS에서 서비스 응용 프로그램 도메인의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-220">This action opens hello [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="f20ff-221">방법에 대 한 tooedit DNS 레코드 참조 [toomanage DNS 영역에 Azure 포털을 hello 어떻게](../dns/dns-operations-dnszones-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-221">For information on how tooedit DNS records, see [How toomanage DNS Zones in hello Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="f20ff-222">구매 취소(도메인 삭제)</span><span class="sxs-lookup"><span data-stu-id="f20ff-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="f20ff-223">응용 프로그램 서비스 도메인 hello를 구입한 후 전체 환불에 대 한 구매 toocancel 5 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-223">After you purchase hello App Service Domain, you have five days toocancel your purchase for a full refund.</span></span> <span data-ttu-id="f20ff-224">5 일 후 응용 프로그램 서비스 도메인 hello를 삭제할 수 있지만 환불을 받을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-224">After five days, you can delete hello App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="f20ff-225">App Service 도메인 열기</span><span class="sxs-lookup"><span data-stu-id="f20ff-225">Open App Service Domain</span></span>

<span data-ttu-id="f20ff-226">Hello hello 왼쪽된 메뉴에서 Azure 포털에서에서 선택 **더 서비스** > **응용 프로그램 서비스 도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-226">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="f20ff-227">선택 hello 도메인 tooyou toocancel 하거나 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-227">Select hello domain tooyou want toocancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="f20ff-228">호스트 이름 바인딩 삭제</span><span class="sxs-lookup"><span data-stu-id="f20ff-228">Delete hostname bindings</span></span>

<span data-ttu-id="f20ff-229">Hello 도메인의 왼쪽된 메뉴에서 선택 **호스트 이름 바인딩을**합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-229">In hello domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="f20ff-230">모든 Azure 서비스에서 호스트 이름 바인딩은 hello 여기에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-230">hello hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="f20ff-231">모든 호스트 이름 바인딩을 삭제 될 때까지 hello 응용 프로그램 서비스 도메인을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-231">You cannot delete hello App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="f20ff-232">**...** > **삭제**를 선택하여 각 호스트 이름 바인딩을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="f20ff-233">모든 hello 바인딩을 삭제 된 후 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-233">After all hello bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="f20ff-234">취소 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="f20ff-234">Cancel or delete</span></span>

<span data-ttu-id="f20ff-235">Hello 도메인의 왼쪽된 메뉴에서 선택 **개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-235">In hello domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="f20ff-236">구입한 hello 도메인에 hello 취소 기간이 지나지 않은, 선택 **구입을 취소**합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-236">If hello cancellation period on hello purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="f20ff-237">그렇지 않으면 **삭제** 단추가 대신 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="f20ff-238">환불을 선택 하지 않고 toodelete hello 도메인 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-238">toodelete hello domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="f20ff-239">선택 **확인** tooconfirm hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-239">Select **OK** tooconfirm hello operation.</span></span> <span data-ttu-id="f20ff-240">Tooproceed 않으려면 hello 확인 대화 상자 외부의 아무 곳 이나 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-240">If you don't want tooproceed, click anywhere outside of hello confirmation dialog.</span></span>

<span data-ttu-id="f20ff-241">Hello 도메인은 구독에서 해제 한 후 모든 사용자에 사용할 수 있는 hello 작업이 완료 되 면 다시 toopurchase 합니다.</span><span class="sxs-lookup"><span data-stu-id="f20ff-241">After hello operation is complete, hello domain is released from your subscription and available for anyone toopurchase again.</span></span> 
