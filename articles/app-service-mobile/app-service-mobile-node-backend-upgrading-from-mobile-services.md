---
title: "모바일 서비스에서 Azure 앱 서비스로 업그레이드 - Node.js"
description: "모바일 서비스 응용 프로그램을 앱 서비스 모바일 앱으로 쉽게 업그레이드하는 방법을 알아봅니다."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: c58f6df0-5aad-40a3-bddc-319c378218e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: ce0572e85c258aa377c3eea7923d43a30c935bb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-to-app-service"></a><span data-ttu-id="285ec-103">기존 Node.js Azure 모바일 서비스를 앱 서비스로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="285ec-103">Upgrade your existing Node.js Azure Mobile Service to App Service</span></span>
<span data-ttu-id="285ec-104">앱 서비스 모바일은 Microsoft Azure를 사용하여 모바일 응용 프로그램을 빌드하는 새로운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-104">App Service Mobile is a new way to build mobile applications using Microsoft Azure.</span></span> <span data-ttu-id="285ec-105">자세한 내용은 [모바일 앱 정의]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="285ec-105">To learn more, see [What are Mobile Apps?].</span></span>

<span data-ttu-id="285ec-106">이 항목에서는 기존 Node.js 백 엔드 응용 프로그램을 Azure 모바일 서비스에서 새로운 앱 서비스 모바일 앱으로 업그레이드하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-106">This topic describes how to upgrade an existing Node.js backend application from Azure Mobile Services to a new App Service Mobile Apps.</span></span> <span data-ttu-id="285ec-107">이 업그레이드를 수행하는 동안 기존 모바일 서비스 응용 프로그램이 계속 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-107">While you perform this upgrade, your existing Mobile Services application can continue to operate.</span></span>  <span data-ttu-id="285ec-108">Node.js 백 엔드 응용 프로그램을 업그레이드해야 하는 경우 [.NET 모바일 서비스 업그레이드](app-service-mobile-net-upgrading-from-mobile-services.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="285ec-108">If you need to upgrade a Node.js backend application, refer to [Upgrading your .NET Mobile Services](app-service-mobile-net-upgrading-from-mobile-services.md).</span></span>

<span data-ttu-id="285ec-109">모바일 백 엔드가 Azure 앱 서비스로 업그레이드되면 모든 앱 서비스 기능에 액세스할 수 있고 모바일 서비스 가격 책정이 아닌 [앱 서비스 가격 책정]에 따라 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-109">When a mobile backend is upgraded to Azure App Service, it has access to all App Service features and are billed according to [App Service pricing], not Mobile Services pricing.</span></span>

## <a name="migrate-vs-upgrade"></a><span data-ttu-id="285ec-110">마이그레이션과 업그레이드 비교</span><span class="sxs-lookup"><span data-stu-id="285ec-110">Migrate vs. upgrade</span></span>
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> <span data-ttu-id="285ec-111">업그레이드를 진행하기 전에 [마이그레이션을 수행](app-service-mobile-migrating-from-mobile-services.md) 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-111">It is recommended that you [perform a migration](app-service-mobile-migrating-from-mobile-services.md) before going through an upgrade.</span></span> <span data-ttu-id="285ec-112">이러한 방식으로 동일한 앱 서비스 계획에 두 버전의 응용 프로그램을 모두 추가 비용 없이 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-112">This way, you can put both versions of your application on the same App Service Plan and incur no additional cost.</span></span>
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a><span data-ttu-id="285ec-113">모바일 앱 Node.js 서버 SDK에서 향상된 기능</span><span class="sxs-lookup"><span data-stu-id="285ec-113">Improvements in Mobile Apps Node.js server SDK</span></span>
<span data-ttu-id="285ec-114">새 [모바일 앱 SDK](https://www.npmjs.com/package/azure-mobile-apps) 업그레이드는 다음을 포함하여 다양한 향상된 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-114">Upgrading to the new [Mobile Apps SDK](https://www.npmjs.com/package/azure-mobile-apps) provides a lot of improvements, including:</span></span>

* <span data-ttu-id="285ec-115">[Express 프레임워크](http://expressjs.com/en/index.html)에 기반하여 새 노드 SDK는 간단하고 새 노드 버전을 유지할 수 있도록 설계됩니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-115">Based on the [Express framework](http://expressjs.com/en/index.html), the new Node SDK is light-weight and designed to keep up with new Node versions as they come out.</span></span> <span data-ttu-id="285ec-116">Express 미들웨어를 통해 응용 프로그램 동작을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-116">You can customize the application behavior with Express middleware.</span></span>
* <span data-ttu-id="285ec-117">모바일 서비스 SDK에 비해 성능이 크게 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-117">Significant performance improvements compared to the Mobile Services SDK.</span></span>
* <span data-ttu-id="285ec-118">모바일 백 엔드를 통해 웹 사이트를 호스팅할 수 있습니다. 마찬가지로 기존 v4 응용 프로그램에 Azure 모바일 SDK를 추가하기는 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-118">You can now host a website together with your mobile backend; similarly, it's easy to add the Azure Mobile SDK to any existing express.v4 application.</span></span>
* <span data-ttu-id="285ec-119">플랫폼 간 및 로컬 개발을 위해 작성된 모바일 앱 SDK는 Windows, Linux 및 OSX 플랫폼에서 개발되고 로컬로 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-119">Built for cross-platform and local development, the Mobile Apps SDK can be developed and run locally on Windows, Linux, and OSX platforms.</span></span> <span data-ttu-id="285ec-120">배포하기 전에 [Mocha](https://mochajs.org/) 테스트를 실행하는 것 같은 일반적인 노드 개발 기술을 사용하는 것은 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-120">It's now easy to use common Node development techniques like running [Mocha](https://mochajs.org/) tests prior to deployment.</span></span>

## <span data-ttu-id="285ec-121"><a name="overview"></a>기본 업그레이드 개요</span><span class="sxs-lookup"><span data-stu-id="285ec-121"><a name="overview"></a>Basic upgrade overview</span></span>
<span data-ttu-id="285ec-122">Node.js 백 엔드 업그레이드를 지원하기 위해 Azure 앱 서비스는 호환성 패키지를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-122">To aid in upgrading a Node.js backend, Azure App Service has provided a compatibility package.</span></span>  <span data-ttu-id="285ec-123">업그레이드 후 새 앱 서비스 사이트에 배포할 수 있는 새 사이트를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-123">After upgrade, you will have a niew site that can be deployed to a new App Service site.</span></span>

<span data-ttu-id="285ec-124">모바일 서비스 클라이언트 SDK는 새 모바일 앱 서버 SDK와 호환할 수 **없습니다** .</span><span class="sxs-lookup"><span data-stu-id="285ec-124">The Mobile Services client SDKs are **not** compatible with the new Mobile Apps server SDK.</span></span> <span data-ttu-id="285ec-125">앱에 대한 서비스 연속성을 제공하기 위해 현재 게시된 클라이언트를 제공하는 사이트에 변경 내용을 게시하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-125">In order to provide continuity of service for your app, you should not publish changes to a site currently serving published clients.</span></span> <span data-ttu-id="285ec-126">대신 중복으로 제공한 새 모바일 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-126">Instead, you should create a new mobile app that serves as a duplicate.</span></span> <span data-ttu-id="285ec-127">이 응용 프로그램을 동일한 앱 서비스 계획에 두어 추가 비용이 발생하지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-127">You can put this application on the same App Service plan to avoid incurring additional financial cost.</span></span>

<span data-ttu-id="285ec-128">다음 두 가지 버전의 응용 프로그램이 있습니다. 하나는 동일하게 유지되고 야생에서 게시된 앱을 제공하며 다른 하나는 업그레이드하고 새 클라이언트 릴리스를 대상으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-128">You will then have two versions of the application: one that stays the same and serves published apps in the wild, and the other which you can then upgrade and target with a new client release.</span></span> <span data-ttu-id="285ec-129">진도에 맞게 코드를 이동하고 테스트할 수 있지만 수행한 버그 수정이 둘 모두에 적용되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-129">You can move and test your code at your pace, but you should make sure that any bug fixes you make get applied to both.</span></span> <span data-ttu-id="285ec-130">야생에서 원하는 수의 클라이언트 앱이 최신 버전으로 업데이트되면 원하는 경우 원래 마이그레이션된 앱을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-130">Once you feel that a desired number of client apps in the wild have updated to the latest version, you can delete the original migrated app if you desire.</span></span> <span data-ttu-id="285ec-131">동일한 앱 서비스 계획에서 모바일 앱으로 호스팅되는 경우 금전적인 추가 비용이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-131">It doesn't incur any additional monetary costs, if hosted in the same App Service plan as your Mobile App.</span></span>

<span data-ttu-id="285ec-132">업그레이드 프로세스에 대한 전체 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-132">The full outline for the upgrade process is as follows:</span></span>

1. <span data-ttu-id="285ec-133">기존(마이그레이션된) Azure 모바일 서비스를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-133">Download your existing (migrated) Azure Mobile Service.</span></span>
2. <span data-ttu-id="285ec-134">호환성 패키지를 사용하여 프로젝트를 Azure 모바일 앱으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-134">Convert the project to an Azure Mobile App using the compatibility package.</span></span>
3. <span data-ttu-id="285ec-135">모든 차이(예: 인증 설정)를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-135">Correct any differences (such as authentication settings).</span></span>
4. <span data-ttu-id="285ec-136">새 앱 서비스에 변환된 Azure 모바일 앱 프로젝트를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-136">Deploy your converted Azure Mobile App project to a new App Service.</span></span>
5. <span data-ttu-id="285ec-137">새 모바일 앱을 사용하는 새 버전의 클라이언트 응용 프로그램을 릴리스합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-137">Release a new version of your client application that use the new Mobile App.</span></span>
6. <span data-ttu-id="285ec-138">(선택 사항) 원래 마이그레이션된 모바일 서비스 앱 삭제</span><span class="sxs-lookup"><span data-stu-id="285ec-138">(Optional) Delete your original migrated mobile service app.</span></span>

<span data-ttu-id="285ec-139">삭제는 원래 마이그레이션된 모바일 서비스에 트래픽이 표시되지 않을 때 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-139">Deletion can occur when you don't see any traffic on your original migrated mobile service.</span></span>

## <span data-ttu-id="285ec-140"><a name="install-npm-package"></a> 필수 조건 설치</span><span class="sxs-lookup"><span data-stu-id="285ec-140"><a name="install-npm-package"></a> Install the Pre-requisites</span></span>
<span data-ttu-id="285ec-141">로컬 컴퓨터에 [노드]를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-141">You should install [Node] on your local machine.</span></span>  <span data-ttu-id="285ec-142">또한 호환성 패키지를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-142">You should also install the compatibility package.</span></span>  <span data-ttu-id="285ec-143">노드를 설치한 후 새 cmd 또는 PowerShell 프롬프트에서 다음 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-143">After Node is installed, you can run the following command from a new cmd or PowerShell prompt:</span></span>

```npm i -g azure-mobile-apps-compatibility```

## <span data-ttu-id="285ec-144"><a name="obtain-ams-scripts"></a> Azure 모바일 서비스 스크립트 가져오기</span><span class="sxs-lookup"><span data-stu-id="285ec-144"><a name="obtain-ams-scripts"></a> Obtain your Azure Mobile Services Scripts</span></span>
* <span data-ttu-id="285ec-145">[Azure 포털]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-145">Log in to the [Azure Portal].</span></span>
* <span data-ttu-id="285ec-146">**모든 리소스** 또는 **앱 서비스**를 사용하여 모바일 서비스 사이트를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-146">Using **All Resources** or **App Services**, find your Mobile Services site.</span></span>
* <span data-ttu-id="285ec-147">사이트 내에서 **도구** -> **Kudu** -> **이동**을 클릭하여 Kudu 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-147">Within the site, click on **Tools** -> **Kudu** -> **Go** to open the Kudu site.</span></span>
* <span data-ttu-id="285ec-148">**디버그 콘솔** -> **PowerShell**을 클릭하여 디버그 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-148">Click on **Debug Console** -> **PowerShell** to open the Debug console.</span></span>
* <span data-ttu-id="285ec-149">각 디렉터리를 차례로 클릭하여 `site/wwwroot/App_Data/config` (으)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-149">Navigate to `site/wwwroot/App_Data/config` by clicking on each directory in turn</span></span>
* <span data-ttu-id="285ec-150">`scripts` 디렉터리 옆에 있는 다운로드 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-150">Click on the download icon next to the `scripts` directory.</span></span>

<span data-ttu-id="285ec-151">ZIP 형식의 스크립트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-151">This will download the scripts in ZIP format.</span></span>  <span data-ttu-id="285ec-152">로컬 컴퓨터에 새 디렉터리를 만들고 디렉터리 내의 `scripts.ZIP` 파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-152">Create a new directory on your local machine and unpack the `scripts.ZIP` file within the directory.</span></span>  <span data-ttu-id="285ec-153">`scripts` 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-153">This will create a `scripts` directory.</span></span>

## <span data-ttu-id="285ec-154"><a name="scaffold-app"></a> 새 Azure 모바일 앱 백 엔드 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="285ec-154"><a name="scaffold-app"></a> Scaffold the new Azure Mobile Apps backend</span></span>
<span data-ttu-id="285ec-155">스크립트 디렉터리를 포함하는 디렉터리에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-155">Run the following command from the directory containing the scripts directory:</span></span>

```scaffold-mobile-app scripts out```

<span data-ttu-id="285ec-156">`out` 디렉터리에 스캐폴드된 Azure 모바일 앱 백 엔드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-156">This will create a scaffolded Azure Mobile Apps backend in the `out` directory.</span></span>  <span data-ttu-id="285ec-157">필수는 아니지만 `out` 디렉터리를 소스 코드 리포지토리로 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-157">Although not required, it's a good idea to check the `out` directory into a source code repository of your choice.</span></span>

## <span data-ttu-id="285ec-158"><a name="deploy-ama-app"></a> Azure 모바일 앱 백 엔드 배포</span><span class="sxs-lookup"><span data-stu-id="285ec-158"><a name="deploy-ama-app"></a> Deploy your Azure Mobile Apps backend</span></span>
<span data-ttu-id="285ec-159">배포하는 동안 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-159">During deployment, you will need to do the following:</span></span>

1. <span data-ttu-id="285ec-160">[Azure 포털]에서 새 모바일 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-160">Create a new Mobile App in the [Azure Portal].</span></span>
2. <span data-ttu-id="285ec-161">연결된 데이터베이스에서 `createViews.sql` 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-161">Run the `createViews.sql` script on your connected database.</span></span>
3. <span data-ttu-id="285ec-162">모바일 서비스에 연결된 데이터베이스를 새 앱 서비스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-162">Link the database that is linked to your Mobile Service to your new App Service.</span></span>
4. <span data-ttu-id="285ec-163">다른 리소스(예: 알림 허브)를 새로운 앱 서비스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-163">Link any other resources (such as Notification Hubs) to the new App Service.</span></span>
5. <span data-ttu-id="285ec-164">새 사이트에 생성된 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-164">Deploy the generated code to your new site.</span></span>

### <a name="create-a-new-mobile-app"></a><span data-ttu-id="285ec-165">새 모바일 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="285ec-165">Create a new Mobile App</span></span>
1. <span data-ttu-id="285ec-166">[Azure 포털]에서 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-166">Log in at the [Azure Portal].</span></span>
2. <span data-ttu-id="285ec-167">**+새로 만들기** > **웹 + 모바일** > **모바일 앱**을 클릭한 다음 모바일 앱 백 엔드에 대한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-167">Click **+NEW** > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="285ec-168">**리소스 그룹**에 대해 기존 리소스 그룹을 선택하거나 새 리소스 그룹을 만듭니다(앱과 같은 이름 사용).</span><span class="sxs-lookup"><span data-stu-id="285ec-168">For the **Resource Group**, select an existing resource group, or create a new one (using the same name as your app.)</span></span>

    <span data-ttu-id="285ec-169">다른 앱 서비스 계획을 선택하거나 새 앱 서비스 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-169">You can either select another App Service plan or create a new one.</span></span> <span data-ttu-id="285ec-170">앱 서비스 계획에 대한 자세한 내용과 다른 가격 책정 계층 및 원하는 위치에서 새 계획을 만드는 방법은 [Azure 앱 서비스 계획의 포괄 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="285ec-170">For more about App Services plans and how to create a new plan in a different pricing tier and in your desired location, see [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
4. <span data-ttu-id="285ec-171">**앱 서비스 계획**에 대해서는 기본 계획( [표준 계층](https://azure.microsoft.com/pricing/details/app-service/)에)이 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-171">For the **App Service plan**, the default plan (in the [Standard tier](https://azure.microsoft.com/pricing/details/app-service/)) is selected.</span></span> <span data-ttu-id="285ec-172">또한 다른 계획을 선택하거나 [새 계획을 만들 수 있습니다](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="285ec-172">You can also  select a different plan, or [create a new one](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan).</span></span> <span data-ttu-id="285ec-173">앱 서비스 계획의 설정에 따라 앱과 연결된 [위치, 기능, 비용 및 계산 리소스](https://azure.microsoft.com/pricing/details/app-service/) 가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-173">The App Service plan's settings determine the [location, features, cost and compute resources](https://azure.microsoft.com/pricing/details/app-service/) associated with your app.</span></span>

    <span data-ttu-id="285ec-174">계획을 결정한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-174">After you decide on the plan, click **Create**.</span></span> <span data-ttu-id="285ec-175">이렇게 모바일 앱 백 엔드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-175">This creates the Mobile App backend.</span></span>

### <a name="run-createviewssql"></a><span data-ttu-id="285ec-176">CreateViews.SQL을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-176">Run CreateViews.SQL</span></span>
<span data-ttu-id="285ec-177">스캐폴드된 앱은 `createViews.sql`(이)라는 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-177">The scaffolded app contains a file called `createViews.sql`.</span></span>  <span data-ttu-id="285ec-178">이 스크립트는 대상 데이터베이스에 대해 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-178">This script must be executed against the target database.</span></span>  <span data-ttu-id="285ec-179">대상 데이터베이스에 대한 연결 문자열은 **연결 문자열** 아래 **설정** 블레이드의 마이그레이션된 모바일 서비스에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-179">The connection string for the target database can be obtained from your migrated mobile service from the **Settings** blade under **Connection Strings**.</span></span>  <span data-ttu-id="285ec-180">`MS_TableConnectionString`(이)라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-180">It is named `MS_TableConnectionString`.</span></span>

<span data-ttu-id="285ec-181">SQL Server Management Studio 또는 Visual Studio 내에서 이 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-181">You can run this script from within SQL Server Management Studio or Visual Studio.</span></span>

### <a name="link-the-database-to-your-app-service"></a><span data-ttu-id="285ec-182">데이터베이스를 앱 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="285ec-182">Link the Database to your App Service</span></span>
<span data-ttu-id="285ec-183">기존 데이터베이스를 앱 서비스에 연결:</span><span class="sxs-lookup"><span data-stu-id="285ec-183">Link the existing database to your App Service:</span></span>

* <span data-ttu-id="285ec-184">[Azure 포털]에서 앱 서비스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-184">In the [Azure Portal], open your App Service.</span></span>
* <span data-ttu-id="285ec-185">**모든 설정** -> **데이터 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-185">Select **All Settings** -> **Data Connections**.</span></span>
* <span data-ttu-id="285ec-186">**+ 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-186">Click on **+ Add**.</span></span>
* <span data-ttu-id="285ec-187">드롭다운 목록에서 **SQL 데이터베이스**</span><span class="sxs-lookup"><span data-stu-id="285ec-187">In the drop-down, select **SQL Database**</span></span>
* <span data-ttu-id="285ec-188">**SQL Database** 아래에서 기존 데이터베이스를 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-188">Under **SQL Database**, select your existing database, then click on **Select**.</span></span>
* <span data-ttu-id="285ec-189">**연결 문자열** 아래에서 데이터베이스에 대한 사용자 이름 및 암호를 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-189">Under **Connection string**, enter the username and password for the database, then click on **OK**.</span></span>
* <span data-ttu-id="285ec-190">**데이터 연결 추가** 블레이드에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-190">In the **Add data connections** blade, click on **OK**.</span></span>

<span data-ttu-id="285ec-191">마이그레이션된 모바일 서비스에서 대상 데이터베이스에 대한 연결 문자열을 확인하여 사용자 이름 및 암호를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-191">The username and password can be found by viewing the Connection String for the target database in your migrated Mobile Service.</span></span>

### <a name="set-up-authentication"></a><span data-ttu-id="285ec-192">인증 설정</span><span class="sxs-lookup"><span data-stu-id="285ec-192">Set up authentication</span></span>
<span data-ttu-id="285ec-193">Azure 모바일 앱을 사용하면 서비스 내에서 Azure Active Directory, Facebook, Google, Microsoft 및 Twitter 인증을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-193">Azure Mobile Apps allows you to configure Azure Active Directory, Facebook, Google, Microsoft and Twitter authentication within the service.</span></span>  <span data-ttu-id="285ec-194">사용자 지정 인증을 개별적으로 개발해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-194">Custom authentication will need to be developed separately.</span></span>  <span data-ttu-id="285ec-195">자세한 내용은 [인증 개념] 설명서 및 [인증 빠른 시작] 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="285ec-195">Refer to the [Authentication Concepts] documentation and [Authentication Quickstart] documentation for more information.</span></span>  

## <span data-ttu-id="285ec-196"><a name="updating-clients"></a>모바일 클라이언트 업데이트</span><span class="sxs-lookup"><span data-stu-id="285ec-196"><a name="updating-clients"></a>Update Mobile clients</span></span>
<span data-ttu-id="285ec-197">작동하는 모바일 앱 백 엔드가 있으면 그것을 사용하는 클라이언트 응용 프로그램의 새 버전에서 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-197">Once you have an operational Mobile App backend, you can work on a new version of your client application which consumes it.</span></span> <span data-ttu-id="285ec-198">또한 모바일 앱은 클라이언트 SDK의 새 버전을 포함하고 위의 서버 업그레이드와 유사합니다. 따라서 모바일 앱 버전을 설치하기 전에 모바일 서비스 SDK에 대한 모든 참조를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-198">Mobile Apps also includes a new version of the client SDKs, and similar to the server upgrade above, you will need to remove all references to the Mobile Services SDKs before installing the Mobile Apps versions.</span></span>

<span data-ttu-id="285ec-199">버전 간의 주요 변경 사항 중 하나는 생성자가 응용 프로그램 키를 더 이상 필요로 하지 않는다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-199">One of the main changes between the versions is that the constructors no longer require an application key.</span></span>
<span data-ttu-id="285ec-200">이제 모바일 앱의 URL에 간단히 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-200">You now simply pass in the URL of your Mobile App.</span></span> <span data-ttu-id="285ec-201">예를 들어 .NET 클라이언트에서 `MobileServiceClient` 생성자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-201">For example, on the .NET clients, the `MobileServiceClient` constructor is now:</span></span>

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of the Mobile App
        );

<span data-ttu-id="285ec-202">아래 링크를 통해 새 SDK를 설치하고 새 구조를 사용하는 데 대한 내용을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-202">You can read about installing the new SDKs and using the new structure via the links below:</span></span>

* [<span data-ttu-id="285ec-203">Android 버전 2.2 이상</span><span class="sxs-lookup"><span data-stu-id="285ec-203">Android version 2.2 or later</span></span>](app-service-mobile-android-how-to-use-client-library.md)
* [<span data-ttu-id="285ec-204">iOS 버전 3.0.0 이상</span><span class="sxs-lookup"><span data-stu-id="285ec-204">iOS version 3.0.0 or later</span></span>](app-service-mobile-ios-how-to-use-client-library.md)
* [<span data-ttu-id="285ec-205">.NET(Windows/Xamarin) 버전 2.0.0 이상</span><span class="sxs-lookup"><span data-stu-id="285ec-205">.NET (Windows/Xamarin) version 2.0.0 or later</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)
* [<span data-ttu-id="285ec-206">Apache Cordova 버전 2.0 이상</span><span class="sxs-lookup"><span data-stu-id="285ec-206">Apache Cordova version 2.0 or later</span></span>](app-service-mobile-cordova-how-to-use-client-library.md)

<span data-ttu-id="285ec-207">응용 프로그램이 푸시 알림을 사용하면 일부 변경 사항이 있는 경우와 같이 각 플랫폼에 대한 특정 등록 지침을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-207">If your application makes use of push notifications, make note of the specific registration instructions for each platform, as there have been some changes there as well.</span></span>

<span data-ttu-id="285ec-208">새 클라이언트 버전을 준비할 때 업그레이드된 서버 프로젝트에 사용해보세요.</span><span class="sxs-lookup"><span data-stu-id="285ec-208">When you have the new client version ready, try it out against your upgraded server project.</span></span> <span data-ttu-id="285ec-209">작동하는지 유효성을 검사한 후에 고객에게 응용 프로그램의 새 버전을 릴리스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-209">After validating that it works, you can release a new version of your application to customers.</span></span> <span data-ttu-id="285ec-210">결국 고객이 이러한 업데이트를 받고 나면 모바일 서비스 버전의 앱을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-210">Eventually, once your customers have had a chance to receive these updates, you can delete the Mobile Services version of your app.</span></span> <span data-ttu-id="285ec-211">이 시점에서 최신 모바일 앱 서버 SDK를 사용하여 앱 서비스 모바일 앱의 업그레이드를 완전히 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="285ec-211">At this point, you have completely upgraded to an App Service Mobile App using the latest Mobile Apps server SDK.</span></span>

<!-- URLs. -->

<span data-ttu-id="285ec-212">[Azure portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="285ec-212">[Azure portal]: https://portal.azure.com/</span></span>
[Azure classic portal]: https://manage.windowsazure.com/
<span data-ttu-id="285ec-213">[모바일 앱 정의]: app-service-mobile-value-prop.md</span><span class="sxs-lookup"><span data-stu-id="285ec-213">[What are Mobile Apps?]: app-service-mobile-value-prop.md</span></span>
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications to your mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication to your mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How to use the .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services to an App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service to App Service]: app-service-mobile-migrating-from-mobile-services.md
<span data-ttu-id="285ec-214">[앱 서비스 가격 책정]: https://azure.microsoft.com/en-us/pricing/details/app-service/</span><span class="sxs-lookup"><span data-stu-id="285ec-214">[App Service pricing]: https://azure.microsoft.com/en-us/pricing/details/app-service/</span></span>
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
<span data-ttu-id="285ec-215">[인증 개념]: ../app-service/app-service-authentication-overview.md</span><span class="sxs-lookup"><span data-stu-id="285ec-215">[Authentication Concepts]: ../app-service/app-service-authentication-overview.md</span></span>
<span data-ttu-id="285ec-216">[인증 빠른 시작]: app-service-mobile-auth.md</span><span class="sxs-lookup"><span data-stu-id="285ec-216">[Authentication Quickstart]: app-service-mobile-auth.md</span></span>

<span data-ttu-id="285ec-217">[Azure 포털]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="285ec-217">[Azure Portal]: https://portal.azure.com/</span></span>
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
