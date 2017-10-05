---
title: "모바일 서비스에서 앱 서비스 모바일 앱으로 마이그레이션"
description: "모바일 서비스 응용 프로그램을 앱 서비스 모바일 앱으로 쉽게 마이그레이션하는 방법을 알아봅니다."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 07507ea2-690f-4f79-8776-3375e2adeb9e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: glenga
ms.openlocfilehash: 16cf05f62602e494affed49e466209b68413e53a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="24d14-103"><a name="article-top"></a>기존 Azure 모바일 서비스를 Azure 앱 서비스로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="24d14-103"><a name="article-top"></a>Migrate your existing Azure Mobile Service to Azure App Service</span></span>
<span data-ttu-id="24d14-104">[Azure 앱 서비스의 일반적인 가용성]을 사용하여 Azure 모바일 서비스 사이트를 쉽게 원래 위치로 마이그레이션하여 Azure 앱 서비스의 모든 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-104">With the [general availability of Azure App Service], Azure Mobile Services sites can be easily migrated in-place to take advantage of all the features of the Azure App Service.</span></span>  <span data-ttu-id="24d14-105">이 문서에서는 Azure 모바일 서비스에서 Azure 앱 서비스에 사이트를 마이그레이션하는 경우의 결과를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-105">This document explains what to expect when migrating your site from Azure Mobile Services to Azure App Service.</span></span>

## <span data-ttu-id="24d14-106"><a name="what-does-migration-do"></a>사이트에 대한 마이그레이션의 기능</span><span class="sxs-lookup"><span data-stu-id="24d14-106"><a name="what-does-migration-do"></a>What does migration do to your site</span></span>
<span data-ttu-id="24d14-107">Azure Mobile Services의 마이그레이션은 코드에 영향을 주지 않고 Mobile Services를 [Azure App Service] 앱으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-107">Migration of your Azure Mobile Service turns your Mobile Service into an [Azure App Service] app without affecting the code.</span></span>  <span data-ttu-id="24d14-108">Notification Hubs, SQL 데이터 연결, 인증 설정, 예약된 작업 및 도메인 이름은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-108">Your Notification Hubs, SQL data connection, authentication settings, scheduled jobs, and domain name remain unchanged.</span></span>  <span data-ttu-id="24d14-109">Azure Mobile Services를 사용하는 모바일 클라이언트는 정상적으로 계속 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-109">Mobile clients using your Azure Mobile Service continue to operate normally.</span></span>  <span data-ttu-id="24d14-110">마이그레이션이 Azure App Service에 전송되면 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-110">Migration restarts your service once it is transferred to Azure App Service.</span></span>

[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

## <span data-ttu-id="24d14-111"><a name="why-migrate"></a>사이트를 마이그레이션해야 하는 이유</span><span class="sxs-lookup"><span data-stu-id="24d14-111"><a name="why-migrate"></a>Why you should migrate your site</span></span>
<span data-ttu-id="24d14-112">Microsoft는 다음을 비롯한 Azure 앱 서비스의 기능을 활용하기 위해 Azure 모바일 서비스를 마이그레이션하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-112">Microsoft is recommending that you migrate your Azure Mobile Service to take advantage of the features of Azure App Service, including:</span></span>

* <span data-ttu-id="24d14-113">[WebJobs] 및 [사용자 지정 도메인 이름]을 포함하는 새로운 호스트 기능.</span><span class="sxs-lookup"><span data-stu-id="24d14-113">New host features, including [WebJobs] and [custom domain names].</span></span>
* <span data-ttu-id="24d14-114">[하이브리드 연결] 외에 [VNet]을 사용하여 온-프레미스 리소스에 연결.</span><span class="sxs-lookup"><span data-stu-id="24d14-114">Connectivity to your on-premises resources using [VNet] in addition to [Hybrid Connections].</span></span>
* <span data-ttu-id="24d14-115">New Relic 또는 [Application Insights]를 통한 모니터링 및 문제 해결.</span><span class="sxs-lookup"><span data-stu-id="24d14-115">Monitoring and troubleshooting with New Relic or [Application Insights].</span></span>
* <span data-ttu-id="24d14-116">[스테이징 슬롯], 롤백 및 프로덕션 내 테스트를 포함하는 기본 제공 DevOps 도구.</span><span class="sxs-lookup"><span data-stu-id="24d14-116">Built-in DevOps tooling, including [staging slots], roll-back, and in-production testing.</span></span>
* <span data-ttu-id="24d14-117">[자동 크기 조정], 부하 분산 및 [성능 모니터링].</span><span class="sxs-lookup"><span data-stu-id="24d14-117">[Auto-scale], load balancing, and [performance monitoring].</span></span>

<span data-ttu-id="24d14-118">Azure 앱 서비스의 이점에 대한 자세한 내용은 [모바일 서비스 vs. App Service] 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24d14-118">For more information on the benefits of Azure App Service, see the [Mobile Services vs. App Service] topic.</span></span>

## <span data-ttu-id="24d14-119"><a name="before-you-begin"></a>시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="24d14-119"><a name="before-you-begin"></a>Before you begin</span></span>
<span data-ttu-id="24d14-120">사이트에서 주요 작업을 시작하기 전에 모바일 서비스 스크립트와 SQL Database를 백업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-120">Before beginning any major work on your site, you should back up your Mobile Service scripts and SQL database.</span></span>

## <span data-ttu-id="24d14-121"><a name="migrating-site"></a>사이트 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="24d14-121"><a name="migrating-site"></a>Migrating your sites</span></span>
<span data-ttu-id="24d14-122">마이그레이션 프로세스는 단일 Azure 지역 내의 모든 사이트를 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-122">The migration process migrates all sites within a single Azure Region.</span></span>

<span data-ttu-id="24d14-123">사이트를 마이그레이션하려면:</span><span class="sxs-lookup"><span data-stu-id="24d14-123">To migrate your site:</span></span>

1. <span data-ttu-id="24d14-124">[Azure 클래식 포털]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-124">Log in to the [Azure Classic Portal].</span></span>
2. <span data-ttu-id="24d14-125">마이그레이션할 지역의 모바일 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-125">Select a Mobile Service in the region you wish to migrate.</span></span>
3. <span data-ttu-id="24d14-126">**App Service로 마이그레이션** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-126">Click the **Migrate to App Service** button.</span></span>

   ![마이그레이션 단추][0]
4. <span data-ttu-id="24d14-128">앱 서비스 대화 상자에 마이그레이션을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-128">Read the Migrate to App Service dialog.</span></span>
5. <span data-ttu-id="24d14-129">제공된 상자에 모바일 서비스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-129">Enter the name of your Mobile Service in the box provided.</span></span>  <span data-ttu-id="24d14-130">예를 들어 도메인 이름이 contoso.azure mobile.net이면 제공된 상자에 *contoso* 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-130">For example, if your domain name is contoso.azure-mobile.net, then enter *contoso* in the box provided.</span></span>
6. <span data-ttu-id="24d14-131">눈금 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-131">Click the tick button.</span></span>

<span data-ttu-id="24d14-132">작업 모니터에서 마이그레이션의 상태를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-132">Monitor the status of the migration in the activity monitor.</span></span> <span data-ttu-id="24d14-133">사이트는 Azure 클래식 포털에서 *마이그레이션 중*으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-133">Your site is listed as *migrating* in the Azure Classic Portal.</span></span>

  ![마이그레이션 작업 모니터링][1]

<span data-ttu-id="24d14-135">각 마이그레이션은 마이그레이션되는 모바일 서비스 당 3-15분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-135">Each migration can take anywhere from 3 to 15 minutes per mobile service being migrated.</span></span>  <span data-ttu-id="24d14-136">마이그레이션하는 동안 사이트를 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-136">Your site remains available during the migration.</span></span>
<span data-ttu-id="24d14-137">사이트는 마이그레이션 프로세스가 끝나면 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-137">Your site is restarted at the end of the migration process.</span></span>  <span data-ttu-id="24d14-138">다시 시작 프로세스 동안 사이트는 사용할 수 없게 되며 몇 초 동안 지속될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-138">The site is unavailable during the restart process, which may last a couple of seconds.</span></span>

## <span data-ttu-id="24d14-139"><a name="finalizing-migration"></a>마이그레이션 완료</span><span class="sxs-lookup"><span data-stu-id="24d14-139"><a name="finalizing-migration"></a>Finalizing the Migration</span></span>
<span data-ttu-id="24d14-140">마이그레이션 프로세스가 끝날 때 모바일 클라이언트에서 사이트를 테스트하도록 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-140">Plan to test your site from a mobile client at the conclusion of the migration process.</span></span>  <span data-ttu-id="24d14-141">모바일 클라이언트를 변경하지 않고 일반적인 모든 클라이언트 작업을 수행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-141">Ensure you can perform all common client actions without changes to the mobile client.</span></span>  

### <span data-ttu-id="24d14-142"><a name="update-app-service-tier"></a>적절한 앱 서비스 가격 책정 계층 선택</span><span class="sxs-lookup"><span data-stu-id="24d14-142"><a name="update-app-service-tier"></a>Select an appropriate App Service pricing tier</span></span>
<span data-ttu-id="24d14-143">Azure 앱 서비스를 마이그레이션한 후에 가격 책정에 유연성이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-143">You have more flexibility in pricing after you migrate to Azure App Service.</span></span>

1. <span data-ttu-id="24d14-144">[Azure 포털]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-144">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="24d14-145">**모든 리소스** 또는 **App Service**를 선택한 후 마이그레이션된 Mobile Services의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-145">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="24d14-146">설정 블레이드가 기본적으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-146">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="24d14-147">설정 메뉴에서 **App Service 계획**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-147">Click **App Service Plan** in the Settings menu.</span></span>
5. <span data-ttu-id="24d14-148">**가격 책정 계층** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-148">Click the **Pricing Tier** tile.</span></span>
6. <span data-ttu-id="24d14-149">요구 사항에 적합한 타일을 클릭한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-149">Click the tile appropriate to your requirements, then Click **Select**.</span></span>  <span data-ttu-id="24d14-150">**모두 보기**를 클릭하여 사용 가능한 가격 책정 계층을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-150">You may need to Click **View all** to see the available pricing tiers.</span></span>

<span data-ttu-id="24d14-151">시작 지점으로 다음 계층이 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-151">As a starting point, we recommend the following tiers:</span></span>

| <span data-ttu-id="24d14-152">모바일 서비스 가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="24d14-152">Mobile Service Pricing Tier</span></span> | <span data-ttu-id="24d14-153">앱 서비스 가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="24d14-153">App Service Pricing Tier</span></span> |
|:--- |:--- |
| <span data-ttu-id="24d14-154">무료</span><span class="sxs-lookup"><span data-stu-id="24d14-154">Free</span></span> |<span data-ttu-id="24d14-155">F1 무료</span><span class="sxs-lookup"><span data-stu-id="24d14-155">F1 Free</span></span> |
| <span data-ttu-id="24d14-156">Basic</span><span class="sxs-lookup"><span data-stu-id="24d14-156">Basic</span></span> |<span data-ttu-id="24d14-157">B1 기본</span><span class="sxs-lookup"><span data-stu-id="24d14-157">B1 Basic</span></span> |
| <span data-ttu-id="24d14-158">표준</span><span class="sxs-lookup"><span data-stu-id="24d14-158">Standard</span></span> |<span data-ttu-id="24d14-159">S1 표준</span><span class="sxs-lookup"><span data-stu-id="24d14-159">S1 Standard</span></span> |

<span data-ttu-id="24d14-160">응용 프로그램에 대한 올바른 가격 책정 계층을 선택하는 데 유연성을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-160">There is considerable flexibility in choosing the right pricing tier for your application.</span></span>  <span data-ttu-id="24d14-161">새 앱 서비스의 가격 책정에 대한 자세한 내용은 [앱 서비스 가격] 을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-161">Refer to [App Service Pricing] for full details on the pricing of your new App Service.</span></span>

> [!TIP]
> <span data-ttu-id="24d14-162">App Service 표준 계층은 [스테이징 슬롯], 자동 백업, 자동 크기 조정을 비롯한 사용하려는 다양한 기능에 대한 액세스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-162">The App Service Standard tier contains access to many features that you may want to use, including [staging slots], automatic backups, and auto-scaling.</span></span>  <span data-ttu-id="24d14-163">이 때 새로운 기능을 확인해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="24d14-163">Check out the new capabilities while you are there!</span></span>
>
>

### <span data-ttu-id="24d14-164"><a name="review-migration-scheduler-jobs"></a>마이그레이션된 스케줄러 작업 검토</span><span class="sxs-lookup"><span data-stu-id="24d14-164"><a name="review-migration-scheduler-jobs"></a>Review the Migrated Scheduler Jobs</span></span>
<span data-ttu-id="24d14-165">스케줄러 작업은 마이그레이션 후에 약 30분까지 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-165">Scheduler Jobs will not be visible until approximately 30 minutes after migration.</span></span>  <span data-ttu-id="24d14-166">예약된 작업은 백그라운드에서 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-166">Scheduled jobs continue to run in the background.</span></span>
<span data-ttu-id="24d14-167">다시 표시된 예약된 작업을 보려면</span><span class="sxs-lookup"><span data-stu-id="24d14-167">To view your scheduled jobs after they are visible again:</span></span>

1. <span data-ttu-id="24d14-168">[Azure 포털]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-168">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="24d14-169">**찾아보기>**를 선택하고 *필터* 상자에 **일정**을 입력한 다음 **스케줄러 컬렉션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-169">Select **Browse>**, enter **Schedule** in the *Filter* box, then select **Scheduler Collections**.</span></span>

<span data-ttu-id="24d14-170">마이그레이션 후에 사용 가능한 무료 스케줄러 작업의 수가 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-170">There are a limited number of free scheduler jobs available post-migration.</span></span>  <span data-ttu-id="24d14-171">사용량 및 [Azure 스케줄러 계획]을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-171">Review your usage and the [Azure Scheduler Plans].</span></span>

### <span data-ttu-id="24d14-172"><a name="configure-cors"></a>필요한 경우 CORS 구성</span><span class="sxs-lookup"><span data-stu-id="24d14-172"><a name="configure-cors"></a>Configure CORS if needed</span></span>
<span data-ttu-id="24d14-173">원본 간 리소스 공유는 웹 사이트가 다른 도메인의 Web API에 액세스하도록 허용하는 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-173">Cross-origin resource sharing is a technique to allow a website to access a Web API on a different domain.</span></span>  <span data-ttu-id="24d14-174">관련된 웹 사이트를 통해 Azure 모바일 서비스를 사용하면 마이그레이션의 일부로 CORS를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-174">If you are using Azure Mobile Services with an associated website, then you need to configure CORS as part of the migration.</span></span>  <span data-ttu-id="24d14-175">Azure 모바일 서비스를 모바일 장치에서 단독으로 액세스하는 경우 드문 경우를 제외하고 CORS를 구성할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-175">If you are accessing Azure Mobile Services exclusively from mobile devices, then CORS does not need to be configured except in rare cases.</span></span>

<span data-ttu-id="24d14-176">마이그레이션된 CORS 설정은 **MS_CrossDomainWhitelist** 앱 설정으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-176">Your migrated CORS settings are available as the **MS_CrossDomainWhitelist** App Setting.</span></span>  <span data-ttu-id="24d14-177">앱 서비스의 CORS 기능에 사이트를 마이그레이션하려면:</span><span class="sxs-lookup"><span data-stu-id="24d14-177">To migrate your site to the App Service CORS facility:</span></span>

1. <span data-ttu-id="24d14-178">[Azure 포털]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-178">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="24d14-179">**모든 리소스** 또는 **App Service**를 선택한 후 마이그레이션된 Mobile Services의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-179">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="24d14-180">설정 블레이드가 기본적으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-180">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="24d14-181">API 메뉴에서 **CORS**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-181">Click **CORS** in the API menu.</span></span>
5. <span data-ttu-id="24d14-182">제공된 상자에 허용된 원본을 입력하고 각각 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-182">Enter any Allowed Origins in the box provided, pressing Enter after each one.</span></span>
6. <span data-ttu-id="24d14-183">허용된 원본 목록이 올바르면 저장 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-183">Once your list of Allowed Origins is correct, click the Save button.</span></span>

> [!TIP]
> <span data-ttu-id="24d14-184">Azure 앱 서비스의 장점 중 하나는 동일한 사이트에서 웹 사이트 및 모바일 서비스를 실행할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-184">One of the advantages of using an Azure App Service is that you can run your web site and mobile service on the same site.</span></span>  <span data-ttu-id="24d14-185">자세한 내용은 [다음 단계](#next-steps) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24d14-185">For more information, see the [next steps](#next-steps) section.</span></span>
>
>

### <span data-ttu-id="24d14-186"><a name="download-publish-profile"></a>새 게시 프로필 다운로드</span><span class="sxs-lookup"><span data-stu-id="24d14-186"><a name="download-publish-profile"></a>Download a new Publishing Profile</span></span>
<span data-ttu-id="24d14-187">Azure 앱 서비스로 마이그레이션할 때 사이트의 게시 프로필이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-187">The publishing profile of your site is changed when migrating to Azure App Service.</span></span>  <span data-ttu-id="24d14-188">Visual Studio 내에서 사이트를 게시하려면 새 게시 프로필이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-188">If you intend to publish your site from within Visual Studio, you need a new publishing profile.</span></span>  <span data-ttu-id="24d14-189">새 게시 프로필을 다운로드하려면</span><span class="sxs-lookup"><span data-stu-id="24d14-189">To download the new publishing profile:</span></span>

1. <span data-ttu-id="24d14-190">[Azure 포털]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-190">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="24d14-191">**모든 리소스** 또는 **App Service**를 선택한 후 마이그레이션된 Mobile Services의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-191">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="24d14-192">**게시 프로필 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-192">Click **Get publish profile**.</span></span>

<span data-ttu-id="24d14-193">PublishSettings 파일이 컴퓨터에 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-193">The PublishSettings file is downloaded to your computer.</span></span>  <span data-ttu-id="24d14-194">일반적으로 파일 이름은 *sitename*.PublishSettings입니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-194">It is normally called *sitename*.PublishSettings.</span></span>  <span data-ttu-id="24d14-195">기존 프로젝트에 게시 설정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-195">Import the publish settings into your existing project:</span></span>

1. <span data-ttu-id="24d14-196">Visual Studio 및 Azure 모바일 서비스 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-196">Open Visual Studio and your Azure Mobile Service project.</span></span>
2. <span data-ttu-id="24d14-197">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-197">Right-Click your project in the **Solution Explorer** and select **Publish...**</span></span>
3. <span data-ttu-id="24d14-198">**가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-198">Click **Import**</span></span>
4. <span data-ttu-id="24d14-199">**찾아보기**를 클릭하고 다운로드한 게시 설정 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-199">Click **Browse** and select your downloaded publish settings file.</span></span>  <span data-ttu-id="24d14-200">**확인**</span><span class="sxs-lookup"><span data-stu-id="24d14-200">Click **OK**</span></span>
5. <span data-ttu-id="24d14-201">**연결 유효성 검사**를 클릭하여 게시 설정이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-201">Click **Validate Connection** to ensure the publish settings work.</span></span>
6. <span data-ttu-id="24d14-202">**게시**를 클릭하여 사이트를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-202">Click **Publish** to publish your site.</span></span>

## <span data-ttu-id="24d14-203"><a name="working-with-your-site"></a>마이그레이션 후에 사이트로 작업</span><span class="sxs-lookup"><span data-stu-id="24d14-203"><a name="working-with-your-site"></a>Working with your site post-migration</span></span>
<span data-ttu-id="24d14-204">마이그레이션 후에 [Azure 포털]에서 새 App Service로 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-204">Start working with your new App Service in the [Azure portal] post-migration.</span></span>  <span data-ttu-id="24d14-205">다음은 해당하는 앱 서비스와 함께 [Azure 클래식 포털]에서 수행하는 데 사용되는 몇 가지 주의 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-205">The following are some notes on specific operations that you used to perform in the [Azure Classic Portal], together with their App Service equivalent.</span></span>

### <span data-ttu-id="24d14-206"><a name="publishing-your-site"></a>마이그레이션된 사이트 다운로드 및 게시</span><span class="sxs-lookup"><span data-stu-id="24d14-206"><a name="publishing-your-site"></a>Downloading and Publishing your migrated site</span></span>
<span data-ttu-id="24d14-207">사이트는 git 또는 ftp를 통해 사용될 수 있고 WebDeploy, TFS, Mercurial, GitHub, FTP 등 다양한 메커니즘을 사용하여 다시 게시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-207">Your site is available via git or ftp and can be republished with various different mechanisms, including WebDeploy, TFS, Mercurial, GitHub, and FTP.</span></span>  <span data-ttu-id="24d14-208">배포 자격 증명은 사이트의 나머지 부분을 통해 마이그레이션됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-208">The deployment credentials are migrated with the rest of your site.</span></span>  <span data-ttu-id="24d14-209">배포 자격 증명을 설정하지 않거나 기억하지 못하는 경우 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-209">If you did not set your deployment credentials or you do not remember them, you can reset them:</span></span>

1. <span data-ttu-id="24d14-210">[Azure 포털]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-210">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="24d14-211">**모든 리소스** 또는 **App Service**를 선택한 후 마이그레이션된 Mobile Services의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-211">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="24d14-212">설정 블레이드가 기본적으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-212">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="24d14-213">게시 메뉴에서 **배포 자격 증명**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-213">Click **Deployment credentials** in the PUBLISHING menu.</span></span>
5. <span data-ttu-id="24d14-214">제공한 상자에 새 배포 자격 증명을 입력한 다음 저장 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-214">Enter the new deployment credentials in the boxes provided, then click the Save button.</span></span>

<span data-ttu-id="24d14-215">이러한 자격 증명을 사용하여 git를 통해 사이트를 복제하거나 GitHub, TFS 또는 Mercurial에서 자동화된 배포를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-215">You can use these credentials to clone the site with git or set up automated deployments from GitHub, TFS, or Mercurial.</span></span>  <span data-ttu-id="24d14-216">자세한 내용은 [Azure 앱 서비스 배포 설명서]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24d14-216">For more information, see the [Azure App Service deployment documentation].</span></span>

### <span data-ttu-id="24d14-217"><a name="appsettings"></a>응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="24d14-217"><a name="appsettings"></a>Application Settings</span></span>
<span data-ttu-id="24d14-218">마이그레이션된 모바일 서비스에 대한 설정은 대부분 앱 설정을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-218">Most settings for a migrated mobile service are available via App Settings.</span></span>  <span data-ttu-id="24d14-219">[Azure 포털]에서 앱 설정의 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-219">You can get a list of the app settings from the [Azure portal].</span></span>
<span data-ttu-id="24d14-220">앱 설정을 보거나 변경하려면:</span><span class="sxs-lookup"><span data-stu-id="24d14-220">To view or change your app settings:</span></span>

1. <span data-ttu-id="24d14-221">[Azure 포털]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-221">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="24d14-222">**모든 리소스** 또는 **App Service**를 선택한 후 마이그레이션된 Mobile Services의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-222">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="24d14-223">설정 블레이드가 기본적으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-223">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="24d14-224">일반 메뉴에서 **응용 프로그램 설정** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-224">Click **Application settings** in the GENERAL menu.</span></span>
5. <span data-ttu-id="24d14-225">앱 설정 섹션으로 스크롤하고 앱 설정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-225">Scroll to the App Settings section and find your app setting.</span></span>
6. <span data-ttu-id="24d14-226">앱 설정 값을 클릭하여 값을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-226">Click the value of the app setting to edit the value.</span></span>  <span data-ttu-id="24d14-227">**저장** 을 클릭하여 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-227">Click **Save** to save the value.</span></span>

<span data-ttu-id="24d14-228">동시에 여러 앱 설정을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-228">You can update multiple app settings at the same time.</span></span>

> [!TIP]
> <span data-ttu-id="24d14-229">동일한 값을 가진 두 응용 프로그램 설정이 있는지 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-229">There are two Application Settings with the same value.</span></span>  <span data-ttu-id="24d14-230">예를 들어 *ApplicationKey* 및 *MS\_ApplicationKey*를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-230">For example, you may see *ApplicationKey* and *MS\_ApplicationKey*.</span></span>  <span data-ttu-id="24d14-231">두 응용 프로그램 설정을 모두 동시에 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-231">Update both application settings at the same time.</span></span>
>
>

### <span data-ttu-id="24d14-232"><a name="authentication"></a>인증</span><span class="sxs-lookup"><span data-stu-id="24d14-232"><a name="authentication"></a>Authentication</span></span>
<span data-ttu-id="24d14-233">모든 인증 설정은 마이그레이션된 사이트에서 앱 설정으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-233">All authentication settings are available as App Settings in your migrated site.</span></span>  <span data-ttu-id="24d14-234">인증 설정을 업데이트하려면 적절한 앱 설정을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-234">To update your authentication settings, you must alter the appropriate app settings.</span></span>  <span data-ttu-id="24d14-235">다음 테이블에서는 인증 공급자에 대한 적절한 앱 설정을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-235">The following table shows the appropriate app settings for your authentication provider:</span></span>

| <span data-ttu-id="24d14-236">공급자</span><span class="sxs-lookup"><span data-stu-id="24d14-236">Provider</span></span> | <span data-ttu-id="24d14-237">클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="24d14-237">Client ID</span></span> | <span data-ttu-id="24d14-238">클라이언트 암호</span><span class="sxs-lookup"><span data-stu-id="24d14-238">Client Secret</span></span> | <span data-ttu-id="24d14-239">기타 설정</span><span class="sxs-lookup"><span data-stu-id="24d14-239">Other Settings</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="24d14-240">Microsoft 계정</span><span class="sxs-lookup"><span data-stu-id="24d14-240">Microsoft Account</span></span> |<span data-ttu-id="24d14-241">**MS\_MicrosoftClientID**</span><span class="sxs-lookup"><span data-stu-id="24d14-241">**MS\_MicrosoftClientID**</span></span> |<span data-ttu-id="24d14-242">**MS\_MicrosoftClientSecret**</span><span class="sxs-lookup"><span data-stu-id="24d14-242">**MS\_MicrosoftClientSecret**</span></span> |<span data-ttu-id="24d14-243">**MS\_MicrosoftPackageSID**</span><span class="sxs-lookup"><span data-stu-id="24d14-243">**MS\_MicrosoftPackageSID**</span></span> |
| <span data-ttu-id="24d14-244">Facebook</span><span class="sxs-lookup"><span data-stu-id="24d14-244">Facebook</span></span> |<span data-ttu-id="24d14-245">**MS\_FacebookAppID**</span><span class="sxs-lookup"><span data-stu-id="24d14-245">**MS\_FacebookAppID**</span></span> |<span data-ttu-id="24d14-246">**MS\_FacebookAppSecret**</span><span class="sxs-lookup"><span data-stu-id="24d14-246">**MS\_FacebookAppSecret**</span></span> | |
| <span data-ttu-id="24d14-247">Twitter</span><span class="sxs-lookup"><span data-stu-id="24d14-247">Twitter</span></span> |<span data-ttu-id="24d14-248">**MS\_TwitterConsumerKey**</span><span class="sxs-lookup"><span data-stu-id="24d14-248">**MS\_TwitterConsumerKey**</span></span> |<span data-ttu-id="24d14-249">**MS\_TwitterConsumerSecret**</span><span class="sxs-lookup"><span data-stu-id="24d14-249">**MS\_TwitterConsumerSecret**</span></span> | |
| <span data-ttu-id="24d14-250">Google</span><span class="sxs-lookup"><span data-stu-id="24d14-250">Google</span></span> |<span data-ttu-id="24d14-251">**MS\_GoogleClientID**</span><span class="sxs-lookup"><span data-stu-id="24d14-251">**MS\_GoogleClientID**</span></span> |<span data-ttu-id="24d14-252">**MS\_GoogleClientSecret**</span><span class="sxs-lookup"><span data-stu-id="24d14-252">**MS\_GoogleClientSecret**</span></span> | |
| <span data-ttu-id="24d14-253">Azure AD</span><span class="sxs-lookup"><span data-stu-id="24d14-253">Azure AD</span></span> |<span data-ttu-id="24d14-254">**MS\_AadClientID**</span><span class="sxs-lookup"><span data-stu-id="24d14-254">**MS\_AadClientID**</span></span> | |<span data-ttu-id="24d14-255">**MS\_AadTenants**</span><span class="sxs-lookup"><span data-stu-id="24d14-255">**MS\_AadTenants**</span></span> |

<span data-ttu-id="24d14-256">참고: **MS\_AadTenants**는 테넌트 도메인의 쉼표로 구분된 목록으로 저장됩니다(모바일 서비스 포털에서 "허용된 테넌트" 필드).</span><span class="sxs-lookup"><span data-stu-id="24d14-256">Note: **MS\_AadTenants** is stored as a comma-separated list of tenant domains (the "Allowed Tenants" fields in the Mobile Services portal).</span></span>

> [!WARNING]
> <span data-ttu-id="24d14-257">**설정 메뉴에 인증 메커니즘을 사용하지 마십시오**</span><span class="sxs-lookup"><span data-stu-id="24d14-257">**Do not use the authentication mechanisms in the Settings menu**</span></span>
>
> <span data-ttu-id="24d14-258">Azure App Service는 *인증/권한 부여* 설정 메뉴에서 별도의 "코드 없는" 인증 및 권한 부여 시스템 및 설정 메뉴에서 (사용되지 않는) *모바일 인증* 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-258">Azure App Service provides a separate "no-code" Authentication and Authorization system under the *Authentication / Authorization* Settings menu and the (deprecated) *Mobile Authentication* option under the Settings menu.</span></span>  <span data-ttu-id="24d14-259">이러한 옵션은 마이그레이션된 Azure 모바일 서비스와 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-259">These options are incompatible with a migrated Azure Mobile Service.</span></span>  <span data-ttu-id="24d14-260">[사이트를 업그레이드](app-service-mobile-net-upgrading-from-mobile-services.md) 하여 Azure 앱 서비스 인증을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-260">You can [upgrade your site](app-service-mobile-net-upgrading-from-mobile-services.md) to take advantage of the Azure App Service authentication.</span></span>
>
>

### <span data-ttu-id="24d14-261"><a name="easytables"></a>데이터</span><span class="sxs-lookup"><span data-stu-id="24d14-261"><a name="easytables"></a>Data</span></span>
<span data-ttu-id="24d14-262">모바일 서비스에서 *데이터* 탭은 Azure Portal 내에서 *쉬운 테이블*로 대체되었습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-262">The *Data* tab in Mobile Services has been replaced by *Easy Tables* within the Azure portal.</span></span>  <span data-ttu-id="24d14-263">쉬운 테이블에 액세스하려면:</span><span class="sxs-lookup"><span data-stu-id="24d14-263">To access Easy Tables:</span></span>

1. <span data-ttu-id="24d14-264">[Azure 포털]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-264">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="24d14-265">**모든 리소스** 또는 **App Service**를 선택한 후 마이그레이션된 Mobile Services의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-265">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="24d14-266">설정 블레이드가 기본적으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-266">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="24d14-267">모바일 메뉴에서 **쉬운 테이블**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-267">Click **Easy tables** in the MOBILE menu.</span></span>

<span data-ttu-id="24d14-268">**추가** 단추를 클릭하여 테이블을 추가하거나 테이블 이름을 클릭하여 기존 테이블에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-268">You can add a table by clicking the **Add** button or access your existing tables by clicking a table name.</span></span>  <span data-ttu-id="24d14-269">다음을 비롯하여 이 블레이드에서 할 수 있는 다양한 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-269">There are various operations you can do from this blade, including:</span></span>

* <span data-ttu-id="24d14-270">테이블 사용 권한 변경</span><span class="sxs-lookup"><span data-stu-id="24d14-270">Changing table permissions</span></span>
* <span data-ttu-id="24d14-271">작업 스크립트 편집</span><span class="sxs-lookup"><span data-stu-id="24d14-271">Editing the operational scripts</span></span>
* <span data-ttu-id="24d14-272">테이블 스키마 관리</span><span class="sxs-lookup"><span data-stu-id="24d14-272">Managing the table schema</span></span>
* <span data-ttu-id="24d14-273">테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="24d14-273">Deleting the table</span></span>
* <span data-ttu-id="24d14-274">테이블 내용 지우기</span><span class="sxs-lookup"><span data-stu-id="24d14-274">Clearing the table contents</span></span>
* <span data-ttu-id="24d14-275">테이블의 특정 행 삭제</span><span class="sxs-lookup"><span data-stu-id="24d14-275">Deleting specific rows of the table</span></span>

### <span data-ttu-id="24d14-276"><a name="easyapis"></a>API</span><span class="sxs-lookup"><span data-stu-id="24d14-276"><a name="easyapis"></a>API</span></span>
<span data-ttu-id="24d14-277">모바일 서비스에서 *API* 탭은 Azure Portal 내에서 *쉬운 API*로 대체되었습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-277">The *API* tab in Mobile Services has been replaced by *Easy APIs* within the Azure portal.</span></span>  <span data-ttu-id="24d14-278">쉬운 API에 액세스하려면:</span><span class="sxs-lookup"><span data-stu-id="24d14-278">To access Easy APIs:</span></span>

1. <span data-ttu-id="24d14-279">[Azure 포털]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-279">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="24d14-280">**모든 리소스** 또는 **App Service**를 선택한 후 마이그레이션된 Mobile Services의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-280">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="24d14-281">설정 블레이드가 기본적으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-281">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="24d14-282">모바일 메뉴에서 **쉬운 API**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-282">Click **Easy APIs** in the MOBILE menu.</span></span>

<span data-ttu-id="24d14-283">마이그레이션된 API는 블레이드에 이미 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-283">Your migrated APIs are already listed in the blade.</span></span>  <span data-ttu-id="24d14-284">또한 이 블레이드에서 API를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-284">You can also add an API from this blade.</span></span>  <span data-ttu-id="24d14-285">특정 API를 관리하려면 API를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-285">To manage a specific API, click the API.</span></span>
<span data-ttu-id="24d14-286">새 블레이드에서 사용 권한을 조정하고 API에 대한 스크립트를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-286">From the new blade, you can adjust the permissions and edit the scripts for the API.</span></span>

### <span data-ttu-id="24d14-287"><a name="on-demand-jobs"></a>스케줄러 작업</span><span class="sxs-lookup"><span data-stu-id="24d14-287"><a name="on-demand-jobs"></a>Scheduler Jobs</span></span>
<span data-ttu-id="24d14-288">모든 스케줄러 작업은 스케줄러 작업 컬렉션 섹션을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-288">All scheduler jobs are available through the Scheduler Job Collections section.</span></span>  <span data-ttu-id="24d14-289">스케줄러 작업에 액세스하려면</span><span class="sxs-lookup"><span data-stu-id="24d14-289">To access your scheduler jobs:</span></span>

1. <span data-ttu-id="24d14-290">[Azure 포털]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-290">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="24d14-291">**찾아보기>**를 선택하고 *필터* 상자에 **일정**을 입력한 다음 **스케줄러 컬렉션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-291">Select **Browse>**, enter **Schedule** in the *Filter* box, then select **Scheduler Collections**.</span></span>
3. <span data-ttu-id="24d14-292">사이트에 대한 작업 컬렉션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-292">Select the Job Collection for your site.</span></span>  <span data-ttu-id="24d14-293">*sitename*-Jobs로 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-293">It is named *sitename*-Jobs.</span></span>
4. <span data-ttu-id="24d14-294">**설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-294">Click **Settings**.</span></span>
5. <span data-ttu-id="24d14-295">관리 아래에 있는 **스케줄러 작업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-295">Click **Scheduler Jobs** under MANAGE.</span></span>

<span data-ttu-id="24d14-296">예약된 작업이 마이그레이션 전에 지정한 빈도와 함께 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-296">Scheduled jobs are listed with the frequency you specified before migration.</span></span>  <span data-ttu-id="24d14-297">주문형 작업은 사용할 수 없게 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-297">On-demand jobs are disabled.</span></span>  <span data-ttu-id="24d14-298">주문형 작업을 실행하려면</span><span class="sxs-lookup"><span data-stu-id="24d14-298">To run an on-demand job:</span></span>

1. <span data-ttu-id="24d14-299">실행하려는 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-299">Select the job you wish to run.</span></span>
2. <span data-ttu-id="24d14-300">필요한 경우 **사용**을 클릭하여 작업을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-300">If necessary, click **Enable** to enable the job.</span></span>
3. <span data-ttu-id="24d14-301">**설정**을 클릭한 다음 **일정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-301">Click **Settings**, then **Schedule**.</span></span>
4. <span data-ttu-id="24d14-302">**한 번** 되풀이를 선택한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-302">Select a Recurrence of **Once**, then Click **Save**</span></span>

<span data-ttu-id="24d14-303">요청 시 작업은 `App_Data/config/scripts/scheduler post-migration`에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-303">Your on-demand jobs are located in `App_Data/config/scripts/scheduler post-migration`.</span></span>  <span data-ttu-id="24d14-304">모든 요청 시 작업을 [WebJobs] 또는 [Functions]로 변환하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-304">We recommend that you convert all on-demand jobs to [WebJobs] or [Functions].</span></span>  <span data-ttu-id="24d14-305">[WebJobs] 또는 [Functions]로 새 스케줄러 작업을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-305">Write new scheduler jobs as [WebJobs] or [Functions].</span></span>

### <span data-ttu-id="24d14-306"><a name="notification-hubs"></a>알림 허브</span><span class="sxs-lookup"><span data-stu-id="24d14-306"><a name="notification-hubs"></a>Notification Hubs</span></span>
<span data-ttu-id="24d14-307">모바일 서비스는 푸시 알림에 알림 허브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-307">Mobile Services uses Notification Hubs for push notifications.</span></span>  <span data-ttu-id="24d14-308">마이그레이션 후에 알림 허브를 모바일 서비스에 연결하는 데 다음 앱 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-308">The following App Settings are used to link the Notification Hub to your Mobile Service after migration:</span></span>

| <span data-ttu-id="24d14-309">응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="24d14-309">Application Setting</span></span> | <span data-ttu-id="24d14-310">설명</span><span class="sxs-lookup"><span data-stu-id="24d14-310">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="24d14-311">**MS\_PushEntityNamespace**</span><span class="sxs-lookup"><span data-stu-id="24d14-311">**MS\_PushEntityNamespace**</span></span> |<span data-ttu-id="24d14-312">알림 허브 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="24d14-312">The Notification Hub Namespace</span></span> |
| <span data-ttu-id="24d14-313">**MS\_NotificationHubName**</span><span class="sxs-lookup"><span data-stu-id="24d14-313">**MS\_NotificationHubName**</span></span> |<span data-ttu-id="24d14-314">알림 허브 이름</span><span class="sxs-lookup"><span data-stu-id="24d14-314">The Notification Hub Name</span></span> |
| <span data-ttu-id="24d14-315">**MS\_NotificationHubConnectionString**</span><span class="sxs-lookup"><span data-stu-id="24d14-315">**MS\_NotificationHubConnectionString**</span></span> |<span data-ttu-id="24d14-316">알림 허브 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="24d14-316">The Notification Hub Connection String</span></span> |
| <span data-ttu-id="24d14-317">**MS\_NamespaceName**</span><span class="sxs-lookup"><span data-stu-id="24d14-317">**MS\_NamespaceName**</span></span> |<span data-ttu-id="24d14-318">MS_PushEntityNamespace에 대한 별칭</span><span class="sxs-lookup"><span data-stu-id="24d14-318">An alias for MS_PushEntityNamespace</span></span> |

<span data-ttu-id="24d14-319">Notification Hubs는 [Azure 포털]을 통해 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-319">Your Notification Hub is managed through the [Azure portal].</span></span>  <span data-ttu-id="24d14-320">알림 허브 이름을 적어둡니다.(앱 설정을 사용하여 찾을 수 있습니다)</span><span class="sxs-lookup"><span data-stu-id="24d14-320">Note the Notification Hub name (you can find this using the App Settings):</span></span>

1. <span data-ttu-id="24d14-321">[Azure 포털]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-321">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="24d14-322">**찾아보기**>를 선택한 다음 **Notification Hubs**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-322">Select **Browse**>, then select **Notification Hubs**</span></span>
3. <span data-ttu-id="24d14-323">모바일 서비스와 연결된 Notification Hubs 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-323">Click the Notification Hub name associated with the mobile service.</span></span>

> [!NOTE]
> <span data-ttu-id="24d14-324">Notification Hubs가 "혼합" 형식이면 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-324">If your Notification HUb is a "Mixed" type, it is not visible.</span></span>  <span data-ttu-id="24d14-325">"혼합" 형식 알림 허브는 알림 허브 및 레거시 서비스 버스 기능을 모두 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-325">"Mixed" type notification hubs utilize both Notification Hubs and legacy Service Bus features.</span></span>  <span data-ttu-id="24d14-326">계속하기 전에 [혼합 네임스페이스를 변환]합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-326">[Convert your Mixed namespaces] before continuing.</span></span>  <span data-ttu-id="24d14-327">변환이 완료되면 Notification Hubs가 [Azure 포털]에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-327">Once the conversion is complete, your notification hub appears in the [Azure portal].</span></span>
>
>

<span data-ttu-id="24d14-328">자세한 내용은 [알림 허브] 설명서를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-328">For more information, review the [Notification Hubs] documentation.</span></span>

> [!TIP]
> <span data-ttu-id="24d14-329">[Azure 포털]의 Notification Hubs 관리 기능은 아직 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-329">Notification Hubs management features in the [Azure portal] are still in preview.</span></span>  <span data-ttu-id="24d14-330">[Azure 클래식 포털] 은 모든 알림 허브를 관리하기 위해 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-330">The [Azure Classic Portal] remains available for managing all your Notification Hubs.</span></span>
>
>

### <span data-ttu-id="24d14-331"><a name="legacy-push"></a>레거시 푸시 설정</span><span class="sxs-lookup"><span data-stu-id="24d14-331"><a name="legacy-push"></a>Legacy Push Settings</span></span>
<span data-ttu-id="24d14-332">Notification Hubs에서 소개하기 전에 모바일 서비스에서 푸시를 구성한 경우 *레거시 푸시*가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-332">If you configured Push on your mobile service before the introduction on Notification Hubs, you are using *legacy push*.</span></span>  <span data-ttu-id="24d14-333">사용 중인 푸시 구성에 Notification Hubs가 표시되지 않으면 *레거시 푸시*가 사용되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-333">If you are using Push and you do not see a Notification Hub listed in your configuration, then it is likely you are using *legacy push*.</span></span>  <span data-ttu-id="24d14-334">이 기능은 다른 기능과 함께 마이그레이션됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-334">This feature is migrated with all the other features.</span></span>  <span data-ttu-id="24d14-335">그러나 마이그레이션이 완료된 직후 알림 허브로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-335">However, we recommend that you upgrade to Notification Hubs soon after the migration is complete.</span></span>

<span data-ttu-id="24d14-336">그 동안 모든 레거시 푸시 설정을 앱 설정에서 사용할 수 있습니다(단, APNS 인증서 예외).</span><span class="sxs-lookup"><span data-stu-id="24d14-336">In the interim, all the legacy push settings (with the notable exception of the APNS certificate) are available in App Settings.</span></span>  <span data-ttu-id="24d14-337">파일 시스템에서 적절한 파일을 대체하여 APNS 인증서를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-337">Update the APNS certificate by replacing the appropriate file on the filesystem.</span></span>

### <span data-ttu-id="24d14-338"><a name="app-settings"></a>기타 앱 설정</span><span class="sxs-lookup"><span data-stu-id="24d14-338"><a name="app-settings"></a>Other App Settings</span></span>
<span data-ttu-id="24d14-339">다음 추가 앱 설정은 모바일 서비스에서 마이그레이션되고 *설정* > *App 설정*에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-339">The following additional app settings are migrated from your Mobile Service and available under *Settings* > *App Settings*:</span></span>

| <span data-ttu-id="24d14-340">응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="24d14-340">Application Setting</span></span> | <span data-ttu-id="24d14-341">설명</span><span class="sxs-lookup"><span data-stu-id="24d14-341">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="24d14-342">**MS\_MobileServiceName**</span><span class="sxs-lookup"><span data-stu-id="24d14-342">**MS\_MobileServiceName**</span></span> |<span data-ttu-id="24d14-343">앱의 이름</span><span class="sxs-lookup"><span data-stu-id="24d14-343">The name of your app</span></span> |
| <span data-ttu-id="24d14-344">**MS\_MobileServiceDomainSuffix**</span><span class="sxs-lookup"><span data-stu-id="24d14-344">**MS\_MobileServiceDomainSuffix**</span></span> |<span data-ttu-id="24d14-345">도메인 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-345">The domain prefix.</span></span> <span data-ttu-id="24d14-346">예:</span><span class="sxs-lookup"><span data-stu-id="24d14-346">i.e</span></span> <span data-ttu-id="24d14-347">azure-mobile.net</span><span class="sxs-lookup"><span data-stu-id="24d14-347">azure-mobile.net</span></span> |
| <span data-ttu-id="24d14-348">**MS\_ApplicationKey**</span><span class="sxs-lookup"><span data-stu-id="24d14-348">**MS\_ApplicationKey**</span></span> |<span data-ttu-id="24d14-349">응용 프로그램 키</span><span class="sxs-lookup"><span data-stu-id="24d14-349">Your application key</span></span> |
| <span data-ttu-id="24d14-350">**MS\_MasterKey**</span><span class="sxs-lookup"><span data-stu-id="24d14-350">**MS\_MasterKey**</span></span> |<span data-ttu-id="24d14-351">앱 마스터 키</span><span class="sxs-lookup"><span data-stu-id="24d14-351">Your app master key</span></span> |

<span data-ttu-id="24d14-352">응용 프로그램 키 및 마스터 키는 원본 모바일 서비스에서 응용 프로그램 키와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-352">The application key and master key are identical to the Application Keys from your original Mobile Service.</span></span>  <span data-ttu-id="24d14-353">특히 응용 프로그램 키는 모바일 클라이언트에서 전송되어 모바일 API를 사용하는 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-353">In particular, the Application Key is sent by mobile clients to validate their use of the mobile API.</span></span>

### <span data-ttu-id="24d14-354"><a name="cliequivalents"></a>해당하는 명령줄</span><span class="sxs-lookup"><span data-stu-id="24d14-354"><a name="cliequivalents"></a>Command-Line Equivalents</span></span>
<span data-ttu-id="24d14-355">더 이상 *Azure 모바일* 명령을 활용하여 Azure 모바일 서비스 사이트를 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-355">You can longer use the *azure mobile* command to manage your Azure Mobile Services site.</span></span>  <span data-ttu-id="24d14-356">대신 많은 함수가 *Azure 사이트* 명령으로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-356">Instead, many functions have been replaced with the *azure site* command.</span></span>  <span data-ttu-id="24d14-357">다음 표를 사용하여 일반적인 명령에 대한 해당 항목을 찾으세요.</span><span class="sxs-lookup"><span data-stu-id="24d14-357">Use the following table to find equivalents for common commands:</span></span>

| <span data-ttu-id="24d14-358">*Azure 모바일* 명령</span><span class="sxs-lookup"><span data-stu-id="24d14-358">*Azure Mobile* Command</span></span> | <span data-ttu-id="24d14-359">해당하는 *Azure 사이트* 명령</span><span class="sxs-lookup"><span data-stu-id="24d14-359">Equivalent *Azure Site* command</span></span> |
|:--- |:--- |
| <span data-ttu-id="24d14-360">모바일 위치</span><span class="sxs-lookup"><span data-stu-id="24d14-360">mobile locations</span></span> |<span data-ttu-id="24d14-361">사이트 위치 목록</span><span class="sxs-lookup"><span data-stu-id="24d14-361">site location list</span></span> |
| <span data-ttu-id="24d14-362">모바일 목록</span><span class="sxs-lookup"><span data-stu-id="24d14-362">mobile list</span></span> |<span data-ttu-id="24d14-363">사이트 목록</span><span class="sxs-lookup"><span data-stu-id="24d14-363">site list</span></span> |
| <span data-ttu-id="24d14-364">mobile show *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-364">mobile show *name*</span></span> |<span data-ttu-id="24d14-365">site show *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-365">site show *name*</span></span> |
| <span data-ttu-id="24d14-366">mobile restart *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-366">mobile restart *name*</span></span> |<span data-ttu-id="24d14-367">site restart *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-367">site restart *name*</span></span> |
| <span data-ttu-id="24d14-368">mobile redeploy *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-368">mobile redeploy *name*</span></span> |<span data-ttu-id="24d14-369">site deployment redeploy *commitId* *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-369">site deployment redeploy *commitId* *name*</span></span> |
| <span data-ttu-id="24d14-370">mobile key set *name* *type* *value*</span><span class="sxs-lookup"><span data-stu-id="24d14-370">mobile key set *name* *type* *value*</span></span> |<span data-ttu-id="24d14-371">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-371">site appsetting delete *key* *name*</span></span> <br/> <span data-ttu-id="24d14-372">site appsetting add *key*=*value* *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-372">site appsetting add *key*=*value* *name*</span></span> |
| <span data-ttu-id="24d14-373">mobile config list *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-373">mobile config list *name*</span></span> |<span data-ttu-id="24d14-374">site appsetting list *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-374">site appsetting list *name*</span></span> |
| <span data-ttu-id="24d14-375">mobile config get *name* *key*</span><span class="sxs-lookup"><span data-stu-id="24d14-375">mobile config get *name* *key*</span></span> |<span data-ttu-id="24d14-376">site appsetting show *key* *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-376">site appsetting show *key* *name*</span></span> |
| <span data-ttu-id="24d14-377">mobile config set *name* *key*</span><span class="sxs-lookup"><span data-stu-id="24d14-377">mobile config set *name* *key*</span></span> |<span data-ttu-id="24d14-378">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-378">site appsetting delete *key* *name*</span></span> <br/> <span data-ttu-id="24d14-379">site appsetting add *key*=*value* *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-379">site appsetting add *key*=*value* *name*</span></span> |
| <span data-ttu-id="24d14-380">mobile domain list *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-380">mobile domain list *name*</span></span> |<span data-ttu-id="24d14-381">site domain list *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-381">site domain list *name*</span></span> |
| <span data-ttu-id="24d14-382">mobile domain add *name* *domain*</span><span class="sxs-lookup"><span data-stu-id="24d14-382">mobile domain add *name* *domain*</span></span> |<span data-ttu-id="24d14-383">site domain add *domain* *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-383">site domain add *domain* *name*</span></span> |
| <span data-ttu-id="24d14-384">mobile domain delete *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-384">mobile domain delete *name*</span></span> |<span data-ttu-id="24d14-385">site domain delete *domain* *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-385">site domain delete *domain* *name*</span></span> |
| <span data-ttu-id="24d14-386">mobile scale show *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-386">mobile scale show *name*</span></span> |<span data-ttu-id="24d14-387">site show *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-387">site show *name*</span></span> |
| <span data-ttu-id="24d14-388">mobile scale change *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-388">mobile scale change *name*</span></span> |<span data-ttu-id="24d14-389">site scale mode *mode* *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-389">site scale mode *mode* *name*</span></span> <br /> <span data-ttu-id="24d14-390">site scale instances *instances* *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-390">site scale instances *instances* *name*</span></span> |
| <span data-ttu-id="24d14-391">mobile appsetting list *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-391">mobile appsetting list *name*</span></span> |<span data-ttu-id="24d14-392">site appsetting list *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-392">site appsetting list *name*</span></span> |
| <span data-ttu-id="24d14-393">mobile appsetting add *name* *key* *value*</span><span class="sxs-lookup"><span data-stu-id="24d14-393">mobile appsetting add *name* *key* *value*</span></span> |<span data-ttu-id="24d14-394">site appsetting add *key*=*value* *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-394">site appsetting add *key*=*value* *name*</span></span> |
| <span data-ttu-id="24d14-395">mobile appsetting delete *name* *key*</span><span class="sxs-lookup"><span data-stu-id="24d14-395">mobile appsetting delete *name* *key*</span></span> |<span data-ttu-id="24d14-396">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-396">site appsetting delete *key* *name*</span></span> |
| <span data-ttu-id="24d14-397">mobile appsetting show *name* *key*</span><span class="sxs-lookup"><span data-stu-id="24d14-397">mobile appsetting show *name* *key*</span></span> |<span data-ttu-id="24d14-398">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="24d14-398">site appsetting delete *key* *name*</span></span> |

<span data-ttu-id="24d14-399">적절한 응용 프로그램 설정을 업데이트하여 인증 또는 푸시 알림 설정을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-399">Update authentication or push notification settings by updating the appropriate Application Setting.</span></span>
<span data-ttu-id="24d14-400">ftp 또는 git를 통해 파일을 편집하고 사이트를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-400">Edit files and publish your site via ftp or git.</span></span>

### <span data-ttu-id="24d14-401"><a name="diagnostics"></a>진단 및 로깅</span><span class="sxs-lookup"><span data-stu-id="24d14-401"><a name="diagnostics"></a>Diagnostics and Logging</span></span>
<span data-ttu-id="24d14-402">Azure 앱 서비스에서 정상적으로 진단 로깅을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-402">Diagnostic Logging is normally disabled in an Azure App Service.</span></span>  <span data-ttu-id="24d14-403">진단 로깅을 사용하려면:</span><span class="sxs-lookup"><span data-stu-id="24d14-403">To enable diagnostic logging:</span></span>

1. <span data-ttu-id="24d14-404">[Azure 포털]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-404">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="24d14-405">**모든 리소스** 또는 **App Service**를 선택한 후 마이그레이션된 Mobile Services의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-405">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="24d14-406">설정 블레이드가 기본적으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-406">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="24d14-407">기능 메뉴에서 **진단 로그** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-407">Select **Diagnostic Logs** under the FEATURES menu.</span></span>
5. <span data-ttu-id="24d14-408">다음 로그에서 **켜기**를 클릭합니다. **응용 프로그램 로깅(파일 시스템)**, **자세한 오류 메시지** 및 **실패한 요청 추적**</span><span class="sxs-lookup"><span data-stu-id="24d14-408">Click **ON** for the following logs: **Application Logging (Filesystem)**, **Detailed error messages**, and **Failed request tracing**</span></span>
6. <span data-ttu-id="24d14-409">웹 서버 로깅에서 **파일 시스템** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-409">Click **File System** for Web server logging</span></span>
7. <span data-ttu-id="24d14-410">페이지 맨 아래에 있는 **저장**</span><span class="sxs-lookup"><span data-stu-id="24d14-410">Click **Save**</span></span>

<span data-ttu-id="24d14-411">로그를 보려면:</span><span class="sxs-lookup"><span data-stu-id="24d14-411">To view the logs:</span></span>

1. <span data-ttu-id="24d14-412">[Azure 포털]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-412">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="24d14-413">**모든 리소스** 또는 **App Service**를 선택한 후 마이그레이션된 Mobile Services의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-413">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="24d14-414">**도구** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-414">Click the **Tools** button</span></span>
4. <span data-ttu-id="24d14-415">관찰 메뉴에서 **로그 스트림** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-415">Select **Log Stream** under the OBSERVE menu.</span></span>

<span data-ttu-id="24d14-416">로그는 생성되면 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-416">Logs are displayed in the window as they are generated.</span></span>  <span data-ttu-id="24d14-417">배포 자격 증명을 사용하여 나중에 분석에 대한 로그를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-417">You can also download the logs for later analysis using your deployment credentials.</span></span> <span data-ttu-id="24d14-418">자세한 내용은 [로깅] 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24d14-418">For more information, see the [Logging] documentation.</span></span>

## <span data-ttu-id="24d14-419"><a name="known-issues"></a>알려진 문제</span><span class="sxs-lookup"><span data-stu-id="24d14-419"><a name="known-issues"></a>Known Issues</span></span>
### <a name="deleting-a-migrated-mobile-app-clone-causes-a-site-outage"></a><span data-ttu-id="24d14-420">마이그레이션된 모바일 앱 복제를 삭제하면 사이트 중단이 발생함</span><span class="sxs-lookup"><span data-stu-id="24d14-420">Deleting a Migrated Mobile App Clone causes a site outage</span></span>
<span data-ttu-id="24d14-421">Azure PowerShell을 사용하여 마이그레이션된 모바일 서비스를 복제하고 복제본을 삭제하면 프로덕션 서비스에 대한 DNS 항목이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-421">If you clone your migrated mobile service using Azure PowerShell, then delete the clone, the DNS entry for your production service is removed.</span></span>  <span data-ttu-id="24d14-422">사이트는 인터넷에서 더 이상 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-422">Your site is no longer be accessible from the Internet.</span></span>  

<span data-ttu-id="24d14-423">해결 방법: 사이트를 복제하려는 경우 포털을 통해 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="24d14-423">Resolution: If you wish to clone your site, do so through the portal.</span></span>

### <a name="changing-webconfig-does-not-work"></a><span data-ttu-id="24d14-424">Web.config를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-424">Changing Web.config does not work</span></span>
<span data-ttu-id="24d14-425">ASP.NET 사이트가 있는 경우 `Web.config` 파일 변경 내용이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-425">If you have an ASP.NET site, changes to the `Web.config` file do not get applied.</span></span>  <span data-ttu-id="24d14-426">Azure 앱 서비스는 시작하는 동안 적절한 `Web.config` 파일을 빌드하여 모바일 서비스 런타임을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-426">The Azure App Service builds a suitable `Web.config` file during startup to support the Mobile Services runtime.</span></span>  <span data-ttu-id="24d14-427">XML 변환 파일을 사용하여 특정 설정(예: 사용자 지정 헤더)를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-427">You can override certain settings (such as custom headers) by using an XML transform file.</span></span>  <span data-ttu-id="24d14-428">호출된 `applicationHost.xdt`에 파일을 만듭니다. 이 파일은 Azure 서비스의 `D:\home\site` 디렉터리에서 종료되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-428">Create a file in called `applicationHost.xdt` - this file must end up in the `D:\home\site` directory on the Azure Service.</span></span>  <span data-ttu-id="24d14-429">사용자 지정 배포 스크립트를 통하거나 Kudu를 사용하여 `applicationHost.xdt` 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-429">Upload the `applicationHost.xdt` file via a custom deployment script or directly using Kudu.</span></span>  <span data-ttu-id="24d14-430">다음은 예제 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-430">The following shows an example document:</span></span>

```
<?xml version="1.0" encoding="utf-8"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <add name="X-Frame-Options" value="DENY" xdt:Transform="Replace" />
        <remove name="X-Powered-By" xdt:Transform="Insert" />
      </customHeaders>
    </httpProtocol>
    <security>
      <requestFiltering removeServerHeader="true" xdt:Transform="SetAttributes(removeServerHeader)" />
    </security>
  </system.webServer>
</configuration>
```

<span data-ttu-id="24d14-431">자세한 내용은 GitHub에 대한 [XDT 변환 샘플] 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24d14-431">For more information, see the [XDT Transform Samples] documentation on GitHub.</span></span>

### <a name="migrated-mobile-services-cannot-be-added-to-traffic-manager"></a><span data-ttu-id="24d14-432">마이그레이션된 모바일 서비스를 트래픽 관리자에 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-432">Migrated Mobile Services cannot be added to Traffic Manager</span></span>
<span data-ttu-id="24d14-433">Traffic Manager 프로필을 만들면 프로필에 마이그레이션된 모바일 서비스를 직접 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-433">When you create a Traffic Manager profile, you cannot directly choose a migrated mobile service to the profile.</span></span>  <span data-ttu-id="24d14-434">"외부 끝점"을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-434">Use an "external endpoint."</span></span>  <span data-ttu-id="24d14-435">PowerShell을 통해서만 외부 끝점을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-435">The external endpoint can only be added through PowerShell.</span></span>  <span data-ttu-id="24d14-436">자세한 내용은 [Traffic Manager 자습서](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-436">For more information, see the [Traffic Manager tutorial](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/).</span></span>

## <span data-ttu-id="24d14-437"><a name="next-steps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="24d14-437"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="24d14-438">응용 프로그램이 App Service에 마이그레이션하지 않지만 더 많은 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-438">Now that your application is migrated to App Service, there are even more features you can use:</span></span>

* <span data-ttu-id="24d14-439">[스테이징 슬롯] 을 배포하면 사이트에 대한 변경 내용을 준비하고 A/B 테스트를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-439">Deployment [staging slots] allow you to stage changes to your site and perform A/B testing.</span></span>
* <span data-ttu-id="24d14-440">[WebJobs] 은 요청 시 예약된 작업을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-440">[WebJobs] provide a replacement for On-demand scheduled jobs.</span></span>
* <span data-ttu-id="24d14-441">TFS, GitHub 또는 Mercurial에 사이트를 연결하여 사이트를 [지속적으로 배포] 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-441">You can [continuously deploy] your site by linking your site to GitHub, TFS, or Mercurial.</span></span>
* <span data-ttu-id="24d14-442">[Application Insights] 를 사용하여 사이트를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-442">You can use [Application Insights] to monitor your site.</span></span>
* <span data-ttu-id="24d14-443">동일한 코드에서 웹 사이트 및 모바일 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-443">Serve a website and a Mobile API from the same code.</span></span>

### <span data-ttu-id="24d14-444"><a name="upgrading-your-site"></a>Azure 모바일 앱 SDK에 모바일 서비스 사이트 업그레이드</span><span class="sxs-lookup"><span data-stu-id="24d14-444"><a name="upgrading-your-site"></a>Upgrading your Mobile Services site to Azure Mobile Apps SDK</span></span>
* <span data-ttu-id="24d14-445">Node.js 기반 서버 프로젝트의 경우 새로운 [Mobile App Node.js SDK]에서 다양한 새로운 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-445">For Node.js-based server projects, the new [Mobile Apps Node.js SDK] provides several new features.</span></span> <span data-ttu-id="24d14-446">예를 들어 이제 로컬 개발 및 디버깅을 수행하고 0.10 이후의 모든 Node.js 버전을 사용할 수 있으며 원하는 Express.js 미들웨어로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-446">For instance, you can now do local development and debugging, use any Node.js version above 0.10, and customize with any Express.js middleware.</span></span>
* <span data-ttu-id="24d14-447">.NET 기반 서버 프로젝트의 경우 새 [Mobile App SDK NuGet 패키지](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/)가 좀 더 유연한 NuGet 종속성을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-447">For .NET-based server projects, the new [Mobile Apps SDK NuGet packages](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) have more flexibility on NuGet dependencies.</span></span>  <span data-ttu-id="24d14-448">이러한 패키지는 새 App Service 인증을 지원하고 어떤 ASP.NET 프로젝트로도 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d14-448">These packages support the new App Service authentication, and compose with any ASP.NET project.</span></span> <span data-ttu-id="24d14-449">업그레이드에 대한 자세한 내용은 [기존 .NET 모바일 서비스를 앱 서비스로 업그레이드](app-service-mobile-net-upgrading-from-mobile-services.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24d14-449">To learn more about upgrading, see [Upgrade your existing .NET Mobile Service to App Service](app-service-mobile-net-upgrading-from-mobile-services.md).</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-migrating-from-mobile-services/migrate-to-app-service-button.PNG
[1]: ./media/app-service-mobile-migrating-from-mobile-services/migration-activity-monitor.png
[2]: ./media/app-service-mobile-migrating-from-mobile-services/triggering-job-with-postman.png

<!-- Links -->
<span data-ttu-id="24d14-450">[앱 서비스 가격]: https://azure.microsoft.com/en-us/pricing/details/app-service/</span><span class="sxs-lookup"><span data-stu-id="24d14-450">[App Service pricing]: https://azure.microsoft.com/en-us/pricing/details/app-service/</span></span>
<span data-ttu-id="24d14-451">[Application Insights]: ../application-insights/app-insights-overview.md</span><span class="sxs-lookup"><span data-stu-id="24d14-451">[Application Insights]: ../application-insights/app-insights-overview.md</span></span>
<span data-ttu-id="24d14-452">[자동 크기 조정]: ../app-service-web/web-sites-scale.md</span><span class="sxs-lookup"><span data-stu-id="24d14-452">[Auto-scale]: ../app-service-web/web-sites-scale.md</span></span>
<span data-ttu-id="24d14-453">[Azure App Service]: ../app-service/app-service-value-prop-what-is.md</span><span class="sxs-lookup"><span data-stu-id="24d14-453">[Azure App Service]: ../app-service/app-service-value-prop-what-is.md</span></span>
<span data-ttu-id="24d14-454">[Azure 앱 서비스 배포 설명서]: ../app-service-web/web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="24d14-454">[Azure App Service deployment documentation]: ../app-service-web/web-sites-deploy.md</span></span>
<span data-ttu-id="24d14-455">[Azure 클래식 포털]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="24d14-455">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
<span data-ttu-id="24d14-456">[Azure 포털]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="24d14-456">[Azure portal]: https://portal.azure.com</span></span>
[Azure Region]: https://azure.microsoft.com/en-us/regions/
<span data-ttu-id="24d14-457">[Azure 스케줄러 계획]: ../scheduler/scheduler-plans-billing.md</span><span class="sxs-lookup"><span data-stu-id="24d14-457">[Azure Scheduler Plans]: ../scheduler/scheduler-plans-billing.md</span></span>
<span data-ttu-id="24d14-458">[지속적으로 배포]: ../app-service-web/app-service-continuous-deployment.md</span><span class="sxs-lookup"><span data-stu-id="24d14-458">[continuously deploy]: ../app-service-web/app-service-continuous-deployment.md</span></span>
<span data-ttu-id="24d14-459">[혼합 네임스페이스를 변환]: https://azure.microsoft.com/en-us/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/</span><span class="sxs-lookup"><span data-stu-id="24d14-459">[Convert your Mixed namespaces]: https://azure.microsoft.com/en-us/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/</span></span>
[curl]: http://curl.haxx.se/
<span data-ttu-id="24d14-460">[사용자 지정 도메인 이름]: ../app-service-web/web-sites-custom-domain-name.md</span><span class="sxs-lookup"><span data-stu-id="24d14-460">[custom domain names]: ../app-service-web/web-sites-custom-domain-name.md</span></span>
[Fiddler]: http://www.telerik.com/fiddler
<span data-ttu-id="24d14-461">[Azure 앱 서비스의 일반적인 가용성]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/</span><span class="sxs-lookup"><span data-stu-id="24d14-461">[general availability of Azure App Service]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/</span></span>
<span data-ttu-id="24d14-462">[하이브리드 연결]: ../app-service-web/web-sites-hybrid-connection-get-started.md</span><span class="sxs-lookup"><span data-stu-id="24d14-462">[Hybrid Connections]: ../app-service-web/web-sites-hybrid-connection-get-started.md</span></span>
<span data-ttu-id="24d14-463">[로깅]: ../app-service-web/web-sites-enable-diagnostic-log.md</span><span class="sxs-lookup"><span data-stu-id="24d14-463">[Logging]: ../app-service-web/web-sites-enable-diagnostic-log.md</span></span>
<span data-ttu-id="24d14-464">[Mobile App Node.js SDK]: https://github.com/azure/azure-mobile-apps-node</span><span class="sxs-lookup"><span data-stu-id="24d14-464">[Mobile Apps Node.js SDK]: https://github.com/azure/azure-mobile-apps-node</span></span>
<span data-ttu-id="24d14-465">[모바일 서비스 vs. App Service]: app-service-mobile-value-prop-migration-from-mobile-services.md</span><span class="sxs-lookup"><span data-stu-id="24d14-465">[Mobile Services vs. App Service]: app-service-mobile-value-prop-migration-from-mobile-services.md</span></span>
<span data-ttu-id="24d14-466">[알림 허브]: ../notification-hubs/notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="24d14-466">[Notification Hubs]: ../notification-hubs/notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="24d14-467">[성능 모니터링]: ../app-service-web/web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="24d14-467">[performance monitoring]: ../app-service-web/web-sites-monitor.md</span></span>
[Postman]: http://www.getpostman.com/
<span data-ttu-id="24d14-468">[스테이징 슬롯]: ../app-service-web/web-sites-staged-publishing.md</span><span class="sxs-lookup"><span data-stu-id="24d14-468">[staging slots]: ../app-service-web/web-sites-staged-publishing.md</span></span>
<span data-ttu-id="24d14-469">[VNet]: ../app-service-web/web-sites-integrate-with-vnet.md</span><span class="sxs-lookup"><span data-stu-id="24d14-469">[VNet]: ../app-service-web/web-sites-integrate-with-vnet.md</span></span>
<span data-ttu-id="24d14-470">[WebJobs]: ../app-service-web/websites-webjobs-resources.md</span><span class="sxs-lookup"><span data-stu-id="24d14-470">[WebJobs]: ../app-service-web/websites-webjobs-resources.md</span></span>
<span data-ttu-id="24d14-471">[XDT 변환 샘플]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples</span><span class="sxs-lookup"><span data-stu-id="24d14-471">[XDT Transform Samples]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples</span></span>
<span data-ttu-id="24d14-472">[Functions]: ../azure-functions/functions-overview.md</span><span class="sxs-lookup"><span data-stu-id="24d14-472">[Functions]: ../azure-functions/functions-overview.md</span></span>
