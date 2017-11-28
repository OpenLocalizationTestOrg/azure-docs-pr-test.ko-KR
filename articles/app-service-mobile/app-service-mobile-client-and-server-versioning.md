---
title: "모바일 앱 및 모바일 서비스에서 aaaClient 및 서버 SDK 버전 관리 | Microsoft Docs"
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
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="ba9cd-103">모바일 앱 및 모바일 서비스에서 클라이언트 및 서버 버전 관리</span><span class="sxs-lookup"><span data-stu-id="ba9cd-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="ba9cd-104">hello 최신 버전의 Azure 모바일 서비스는 hello **모바일 앱** Azure 앱 서비스 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-104">hello latest version of Azure Mobile Services is hello **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="ba9cd-105">모바일 응용 프로그램 클라이언트 hello 및 서버 Sdk는 모바일 서비스에서 항목에 따라 원래 되어도 없지만 *하지* 서로 호환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-105">hello Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="ba9cd-106">즉, *Mobile Apps* 서버 SDK 및 마찬가지로 *Mobile Services*를 사용하는 *Mobile Apps* 클라이언트 SDK를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="ba9cd-107">이 계약은 hello 클라이언트와 서버 Sdk에서 사용 되는 특별 한 헤더 값을 통해 적용 `ZUMO-API-VERSION`합니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-107">This contract is enforced through a special header value used by hello client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="ba9cd-108">참고: 때마다이 문서는 참조 tooa *모바일 서비스* 백 엔드, 필요 하지 않습니다 반드시 toobe 모바일 서비스에서 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-108">Note: whenever this document refers tooa *Mobile Services* backend, it does not necessarily need toobe hosted on Mobile Services.</span></span> <span data-ttu-id="ba9cd-109">Hello 서비스 여전히 사용 될 수 있지만 가능한 toomigrate 코드 변경 하지 않고 앱 서비스 모바일 서비스 toorun은 이제 *모바일 서비스* SDK 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-109">It is now possible toomigrate a mobile service toorun on App Service without any code changes, but hello service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="ba9cd-110">에 대해 더 알아봅니다 toolearn hello 문서를 참조 tooApp 서비스 코드 변경 없이 마이그레이션할 [모바일 서비스 tooAzure 앱 서비스를 마이그레이션할]합니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-110">toolearn more about migrating tooApp Service without any code changes, see hello article [Migrate a Mobile Service tooAzure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="ba9cd-111">헤더 사양</span><span class="sxs-lookup"><span data-stu-id="ba9cd-111">Header specification</span></span>
<span data-ttu-id="ba9cd-112">hello 키 `ZUMO-API-VERSION` hello HTTP 헤더 또는 hello 쿼리 문자열에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-112">hello key `ZUMO-API-VERSION` may be specified in either hello HTTP header or hello query string.</span></span> <span data-ttu-id="ba9cd-113">hello 값은 버전 문자열 hello 형태로 **x.y.z 형식이 며**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-113">hello value is a version string in hello form **x.y.z**.</span></span>

<span data-ttu-id="ba9cd-114">예:</span><span class="sxs-lookup"><span data-stu-id="ba9cd-114">For example:</span></span>

<span data-ttu-id="ba9cd-115">GET https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="ba9cd-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="ba9cd-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="ba9cd-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="ba9cd-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="ba9cd-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="ba9cd-118">버전 확인 건너뛰기</span><span class="sxs-lookup"><span data-stu-id="ba9cd-118">Opting out of version checking</span></span>
<span data-ttu-id="ba9cd-119">버전의 값을 설정 하 여 확인을 취소 수 **true** hello 응용 프로그램 설정에 대 한 **MS_SkipVersionCheck**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-119">You can opt out of version checking by setting a value of **true** for hello app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="ba9cd-120">Web.config 파일에 또는 hello hello Azure 포털의 응용 프로그램 설정 섹션에서에서이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-120">Specify this either in your web.config or in hello Application Settings section of hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="ba9cd-121">모바일 서비스와 특히 hello 오프 라인 동기화, 인증 및 푸시 알림 영역에서에서 모바일 응용 프로그램 간의 동작 변경의 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in hello areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="ba9cd-122">이러한 동작 변경 내용은 앱의 기능을 해제 되지 않도록 테스트 tooensure 완료 후 확인 버전만 취소 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-122">You should only opt out of version checking after complete testing tooensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="ba9cd-123">모든 버전에 대한 호환성 요약</span><span class="sxs-lookup"><span data-stu-id="ba9cd-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="ba9cd-124">아래 hello 차트에서는 모든 클라이언트 및 서버 형식 간에 hello 호환성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-124">hello chart below shows hello compatibility between all client and server types.</span></span> <span data-ttu-id="ba9cd-125">백 엔드 어느 모바일으로 분류 됩니다 **서비스** 또는 모바일 **앱** hello 서버에서 사용 하는 SDK에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on hello server SDK that it uses.</span></span>

|  | <span data-ttu-id="ba9cd-126">**모바일 서비스** Node.js 또는 .NET</span><span class="sxs-lookup"><span data-stu-id="ba9cd-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="ba9cd-127">**모바일 앱** Node.js 또는 .NET</span><span class="sxs-lookup"><span data-stu-id="ba9cd-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba9cd-128">[모바일 서비스 클라이언트]</span><span class="sxs-lookup"><span data-stu-id="ba9cd-128">[Mobile Services clients]</span></span> |<span data-ttu-id="ba9cd-129">확인</span><span class="sxs-lookup"><span data-stu-id="ba9cd-129">Ok</span></span> |<span data-ttu-id="ba9cd-130">오류\*</span><span class="sxs-lookup"><span data-stu-id="ba9cd-130">Error\*</span></span> |
| <span data-ttu-id="ba9cd-131">[모바일 앱 클라이언트]</span><span class="sxs-lookup"><span data-stu-id="ba9cd-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="ba9cd-132">오류\*</span><span class="sxs-lookup"><span data-stu-id="ba9cd-132">Error\*</span></span> |<span data-ttu-id="ba9cd-133">확인</span><span class="sxs-lookup"><span data-stu-id="ba9cd-133">Ok</span></span> |

<span data-ttu-id="ba9cd-134">\***MS_SkipVersionCheck**를 지정하여 제어될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="ba9cd-135"><a name="1.0.0"></a>모바일 서비스 클라이언트 및 서버</span><span class="sxs-lookup"><span data-stu-id="ba9cd-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="ba9cd-136">hello 테이블 아래에 hello 클라이언트 Sdk와 호환 되는 **모바일 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-136">hello client SDKs in hello table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="ba9cd-137">참고: hello 모바일 서비스 클라이언트 Sdk *없는* 헤더 값에 대 한 보내기 `ZUMO-API-VERSION`합니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-137">Note: hello Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="ba9cd-138">이 헤더 또는 쿼리 문자열 값인 hello 서비스에서 수신 하는 경우 위에 설명 된 대로 선택한 명시적으로 하지 않으면 오류가 반환 될 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-138">If hello service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="ba9cd-139"><a name="MobileServicesClients"></a> 모바일 *서비스* 클라이언트 SDK</span><span class="sxs-lookup"><span data-stu-id="ba9cd-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="ba9cd-140">클라이언트 플랫폼</span><span class="sxs-lookup"><span data-stu-id="ba9cd-140">Client platform</span></span> | <span data-ttu-id="ba9cd-141">버전</span><span class="sxs-lookup"><span data-stu-id="ba9cd-141">Version</span></span> | <span data-ttu-id="ba9cd-142">버전 헤더 값</span><span class="sxs-lookup"><span data-stu-id="ba9cd-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba9cd-143">관리된 클라이언트(Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="ba9cd-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="ba9cd-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="ba9cd-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="ba9cd-145">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba9cd-145">n/a</span></span> |
| <span data-ttu-id="ba9cd-146">iOS</span><span class="sxs-lookup"><span data-stu-id="ba9cd-146">iOS</span></span> |[<span data-ttu-id="ba9cd-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="ba9cd-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="ba9cd-148">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba9cd-148">n/a</span></span> |
| <span data-ttu-id="ba9cd-149">Android</span><span class="sxs-lookup"><span data-stu-id="ba9cd-149">Android</span></span> |[<span data-ttu-id="ba9cd-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="ba9cd-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="ba9cd-151">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba9cd-151">n/a</span></span> |
| <span data-ttu-id="ba9cd-152">HTML</span><span class="sxs-lookup"><span data-stu-id="ba9cd-152">HTML</span></span> |[<span data-ttu-id="ba9cd-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="ba9cd-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="ba9cd-154">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba9cd-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="ba9cd-155">모바일 *서비스* 서버 SDK</span><span class="sxs-lookup"><span data-stu-id="ba9cd-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="ba9cd-156">서버 플랫폼</span><span class="sxs-lookup"><span data-stu-id="ba9cd-156">Server platform</span></span> | <span data-ttu-id="ba9cd-157">버전</span><span class="sxs-lookup"><span data-stu-id="ba9cd-157">Version</span></span> | <span data-ttu-id="ba9cd-158">수락된 버전 헤더</span><span class="sxs-lookup"><span data-stu-id="ba9cd-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba9cd-159">.NET</span><span class="sxs-lookup"><span data-stu-id="ba9cd-159">.NET</span></span> |[<span data-ttu-id="ba9cd-160">WindowsAzure.MobileServices.Backend.* 버전 1.0.x</span><span class="sxs-lookup"><span data-stu-id="ba9cd-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="ba9cd-161">* * 버전 헤더가 * *</span><span class="sxs-lookup"><span data-stu-id="ba9cd-161">**No version header **</span></span> |
| <span data-ttu-id="ba9cd-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="ba9cd-162">Node.js</span></span> |<span data-ttu-id="ba9cd-163">(서비스 예정)</span><span class="sxs-lookup"><span data-stu-id="ba9cd-163">(coming soon)</span></span> |<span data-ttu-id="ba9cd-164">**버전 헤더 없음**</span><span class="sxs-lookup"><span data-stu-id="ba9cd-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="ba9cd-165">모바일 서비스 백 엔드의 동작</span><span class="sxs-lookup"><span data-stu-id="ba9cd-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="ba9cd-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="ba9cd-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="ba9cd-167">MS_SkipVersionCheck의 값</span><span class="sxs-lookup"><span data-stu-id="ba9cd-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="ba9cd-168">응답</span><span class="sxs-lookup"><span data-stu-id="ba9cd-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba9cd-169">지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="ba9cd-169">Not specified</span></span> |<span data-ttu-id="ba9cd-170">모두</span><span class="sxs-lookup"><span data-stu-id="ba9cd-170">Any</span></span> |<span data-ttu-id="ba9cd-171">200 - 확인</span><span class="sxs-lookup"><span data-stu-id="ba9cd-171">200 - OK</span></span> |
| <span data-ttu-id="ba9cd-172">어떤 값</span><span class="sxs-lookup"><span data-stu-id="ba9cd-172">Any value</span></span> |<span data-ttu-id="ba9cd-173">True</span><span class="sxs-lookup"><span data-stu-id="ba9cd-173">True</span></span> |<span data-ttu-id="ba9cd-174">200 - 확인</span><span class="sxs-lookup"><span data-stu-id="ba9cd-174">200 - OK</span></span> |
| <span data-ttu-id="ba9cd-175">어떤 값</span><span class="sxs-lookup"><span data-stu-id="ba9cd-175">Any value</span></span> |<span data-ttu-id="ba9cd-176">False/지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="ba9cd-176">False/Not Specified</span></span> |<span data-ttu-id="ba9cd-177">400 - 잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="ba9cd-177">400 - Bad Request</span></span> |

## <span data-ttu-id="ba9cd-178"><a name="2.0.0"></a>Azure 모바일 앱 클라이언트 및 서버</span><span class="sxs-lookup"><span data-stu-id="ba9cd-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="ba9cd-179"><a name="MobileAppsClients"></a> 모바일 *앱* 클라이언트 SDK</span><span class="sxs-lookup"><span data-stu-id="ba9cd-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="ba9cd-180">다음 버전의 hello 클라이언트 SDK hello로 시작 도입 된 버전을 확인에 대 한 **Azure 모바일 앱**:</span><span class="sxs-lookup"><span data-stu-id="ba9cd-180">Version checking was introduced starting with hello following versions of hello client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="ba9cd-181">클라이언트 플랫폼</span><span class="sxs-lookup"><span data-stu-id="ba9cd-181">Client platform</span></span> | <span data-ttu-id="ba9cd-182">버전</span><span class="sxs-lookup"><span data-stu-id="ba9cd-182">Version</span></span> | <span data-ttu-id="ba9cd-183">버전 헤더 값</span><span class="sxs-lookup"><span data-stu-id="ba9cd-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba9cd-184">관리된 클라이언트(Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="ba9cd-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="ba9cd-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="ba9cd-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="ba9cd-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="ba9cd-186">2.0.0</span></span> |
| <span data-ttu-id="ba9cd-187">iOS</span><span class="sxs-lookup"><span data-stu-id="ba9cd-187">iOS</span></span> |[<span data-ttu-id="ba9cd-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="ba9cd-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="ba9cd-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="ba9cd-189">2.0.0</span></span> |
| <span data-ttu-id="ba9cd-190">Android</span><span class="sxs-lookup"><span data-stu-id="ba9cd-190">Android</span></span> |[<span data-ttu-id="ba9cd-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="ba9cd-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="ba9cd-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="ba9cd-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="ba9cd-193">모바일 *앱* 서버 SDK</span><span class="sxs-lookup"><span data-stu-id="ba9cd-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="ba9cd-194">버전 검사는 다음 서버 SDK 버전에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba9cd-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="ba9cd-195">서버 플랫폼</span><span class="sxs-lookup"><span data-stu-id="ba9cd-195">Server platform</span></span> | <span data-ttu-id="ba9cd-196">SDK)</span><span class="sxs-lookup"><span data-stu-id="ba9cd-196">SDK</span></span> | <span data-ttu-id="ba9cd-197">수락된 버전 헤더</span><span class="sxs-lookup"><span data-stu-id="ba9cd-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba9cd-198">.NET</span><span class="sxs-lookup"><span data-stu-id="ba9cd-198">.NET</span></span> |[<span data-ttu-id="ba9cd-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="ba9cd-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="ba9cd-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="ba9cd-200">2.0.0</span></span> |
| <span data-ttu-id="ba9cd-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="ba9cd-201">Node.js</span></span> |[<span data-ttu-id="ba9cd-202">azure-mobile-apps)</span><span class="sxs-lookup"><span data-stu-id="ba9cd-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="ba9cd-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="ba9cd-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="ba9cd-204">모바일 앱 백 엔드의 동작</span><span class="sxs-lookup"><span data-stu-id="ba9cd-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="ba9cd-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="ba9cd-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="ba9cd-206">MS_SkipVersionCheck의 값</span><span class="sxs-lookup"><span data-stu-id="ba9cd-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="ba9cd-207">응답</span><span class="sxs-lookup"><span data-stu-id="ba9cd-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba9cd-208">x.y.z 또는 Null</span><span class="sxs-lookup"><span data-stu-id="ba9cd-208">x.y.z or Null</span></span> |<span data-ttu-id="ba9cd-209">True</span><span class="sxs-lookup"><span data-stu-id="ba9cd-209">True</span></span> |<span data-ttu-id="ba9cd-210">200 - 확인</span><span class="sxs-lookup"><span data-stu-id="ba9cd-210">200 - OK</span></span> |
| <span data-ttu-id="ba9cd-211">Null</span><span class="sxs-lookup"><span data-stu-id="ba9cd-211">Null</span></span> |<span data-ttu-id="ba9cd-212">False/지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="ba9cd-212">False/Not Specified</span></span> |<span data-ttu-id="ba9cd-213">400 - 잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="ba9cd-213">400 - Bad Request</span></span> |
| <span data-ttu-id="ba9cd-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="ba9cd-214">1.x.y</span></span> |<span data-ttu-id="ba9cd-215">False/지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="ba9cd-215">False/Not Specified</span></span> |<span data-ttu-id="ba9cd-216">400 - 잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="ba9cd-216">400 - Bad Request</span></span> |
| <span data-ttu-id="ba9cd-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="ba9cd-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="ba9cd-218">False/지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="ba9cd-218">False/Not Specified</span></span> |<span data-ttu-id="ba9cd-219">200 - 확인</span><span class="sxs-lookup"><span data-stu-id="ba9cd-219">200 - OK</span></span> |
| <span data-ttu-id="ba9cd-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="ba9cd-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="ba9cd-221">False/지정되지 않음</span><span class="sxs-lookup"><span data-stu-id="ba9cd-221">False/Not Specified</span></span> |<span data-ttu-id="ba9cd-222">400 - 잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="ba9cd-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ba9cd-223">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ba9cd-223">Next Steps</span></span>
* <span data-ttu-id="ba9cd-224">[모바일 서비스 tooAzure 앱 서비스를 마이그레이션할]</span><span class="sxs-lookup"><span data-stu-id="ba9cd-224">[Migrate a Mobile Service tooAzure App Service]</span></span>

[모바일 서비스 클라이언트]: #MobileServicesClients
[모바일 앱 클라이언트]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[모바일 서비스 tooAzure 앱 서비스를 마이그레이션할]: app-service-mobile-migrating-from-mobile-services.md
