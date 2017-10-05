---
title: "Mobile Apps 및 Mobile Services에서 클라이언트 및 서버 SDK 버전 관리 | Microsoft Docs"
description: "모바일 서비스와 Azure 모바일 앱에 대한 클라이언트 SDK의 목록 및 서버 SDK 버전과 호환성"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: f79e819b1547f81498ea213858faf3c75e374782
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="69e15-103">모바일 앱 및 모바일 서비스에서 클라이언트 및 서버 버전 관리</span><span class="sxs-lookup"><span data-stu-id="69e15-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="69e15-104">Azure 모바일 서비스의 최신 버전은 Azure 앱 서비스의 **모바일 앱** 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-104">The latest version of Azure Mobile Services is the **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="69e15-105">모바일 앱 클라이언트 및 서버 SDK는 원래 모바일 서비스를 기반으로 하지만 서로 호환되지 *않습니다* .</span><span class="sxs-lookup"><span data-stu-id="69e15-105">The Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="69e15-106">즉, *Mobile Apps* 서버 SDK 및 마찬가지로 *Mobile Services*를 사용하는 *Mobile Apps* 클라이언트 SDK를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="69e15-107">이 계약은 클라이언트 및 서버 SDK인 `ZUMO-API-VERSION`에서 사용하는 특별한 헤더 값을 통해 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-107">This contract is enforced through a special header value used by the client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="69e15-108">참고: 이 문서가 *모바일 서비스* 백 엔드를 참조할 때마다 반드시 모바일 서비스에서 호스팅해야 할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-108">Note: whenever this document refers to a *Mobile Services* backend, it does not necessarily need to be hosted on Mobile Services.</span></span> <span data-ttu-id="69e15-109">이제 코드를 변경하지 않고 App Service에서 실행되도록 Mobile Services를 마이그레이션할 수 있지만 서비스는 *Mobile Services* SDK 버전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-109">It is now possible to migrate a mobile service to run on App Service without any code changes, but the service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="69e15-110">코드 변경 없이 앱 서비스에 마이그레이션하는 방법을 자세히 알아보려면 [Azure 앱 서비스에 모바일 서비스 마이그레이션]문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69e15-110">To learn more about migrating to App Service without any code changes, see the article [Migrate a Mobile Service to Azure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="69e15-111">헤더 사양</span><span class="sxs-lookup"><span data-stu-id="69e15-111">Header specification</span></span>
<span data-ttu-id="69e15-112">키 `ZUMO-API-VERSION` 는 HTTP 헤더 또는 쿼리 문자열에 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-112">The key `ZUMO-API-VERSION` may be specified in either the HTTP header or the query string.</span></span> <span data-ttu-id="69e15-113">값은 **x.y.z**형식의 버전 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-113">The value is a version string in the form **x.y.z**.</span></span>

<span data-ttu-id="69e15-114">예:</span><span class="sxs-lookup"><span data-stu-id="69e15-114">For example:</span></span>

<span data-ttu-id="69e15-115">GET https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="69e15-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="69e15-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="69e15-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="69e15-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="69e15-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="69e15-118">버전 확인 건너뛰기</span><span class="sxs-lookup"><span data-stu-id="69e15-118">Opting out of version checking</span></span>
<span data-ttu-id="69e15-119">앱 설정 **MS_SkipVersionCheck**에 대한 **true** 값을 설정하여 버전 확인을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-119">You can opt out of version checking by setting a value of **true** for the app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="69e15-120">Web.config 또는 Azure 포털의 응용 프로그램 설정 섹션에서 이를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-120">Specify this either in your web.config or in the Application Settings section of the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="69e15-121">오프라인 동기화, 인증 및 푸시 알림 영역에서 특히 모바일 서비스와 모바일 앱 간의 많은 동작 변경 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in the areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="69e15-122">이러한 동작 변경이 앱의 기능을 중단하지 않도록 테스트를 완료한 후에 버전 확인을 옵트아웃해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-122">You should only opt out of version checking after complete testing to ensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="69e15-123">모든 버전에 대한 호환성 요약</span><span class="sxs-lookup"><span data-stu-id="69e15-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="69e15-124">아래 차트에서는 모든 클라이언트 및 서버 형식 간의 호환성을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-124">The chart below shows the compatibility between all client and server types.</span></span> <span data-ttu-id="69e15-125">백 엔드는 사용하는 서버 SDK에 기반하여 모바일 **서비스** 또는 모바일 **앱**으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on the server SDK that it uses.</span></span>

|  | <span data-ttu-id="69e15-126">**모바일 서비스** Node.js 또는 .NET</span><span class="sxs-lookup"><span data-stu-id="69e15-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="69e15-127">**모바일 앱** Node.js 또는 .NET</span><span class="sxs-lookup"><span data-stu-id="69e15-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="69e15-128">[모바일 서비스 클라이언트]</span><span class="sxs-lookup"><span data-stu-id="69e15-128">[Mobile Services clients]</span></span> |<span data-ttu-id="69e15-129">확인</span><span class="sxs-lookup"><span data-stu-id="69e15-129">Ok</span></span> |<span data-ttu-id="69e15-130">오류\*</span><span class="sxs-lookup"><span data-stu-id="69e15-130">Error\*</span></span> |
| <span data-ttu-id="69e15-131">[모바일 앱 클라이언트]</span><span class="sxs-lookup"><span data-stu-id="69e15-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="69e15-132">오류\*</span><span class="sxs-lookup"><span data-stu-id="69e15-132">Error\*</span></span> |<span data-ttu-id="69e15-133">확인</span><span class="sxs-lookup"><span data-stu-id="69e15-133">Ok</span></span> |

<span data-ttu-id="69e15-134">\***MS_SkipVersionCheck**를 지정하여 제어될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  The anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: the fwlink to this document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="69e15-135"><a name="1.0.0"></a>모바일 서비스 클라이언트 및 서버</span><span class="sxs-lookup"><span data-stu-id="69e15-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="69e15-136">아래 테이블의 클라이언트 SDK는 **모바일 서비스**와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-136">The client SDKs in the table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="69e15-137">참고: 모바일 서비스 클라이언트 SDK는 `ZUMO-API-VERSION`에 헤더 값을 보내지 *않습니다*.</span><span class="sxs-lookup"><span data-stu-id="69e15-137">Note: the Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="69e15-138">서비스가 헤더 또는 쿼리 문자열 값을 수신하는 경우 위에서 설명한 대로 명시적으로 건너뛰지 않으면 오류가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-138">If the service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="69e15-139"><a name="MobileServicesClients"></a> 모바일 *서비스* 클라이언트 SDK</span><span class="sxs-lookup"><span data-stu-id="69e15-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="69e15-140">클라이언트 플랫폼</span><span class="sxs-lookup"><span data-stu-id="69e15-140">Client platform</span></span> | <span data-ttu-id="69e15-141">버전</span><span class="sxs-lookup"><span data-stu-id="69e15-141">Version</span></span> | <span data-ttu-id="69e15-142">버전 헤더 값</span><span class="sxs-lookup"><span data-stu-id="69e15-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="69e15-143">관리된 클라이언트(Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="69e15-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="69e15-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="69e15-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="69e15-145">해당 없음</span><span class="sxs-lookup"><span data-stu-id="69e15-145">n/a</span></span> |
| <span data-ttu-id="69e15-146">iOS</span><span class="sxs-lookup"><span data-stu-id="69e15-146">iOS</span></span> |[<span data-ttu-id="69e15-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="69e15-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="69e15-148">해당 없음</span><span class="sxs-lookup"><span data-stu-id="69e15-148">n/a</span></span> |
| <span data-ttu-id="69e15-149">Android</span><span class="sxs-lookup"><span data-stu-id="69e15-149">Android</span></span> |[<span data-ttu-id="69e15-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="69e15-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="69e15-151">해당 없음</span><span class="sxs-lookup"><span data-stu-id="69e15-151">n/a</span></span> |
| <span data-ttu-id="69e15-152">HTML</span><span class="sxs-lookup"><span data-stu-id="69e15-152">HTML</span></span> |[<span data-ttu-id="69e15-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="69e15-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="69e15-154">해당 없음</span><span class="sxs-lookup"><span data-stu-id="69e15-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="69e15-155">모바일 *서비스* 서버 SDK</span><span class="sxs-lookup"><span data-stu-id="69e15-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="69e15-156">서버 플랫폼</span><span class="sxs-lookup"><span data-stu-id="69e15-156">Server platform</span></span> | <span data-ttu-id="69e15-157">버전</span><span class="sxs-lookup"><span data-stu-id="69e15-157">Version</span></span> | <span data-ttu-id="69e15-158">수락된 버전 헤더</span><span class="sxs-lookup"><span data-stu-id="69e15-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="69e15-159">.NET</span><span class="sxs-lookup"><span data-stu-id="69e15-159">.NET</span></span> |[<span data-ttu-id="69e15-160">WindowsAzure.MobileServices.Backend.* 버전 1.0.x</span><span class="sxs-lookup"><span data-stu-id="69e15-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="69e15-161">* * 버전 헤더가 * *</span><span class="sxs-lookup"><span data-stu-id="69e15-161">**No version header **</span></span> |
| <span data-ttu-id="69e15-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="69e15-162">Node.js</span></span> |<span data-ttu-id="69e15-163">(서비스 예정)</span><span class="sxs-lookup"><span data-stu-id="69e15-163">(coming soon)</span></span> |<span data-ttu-id="69e15-164">**버전 헤더 없음**</span><span class="sxs-lookup"><span data-stu-id="69e15-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="69e15-165">모바일 서비스 백 엔드의 동작</span><span class="sxs-lookup"><span data-stu-id="69e15-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="69e15-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="69e15-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="69e15-167">MS_SkipVersionCheck의 값</span><span class="sxs-lookup"><span data-stu-id="69e15-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="69e15-168">응답</span><span class="sxs-lookup"><span data-stu-id="69e15-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="69e15-169">지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="69e15-169">Not specified</span></span> |<span data-ttu-id="69e15-170">모두</span><span class="sxs-lookup"><span data-stu-id="69e15-170">Any</span></span> |<span data-ttu-id="69e15-171">200 - 확인</span><span class="sxs-lookup"><span data-stu-id="69e15-171">200 - OK</span></span> |
| <span data-ttu-id="69e15-172">어떤 값</span><span class="sxs-lookup"><span data-stu-id="69e15-172">Any value</span></span> |<span data-ttu-id="69e15-173">True</span><span class="sxs-lookup"><span data-stu-id="69e15-173">True</span></span> |<span data-ttu-id="69e15-174">200 - 확인</span><span class="sxs-lookup"><span data-stu-id="69e15-174">200 - OK</span></span> |
| <span data-ttu-id="69e15-175">어떤 값</span><span class="sxs-lookup"><span data-stu-id="69e15-175">Any value</span></span> |<span data-ttu-id="69e15-176">False/지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="69e15-176">False/Not Specified</span></span> |<span data-ttu-id="69e15-177">400 - 잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="69e15-177">400 - Bad Request</span></span> |

## <span data-ttu-id="69e15-178"><a name="2.0.0"></a>Azure 모바일 앱 클라이언트 및 서버</span><span class="sxs-lookup"><span data-stu-id="69e15-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="69e15-179"><a name="MobileAppsClients"></a> 모바일 *앱* 클라이언트 SDK</span><span class="sxs-lookup"><span data-stu-id="69e15-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="69e15-180">버전 확인은 **Azure 모바일 앱**에 대한 클라이언트 SDK의 다음 버전부터 도입됩니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-180">Version checking was introduced starting with the following versions of the client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="69e15-181">클라이언트 플랫폼</span><span class="sxs-lookup"><span data-stu-id="69e15-181">Client platform</span></span> | <span data-ttu-id="69e15-182">버전</span><span class="sxs-lookup"><span data-stu-id="69e15-182">Version</span></span> | <span data-ttu-id="69e15-183">버전 헤더 값</span><span class="sxs-lookup"><span data-stu-id="69e15-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="69e15-184">관리된 클라이언트(Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="69e15-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="69e15-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="69e15-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="69e15-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="69e15-186">2.0.0</span></span> |
| <span data-ttu-id="69e15-187">iOS</span><span class="sxs-lookup"><span data-stu-id="69e15-187">iOS</span></span> |[<span data-ttu-id="69e15-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="69e15-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="69e15-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="69e15-189">2.0.0</span></span> |
| <span data-ttu-id="69e15-190">Android</span><span class="sxs-lookup"><span data-stu-id="69e15-190">Android</span></span> |[<span data-ttu-id="69e15-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="69e15-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="69e15-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="69e15-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="69e15-193">모바일 *앱* 서버 SDK</span><span class="sxs-lookup"><span data-stu-id="69e15-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="69e15-194">버전 검사는 다음 서버 SDK 버전에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69e15-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="69e15-195">서버 플랫폼</span><span class="sxs-lookup"><span data-stu-id="69e15-195">Server platform</span></span> | <span data-ttu-id="69e15-196">SDK)</span><span class="sxs-lookup"><span data-stu-id="69e15-196">SDK</span></span> | <span data-ttu-id="69e15-197">수락된 버전 헤더</span><span class="sxs-lookup"><span data-stu-id="69e15-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="69e15-198">.NET</span><span class="sxs-lookup"><span data-stu-id="69e15-198">.NET</span></span> |[<span data-ttu-id="69e15-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="69e15-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="69e15-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="69e15-200">2.0.0</span></span> |
| <span data-ttu-id="69e15-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="69e15-201">Node.js</span></span> |[<span data-ttu-id="69e15-202">azure-mobile-apps)</span><span class="sxs-lookup"><span data-stu-id="69e15-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="69e15-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="69e15-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="69e15-204">모바일 앱 백 엔드의 동작</span><span class="sxs-lookup"><span data-stu-id="69e15-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="69e15-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="69e15-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="69e15-206">MS_SkipVersionCheck의 값</span><span class="sxs-lookup"><span data-stu-id="69e15-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="69e15-207">응답</span><span class="sxs-lookup"><span data-stu-id="69e15-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="69e15-208">x.y.z 또는 Null</span><span class="sxs-lookup"><span data-stu-id="69e15-208">x.y.z or Null</span></span> |<span data-ttu-id="69e15-209">True</span><span class="sxs-lookup"><span data-stu-id="69e15-209">True</span></span> |<span data-ttu-id="69e15-210">200 - 확인</span><span class="sxs-lookup"><span data-stu-id="69e15-210">200 - OK</span></span> |
| <span data-ttu-id="69e15-211">Null</span><span class="sxs-lookup"><span data-stu-id="69e15-211">Null</span></span> |<span data-ttu-id="69e15-212">False/지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="69e15-212">False/Not Specified</span></span> |<span data-ttu-id="69e15-213">400 - 잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="69e15-213">400 - Bad Request</span></span> |
| <span data-ttu-id="69e15-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="69e15-214">1.x.y</span></span> |<span data-ttu-id="69e15-215">False/지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="69e15-215">False/Not Specified</span></span> |<span data-ttu-id="69e15-216">400 - 잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="69e15-216">400 - Bad Request</span></span> |
| <span data-ttu-id="69e15-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="69e15-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="69e15-218">False/지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="69e15-218">False/Not Specified</span></span> |<span data-ttu-id="69e15-219">200 - 확인</span><span class="sxs-lookup"><span data-stu-id="69e15-219">200 - OK</span></span> |
| <span data-ttu-id="69e15-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="69e15-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="69e15-221">False/지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="69e15-221">False/Not Specified</span></span> |<span data-ttu-id="69e15-222">400 - 잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="69e15-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="69e15-223">다음 단계</span><span class="sxs-lookup"><span data-stu-id="69e15-223">Next Steps</span></span>
* <span data-ttu-id="69e15-224">[Azure 앱 서비스에 모바일 서비스 마이그레이션]</span><span class="sxs-lookup"><span data-stu-id="69e15-224">[Migrate a Mobile Service to Azure App Service]</span></span>

<span data-ttu-id="69e15-225">[모바일 서비스 클라이언트]: #MobileServicesClients</span><span class="sxs-lookup"><span data-stu-id="69e15-225">[Mobile Services clients]: #MobileServicesClients</span></span>
<span data-ttu-id="69e15-226">[모바일 앱 클라이언트]: #MobileAppsClients</span><span class="sxs-lookup"><span data-stu-id="69e15-226">[Mobile Apps clients]: #MobileAppsClients</span></span>


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
<span data-ttu-id="69e15-227">[Azure 앱 서비스에 모바일 서비스 마이그레이션]: app-service-mobile-migrating-from-mobile-services.md</span><span class="sxs-lookup"><span data-stu-id="69e15-227">[Migrate a Mobile Service to Azure App Service]: app-service-mobile-migrating-from-mobile-services.md</span></span>
