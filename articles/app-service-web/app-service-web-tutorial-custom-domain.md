---
title: "Azure Web Apps에 기존 사용자 지정 DNS 이름 매핑 | Microsoft Docs"
description: "Azure App Service의 웹앱, 모바일 앱 백 엔드 또는 API 앱에 기존 사용자 지정 DNS 도메인 이름(베니티 도메인)을 추가하는 방법을 알아봅니다."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 973cda462e8d258cc848e1036891c7f8af043102
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="map-an-existing-custom-dns-name-to-azure-web-apps"></a><span data-ttu-id="0b5f3-103">Azure Web Apps에 기존 사용자 지정 DNS 이름 매핑</span><span class="sxs-lookup"><span data-stu-id="0b5f3-103">Map an existing custom DNS name to Azure Web Apps</span></span>

<span data-ttu-id="0b5f3-104">[Azure Web Apps](app-service-web-overview.md)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="0b5f3-105">이 자습서에서는 기존 사용자 지정 DNS 이름을 Azure Web Apps에 매핑하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-105">This tutorial shows you how to map an existing custom DNS name to Azure Web Apps.</span></span>

![Azure 앱에 대한 포털 탐색](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="0b5f3-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0b5f3-108">CNAME 레코드를 사용하여 하위 도메인(예: `www.contoso.com`) 매핑</span><span class="sxs-lookup"><span data-stu-id="0b5f3-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="0b5f3-109">A 레코드를 사용하여 루트 도메인(예: `contoso.com`) 매핑</span><span class="sxs-lookup"><span data-stu-id="0b5f3-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="0b5f3-110">CNAME 레코드를 사용하여 와일드카드 도메인(예: `*.contoso.com`) 매핑</span><span class="sxs-lookup"><span data-stu-id="0b5f3-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="0b5f3-111">스크립트로 도메인 매핑 자동화</span><span class="sxs-lookup"><span data-stu-id="0b5f3-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="0b5f3-112">**CNAME 레코드** 또는 **A 레코드**를 사용하여 사용자 지정 DNS 이름을 App Service에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-112">You can use either a **CNAME record** or an **A record** to map a custom DNS name to App Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="0b5f3-113">루트 도메인(예: `contoso.com`)을 제외한 모든 사용자 지정 DNS 이름에 대해 CNAME을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="0b5f3-114">라이브 사이트 및 해당 DNS 도메인 이름을 App Service로 마이그레이션하려면 [활성 DNS 이름을 Azure App Service로 마이그레이션](app-service-custom-domain-name-migrate.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-114">To migrate a live site and its DNS domain name to App Service, see [Migrate an active DNS name to Azure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b5f3-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0b5f3-115">Prerequisites</span></span>

<span data-ttu-id="0b5f3-116">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-116">To complete this tutorial:</span></span>

* <span data-ttu-id="0b5f3-117">[App Service 앱을 만들거나](/azure/app-service/) 다른 자습서를 위해 만든 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="0b5f3-118">도메인 이름을 구입하고 도메인 공급자(예: GoDaddy)의 DNS 레지스트리에 대한 액세스 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-118">Purchase a domain name and make sure you have access to the DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="0b5f3-119">예를 들어 `contoso.com` 및 `www.contoso.com`에 대한 DNS 항목을 추가하려면 `contoso.com` 루트 도메인에 대한 DNS 설정을 구성할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-119">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must be able to configure the DNS settings for the `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0b5f3-120">기존 도메인 이름이 없으면 [Azure Portal을 사용하여 도메인을 구입](custom-dns-web-site-buydomains-web-app.md)하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-120">If you don't have an existing domain name, consider [purchasing a domain using the Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-the-app"></a><span data-ttu-id="0b5f3-121">앱 준비</span><span class="sxs-lookup"><span data-stu-id="0b5f3-121">Prepare the app</span></span>

<span data-ttu-id="0b5f3-122">사용자 지정 DNS 이름을 웹앱에 매핑하려면 [App Service 계획](https://azure.microsoft.com/pricing/details/app-service/)이 유료 계층(**공유**, **기본**, **표준** 또는 **프리미엄**)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-122">To map a custom DNS name to a web app, the web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="0b5f3-123">이 단계에서는 App Service 앱이 지원되는 가격 책정 계층에 속하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-123">In this step, you make sure that the App Service app is in the supported pricing tier.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="0b5f3-124">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="0b5f3-124">Sign in to Azure</span></span>

<span data-ttu-id="0b5f3-125">[클래식 포털](https://portal.azure.com)을 열고 Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-125">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="0b5f3-126">Azure Portal에서 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-126">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="0b5f3-127">왼쪽 메뉴에서 **App Services**를 선택한 다음 앱 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-127">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![Azure 앱에 대한 포털 탐색](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="0b5f3-129">App Service 앱의 관리 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-129">You see the management page of the App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-the-pricing-tier"></a><span data-ttu-id="0b5f3-130">가격 책정 계층 확인</span><span class="sxs-lookup"><span data-stu-id="0b5f3-130">Check the pricing tier</span></span>

<span data-ttu-id="0b5f3-131">앱 페이지의 왼쪽 탐색 영역에서 **설정** 섹션으로 스크롤하고 **강화(App Service 계획)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-131">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![강화 메뉴](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="0b5f3-133">앱의 현재 계층은 파란색 테두리로 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-133">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="0b5f3-134">앱이 **무료** 계층에 속해 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-134">Check to make sure that the app is not in the **Free** tier.</span></span> <span data-ttu-id="0b5f3-135">사용자 지정 DNS는 **무료** 계층에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-135">Custom DNS is not supported in the **Free** tier.</span></span> 

![가격 책정 계층 확인](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="0b5f3-137">App Service 계획이 **무료** 계층이 아닌 경우 **가격 책정 계층 선택** 페이지를 닫고 [CNAME 레코드 매핑](#cname)으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-137">If the App Service plan is not **Free**, close the **Choose your pricing tier** page and skip to [Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="0b5f3-138">강화 - App Service 계획</span><span class="sxs-lookup"><span data-stu-id="0b5f3-138">Scale up the App Service plan</span></span>

<span data-ttu-id="0b5f3-139">무료가 아닌 계층(**공유**, **기본**, **표준** 또는 **프리미엄**) 중에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-139">Select any of the non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="0b5f3-140">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-140">Click **Select**.</span></span>

![가격 책정 계층 확인](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="0b5f3-142">다음 알림이 표시되면 강화 작업이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-142">When you see the following notification, the scale operation is complete.</span></span>

![크기 조정 작업 확인](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="0b5f3-144">CNAME 레코드 매핑</span><span class="sxs-lookup"><span data-stu-id="0b5f3-144">Map a CNAME record</span></span>

<span data-ttu-id="0b5f3-145">자습서 예제에서는 `www` 하위 도메인(예: `www.contoso.com`)에 대한 CNAME 레코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-145">In the tutorial example, you add a CNAME record for the `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-cname-record"></a><span data-ttu-id="0b5f3-146">CNAME 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="0b5f3-146">Create the CNAME record</span></span>

<span data-ttu-id="0b5f3-147">CNAME 레코드를 추가하여 하위 도메인을 앱의 기본 호스트 이름(`<app_name>.azurewebsites.net`)에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-147">Add a CNAME record to map a subdomain to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="0b5f3-148">`www.contoso.com` 도메인 예제의 경우 `www` 이름을 `<app_name>.azurewebsites.net`에 매핑하는 CNAME 레코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-148">For the `www.contoso.com` domain example, add a CNAME record that maps the name `www` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="0b5f3-149">CNAME을 추가하면 DNS 레코드 페이지가 다음 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-149">After you add the CNAME, the DNS records page looks like the following example:</span></span>

![Azure 앱에 대한 포털 탐색](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-the-cname-record-mapping-in-azure"></a><span data-ttu-id="0b5f3-151">Azure에서 CNAME 레코드 매핑 사용</span><span class="sxs-lookup"><span data-stu-id="0b5f3-151">Enable the CNAME record mapping in Azure</span></span>

<span data-ttu-id="0b5f3-152">Azure Portal의 앱 페이지 왼쪽 탐색 영역에서 **사용자 지정 도메인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-152">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![사용자 지정 도메인 메뉴](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="0b5f3-154">앱의 **사용자 지정 도메인** 페이지에서 정규화된 사용자 지정 DNS 이름(`www.contoso.com`)을 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-154">In the **Custom domains** page of the app, add the fully qualified custom DNS name (`www.contoso.com`) to the list.</span></span>

<span data-ttu-id="0b5f3-155">**호스트 이름 추가** 옆에 있는 **+** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-155">Select the **+** icon next to **Add hostname**.</span></span>

![호스트 이름 추가](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="0b5f3-157">`www.contoso.com`과 같이 CNAME 레코드를 추가한 정규화된 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-157">Type the fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="0b5f3-158">**유효성 검사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-158">Select **Validate**.</span></span>

<span data-ttu-id="0b5f3-159">**호스트 이름 추가** 단추가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-159">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="0b5f3-160">**호스트 이름 레코드 형식**이 **CNAME (www.example.com 또는 하위 도메인)**으로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-160">Make sure that **Hostname record type** is set to **CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="0b5f3-161">**호스트 이름 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-161">Select **Add hostname**.</span></span>

![앱에 DNS 이름 추가](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="0b5f3-163">새 호스트 이름이 앱의 **사용자 지정 도메인** 페이지에 반영되는 데에는 약간의 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-163">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="0b5f3-164">데이터를 업데이트하려면 브라우저를 새로 고쳐 보세요.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-164">Try refreshing the browser to update the data.</span></span>

![추가된 CNAME 레코드](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="0b5f3-166">이전에 단계를 잊었거나 철자를 잘못 입력한 경우에는 페이지 아래쪽에 확인 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-166">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![확인 오류](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="0b5f3-168">A 레코드 매핑</span><span class="sxs-lookup"><span data-stu-id="0b5f3-168">Map an A record</span></span>

<span data-ttu-id="0b5f3-169">자습서의 예제에서는 루트 도메인(예: `contoso.com`)에 대한 A 레코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-169">In the tutorial example, you add an A record for the root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-the-apps-ip-address"></a><span data-ttu-id="0b5f3-170">앱의 IP 주소 복사</span><span class="sxs-lookup"><span data-stu-id="0b5f3-170">Copy the app's IP address</span></span>

<span data-ttu-id="0b5f3-171">A 레코드를 매핑하려면 앱의 외부 IP 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-171">To map an A record, you need the app's external IP address.</span></span> <span data-ttu-id="0b5f3-172">이 IP 주소는 Azure Portal에서 보여 주는 해당 앱의 **사용자 지정 도메인** 페이지에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-172">You can find this IP address in the app's **Custom domains** page in the Azure portal.</span></span>

<span data-ttu-id="0b5f3-173">Azure Portal의 앱 페이지 왼쪽 탐색 영역에서 **사용자 지정 도메인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-173">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![사용자 지정 도메인 메뉴](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="0b5f3-175">**사용자 지정 도메인** 페이지에서 앱의 IP 주소를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-175">In the **Custom domains** page, copy the app's IP address.</span></span>

![Azure 앱에 대한 포털 탐색](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-a-record"></a><span data-ttu-id="0b5f3-177">A 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="0b5f3-177">Create the A record</span></span>

<span data-ttu-id="0b5f3-178">앱에 A 레코드를 매핑하려면 App Service에 다음 **두** 개의 DNS 레코드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-178">To map an A record to an app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="0b5f3-179">앱의 IP 주소에 매핑할 **A** 레코드</span><span class="sxs-lookup"><span data-stu-id="0b5f3-179">An **A** record to map to the app's IP address.</span></span>
- <span data-ttu-id="0b5f3-180">앱의 기본 호스트 이름(`<app_name>.azurewebsites.net`)에 매핑할 **TXT** 레코드 -</span><span class="sxs-lookup"><span data-stu-id="0b5f3-180">A **TXT** record to map to the app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="0b5f3-181">App Service에서 구성할 때만 이 레코드를 사용하여 사용자 지정 도메인을 소유하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-181">App Service uses this record only at configuration time, to verify that you own the custom domain.</span></span> <span data-ttu-id="0b5f3-182">App Service에서 사용자 지정 도메인의 유효성을 검사하고 해당 도메인을 구성한 후에는 이 TXT 레코드를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="0b5f3-183">`contoso.com` 도메인 예제의 경우 다음 표에 따라 A 및 TXT 레코드를 만듭니다(`@`는 일반적으로 루트 도메인을 나타냄).</span><span class="sxs-lookup"><span data-stu-id="0b5f3-183">For the `contoso.com` domain example, create the A and TXT records according to the following table (`@` typically represents the root domain).</span></span> 

| <span data-ttu-id="0b5f3-184">레코드 형식</span><span class="sxs-lookup"><span data-stu-id="0b5f3-184">Record type</span></span> | <span data-ttu-id="0b5f3-185">호스트</span><span class="sxs-lookup"><span data-stu-id="0b5f3-185">Host</span></span> | <span data-ttu-id="0b5f3-186">값</span><span class="sxs-lookup"><span data-stu-id="0b5f3-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="0b5f3-187">A</span><span class="sxs-lookup"><span data-stu-id="0b5f3-187">A</span></span> | `@` | <span data-ttu-id="0b5f3-188">[앱의 IP 주소 복사](#info)에서 가져온 IP 주소</span><span class="sxs-lookup"><span data-stu-id="0b5f3-188">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="0b5f3-189">TXT</span><span class="sxs-lookup"><span data-stu-id="0b5f3-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="0b5f3-190">레코드를 추가하면 DNS 레코드 페이지가 다음 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-190">When the records are added, the DNS records page looks like the following example:</span></span>

![DNS 레코드 페이지](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-the-a-record-mapping-in-the-app"></a><span data-ttu-id="0b5f3-192">앱에서 A 레코드 매핑 사용</span><span class="sxs-lookup"><span data-stu-id="0b5f3-192">Enable the A record mapping in the app</span></span>

<span data-ttu-id="0b5f3-193">Azure Portal에서 해당 앱의 **사용자 지정 도메인** 페이지로 돌아가서 정규화된 사용자 지정 DNS 이름(예: `contoso.com`)을 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-193">Back in the app's **Custom domains** page in the Azure portal, add the fully qualified custom DNS name (for example, `contoso.com`) to the list.</span></span>

<span data-ttu-id="0b5f3-194">**호스트 이름 추가** 옆에 있는 **+** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-194">Select the **+** icon next to **Add hostname**.</span></span>

![호스트 이름 추가](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="0b5f3-196">`contoso.com`과 같이 A 레코드를 구성한 정규화된 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-196">Type the fully qualified domain name that you configured the A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="0b5f3-197">**유효성 검사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-197">Select **Validate**.</span></span>

<span data-ttu-id="0b5f3-198">**호스트 이름 추가** 단추가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-198">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="0b5f3-199">**호스트 이름 레코드 형식**이 **A 레코드(example.com)**로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-199">Make sure that **Hostname record type** is set to **A record (example.com)**.</span></span>

<span data-ttu-id="0b5f3-200">**호스트 이름 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-200">Select **Add hostname**.</span></span>

![앱에 DNS 이름 추가](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="0b5f3-202">새 호스트 이름이 앱의 **사용자 지정 도메인** 페이지에 반영되는 데에는 약간의 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-202">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="0b5f3-203">데이터를 업데이트하려면 브라우저를 새로 고쳐 보세요.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-203">Try refreshing the browser to update the data.</span></span>

![추가된 A 레코드](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="0b5f3-205">이전에 단계를 잊었거나 철자를 잘못 입력한 경우에는 페이지 아래쪽에 확인 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-205">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![확인 오류](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="0b5f3-207">와일드카드 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="0b5f3-207">Map a wildcard domain</span></span>

<span data-ttu-id="0b5f3-208">이 자습서의 예제에서는 CNAME 레코드를 추가하여 [와일드카드 DNS 이름](https://en.wikipedia.org/wiki/Wildcard_DNS_record)(예: `*.contoso.com`)을 App Service 앱에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-208">In the tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) to the App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-cname-record"></a><span data-ttu-id="0b5f3-209">CNAME 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="0b5f3-209">Create the CNAME record</span></span>

<span data-ttu-id="0b5f3-210">CNAME 레코드를 추가하여 와일드카드 이름을 앱의 기본 호스트 이름(`<app_name>.azurewebsites.net`)에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-210">Add a CNAME record to map a wildcard name to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="0b5f3-211">`*.contoso.com` 도메인 예제의 경우 CNAME 레코드에서는 `*` 이름을 `<app_name>.azurewebsites.net`에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-211">For the `*.contoso.com` domain example, the CNAME record will map the name `*` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="0b5f3-212">CNAME을 추가하면 DNS 레코드 페이지가 다음 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-212">When the CNAME is added, the DNS records page looks like the following example:</span></span>

![Azure 앱에 대한 포털 탐색](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-the-cname-record-mapping-in-the-app"></a><span data-ttu-id="0b5f3-214">앱에서 CNAME 레코드 매핑 사용</span><span class="sxs-lookup"><span data-stu-id="0b5f3-214">Enable the CNAME record mapping in the app</span></span>

<span data-ttu-id="0b5f3-215">이제 와일드카드 이름과 일치하는 모든 하위 도메인을 앱에 추가할 수 있습니다(예: `sub1.contoso.com`과 `sub2.contoso.com`은 `*.contoso.com`과 일치함).</span><span class="sxs-lookup"><span data-stu-id="0b5f3-215">You can now add any subdomain that matches the wildcard name to the app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="0b5f3-216">Azure Portal의 앱 페이지 왼쪽 탐색 영역에서 **사용자 지정 도메인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-216">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![사용자 지정 도메인 메뉴](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="0b5f3-218">**호스트 이름 추가** 옆에 있는 **+** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-218">Select the **+** icon next to **Add hostname**.</span></span>

![호스트 이름 추가](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="0b5f3-220">와일드카드 도메인과 일치하는 정규화된 도메인 이름(예: `sub1.contoso.com`)을 입력한 다음 **유효성 검사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-220">Type a fully qualified domain name that matches the wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="0b5f3-221">**호스트 이름 추가** 단추가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-221">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="0b5f3-222">**호스트 이름 레코드 형식**이 **CNAME 레코드 (www.example.com 또는 하위 도메인)**으로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-222">Make sure that **Hostname record type** is set to **CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="0b5f3-223">**호스트 이름 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-223">Select **Add hostname**.</span></span>

![앱에 DNS 이름 추가](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="0b5f3-225">새 호스트 이름이 앱의 **사용자 지정 도메인** 페이지에 반영되는 데에는 약간의 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-225">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="0b5f3-226">데이터를 업데이트하려면 브라우저를 새로 고쳐 보세요.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-226">Try refreshing the browser to update the data.</span></span>

<span data-ttu-id="0b5f3-227">**+** 아이콘을 다시 선택하여 와일드카드 도메인과 일치하는 다른 호스트 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-227">Select the **+** icon again to add another hostname that matches the wildcard domain.</span></span> <span data-ttu-id="0b5f3-228">예를 들어 `sub2.contoso.com`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-228">For example, add `sub2.contoso.com`.</span></span>

![추가된 CNAME 레코드](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="0b5f3-230">브라우저에서 테스트</span><span class="sxs-lookup"><span data-stu-id="0b5f3-230">Test in browser</span></span>

<span data-ttu-id="0b5f3-231">이전에 구성한 DNS 이름(예: `contoso.com`, `www.contoso.com`, `sub1.contoso.com` 및 `sub2.contoso.com`)을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-231">Browse to the DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Azure 앱에 대한 포털 탐색](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="0b5f3-233">스크립트를 사용하여 자동화</span><span class="sxs-lookup"><span data-stu-id="0b5f3-233">Automate with scripts</span></span>

<span data-ttu-id="0b5f3-234">[Azure CLI](/cli/azure/install-azure-cli) 또는 [Azure PowerShell](/powershell/azure/overview)을 사용하여 스크립트를 통해 사용자 지정 도메인의 관리를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-234">You can automate management of custom domains with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="0b5f3-235">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0b5f3-235">Azure CLI</span></span> 

<span data-ttu-id="0b5f3-236">다음 명령은 구성된 사용자 지정 DNS 이름을 App Service 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-236">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="0b5f3-237">자세한 내용은 [웹앱에 사용자 지정 도메인 매핑](scripts/app-service-cli-configure-custom-domain.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-237">For more information, see [Map a custom domain to a web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="0b5f3-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b5f3-238">Azure PowerShell</span></span> 

<span data-ttu-id="0b5f3-239">다음 명령은 구성된 사용자 지정 DNS 이름을 App Service 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-239">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="0b5f3-240">자세한 내용은 [Web App에 사용자 지정 도메인 할당](scripts/app-service-powershell-configure-custom-domain.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-240">For more information, see [Assign a custom domain to a web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b5f3-241">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0b5f3-241">Next steps</span></span>

<span data-ttu-id="0b5f3-242">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0b5f3-243">CNAME 레코드를 사용하여 하위 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="0b5f3-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="0b5f3-244">A 레코드를 사용하여 루트 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="0b5f3-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="0b5f3-245">CNAME 레코드를 사용하여 와일드카드 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="0b5f3-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="0b5f3-246">스크립트로 도메인 매핑 자동화</span><span class="sxs-lookup"><span data-stu-id="0b5f3-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="0b5f3-247">다음 자습서로 이동하여 사용자 지정 SSL 인증서를 웹앱에 바인딩하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0b5f3-247">Advance to the next tutorial to learn how to bind a custom SSL certificate to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0b5f3-248">Azure Web Apps에 기존 사용자 지정 SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="0b5f3-248">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
