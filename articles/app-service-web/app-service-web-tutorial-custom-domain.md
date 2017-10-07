---
title: "기존 사용자 지정 DNS aaaMap tooAzure 웹 앱 이름을 | Microsoft Docs"
description: "Tooadd 기존 사용자 지정 DNS 도메인 (베 니 티 도메인) tooa 웹 앱, 모바일 앱 백 엔드, 또는 Azure 앱 서비스에서 API 앱 이름 지정 방법을 알아봅니다."
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
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a><span data-ttu-id="a07fd-103">지도 기존 사용자 지정 DNS 이름 tooAzure 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="a07fd-103">Map an existing custom DNS name tooAzure Web Apps</span></span>

<span data-ttu-id="a07fd-104">[Azure Web Apps](app-service-web-overview.md)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="a07fd-105">이 자습서는 기존 사용자 지정 DNS toomap tooAzure 웹 응용 프로그램 이름 지정 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-105">This tutorial shows you how toomap an existing custom DNS name tooAzure Web Apps.</span></span>

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="a07fd-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a07fd-108">CNAME 레코드를 사용하여 하위 도메인(예: `www.contoso.com`) 매핑</span><span class="sxs-lookup"><span data-stu-id="a07fd-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="a07fd-109">A 레코드를 사용하여 루트 도메인(예: `contoso.com`) 매핑</span><span class="sxs-lookup"><span data-stu-id="a07fd-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="a07fd-110">CNAME 레코드를 사용하여 와일드카드 도메인(예: `*.contoso.com`) 매핑</span><span class="sxs-lookup"><span data-stu-id="a07fd-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="a07fd-111">스크립트로 도메인 매핑 자동화</span><span class="sxs-lookup"><span data-stu-id="a07fd-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="a07fd-112">하나를 사용할 수는 **CNAME 레코드** 또는 **레코드** toomap 사용자 지정 DNS tooApp 서비스 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-112">You can use either a **CNAME record** or an **A record** toomap a custom DNS name tooApp Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="a07fd-113">루트 도메인(예: `contoso.com`)을 제외한 모든 사용자 지정 DNS 이름에 대해 CNAME을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="a07fd-114">toomigrate 라이브 사이트 및 서비스의 DNS 도메인 이름 tooApp 참조 [활성 DNS 이름 tooAzure 앱 서비스를 마이그레이션할](app-service-custom-domain-name-migrate.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-114">toomigrate a live site and its DNS domain name tooApp Service, see [Migrate an active DNS name tooAzure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a07fd-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a07fd-115">Prerequisites</span></span>

<span data-ttu-id="a07fd-116">toocomplete이이 자습서:</span><span class="sxs-lookup"><span data-stu-id="a07fd-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="a07fd-117">[App Service 앱을 만들거나](/azure/app-service/) 다른 자습서를 위해 만든 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="a07fd-118">도메인 이름을 구매 하 고 (예: GoDaddy) 도메인 공급자에 대 한 액세스 toohello DNS 레지스트리에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-118">Purchase a domain name and make sure you have access toohello DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="a07fd-119">에 대 한 DNS 항목 예를 들어 tooadd `contoso.com` 및 `www.contoso.com`, hello에 대 한 수 tooconfigure hello DNS 설정을 해야 `contoso.com` 루트 도메인.</span><span class="sxs-lookup"><span data-stu-id="a07fd-119">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must be able tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="a07fd-120">기존 도메인 이름 지정을 고려 하십시오. 없는 경우 [Azure 포털 hello를 사용 하 여 도메인을 구입](custom-dns-web-site-buydomains-web-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-120">If you don't have an existing domain name, consider [purchasing a domain using hello Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-hello-app"></a><span data-ttu-id="a07fd-121">Hello 앱 준비</span><span class="sxs-lookup"><span data-stu-id="a07fd-121">Prepare hello app</span></span>

<span data-ttu-id="a07fd-122">사용자 지정 DNS 이름 tooa 웹 앱의 경우 hello 웹 응용 프로그램의 toomap [앱 서비스 계획](https://azure.microsoft.com/pricing/details/app-service/) 유료 계층 이어야 합니다 (**Shared**, **기본**, **표준**, 또는  **프리미엄**).</span><span class="sxs-lookup"><span data-stu-id="a07fd-122">toomap a custom DNS name tooa web app, hello web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="a07fd-123">이 단계에서는 수 있도록 해당 hello hello 앱이 앱 서비스 가격 책정 계층을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-123">In this step, you make sure that hello App Service app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="a07fd-124">TooAzure에 로그인</span><span class="sxs-lookup"><span data-stu-id="a07fd-124">Sign in tooAzure</span></span>

<span data-ttu-id="a07fd-125">열기 hello [Azure 포털](https://portal.azure.com) Azure 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-125">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="a07fd-126">Hello Azure 포털에서에서 toohello 응용 프로그램 이동</span><span class="sxs-lookup"><span data-stu-id="a07fd-126">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="a07fd-127">Hello 왼쪽된 메뉴에서 선택 **응용 프로그램 서비스**, hello 응용 프로그램의 hello 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-127">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="a07fd-129">Hello 앱 서비스 앱의 관리 페이지가 hello 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-129">You see hello management page of hello App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="a07fd-130">가격 책정 계층 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-130">Check hello pricing tier</span></span>

<span data-ttu-id="a07fd-131">왼쪽 탐색 hello 응용 프로그램 페이지의 hello, toohello 스크롤하여 **설정** 선택한 섹션 **(앱 서비스 계획) 수직**합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-131">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![강화 메뉴](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="a07fd-133">hello 응용 프로그램의 현재 계층에 파란색 테두리가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-133">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="a07fd-134">Toomake hello 앱 hello 중이 아닌지 확인 **무료** 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-134">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="a07fd-135">사용자 지정 DNS hello에서 지원 되지 않습니다 **무료** 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-135">Custom DNS is not supported in hello **Free** tier.</span></span> 

![가격 책정 계층 확인](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="a07fd-137">Hello 앱 서비스 계획이 없는 경우 **무료**닫기, hello **가격 책정 계층 선택** 페이지 및 너무 건너뛸[CNAME 레코드 매핑할](#cname)합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-137">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="a07fd-138">앱 서비스 계획 hello 수직 확장</span><span class="sxs-lookup"><span data-stu-id="a07fd-138">Scale up hello App Service plan</span></span>

<span data-ttu-id="a07fd-139">Hello 이미 계층 중 하나를 선택 (**Shared**, **기본**, **표준**, 또는 **프리미엄**).</span><span class="sxs-lookup"><span data-stu-id="a07fd-139">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="a07fd-140">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-140">Click **Select**.</span></span>

![가격 책정 계층 확인](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="a07fd-142">Hello 알림을 다음 표시 되 면 hello 크기 조정 작업이 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-142">When you see hello following notification, hello scale operation is complete.</span></span>

![크기 조정 작업 확인](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="a07fd-144">CNAME 레코드 매핑</span><span class="sxs-lookup"><span data-stu-id="a07fd-144">Map a CNAME record</span></span>

<span data-ttu-id="a07fd-145">Hello 자습서 예제에서는 hello에 대 한 CNAME 레코드를 추가 하면 `www` 하위 도메인 (예를 들어 `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="a07fd-145">In hello tutorial example, you add a CNAME record for hello `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="a07fd-146">Hello CNAME 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="a07fd-146">Create hello CNAME record</span></span>

<span data-ttu-id="a07fd-147">CNAME 레코드 toomap 하위 도메인 toohello 앱의 기본 호스트 이름이 추가 (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="a07fd-147">Add a CNAME record toomap a subdomain toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="a07fd-148">Hello에 대 한 `www.contoso.com` 도메인 예 hello 이름을 매핑하는 CNAME 레코드를 추가 `www` 너무`<app_name>.azurewebsites.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-148">For hello `www.contoso.com` domain example, add a CNAME record that maps hello name `www` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="a07fd-149">Hello CNAME을 추가한 후 다음 예제는 hello 같이 hello DNS 레코드 페이지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-149">After you add hello CNAME, hello DNS records page looks like hello following example:</span></span>

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a><span data-ttu-id="a07fd-151">Azure의 hello CNAME 레코드 매핑을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-151">Enable hello CNAME record mapping in Azure</span></span>

<span data-ttu-id="a07fd-152">Hello hello Azure 포털의에서 왼쪽 hello 앱 페이지 탐색, 선택 **사용자 지정 도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-152">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![사용자 지정 도메인 메뉴](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="a07fd-154">Hello에 **사용자 지정 도메인** 페이지 hello 응용 프로그램의 정규화 된 사용자 지정 DNS 이름 hello 추가 (`www.contoso.com`) toohello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-154">In hello **Custom domains** page of hello app, add hello fully qualified custom DNS name (`www.contoso.com`) toohello list.</span></span>

<span data-ttu-id="a07fd-155">선택 hello  **+**  아이콘 다음 너무**호스트 이름 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-155">Select hello **+** icon next too**Add hostname**.</span></span>

![호스트 이름 추가](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="a07fd-157">형식 hello 정규화 된 도메인 이름에 대 한 CNAME 레코드를와 같은 추가 `www.contoso.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-157">Type hello fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="a07fd-158">**유효성 검사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-158">Select **Validate**.</span></span>

<span data-ttu-id="a07fd-159">hello **호스트 이름 추가** 단추가 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-159">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="a07fd-160">다음 사항을 확인 **Hostname 레코드 종류** 너무 설정**CNAME (www.example.com 또는 모든 하위 도메인)**합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-160">Make sure that **Hostname record type** is set too**CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="a07fd-161">**호스트 이름 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-161">Select **Add hostname**.</span></span>

![DNS 이름 toohello 앱 추가](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="a07fd-163">Hello 새 호스트 이름 toobe hello 응용 프로그램에 반영 약간의 시간이 걸릴 수 있습니다 **사용자 지정 도메인** 페이지.</span><span class="sxs-lookup"><span data-stu-id="a07fd-163">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="a07fd-164">Hello 브라우저 tooupdate hello 데이터를 새로 고쳐 보십시오.</span><span class="sxs-lookup"><span data-stu-id="a07fd-164">Try refreshing hello browser tooupdate hello data.</span></span>

![추가된 CNAME 레코드](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="a07fd-166">단계를 수행 하지 하는 경우 또는 어딘가에 보시 겠어요 hello hello 페이지 맨 아래에 확인 오류 이전에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-166">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![확인 오류](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="a07fd-168">A 레코드 매핑</span><span class="sxs-lookup"><span data-stu-id="a07fd-168">Map an A record</span></span>

<span data-ttu-id="a07fd-169">Hello 자습서 예제에서는 hello 루트 도메인에 대 한 A 레코드를 추가 하면 (예를 들어 `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="a07fd-169">In hello tutorial example, you add an A record for hello root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a><span data-ttu-id="a07fd-170">Hello 응용 프로그램의 IP 주소를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-170">Copy hello app's IP address</span></span>

<span data-ttu-id="a07fd-171">toomap A 레코드를 hello 응용 프로그램의 외부 IP 주소를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-171">toomap an A record, you need hello app's external IP address.</span></span> <span data-ttu-id="a07fd-172">Hello 앱에서이 IP 주소를 찾을 수 있습니다 **사용자 지정 도메인** hello Azure 포털에서에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-172">You can find this IP address in hello app's **Custom domains** page in hello Azure portal.</span></span>

<span data-ttu-id="a07fd-173">Hello hello Azure 포털의에서 왼쪽 hello 앱 페이지 탐색, 선택 **사용자 지정 도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-173">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![사용자 지정 도메인 메뉴](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="a07fd-175">Hello에 **사용자 지정 도메인** 페이지, hello 응용 프로그램의 IP 주소를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-175">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a><span data-ttu-id="a07fd-177">Hello A 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="a07fd-177">Create hello A record</span></span>

<span data-ttu-id="a07fd-178">앱 서비스에 필요한 toomap A 레코드 tooan 앱 **두** DNS 레코드:</span><span class="sxs-lookup"><span data-stu-id="a07fd-178">toomap an A record tooan app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="a07fd-179">**A** toomap toohello 응용 프로그램의 IP 주소를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-179">An **A** record toomap toohello app's IP address.</span></span>
- <span data-ttu-id="a07fd-180">A **TXT** toomap toohello 앱의 기본 호스트 이름이 기록 `<app_name>.azurewebsites.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-180">A **TXT** record toomap toohello app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="a07fd-181">응용 프로그램 서비스 구성 타임 tooverify hello 사용자 지정 도메인을 소유 하에이 레코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-181">App Service uses this record only at configuration time, tooverify that you own hello custom domain.</span></span> <span data-ttu-id="a07fd-182">App Service에서 사용자 지정 도메인의 유효성을 검사하고 해당 도메인을 구성한 후에는 이 TXT 레코드를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="a07fd-183">Hello에 대 한 `contoso.com` 도메인 예 toohello 표 다음에 따라 hello A와 TXT 레코드를 만듭니다 (`@` 일반적으로 나타내는 hello 루트 도메인).</span><span class="sxs-lookup"><span data-stu-id="a07fd-183">For hello `contoso.com` domain example, create hello A and TXT records according toohello following table (`@` typically represents hello root domain).</span></span> 

| <span data-ttu-id="a07fd-184">레코드 형식</span><span class="sxs-lookup"><span data-stu-id="a07fd-184">Record type</span></span> | <span data-ttu-id="a07fd-185">호스트</span><span class="sxs-lookup"><span data-stu-id="a07fd-185">Host</span></span> | <span data-ttu-id="a07fd-186">값</span><span class="sxs-lookup"><span data-stu-id="a07fd-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="a07fd-187">A</span><span class="sxs-lookup"><span data-stu-id="a07fd-187">A</span></span> | `@` | <span data-ttu-id="a07fd-188">IP 주소를 [복사 hello 응용 프로그램의 IP 주소](#info)</span><span class="sxs-lookup"><span data-stu-id="a07fd-188">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="a07fd-189">TXT</span><span class="sxs-lookup"><span data-stu-id="a07fd-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="a07fd-190">Hello 레코드를 추가 하는 경우 다음 예제는 hello 같이 hello DNS 레코드 페이지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-190">When hello records are added, hello DNS records page looks like hello following example:</span></span>

![DNS 레코드 페이지](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a><span data-ttu-id="a07fd-192">Hello 응용 프로그램에서 레코드 매핑 hello를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="a07fd-192">Enable hello A record mapping in hello app</span></span>

<span data-ttu-id="a07fd-193">Hello 앱에 다시 **사용자 지정 도메인** hello Azure 포털에서에서 페이지 hello 정규화 된 사용자 지정 DNS 이름을 추가 합니다 (예를 들어 `contoso.com`) toohello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-193">Back in hello app's **Custom domains** page in hello Azure portal, add hello fully qualified custom DNS name (for example, `contoso.com`) toohello list.</span></span>

<span data-ttu-id="a07fd-194">선택 hello  **+**  아이콘 다음 너무**호스트 이름 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-194">Select hello **+** icon next too**Add hostname**.</span></span>

![호스트 이름 추가](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="a07fd-196">형식 hello 정규화 된 도메인 이름에 대 한 hello A 레코드를와 같은 구성 `contoso.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-196">Type hello fully qualified domain name that you configured hello A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="a07fd-197">**유효성 검사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-197">Select **Validate**.</span></span>

<span data-ttu-id="a07fd-198">hello **호스트 이름 추가** 단추가 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-198">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="a07fd-199">다음 사항을 확인 **Hostname 레코드 종류** 너무 설정 되어**레코드 (example.com)**합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-199">Make sure that **Hostname record type** is set too**A record (example.com)**.</span></span>

<span data-ttu-id="a07fd-200">**호스트 이름 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-200">Select **Add hostname**.</span></span>

![DNS 이름 toohello 앱 추가](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="a07fd-202">Hello 새 호스트 이름 toobe hello 응용 프로그램에 반영 약간의 시간이 걸릴 수 있습니다 **사용자 지정 도메인** 페이지.</span><span class="sxs-lookup"><span data-stu-id="a07fd-202">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="a07fd-203">Hello 브라우저 tooupdate hello 데이터를 새로 고쳐 보십시오.</span><span class="sxs-lookup"><span data-stu-id="a07fd-203">Try refreshing hello browser tooupdate hello data.</span></span>

![추가된 A 레코드](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="a07fd-205">단계를 수행 하지 하는 경우 또는 어딘가에 보시 겠어요 hello hello 페이지 맨 아래에 확인 오류 이전에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-205">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![확인 오류](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="a07fd-207">와일드카드 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="a07fd-207">Map a wildcard domain</span></span>

<span data-ttu-id="a07fd-208">매핑할 hello 자습서 예제에서는 [와일드 카드 DNS 이름이](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (예를 들어 `*.contoso.com`) toohello CNAME 레코드를 추가 하 여 앱 서비스 앱.</span><span class="sxs-lookup"><span data-stu-id="a07fd-208">In hello tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) toohello App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="a07fd-209">Hello CNAME 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="a07fd-209">Create hello CNAME record</span></span>

<span data-ttu-id="a07fd-210">CNAME 레코드 toomap 와일드 카드 이름 toohello 앱의 기본 호스트 이름이 추가 (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="a07fd-210">Add a CNAME record toomap a wildcard name toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="a07fd-211">Hello에 대 한 `*.contoso.com` 도메인 예 hello CNAME 레코드는 hello 이름 매핑됩니다 `*` 너무`<app_name>.azurewebsites.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-211">For hello `*.contoso.com` domain example, hello CNAME record will map hello name `*` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="a07fd-212">Hello CNAME 추가 되 면 다음 예제는 hello 같이 hello DNS 레코드 페이지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-212">When hello CNAME is added, hello DNS records page looks like hello following example:</span></span>

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a><span data-ttu-id="a07fd-214">Hello 응용 프로그램에서 hello CNAME 레코드 매핑을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-214">Enable hello CNAME record mapping in hello app</span></span>

<span data-ttu-id="a07fd-215">이제 hello 와일드 카드 이름 toohello 앱 일치 하는 모든 하위 도메인을 추가할 수 있습니다 (예를 들어 `sub1.contoso.com` 및 `sub2.contoso.com` 일치 `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="a07fd-215">You can now add any subdomain that matches hello wildcard name toohello app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="a07fd-216">Hello hello Azure 포털의에서 왼쪽 hello 앱 페이지 탐색, 선택 **사용자 지정 도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-216">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![사용자 지정 도메인 메뉴](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="a07fd-218">선택 hello  **+**  아이콘 다음 너무**호스트 이름 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-218">Select hello **+** icon next too**Add hostname**.</span></span>

![호스트 이름 추가](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="a07fd-220">Hello 와일드 카드 도메인에 일치 하는 정규화 된 도메인 이름을 입력 (예를 들어 `sub1.contoso.com`)를 선택한 후 **유효성 검사**합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-220">Type a fully qualified domain name that matches hello wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="a07fd-221">hello **호스트 이름 추가** 단추가 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-221">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="a07fd-222">다음 사항을 확인 **Hostname 레코드 종류** 너무 설정**CNAME 레코드 (www.example.com 또는 모든 하위 도메인)**합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-222">Make sure that **Hostname record type** is set too**CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="a07fd-223">**호스트 이름 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-223">Select **Add hostname**.</span></span>

![DNS 이름 toohello 앱 추가](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="a07fd-225">Hello 새 호스트 이름 toobe hello 응용 프로그램에 반영 약간의 시간이 걸릴 수 있습니다 **사용자 지정 도메인** 페이지.</span><span class="sxs-lookup"><span data-stu-id="a07fd-225">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="a07fd-226">Hello 브라우저 tooupdate hello 데이터를 새로 고쳐 보십시오.</span><span class="sxs-lookup"><span data-stu-id="a07fd-226">Try refreshing hello browser tooupdate hello data.</span></span>

<span data-ttu-id="a07fd-227">선택 hello  **+**  아이콘 다시 tooadd hello 와일드 카드 도메인 일치 하는 다른 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-227">Select hello **+** icon again tooadd another hostname that matches hello wildcard domain.</span></span> <span data-ttu-id="a07fd-228">예를 들어 `sub2.contoso.com`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-228">For example, add `sub2.contoso.com`.</span></span>

![추가된 CNAME 레코드](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="a07fd-230">브라우저에서 테스트</span><span class="sxs-lookup"><span data-stu-id="a07fd-230">Test in browser</span></span>

<span data-ttu-id="a07fd-231">찾아보기 이전에 구성 된 toohello DNS 이름 (예를 들어 `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, 및 `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="a07fd-231">Browse toohello DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="a07fd-233">스크립트를 사용하여 자동화</span><span class="sxs-lookup"><span data-stu-id="a07fd-233">Automate with scripts</span></span>

<span data-ttu-id="a07fd-234">Hello를 사용 하 여 스크립트를 사용 하는 사용자 지정 도메인의 관리를 자동화할 수 [Azure CLI](/cli/azure/install-azure-cli) 또는 [Azure PowerShell](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-234">You can automate management of custom domains with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="a07fd-235">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a07fd-235">Azure CLI</span></span> 

<span data-ttu-id="a07fd-236">다음 명령을 hello는 구성 된 사용자 지정 DNS 이름 tooan 앱 서비스 앱을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-236">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="a07fd-237">자세한 내용은 참조 [tooa 웹 응용 프로그램 사용자 지정 도메인을 매핑할](scripts/app-service-cli-configure-custom-domain.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-237">For more information, see [Map a custom domain tooa web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="a07fd-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a07fd-238">Azure PowerShell</span></span> 

<span data-ttu-id="a07fd-239">다음 명령을 hello는 구성 된 사용자 지정 DNS 이름 tooan 앱 서비스 앱을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-239">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="a07fd-240">자세한 내용은 참조 [tooa 웹 응용 프로그램 사용자 지정 도메인을 할당](scripts/app-service-powershell-configure-custom-domain.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-240">For more information, see [Assign a custom domain tooa web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a07fd-241">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a07fd-241">Next steps</span></span>

<span data-ttu-id="a07fd-242">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a07fd-243">CNAME 레코드를 사용하여 하위 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="a07fd-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="a07fd-244">A 레코드를 사용하여 루트 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="a07fd-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="a07fd-245">CNAME 레코드를 사용하여 와일드카드 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="a07fd-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="a07fd-246">스크립트로 도메인 매핑 자동화</span><span class="sxs-lookup"><span data-stu-id="a07fd-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="a07fd-247">다음 자습서 toolearn toohello 진행 방법을 toobind 사용자 지정 SSL 인증서 tooa 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="a07fd-247">Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a07fd-248">기존 사용자 지정 SSL 인증서 tooAzure 웹 응용 프로그램 바인딩</span><span class="sxs-lookup"><span data-stu-id="a07fd-248">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
