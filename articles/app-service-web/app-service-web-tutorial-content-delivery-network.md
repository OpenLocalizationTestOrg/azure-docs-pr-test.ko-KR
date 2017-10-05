---
title: "Azure App Service에 CDN 추가 | Microsoft Docs"
description: "Azure App Service에 CDN(Content Delivery Network) 추가하여 전 세계의 고객에게 가까운 서버에서 정적 파일을 캐시하고 제공합니다."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 257b75d01f3904661c1a188a2d53ffcb74f48f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-content-delivery-network-cdn-to-an-azure-app-service"></a><span data-ttu-id="0cc3c-103">Azure App Service에 CDN(Content Delivery Network) 추가</span><span class="sxs-lookup"><span data-stu-id="0cc3c-103">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>

<span data-ttu-id="0cc3c-104">[Azure CDN(Content Delivery Network)](../cdn/cdn-overview.md)은 전략적으로 배치된 위치에서 정적 웹 콘텐츠를 캐싱하여 사용자에게 콘텐츠를 배달하기 위한 최대 처리량을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users.</span></span> <span data-ttu-id="0cc3c-105">또한 CDN은 웹앱에 대한 서버 부하를 감소시킵니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-105">The CDN also decreases server load on your web app.</span></span> <span data-ttu-id="0cc3c-106">이 자습서에서는 Azure CDN을 [Azure App Service의 웹앱](app-service-web-overview.md)에 추가하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-106">This tutorial shows how to add Azure CDN to a [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="0cc3c-107">사용하게 될 샘플 정적 HTML 사이트의 홈 페이지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-107">Here's the home page of the sample static HTML site that you'll work with:</span></span>

![샘플 앱 홈 페이지](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="0cc3c-109">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="0cc3c-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0cc3c-110">CDN 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="0cc3c-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="0cc3c-111">캐시된 자산 새로 고침</span><span class="sxs-lookup"><span data-stu-id="0cc3c-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="0cc3c-112">쿼리 문자열을 사용하여 캐시된 버전 제어</span><span class="sxs-lookup"><span data-stu-id="0cc3c-112">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="0cc3c-113">CDN 끝점에 사용자 지정 도메인 사용</span><span class="sxs-lookup"><span data-stu-id="0cc3c-113">Use a custom domain for the CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0cc3c-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0cc3c-114">Prerequisites</span></span>

<span data-ttu-id="0cc3c-115">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-115">To complete this tutorial:</span></span>

- [<span data-ttu-id="0cc3c-116">Git 설치</span><span class="sxs-lookup"><span data-stu-id="0cc3c-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="0cc3c-117">Azure CLI 2.0 설치</span><span class="sxs-lookup"><span data-stu-id="0cc3c-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-web-app"></a><span data-ttu-id="0cc3c-118">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="0cc3c-118">Create the web app</span></span>

<span data-ttu-id="0cc3c-119">사용할 웹앱을 만들려면 **앱 찾아보기** 단계를 통해 [정적 HTML 빠른 시작](app-service-web-get-started-html.md)을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-119">To create the web app that you'll work with, follow the [static HTML quickstart](app-service-web-get-started-html.md) through the **Browse to the app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="0cc3c-120">사용자 지정 도메인 준비</span><span class="sxs-lookup"><span data-stu-id="0cc3c-120">Have a custom domain ready</span></span>

<span data-ttu-id="0cc3c-121">이 자습서의 사용자 지정 도메인 단계를 완료하려면 사용자 지정 도메인을 소유하고 도메인 공급자(예: GoDaddy)의 DNS 레지스트리에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-121">To complete the custom domain step of this tutorial, you need to own a custom domain and have access to your DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="0cc3c-122">예를 들어 `contoso.com` 및 `www.contoso.com`에 대한 DNS 항목을 추가하려면 `contoso.com` 루트 도메인에 대한 DNS 설정을 구성할 수 있는 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-122">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must have access to configure the DNS settings for the `contoso.com` root domain.</span></span>

<span data-ttu-id="0cc3c-123">아직 도메인 이름이 없는 경우 Azure Portal을 사용하여 도메인을 구매하려면 [App Service 도메인 자습서](custom-dns-web-site-buydomains-web-app.md)를 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-123">If you don't already have a domain name, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="0cc3c-124">Azure 포털에 로그인</span><span class="sxs-lookup"><span data-stu-id="0cc3c-124">Log in to the Azure portal</span></span>

<span data-ttu-id="0cc3c-125">브라우저를 열고 [Azure Portal](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-125">Open a browser and navigate to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="0cc3c-126">CDN 프로필 및 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="0cc3c-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="0cc3c-127">왼쪽 탐색 영역에서 **App Services**를 선택한 다음 [정적 HTML 빠른 시작](app-service-web-get-started-html.md)에서 만든 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-127">In the left navigation, select **App Services**, and then select the app that you created in the [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![포털에서 App Service 앱 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="0cc3c-129">**App Service** 페이지의 **설정** 섹션에서 **네트워킹 > 앱에서 Azure CDN 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-129">In the **App Service** page, in the **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![포털에서 CDN 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="0cc3c-131">**Azure Content Delivery Network** 페이지에서 테이블에 지정된 대로 **새 끝점** 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-131">In the **Azure Content Delivery Network** page, provide the **New endpoint** settings as specified in the table.</span></span>

![포털에서 프로필 및 끝점 만들기](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="0cc3c-133">설정</span><span class="sxs-lookup"><span data-stu-id="0cc3c-133">Setting</span></span> | <span data-ttu-id="0cc3c-134">제안 값</span><span class="sxs-lookup"><span data-stu-id="0cc3c-134">Suggested value</span></span> | <span data-ttu-id="0cc3c-135">설명</span><span class="sxs-lookup"><span data-stu-id="0cc3c-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="0cc3c-136">**CDN 프로필**</span><span class="sxs-lookup"><span data-stu-id="0cc3c-136">**CDN profile**</span></span> | <span data-ttu-id="0cc3c-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="0cc3c-137">myCDNProfile</span></span> | <span data-ttu-id="0cc3c-138">**새로 만들기**를 선택하여 CDN 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-138">Select **Create new** to create a CDN profile.</span></span> <span data-ttu-id="0cc3c-139">CDN 프로필은 동일한 가격 책정 계층을 가진 CDN 끝점의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-139">A CDN profile is a collection of CDN endpoints with the same pricing tier.</span></span> |
| <span data-ttu-id="0cc3c-140">**가격 책정 계층**</span><span class="sxs-lookup"><span data-stu-id="0cc3c-140">**Pricing tier**</span></span> | <span data-ttu-id="0cc3c-141">Standard Akamai</span><span class="sxs-lookup"><span data-stu-id="0cc3c-141">Standard Akamai</span></span> | <span data-ttu-id="0cc3c-142">[가격 책정 계층](../cdn/cdn-overview.md#azure-cdn-features)은 공급자 및 사용 가능한 기능을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-142">The [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies the provider and available features.</span></span> <span data-ttu-id="0cc3c-143">이 자습서에서는 표준 Akamai를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="0cc3c-144">**CDN 끝점 이름**</span><span class="sxs-lookup"><span data-stu-id="0cc3c-144">**CDN endpoint name**</span></span> | <span data-ttu-id="0cc3c-145">azureedge.net 도메인에서 고유한 이름</span><span class="sxs-lookup"><span data-stu-id="0cc3c-145">Any name that is unique in the azureedge.net domain</span></span> | <span data-ttu-id="0cc3c-146">도메인인 *\<endpointname>.azureedge.net*에서 캐시된 리소스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-146">You access your cached resources at the domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="0cc3c-147">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-147">Select **Create**.</span></span>

<span data-ttu-id="0cc3c-148">Azure에서는 프로필 및 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-148">Azure creates the profile and endpoint.</span></span> <span data-ttu-id="0cc3c-149">새 끝점은 동일한 페이지의 **끝점** 목록에서 표시되고 프로비전될 때 상태가 **실행 중**입니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-149">The new endpoint appears in the **Endpoints** list on the same page, and when it's provisioned the status is **Running**.</span></span>

![목록의 새 끝점](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-the-cdn-endpoint"></a><span data-ttu-id="0cc3c-151">CDN 끝점 테스트</span><span class="sxs-lookup"><span data-stu-id="0cc3c-151">Test the CDN endpoint</span></span>

<span data-ttu-id="0cc3c-152">Verizon 가격 책정 계층을 선택한 경우 끝점 전파를 위해 일반적으로 약 90분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="0cc3c-153">Akamai의 경우 전파하는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="0cc3c-154">샘플 앱에는 `index.html` 파일 및 다른 정적 자산을 포함하는 *css*, *img* 및 *js* 폴더가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-154">The sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="0cc3c-155">이러한 파일에 대한 콘텐츠 경로는 CDN 끝점과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-155">The content paths for all of these files are the same at the CDN endpoint.</span></span> <span data-ttu-id="0cc3c-156">예를 들어 다음 URL은 모두 *css* 폴더의 *bootstrap.css* 파일에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-156">For example, both of the following URLs access the *bootstrap.css* file in the *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="0cc3c-157">브라우저를 다음 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-157">Navigate a browser to the following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![CDN에서 제공되는 샘플 앱 홈 페이지](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="0cc3c-159">Azure 웹앱에서 이전에 실행한 것과 동일한 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-159">You see the same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="0cc3c-160">Azure CDN에서 원본 웹앱의 자산을 검색하고 CDN 끝점에서 제공하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-160">Azure CDN has retrieved the origin web app's assets and is serving them from the CDN endpoint</span></span>

<span data-ttu-id="0cc3c-161">이 페이지가 CDN에서 캐시된다는 것을 보장하기 위해 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-161">To ensure that this page is cached in the CDN, refresh the page.</span></span> <span data-ttu-id="0cc3c-162">동일한 자산에 대한 두 개의 요청에서 CDN은 요청된 콘텐츠를 캐시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-162">Two requests for the same asset are sometimes required for the CDN to cache the requested content.</span></span>

<span data-ttu-id="0cc3c-163">Azure CDN 프로필 및 끝점을 만드는 방법에 대한 자세한 내용은 [Azure CDN 시작](../cdn/cdn-create-new-endpoint.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-the-cdn"></a><span data-ttu-id="0cc3c-164">CDN 제거</span><span class="sxs-lookup"><span data-stu-id="0cc3c-164">Purge the CDN</span></span>

<span data-ttu-id="0cc3c-165">CDN은 TTL(time-to-live) 구성을 기반으로 원본 웹앱의 자원을 주기적으로 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-165">The CDN periodically refreshes its resources from the origin web app based on the time-to-live (TTL) configuration.</span></span> <span data-ttu-id="0cc3c-166">기본 TTL은 7일입니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-166">The default TTL is seven days.</span></span>

<span data-ttu-id="0cc3c-167">예를 들어 때때로 웹앱에 업데이트된 콘텐츠를 배포할 때 TTL이 만료되기 전에 CDN을 새로 고쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-167">At times you might need to refresh the CDN before the TTL expiration -- for example, when you deploy updated content to the web app.</span></span> <span data-ttu-id="0cc3c-168">새로 고침을 트리거하기 위해 CDN 리소스를 수동으로 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-168">To trigger a refresh, you can manually purge the CDN resources.</span></span> 

<span data-ttu-id="0cc3c-169">자습서의 이 섹션에서는 웹앱에 대한 변경 내용을 배포하고 CDN을 삭제하여 캐시를 새로 고치기 위해 CDN을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-169">In this section of the tutorial, you deploy a change to the web app and purge the CDN to trigger the CDN to refresh its cache.</span></span>

### <a name="deploy-a-change-to-the-web-app"></a><span data-ttu-id="0cc3c-170">웹앱에 대한 변경 내용 배포</span><span class="sxs-lookup"><span data-stu-id="0cc3c-170">Deploy a change to the web app</span></span>

<span data-ttu-id="0cc3c-171">다음 예제와 같이 `index.html` 파일을 열고 "-V2"를 H1 제목에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-171">Open the `index.html` file and add "- V2" to the H1 heading, as shown in the following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="0cc3c-172">변경 내용을 커밋하고 웹앱에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-172">Commit your change and deploy it to the web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="0cc3c-173">배포가 완료되면 웹앱 URL을 찾아 변경 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-173">Once deployment has completed, browse to the web app URL and you see the change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![웹앱의 제목에서 V2](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="0cc3c-175">홈 페이지의 CDN 끝점 URL로 이동하더라도 CDN에서 캐시된 버전이 아직 만료되지 않았기 때문에 변경 내용을 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-175">Browse to the CDN endpoint URL for the home page and you don't see the change because the cached version in the CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![CDN의 제목에서 V2 없음](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-the-cdn-in-the-portal"></a><span data-ttu-id="0cc3c-177">포털에서 CDN 제거</span><span class="sxs-lookup"><span data-stu-id="0cc3c-177">Purge the CDN in the portal</span></span>

<span data-ttu-id="0cc3c-178">CDN을 트리거하여 캐시된 버전을 업데이트하려면 CDN을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-178">To trigger the CDN to update its cached version, purge the CDN.</span></span>

<span data-ttu-id="0cc3c-179">포털 왼쪽 탐색 영역에서 **리소스 그룹**을 선택한 다음 웹앱(myResourceGroup)에 만든 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-179">In the portal left navigation, select **Resource groups**, and then select the resource group that you created for your web app (myResourceGroup).</span></span>

![리소스 그룹 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="0cc3c-181">리소스의 목록에서 CDN 끝점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-181">In the list of resources, select your CDN endpoint.</span></span>

![끝점 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="0cc3c-183">**끝점** 페이지의 맨 위에서 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-183">At the top of the **Endpoint** page, click **Purge**.</span></span>

![제거 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="0cc3c-185">제거하려는 콘텐츠 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-185">Enter the content paths you wish to purge.</span></span> <span data-ttu-id="0cc3c-186">전체 파일 경로를 전달하여 개별 파일을 제거하거나 경로 세그먼트를 전달하여 폴더에서 모든 콘텐츠를 제거하고 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-186">You can pass a complete file path to purge an individual file, or a path segment to purge and refresh all content in a folder.</span></span> <span data-ttu-id="0cc3c-187">`index.html`을 변경했으므로 경로 중 하나인지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-187">Since you changed `index.html`, make sure that is one of the paths.</span></span>

<span data-ttu-id="0cc3c-188">페이지 맨 아래에서 **제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-188">At the bottom of the page, select **Purge**.</span></span>

![페이지 제거](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-the-cdn-is-updated"></a><span data-ttu-id="0cc3c-190">CDN이 업데이트되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="0cc3c-190">Verify that the CDN is updated</span></span>

<span data-ttu-id="0cc3c-191">제거 요청 처리가 완료될 때까지 일반적으로 몇 분 정도를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-191">Wait until the purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="0cc3c-192">현재 상태를 보려면 페이지 맨 아래에 있는 벨 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-192">To see the current status, select the bell icon at the top of the page.</span></span> 

![제거 알림](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="0cc3c-194">`index.html`에 대한 CDN 끝점 URL로 이동하면 이제 홈 페이지에서 제목에 추가한 V2가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-194">Browse to the CDN endpoint URL for `index.html`, and now you see the V2 that you added to the title on the home page.</span></span> <span data-ttu-id="0cc3c-195">CDN 캐시를 새로 고쳤다는 것을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-195">This shows that the CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![CDN의 제목에서 V2](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="0cc3c-197">자세한 내용은 [Azure CDN 끝점 제거](../cdn/cdn-purge-endpoint.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-to-version-content"></a><span data-ttu-id="0cc3c-198">버전 콘텐츠에 쿼리 문자열 사용</span><span class="sxs-lookup"><span data-stu-id="0cc3c-198">Use query strings to version content</span></span>

<span data-ttu-id="0cc3c-199">Azure CDN은 다음과 같은 캐싱 동작 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-199">The Azure CDN offers the following caching behavior options:</span></span>

* <span data-ttu-id="0cc3c-200">쿼리 문자열 무시</span><span class="sxs-lookup"><span data-stu-id="0cc3c-200">Ignore query strings</span></span>
* <span data-ttu-id="0cc3c-201">쿼리 문자열에 대한 캐싱 우회</span><span class="sxs-lookup"><span data-stu-id="0cc3c-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="0cc3c-202">모든 고유한 URL 캐시</span><span class="sxs-lookup"><span data-stu-id="0cc3c-202">Cache every unique URL</span></span> 

<span data-ttu-id="0cc3c-203">이 중 첫 번째 옵션이 기본값입니다. 즉 액세스하는 URL의 쿼리 문자열에 관계없이 캐시된 자산의 버전이 하나뿐임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-203">The first of these is the default, which means there is only one cached version of an asset regardless of the query string in the URL.</span></span> 

<span data-ttu-id="0cc3c-204">자습서의 이 섹션에서는 캐싱 동작을 변경하여 고유한 URL을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-204">In this section of the tutorial, you change the caching behavior to cache every unique URL.</span></span>

### <a name="change-the-cache-behavior"></a><span data-ttu-id="0cc3c-205">캐시 동작 변경</span><span class="sxs-lookup"><span data-stu-id="0cc3c-205">Change the cache behavior</span></span>

<span data-ttu-id="0cc3c-206">Azure Portal의 **CDN 끝점** 페이지에서 **캐시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-206">In the Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="0cc3c-207">**쿼리 문자열 캐싱 동작** 드롭다운 목록에서 **모든 고유한 URL 캐시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-207">Select **Cache every unique URL** from the **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="0cc3c-208">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-208">Select **Save**.</span></span>

![쿼리 문자열 캐싱 동작 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="0cc3c-210">고유 URL을 별도로 캐시했는지 확인</span><span class="sxs-lookup"><span data-stu-id="0cc3c-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="0cc3c-211">브라우저의 CDN 끝점에서 홈 페이지로 이동하지만 쿼리 문자열을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-211">In a browser, navigate to the home page at the CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="0cc3c-212">CDN은 제목에 "V2"를 포함하는 현재 웹앱 콘텐츠를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-212">The CDN returns the current web app content, which includes "V2" in the heading.</span></span> 

<span data-ttu-id="0cc3c-213">이 페이지가 CDN에서 캐시된다는 것을 보장하기 위해 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-213">To ensure that this page is cached in the CDN, refresh the page.</span></span> 

<span data-ttu-id="0cc3c-214">`index.html`을 열고 "V2" "V3"으로 바꾸고 변경 내용을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-214">Open `index.html` and change "V2" to "V3", and deploy the change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="0cc3c-215">브라우저에서 `q=2`과 같은 새 쿼리 문자열이 있는 CDN 끝점 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-215">In a browser, go to the CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="0cc3c-216">CDN은 현재 `index.html` 파일을 가져오고 "V3"를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-216">The CDN gets the current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="0cc3c-217">그러나 `q=1` 쿼리 문자열을 사용하여 CDN 끝점으로 이동하는 경우 "V2"를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-217">But if you navigate to the CDN endpoint with the `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![CDN에서 제목에 V3, 쿼리 문자열 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![CDN에서 제목에 V2, 쿼리 문자열 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="0cc3c-220">이 출력에서는 각 쿼리 문자열이 다르게 처리됨을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="0cc3c-221">이전에는 q=1이 사용되어 캐시된 내용(V2)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="0cc3c-222">q=2는 새로운 쿼리 문자열이므로 최신 웹앱 내용(V3)을 검색하여 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-222">q=2 is new, so the latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="0cc3c-223">자세한 내용은 [쿼리 문자열을 사용하여 Azure CDN 캐싱 동작 제어](../cdn/cdn-query-string.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-to-a-cdn-endpoint"></a><span data-ttu-id="0cc3c-224">CDN 끝점에 사용자 지정 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="0cc3c-224">Map a custom domain to a CDN endpoint</span></span>

<span data-ttu-id="0cc3c-225">CNAME 레코드를 만들어서 CDN 끝점에 사용자 지정 도메인을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-225">You'll map your custom domain to your CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="0cc3c-226">CNAME 레코드는 원본 도메인을 대상 도메인에 매핑하는 DNS 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-226">A CNAME record is a DNS feature that maps a source domain to a destination domain.</span></span> <span data-ttu-id="0cc3c-227">예를 들어 `cdn.contoso.com` 또는 `static.contoso.com`를 `contoso.azureedge.net`에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` to `contoso.azureedge.net`.</span></span>

<span data-ttu-id="0cc3c-228">사용자 지정 도메인이 없는 경우 Azure Portal을 사용하여 도메인을 구매하려면 [App Service 도메인 자습서](custom-dns-web-site-buydomains-web-app.md)를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-228">If you don't have a custom domain, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

### <a name="find-the-hostname-to-use-with-the-cname"></a><span data-ttu-id="0cc3c-229">CNAME을 사용하여 호스트 이름 찾기</span><span class="sxs-lookup"><span data-stu-id="0cc3c-229">Find the hostname to use with the CNAME</span></span>

<span data-ttu-id="0cc3c-230">Azure Portal의 **끝점** 페이지에 있는 왼쪽 탐색 영역에서 **개요**를 선택한 다음 페이지 맨 위에 있는 **+ 사용자 지정 도메인** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-230">In the Azure portal **Endpoint** page, make sure **Overview** is selected in the left navigation, and then select the **+ Custom Domain** button at the top of the page.</span></span>

![사용자 지정 도메인 추가 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="0cc3c-232">**사용자 지정 도메인 추가** 페이지에서 CNAME 레코드를 만드는 데 사용할 끝점 호스트 이름을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-232">In the **Add a custom domain** page, you see the endpoint host name to use in creating a CNAME record.</span></span> <span data-ttu-id="0cc3c-233">호스트 이름은 CDN 끝점 URL인 **&lt;EndpointName>.azureedge.net**에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-233">The host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![도메인 페이지 추가](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-the-cname-with-your-domain-registrar"></a><span data-ttu-id="0cc3c-235">도메인 등록 기관과 함께 CNAME 구성</span><span class="sxs-lookup"><span data-stu-id="0cc3c-235">Configure the CNAME with your domain registrar</span></span>

<span data-ttu-id="0cc3c-236">도메인 등록 기관의 웹 사이트로 이동한 다음 DNS 레코드를 만들기 위한 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-236">Navigate to your domain registrar's web site, and locate the section for creating DNS records.</span></span> <span data-ttu-id="0cc3c-237">**도메인 이름**, **DNS** 또는 **이름 서버 관리**와 같은 섹션에서 이를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="0cc3c-238">CNAME을 관리하기 위한 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-238">Find the section for managing CNAMEs.</span></span> <span data-ttu-id="0cc3c-239">고급 설정 페이지로 이동하여 CNAME, 별칭 또는 하위 도메인과 같은 단어를 찾아야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-239">You may have to go to an advanced settings page and look for the words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="0cc3c-240">선택한 하위 도메인(예: **static** 또는 **cdn**)을 포털에서 이전에 표시한 **끝점 호스트 이름**에 매핑하는 CNAME 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) to the **Endpoint host name** shown earlier in the portal.</span></span> 

### <a name="enter-the-custom-domain-in-azure"></a><span data-ttu-id="0cc3c-241">Azure에서 사용자 지정 도메인 입력</span><span class="sxs-lookup"><span data-stu-id="0cc3c-241">Enter the custom domain in Azure</span></span>

<span data-ttu-id="0cc3c-242">**사용자 지정 도메인 추가** 페이지로 돌아가 하위 도메인을 포함하는 사용자 지정 도메인을 대화 상자에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-242">Return to the **Add a custom domain** page, and enter your custom domain, including the subdomain, in the dialog box.</span></span> <span data-ttu-id="0cc3c-243">예를 들어 `cdn.contoso.com`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="0cc3c-244">Azure에서 입력한 도메인 이름에 대한 CNAME 레코드가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-244">Azure verifies that the CNAME record exists for the domain name you have entered.</span></span> <span data-ttu-id="0cc3c-245">CNAME이 올바르면 사용자 지정 도메인의 유효성이 검사됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-245">If the CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="0cc3c-246">CNAME 레코드가 인터넷의 이름 서버로 전파되는 데 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-246">It can take time for the CNAME record to propagate to name servers on the Internet.</span></span> <span data-ttu-id="0cc3c-247">도메인의 유효성이 바로 검사되지 않으면 몇 분 후에 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-the-custom-domain"></a><span data-ttu-id="0cc3c-248">사용자 지정 도메인 테스트</span><span class="sxs-lookup"><span data-stu-id="0cc3c-248">Test the custom domain</span></span>

<span data-ttu-id="0cc3c-249">브라우저에서 사용자 지정 도메인을 사용하여 `index.html` 파일로 이동(예: `cdn.contoso.com/index.html`)하여 결과가 직접 `<endpointname>azureedge.net/index.html`으로 이동할 경우와 동일한지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-249">In a browser, navigate to the `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) to verify that the result is the same as when you go directly to `<endpointname>azureedge.net/index.html`.</span></span>

![사용자 지정 도메인 URL을 사용하는 샘플 앱 홈 페이지](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="0cc3c-251">자세한 내용은 [사용자 지정 도메인에 Azure CDN 컨텐츠 매핑](../cdn/cdn-map-content-to-custom-domain.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-251">For more information, see [Map Azure CDN content to a custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="0cc3c-252">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0cc3c-252">Next steps</span></span>

<span data-ttu-id="0cc3c-253">학습한 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0cc3c-254">CDN 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="0cc3c-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="0cc3c-255">캐시된 자산 새로 고침</span><span class="sxs-lookup"><span data-stu-id="0cc3c-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="0cc3c-256">쿼리 문자열을 사용하여 캐시된 버전 제어</span><span class="sxs-lookup"><span data-stu-id="0cc3c-256">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="0cc3c-257">CDN 끝점에 사용자 지정 도메인 사용</span><span class="sxs-lookup"><span data-stu-id="0cc3c-257">Use a custom domain for the CDN endpoint.</span></span>

<span data-ttu-id="0cc3c-258">다음 문서에서 CDN 성능을 최적화하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0cc3c-258">Learn how to optimize CDN performance in the following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0cc3c-259">Azure CDN에서 파일을 압축하여 성능 향상</span><span class="sxs-lookup"><span data-stu-id="0cc3c-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="0cc3c-260">Azure CDN 끝점에 자산 미리 로드</span><span class="sxs-lookup"><span data-stu-id="0cc3c-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
