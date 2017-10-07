---
title: "모바일 서비스 tooAzure 앱 서비스에서 aaaUpgrade"
description: "Tooeasily 모바일 서비스 응용 프로그램 tooan 앱 서비스 모바일 앱을 업그레이드 하는 방법에 대해 알아봅니다"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 9c0ac353-afb6-462b-ab94-d91b8247322f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b75a1b824e8ef0d36c9053f2f19af051479f928
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-net-azure-mobile-service-tooapp-service"></a><span data-ttu-id="05abd-103">프로그램 기존.NET Azure 모바일 서비스 tooApp 서비스 업그레이드</span><span class="sxs-lookup"><span data-stu-id="05abd-103">Upgrade your existing .NET Azure Mobile Service tooApp Service</span></span>
<span data-ttu-id="05abd-104">앱 서비스 모바일을 새로운 방식으로 toobuild 모바일 응용 프로그램 Microsoft Azure를 사용 하 여입니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-104">App Service Mobile is a new way toobuild mobile applications using Microsoft Azure.</span></span> <span data-ttu-id="05abd-105">toolearn 더 참조 [모바일 앱 이란?]합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-105">toolearn more, see [What are Mobile Apps?].</span></span>

<span data-ttu-id="05abd-106">이 항목에서는 설명 방법을 tooupgrade tooa Azure 모바일 서비스에서에서 기존.NET 백 엔드 응용 프로그램이 새 앱 서비스 모바일 앱.</span><span class="sxs-lookup"><span data-stu-id="05abd-106">This topic describes how tooupgrade an existing .NET backend application from Azure Mobile Services tooa new App Service Mobile Apps.</span></span> <span data-ttu-id="05abd-107">이 업그레이드를 수행 하는 동안 기존 모바일 서비스 응용 프로그램 toooperate를 계속 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-107">While you perform this upgrade, your existing Mobile Services application can continue toooperate.</span></span>   <span data-ttu-id="05abd-108">Tooupgrade Node.js 백 엔드 응용 프로그램, 필요한 경우 너무 참조[Node.js 모바일 서비스를 업그레이드](app-service-mobile-node-backend-upgrading-from-mobile-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-108">If you need tooupgrade a Node.js backend application, refer too[Upgrading your Node.js Mobile Services](app-service-mobile-node-backend-upgrading-from-mobile-services.md).</span></span>

<span data-ttu-id="05abd-109">너무에 따라 청구 되며 앱 서비스 기능 액세스 tooall 모바일 백 엔드 응용 프로그램 서비스 업그레이드 tooAzure 인 경우에[앱 서비스 가격 책정], 모바일 서비스 가격 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-109">When a mobile backend is upgraded tooAzure App Service, it has access tooall App Service features and are billed according too[App Service pricing], not Mobile Services pricing.</span></span>

## <a name="migrate-vs-upgrade"></a><span data-ttu-id="05abd-110">마이그레이션과 업그레이드 비교</span><span class="sxs-lookup"><span data-stu-id="05abd-110">Migrate vs. upgrade</span></span>
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> <span data-ttu-id="05abd-111">업그레이드를 진행하기 전에 [마이그레이션을 수행](app-service-mobile-migrating-from-mobile-services.md) 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-111">It is recommended that you [perform a migration](app-service-mobile-migrating-from-mobile-services.md) before going through an upgrade.</span></span> <span data-ttu-id="05abd-112">이러한 방식으로 응용 프로그램의 두 버전 모두 넣을 수 있습니다에 동일한 앱 서비스 계획 hello 및 추가 비용 없이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-112">This way, you can put both versions of your application on hello same App Service Plan and incur no additional cost.</span></span>
>
>

### <a name="improvements-in-mobile-apps-net-server-sdk"></a><span data-ttu-id="05abd-113">모바일 앱 .NET 서버 SDK에서 향상된 기능</span><span class="sxs-lookup"><span data-stu-id="05abd-113">Improvements in Mobile Apps .NET server SDK</span></span>
<span data-ttu-id="05abd-114">새 toohello 업그레이드 [모바일 앱 SDK](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-114">Upgrading toohello new [Mobile Apps SDK](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) provides hello following benefits:</span></span>

* <span data-ttu-id="05abd-115">NuGet 종속성에서 유연성이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-115">More flexibility on NuGet dependencies.</span></span> <span data-ttu-id="05abd-116">호스팅 환경에 더 이상 hello 호환 되는 대체 버전을 사용할 수 있도록 고유한 버전의 NuGet 패키지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-116">hello hosting environment no longer provides its own versions of NuGet packages, so you can use alternative compatible versions.</span></span> <span data-ttu-id="05abd-117">그러나 중요 한 새 bugfixes 또는 보안 업데이트 toohello 모바일 서버 SDK 또는 종속성 경우에 서비스에 수동으로 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-117">However, if there are new critical bugfixes or security updates toohello Mobile Server SDK or dependencies, you must update your service manually.</span></span>
* <span data-ttu-id="05abd-118">보다 융통성 있게 hello 모바일 SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-118">More flexibility in hello mobile SDK.</span></span> <span data-ttu-id="05abd-119">기능을 명시적으로 제어할 수 있습니다 및 경로 설정, 인증, Api, 테이블 및 푸시 등록 끝점 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-119">You can explicitly control which features and routes are set up, such as authentication, table APIs, and hello push registration endpoint.</span></span> <span data-ttu-id="05abd-120">toolearn 더 참조 [어떻게 Azure 모바일 앱 용.NET 서버 SDK hello를 toouse](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-120">toolearn more, see [How toouse hello .NET server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>
* <span data-ttu-id="05abd-121">다른 ASP.NET 프로젝트 형식 및 경로를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-121">Support for other ASP.NET project types and routes.</span></span> <span data-ttu-id="05abd-122">이제 모바일 백 엔드 프로젝트와 동일한 프로젝트 hello에 MVC 및 Web API 컨트롤러를 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-122">You can now host MVC and Web API controllers in hello same project as your mobile backend project.</span></span>
* <span data-ttu-id="05abd-123">웹 및 모바일 앱에서 일반적인 인증 구성을 toouse 수 있게 해 주는 새 앱 서비스 인증 기능에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="05abd-123">Support for new App Service authentication features, which allow you toouse a common authentication configuration across your web and mobile apps.</span></span>

## <span data-ttu-id="05abd-124"><a name="overview"></a>기본 업그레이드 개요</span><span class="sxs-lookup"><span data-stu-id="05abd-124"><a name="overview"></a>Basic upgrade overview</span></span>
<span data-ttu-id="05abd-125">대부분의 경우에서 업그레이드는 처럼 간단할 toohello 새 모바일 앱 서버 SDK를 전환 하 고 새 모바일 앱 인스턴스로 코드를 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-125">In many cases, upgrading will be as simple as switching toohello new Mobile Apps server SDK and republishing your code onto a new Mobile App instance.</span></span> <span data-ttu-id="05abd-126">그러나 고급 인증 시나리오 및 예약된 작업 사용과 같이 추가 구성이 필요한 일부 시나리오도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-126">There are, however some scenarios which will require some additional configuration, such as advanced authentication scenarios and working with scheduled jobs.</span></span> <span data-ttu-id="05abd-127">이러한 각 hello에 대해서는 나중에 섹션.</span><span class="sxs-lookup"><span data-stu-id="05abd-127">Each of these is covered in hello later sections.</span></span>

> [!TIP]
> <span data-ttu-id="05abd-128">읽기 및 업그레이드를 시작 하기 전에이 항목의 나머지 부분 hello를 완전히 이해 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-128">It is advised that you read and understand hello rest of this topic completely before starting an upgrade.</span></span> <span data-ttu-id="05abd-129">아래 설명선에 표시된 사용하는 기능을 모두 기록해 두세요.</span><span class="sxs-lookup"><span data-stu-id="05abd-129">Make note of any features you use which are called out below.</span></span>
>
>

<span data-ttu-id="05abd-130">hello 모바일 서비스 클라이언트 Sdk는 **하지** hello 새로운 모바일 앱 서버 SDK와 호환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-130">hello Mobile Services client SDKs are **not** compatible with hello new Mobile Apps server SDK.</span></span> <span data-ttu-id="05abd-131">앱에 대 한 서비스, 순서 tooprovide 지속적인 하지 변경 tooa 사이트에서는 현재 게시 된 클라이언트를 게시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-131">In order tooprovide continuity of service for your app, you should not publish changes tooa site currently serving published clients.</span></span> <span data-ttu-id="05abd-132">대신 중복으로 제공한 새 모바일 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-132">Instead, you should create a new mobile app that serves as a duplicate.</span></span> <span data-ttu-id="05abd-133">이 응용 프로그램을 넣을 수 hello에서 동일한 앱 서비스 계획 tooavoid 재무 추가 비용 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-133">You can put this application on hello same App Service plan tooavoid incurring additional financial cost.</span></span>

<span data-ttu-id="05abd-134">다음 두 가지 버전 hello 응용 프로그램의: 하나는 유지 되며 동일 hello 및 새 클라이언트 릴리스로 업그레이드할 때는 다른 및 대상 hello 와일드 카드, 및 hello에 게시 된 앱을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-134">You will then have two versions of hello application: one which stays hello same and serves published apps in hello wild, and hello other which you can then upgrade and target with a new client release.</span></span> <span data-ttu-id="05abd-135">이동 하 고, 속도로 코드를 테스트할 수 있지만 그러면 만들면 버그 수정 사항이 적용 된 tooboth을 가져올 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-135">You can move and test your code at your pace, but you should make sure that any bug fixes you make get applied tooboth.</span></span> <span data-ttu-id="05abd-136">원하는 수의 hello 와일드 카드에 클라이언트 앱 toohello 최신 버전 업데이트, 원하는 경우 hello 원래 마이그레이션된 응용 프로그램을 삭제할 수 있습니다 수 있다고 생각 되 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-136">Once you feel that a desired number of client apps in hello wild have updated toohello latest version, you can delete hello original migrated app if you desire.</span></span>

<span data-ttu-id="05abd-137">hello hello 업그레이드 프로세스에 대 한 전체 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-137">hello full outline for hello upgrade process is as follows:</span></span>

1. <span data-ttu-id="05abd-138">새 모바일 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="05abd-138">Create a new Mobile App</span></span>
2. <span data-ttu-id="05abd-139">업데이트 hello 프로젝트 toouse hello 새로운 서버 Sdk</span><span class="sxs-lookup"><span data-stu-id="05abd-139">Update hello project toouse hello new Server SDKs</span></span>
3. <span data-ttu-id="05abd-140">새 버전의 클라이언트 응용 프로그램 릴리스</span><span class="sxs-lookup"><span data-stu-id="05abd-140">Release a new version of your client application</span></span>
4. <span data-ttu-id="05abd-141">(선택 사항) 원래 마이그레이션된 인스턴스 삭제</span><span class="sxs-lookup"><span data-stu-id="05abd-141">(Optional) Delete your original migrated instance</span></span>

## <span data-ttu-id="05abd-142"><a name="mobile-app-version"></a>두 번째 응용 프로그램 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="05abd-142"><a name="mobile-app-version"></a>Creating a second application instance</span></span>
<span data-ttu-id="05abd-143">hello 업그레이드할 때의 첫 번째 단계는 hello 새 버전의 응용 프로그램을 호스팅하려는 toocreate hello 모바일 응용 프로그램 리소스.</span><span class="sxs-lookup"><span data-stu-id="05abd-143">hello first step in upgrading is toocreate hello Mobile App resource which will host hello new version of your application.</span></span> <span data-ttu-id="05abd-144">기존 모바일 서비스를 이미 마이그레이션한 경우 좋습니다 toocreate hello이이 버전과 동일한 호스팅 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-144">If you have already migrated an existing mobile service, you will want toocreate this version on hello same hosting plan.</span></span> <span data-ttu-id="05abd-145">열기 hello [Azure 포털] tooyour 탐색 및 응용 프로그램 마이그레이션.</span><span class="sxs-lookup"><span data-stu-id="05abd-145">Open hello [Azure portal] and navigate tooyour migrated application.</span></span> <span data-ttu-id="05abd-146">앱 서비스 계획에서 실행 되는 hello를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-146">Make note of hello App Service Plan it is running on.</span></span>

<span data-ttu-id="05abd-147">다음으로, 다음 hello hello 두 번째 응용 프로그램 인스턴스를 만들 [.NET 백 엔드 만들기 지침](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app)합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-147">Next, create hello second application instance by following hello [.NET backend creation instructions](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app).</span></span> <span data-ttu-id="05abd-148">때 선택 하면 앱 서비스 계획 또는 "계획 호스팅" 증명된 tooselect hello 마이그레이션된 응용 프로그램의 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-148">When prompted tooselect you App Service Plan or "hosting plan" choose hello plan of your migrated application.</span></span>

<span data-ttu-id="05abd-149">Toouse hello 동일한 데이터베이스와 알림 허브와 모바일 서비스에서 수행한 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-149">You will likely want toouse hello same database and Notification Hub as you did in Mobile Services.</span></span> <span data-ttu-id="05abd-150">열어 이러한 값을 복사할 수는 있지만 [Azure 포털] toohello 원래 응용 프로그램 탐색을 클릭 하 고 **설정** > **응용 프로그램 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-150">You can copy these values by opening [Azure portal] and navigating toohello original application, then click **Settings** > **Application settings**.</span></span> <span data-ttu-id="05abd-151">**연결 문자열**에서 `MS_NotificationHubConnectionString` 및 `MS_TableConnectionString`을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-151">Under **Connection Strings**, copy `MS_NotificationHubConnectionString` and `MS_TableConnectionString`.</span></span> <span data-ttu-id="05abd-152">새 업그레이드 사이트 tooyour 이동한 모든 기존 값 덮어쓰기에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-152">Navigate tooyour new upgrade site and paste them in, overwriting any existing values.</span></span> <span data-ttu-id="05abd-153">앱에 필요한 다른 응용 프로그램 설정에 이 프로세스를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-153">Repeat this process for any other application settings your app needs.</span></span> <span data-ttu-id="05abd-154">연결 문자열 및 응용 프로그램 설정을 hello에서 읽을 수는 마이그레이션된 서비스를 사용 하지 **구성** hello hello의 모바일 서비스 섹션의 탭 [Azure 클래식 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-154">If not using a migrated service, you can read connection strings and app settings from hello **Configure** tab of hello Mobile Services section of hello [Azure classic portal].</span></span>

<span data-ttu-id="05abd-155">응용 프로그램에 대 한 hello ASP.NET 프로젝트의 복사본을 만들고 tooyour 새 사이트를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-155">Make a copy of hello ASP.NET project for your application and publish it tooyour new site.</span></span> <span data-ttu-id="05abd-156">Hello 새 URL로 업데이트 하는 클라이언트 응용 프로그램의 복사본을 사용 하 여 예상 대로 작동 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-156">Using a copy of your client application updated with hello new URL, validate that everything works as expected.</span></span>

## <a name="updating-hello-server-project"></a><span data-ttu-id="05abd-157">Hello 서버 프로젝트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-157">Updating hello server project</span></span>
<span data-ttu-id="05abd-158">모바일 앱 제공 새 [모바일 앱 서버 SDK] hello 많이 제공 하는 모바일 서비스 런타임 hello와 동일한 기능을 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-158">Mobile Apps provides a new [Mobile App Server SDK] which provides much of hello same functionality as hello Mobile Services runtime.</span></span> <span data-ttu-id="05abd-159">첫째, 모든 참조 toohello 모바일 서비스 패키지를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-159">First, you should remove all references toohello Mobile Services packages.</span></span> <span data-ttu-id="05abd-160">Hello NuGet 패키지 관리자에서 검색 `WindowsAzure.MobileServices.Backend`합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-160">In hello NuGet package manager, search for `WindowsAzure.MobileServices.Backend`.</span></span> <span data-ttu-id="05abd-161">대부분의 앱에서 `WindowsAzure.MobileServices.Backend.Tables` 및 `WindowsAzure.MobileServices.Backend.Entity`를 포함하여 여러 패키지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-161">Most apps will see several packages here, including `WindowsAzure.MobileServices.Backend.Tables` and `WindowsAzure.MobileServices.Backend.Entity`.</span></span> <span data-ttu-id="05abd-162">이 경우 시작 hello 종속성 트리에서 hello 가장 낮은 패키지와 같은 `Entity`, 하 고 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-162">In such a case, start with hello lowest package in hello dependency tree, such as `Entity`, and remove it.</span></span> <span data-ttu-id="05abd-163">메시지가 표시되면 모든 종속 패키지를 제거하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="05abd-163">When prompted, do not remove all dependant packages.</span></span> <span data-ttu-id="05abd-164">`WindowsAzure.MobileServices.Backend` 자체를 제거할 때까지 이 프로세스를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-164">Repeat this process until you have removed `WindowsAzure.MobileServices.Backend` itself.</span></span>

<span data-ttu-id="05abd-165">이 시점에서 더 이상 모바일 서비스 SDK를 참조하지 않는 프로젝트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-165">At this point you will have a project that no longer references Mobile Services SDKs.</span></span>

<span data-ttu-id="05abd-166">다음 참조 hello 모바일 앱 SDK를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-166">Next you will add references hello Mobile Apps SDK.</span></span> <span data-ttu-id="05abd-167">이 업그레이드에 대 한 대부분의 개발자는 toodownload 원하고 hello 설치 `Microsoft.Azure.Mobile.Server.Quickstart` hello 전체 필요한 집합에서 끌어오고이으로 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-167">For this upgrade, most developers will want toodownload and install hello `Microsoft.Azure.Mobile.Server.Quickstart` package, as this will pull in hello entire required set.</span></span>

<span data-ttu-id="05abd-168">Hello Sdk 간의 차이로 인해 발생 한 몇몇 컴파일러 오류가 이지만 hello이이 단원의 나머지 부분에 대해서는 설명를 쉽게 tooaddress 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-168">There will be quite a few compiler errors resulting from differences between hello SDKs, but these are easy tooaddress and are covered in hello rest of this section.</span></span>

### <a name="base-configuration"></a><span data-ttu-id="05abd-169">기본 구성</span><span class="sxs-lookup"><span data-stu-id="05abd-169">Base configuration</span></span>
<span data-ttu-id="05abd-170">그런 다음 WebApiConfig.cs에서</span><span class="sxs-lookup"><span data-stu-id="05abd-170">Then, in WebApiConfig.cs, you can replace:</span></span>

        // Use this class tooset configuration options for your mobile service
        ConfigOptions options = new ConfigOptions();

        // Use this class tooset WebAPI configuration options
        HttpConfiguration config = ServiceConfig.Initialize(new ConfigBuilder(options));

<span data-ttu-id="05abd-171">다음으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-171">with</span></span>

        HttpConfiguration config = new HttpConfiguration();
        new MobileAppConfiguration()
            .UseDefaultConfiguration()
        .ApplyTo(config);

> [!NOTE]
> <span data-ttu-id="05abd-172">원할 경우 toolearn hello 새.NET 서버 SDK 및 앱에서 기능이 tooadd/제거 하는 방법에 대 한 hello를 참조 하십시오 [어떻게 toouse hello.NET 서버 SDK] 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-172">If you wish toolearn more about hello new .NET server SDK and how tooadd/remove features from your app, please see hello [How toouse hello .NET server SDK] topic.</span></span>
>
>

<span data-ttu-id="05abd-173">응용 프로그램 정하는 경우 hello 인증 기능을 사용, tooregister OWIN 미들웨어 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-173">If your app makes use of hello authentication features, you will also need tooregister an OWIN middleware.</span></span> <span data-ttu-id="05abd-174">이 경우 새 OWIN 시작 클래스로 구성 코드 위의 hello를 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-174">In this case, you should move hello above configuration code into a new OWIN Startup class.</span></span>

1. <span data-ttu-id="05abd-175">Hello NuGet 패키지 추가 `Microsoft.Owin.Host.SystemWeb` 프로젝트에 아직 포함 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="05abd-175">Add hello NuGet package `Microsoft.Owin.Host.SystemWeb` if it is not already included in your project.</span></span>
2. <span data-ttu-id="05abd-176">Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** -> **새 항목**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-176">In Visual Studio, right click on your project and select **Add** -> **New Item**.</span></span> <span data-ttu-id="05abd-177">**웹** -> **일반** -> **OWIN 시작 클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-177">Select **Web** -> **General** -> **OWIN Startup class**.</span></span>
3. <span data-ttu-id="05abd-178">MobileAppConfiguration에 대 한 코드 위의 hello 이동 `WebApiConfig.Register()` toohello `Configuration()` 새 시작 클래스의 메서드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-178">Move hello above code for MobileAppConfiguration from `WebApiConfig.Register()` toohello `Configuration()` method of your new startup class.</span></span>

<span data-ttu-id="05abd-179">있는지 hello 확인 `Configuration()` 메서드로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-179">Make sure hello `Configuration()` method ends with:</span></span>

        app.UseWebApi(config)
        app.UseAppServiceAuthentication(config);

<span data-ttu-id="05abd-180">아래의 hello full 인증 섹션에서 다루는 관련된 tooauthentication 추가 변경 내용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-180">There are additional changes related tooauthentication which are covered in hello full authentication section below.</span></span>

### <a name="working-with-data"></a><span data-ttu-id="05abd-181">데이터 작업</span><span class="sxs-lookup"><span data-stu-id="05abd-181">Working with Data</span></span>
<span data-ttu-id="05abd-182">모바일 서비스에서 hello 모바일 응용 프로그램 이름 hello Entity Framework 설치 프로그램에서 hello 기본 스키마 이름으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-182">In Mobile Services, hello mobile app name served as hello default schema name in hello Entity Framework setup.</span></span>

<span data-ttu-id="05abd-183">동일 해야 하는 tooensure hello 참조 스키마 되 고 이전 처럼 응용 프로그램에 대 한 hello DbContext에서에서 tooset hello 스키마를 따르는 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="05abd-183">tooensure that you have hello same schema being referenced as before, use hello following tooset hello schema in hello DbContext for your application:</span></span>

        string schema = System.Configuration.ConfigurationManager.AppSettings.Get("MS_MobileServiceName");

<span data-ttu-id="05abd-184">MS_MobileServiceName 위에 hello 수행 하는 경우에 설정 되어 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="05abd-184">Please make sure you have MS_MobileServiceName set if you do hello above.</span></span> <span data-ttu-id="05abd-185">또한 응용 프로그램이 이전에 사용자 지정한 경우 다른 스키마 이름을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-185">You can also provide another schema name if your application customized this previously.</span></span>

### <a name="system-properties"></a><span data-ttu-id="05abd-186">시스템 속성</span><span class="sxs-lookup"><span data-stu-id="05abd-186">System Properties</span></span>
#### <a name="naming"></a><span data-ttu-id="05abd-187">이름 지정</span><span class="sxs-lookup"><span data-stu-id="05abd-187">Naming</span></span>
<span data-ttu-id="05abd-188">Hello Azure 모바일 서비스 서버 SDK, 시스템 속성에에서 항상 포함 되는 두 개의 밑줄이 (`__`) hello 속성에 대 한 접두사:</span><span class="sxs-lookup"><span data-stu-id="05abd-188">In hello Azure Mobile Services server SDK, system properties always contain a double underscore (`__`) prefix for hello properties:</span></span>

* <span data-ttu-id="05abd-189">__createdAt</span><span class="sxs-lookup"><span data-stu-id="05abd-189">__createdAt</span></span>
* <span data-ttu-id="05abd-190">__updatedAt</span><span class="sxs-lookup"><span data-stu-id="05abd-190">__updatedAt</span></span>
* <span data-ttu-id="05abd-191">__deleted</span><span class="sxs-lookup"><span data-stu-id="05abd-191">__deleted</span></span>
* <span data-ttu-id="05abd-192">__version</span><span class="sxs-lookup"><span data-stu-id="05abd-192">__version</span></span>

<span data-ttu-id="05abd-193">hello 모바일 서비스 클라이언트 Sdk가이 형식의 시스템 속성을 구문 분석 하기 위한 특수 논리가 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-193">hello Mobile Services client SDKs have special logic for parsing system properties in this format.</span></span>

<span data-ttu-id="05abd-194">시스템 속성 Azure 모바일 앱에는 특수 한 서식을 지정 하 고 있는 hello 이름 다음에 더 이상:</span><span class="sxs-lookup"><span data-stu-id="05abd-194">In Azure Mobile Apps, system properties no longer have a special format and have hello following names:</span></span>

* <span data-ttu-id="05abd-195">createdAt</span><span class="sxs-lookup"><span data-stu-id="05abd-195">createdAt</span></span>
* <span data-ttu-id="05abd-196">updatedAt</span><span class="sxs-lookup"><span data-stu-id="05abd-196">updatedAt</span></span>
* <span data-ttu-id="05abd-197">deleted</span><span class="sxs-lookup"><span data-stu-id="05abd-197">deleted</span></span>
* <span data-ttu-id="05abd-198">버전</span><span class="sxs-lookup"><span data-stu-id="05abd-198">version</span></span>

<span data-ttu-id="05abd-199">hello 모바일 앱 클라이언트 Sdk 사용 하 여 hello 새 시스템 속성 이름은 변경 되지 않으므로 tooclient 코드가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-199">hello Mobile Apps client SDKs use hello new system properties names, so no changes are required tooclient code.</span></span> <span data-ttu-id="05abd-200">그러나 직접 있다면 tooyour 서비스를 호출한 REST을 만드는 다음 쿼리를 적절 하 게 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-200">However, if you are directly making REST calls tooyour service then you should change your queries accordingly.</span></span>

#### <a name="local-store"></a><span data-ttu-id="05abd-201">로컬 저장소</span><span class="sxs-lookup"><span data-stu-id="05abd-201">Local store</span></span>
<span data-ttu-id="05abd-202">시스템 속성 변경 내용을 toohello 이름을 hello 의미 모바일 서비스에 대 한 오프 라인 동기화 로컬 데이터베이스는 모바일 앱와 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-202">hello changes toohello names of system properties mean that an offline sync local database for Mobile Services is not compatible with Mobile Apps.</span></span> <span data-ttu-id="05abd-203">가능 하면 모바일 서비스 tooMobile 보류 중인 변경 내용이 후까지 앱 보냈습니다 toohello 서버에서에서 클라이언트 응용 프로그램을 업그레이드 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="05abd-203">If possible, you should avoid upgrading client apps from Mobile Services tooMobile Apps until after pending changes have been sent toohello server.</span></span> <span data-ttu-id="05abd-204">그런 다음 hello 업그레이드 된 응용 프로그램에는 새 데이터베이스 파일 이름을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-204">Then, hello upgraded app should use a new database filename.</span></span>

<span data-ttu-id="05abd-205">Hello 작업 큐에 오프 라인 변경 내용이 보류 중인 동안 tooMobile 모바일 서비스 응용 프로그램에서에서 업그레이드 되는 클라이언트 응용 프로그램 hello 시스템 데이터베이스에서 업데이트 된 toouse hello 새 열 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-205">If a client app is upgraded from Mobile Services tooMobile Apps while there are pending offline changes in hello operation queue, then hello system database must be updated toouse hello new column names.</span></span> <span data-ttu-id="05abd-206">Ios, 이렇게 간단한 마이그레이션을 toochange hello 열 이름을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-206">On iOS, this can be achieved using lightweight migrations toochange hello column names.</span></span> <span data-ttu-id="05abd-207">Android 및 hello.NET 관리 되는 클라이언트에 데이터 개체 테이블에 대 한 사용자 지정 SQL toorename에 hello 열 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-207">On Android and hello .NET managed client, you should write custom SQL toorename hello columns for your data object tables.</span></span>

<span data-ttu-id="05abd-208">Ios, 사용자 데이터 엔터티 toomatch hello 다음에 대 한 핵심 데이터 스키마를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-208">On iOS, you should change your Core Data schema for your data entities toomatch hello following.</span></span> <span data-ttu-id="05abd-209">속성을 hello 참고 `createdAt`, `updatedAt` 및 `version` 더 이상는 `ms_` 접두사:</span><span class="sxs-lookup"><span data-stu-id="05abd-209">Note that hello properties `createdAt`, `updatedAt` and `version` no longer have an `ms_` prefix:</span></span>

| <span data-ttu-id="05abd-210">특성</span><span class="sxs-lookup"><span data-stu-id="05abd-210">Attribute</span></span> | <span data-ttu-id="05abd-211">유형</span><span class="sxs-lookup"><span data-stu-id="05abd-211">Type</span></span> | <span data-ttu-id="05abd-212">참고</span><span class="sxs-lookup"><span data-stu-id="05abd-212">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05abd-213">id</span><span class="sxs-lookup"><span data-stu-id="05abd-213">id</span></span> |<span data-ttu-id="05abd-214">문자열, 필수로 표시</span><span class="sxs-lookup"><span data-stu-id="05abd-214">String, marked required</span></span> |<span data-ttu-id="05abd-215">원격 저장소의 기본 키</span><span class="sxs-lookup"><span data-stu-id="05abd-215">primary key in remote store</span></span> |
| <span data-ttu-id="05abd-216">createdAt</span><span class="sxs-lookup"><span data-stu-id="05abd-216">createdAt</span></span> |<span data-ttu-id="05abd-217">Date</span><span class="sxs-lookup"><span data-stu-id="05abd-217">Date</span></span> |<span data-ttu-id="05abd-218">(선택 사항) 지도 toocreatedAt 시스템 속성</span><span class="sxs-lookup"><span data-stu-id="05abd-218">(optional) maps toocreatedAt system property</span></span> |
| <span data-ttu-id="05abd-219">updatedAt</span><span class="sxs-lookup"><span data-stu-id="05abd-219">updatedAt</span></span> |<span data-ttu-id="05abd-220">Date</span><span class="sxs-lookup"><span data-stu-id="05abd-220">Date</span></span> |<span data-ttu-id="05abd-221">(선택 사항) 지도 tooupdatedAt 시스템 속성</span><span class="sxs-lookup"><span data-stu-id="05abd-221">(optional) maps tooupdatedAt system property</span></span> |
| <span data-ttu-id="05abd-222">버전</span><span class="sxs-lookup"><span data-stu-id="05abd-222">version</span></span> |<span data-ttu-id="05abd-223">문자열</span><span class="sxs-lookup"><span data-stu-id="05abd-223">String</span></span> |<span data-ttu-id="05abd-224">(선택 사항) 사용 하는 toodetect 충돌, 지도 tooversion</span><span class="sxs-lookup"><span data-stu-id="05abd-224">(optional) used toodetect conflicts, maps tooversion</span></span> |

#### <a name="querying-system-properties"></a><span data-ttu-id="05abd-225">시스템 속성 쿼리</span><span class="sxs-lookup"><span data-stu-id="05abd-225">Querying system properties</span></span>
<span data-ttu-id="05abd-226">Azure 모바일 서비스에서 시스템 속성은 전송 되지 기본적으로 하지만 쿼리 문자열 hello를 사용 하 여 요청 된 경우에 `__systemProperties`합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-226">In Azure Mobile Services, system properties are not sent by default, but only when they are requested using hello query string `__systemProperties`.</span></span> <span data-ttu-id="05abd-227">Azure 모바일 앱 시스템 속성은 한 반면 **항상 선택** 속하므로 hello 서버 SDK 개체 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-227">In contrast, in Azure Mobile Apps system properties are **always selected** since they are part of hello server SDK object model.</span></span>

<span data-ttu-id="05abd-228">이 변경 사항은 `MappedEntityDomainManager`의 확장과 같은 도메인 관리자의 사용자 지정 구현에 주로 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-228">This change mainly impacts custom implementations of domain managers, such as extensions of `MappedEntityDomainManager`.</span></span> <span data-ttu-id="05abd-229">모바일 서비스에서 클라이언트는 하지 모든 시스템 속성을 요청할 경우 가능한 toouse는 `MappedEntityDomainManager` 모든 속성이 실제로 매핑되지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-229">In Mobile Services, if a client never requests any system properties, it is possible toouse a `MappedEntityDomainManager` that does not actually map all properties.</span></span> <span data-ttu-id="05abd-230">그러나 Azure 모바일 앱에서 이러한 매핑되지 않은 속성은 가져오기 쿼리에서 오류를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-230">However, in Azure Mobile Apps, these unmapped properties will cause an error in GET queries.</span></span>

<span data-ttu-id="05abd-231">가장 쉬운 방법은 tooresolve hello 문제 hello에서 상속 되도록 toomodify 프로그램 Dto는 `ITableData` 대신 `EntityData`합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-231">hello easiest way tooresolve hello issue is toomodify your DTOs so that they inherit from `ITableData` instead of `EntityData`.</span></span> <span data-ttu-id="05abd-232">그런 다음 추가 hello `[NotMapped]` 생략 해야 toohello 필드 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-232">Then, add hello `[NotMapped]` attribute toohello fields that should be omitted.</span></span>

<span data-ttu-id="05abd-233">예를 들어 hello 다음 정의 `TodoItem` 시스템 속성이 없는:</span><span class="sxs-lookup"><span data-stu-id="05abd-233">For example, hello following defines `TodoItem` with no system properties:</span></span>

    using System.ComponentModel.DataAnnotations.Schema;

    public class TodoItem : ITableData
    {
        public string Text { get; set; }

        public bool Complete { get; set; }

        public string Id { get; set; }

        [NotMapped]
        public DateTimeOffset? CreatedAt { get; set; }

        [NotMapped]
        public DateTimeOffset? UpdatedAt { get; set; }

        [NotMapped]
        public bool Deleted { get; set; }

        [NotMapped]
        public byte[] Version { get; set; }
    }

<span data-ttu-id="05abd-234">참고:에 오류가 발생 하는 경우 `NotMapped`, 참조 toohello 어셈블리 추가 `System.ComponentModel.DataAnnotations`합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-234">Note: if you get errors on `NotMapped`, add a reference toohello assembly `System.ComponentModel.DataAnnotations`.</span></span>

### <a name="cors"></a><span data-ttu-id="05abd-235">CORS</span><span class="sxs-lookup"><span data-stu-id="05abd-235">CORS</span></span>
<span data-ttu-id="05abd-236">모바일 서비스에는 ASP.NET CORS 솔루션 hello를 래핑하여 CORS에 대 한 지원이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-236">Mobile Services included some support for CORS by wrapping hello ASP.NET CORS solution.</span></span> <span data-ttu-id="05abd-237">이 배치 계층은 되었으므로 제거 toogive hello 개발자 자세히 제어할 직접 활용할 수 있습니다 [ASP.NET CORS 지원](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-237">This wrapping layer has been removed toogive hello developer more control, so you can directly leverage [ASP.NET CORS support](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

<span data-ttu-id="05abd-238">hello 주 관련 CORS를 사용 하는 경우 영역은 해당 hello `eTag` 및 `Location` hello 클라이언트 Sdk toowork 되려면에서 제대로 헤더를 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-238">hello main areas of concern if using CORS are that hello `eTag` and `Location` headers must be allowed in order for hello client SDKs toowork properly.</span></span>

### <a name="push-notifications"></a><span data-ttu-id="05abd-239">푸시 알림</span><span class="sxs-lookup"><span data-stu-id="05abd-239">Push Notifications</span></span>
<span data-ttu-id="05abd-240">푸시에 대 한 hello 서버 SDK에서에서 누락 될 수 있는 hello 주 항목에는 hello PushRegistrationHandler 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-240">For push, hello main item that you may find missing from hello Server SDK is hello PushRegistrationHandler class.</span></span> <span data-ttu-id="05abd-241">모바일 앱에서는 등록이 약간 다르게 처리되며, 기본적으로 태그 없는 등록이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-241">Registrations are handled slightly differently in Mobile Apps, and tagless registrations are enabled by default.</span></span> <span data-ttu-id="05abd-242">사용자 지정 API를 통해 태그를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-242">Managing tags may be accomplished by using custom APIs.</span></span> <span data-ttu-id="05abd-243">Hello를 참조 하십시오 [태그에 대 한 등록](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags) 자세한 정보에 대 한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-243">Please see hello [registering for tags](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags) instructions for more information.</span></span>

### <a name="scheduled-jobs"></a><span data-ttu-id="05abd-244">예약된 작업</span><span class="sxs-lookup"><span data-stu-id="05abd-244">Scheduled Jobs</span></span>
<span data-ttu-id="05abd-245">.NET 백 엔드에 있는 모든 기존 작업 toobe 개별적으로 업그레이드할 필요 하므로 예약 된 작업은 모바일 앱에 빌드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-245">Scheduled jobs are not built into Mobile Apps, so any existing jobs that you have in your .NET backend will need toobe upgraded individually.</span></span> <span data-ttu-id="05abd-246">한 가지 옵션은 예약된 된 toocreate [웹 작업] hello 모바일 응용 프로그램 코드 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-246">One option is toocreate a scheduled [Web Job] on hello Mobile App code site.</span></span> <span data-ttu-id="05abd-247">또한 작업 코드를 보유 하는 컨트롤러를 설정 하 고 hello 구성 수 [Azure 스케줄러] toohit 예상 hello 일정에 따라 해당 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-247">You could also set up a controller that holds your job code and configure hello [Azure Scheduler] toohit that endpoint on hello expected schedule.</span></span>

### <a name="miscellaneous-changes"></a><span data-ttu-id="05abd-248">기타 변경 내용</span><span class="sxs-lookup"><span data-stu-id="05abd-248">Miscellaneous changes</span></span>
<span data-ttu-id="05abd-249">모바일 클라이언트에서 사용 될 수 있는 모든 ApiControllers 이제 hello 있어야 `[MobileAppController]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-249">All ApiControllers which will be consumed by a mobile client must now have hello `[MobileAppController]` attribute.</span></span> <span data-ttu-id="05abd-250">더 이상 영향을 받지 다른 ApiControllers toogo hello 모바일 포맷터를 기본적으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-250">This is no longer included by default so that other ApiControllers toogo unaffected by hello mobile formatters.</span></span>

<span data-ttu-id="05abd-251">hello `ApiServices` 개체는 더 이상 hello SDK의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-251">hello `ApiServices` object is no longer part of hello SDK.</span></span> <span data-ttu-id="05abd-252">모바일 앱 설정 tooaccess hello 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-252">tooaccess Mobile App settings, you can use hello following:</span></span>

    MobileAppSettingsDictionary settings = this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

<span data-ttu-id="05abd-253">마찬가지로, 로깅 이제 현재 hello 표준 ASP.NET 추적 쓰기:</span><span class="sxs-lookup"><span data-stu-id="05abd-253">Similarly, logging is now accomplished using hello standard ASP.NET trace writing:</span></span>

    ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
    traceWriter.Info("Hello, World");  

## <span data-ttu-id="05abd-254"><a name="authentication"></a>인증 고려 사항</span><span class="sxs-lookup"><span data-stu-id="05abd-254"><a name="authentication"></a>Authentication considerations</span></span>
<span data-ttu-id="05abd-255">이제 모바일 서비스의 인증 구성 요소 hello hello 응용 프로그램 서비스 인증/권한 부여 기능으로 이동 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-255">hello authentication components of Mobile Services have now been moved into hello App Service Authentication/Authorization feature.</span></span> <span data-ttu-id="05abd-256">읽는 hello 하 여 사이트에 대 한이 기능을 사용 하는 방법에 대 한 학습할 수 있는 [추가 인증 tooyour 모바일 앱](app-service-mobile-ios-get-started-users.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-256">You can learn about enabling this for your site by reading hello [Add authentication tooyour mobile app](app-service-mobile-ios-get-started-users.md) topic.</span></span>

<span data-ttu-id="05abd-257">AAD, Facebook, Google, 등의 일부 공급자에 대 한 복사 응용 프로그램에서 수 tooleverage hello 기존 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-257">For some providers, such as AAD, Facebook, and Google, you should be able tooleverage hello existing registration from your copy application.</span></span> <span data-ttu-id="05abd-258">단순히 toonavigate toohello id 공급자의 포털 필요 하 고 새 리디렉션 URL toohello 등록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-258">You simply need toonavigate toohello identity provider's portal and add a new redirect URL toohello registration.</span></span> <span data-ttu-id="05abd-259">Hello 클라이언트 ID와 암호가 있는 응용 프로그램 서비스 인증/권한 부여를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-259">Then configure App Service Authentication/Authorization with hello client ID and secret.</span></span>

### <a name="controller-action-authorization"></a><span data-ttu-id="05abd-260">컨트롤러 작업 권한 부여</span><span class="sxs-lookup"><span data-stu-id="05abd-260">Controller action authorization</span></span>
<span data-ttu-id="05abd-261">Hello의 인스턴스를 모두 `[AuthorizeLevel(AuthorizationLevel.User)]` 특성에서 변경 된 toouse 이제 해야 표준 ASP.NET hello `[Authorize]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-261">Any instances of hello `[AuthorizeLevel(AuthorizationLevel.User)]` attribute must now be changed toouse hello standard ASP.NET `[Authorize]` attribute.</span></span> <span data-ttu-id="05abd-262">또한 컨트롤러는 다른 ASP.NET 응용 프로그램에서와 같이 이제 기본적으로 익명입니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-262">Additionally, controllers are now Anonymous by default, as in other ASP.NET applications.</span></span>
<span data-ttu-id="05abd-263">Hello 중 하나를 사용 하 던 관리자 또는 응용 프로그램 등의 다른 AuthorizeLevel 옵션 걸어 이러한 사라지게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-263">If you were using one of hello other AuthorizeLevel options, such as Admin or Application, please note that these are gone.</span></span> <span data-ttu-id="05abd-264">대신 공유 암호에 대 한 AuthorizationFilters를 설정 하거나 AAD 서비스 사용자 tooenable 서비스 간 호출을 안전 하 게 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-264">You can instead set up AuthorizationFilters for shared secrets or configure an AAD Service Principal tooenable service-to-service calls securely.</span></span>

### <a name="getting-additional-user-information"></a><span data-ttu-id="05abd-265">추가 사용자 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="05abd-265">Getting additional user information</span></span>
<span data-ttu-id="05abd-266">Hello 통해 액세스 토큰을 포함 하 여 추가 사용자 정보를 얻을 수 `GetAppServiceIdentityAsync()` 메서드:</span><span class="sxs-lookup"><span data-stu-id="05abd-266">You can get additional user information, including access tokens through hello `GetAppServiceIdentityAsync()` method:</span></span>

        FacebookCredentials creds = await this.User.GetAppServiceIdentityAsync<FacebookCredentials>();

<span data-ttu-id="05abd-267">또한 응용 프로그램은 데이터베이스에서이 저장 하는 등 사용자 Id에 종속성을 하는 경우 반드시 모바일 서비스와 앱 서비스 모바일 앱 간 사용자 Id를 hello toonote 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-267">Additionally, if your application takes dependencies on user IDs, such as storing them in a database, it is important toonote that hello user IDs between Mobile Services and App Service Mobile Apps are different.</span></span> <span data-ttu-id="05abd-268">여전히 hello Mobile Services 사용자 ID를 통해 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-268">You can still get hello Mobile Services User ID, though.</span></span> <span data-ttu-id="05abd-269">Hello ProviderCredentials 하위 클래스의 모든 사용자 Id 속성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-269">All of hello ProviderCredentials subclasses have a UserId property.</span></span> <span data-ttu-id="05abd-270">따라서 하기 전에 hello 예제에서 계속 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-270">So continuing from hello example before:</span></span>

        string mobileServicesUserId = creds.Provider + ":" + creds.UserId;

<span data-ttu-id="05abd-271">앱에서 모든 종속성에 사용자 Id 사용 하는 경우 반드시 활용 가능한 경우 id 공급자와 같은 등록 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-271">If your app does take any dependencies on user IDs, it is important that you leverage hello same registration with an identity provider if possible.</span></span> <span data-ttu-id="05abd-272">사용자 Id를 사용 하는 일반적으로 범위가 지정 된 toohello 응용 프로그램 등록 되므로 새 등록 소개 사용자 tootheir 데이터 일치 하는 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-272">User IDs are typically scoped toohello application registration that was used, so introducing a new registration could create problems with matching users tootheir data.</span></span>

### <a name="custom-authentication"></a><span data-ttu-id="05abd-273">사용자 지정 인증</span><span class="sxs-lookup"><span data-stu-id="05abd-273">Custom authentication</span></span>
<span data-ttu-id="05abd-274">앱 사용자 지정 인증 솔루션을 사용 하는 경우 해당 hello 업그레이드 된 사이트에 액세스 toohello 시스템 있는지 toomake 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-274">If your app is using a custom authentication solution, you will want toomake sure that hello upgraded site has access toohello system.</span></span> <span data-ttu-id="05abd-275">Hello hello에 대 한 사용자 지정 인증에 대 한 새 지침에 따라 [.NET 서버 SDK 개요] toointegrate 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-275">Follow hello new instructions for custom authentication in hello [.NET server SDK overview] toointegrate your solution.</span></span> <span data-ttu-id="05abd-276">미리 보기에서 여전히 hello 사용자 지정 인증 구성 요소가 인지 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="05abd-276">Please note that hello custom authentication components are still in preview.</span></span>

## <span data-ttu-id="05abd-277"><a name="updating-clients"></a>클라이언트 업데이트</span><span class="sxs-lookup"><span data-stu-id="05abd-277"><a name="updating-clients"></a>Updating clients</span></span>
<span data-ttu-id="05abd-278">작동하는 모바일 앱 백 엔드가 있으면 그것을 사용하는 클라이언트 응용 프로그램의 새 버전에서 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-278">Once you have an operational Mobile App backend, you can work on a new version of your client application which consumes it.</span></span> <span data-ttu-id="05abd-279">모바일 앱도 hello 클라이언트 Sdk의 새 버전을 포함 하며, 유사한 toohello 서버 업그레이드 위의 tooremove 하기 전에 toohello 모바일 서비스 Sdk를 참조 하는 모든가 필요 hello 모바일 앱 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-279">Mobile Apps also includes a new version of hello client SDKs, and similar toohello server upgrade above, you will need tooremove all references toohello Mobile Services SDKs before installing hello Mobile Apps versions.</span></span>

<span data-ttu-id="05abd-280">Hello 버전 간의 주요 변경 내용은 hello 중 하나는 hello 생성자에 더 이상 응용 프로그램 키 필요입니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-280">One of hello main changes between hello versions is that hello constructors no longer require an application key.</span></span> <span data-ttu-id="05abd-281">이제 단순히 전달 모바일 앱의 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-281">You now simply pass in hello URL of your Mobile App.</span></span> <span data-ttu-id="05abd-282">예를 들어 hello.NET 클라이언트를 hello `MobileServiceClient` 생성자는 이제:</span><span class="sxs-lookup"><span data-stu-id="05abd-282">For example, on hello .NET clients, hello `MobileServiceClient` constructor is now:</span></span>

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net", // URL of hello Mobile App
        );

<span data-ttu-id="05abd-283">설치에 대 한 읽을 수 새 Sdk hello 및 hello 아래 hello 링크를 통해 새 구조를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="05abd-283">You can read about installing hello new SDKs and using hello new structure via hello links below:</span></span>

* [<span data-ttu-id="05abd-284">iOS 버전 3.0.0 이상</span><span class="sxs-lookup"><span data-stu-id="05abd-284">iOS version 3.0.0 or later</span></span>](app-service-mobile-ios-how-to-use-client-library.md)
* [<span data-ttu-id="05abd-285">.NET(Windows/Xamarin) 버전 2.0.0 이상</span><span class="sxs-lookup"><span data-stu-id="05abd-285">.NET (Windows/Xamarin) version 2.0.0 or later</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<span data-ttu-id="05abd-286">응용 프로그램이 경우 개의 푸시 알림을 사용 하 여, hello 각 플랫폼에 대 한 특정 등록 지침을 기록해 대로 몇 가지 변경 사항이 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-286">If your application makes use of push notifications, make note of hello specific registration instructions for each platform, as there have been some changes there as well.</span></span>

<span data-ttu-id="05abd-287">Hello 새 클라이언트 버전 준비을 사용 하는 경우 사용해 업그레이드 된 서버 프로젝트에 대해 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-287">When you have hello new client version ready, try it out against your upgraded server project.</span></span> <span data-ttu-id="05abd-288">확인 한 후 작동 하는지, 새 버전의 응용 프로그램 toocustomers 놓을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-288">After validating that it works, you can release a new version of your application toocustomers.</span></span> <span data-ttu-id="05abd-289">결국 고객이 있는 반면 기회 tooreceive 이러한 업데이트를 일단 응용 프로그램의 hello 모바일 서비스 버전을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-289">Eventually, once your customers have had a chance tooreceive these updates, you can delete hello Mobile Services version of your app.</span></span> <span data-ttu-id="05abd-290">앱 서비스 모바일 앱 tooan 완전히 업그레이드이 시점에서 hello 최신 모바일 앱 서버 SDK를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05abd-290">At this point, you have completely upgraded tooan App Service Mobile App using hello latest Mobile Apps server SDK.</span></span>

<!-- URLs. -->

[Azure 포털]: https://portal.azure.com/
[Azure 클래식 포털]: https://manage.windowsazure.com/
[모바일 앱 이란?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[모바일 앱 서버 SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure 스케줄러]: /en-us/documentation/services/scheduler/
[웹 작업]: ../app-service-web/websites-webjobs-resources.md
[어떻게 toouse hello.NET 서버 SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[앱 서비스 가격 책정]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET 서버 SDK 개요]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
