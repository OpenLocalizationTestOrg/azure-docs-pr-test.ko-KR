---
title: "Azure App Service로 활성 DNS 이름 마이그레이션 | Microsoft Docs"
description: "가동 중지 시간 없이 라이브 사이트에 이미 할당된 사용자 지정 DNS 도메인 이름을 Azure App Service로 마이그레이션하는 방법을 알아봅니다."
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
ms.openlocfilehash: 89308c1c684a639950467b72d26703cc07c50c14
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-an-active-dns-name-to-azure-app-service"></a><span data-ttu-id="eba4f-103">Azure App Service로 활성 DNS 이름 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="eba4f-103">Migrate an active DNS name to Azure App Service</span></span>

<span data-ttu-id="eba4f-104">이 문서에서는 가동 중지 시간 없이 [Azure App Service](../app-service/app-service-value-prop-what-is.md)로 활성 DNS 이름을 마이그레이션하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-104">This article shows you how to migrate an active DNS name to [Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="eba4f-105">라이브 사이트 및 해당 DNS 도메인 이름을 App Service로 마이그레이션하는 경우 DNS 이름이 이미 라이브 트래픽 서비스를 제공하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-105">When you migrate a live site and its DNS domain name to App Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="eba4f-106">활성 DNS 이름을 App Service 앱에 미리 바인딩하여 마이그레이션하는 동안 DNS 확인에 가동 중지 시간이 발생하지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-106">You can avoid downtime in DNS resolution during the migration by binding the active DNS name to your App Service app preemptively.</span></span>

<span data-ttu-id="eba4f-107">DNS 확인의 중단을 염려하지 않는 경우에는 [Azure Web Apps에 기존 사용자 지정 DNS 이름 매핑](app-service-web-tutorial-custom-domain.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eba4f-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eba4f-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="eba4f-108">Prerequisites</span></span>

<span data-ttu-id="eba4f-109">이 방법을 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-109">To complete this how-to:</span></span>

- <span data-ttu-id="eba4f-110">[App Service 앱이 무료 계층에 있지 않은지 확인합니다](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="eba4f-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-the-domain-name-preemptively"></a><span data-ttu-id="eba4f-111">도메인 이름을 먼저 바인딩</span><span class="sxs-lookup"><span data-stu-id="eba4f-111">Bind the domain name preemptively</span></span>

<span data-ttu-id="eba4f-112">사용자 지정 도메인을 먼저 바인딩하는 경우 DNS 레코드를 변경하기 전에 다음 두 가지를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-112">When you bind a custom domain preemptively, you accomplish both of the following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="eba4f-113">도메인 소유권 확인</span><span class="sxs-lookup"><span data-stu-id="eba4f-113">Verify domain ownership</span></span>
- <span data-ttu-id="eba4f-114">앱에 대해 도메인 이름 사용</span><span class="sxs-lookup"><span data-stu-id="eba4f-114">Enable the domain name for your app</span></span>

<span data-ttu-id="eba4f-115">마지막으로 이전 사이트에서 App Service 앱으로 사용자 지정 DNS 이름을 마이그레이션하는 경우 DNS 확인에 가동 중지 시간이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-115">When you finally migrate your custom DNS name from the old site to the App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="eba4f-116">도메인 확인 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="eba4f-116">Create domain verification record</span></span>

<span data-ttu-id="eba4f-117">도메인 소유권을 확인하려면 TXT 레코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-117">To verify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="eba4f-118">TXT 레코드는 _awverify.&lt;subdomain>_에서 _&lt;appname>.azurewebsites.net_으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-118">The TXT record maps from _awverify.&lt;subdomain>_ to _&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="eba4f-119">필요한 TXT 레코드는 마이그레이션할 DNS 레코드에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-119">The TXT record you need depends on the DNS record you want to migrate.</span></span> <span data-ttu-id="eba4f-120">예제를 보려면 다음 표를 참조하세요(`@`은 일반적으로 루트 도메인을 나타냄).</span><span class="sxs-lookup"><span data-stu-id="eba4f-120">For examples, see the following table (`@` typically represents the root domain):</span></span>  

| <span data-ttu-id="eba4f-121">DNS 레코드 예제</span><span class="sxs-lookup"><span data-stu-id="eba4f-121">DNS record example</span></span> | <span data-ttu-id="eba4f-122">TXT 호스트</span><span class="sxs-lookup"><span data-stu-id="eba4f-122">TXT Host</span></span> | <span data-ttu-id="eba4f-123">TXT 값</span><span class="sxs-lookup"><span data-stu-id="eba4f-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="eba4f-124">@(루트)</span><span class="sxs-lookup"><span data-stu-id="eba4f-124">@ (root)</span></span> | <span data-ttu-id="eba4f-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="eba4f-125">_awverify_</span></span> | <span data-ttu-id="eba4f-126">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="eba4f-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="eba4f-127">www(하위)</span><span class="sxs-lookup"><span data-stu-id="eba4f-127">www (sub)</span></span> | <span data-ttu-id="eba4f-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="eba4f-128">_awverify.www_</span></span> | <span data-ttu-id="eba4f-129">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="eba4f-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="eba4f-130">\*(와일드카드)</span><span class="sxs-lookup"><span data-stu-id="eba4f-130">\* (wildcard)</span></span> | <span data-ttu-id="eba4f-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="eba4f-131">_awverify.\*_</span></span> | <span data-ttu-id="eba4f-132">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="eba4f-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="eba4f-133">DNS 레코드 페이지에서 마이그레이션할 DNS 이름의 레코드 종류에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-133">In your DNS records page, note the record type of the DNS name you want to migrate.</span></span> <span data-ttu-id="eba4f-134">App Service는 CNAME 및 A 레코드로부터의 매핑을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-the-domain-for-your-app"></a><span data-ttu-id="eba4f-135">앱에 대해 도메인 사용</span><span class="sxs-lookup"><span data-stu-id="eba4f-135">Enable the domain for your app</span></span>

<span data-ttu-id="eba4f-136">[Azure Portal](https://portal.azure.com) 앱 페이지 왼쪽 탐색 영역에서 **사용자 지정 도메인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-136">In the [Azure portal](https://portal.azure.com), in the left navigation of the app page, select **Custom domains**.</span></span> 

![사용자 지정 도메인 메뉴](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="eba4f-138">**사용자 지정 도메인** 페이지에서 **호스트 이름 추가** 옆의 **+** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-138">In the **Custom domains** page, select the **+** icon next to **Add hostname**.</span></span>

![호스트 이름 추가](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="eba4f-140">`www.contoso.com`과 같이 TXT 레코드를 추가한 정규화된 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-140">Type the fully qualified domain name that you added the TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="eba4f-141">와일드카드 도메인(예: \*.contoso.com)의 경우 와일드카드 도메인과 일치하는 DNS 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches the wildcard domain.</span></span> 

<span data-ttu-id="eba4f-142">**유효성 검사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-142">Select **Validate**.</span></span>

<span data-ttu-id="eba4f-143">**호스트 이름 추가** 단추가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-143">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="eba4f-144">**호스트 이름 레코드 종류**가 마이그레이션할 DNS 레코드 종류로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-144">Make sure that **Hostname record type** is set to the DNS record type you want to migrate.</span></span>

<span data-ttu-id="eba4f-145">**호스트 이름 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-145">Select **Add hostname**.</span></span>

![앱에 DNS 이름 추가](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="eba4f-147">새 호스트 이름이 앱의 **사용자 지정 도메인** 페이지에 반영되는 데에는 약간의 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-147">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="eba4f-148">데이터를 업데이트하려면 브라우저를 새로 고쳐 보세요.</span><span class="sxs-lookup"><span data-stu-id="eba4f-148">Try refreshing the browser to update the data.</span></span>

![추가된 CNAME 레코드](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="eba4f-150">이제 Azure 앱에서 사용자 지정 DNS 이름을 사용할 수 있도록 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-the-active-dns-name"></a><span data-ttu-id="eba4f-151">활성 DNS 이름 다시 매핑</span><span class="sxs-lookup"><span data-stu-id="eba4f-151">Remap the active DNS name</span></span>

<span data-ttu-id="eba4f-152">남아 있는 유일한 작업은 활성 DNS 레코드가 App Service를 가리키도록 다시 매핑하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-152">The only thing left to do is remapping your active DNS record to point to App Service.</span></span> <span data-ttu-id="eba4f-153">현재는 여전히 이전 사이트를 가리키고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-153">Right now, it still points to your old site.</span></span>

<a name="info"></a>

### <a name="copy-the-apps-ip-address-a-record-only"></a><span data-ttu-id="eba4f-154">앱의 IP 주소 복사(A 레코드만 해당)</span><span class="sxs-lookup"><span data-stu-id="eba4f-154">Copy the app's IP address (A record only)</span></span>

<span data-ttu-id="eba4f-155">CNAME 레코드를 다시 매핑하는 경우 이 섹션을 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="eba4f-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="eba4f-156">A 레코드를 다시 매핑하려면 **사용자 지정 도메인** 페이지에 표시되는 App Service 앱의 외부 IP 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-156">To remap an A record, you need the App Service app's external IP address, which is shown in the **Custom domains** page.</span></span>

<span data-ttu-id="eba4f-157">오른쪽 상단 모서리에서 **X**를 선택하여 **호스트 이름 추가** 페이지를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-157">Close the **Add hostname** page by selecting **X** in the upper-right corner.</span></span> 

<span data-ttu-id="eba4f-158">**사용자 지정 도메인** 페이지에서 앱의 IP 주소를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-158">In the **Custom domains** page, copy the app's IP address.</span></span>

![Azure 앱에 대한 포털 탐색](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-the-dns-record"></a><span data-ttu-id="eba4f-160">DNS 레코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="eba4f-160">Update the DNS record</span></span>

<span data-ttu-id="eba4f-161">다시 도메인 공급자의 DNS 레코드 페이지에서 다시 매핑할 DNS 레코드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-161">Back in the DNS records page of your domain provider, select the DNS record to remap.</span></span>

<span data-ttu-id="eba4f-162">`contoso.com` 루트 도메인 예제의 경우 다음 표의 예제와 같은 A 또는 CNAME 레코드를 다시 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-162">For the `contoso.com` root domain example, remap the A or CNAME record like the examples in the following table:</span></span> 

| <span data-ttu-id="eba4f-163">FQDN 예</span><span class="sxs-lookup"><span data-stu-id="eba4f-163">FQDN example</span></span> | <span data-ttu-id="eba4f-164">레코드 형식</span><span class="sxs-lookup"><span data-stu-id="eba4f-164">Record type</span></span> | <span data-ttu-id="eba4f-165">호스트</span><span class="sxs-lookup"><span data-stu-id="eba4f-165">Host</span></span> | <span data-ttu-id="eba4f-166">값</span><span class="sxs-lookup"><span data-stu-id="eba4f-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="eba4f-167">contoso.com(루트)</span><span class="sxs-lookup"><span data-stu-id="eba4f-167">contoso.com (root)</span></span> | <span data-ttu-id="eba4f-168">A</span><span class="sxs-lookup"><span data-stu-id="eba4f-168">A</span></span> | `@` | <span data-ttu-id="eba4f-169">[앱의 IP 주소 복사](#info)에서 가져온 IP 주소</span><span class="sxs-lookup"><span data-stu-id="eba4f-169">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="eba4f-170">www.contoso.com(하위)</span><span class="sxs-lookup"><span data-stu-id="eba4f-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="eba4f-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="eba4f-171">CNAME</span></span> | `www` | <span data-ttu-id="eba4f-172">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="eba4f-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="eba4f-173">\*.contoso.com(와일드카드)</span><span class="sxs-lookup"><span data-stu-id="eba4f-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="eba4f-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="eba4f-174">CNAME</span></span> | _\*_ | <span data-ttu-id="eba4f-175">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="eba4f-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="eba4f-176">설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-176">Save your settings.</span></span>

<span data-ttu-id="eba4f-177">DNS 쿼리는 DNS가 전파된 직후 App Service 앱에 대해 확인을 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-177">DNS queries should start resolving to your App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eba4f-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eba4f-178">Next steps</span></span>

<span data-ttu-id="eba4f-179">사용자 지정 SSL 인증서를 App Service에 바인딩하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="eba4f-179">Learn how to bind a custom SSL certificate to App Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eba4f-180">Azure Web Apps에 기존 사용자 지정 SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="eba4f-180">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
