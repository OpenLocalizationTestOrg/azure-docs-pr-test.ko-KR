---
title: "모바일 서비스에서 Azure 앱 서비스로 업그레이드"
description: "모바일 서비스 응용 프로그램을 앱 서비스 모바일 앱으로 쉽게 업그레이드하는 방법을 알아봅니다."
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
ms.openlocfilehash: 81173b34d0d3b07c5c49d867b1dc5060c7311f12
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="upgrade-your-existing-net-azure-mobile-service-to-app-service"></a><span data-ttu-id="2a3fb-103">기존 .NET Azure 모바일 서비스를 앱 서비스로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="2a3fb-103">Upgrade your existing .NET Azure Mobile Service to App Service</span></span>
<span data-ttu-id="2a3fb-104">앱 서비스 모바일은 Microsoft Azure를 사용하여 모바일 응용 프로그램을 빌드하는 새로운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-104">App Service Mobile is a new way to build mobile applications using Microsoft Azure.</span></span> <span data-ttu-id="2a3fb-105">자세한 내용은 [모바일 앱 정의]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-105">To learn more, see [What are Mobile Apps?].</span></span>

<span data-ttu-id="2a3fb-106">이 항목에서는 기존 .NET 백 엔드 응용 프로그램을 Azure 모바일 서비스에서 새로운 앱 서비스 모바일 앱으로 업그레이드하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-106">This topic describes how to upgrade an existing .NET backend application from Azure Mobile Services to a new App Service Mobile Apps.</span></span> <span data-ttu-id="2a3fb-107">이 업그레이드를 수행하는 동안 기존 모바일 서비스 응용 프로그램이 계속 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-107">While you perform this upgrade, your existing Mobile Services application can continue to operate.</span></span>   <span data-ttu-id="2a3fb-108">Node.js 백 엔드 응용 프로그램을 업그레이드해야 하는 경우 [Node.js 모바일 서비스 업그레이드](app-service-mobile-node-backend-upgrading-from-mobile-services.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-108">If you need to upgrade a Node.js backend application, refer to [Upgrading your Node.js Mobile Services](app-service-mobile-node-backend-upgrading-from-mobile-services.md).</span></span>

<span data-ttu-id="2a3fb-109">모바일 백 엔드가 Azure 앱 서비스로 업그레이드되면 모든 앱 서비스 기능에 액세스할 수 있고 모바일 서비스 가격 책정이 아닌 [앱 서비스 가격 책정]에 따라 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-109">When a mobile backend is upgraded to Azure App Service, it has access to all App Service features and are billed according to [App Service pricing], not Mobile Services pricing.</span></span>

## <a name="migrate-vs-upgrade"></a><span data-ttu-id="2a3fb-110">마이그레이션과 업그레이드 비교</span><span class="sxs-lookup"><span data-stu-id="2a3fb-110">Migrate vs. upgrade</span></span>
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> <span data-ttu-id="2a3fb-111">업그레이드를 진행하기 전에 [마이그레이션을 수행](app-service-mobile-migrating-from-mobile-services.md) 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-111">It is recommended that you [perform a migration](app-service-mobile-migrating-from-mobile-services.md) before going through an upgrade.</span></span> <span data-ttu-id="2a3fb-112">이러한 방식으로 동일한 앱 서비스 계획에 두 버전의 응용 프로그램을 모두 추가 비용 없이 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-112">This way, you can put both versions of your application on the same App Service Plan and incur no additional cost.</span></span>
>
>

### <a name="improvements-in-mobile-apps-net-server-sdk"></a><span data-ttu-id="2a3fb-113">모바일 앱 .NET 서버 SDK에서 향상된 기능</span><span class="sxs-lookup"><span data-stu-id="2a3fb-113">Improvements in Mobile Apps .NET server SDK</span></span>
<span data-ttu-id="2a3fb-114">새 [모바일 앱 SDK](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) 의 업그레이드는 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-114">Upgrading to the new [Mobile Apps SDK](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) provides the following benefits:</span></span>

* <span data-ttu-id="2a3fb-115">NuGet 종속성에서 유연성이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-115">More flexibility on NuGet dependencies.</span></span> <span data-ttu-id="2a3fb-116">호스팅 환경이 고유한 버전의 NuGet 패키지를 더 이상 제공하지 않으므로 호환되는 대체 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-116">The hosting environment no longer provides its own versions of NuGet packages, so you can use alternative compatible versions.</span></span> <span data-ttu-id="2a3fb-117">그러나 모바일 서버 SDK 또는 종속성에 대한 새 주요 오류수정 또는 보안 업데이트가 있는 경우 서비스를 수동으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-117">However, if there are new critical bugfixes or security updates to the Mobile Server SDK or dependencies, you must update your service manually.</span></span>
* <span data-ttu-id="2a3fb-118">모바일 SDK에서 유연성이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-118">More flexibility in the mobile SDK.</span></span> <span data-ttu-id="2a3fb-119">인증, 테이블 API 및 푸시 등록 끝점 등 어떤 기능 및 경로를 설정할 것인지 명시적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-119">You can explicitly control which features and routes are set up, such as authentication, table APIs, and the push registration endpoint.</span></span> <span data-ttu-id="2a3fb-120">자세한 내용은 [에 .NET 서버 SDK를 사용하는 방법](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-120">To learn more, see [How to use the .NET server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>
* <span data-ttu-id="2a3fb-121">다른 ASP.NET 프로젝트 형식 및 경로를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-121">Support for other ASP.NET project types and routes.</span></span> <span data-ttu-id="2a3fb-122">이제 모바일 백 엔드 프로젝트와 동일한 프로젝트에서 MVC 및 Web API 컨트롤러를 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-122">You can now host MVC and Web API controllers in the same project as your mobile backend project.</span></span>
* <span data-ttu-id="2a3fb-123">새로운 앱 서비스 인증 기능을 지원하며 이는 웹 및 모바일 앱에서 일반 인증 구성을 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-123">Support for new App Service authentication features, which allow you to use a common authentication configuration across your web and mobile apps.</span></span>

## <span data-ttu-id="2a3fb-124"><a name="overview"></a>기본 업그레이드 개요</span><span class="sxs-lookup"><span data-stu-id="2a3fb-124"><a name="overview"></a>Basic upgrade overview</span></span>
<span data-ttu-id="2a3fb-125">대부분의 경우 새 모바일 앱 서버 SDK로 전환한 다음 새 모바일 앱 인스턴스에 코드를 다시 게시하기만 하면 간단히 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-125">In many cases, upgrading will be as simple as switching to the new Mobile Apps server SDK and republishing your code onto a new Mobile App instance.</span></span> <span data-ttu-id="2a3fb-126">그러나 고급 인증 시나리오 및 예약된 작업 사용과 같이 추가 구성이 필요한 일부 시나리오도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-126">There are, however some scenarios which will require some additional configuration, such as advanced authentication scenarios and working with scheduled jobs.</span></span> <span data-ttu-id="2a3fb-127">각 시나리오는 이후 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-127">Each of these is covered in the later sections.</span></span>

> [!TIP]
> <span data-ttu-id="2a3fb-128">업그레이드를 시작하기 전에 이 항목의 나머지 부분을 읽고 완전히 이해하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-128">It is advised that you read and understand the rest of this topic completely before starting an upgrade.</span></span> <span data-ttu-id="2a3fb-129">아래 설명선에 표시된 사용하는 기능을 모두 기록해 두세요.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-129">Make note of any features you use which are called out below.</span></span>
>
>

<span data-ttu-id="2a3fb-130">모바일 서비스 클라이언트 SDK는 새 모바일 앱 서버 SDK와 호환할 수 **없습니다** .</span><span class="sxs-lookup"><span data-stu-id="2a3fb-130">The Mobile Services client SDKs are **not** compatible with the new Mobile Apps server SDK.</span></span> <span data-ttu-id="2a3fb-131">앱에 대한 서비스 연속성을 제공하기 위해 현재 게시된 클라이언트를 제공하는 사이트에 변경 내용을 게시하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-131">In order to provide continuity of service for your app, you should not publish changes to a site currently serving published clients.</span></span> <span data-ttu-id="2a3fb-132">대신 중복으로 제공한 새 모바일 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-132">Instead, you should create a new mobile app that serves as a duplicate.</span></span> <span data-ttu-id="2a3fb-133">이 응용 프로그램을 동일한 앱 서비스 계획에 두어 추가 비용이 발생하지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-133">You can put this application on the same App Service plan to avoid incurring additional financial cost.</span></span>

<span data-ttu-id="2a3fb-134">다음 두 가지 버전의 응용 프로그램이 있습니다. 하나는 동일하게 유지되고 야생에서 게시된 앱을 제공하며 다른 하나는 업그레이드하고 새 클라이언트 릴리스를 대상으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-134">You will then have two versions of the application: one which stays the same and serves published apps in the wild, and the other which you can then upgrade and target with a new client release.</span></span> <span data-ttu-id="2a3fb-135">진도에 맞게 코드를 이동하고 테스트할 수 있지만 수행한 버그 수정이 둘 모두에 적용되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-135">You can move and test your code at your pace, but you should make sure that any bug fixes you make get applied to both.</span></span> <span data-ttu-id="2a3fb-136">야생에서 원하는 수의 클라이언트 앱이 최신 버전으로 업데이트되면 원하는 경우 원래 마이그레이션된 앱을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-136">Once you feel that a desired number of client apps in the wild have updated to the latest version, you can delete the original migrated app if you desire.</span></span>

<span data-ttu-id="2a3fb-137">업그레이드 프로세스에 대한 전체 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-137">The full outline for the upgrade process is as follows:</span></span>

1. <span data-ttu-id="2a3fb-138">새 모바일 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="2a3fb-138">Create a new Mobile App</span></span>
2. <span data-ttu-id="2a3fb-139">프로젝트를 업데이트하여 새 서버 SDK 사용</span><span class="sxs-lookup"><span data-stu-id="2a3fb-139">Update the project to use the new Server SDKs</span></span>
3. <span data-ttu-id="2a3fb-140">새 버전의 클라이언트 응용 프로그램 릴리스</span><span class="sxs-lookup"><span data-stu-id="2a3fb-140">Release a new version of your client application</span></span>
4. <span data-ttu-id="2a3fb-141">(선택 사항) 원래 마이그레이션된 인스턴스 삭제</span><span class="sxs-lookup"><span data-stu-id="2a3fb-141">(Optional) Delete your original migrated instance</span></span>

## <span data-ttu-id="2a3fb-142"><a name="mobile-app-version"></a>두 번째 응용 프로그램 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="2a3fb-142"><a name="mobile-app-version"></a>Creating a second application instance</span></span>
<span data-ttu-id="2a3fb-143">업그레이드의 첫 번째 단계는 새 버전의 응용 프로그램을 호스트할 모바일 앱 리소스를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-143">The first step in upgrading is to create the Mobile App resource which will host the new version of your application.</span></span> <span data-ttu-id="2a3fb-144">기존 모바일 서비스를 이미 마이그레이션한 경우 동일한 호스팅 계획에 이 버전을 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-144">If you have already migrated an existing mobile service, you will want to create this version on the same hosting plan.</span></span> <span data-ttu-id="2a3fb-145">[Azure Portal] 을 열고 마이그레이션된 응용 프로그램으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-145">Open the [Azure portal] and navigate to your migrated application.</span></span> <span data-ttu-id="2a3fb-146">앱 서비스 계획에서 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-146">Make note of the App Service Plan it is running on.</span></span>

<span data-ttu-id="2a3fb-147">다음으로 [.NET 백 엔드 만들기 지침](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app)을 수행하여 두 번째 응용 프로그램 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-147">Next, create the second application instance by following the [.NET backend creation instructions](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app).</span></span> <span data-ttu-id="2a3fb-148">앱 서비스 계획 또는 "호스팅 계획"을 선택하라는 메시지가 나타나면 마이그레이션된 응용 프로그램의 계획을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-148">When prompted to select you App Service Plan or "hosting plan" choose the plan of your migrated application.</span></span>

<span data-ttu-id="2a3fb-149">모바일 서비스와 동일한 데이터베이스 및 알림 허브를 사용하려는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-149">You will likely want to use the same database and Notification Hub as you did in Mobile Services.</span></span> <span data-ttu-id="2a3fb-150">[Azure Portal]을 열고 원래 응용 프로그램 탐색하여 이러한 값을 복사한 다음 **설정** > **응용 프로그램 설정**을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-150">You can copy these values by opening [Azure portal] and navigating to the original application, then click **Settings** > **Application settings**.</span></span> <span data-ttu-id="2a3fb-151">**연결 문자열**에서 `MS_NotificationHubConnectionString` 및 `MS_TableConnectionString`을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-151">Under **Connection Strings**, copy `MS_NotificationHubConnectionString` and `MS_TableConnectionString`.</span></span> <span data-ttu-id="2a3fb-152">새 업그레이드 사이트로 이동하고 붙여 넣어 기존 값을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-152">Navigate to your new upgrade site and paste them in, overwriting any existing values.</span></span> <span data-ttu-id="2a3fb-153">앱에 필요한 다른 응용 프로그램 설정에 이 프로세스를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-153">Repeat this process for any other application settings your app needs.</span></span> <span data-ttu-id="2a3fb-154">마이그레이션된 서비스를 사용하지 않는 경우 **Azure 클래식 포털** 에 있는 모바일 서비스 섹션의 [구성]탭에서 연결 문자열 및 앱 설정을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-154">If not using a migrated service, you can read connection strings and app settings from the **Configure** tab of the Mobile Services section of the [Azure classic portal].</span></span>

<span data-ttu-id="2a3fb-155">응용 프로그램에 대한 ASP.NET 프로젝트의 복사본을 만들고 새 사이트에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-155">Make a copy of the ASP.NET project for your application and publish it to your new site.</span></span> <span data-ttu-id="2a3fb-156">새 URL를 통해 업데이트된 클라이언트 응용 프로그램의 복사본을 사용하여 모든 작업이 예상 대로 작동하는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-156">Using a copy of your client application updated with the new URL, validate that everything works as expected.</span></span>

## <a name="updating-the-server-project"></a><span data-ttu-id="2a3fb-157">서버 프로젝트 업데이트</span><span class="sxs-lookup"><span data-stu-id="2a3fb-157">Updating the server project</span></span>
<span data-ttu-id="2a3fb-158">모바일 앱은 모바일 서비스 런타임과 동일한 기능을 대부분 제공하는 새로운 [모바일 앱 서버 SDK] 를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-158">Mobile Apps provides a new [Mobile App Server SDK] which provides much of the same functionality as the Mobile Services runtime.</span></span> <span data-ttu-id="2a3fb-159">먼저 모바일 서비스 패키지에 대한 모든 참조를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-159">First, you should remove all references to the Mobile Services packages.</span></span> <span data-ttu-id="2a3fb-160">NuGet 패키지 관리자에서 `WindowsAzure.MobileServices.Backend`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-160">In the NuGet package manager, search for `WindowsAzure.MobileServices.Backend`.</span></span> <span data-ttu-id="2a3fb-161">대부분의 앱에서 `WindowsAzure.MobileServices.Backend.Tables` 및 `WindowsAzure.MobileServices.Backend.Entity`를 포함하여 여러 패키지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-161">Most apps will see several packages here, including `WindowsAzure.MobileServices.Backend.Tables` and `WindowsAzure.MobileServices.Backend.Entity`.</span></span> <span data-ttu-id="2a3fb-162">이 경우 `Entity`와 같은 종속성 트리에서 가장 낮은 패키지를 시작하고 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-162">In such a case, start with the lowest package in the dependency tree, such as `Entity`, and remove it.</span></span> <span data-ttu-id="2a3fb-163">메시지가 표시되면 모든 종속 패키지를 제거하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-163">When prompted, do not remove all dependant packages.</span></span> <span data-ttu-id="2a3fb-164">`WindowsAzure.MobileServices.Backend` 자체를 제거할 때까지 이 프로세스를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-164">Repeat this process until you have removed `WindowsAzure.MobileServices.Backend` itself.</span></span>

<span data-ttu-id="2a3fb-165">이 시점에서 더 이상 모바일 서비스 SDK를 참조하지 않는 프로젝트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-165">At this point you will have a project that no longer references Mobile Services SDKs.</span></span>

<span data-ttu-id="2a3fb-166">다음으로 모바일 앱 SDK 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-166">Next you will add references the Mobile Apps SDK.</span></span> <span data-ttu-id="2a3fb-167">이 업그레이드를 위해 대부분의 개발자는 `Microsoft.Azure.Mobile.Server.Quickstart` 패키지를 다운로드하고 설치할 수 있으며, 전체 필수 집합으로 가져오게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-167">For this upgrade, most developers will want to download and install the `Microsoft.Azure.Mobile.Server.Quickstart` package, as this will pull in the entire required set.</span></span>

<span data-ttu-id="2a3fb-168">SDK 간의 차이로 인해 발생하는 몇 가지 컴파일러 오류가 있지만 쉽게 해결할 수 있으며 이 섹션의 나머지 부분에서 다루게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-168">There will be quite a few compiler errors resulting from differences between the SDKs, but these are easy to address and are covered in the rest of this section.</span></span>

### <a name="base-configuration"></a><span data-ttu-id="2a3fb-169">기본 구성</span><span class="sxs-lookup"><span data-stu-id="2a3fb-169">Base configuration</span></span>
<span data-ttu-id="2a3fb-170">그런 다음 WebApiConfig.cs에서</span><span class="sxs-lookup"><span data-stu-id="2a3fb-170">Then, in WebApiConfig.cs, you can replace:</span></span>

        // Use this class to set configuration options for your mobile service
        ConfigOptions options = new ConfigOptions();

        // Use this class to set WebAPI configuration options
        HttpConfiguration config = ServiceConfig.Initialize(new ConfigBuilder(options));

<span data-ttu-id="2a3fb-171">다음으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-171">with</span></span>

        HttpConfiguration config = new HttpConfiguration();
        new MobileAppConfiguration()
            .UseDefaultConfiguration()
        .ApplyTo(config);

> [!NOTE]
> <span data-ttu-id="2a3fb-172">앱에서 기능을 추가/제거하는 방법 및 새 .NET 서버 SDK에 대한 자세한 내용을 보려면, [.NET 서버 SDK를 사용하는 방법] 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-172">If you wish to learn more about the new .NET server SDK and how to add/remove features from your app, please see the [How to use the .NET server SDK] topic.</span></span>
>
>

<span data-ttu-id="2a3fb-173">또한 앱이 인증 기능을 사용하는 경우 OWIN 미들웨어를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-173">If your app makes use of the authentication features, you will also need to register an OWIN middleware.</span></span> <span data-ttu-id="2a3fb-174">이 경우 새 OWIN 시작 클래스에 위의 구성 코드를 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-174">In this case, you should move the above configuration code into a new OWIN Startup class.</span></span>

1. <span data-ttu-id="2a3fb-175">프로젝트에 아직 포함되지 않은 경우 NuGet 패키지 `Microsoft.Owin.Host.SystemWeb` 를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-175">Add the NuGet package `Microsoft.Owin.Host.SystemWeb` if it is not already included in your project.</span></span>
2. <span data-ttu-id="2a3fb-176">Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** -> **새 항목**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-176">In Visual Studio, right click on your project and select **Add** -> **New Item**.</span></span> <span data-ttu-id="2a3fb-177">**웹** -> **일반** -> **OWIN 시작 클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-177">Select **Web** -> **General** -> **OWIN Startup class**.</span></span>
3. <span data-ttu-id="2a3fb-178">MobileAppConfiguration에 대한 위의 코드를 `WebApiConfig.Register()`에서 새 시작 클래스의 `Configuration()` 메서드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-178">Move the above code for MobileAppConfiguration from `WebApiConfig.Register()` to the `Configuration()` method of your new startup class.</span></span>

<span data-ttu-id="2a3fb-179">`Configuration()` 메서드가 다음으로 끝나도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-179">Make sure the `Configuration()` method ends with:</span></span>

        app.UseWebApi(config)
        app.UseAppServiceAuthentication(config);

<span data-ttu-id="2a3fb-180">아래 전체 인증 섹션에서 다루는 인증에 관련된 추가 변경 내용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-180">There are additional changes related to authentication which are covered in the full authentication section below.</span></span>

### <a name="working-with-data"></a><span data-ttu-id="2a3fb-181">데이터 작업</span><span class="sxs-lookup"><span data-stu-id="2a3fb-181">Working with Data</span></span>
<span data-ttu-id="2a3fb-182">모바일 서비스에서 모바일 앱 이름은 Entity Framework 설치 프로그램의 기본 스키마 이름으로 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-182">In Mobile Services, the mobile app name served as the default schema name in the Entity Framework setup.</span></span>

<span data-ttu-id="2a3fb-183">이전에 참조된 동일한 스키마가 있는지 확인하려면 다음을 사용하여 응용 프로그램에 DbContext의 스키마를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-183">To ensure that you have the same schema being referenced as before, use the following to set the schema in the DbContext for your application:</span></span>

        string schema = System.Configuration.ConfigurationManager.AppSettings.Get("MS_MobileServiceName");

<span data-ttu-id="2a3fb-184">위의 작업을 수행하는 경우 MS_MobileServiceName을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-184">Please make sure you have MS_MobileServiceName set if you do the above.</span></span> <span data-ttu-id="2a3fb-185">또한 응용 프로그램이 이전에 사용자 지정한 경우 다른 스키마 이름을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-185">You can also provide another schema name if your application customized this previously.</span></span>

### <a name="system-properties"></a><span data-ttu-id="2a3fb-186">시스템 속성</span><span class="sxs-lookup"><span data-stu-id="2a3fb-186">System Properties</span></span>
#### <a name="naming"></a><span data-ttu-id="2a3fb-187">이름 지정</span><span class="sxs-lookup"><span data-stu-id="2a3fb-187">Naming</span></span>
<span data-ttu-id="2a3fb-188">Azure 모바일 서비스 서버 SDK에서 시스템 속성은 항상 속성에 대해 두 개의 밑줄(`__`) 접두사를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-188">In the Azure Mobile Services server SDK, system properties always contain a double underscore (`__`) prefix for the properties:</span></span>

* <span data-ttu-id="2a3fb-189">__createdAt</span><span class="sxs-lookup"><span data-stu-id="2a3fb-189">__createdAt</span></span>
* <span data-ttu-id="2a3fb-190">__updatedAt</span><span class="sxs-lookup"><span data-stu-id="2a3fb-190">__updatedAt</span></span>
* <span data-ttu-id="2a3fb-191">__deleted</span><span class="sxs-lookup"><span data-stu-id="2a3fb-191">__deleted</span></span>
* <span data-ttu-id="2a3fb-192">__version</span><span class="sxs-lookup"><span data-stu-id="2a3fb-192">__version</span></span>

<span data-ttu-id="2a3fb-193">모바일 서비스 클라이언트 SDK는 이 형식에서 시스템 속성을 구문 분석하기 위한 특수한 논리입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-193">The Mobile Services client SDKs have special logic for parsing system properties in this format.</span></span>

<span data-ttu-id="2a3fb-194">Azure 모바일 앱에서 시스템 속성에는 더 이상 특별 한 형식 및 다음과 같은 이름이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-194">In Azure Mobile Apps, system properties no longer have a special format and have the following names:</span></span>

* <span data-ttu-id="2a3fb-195">createdAt</span><span class="sxs-lookup"><span data-stu-id="2a3fb-195">createdAt</span></span>
* <span data-ttu-id="2a3fb-196">updatedAt</span><span class="sxs-lookup"><span data-stu-id="2a3fb-196">updatedAt</span></span>
* <span data-ttu-id="2a3fb-197">deleted</span><span class="sxs-lookup"><span data-stu-id="2a3fb-197">deleted</span></span>
* <span data-ttu-id="2a3fb-198">버전</span><span class="sxs-lookup"><span data-stu-id="2a3fb-198">version</span></span>

<span data-ttu-id="2a3fb-199">모바일 앱 클라이언트 SDK는 새 시스템 속성 이름을 사용하므로 클라이언트 코드에는 변경이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-199">The Mobile Apps client SDKs use the new system properties names, so no changes are required to client code.</span></span> <span data-ttu-id="2a3fb-200">그러나 서비스에 직접 REST 호출을 하는 경우 쿼리를 적절하게 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-200">However, if you are directly making REST calls to your service then you should change your queries accordingly.</span></span>

#### <a name="local-store"></a><span data-ttu-id="2a3fb-201">로컬 저장소</span><span class="sxs-lookup"><span data-stu-id="2a3fb-201">Local store</span></span>
<span data-ttu-id="2a3fb-202">시스템 속성의 이름에 변경 사항이 있으면 모바일 서비스에 대한 오프라인 동기화 로컬 데이터베이스가 모바일 앱과 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-202">The changes to the names of system properties mean that an offline sync local database for Mobile Services is not compatible with Mobile Apps.</span></span> <span data-ttu-id="2a3fb-203">가능한 경우 보류 중인 변경 내용이 서버에 보내진 이후까지 모바일 서비스에서 모바일 앱에 클라이언트 앱 업그레이드하지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-203">If possible, you should avoid upgrading client apps from Mobile Services to Mobile Apps until after pending changes have been sent to the server.</span></span> <span data-ttu-id="2a3fb-204">그런 다음 업그레이드된 앱은 새 데이터베이스 파일 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-204">Then, the upgraded app should use a new database filename.</span></span>

<span data-ttu-id="2a3fb-205">작업 큐에 오프라인 변경 내용을 보류 중인 동안 클라이언트 앱이 모바일 서비스에서 모바일 앱으로 업그레이드되면 시스템 데이터베이스는 새 열 이름을 사용하도록 업데이트되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-205">If a client app is upgraded from Mobile Services to Mobile Apps while there are pending offline changes in the operation queue, then the system database must be updated to use the new column names.</span></span> <span data-ttu-id="2a3fb-206">iOS에서 열 이름을 변경하는 간단한 마이그레이션을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-206">On iOS, this can be achieved using lightweight migrations to change the column names.</span></span> <span data-ttu-id="2a3fb-207">Android 및 .NET 관리된 클라이언트에서 사용자 지정 SQL을 작성하여 데이터 개체 테이블에 대한 열 이름을 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-207">On Android and the .NET managed client, you should write custom SQL to rename the columns for your data object tables.</span></span>

<span data-ttu-id="2a3fb-208">iOS에서 다음과 일치하도록 데이터 엔터티에 대한 핵심 데이터 스키마를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-208">On iOS, you should change your Core Data schema for your data entities to match the following.</span></span> <span data-ttu-id="2a3fb-209">속성 `createdAt`, `updatedAt` 및 `version`에는 더 이상 `ms_` 접두사가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-209">Note that the properties `createdAt`, `updatedAt` and `version` no longer have an `ms_` prefix:</span></span>

| <span data-ttu-id="2a3fb-210">특성</span><span class="sxs-lookup"><span data-stu-id="2a3fb-210">Attribute</span></span> | <span data-ttu-id="2a3fb-211">유형</span><span class="sxs-lookup"><span data-stu-id="2a3fb-211">Type</span></span> | <span data-ttu-id="2a3fb-212">참고</span><span class="sxs-lookup"><span data-stu-id="2a3fb-212">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a3fb-213">id</span><span class="sxs-lookup"><span data-stu-id="2a3fb-213">id</span></span> |<span data-ttu-id="2a3fb-214">문자열, 필수로 표시</span><span class="sxs-lookup"><span data-stu-id="2a3fb-214">String, marked required</span></span> |<span data-ttu-id="2a3fb-215">원격 저장소의 기본 키</span><span class="sxs-lookup"><span data-stu-id="2a3fb-215">primary key in remote store</span></span> |
| <span data-ttu-id="2a3fb-216">createdAt</span><span class="sxs-lookup"><span data-stu-id="2a3fb-216">createdAt</span></span> |<span data-ttu-id="2a3fb-217">Date</span><span class="sxs-lookup"><span data-stu-id="2a3fb-217">Date</span></span> |<span data-ttu-id="2a3fb-218">(옵션) createdAt 시스템 속성에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-218">(optional) maps to createdAt system property</span></span> |
| <span data-ttu-id="2a3fb-219">updatedAt</span><span class="sxs-lookup"><span data-stu-id="2a3fb-219">updatedAt</span></span> |<span data-ttu-id="2a3fb-220">Date</span><span class="sxs-lookup"><span data-stu-id="2a3fb-220">Date</span></span> |<span data-ttu-id="2a3fb-221">(옵션) updatedAt 시스템 속성에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-221">(optional) maps to updatedAt system property</span></span> |
| <span data-ttu-id="2a3fb-222">버전</span><span class="sxs-lookup"><span data-stu-id="2a3fb-222">version</span></span> |<span data-ttu-id="2a3fb-223">String</span><span class="sxs-lookup"><span data-stu-id="2a3fb-223">String</span></span> |<span data-ttu-id="2a3fb-224">(옵션) 충돌을 검색하는 데 사용되며 version에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-224">(optional) used to detect conflicts, maps to version</span></span> |

#### <a name="querying-system-properties"></a><span data-ttu-id="2a3fb-225">시스템 속성 쿼리</span><span class="sxs-lookup"><span data-stu-id="2a3fb-225">Querying system properties</span></span>
<span data-ttu-id="2a3fb-226">Azure 모바일 서비스에서 시스템 속성은 기본적으로 전송되지 않지만 쿼리 문자열 `__systemProperties`을 사용하여 요청된 경우에만 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-226">In Azure Mobile Services, system properties are not sent by default, but only when they are requested using the query string `__systemProperties`.</span></span> <span data-ttu-id="2a3fb-227">반면 Azure 모바일 앱 시스템에서 속성은 서버 SDK 개체 모델의 일부이기 때문에 **항상 선택** 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-227">In contrast, in Azure Mobile Apps system properties are **always selected** since they are part of the server SDK object model.</span></span>

<span data-ttu-id="2a3fb-228">이 변경 사항은 `MappedEntityDomainManager`의 확장과 같은 도메인 관리자의 사용자 지정 구현에 주로 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-228">This change mainly impacts custom implementations of domain managers, such as extensions of `MappedEntityDomainManager`.</span></span> <span data-ttu-id="2a3fb-229">모바일 서비스에서 클라이언트가 시스템 속성을 요구하지 않으면 모든 속성이 실제로 매핑되지 않는 `MappedEntityDomainManager` 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-229">In Mobile Services, if a client never requests any system properties, it is possible to use a `MappedEntityDomainManager` that does not actually map all properties.</span></span> <span data-ttu-id="2a3fb-230">그러나 Azure 모바일 앱에서 이러한 매핑되지 않은 속성은 가져오기 쿼리에서 오류를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-230">However, in Azure Mobile Apps, these unmapped properties will cause an error in GET queries.</span></span>

<span data-ttu-id="2a3fb-231">문제를 해결하는 가장 쉬운 방법은 DTO를 수정하여 `EntityData` 대신 `ITableData`을 상속하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-231">The easiest way to resolve the issue is to modify your DTOs so that they inherit from `ITableData` instead of `EntityData`.</span></span> <span data-ttu-id="2a3fb-232">그런 다음 `[NotMapped]` 특성을 생략해야 하는 필드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-232">Then, add the `[NotMapped]` attribute to the fields that should be omitted.</span></span>

<span data-ttu-id="2a3fb-233">예를 들어 다음은 시스템 속성이 없는 `TodoItem` 을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-233">For example, the following defines `TodoItem` with no system properties:</span></span>

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

<span data-ttu-id="2a3fb-234">참고: `NotMapped`에 오류가 발생하는 경우 어셈블리 `System.ComponentModel.DataAnnotations`에 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-234">Note: if you get errors on `NotMapped`, add a reference to the assembly `System.ComponentModel.DataAnnotations`.</span></span>

### <a name="cors"></a><span data-ttu-id="2a3fb-235">CORS</span><span class="sxs-lookup"><span data-stu-id="2a3fb-235">CORS</span></span>
<span data-ttu-id="2a3fb-236">모바일 서비스는 ASP.NET CORS 솔루션을 래핑하여 CORS에 대한 지원을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-236">Mobile Services included some support for CORS by wrapping the ASP.NET CORS solution.</span></span> <span data-ttu-id="2a3fb-237">래핑 계층이 개발자에게 더 많은 제어를 제공하도록 제거되었으므로 직접 [ASP.NET CORS 지원](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-237">This wrapping layer has been removed to give the developer more control, so you can directly leverage [ASP.NET CORS support](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

<span data-ttu-id="2a3fb-238">우려되는 부분은 CORS를 사용하는 경우 클라이언트 SDK가 제대로 작동하려면 `eTag` 및 `Location` 헤더를 허용해야 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-238">The main areas of concern if using CORS are that the `eTag` and `Location` headers must be allowed in order for the client SDKs to work properly.</span></span>

### <a name="push-notifications"></a><span data-ttu-id="2a3fb-239">푸시 알림</span><span class="sxs-lookup"><span data-stu-id="2a3fb-239">Push Notifications</span></span>
<span data-ttu-id="2a3fb-240">푸시를 위해 서버 SDK에서 누락된 주요 항목은 PushRegistrationHandler 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-240">For push, the main item that you may find missing from the Server SDK is the PushRegistrationHandler class.</span></span> <span data-ttu-id="2a3fb-241">모바일 앱에서는 등록이 약간 다르게 처리되며, 기본적으로 태그 없는 등록이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-241">Registrations are handled slightly differently in Mobile Apps, and tagless registrations are enabled by default.</span></span> <span data-ttu-id="2a3fb-242">사용자 지정 API를 통해 태그를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-242">Managing tags may be accomplished by using custom APIs.</span></span> <span data-ttu-id="2a3fb-243">자세한 정보는 [태그에 대한 등록](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags) 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-243">Please see the [registering for tags](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags) instructions for more information.</span></span>

### <a name="scheduled-jobs"></a><span data-ttu-id="2a3fb-244">예약된 작업</span><span class="sxs-lookup"><span data-stu-id="2a3fb-244">Scheduled Jobs</span></span>
<span data-ttu-id="2a3fb-245">예약된 작업은 모바일 앱에 빌드되지 않으므로 .NET 백 엔드에 있는 기존 작업을 모두 개별적으로 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-245">Scheduled jobs are not built into Mobile Apps, so any existing jobs that you have in your .NET backend will need to be upgraded individually.</span></span> <span data-ttu-id="2a3fb-246">한 가지 옵션은 모바일 앱 코드 사이트에 예약된 [웹 작업] 을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-246">One option is to create a scheduled [Web Job] on the Mobile App code site.</span></span> <span data-ttu-id="2a3fb-247">작업 코드를 포함하는 컨트롤러를 설정하고 예상 일정에 따라 해당 끝점에 도달하도록 [Azure 스케줄러] 를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-247">You could also set up a controller that holds your job code and configure the [Azure Scheduler] to hit that endpoint on the expected schedule.</span></span>

### <a name="miscellaneous-changes"></a><span data-ttu-id="2a3fb-248">기타 변경 내용</span><span class="sxs-lookup"><span data-stu-id="2a3fb-248">Miscellaneous changes</span></span>
<span data-ttu-id="2a3fb-249">모바일 클라이언트에서 사용될 수 있는 모든 ApiControllers에는 이제 `[MobileAppController]` 특성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-249">All ApiControllers which will be consumed by a mobile client must now have the `[MobileAppController]` attribute.</span></span> <span data-ttu-id="2a3fb-250">더 이상 기본적으로 포함되지 않으므로 다른 ApiControllers는 모바일 포맷터에 의해 영향을 받지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-250">This is no longer included by default so that other ApiControllers to go unaffected by the mobile formatters.</span></span>

<span data-ttu-id="2a3fb-251">`ApiServices` 개체는 더이상 SDK의 일부가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-251">The `ApiServices` object is no longer part of the SDK.</span></span> <span data-ttu-id="2a3fb-252">모바일 앱 설정에 액세스하려면 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-252">To access Mobile App settings, you can use the following:</span></span>

    MobileAppSettingsDictionary settings = this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

<span data-ttu-id="2a3fb-253">마찬가지로, 로깅은 이제 표준 ASP.NET 추적 쓰기를 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-253">Similarly, logging is now accomplished using the standard ASP.NET trace writing:</span></span>

    ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
    traceWriter.Info("Hello, World");  

## <span data-ttu-id="2a3fb-254"><a name="authentication"></a>인증 고려 사항</span><span class="sxs-lookup"><span data-stu-id="2a3fb-254"><a name="authentication"></a>Authentication considerations</span></span>
<span data-ttu-id="2a3fb-255">이제 모바일 서비스의 인증 구성 요소는 앱 서비스 인증/권한 부여 기능으로 옮겨졌습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-255">The authentication components of Mobile Services have now been moved into the App Service Authentication/Authorization feature.</span></span> <span data-ttu-id="2a3fb-256">[모바일 앱에 인증 추가](app-service-mobile-ios-get-started-users.md) 항목을 읽어서 사이트에 이 옵션을 사용하는 데 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-256">You can learn about enabling this for your site by reading the [Add authentication to your mobile app](app-service-mobile-ios-get-started-users.md) topic.</span></span>

<span data-ttu-id="2a3fb-257">AAD, Facebook, Google 등의 일부 공급자의 경우 복사 응용 프로그램에서 기존 등록을 활용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-257">For some providers, such as AAD, Facebook, and Google, you should be able to leverage the existing registration from your copy application.</span></span> <span data-ttu-id="2a3fb-258">단순히 ID 공급자의 포털로 이동하고 새 리디렉션 URL을 등록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-258">You simply need to navigate to the identity provider's portal and add a new redirect URL to the registration.</span></span> <span data-ttu-id="2a3fb-259">그런 다음 클라이언트 ID 및 암호를 통해 앱 서비스 인증/권한 부여를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-259">Then configure App Service Authentication/Authorization with the client ID and secret.</span></span>

### <a name="controller-action-authorization"></a><span data-ttu-id="2a3fb-260">컨트롤러 작업 권한 부여</span><span class="sxs-lookup"><span data-stu-id="2a3fb-260">Controller action authorization</span></span>
<span data-ttu-id="2a3fb-261">`[AuthorizeLevel(AuthorizationLevel.User)]` 특성의 인스턴스는 이제 표준 ASP.NET `[Authorize]` 특성을 사용하도록 변경되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-261">Any instances of the `[AuthorizeLevel(AuthorizationLevel.User)]` attribute must now be changed to use the standard ASP.NET `[Authorize]` attribute.</span></span> <span data-ttu-id="2a3fb-262">또한 컨트롤러는 다른 ASP.NET 응용 프로그램에서와 같이 이제 기본적으로 익명입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-262">Additionally, controllers are now Anonymous by default, as in other ASP.NET applications.</span></span>
<span data-ttu-id="2a3fb-263">관리자 또는 응용 프로그램을 같은 다른 AuthorizeLevel 옵션 중 하나를 사용하는 경우 이러한 내용이 사라지도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-263">If you were using one of the other AuthorizeLevel options, such as Admin or Application, please note that these are gone.</span></span> <span data-ttu-id="2a3fb-264">대신 공유 암호에 AuthorizationFilters를 설정하거나 AAD 서비스 주체를 구성하여 서비스 간 호출을 안전하게 사용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-264">You can instead set up AuthorizationFilters for shared secrets or configure an AAD Service Principal to enable service-to-service calls securely.</span></span>

### <a name="getting-additional-user-information"></a><span data-ttu-id="2a3fb-265">추가 사용자 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="2a3fb-265">Getting additional user information</span></span>
<span data-ttu-id="2a3fb-266">`GetAppServiceIdentityAsync()` 메서드를 통해 액세스 토큰을 포함하는 추가 사용자 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-266">You can get additional user information, including access tokens through the `GetAppServiceIdentityAsync()` method:</span></span>

        FacebookCredentials creds = await this.User.GetAppServiceIdentityAsync<FacebookCredentials>();

<span data-ttu-id="2a3fb-267">또한 데이터베이스에 사용자 ID를 저장하는 경우와 같이 응용 프로그램이 사용자 ID에 종속된 경우 모바일 서비스와 앱 서비스 모바일 앱 간에 사용자 ID가 서로 다르다는 것에 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-267">Additionally, if your application takes dependencies on user IDs, such as storing them in a database, it is important to note that the user IDs between Mobile Services and App Service Mobile Apps are different.</span></span> <span data-ttu-id="2a3fb-268">그러나 모바일 서비스 사용자 ID도 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-268">You can still get the Mobile Services User ID, though.</span></span> <span data-ttu-id="2a3fb-269">ProviderCredentials 하위 클래스는 모두 UserId 속성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-269">All of the ProviderCredentials subclasses have a UserId property.</span></span> <span data-ttu-id="2a3fb-270">따라서 앞의 예제부터 계속 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-270">So continuing from the example before:</span></span>

        string mobileServicesUserId = creds.Provider + ":" + creds.UserId;

<span data-ttu-id="2a3fb-271">앱이 사용자 ID에 종속된 경우 가능하면 ID 공급자와 함께 동일한 등록을 활용하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-271">If your app does take any dependencies on user IDs, it is important that you leverage the same registration with an identity provider if possible.</span></span> <span data-ttu-id="2a3fb-272">일반적으로 사용자 ID의 범위는 사용된 응용 프로그램 등록으로 지정되므로 새 등록을 도입하면 사용자를 해당 데이터에 일치시킬 때 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-272">User IDs are typically scoped to the application registration that was used, so introducing a new registration could create problems with matching users to their data.</span></span>

### <a name="custom-authentication"></a><span data-ttu-id="2a3fb-273">사용자 지정 인증</span><span class="sxs-lookup"><span data-stu-id="2a3fb-273">Custom authentication</span></span>
<span data-ttu-id="2a3fb-274">앱이 사용자 지정 인증 솔루션을 사용하는 경우 업그레이드된 사이트가 시스템에 액세스하도록 하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-274">If your app is using a custom authentication solution, you will want to make sure that the upgraded site has access to the system.</span></span> <span data-ttu-id="2a3fb-275">[.NET 서버 SDK 개요] 에서 사용자 지정 인증에 대한 새 지침을 수행하여 솔루션을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-275">Follow the new instructions for custom authentication in the [.NET server SDK overview] to integrate your solution.</span></span> <span data-ttu-id="2a3fb-276">사용자 지정 인증 구성 요소가 여전히 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-276">Please note that the custom authentication components are still in preview.</span></span>

## <span data-ttu-id="2a3fb-277"><a name="updating-clients"></a>클라이언트 업데이트</span><span class="sxs-lookup"><span data-stu-id="2a3fb-277"><a name="updating-clients"></a>Updating clients</span></span>
<span data-ttu-id="2a3fb-278">작동하는 모바일 앱 백 엔드가 있으면 그것을 사용하는 클라이언트 응용 프로그램의 새 버전에서 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-278">Once you have an operational Mobile App backend, you can work on a new version of your client application which consumes it.</span></span> <span data-ttu-id="2a3fb-279">또한 모바일 앱은 클라이언트 SDK의 새 버전을 포함하고 위의 서버 업그레이드와 유사합니다. 따라서 모바일 앱 버전을 설치하기 전에 모바일 서비스 SDK에 대한 모든 참조를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-279">Mobile Apps also includes a new version of the client SDKs, and similar to the server upgrade above, you will need to remove all references to the Mobile Services SDKs before installing the Mobile Apps versions.</span></span>

<span data-ttu-id="2a3fb-280">버전 간의 주요 변경 사항 중 하나는 생성자가 응용 프로그램 키를 더 이상 필요로 하지 않는다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-280">One of the main changes between the versions is that the constructors no longer require an application key.</span></span> <span data-ttu-id="2a3fb-281">이제 모바일 앱의 URL에 간단히 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-281">You now simply pass in the URL of your Mobile App.</span></span> <span data-ttu-id="2a3fb-282">예를 들어 .NET 클라이언트에서 `MobileServiceClient` 생성자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-282">For example, on the .NET clients, the `MobileServiceClient` constructor is now:</span></span>

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net", // URL of the Mobile App
        );

<span data-ttu-id="2a3fb-283">아래 링크를 통해 새 SDK를 설치하고 새 구조를 사용하는 데 대한 내용을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-283">You can read about installing the new SDKs and using the new structure via the links below:</span></span>

* [<span data-ttu-id="2a3fb-284">iOS 버전 3.0.0 이상</span><span class="sxs-lookup"><span data-stu-id="2a3fb-284">iOS version 3.0.0 or later</span></span>](app-service-mobile-ios-how-to-use-client-library.md)
* [<span data-ttu-id="2a3fb-285">.NET(Windows/Xamarin) 버전 2.0.0 이상</span><span class="sxs-lookup"><span data-stu-id="2a3fb-285">.NET (Windows/Xamarin) version 2.0.0 or later</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<span data-ttu-id="2a3fb-286">응용 프로그램이 푸시 알림을 사용하면 일부 변경 사항이 있는 경우와 같이 각 플랫폼에 대한 특정 등록 지침을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-286">If your application makes use of push notifications, make note of the specific registration instructions for each platform, as there have been some changes there as well.</span></span>

<span data-ttu-id="2a3fb-287">새 클라이언트 버전을 준비할 때 업그레이드된 서버 프로젝트에 사용해보세요.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-287">When you have the new client version ready, try it out against your upgraded server project.</span></span> <span data-ttu-id="2a3fb-288">작동하는지 유효성을 검사한 후에 고객에게 응용 프로그램의 새 버전을 릴리스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-288">After validating that it works, you can release a new version of your application to customers.</span></span> <span data-ttu-id="2a3fb-289">결국 고객이 이러한 업데이트를 받고 나면 모바일 서비스 버전의 앱을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-289">Eventually, once your customers have had a chance to receive these updates, you can delete the Mobile Services version of your app.</span></span> <span data-ttu-id="2a3fb-290">이 시점에서 최신 모바일 앱 서버 SDK를 사용하여 앱 서비스 모바일 앱의 업그레이드를 완전히 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="2a3fb-290">At this point, you have completely upgraded to an App Service Mobile App using the latest Mobile Apps server SDK.</span></span>

<!-- URLs. -->

<span data-ttu-id="2a3fb-291">[Azure Portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="2a3fb-291">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="2a3fb-292">[구성]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="2a3fb-292">[Azure classic portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="2a3fb-293">[모바일 앱 정의]: app-service-mobile-value-prop.md</span><span class="sxs-lookup"><span data-stu-id="2a3fb-293">[What are Mobile Apps?]: app-service-mobile-value-prop.md</span></span>
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
<span data-ttu-id="2a3fb-294">[모바일 앱 서버 SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server</span><span class="sxs-lookup"><span data-stu-id="2a3fb-294">[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server</span></span>
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications to your mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication to your mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
<span data-ttu-id="2a3fb-295">[Azure 스케줄러]: /en-us/documentation/services/scheduler/</span><span class="sxs-lookup"><span data-stu-id="2a3fb-295">[Azure Scheduler]: /en-us/documentation/services/scheduler/</span></span>
<span data-ttu-id="2a3fb-296">[웹 작업]: ../app-service-web/websites-webjobs-resources.md</span><span class="sxs-lookup"><span data-stu-id="2a3fb-296">[Web Job]: ../app-service-web/websites-webjobs-resources.md</span></span>
<span data-ttu-id="2a3fb-297">[.NET 서버 SDK를 사용하는 방법]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="2a3fb-297">[How to use the .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span></span>
[Migrate from Mobile Services to an App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service to App Service]: app-service-mobile-migrating-from-mobile-services.md
<span data-ttu-id="2a3fb-298">[앱 서비스 가격 책정]: https://azure.microsoft.com/en-us/pricing/details/app-service/</span><span class="sxs-lookup"><span data-stu-id="2a3fb-298">[App Service pricing]: https://azure.microsoft.com/en-us/pricing/details/app-service/</span></span>
<span data-ttu-id="2a3fb-299">[.NET 서버 SDK 개요]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="2a3fb-299">[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span></span>
