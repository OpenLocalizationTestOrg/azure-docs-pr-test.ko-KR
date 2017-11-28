---
title: "CDN tooan Azure 앱 서비스 aaaAdd | Microsoft Docs"
description: "네트워크 CDN (콘텐츠 배달) tooan Azure 앱 서비스 toocache를 추가 하 고 hello 전 세계 닫기 tooyour 고객 서버에서 정적 파일을 제공 합니다."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a><span data-ttu-id="61260-103">추가 네트워크 CDN (콘텐츠 배달) tooan Azure 앱 서비스</span><span class="sxs-lookup"><span data-stu-id="61260-103">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>

<span data-ttu-id="61260-104">[Azure 네트워크 CDN (콘텐츠 배달)](../cdn/cdn-overview.md) 전략적으로 배치 된 위치 tooprovide 최대 처리량 toousers 콘텐츠를 제공 하기 위한 정적 웹 콘텐츠를 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations tooprovide maximum throughput for delivering content toousers.</span></span> <span data-ttu-id="61260-105">hello CDN은 웹 응용 프로그램에 서버 부하를 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="61260-105">hello CDN also decreases server load on your web app.</span></span> <span data-ttu-id="61260-106">이 자습서에서는 어떻게 tooadd Azure CDN tooa [Azure 앱 서비스의 웹 앱](app-service-web-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-106">This tutorial shows how tooadd Azure CDN tooa [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="61260-107">Hello 사이트의 홈 페이지 hello 샘플 정적 HTML 사용 하는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="61260-107">Here's hello home page of hello sample static HTML site that you'll work with:</span></span>

![샘플 앱 홈 페이지](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="61260-109">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="61260-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="61260-110">CDN 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="61260-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="61260-111">캐시된 자산 새로 고침</span><span class="sxs-lookup"><span data-stu-id="61260-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="61260-112">사용 하 여 쿼리 문자열 캐시 toocontrol 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="61260-112">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="61260-113">Hello CDN 끝점에 대 한 사용자 지정 도메인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-113">Use a custom domain for hello CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61260-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="61260-114">Prerequisites</span></span>

<span data-ttu-id="61260-115">toocomplete이이 자습서:</span><span class="sxs-lookup"><span data-stu-id="61260-115">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="61260-116">Git 설치</span><span class="sxs-lookup"><span data-stu-id="61260-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="61260-117">Azure CLI 2.0 설치</span><span class="sxs-lookup"><span data-stu-id="61260-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a><span data-ttu-id="61260-118">Hello 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="61260-118">Create hello web app</span></span>

<span data-ttu-id="61260-119">사용 합니다, 따라 hello toocreate hello 웹 앱 [정적 HTML 퀵 스타트](app-service-web-get-started-html.md) hello를 통해 **찾아보기 toohello 앱** 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="61260-119">toocreate hello web app that you'll work with, follow hello [static HTML quickstart](app-service-web-get-started-html.md) through hello **Browse toohello app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="61260-120">사용자 지정 도메인 준비</span><span class="sxs-lookup"><span data-stu-id="61260-120">Have a custom domain ready</span></span>

<span data-ttu-id="61260-121">toocomplete hello 사용자 지정 도메인 단계가이 자습서의 사용자 지정 도메인 tooown 필요 하 고이 도메인 공급자 (예: GoDaddy)에 대 한 액세스 tooyour DNS 레지스트리는 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-121">toocomplete hello custom domain step of this tutorial, you need tooown a custom domain and have access tooyour DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="61260-122">에 대 한 DNS 항목 예를 들어 tooadd `contoso.com` 및 `www.contoso.com`, hello에 대 한 액세스 tooconfigure hello DNS 설정이 있어야 `contoso.com` 루트 도메인.</span><span class="sxs-lookup"><span data-stu-id="61260-122">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must have access tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

<span data-ttu-id="61260-123">도메인 이름이 없는 경우 다음과 같은 hello [앱 서비스 도메인 자습서](custom-dns-web-site-buydomains-web-app.md) 사용 하 여 도메인 toopurchase hello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="61260-123">If you don't already have a domain name, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="61260-124">Azure 포털 toohello에 로그인</span><span class="sxs-lookup"><span data-stu-id="61260-124">Log in toohello Azure portal</span></span>

<span data-ttu-id="61260-125">브라우저를 열고 탐색 toohello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-125">Open a browser and navigate toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="61260-126">CDN 프로필 및 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="61260-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="61260-127">왼쪽 탐색 hello, 선택 **응용 프로그램 서비스**, 다음 hello에서 만든 hello 앱을 선택 하 고 [정적 HTML 퀵 스타트](app-service-web-get-started-html.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-127">In hello left navigation, select **App Services**, and then select hello app that you created in hello [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![Hello 포털에서 앱 서비스 앱 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="61260-129">Hello에 **앱 서비스** 페이지 hello에서 **설정** 섹션에서 **네트워킹 > 응용 프로그램에 대 한 Azure CDN 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-129">In hello **App Service** page, in hello **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![Hello 포털에서 CDN을 선택 합니다.](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="61260-131">Hello에 **Azure 콘텐츠 배달 네트워크** 페이지를 hello 제공 **새 끝점** hello 테이블에 지정 된 대로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-131">In hello **Azure Content Delivery Network** page, provide hello **New endpoint** settings as specified in hello table.</span></span>

![Hello 포털에서 프로필 및 끝점 만들기](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="61260-133">설정</span><span class="sxs-lookup"><span data-stu-id="61260-133">Setting</span></span> | <span data-ttu-id="61260-134">제안 값</span><span class="sxs-lookup"><span data-stu-id="61260-134">Suggested value</span></span> | <span data-ttu-id="61260-135">설명</span><span class="sxs-lookup"><span data-stu-id="61260-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="61260-136">**CDN 프로필**</span><span class="sxs-lookup"><span data-stu-id="61260-136">**CDN profile**</span></span> | <span data-ttu-id="61260-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="61260-137">myCDNProfile</span></span> | <span data-ttu-id="61260-138">선택 **새로 만들기** toocreate CDN 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="61260-138">Select **Create new** toocreate a CDN profile.</span></span> <span data-ttu-id="61260-139">CDN 프로필 hello로 CDN 끝점의 컬렉션은 같은 가격 책정 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="61260-139">A CDN profile is a collection of CDN endpoints with hello same pricing tier.</span></span> |
| <span data-ttu-id="61260-140">**가격 책정 계층**</span><span class="sxs-lookup"><span data-stu-id="61260-140">**Pricing tier**</span></span> | <span data-ttu-id="61260-141">Standard Akamai</span><span class="sxs-lookup"><span data-stu-id="61260-141">Standard Akamai</span></span> | <span data-ttu-id="61260-142">hello [가격 책정 계층](../cdn/cdn-overview.md#azure-cdn-features) hello 공급자 및 사용 가능한 기능을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-142">hello [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies hello provider and available features.</span></span> <span data-ttu-id="61260-143">이 자습서에서는 표준 Akamai를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="61260-144">**CDN 끝점 이름**</span><span class="sxs-lookup"><span data-stu-id="61260-144">**CDN endpoint name**</span></span> | <span data-ttu-id="61260-145">Hello azureedge.net 도메인에서 고유한 이름</span><span class="sxs-lookup"><span data-stu-id="61260-145">Any name that is unique in hello azureedge.net domain</span></span> | <span data-ttu-id="61260-146">Hello 도메인에서 캐시 된 리소스에 액세스 하면  *\<endpointname >. azureedge.net*합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-146">You access your cached resources at hello domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="61260-147">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-147">Select **Create**.</span></span>

<span data-ttu-id="61260-148">Azure는 hello 프로필 및 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="61260-148">Azure creates hello profile and endpoint.</span></span> <span data-ttu-id="61260-149">hello에 새 끝점의 hello 표시 **끝점** 목록에서 같은 페이지 hello 그리고 hello 상태가 프로 비전 될 때 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-149">hello new endpoint appears in hello **Endpoints** list on hello same page, and when it's provisioned hello status is **Running**.</span></span>

![목록의 새 끝점](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="61260-151">테스트 hello CDN 끝점</span><span class="sxs-lookup"><span data-stu-id="61260-151">Test hello CDN endpoint</span></span>

<span data-ttu-id="61260-152">Verizon 가격 책정 계층을 선택한 경우 끝점 전파를 위해 일반적으로 약 90분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="61260-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="61260-153">Akamai의 경우 전파하는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="61260-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="61260-154">hello 샘플 응용 프로그램에는 `index.html` 파일 및 *css*, *img*, 및 *js* 다른 정적 자산을 포함 하는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="61260-154">hello sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="61260-155">이 모든 파일에 대 한 경로 콘텐츠 hello hello CDN 끝점에서 동일한 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-155">hello content paths for all of these files are hello same at hello CDN endpoint.</span></span> <span data-ttu-id="61260-156">예를 들어 hello 다음 Url의 액세스 hello *bootstrap.css* hello에 대 한 파일 *css* 폴더:</span><span class="sxs-lookup"><span data-stu-id="61260-156">For example, both of hello following URLs access hello *bootstrap.css* file in hello *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="61260-157">Url 브라우저 toohello를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-157">Navigate a browser toohello following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![CDN에서 제공되는 샘플 앱 홈 페이지](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="61260-159">Hello Azure 웹 앱의 앞부분에 나오는 실행 하는 동일한 페이지를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-159">You see hello same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="61260-160">Azure CDN이 hello 원본 웹 앱의 자산을 검색 하 고 hello CDN 끝점에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61260-160">Azure CDN has retrieved hello origin web app's assets and is serving them from hello CDN endpoint</span></span>

<span data-ttu-id="61260-161">tooensure이이 페이지 hello CDN에서 새로 고침 hello 페이지에에서 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61260-161">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> <span data-ttu-id="61260-162">두 개에 대 한 hello 같은 자산의 경우에 따라 필요한 hello CDN toocache hello 요청한 콘텐츠를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-162">Two requests for hello same asset are sometimes required for hello CDN toocache hello requested content.</span></span>

<span data-ttu-id="61260-163">Azure CDN 프로필 및 끝점을 만드는 방법에 대한 자세한 내용은 [Azure CDN 시작](../cdn/cdn-create-new-endpoint.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="61260-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-hello-cdn"></a><span data-ttu-id="61260-164">CDN hello를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-164">Purge hello CDN</span></span>

<span data-ttu-id="61260-165">hello CDN에는 hello 활성 시간 (TTL) 구성에 따라 hello 원본 웹 앱에서 리소스를 주기적으로 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="61260-165">hello CDN periodically refreshes its resources from hello origin web app based on hello time-to-live (TTL) configuration.</span></span> <span data-ttu-id="61260-166">hello 기본 TTL은 7 일입니다.</span><span class="sxs-lookup"><span data-stu-id="61260-166">hello default TTL is seven days.</span></span>

<span data-ttu-id="61260-167">때때로 hello-TTL 만료 전에 toorefresh hello CDN 예를 들어 때 필요한 업데이트 된 콘텐츠 toohello 웹 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-167">At times you might need toorefresh hello CDN before hello TTL expiration -- for example, when you deploy updated content toohello web app.</span></span> <span data-ttu-id="61260-168">새로 고침 tootrigger hello CDN 리소스를 수동으로 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61260-168">tootrigger a refresh, you can manually purge hello CDN resources.</span></span> 

<span data-ttu-id="61260-169">Hello 자습서의이 섹션에서는 변경 toohello 웹 앱을 배포 하 고 hello CDN tootrigger hello CDN toorefresh 해당 캐시를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-169">In this section of hello tutorial, you deploy a change toohello web app and purge hello CDN tootrigger hello CDN toorefresh its cache.</span></span>

### <a name="deploy-a-change-toohello-web-app"></a><span data-ttu-id="61260-170">변경 toohello 웹 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="61260-170">Deploy a change toohello web app</span></span>

<span data-ttu-id="61260-171">열기 hello `index.html` 파일을 추가 "-V2" hello 다음 예제와 같이 toohello H1 제목을:</span><span class="sxs-lookup"><span data-stu-id="61260-171">Open hello `index.html` file and add "- V2" toohello H1 heading, as shown in hello following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="61260-172">변경 내용을 커밋하고 toohello 웹 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-172">Commit your change and deploy it toohello web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="61260-173">배포가 완료 되 면 찾아보기 toohello 웹 앱 URL을 변경 하는 hello를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-173">Once deployment has completed, browse toohello web app URL and you see hello change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![웹앱의 제목에서 V2](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="61260-175">Hello 홈 페이지에 대 한 찾아보기 toohello CDN 끝점 URL hello CDN에에서 캐시 된 버전 hello 아직 만료 되지 않으므로 변경할 hello를 보이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="61260-175">Browse toohello CDN endpoint URL for hello home page and you don't see hello change because hello cached version in hello CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![CDN의 제목에서 V2 없음](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a><span data-ttu-id="61260-177">Hello CDN hello 포털에서 제거</span><span class="sxs-lookup"><span data-stu-id="61260-177">Purge hello CDN in hello portal</span></span>

<span data-ttu-id="61260-178">tootrigger는 CDN tooupdate 캐시 된 버전의 hello를 CDN hello를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-178">tootrigger hello CDN tooupdate its cached version, purge hello CDN.</span></span>

<span data-ttu-id="61260-179">Hello 포털 왼쪽된 탐색 영역에서 선택 **리소스 그룹**, 한 다음 웹 앱 (myResourceGroup)에 대해 만든 hello 리소스 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-179">In hello portal left navigation, select **Resource groups**, and then select hello resource group that you created for your web app (myResourceGroup).</span></span>

![리소스 그룹 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="61260-181">Hello 리소스 목록에서 CDN 끝점을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-181">In hello list of resources, select your CDN endpoint.</span></span>

![끝점 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="61260-183">Hello의 hello 위쪽 **끝점** 페이지 **제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-183">At hello top of hello **Endpoint** page, click **Purge**.</span></span>

![제거 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="61260-185">원하는 toopurge hello 콘텐츠 경로 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-185">Enter hello content paths you wish toopurge.</span></span> <span data-ttu-id="61260-186">개별 파일 또는 경로 세그먼트 toopurge 전체 파일 경로 toopurge를 전달할 수 있으며 폴더의 모든 콘텐츠를 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61260-186">You can pass a complete file path toopurge an individual file, or a path segment toopurge and refresh all content in a folder.</span></span> <span data-ttu-id="61260-187">변경한 이후 `index.html`, 인지 확인 하는 hello 경로 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="61260-187">Since you changed `index.html`, make sure that is one of hello paths.</span></span>

<span data-ttu-id="61260-188">Hello 페이지의 hello 맨 아래에 선택 **제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-188">At hello bottom of hello page, select **Purge**.</span></span>

![페이지 제거](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a><span data-ttu-id="61260-190">해당 hello CDN은 업데이트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-190">Verify that hello CDN is updated</span></span>

<span data-ttu-id="61260-191">Hello 삭제 요청은 몇 분 정도 일반적으로 처리를 완료할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="61260-191">Wait until hello purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="61260-192">toosee hello 현재 상태를 hello hello 페이지 위쪽에 선택 hello 종 모양 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="61260-192">toosee hello current status, select hello bell icon at hello top of hello page.</span></span> 

![제거 알림](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="61260-194">Toohello CDN 끝점 URL에 대 한 찾아보기 `index.html`, 나타나고 이제 hello V2 toohello 제목 hello 홈 페이지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-194">Browse toohello CDN endpoint URL for `index.html`, and now you see hello V2 that you added toohello title on hello home page.</span></span> <span data-ttu-id="61260-195">Hello CDN에 캐시를 새로 고칠를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-195">This shows that hello CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![CDN의 제목에서 V2](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="61260-197">자세한 내용은 [Azure CDN 끝점 제거](../cdn/cdn-purge-endpoint.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="61260-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-tooversion-content"></a><span data-ttu-id="61260-198">쿼리 문자열 tooversion 콘텐츠 사용</span><span class="sxs-lookup"><span data-stu-id="61260-198">Use query strings tooversion content</span></span>

<span data-ttu-id="61260-199">Azure CDN hello hello 다음 캐싱 동작 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-199">hello Azure CDN offers hello following caching behavior options:</span></span>

* <span data-ttu-id="61260-200">쿼리 문자열 무시</span><span class="sxs-lookup"><span data-stu-id="61260-200">Ignore query strings</span></span>
* <span data-ttu-id="61260-201">쿼리 문자열에 대한 캐싱 우회</span><span class="sxs-lookup"><span data-stu-id="61260-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="61260-202">모든 고유한 URL 캐시</span><span class="sxs-lookup"><span data-stu-id="61260-202">Cache every unique URL</span></span> 

<span data-ttu-id="61260-203">먼저 hello 이러한은 hello default, 자산 hello URL에 쿼리 문자열 hello에 관계 없이 캐시 된 버전을 하나만 있다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="61260-203">hello first of these is hello default, which means there is only one cached version of an asset regardless of hello query string in hello URL.</span></span> 

<span data-ttu-id="61260-204">Hello 자습서의이 섹션에서는 각 고유한 URL 동작 toocache 캐싱 hello를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61260-204">In this section of hello tutorial, you change hello caching behavior toocache every unique URL.</span></span>

### <a name="change-hello-cache-behavior"></a><span data-ttu-id="61260-205">Hello 캐시 동작 변경</span><span class="sxs-lookup"><span data-stu-id="61260-205">Change hello cache behavior</span></span>

<span data-ttu-id="61260-206">Hello Azure 포털에서에서 **CDN 끝점** 페이지에서 **캐시**합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-206">In hello Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="61260-207">선택 **각 고유한 URL 캐시** hello에서 **쿼리 문자열 캐싱 동작** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="61260-207">Select **Cache every unique URL** from hello **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="61260-208">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-208">Select **Save**.</span></span>

![쿼리 문자열 캐싱 동작 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="61260-210">고유 URL을 별도로 캐시했는지 확인</span><span class="sxs-lookup"><span data-stu-id="61260-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="61260-211">브라우저에서 hello CDN 끝점에 toohello 홈 페이지를 탐색 하는 쿼리 문자열을 포함.</span><span class="sxs-lookup"><span data-stu-id="61260-211">In a browser, navigate toohello home page at hello CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="61260-212">CDN hello hello 현재 웹 응용 프로그램 콘텐츠를 hello 제목에 "V2"를 포함 하는 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-212">hello CDN returns hello current web app content, which includes "V2" in hello heading.</span></span> 

<span data-ttu-id="61260-213">tooensure이이 페이지 hello CDN에서 새로 고침 hello 페이지에에서 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61260-213">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> 

<span data-ttu-id="61260-214">열기 `index.html` 너무 "V2" 변경 "V3" hello 변경 내용 배포 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-214">Open `index.html` and change "V2" too"V3", and deploy hello change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="61260-215">브라우저에서 새 쿼리 문자열로 toohello CDN 끝점 URL을와 같은 이동 `q=2`합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-215">In a browser, go toohello CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="61260-216">CDN hello hello 현재 가져옵니다 `index.html` 파일을 "V3"를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-216">hello CDN gets hello current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="61260-217">Hello로 toohello CDN 끝점을 이동 하는 경우 하지만 `q=1` 쿼리 문자열, "V2"를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="61260-217">But if you navigate toohello CDN endpoint with hello `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![CDN에서 제목에 V3, 쿼리 문자열 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![CDN에서 제목에 V2, 쿼리 문자열 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="61260-220">이 출력에서는 각 쿼리 문자열이 다르게 처리됨을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="61260-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="61260-221">이전에는 q=1이 사용되어 캐시된 내용(V2)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="61260-222">q = 2 이므로 새로 만들었거나, hello 최신 웹 응용 프로그램 콘텐츠 검색 되 고 (V3)을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-222">q=2 is new, so hello latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="61260-223">자세한 내용은 [쿼리 문자열을 사용하여 Azure CDN 캐싱 동작 제어](../cdn/cdn-query-string.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="61260-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a><span data-ttu-id="61260-224">사용자 지정 도메인 tooa CDN 끝점 매핑</span><span class="sxs-lookup"><span data-stu-id="61260-224">Map a custom domain tooa CDN endpoint</span></span>

<span data-ttu-id="61260-225">CNAME 레코드를 만들어 사용자 지정 도메인 tooyour를 CDN 끝점 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-225">You'll map your custom domain tooyour CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="61260-226">CNAME 레코드는 원본 도메인 tooa 대상 도메인을 매핑하는 DNS 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="61260-226">A CNAME record is a DNS feature that maps a source domain tooa destination domain.</span></span> <span data-ttu-id="61260-227">예를 들어 매핑하는 `cdn.contoso.com` 또는 `static.contoso.com` 너무`contoso.azureedge.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` too`contoso.azureedge.net`.</span></span>

<span data-ttu-id="61260-228">사용자 지정 도메인이 없는 경우 다음과 같은 hello [앱 서비스 도메인 자습서](custom-dns-web-site-buydomains-web-app.md) 사용 하 여 도메인 toopurchase hello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="61260-228">If you don't have a custom domain, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a><span data-ttu-id="61260-229">CNAME hello로 hello hostname toouse 찾기</span><span class="sxs-lookup"><span data-stu-id="61260-229">Find hello hostname toouse with hello CNAME</span></span>

<span data-ttu-id="61260-230">Hello Azure 포털에서에서 **끝점** 페이지에서 **개요** hello 탐색 및 선택 hello 왼쪽에서 선택 된 **+ 사용자 지정 도메인** hello hello 페이지 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="61260-230">In hello Azure portal **Endpoint** page, make sure **Overview** is selected in hello left navigation, and then select hello **+ Custom Domain** button at hello top of hello page.</span></span>

![사용자 지정 도메인 추가 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="61260-232">Hello에 **사용자 지정 도메인 추가** 페이지에 CNAME 레코드를 만드는 hello 끝점 호스트 이름 toouse 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-232">In hello **Add a custom domain** page, you see hello endpoint host name toouse in creating a CNAME record.</span></span> <span data-ttu-id="61260-233">CDN 끝점 URL에서 파생 된 hello 호스트 이름:  **&lt;EndpointName >. azureedge.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-233">hello host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![도메인 페이지 추가](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a><span data-ttu-id="61260-235">도메인 등록 기관과 함께 CNAME hello 구성</span><span class="sxs-lookup"><span data-stu-id="61260-235">Configure hello CNAME with your domain registrar</span></span>

<span data-ttu-id="61260-236">Tooyour 도메인 등록 기관의 웹 사이트를 탐색 하 고 DNS 레코드를 만들기 위한 hello 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="61260-236">Navigate tooyour domain registrar's web site, and locate hello section for creating DNS records.</span></span> <span data-ttu-id="61260-237">**도메인 이름**, **DNS** 또는 **이름 서버 관리**와 같은 섹션에서 이를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61260-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="61260-238">CNAMEs를 관리 하기 위한 hello 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="61260-238">Find hello section for managing CNAMEs.</span></span> <span data-ttu-id="61260-239">Toogo tooan 고급 설정 페이지를 가질 수 고 CNAME, 별칭 또는 하위 도메인 hello 단어를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61260-239">You may have toogo tooan advanced settings page and look for hello words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="61260-240">선택된 된 하위 도메인을 매핑하는 CNAME 레코드를 만듭니다 (예를 들어 **정적** 또는 **cdn**) toohello **끝점 호스트 이름** hello 포털의 앞부분에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) toohello **Endpoint host name** shown earlier in hello portal.</span></span> 

### <a name="enter-hello-custom-domain-in-azure"></a><span data-ttu-id="61260-241">Azure의 hello 사용자 지정 도메인을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-241">Enter hello custom domain in Azure</span></span>

<span data-ttu-id="61260-242">Toohello 반환 **사용자 지정 도메인 추가** 페이지 및 hello 하위 도메인을 포함 하 여 hello 대화 상자에서 사용자 지정 도메인을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-242">Return toohello **Add a custom domain** page, and enter your custom domain, including hello subdomain, in hello dialog box.</span></span> <span data-ttu-id="61260-243">예를 들어 `cdn.contoso.com`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="61260-244">Azure는 입력 한 hello 도메인 이름에 대 한 hello CNAME 레코드가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-244">Azure verifies that hello CNAME record exists for hello domain name you have entered.</span></span> <span data-ttu-id="61260-245">Hello CNAME이 올바르면 사용자 지정 도메인의 유효성이 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61260-245">If hello CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="61260-246">Hello 인터넷에서 CNAME 레코드 toopropagate tooname 서버 hello에 대 한 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61260-246">It can take time for hello CNAME record toopropagate tooname servers on hello Internet.</span></span> <span data-ttu-id="61260-247">도메인의 유효성이 바로 검사되지 않으면 몇 분 후에 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-hello-custom-domain"></a><span data-ttu-id="61260-248">테스트 hello에 대 한 사용자 지정 도메인</span><span class="sxs-lookup"><span data-stu-id="61260-248">Test hello custom domain</span></span>

<span data-ttu-id="61260-249">브라우저에서 탐색 toohello `index.html` 사용자 지정 도메인을 사용 하 여 파일 (예를 들어 `cdn.contoso.com/index.html`) hello 결과 tooverify hello로 수행 하는 경우 직접 너무 동일`<endpointname>azureedge.net/index.html`합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-249">In a browser, navigate toohello `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) tooverify that hello result is hello same as when you go directly too`<endpointname>azureedge.net/index.html`.</span></span>

![사용자 지정 도메인 URL을 사용하는 샘플 앱 홈 페이지](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="61260-251">자세한 내용은 참조 [맵 Azure CDN 콘텐츠 tooa 사용자 지정 도메인](../cdn/cdn-map-content-to-custom-domain.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-251">For more information, see [Map Azure CDN content tooa custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="61260-252">다음 단계</span><span class="sxs-lookup"><span data-stu-id="61260-252">Next steps</span></span>

<span data-ttu-id="61260-253">학습한 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="61260-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="61260-254">CDN 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="61260-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="61260-255">캐시된 자산 새로 고침</span><span class="sxs-lookup"><span data-stu-id="61260-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="61260-256">사용 하 여 쿼리 문자열 캐시 toocontrol 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="61260-256">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="61260-257">Hello CDN 끝점에 대 한 사용자 지정 도메인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="61260-257">Use a custom domain for hello CDN endpoint.</span></span>

<span data-ttu-id="61260-258">Toooptimize CDN 성능에 따라 hello 문서 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="61260-258">Learn how toooptimize CDN performance in hello following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="61260-259">Azure CDN에서 파일을 압축하여 성능 향상</span><span class="sxs-lookup"><span data-stu-id="61260-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="61260-260">Azure CDN 끝점에 자산 미리 로드</span><span class="sxs-lookup"><span data-stu-id="61260-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
