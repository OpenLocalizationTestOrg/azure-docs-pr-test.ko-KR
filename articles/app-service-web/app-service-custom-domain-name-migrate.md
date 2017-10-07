---
title: "aaaMigrate active DNS 이름을 tooAzure 앱 서비스 | Microsoft Docs"
description: "Toomigrate tooa 이미 할당 되어 있는 사용자 지정 DNS 도메인 이름을 사이트 tooAzure 앱 서비스 가동 중지 시간 없이 라이브 하는 방법에 대해 알아봅니다."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a><span data-ttu-id="d1549-103">마이그레이션 활성 DNS 이름 tooAzure 앱 서비스</span><span class="sxs-lookup"><span data-stu-id="d1549-103">Migrate an active DNS name tooAzure App Service</span></span>

<span data-ttu-id="d1549-104">이 문서에서는 어떻게 toomigrate active DNS 이름이 너무[Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) 가동 중지 시간 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-104">This article shows you how toomigrate an active DNS name too[Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="d1549-105">라이브 사이트 및 해당 DNS 도메인 이름 tooApp 서비스를 마이그레이션하는 경우 DNS 이름을 이미 제공 하는 중인 라이브 트래픽입니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-105">When you migrate a live site and its DNS domain name tooApp Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="d1549-106">Hello 활성 DNS 이름 tooyour 앱 서비스 앱을 미리 바인딩하여 hello 마이그레이션하는 동안 DNS 확인에 가동 중지 시간을 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-106">You can avoid downtime in DNS resolution during hello migration by binding hello active DNS name tooyour App Service app preemptively.</span></span>

<span data-ttu-id="d1549-107">DNS 확인에 가동 중지 시간에 대 한 걱정 모르겠으면 참조 [는 기존 사용자 지정 DNS 이름 tooAzure 웹 응용 프로그램을 매핑할](app-service-web-tutorial-custom-domain.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1549-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d1549-108">Prerequisites</span></span>

<span data-ttu-id="d1549-109">이 방법 toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d1549-109">toocomplete this how-to:</span></span>

- <span data-ttu-id="d1549-110">[App Service 앱이 무료 계층에 있지 않은지 확인합니다](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="d1549-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-hello-domain-name-preemptively"></a><span data-ttu-id="d1549-111">여기서 hello 도메인 이름 바인딩</span><span class="sxs-lookup"><span data-stu-id="d1549-111">Bind hello domain name preemptively</span></span>

<span data-ttu-id="d1549-112">여기서 사용자 지정 도메인을 바인딩하는 경우 DNS 레코드를 변경 하기 전에 hello 다음 중 둘 다 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-112">When you bind a custom domain preemptively, you accomplish both of hello following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="d1549-113">도메인 소유권 확인</span><span class="sxs-lookup"><span data-stu-id="d1549-113">Verify domain ownership</span></span>
- <span data-ttu-id="d1549-114">앱에 대 한 hello 도메인 이름을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d1549-114">Enable hello domain name for your app</span></span>

<span data-ttu-id="d1549-115">Hello 이전 사이트 toohello 앱 서비스 앱에서에서 사용자 지정 DNS 이름을 마지막으로 마이그레이션하면 됩니다 가동 중지 시간 없이 DNS 확인에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-115">When you finally migrate your custom DNS name from hello old site toohello App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="d1549-116">도메인 확인 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="d1549-116">Create domain verification record</span></span>

<span data-ttu-id="d1549-117">tooverify 도메인 소유권을 TXT 추가 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-117">tooverify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="d1549-118">hello TXT 레코드에서 매핑합니다 _awverify.&lt; 하위 도메인 >_ too_&lt;응용 프로그램 이름 >. azurewebsites.net_ 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-118">hello TXT record maps from _awverify.&lt;subdomain>_ too_&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="d1549-119">TXT 레코드 필요한 hello hello toomigrate DNS 레코드에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-119">hello TXT record you need depends on hello DNS record you want toomigrate.</span></span> <span data-ttu-id="d1549-120">예제를 보려면 다음 표는 hello (`@` 일반적으로 나타내는 hello 루트 도메인):</span><span class="sxs-lookup"><span data-stu-id="d1549-120">For examples, see hello following table (`@` typically represents hello root domain):</span></span>  

| <span data-ttu-id="d1549-121">DNS 레코드 예제</span><span class="sxs-lookup"><span data-stu-id="d1549-121">DNS record example</span></span> | <span data-ttu-id="d1549-122">TXT 호스트</span><span class="sxs-lookup"><span data-stu-id="d1549-122">TXT Host</span></span> | <span data-ttu-id="d1549-123">TXT 값</span><span class="sxs-lookup"><span data-stu-id="d1549-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="d1549-124">@(루트)</span><span class="sxs-lookup"><span data-stu-id="d1549-124">@ (root)</span></span> | <span data-ttu-id="d1549-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="d1549-125">_awverify_</span></span> | <span data-ttu-id="d1549-126">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="d1549-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="d1549-127">www(하위)</span><span class="sxs-lookup"><span data-stu-id="d1549-127">www (sub)</span></span> | <span data-ttu-id="d1549-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="d1549-128">_awverify.www_</span></span> | <span data-ttu-id="d1549-129">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="d1549-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="d1549-130">\*(와일드카드)</span><span class="sxs-lookup"><span data-stu-id="d1549-130">\* (wildcard)</span></span> | <span data-ttu-id="d1549-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="d1549-131">_awverify.\*_</span></span> | <span data-ttu-id="d1549-132">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="d1549-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="d1549-133">DNS 레코드 페이지의 note hello 레코드 종류 hello toomigrate 원하는 DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-133">In your DNS records page, note hello record type of hello DNS name you want toomigrate.</span></span> <span data-ttu-id="d1549-134">App Service는 CNAME 및 A 레코드로부터의 매핑을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-hello-domain-for-your-app"></a><span data-ttu-id="d1549-135">앱에 대 한 hello 도메인을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d1549-135">Enable hello domain for your app</span></span>

<span data-ttu-id="d1549-136">Hello에 [Azure 포털](https://portal.azure.com)hello hello 응용 프로그램 페이지의 왼쪽된 탐색에서 선택 **사용자 지정 도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-136">In hello [Azure portal](https://portal.azure.com), in hello left navigation of hello app page, select **Custom domains**.</span></span> 

![사용자 지정 도메인 메뉴](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="d1549-138">Hello에 **사용자 지정 도메인** 페이지, 선택 hello  **+**  아이콘 다음 너무**호스트 이름 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-138">In hello **Custom domains** page, select hello **+** icon next too**Add hostname**.</span></span>

![호스트 이름 추가](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="d1549-140">형식 hello 정규화 된 도메인 이름에 대 한 hello TXT 레코드를와 같은 추가 `www.contoso.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-140">Type hello fully qualified domain name that you added hello TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="d1549-141">와일드 카드 도메인에 대 한 (같은 \*. contoso.com)을 hello 와일드 카드 도메인 일치 하는 모든 DNS 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches hello wildcard domain.</span></span> 

<span data-ttu-id="d1549-142">**유효성 검사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-142">Select **Validate**.</span></span>

<span data-ttu-id="d1549-143">hello **호스트 이름 추가** 단추가 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-143">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="d1549-144">다음 사항을 확인 **Hostname 레코드 종류** toohello DNS 레코드 종류 toomigrate 원하는 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-144">Make sure that **Hostname record type** is set toohello DNS record type you want toomigrate.</span></span>

<span data-ttu-id="d1549-145">**호스트 이름 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-145">Select **Add hostname**.</span></span>

![DNS 이름 toohello 앱 추가](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="d1549-147">Hello 새 호스트 이름 toobe hello 응용 프로그램에 반영 약간의 시간이 걸릴 수 있습니다 **사용자 지정 도메인** 페이지.</span><span class="sxs-lookup"><span data-stu-id="d1549-147">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="d1549-148">Hello 브라우저 tooupdate hello 데이터를 새로 고쳐 보십시오.</span><span class="sxs-lookup"><span data-stu-id="d1549-148">Try refreshing hello browser tooupdate hello data.</span></span>

![추가된 CNAME 레코드](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="d1549-150">이제 Azure 앱에서 사용자 지정 DNS 이름을 사용할 수 있도록 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-hello-active-dns-name"></a><span data-ttu-id="d1549-151">Hello 활성 DNS 이름을 다시 매핑</span><span class="sxs-lookup"><span data-stu-id="d1549-151">Remap hello active DNS name</span></span>

<span data-ttu-id="d1549-152">hello 것만 왼쪽된 toodo은 다시 매핑에 활성 DNS 레코드 toopoint tooApp 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-152">hello only thing left toodo is remapping your active DNS record toopoint tooApp Service.</span></span> <span data-ttu-id="d1549-153">오른쪽 이제 여전히 가리키도록 tooyour 이전 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-153">Right now, it still points tooyour old site.</span></span>

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a><span data-ttu-id="d1549-154">Hello 응용 프로그램의 IP 주소 (A 레코드만 해당)를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-154">Copy hello app's IP address (A record only)</span></span>

<span data-ttu-id="d1549-155">CNAME 레코드를 다시 매핑하는 경우 이 섹션을 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="d1549-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="d1549-156">hello에 표시 되어 hello 앱 서비스 앱의 외부 IP 주소가 필요한 tooremap A 레코드 **사용자 지정 도메인** 페이지.</span><span class="sxs-lookup"><span data-stu-id="d1549-156">tooremap an A record, you need hello App Service app's external IP address, which is shown in hello **Custom domains** page.</span></span>

<span data-ttu-id="d1549-157">닫기 hello **호스트 이름 추가** 페이지를 선택 하 여 **X** hello 오른쪽 위 모퉁이에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-157">Close hello **Add hostname** page by selecting **X** in hello upper-right corner.</span></span> 

<span data-ttu-id="d1549-158">Hello에 **사용자 지정 도메인** 페이지, hello 응용 프로그램의 IP 주소를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-158">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a><span data-ttu-id="d1549-160">Hello DNS 레코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="d1549-160">Update hello DNS record</span></span>

<span data-ttu-id="d1549-161">도메인 공급자의 DNS 레코드 페이지 hello에 다시 hello DNS 레코드 tooremap를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-161">Back in hello DNS records page of your domain provider, select hello DNS record tooremap.</span></span>

<span data-ttu-id="d1549-162">Hello에 대 한 `contoso.com` 루트 도메인 예, 다음 표에 hello에 hello 예제와 같은 hello A 또는 CNAME 레코드를 다시 매핑해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-162">For hello `contoso.com` root domain example, remap hello A or CNAME record like hello examples in hello following table:</span></span> 

| <span data-ttu-id="d1549-163">FQDN 예</span><span class="sxs-lookup"><span data-stu-id="d1549-163">FQDN example</span></span> | <span data-ttu-id="d1549-164">레코드 형식</span><span class="sxs-lookup"><span data-stu-id="d1549-164">Record type</span></span> | <span data-ttu-id="d1549-165">호스트</span><span class="sxs-lookup"><span data-stu-id="d1549-165">Host</span></span> | <span data-ttu-id="d1549-166">값</span><span class="sxs-lookup"><span data-stu-id="d1549-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="d1549-167">contoso.com(루트)</span><span class="sxs-lookup"><span data-stu-id="d1549-167">contoso.com (root)</span></span> | <span data-ttu-id="d1549-168">A</span><span class="sxs-lookup"><span data-stu-id="d1549-168">A</span></span> | `@` | <span data-ttu-id="d1549-169">IP 주소를 [복사 hello 응용 프로그램의 IP 주소](#info)</span><span class="sxs-lookup"><span data-stu-id="d1549-169">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="d1549-170">www.contoso.com(하위)</span><span class="sxs-lookup"><span data-stu-id="d1549-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="d1549-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="d1549-171">CNAME</span></span> | `www` | <span data-ttu-id="d1549-172">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="d1549-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="d1549-173">\*.contoso.com(와일드카드)</span><span class="sxs-lookup"><span data-stu-id="d1549-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="d1549-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="d1549-174">CNAME</span></span> | _\*_ | <span data-ttu-id="d1549-175">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="d1549-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="d1549-176">설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-176">Save your settings.</span></span>

<span data-ttu-id="d1549-177">DNS 쿼리 DNS 전파가 발생 직후 tooyour 앱 서비스 앱 확인을 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-177">DNS queries should start resolving tooyour App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1549-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d1549-178">Next steps</span></span>

<span data-ttu-id="d1549-179">사용자 지정 SSL toobind tooApp 서비스 인증서 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d1549-179">Learn how toobind a custom SSL certificate tooApp Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d1549-180">기존 사용자 지정 SSL 인증서 tooAzure 웹 응용 프로그램 바인딩</span><span class="sxs-lookup"><span data-stu-id="d1549-180">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
