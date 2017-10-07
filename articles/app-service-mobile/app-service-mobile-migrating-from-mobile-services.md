---
title: "모바일 서비스 tooan 앱 서비스 모바일 앱에서 aaaMigrate"
description: "Tooeasily 모바일 서비스 응용 프로그램 tooan 앱 서비스 모바일 앱을 마이그레이션 방법에 대해 알아봅니다"
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
ms.openlocfilehash: cd2e8d98595703389300b79da9bf51cdcefe7b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="369c6-103"><a name="article-top"></a>마이그레이션에 기존 Azure 모바일 서비스 tooAzure 앱 서비스</span><span class="sxs-lookup"><span data-stu-id="369c6-103"><a name="article-top"></a>Migrate your existing Azure Mobile Service tooAzure App Service</span></span>
<span data-ttu-id="369c6-104">Hello로 [Azure 앱 서비스의 일반적인 가용성], Azure 모바일 서비스 사이트를 쉽게 수 마이그레이션된 내부 tootake hello Azure 앱 서비스의 모든 기능을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-104">With hello [general availability of Azure App Service], Azure Mobile Services sites can be easily migrated in-place tootake advantage of all the features of hello Azure App Service.</span></span>  <span data-ttu-id="369c6-105">이 문서에서는 Azure Mobile Services tooAzure 앱 서비스에서에서 사이트를 마이그레이션하는 경우 어떤 tooexpect를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-105">This document explains what tooexpect when migrating your site from Azure Mobile Services tooAzure App Service.</span></span>

## <span data-ttu-id="369c6-106"><a name="what-does-migration-do"></a>마이그레이션을 수행 하는 tooyour 사이트</span><span class="sxs-lookup"><span data-stu-id="369c6-106"><a name="what-does-migration-do"></a>What does migration do tooyour site</span></span>
<span data-ttu-id="369c6-107">Azure 모바일 서비스의 마이그레이션 설정에 모바일 서비스는 [Azure 앱 서비스] hello 코드에 영향을 주지 않고 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-107">Migration of your Azure Mobile Service turns your Mobile Service into an [Azure App Service] app without affecting hello code.</span></span>  <span data-ttu-id="369c6-108">Notification Hubs, SQL 데이터 연결, 인증 설정, 예약된 작업 및 도메인 이름은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-108">Your Notification Hubs, SQL data connection, authentication settings, scheduled jobs, and domain name remain unchanged.</span></span>  <span data-ttu-id="369c6-109">Azure 모바일 서비스를 사용 하 여 모바일 클라이언트 toooperate를 정상적으로 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-109">Mobile clients using your Azure Mobile Service continue toooperate normally.</span></span>  <span data-ttu-id="369c6-110">마이그레이션 전송된 tooAzure 앱 서비스 되 면 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-110">Migration restarts your service once it is transferred tooAzure App Service.</span></span>

[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

## <span data-ttu-id="369c6-111"><a name="why-migrate"></a>사이트를 마이그레이션해야 하는 이유</span><span class="sxs-lookup"><span data-stu-id="369c6-111"><a name="why-migrate"></a>Why you should migrate your site</span></span>
<span data-ttu-id="369c6-112">Microsoft는 포함 하 여 Azure 앱 서비스의 hello 기능에 Azure 모바일 서비스 tootake 활용 마이그레이션하는 권장:</span><span class="sxs-lookup"><span data-stu-id="369c6-112">Microsoft is recommending that you migrate your Azure Mobile Service tootake advantage of hello features of Azure App Service, including:</span></span>

* <span data-ttu-id="369c6-113">[WebJobs] 및 [사용자 지정 도메인 이름]을 포함하는 새로운 호스트 기능.</span><span class="sxs-lookup"><span data-stu-id="369c6-113">New host features, including [WebJobs] and [custom domain names].</span></span>
* <span data-ttu-id="369c6-114">연결 tooyour 온-프레미스 리소스를 사용 하 여 [VNet] 또한 너무[하이브리드 연결]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-114">Connectivity tooyour on-premises resources using [VNet] in addition too[Hybrid Connections].</span></span>
* <span data-ttu-id="369c6-115">New Relic 또는 [Application Insights]를 통한 모니터링 및 문제 해결.</span><span class="sxs-lookup"><span data-stu-id="369c6-115">Monitoring and troubleshooting with New Relic or [Application Insights].</span></span>
* <span data-ttu-id="369c6-116">[스테이징 슬롯], 롤백 및 프로덕션 내 테스트를 포함하는 기본 제공 DevOps 도구.</span><span class="sxs-lookup"><span data-stu-id="369c6-116">Built-in DevOps tooling, including [staging slots], roll-back, and in-production testing.</span></span>
* <span data-ttu-id="369c6-117">[자동 크기 조정], 부하 분산 및 [성능 모니터링].</span><span class="sxs-lookup"><span data-stu-id="369c6-117">[Auto-scale], load balancing, and [performance monitoring].</span></span>

<span data-ttu-id="369c6-118">Azure 앱 서비스의 hello 이점에 자세한 내용은 참조 hello [모바일 서비스 vs. App Service] 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="369c6-118">For more information on hello benefits of Azure App Service, see hello [Mobile Services vs. App Service] topic.</span></span>

## <span data-ttu-id="369c6-119"><a name="before-you-begin"></a>시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="369c6-119"><a name="before-you-begin"></a>Before you begin</span></span>
<span data-ttu-id="369c6-120">사이트에서 주요 작업을 시작하기 전에 모바일 서비스 스크립트와 SQL Database를 백업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-120">Before beginning any major work on your site, you should back up your Mobile Service scripts and SQL database.</span></span>

## <span data-ttu-id="369c6-121"><a name="migrating-site"></a>사이트 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="369c6-121"><a name="migrating-site"></a>Migrating your sites</span></span>
<span data-ttu-id="369c6-122">hello 마이그레이션 프로세스는 단일 Azure 지역에 있는 모든 사이트를 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-122">hello migration process migrates all sites within a single Azure Region.</span></span>

<span data-ttu-id="369c6-123">toomigrate 사이트:</span><span class="sxs-lookup"><span data-stu-id="369c6-123">toomigrate your site:</span></span>

1. <span data-ttu-id="369c6-124">Toohello 로그인 [Azure 클래식 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-124">Log in toohello [Azure Classic Portal].</span></span>
2. <span data-ttu-id="369c6-125">모바일 서비스를 선택 하 시겠습니까 toomigrate hello 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-125">Select a Mobile Service in hello region you wish toomigrate.</span></span>
3. <span data-ttu-id="369c6-126">Hello 클릭 **tooApp 서비스 마이그레이션** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-126">Click hello **Migrate tooApp Service** button.</span></span>

   ![hello 마이그레이션 단추][0]
4. <span data-ttu-id="369c6-128">Hello 마이그레이션 tooApp 서비스 대화 상자를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-128">Read hello Migrate tooApp Service dialog.</span></span>
5. <span data-ttu-id="369c6-129">제공 된 hello 상자에 모바일 서비스의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-129">Enter hello name of your Mobile Service in hello box provided.</span></span>  <span data-ttu-id="369c6-130">예를 들어 도메인 이름이 contoso.azure mobile.net 이면 다음를 입력 *contoso* hello 상자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-130">For example, if your domain name is contoso.azure-mobile.net, then enter *contoso* in hello box provided.</span></span>
6. <span data-ttu-id="369c6-131">Hello 눈금 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-131">Click hello tick button.</span></span>

<span data-ttu-id="369c6-132">Hello hello 작업 모니터에서 hello 마이그레이션 상태를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-132">Monitor hello status of hello migration in hello activity monitor.</span></span> <span data-ttu-id="369c6-133">사이트가로 나열 되어 *마이그레이션* hello Azure 클래식 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="369c6-133">Your site is listed as *migrating* in hello Azure Classic Portal.</span></span>

  ![마이그레이션 작업 모니터링][1]

<span data-ttu-id="369c6-135">각 마이그레이션에서 마이그레이션 중인 모바일 서비스 당 3 too15 분 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-135">Each migration can take anywhere from 3 too15 minutes per mobile service being migrated.</span></span>  <span data-ttu-id="369c6-136">Hello 마이그레이션하는 동안 사이트에 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-136">Your site remains available during hello migration.</span></span>
<span data-ttu-id="369c6-137">사이트는 hello hello 마이그레이션 프로세스가 끝날 때 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-137">Your site is restarted at hello end of hello migration process.</span></span>  <span data-ttu-id="369c6-138">몇 초 정도 지속 되는 hello 다시 시작 프로세스 중에 hello 사이트를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-138">hello site is unavailable during hello restart process, which may last a couple of seconds.</span></span>

## <span data-ttu-id="369c6-139"><a name="finalizing-migration"></a>Hello 마이그레이션을 완료 하는 중</span><span class="sxs-lookup"><span data-stu-id="369c6-139"><a name="finalizing-migration"></a>Finalizing hello Migration</span></span>
<span data-ttu-id="369c6-140">Tootest hello 마이그레이션 프로세스의 hello 결론에 모바일 클라이언트에서 사이트를 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-140">Plan tootest your site from a mobile client at hello conclusion of hello migration process.</span></span>  <span data-ttu-id="369c6-141">Toohello 모바일 클라이언트 변경 하지 않고 모든 일반적인 클라이언트 작업을 수행할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-141">Ensure you can perform all common client actions without changes toohello mobile client.</span></span>  

### <span data-ttu-id="369c6-142"><a name="update-app-service-tier"></a>적절한 앱 서비스 가격 책정 계층 선택</span><span class="sxs-lookup"><span data-stu-id="369c6-142"><a name="update-app-service-tier"></a>Select an appropriate App Service pricing tier</span></span>
<span data-ttu-id="369c6-143">가격 tooAzure 앱 서비스를 마이그레이션한 후에 더 많은 유연성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-143">You have more flexibility in pricing after you migrate tooAzure App Service.</span></span>

1. <span data-ttu-id="369c6-144">Toohello 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-144">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="369c6-145">선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-145">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="369c6-146">기본적으로 hello 설정 블레이드에서가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-146">hello Settings blade opens by default.</span></span>
4. <span data-ttu-id="369c6-147">클릭 **앱 서비스 계획** hello 설정 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-147">Click **App Service Plan** in hello Settings menu.</span></span>
5. <span data-ttu-id="369c6-148">Hello 클릭 **가격 책정 계층** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-148">Click hello **Pricing Tier** tile.</span></span>
6. <span data-ttu-id="369c6-149">Hello 타일 적절 한 tooyour 요구 사항를 클릭 한 다음 클릭 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-149">Click hello tile appropriate tooyour requirements, then Click **Select**.</span></span>  <span data-ttu-id="369c6-150">TooClick 할 수 있습니다 **모든 보기** toosee hello 가격 책정 계층을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-150">You may need tooClick **View all** toosee hello available pricing tiers.</span></span>

<span data-ttu-id="369c6-151">시작 지점으로 계층을 따라 hello를 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-151">As a starting point, we recommend hello following tiers:</span></span>

| <span data-ttu-id="369c6-152">모바일 서비스 가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="369c6-152">Mobile Service Pricing Tier</span></span> | <span data-ttu-id="369c6-153">앱 서비스 가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="369c6-153">App Service Pricing Tier</span></span> |
|:--- |:--- |
| <span data-ttu-id="369c6-154">무료</span><span class="sxs-lookup"><span data-stu-id="369c6-154">Free</span></span> |<span data-ttu-id="369c6-155">F1 무료</span><span class="sxs-lookup"><span data-stu-id="369c6-155">F1 Free</span></span> |
| <span data-ttu-id="369c6-156">Basic</span><span class="sxs-lookup"><span data-stu-id="369c6-156">Basic</span></span> |<span data-ttu-id="369c6-157">B1 기본</span><span class="sxs-lookup"><span data-stu-id="369c6-157">B1 Basic</span></span> |
| <span data-ttu-id="369c6-158">표준</span><span class="sxs-lookup"><span data-stu-id="369c6-158">Standard</span></span> |<span data-ttu-id="369c6-159">S1 표준</span><span class="sxs-lookup"><span data-stu-id="369c6-159">S1 Standard</span></span> |

<span data-ttu-id="369c6-160">Hello 오른쪽 가격대 키를 눌러 응용 프로그램에 대 한 중요 한 선택 유연성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-160">There is considerable flexibility in choosing hello right pricing tier for your application.</span></span>  <span data-ttu-id="369c6-161">너무 참조[앱 서비스 가격 책정] hello 새 앱 서비스 가격 정보.</span><span class="sxs-lookup"><span data-stu-id="369c6-161">Refer too[App Service Pricing] for full details on hello pricing of your new App Service.</span></span>

> [!TIP]
> <span data-ttu-id="369c6-162">hello 표준으로 서비스 응용 프로그램 계층 기능이 포함 되어 액세스 toomany toouse, 경우가 포함 하 여 [스테이징 슬롯], 자동 백업 되 고, 자동 크기 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-162">hello App Service Standard tier contains access toomany features that you may want toouse, including [staging slots], automatic backups, and auto-scaling.</span></span>  <span data-ttu-id="369c6-163">발생 된 hello 새로운 기능을 확인해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="369c6-163">Check out hello new capabilities while you are there!</span></span>
>
>

### <span data-ttu-id="369c6-164"><a name="review-migration-scheduler-jobs"></a>Hello 마이그레이션된 스케줄러 작업을 검토</span><span class="sxs-lookup"><span data-stu-id="369c6-164"><a name="review-migration-scheduler-jobs"></a>Review hello Migrated Scheduler Jobs</span></span>
<span data-ttu-id="369c6-165">스케줄러 작업은 마이그레이션 후에 약 30분까지 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-165">Scheduler Jobs will not be visible until approximately 30 minutes after migration.</span></span>  <span data-ttu-id="369c6-166">Toorun hello 백그라운드에서 계속 하는 예약 된 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-166">Scheduled jobs continue toorun in hello background.</span></span>
<span data-ttu-id="369c6-167">tooview 다시 표시 되 후 예약 된 작업:</span><span class="sxs-lookup"><span data-stu-id="369c6-167">tooview your scheduled jobs after they are visible again:</span></span>

1. <span data-ttu-id="369c6-168">Toohello 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-168">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="369c6-169">선택 **찾아보기 >**, 입력 **일정** hello에 *필터* 상자를 선택한 다음 선택 **스케줄러 컬렉션**합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-169">Select **Browse>**, enter **Schedule** in hello *Filter* box, then select **Scheduler Collections**.</span></span>

<span data-ttu-id="369c6-170">마이그레이션 후에 사용 가능한 무료 스케줄러 작업의 수가 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-170">There are a limited number of free scheduler jobs available post-migration.</span></span>  <span data-ttu-id="369c6-171">사용 및 hello 검토 [Azure 스케줄러 계획]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-171">Review your usage and hello [Azure Scheduler Plans].</span></span>

### <span data-ttu-id="369c6-172"><a name="configure-cors"></a>필요한 경우 CORS 구성</span><span class="sxs-lookup"><span data-stu-id="369c6-172"><a name="configure-cors"></a>Configure CORS if needed</span></span>
<span data-ttu-id="369c6-173">크로스-원본 자원 공유 기법 tooallow 웹 사이트 tooaccess 다른 도메인의 웹 API입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-173">Cross-origin resource sharing is a technique tooallow a website tooaccess a Web API on a different domain.</span></span>  <span data-ttu-id="369c6-174">연결 된 웹 사이트와 Azure 모바일 서비스를 사용 하는 hello 마이그레이션의 일부로 CORS tooconfigure를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-174">If you are using Azure Mobile Services with an associated website, then you need tooconfigure CORS as part of hello migration.</span></span>  <span data-ttu-id="369c6-175">모바일 장치에서 단독으로 Azure 모바일 서비스를 액세스 하면 다음 CORS 드문 경우에서를 제외 하 고 구성 toobe를 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-175">If you are accessing Azure Mobile Services exclusively from mobile devices, then CORS does not need toobe configured except in rare cases.</span></span>

<span data-ttu-id="369c6-176">마이그레이션된 CORS 설정에는 hello로 사용할 수 **MS_CrossDomainWhitelist** 앱 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-176">Your migrated CORS settings are available as hello **MS_CrossDomainWhitelist** App Setting.</span></span>  <span data-ttu-id="369c6-177">toomigrate 프로그램 사이트 toohello 앱 서비스의 CORS 기능:</span><span class="sxs-lookup"><span data-stu-id="369c6-177">toomigrate your site toohello App Service CORS facility:</span></span>

1. <span data-ttu-id="369c6-178">Toohello 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-178">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="369c6-179">선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-179">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="369c6-180">기본적으로 hello 설정 블레이드에서가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-180">hello Settings blade opens by default.</span></span>
4. <span data-ttu-id="369c6-181">클릭 **CORS** hello API 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-181">Click **CORS** in hello API menu.</span></span>
5. <span data-ttu-id="369c6-182">한 다음 Enter 키를 제공 된 hello 상자에 허용 된 원본을 입력 하십시오.</span><span class="sxs-lookup"><span data-stu-id="369c6-182">Enter any Allowed Origins in hello box provided, pressing Enter after each one.</span></span>
6. <span data-ttu-id="369c6-183">Origin 허용 목록이 잘못 되 면 hello 저장 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-183">Once your list of Allowed Origins is correct, click hello Save button.</span></span>

> [!TIP]
> <span data-ttu-id="369c6-184">Hello에 웹 사이트와 모바일 서비스를 실행할 수는 Azure 응용 프로그램 서비스를 사용 하 여 hello 이점 중 하나는 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-184">One of hello advantages of using an Azure App Service is that you can run your web site and mobile service on hello same site.</span></span>  <span data-ttu-id="369c6-185">자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="369c6-185">For more information, see hello [next steps](#next-steps) section.</span></span>
>
>

### <span data-ttu-id="369c6-186"><a name="download-publish-profile"></a>새 게시 프로필 다운로드</span><span class="sxs-lookup"><span data-stu-id="369c6-186"><a name="download-publish-profile"></a>Download a new Publishing Profile</span></span>
<span data-ttu-id="369c6-187">사이트의 게시 프로필 hello tooAzure 앱 서비스를 마이그레이션할 때 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-187">hello publishing profile of your site is changed when migrating tooAzure App Service.</span></span>  <span data-ttu-id="369c6-188">Visual Studio에서 사이트를 toopublish을 가져오려는 경우 새 게시 프로필을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-188">If you intend toopublish your site from within Visual Studio, you need a new publishing profile.</span></span>  <span data-ttu-id="369c6-189">toodownload hello 새 게시 프로필:</span><span class="sxs-lookup"><span data-stu-id="369c6-189">toodownload hello new publishing profile:</span></span>

1. <span data-ttu-id="369c6-190">Toohello 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-190">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="369c6-191">선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-191">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="369c6-192">**게시 프로필 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-192">Click **Get publish profile**.</span></span>

<span data-ttu-id="369c6-193">hello PublishSettings 파일은 다운로드 한 tooyour 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-193">hello PublishSettings file is downloaded tooyour computer.</span></span>  <span data-ttu-id="369c6-194">일반적으로 파일 이름은 *sitename*.PublishSettings입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-194">It is normally called *sitename*.PublishSettings.</span></span>  <span data-ttu-id="369c6-195">가져오기 hello 게시 하 여 기존 프로젝트에는 설정:</span><span class="sxs-lookup"><span data-stu-id="369c6-195">Import hello publish settings into your existing project:</span></span>

1. <span data-ttu-id="369c6-196">Visual Studio 및 Azure 모바일 서비스 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-196">Open Visual Studio and your Azure Mobile Service project.</span></span>
2. <span data-ttu-id="369c6-197">Hello에서 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택 **게시...**</span><span class="sxs-lookup"><span data-stu-id="369c6-197">Right-Click your project in hello **Solution Explorer** and select **Publish...**</span></span>
3. <span data-ttu-id="369c6-198">**가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-198">Click **Import**</span></span>
4. <span data-ttu-id="369c6-199">**찾아보기**를 클릭하고 다운로드한 게시 설정 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-199">Click **Browse** and select your downloaded publish settings file.</span></span>  <span data-ttu-id="369c6-200">**확인**</span><span class="sxs-lookup"><span data-stu-id="369c6-200">Click **OK**</span></span>
5. <span data-ttu-id="369c6-201">클릭 **연결 유효성 검사** tooensure hello 설정 작업을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-201">Click **Validate Connection** tooensure hello publish settings work.</span></span>
6. <span data-ttu-id="369c6-202">클릭 **게시** toopublish 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-202">Click **Publish** toopublish your site.</span></span>

## <span data-ttu-id="369c6-203"><a name="working-with-your-site"></a>마이그레이션 후에 사이트로 작업</span><span class="sxs-lookup"><span data-stu-id="369c6-203"><a name="working-with-your-site"></a>Working with your site post-migration</span></span>
<span data-ttu-id="369c6-204">Hello에 새 앱 서비스에서 작업 시작 [Azure 포털] 마이그레이션 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-204">Start working with your new App Service in hello [Azure portal] post-migration.</span></span>  <span data-ttu-id="369c6-205">hello는 다음과 같은 hello에 tooperform를 사용 하는 특정 작업에 대 한 몇 가지 메모 [Azure 클래식 포털]앱 서비스 동등한 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-205">hello following are some notes on specific operations that you used tooperform in hello [Azure Classic Portal], together with their App Service equivalent.</span></span>

### <span data-ttu-id="369c6-206"><a name="publishing-your-site"></a>마이그레이션된 사이트 다운로드 및 게시</span><span class="sxs-lookup"><span data-stu-id="369c6-206"><a name="publishing-your-site"></a>Downloading and Publishing your migrated site</span></span>
<span data-ttu-id="369c6-207">사이트는 git 또는 ftp를 통해 사용될 수 있고 WebDeploy, TFS, Mercurial, GitHub, FTP 등 다양한 메커니즘을 사용하여 다시 게시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-207">Your site is available via git or ftp and can be republished with various different mechanisms, including WebDeploy, TFS, Mercurial, GitHub, and FTP.</span></span>  <span data-ttu-id="369c6-208">배포 자격 증명 hello hello 나머지 사이트도 마이그레이션됩니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-208">hello deployment credentials are migrated with hello rest of your site.</span></span>  <span data-ttu-id="369c6-209">배포 자격 증명을 설정하지 않거나 기억하지 못하는 경우 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-209">If you did not set your deployment credentials or you do not remember them, you can reset them:</span></span>

1. <span data-ttu-id="369c6-210">Toohello 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-210">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="369c6-211">선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-211">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="369c6-212">기본적으로 hello 설정 블레이드에서가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-212">hello Settings blade opens by default.</span></span>
4. <span data-ttu-id="369c6-213">클릭 **배포 자격 증명** hello 게시 메뉴에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-213">Click **Deployment credentials** in hello PUBLISHING menu.</span></span>
5. <span data-ttu-id="369c6-214">Hello 새 배포 자격 증명도 제공 하는 hello 상자에 입력 한 다음 hello 저장 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-214">Enter hello new deployment credentials in hello boxes provided, then click hello Save button.</span></span>

<span data-ttu-id="369c6-215">Git와 함께 이러한 자격 증명 tooclone hello 사이트를 사용 하거나 GitHub, TFS 또는 Mercurial에서 자동화 된 배포를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-215">You can use these credentials tooclone hello site with git or set up automated deployments from GitHub, TFS, or Mercurial.</span></span>  <span data-ttu-id="369c6-216">자세한 내용은 참조 hello [Azure 앱 서비스 배포 설명서]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-216">For more information, see hello [Azure App Service deployment documentation].</span></span>

### <span data-ttu-id="369c6-217"><a name="appsettings"></a>응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="369c6-217"><a name="appsettings"></a>Application Settings</span></span>
<span data-ttu-id="369c6-218">마이그레이션된 모바일 서비스에 대한 설정은 대부분 앱 설정을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-218">Most settings for a migrated mobile service are available via App Settings.</span></span>  <span data-ttu-id="369c6-219">Hello에서 hello 응용 프로그램 설정 목록이 가져올 수 있습니다 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-219">You can get a list of hello app settings from hello [Azure portal].</span></span>
<span data-ttu-id="369c6-220">tooview 응용 프로그램 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-220">tooview or change your app settings:</span></span>

1. <span data-ttu-id="369c6-221">Toohello 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-221">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="369c6-222">선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-222">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="369c6-223">기본적으로 hello 설정 블레이드에서가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-223">hello Settings blade opens by default.</span></span>
4. <span data-ttu-id="369c6-224">클릭 **응용 프로그램 설정** hello 일반 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-224">Click **Application settings** in hello GENERAL menu.</span></span>
5. <span data-ttu-id="369c6-225">응용 프로그램 설정 섹션 toohello 스크롤하여 응용 프로그램 설정의 찾을 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-225">Scroll toohello App Settings section and find your app setting.</span></span>
6. <span data-ttu-id="369c6-226">Hello 앱 설정 tooedit hello 값의 hello 값을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-226">Click hello value of hello app setting tooedit hello value.</span></span>  <span data-ttu-id="369c6-227">클릭 **저장** toosave hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-227">Click **Save** toosave hello value.</span></span>

<span data-ttu-id="369c6-228">Hello에서 여러 앱 설정을 업데이트할 수 있습니다 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-228">You can update multiple app settings at hello same time.</span></span>

> [!TIP]
> <span data-ttu-id="369c6-229">두 가지 응용 프로그램 설정을 hello로 동일한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-229">There are two Application Settings with hello same value.</span></span>  <span data-ttu-id="369c6-230">예를 들어 *ApplicationKey* 및 *MS\_ApplicationKey*를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-230">For example, you may see *ApplicationKey* and *MS\_ApplicationKey*.</span></span>  <span data-ttu-id="369c6-231">Hello에 두 응용 프로그램 설정을 업데이트 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-231">Update both application settings at hello same time.</span></span>
>
>

### <span data-ttu-id="369c6-232"><a name="authentication"></a>인증</span><span class="sxs-lookup"><span data-stu-id="369c6-232"><a name="authentication"></a>Authentication</span></span>
<span data-ttu-id="369c6-233">모든 인증 설정은 마이그레이션된 사이트에서 앱 설정으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-233">All authentication settings are available as App Settings in your migrated site.</span></span>  <span data-ttu-id="369c6-234">tooupdate 인증 설정에 적절 한 응용 프로그램 설정을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-234">tooupdate your authentication settings, you must alter the appropriate app settings.</span></span>  <span data-ttu-id="369c6-235">hello 아래 표에 나와 인증 공급자에 대 한 hello 적절 한 응용 프로그램 설정.</span><span class="sxs-lookup"><span data-stu-id="369c6-235">hello following table shows hello appropriate app settings for your authentication provider:</span></span>

| <span data-ttu-id="369c6-236">공급자</span><span class="sxs-lookup"><span data-stu-id="369c6-236">Provider</span></span> | <span data-ttu-id="369c6-237">클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="369c6-237">Client ID</span></span> | <span data-ttu-id="369c6-238">클라이언트 암호</span><span class="sxs-lookup"><span data-stu-id="369c6-238">Client Secret</span></span> | <span data-ttu-id="369c6-239">기타 설정</span><span class="sxs-lookup"><span data-stu-id="369c6-239">Other Settings</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="369c6-240">Microsoft 계정</span><span class="sxs-lookup"><span data-stu-id="369c6-240">Microsoft Account</span></span> |<span data-ttu-id="369c6-241">**MS\_MicrosoftClientID**</span><span class="sxs-lookup"><span data-stu-id="369c6-241">**MS\_MicrosoftClientID**</span></span> |<span data-ttu-id="369c6-242">**MS\_MicrosoftClientSecret**</span><span class="sxs-lookup"><span data-stu-id="369c6-242">**MS\_MicrosoftClientSecret**</span></span> |<span data-ttu-id="369c6-243">**MS\_MicrosoftPackageSID**</span><span class="sxs-lookup"><span data-stu-id="369c6-243">**MS\_MicrosoftPackageSID**</span></span> |
| <span data-ttu-id="369c6-244">Facebook</span><span class="sxs-lookup"><span data-stu-id="369c6-244">Facebook</span></span> |<span data-ttu-id="369c6-245">**MS\_FacebookAppID**</span><span class="sxs-lookup"><span data-stu-id="369c6-245">**MS\_FacebookAppID**</span></span> |<span data-ttu-id="369c6-246">**MS\_FacebookAppSecret**</span><span class="sxs-lookup"><span data-stu-id="369c6-246">**MS\_FacebookAppSecret**</span></span> | |
| <span data-ttu-id="369c6-247">Twitter</span><span class="sxs-lookup"><span data-stu-id="369c6-247">Twitter</span></span> |<span data-ttu-id="369c6-248">**MS\_TwitterConsumerKey**</span><span class="sxs-lookup"><span data-stu-id="369c6-248">**MS\_TwitterConsumerKey**</span></span> |<span data-ttu-id="369c6-249">**MS\_TwitterConsumerSecret**</span><span class="sxs-lookup"><span data-stu-id="369c6-249">**MS\_TwitterConsumerSecret**</span></span> | |
| <span data-ttu-id="369c6-250">Google</span><span class="sxs-lookup"><span data-stu-id="369c6-250">Google</span></span> |<span data-ttu-id="369c6-251">**MS\_GoogleClientID**</span><span class="sxs-lookup"><span data-stu-id="369c6-251">**MS\_GoogleClientID**</span></span> |<span data-ttu-id="369c6-252">**MS\_GoogleClientSecret**</span><span class="sxs-lookup"><span data-stu-id="369c6-252">**MS\_GoogleClientSecret**</span></span> | |
| <span data-ttu-id="369c6-253">Azure AD</span><span class="sxs-lookup"><span data-stu-id="369c6-253">Azure AD</span></span> |<span data-ttu-id="369c6-254">**MS\_AadClientID**</span><span class="sxs-lookup"><span data-stu-id="369c6-254">**MS\_AadClientID**</span></span> | |<span data-ttu-id="369c6-255">**MS\_AadTenants**</span><span class="sxs-lookup"><span data-stu-id="369c6-255">**MS\_AadTenants**</span></span> |

<span data-ttu-id="369c6-256">참고: **MS\_AadTenants** 테 넌 트 도메인 (hello hello 모바일 서비스 포털에서 필드 "허용 테 넌 트")의 쉼표로 구분 된 목록으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-256">Note: **MS\_AadTenants** is stored as a comma-separated list of tenant domains (hello "Allowed Tenants" fields in hello Mobile Services portal).</span></span>

> [!WARNING]
> <span data-ttu-id="369c6-257">**Hello 설정 메뉴에서 hello 인증 메커니즘을 사용 하지 않습니다**</span><span class="sxs-lookup"><span data-stu-id="369c6-257">**Do not use hello authentication mechanisms in hello Settings menu**</span></span>
>
> <span data-ttu-id="369c6-258">Azure 앱 서비스는 hello에서 별도 "코드 없음" 인증 및 권한 부여 시스템 제공 *인증 / 권한 부여* 설정 메뉴 및 (사용 되지 않음) hello *모바일 인증* hello 설정 메뉴에서 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-258">Azure App Service provides a separate "no-code" Authentication and Authorization system under hello *Authentication / Authorization* Settings menu and hello (deprecated) *Mobile Authentication* option under hello Settings menu.</span></span>  <span data-ttu-id="369c6-259">이러한 옵션은 마이그레이션된 Azure 모바일 서비스와 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-259">These options are incompatible with a migrated Azure Mobile Service.</span></span>  <span data-ttu-id="369c6-260">할 수 있습니다 [사이트 업그레이드](app-service-mobile-net-upgrading-from-mobile-services.md) hello Azure 앱 서비스 인증 tootake 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-260">You can [upgrade your site](app-service-mobile-net-upgrading-from-mobile-services.md) tootake advantage of hello Azure App Service authentication.</span></span>
>
>

### <span data-ttu-id="369c6-261"><a name="easytables"></a>데이터</span><span class="sxs-lookup"><span data-stu-id="369c6-261"><a name="easytables"></a>Data</span></span>
<span data-ttu-id="369c6-262">hello *데이터* 모바일 서비스에서 탭으로 대체 되었습니다 *쉽게 테이블* hello Azure 포털 내에서.</span><span class="sxs-lookup"><span data-stu-id="369c6-262">hello *Data* tab in Mobile Services has been replaced by *Easy Tables* within hello Azure portal.</span></span>  <span data-ttu-id="369c6-263">tooaccess 쉽게 테이블:</span><span class="sxs-lookup"><span data-stu-id="369c6-263">tooaccess Easy Tables:</span></span>

1. <span data-ttu-id="369c6-264">Toohello 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-264">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="369c6-265">선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-265">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="369c6-266">기본적으로 hello 설정 블레이드에서가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-266">hello Settings blade opens by default.</span></span>
4. <span data-ttu-id="369c6-267">클릭 **쉽게 테이블** hello 모바일 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-267">Click **Easy tables** in hello MOBILE menu.</span></span>

<span data-ttu-id="369c6-268">Hello를 클릭 하 여 테이블을 추가할 수 있습니다 **추가** 단추 또는 테이블 이름을 클릭 하 여 기존 테이블에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-268">You can add a table by clicking hello **Add** button or access your existing tables by clicking a table name.</span></span>  <span data-ttu-id="369c6-269">다음을 비롯하여 이 블레이드에서 할 수 있는 다양한 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-269">There are various operations you can do from this blade, including:</span></span>

* <span data-ttu-id="369c6-270">테이블 사용 권한 변경</span><span class="sxs-lookup"><span data-stu-id="369c6-270">Changing table permissions</span></span>
* <span data-ttu-id="369c6-271">Hello 작업 스크립트를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-271">Editing hello operational scripts</span></span>
* <span data-ttu-id="369c6-272">Hello 테이블 스키마 관리</span><span class="sxs-lookup"><span data-stu-id="369c6-272">Managing hello table schema</span></span>
* <span data-ttu-id="369c6-273">Hello 테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="369c6-273">Deleting hello table</span></span>
* <span data-ttu-id="369c6-274">Hello 테이블 내용 지우기</span><span class="sxs-lookup"><span data-stu-id="369c6-274">Clearing hello table contents</span></span>
* <span data-ttu-id="369c6-275">Hello 테이블의 특정 행 삭제</span><span class="sxs-lookup"><span data-stu-id="369c6-275">Deleting specific rows of hello table</span></span>

### <span data-ttu-id="369c6-276"><a name="easyapis"></a>API</span><span class="sxs-lookup"><span data-stu-id="369c6-276"><a name="easyapis"></a>API</span></span>
<span data-ttu-id="369c6-277">hello *API* 모바일 서비스에서 탭으로 대체 되었습니다 *쉽게 Api* hello Azure 포털 내에서.</span><span class="sxs-lookup"><span data-stu-id="369c6-277">hello *API* tab in Mobile Services has been replaced by *Easy APIs* within hello Azure portal.</span></span>  <span data-ttu-id="369c6-278">tooaccess 쉽게 Api:</span><span class="sxs-lookup"><span data-stu-id="369c6-278">tooaccess Easy APIs:</span></span>

1. <span data-ttu-id="369c6-279">Toohello 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-279">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="369c6-280">선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-280">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="369c6-281">기본적으로 hello 설정 블레이드에서가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-281">hello Settings blade opens by default.</span></span>
4. <span data-ttu-id="369c6-282">클릭 **쉽게 Api** hello 모바일 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-282">Click **Easy APIs** in hello MOBILE menu.</span></span>

<span data-ttu-id="369c6-283">마이그레이션된 Api는 이미 hello 블레이드에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-283">Your migrated APIs are already listed in hello blade.</span></span>  <span data-ttu-id="369c6-284">또한 이 블레이드에서 API를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-284">You can also add an API from this blade.</span></span>  <span data-ttu-id="369c6-285">특정 API toomanage hello API를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-285">toomanage a specific API, click hello API.</span></span>
<span data-ttu-id="369c6-286">Hello 새 블레이드에서 hello 사용 권한 조정 하 고 hello API에 대 한 hello 스크립트를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-286">From hello new blade, you can adjust hello permissions and edit hello scripts for hello API.</span></span>

### <span data-ttu-id="369c6-287"><a name="on-demand-jobs"></a>스케줄러 작업</span><span class="sxs-lookup"><span data-stu-id="369c6-287"><a name="on-demand-jobs"></a>Scheduler Jobs</span></span>
<span data-ttu-id="369c6-288">모든 스케줄러 작업은 스케줄러 작업 컬렉션 섹션 hello를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-288">All scheduler jobs are available through hello Scheduler Job Collections section.</span></span>  <span data-ttu-id="369c6-289">tooaccess 스케줄러 작업:</span><span class="sxs-lookup"><span data-stu-id="369c6-289">tooaccess your scheduler jobs:</span></span>

1. <span data-ttu-id="369c6-290">Toohello 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-290">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="369c6-291">선택 **찾아보기 >**, 입력 **일정** hello에 *필터* 상자를 선택한 다음 선택 **스케줄러 컬렉션**합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-291">Select **Browse>**, enter **Schedule** in hello *Filter* box, then select **Scheduler Collections**.</span></span>
3. <span data-ttu-id="369c6-292">사이트에 대 한 hello 작업 컬렉션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-292">Select hello Job Collection for your site.</span></span>  <span data-ttu-id="369c6-293">*sitename*-Jobs로 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-293">It is named *sitename*-Jobs.</span></span>
4. <span data-ttu-id="369c6-294">**설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-294">Click **Settings**.</span></span>
5. <span data-ttu-id="369c6-295">관리 아래에 있는 **스케줄러 작업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-295">Click **Scheduler Jobs** under MANAGE.</span></span>

<span data-ttu-id="369c6-296">마이그레이션을 시작 하기 전에 지정한 hello 빈도로 예약 된 작업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-296">Scheduled jobs are listed with hello frequency you specified before migration.</span></span>  <span data-ttu-id="369c6-297">주문형 작업은 사용할 수 없게 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-297">On-demand jobs are disabled.</span></span>  <span data-ttu-id="369c6-298">toorun 주문형 작업:</span><span class="sxs-lookup"><span data-stu-id="369c6-298">toorun an on-demand job:</span></span>

1. <span data-ttu-id="369c6-299">Toorun hello 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-299">Select hello job you wish toorun.</span></span>
2. <span data-ttu-id="369c6-300">필요한 경우 클릭 **사용** tooenable hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-300">If necessary, click **Enable** tooenable hello job.</span></span>
3. <span data-ttu-id="369c6-301">**설정**을 클릭한 다음 **일정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-301">Click **Settings**, then **Schedule**.</span></span>
4. <span data-ttu-id="369c6-302">**한 번** 되풀이를 선택한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-302">Select a Recurrence of **Once**, then Click **Save**</span></span>

<span data-ttu-id="369c6-303">요청 시 작업은 `App_Data/config/scripts/scheduler post-migration`에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-303">Your on-demand jobs are located in `App_Data/config/scripts/scheduler post-migration`.</span></span>  <span data-ttu-id="369c6-304">모든 주문형 작업은 너무 변환 하는 것이 좋습니다[WebJobs] 또는 [Functions]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-304">We recommend that you convert all on-demand jobs too[WebJobs] or [Functions].</span></span>  <span data-ttu-id="369c6-305">[WebJobs] 또는 [Functions]로 새 스케줄러 작업을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-305">Write new scheduler jobs as [WebJobs] or [Functions].</span></span>

### <span data-ttu-id="369c6-306"><a name="notification-hubs"></a>알림 허브</span><span class="sxs-lookup"><span data-stu-id="369c6-306"><a name="notification-hubs"></a>Notification Hubs</span></span>
<span data-ttu-id="369c6-307">모바일 서비스는 푸시 알림에 알림 허브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-307">Mobile Services uses Notification Hubs for push notifications.</span></span>  <span data-ttu-id="369c6-308">앱 설정에 따라 hello 마이그레이션 후 사용 되는 toolink hello 알림 허브 tooyour 모바일 서비스에는:</span><span class="sxs-lookup"><span data-stu-id="369c6-308">hello following App Settings are used toolink hello Notification Hub tooyour Mobile Service after migration:</span></span>

| <span data-ttu-id="369c6-309">응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="369c6-309">Application Setting</span></span> | <span data-ttu-id="369c6-310">설명</span><span class="sxs-lookup"><span data-stu-id="369c6-310">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="369c6-311">**MS\_PushEntityNamespace**</span><span class="sxs-lookup"><span data-stu-id="369c6-311">**MS\_PushEntityNamespace**</span></span> |<span data-ttu-id="369c6-312">알림 허브 Namespace hello</span><span class="sxs-lookup"><span data-stu-id="369c6-312">hello Notification Hub Namespace</span></span> |
| <span data-ttu-id="369c6-313">**MS\_NotificationHubName**</span><span class="sxs-lookup"><span data-stu-id="369c6-313">**MS\_NotificationHubName**</span></span> |<span data-ttu-id="369c6-314">hello 알림 허브 이름</span><span class="sxs-lookup"><span data-stu-id="369c6-314">hello Notification Hub Name</span></span> |
| <span data-ttu-id="369c6-315">**MS\_NotificationHubConnectionString**</span><span class="sxs-lookup"><span data-stu-id="369c6-315">**MS\_NotificationHubConnectionString**</span></span> |<span data-ttu-id="369c6-316">hello 알림 허브 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="369c6-316">hello Notification Hub Connection String</span></span> |
| <span data-ttu-id="369c6-317">**MS\_NamespaceName**</span><span class="sxs-lookup"><span data-stu-id="369c6-317">**MS\_NamespaceName**</span></span> |<span data-ttu-id="369c6-318">MS_PushEntityNamespace에 대한 별칭</span><span class="sxs-lookup"><span data-stu-id="369c6-318">An alias for MS_PushEntityNamespace</span></span> |

<span data-ttu-id="369c6-319">알림 허브는 hello을 통해 관리 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-319">Your Notification Hub is managed through hello [Azure portal].</span></span>  <span data-ttu-id="369c6-320">Hello 알림 허브 이름 (이 찾을 수 있습니다 hello 응용 프로그램 설정을 사용 하 여) note:</span><span class="sxs-lookup"><span data-stu-id="369c6-320">Note hello Notification Hub name (you can find this using hello App Settings):</span></span>

1. <span data-ttu-id="369c6-321">Toohello 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-321">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="369c6-322">**찾아보기**>를 선택한 다음 **Notification Hubs**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-322">Select **Browse**>, then select **Notification Hubs**</span></span>
3. <span data-ttu-id="369c6-323">Hello 모바일 서비스와 연결 된 hello 알림 허브 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-323">Click hello Notification Hub name associated with hello mobile service.</span></span>

> [!NOTE]
> <span data-ttu-id="369c6-324">Notification Hubs가 "혼합" 형식이면 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-324">If your Notification HUb is a "Mixed" type, it is not visible.</span></span>  <span data-ttu-id="369c6-325">"혼합" 형식 알림 허브는 알림 허브 및 레거시 서비스 버스 기능을 모두 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-325">"Mixed" type notification hubs utilize both Notification Hubs and legacy Service Bus features.</span></span>  <span data-ttu-id="369c6-326">계속하기 전에 [혼합 네임스페이스를 변환]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-326">[Convert your Mixed namespaces] before continuing.</span></span>  <span data-ttu-id="369c6-327">Hello 변환이 완료 되 면 알림 허브 hello가 표시 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-327">Once hello conversion is complete, your notification hub appears in hello [Azure portal].</span></span>
>
>

<span data-ttu-id="369c6-328">자세한 내용을 보려면 검토 hello [알림 허브] 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-328">For more information, review hello [Notification Hubs] documentation.</span></span>

> [!TIP]
> <span data-ttu-id="369c6-329">Hello에 알림 허브 관리 기능 [Azure 포털] 미리 보기에서 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-329">Notification Hubs management features in hello [Azure portal] are still in preview.</span></span>  <span data-ttu-id="369c6-330">hello [Azure 클래식 포털] 모든 알림 허브를 관리 하기 위한 사용 가능한 상태로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-330">hello [Azure Classic Portal] remains available for managing all your Notification Hubs.</span></span>
>
>

### <span data-ttu-id="369c6-331"><a name="legacy-push"></a>레거시 푸시 설정</span><span class="sxs-lookup"><span data-stu-id="369c6-331"><a name="legacy-push"></a>Legacy Push Settings</span></span>
<span data-ttu-id="369c6-332">사용 하는 알림 허브에 hello 소개 하기 전에 모바일 서비스에 푸시를 구성한 경우 *기존 푸시*합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-332">If you configured Push on your mobile service before hello introduction on Notification Hubs, you are using *legacy push*.</span></span>  <span data-ttu-id="369c6-333">사용 중인 푸시 구성에 Notification Hubs가 표시되지 않으면 *레거시 푸시*가 사용되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-333">If you are using Push and you do not see a Notification Hub listed in your configuration, then it is likely you are using *legacy push*.</span></span>  <span data-ttu-id="369c6-334">이 기능은 다른 기능과 함께 마이그레이션됩니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-334">This feature is migrated with all the other features.</span></span>  <span data-ttu-id="369c6-335">그러나 hello 마이그레이션이 완료 된 후에 곧 tooNotification 허브를 업그레이드 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-335">However, we recommend that you upgrade tooNotification Hubs soon after hello migration is complete.</span></span>

<span data-ttu-id="369c6-336">중간 hello, 모든 hello 기존 푸시 설정 (주목할 만한 예외 hello APNS 인증서의 hello)에서 사용할 수 있습니다 앱 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-336">In hello interim, all hello legacy push settings (with hello notable exception of hello APNS certificate) are available in App Settings.</span></span>  <span data-ttu-id="369c6-337">Hello hello 파일 시스템에 적합 한 파일을 대체 하 여 hello APNS 인증서를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-337">Update hello APNS certificate by replacing hello appropriate file on hello filesystem.</span></span>

### <span data-ttu-id="369c6-338"><a name="app-settings"></a>기타 앱 설정</span><span class="sxs-lookup"><span data-stu-id="369c6-338"><a name="app-settings"></a>Other App Settings</span></span>
<span data-ttu-id="369c6-339">추가 응용 프로그램 설정은 다음 hello은 모바일 서비스에서 마이그레이션된 및에서 사용할 수 있는 *설정* > *앱 설정*:</span><span class="sxs-lookup"><span data-stu-id="369c6-339">hello following additional app settings are migrated from your Mobile Service and available under *Settings* > *App Settings*:</span></span>

| <span data-ttu-id="369c6-340">응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="369c6-340">Application Setting</span></span> | <span data-ttu-id="369c6-341">설명</span><span class="sxs-lookup"><span data-stu-id="369c6-341">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="369c6-342">**MS\_MobileServiceName**</span><span class="sxs-lookup"><span data-stu-id="369c6-342">**MS\_MobileServiceName**</span></span> |<span data-ttu-id="369c6-343">앱의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="369c6-343">hello name of your app</span></span> |
| <span data-ttu-id="369c6-344">**MS\_MobileServiceDomainSuffix**</span><span class="sxs-lookup"><span data-stu-id="369c6-344">**MS\_MobileServiceDomainSuffix**</span></span> |<span data-ttu-id="369c6-345">hello 도메인 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-345">hello domain prefix.</span></span> <span data-ttu-id="369c6-346">예:</span><span class="sxs-lookup"><span data-stu-id="369c6-346">i.e</span></span> <span data-ttu-id="369c6-347">azure-mobile.net</span><span class="sxs-lookup"><span data-stu-id="369c6-347">azure-mobile.net</span></span> |
| <span data-ttu-id="369c6-348">**MS\_ApplicationKey**</span><span class="sxs-lookup"><span data-stu-id="369c6-348">**MS\_ApplicationKey**</span></span> |<span data-ttu-id="369c6-349">응용 프로그램 키</span><span class="sxs-lookup"><span data-stu-id="369c6-349">Your application key</span></span> |
| <span data-ttu-id="369c6-350">**MS\_MasterKey**</span><span class="sxs-lookup"><span data-stu-id="369c6-350">**MS\_MasterKey**</span></span> |<span data-ttu-id="369c6-351">앱 마스터 키</span><span class="sxs-lookup"><span data-stu-id="369c6-351">Your app master key</span></span> |

<span data-ttu-id="369c6-352">hello 응용 프로그램 키와 마스터 키에는 원래 모바일 서비스에서 동일한 toohello 응용 프로그램 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-352">hello application key and master key are identical toohello Application Keys from your original Mobile Service.</span></span>  <span data-ttu-id="369c6-353">특히, 응용 프로그램 키 hello hello 모바일 API의 사용을 toovalidate 모바일 클라이언트에서 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-353">In particular, hello Application Key is sent by mobile clients toovalidate their use of hello mobile API.</span></span>

### <span data-ttu-id="369c6-354"><a name="cliequivalents"></a>해당하는 명령줄</span><span class="sxs-lookup"><span data-stu-id="369c6-354"><a name="cliequivalents"></a>Command-Line Equivalents</span></span>
<span data-ttu-id="369c6-355">Hello를 더 이상 사용할 수 *azure 모바일* toomanage Azure 모바일 서비스 사이트 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-355">You can longer use hello *azure mobile* command toomanage your Azure Mobile Services site.</span></span>  <span data-ttu-id="369c6-356">다양 한 함수 hello로 대체 되었습니다 대신 *azure 사이트* 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-356">Instead, many functions have been replaced with hello *azure site* command.</span></span>  <span data-ttu-id="369c6-357">다음 테이블 toofind 해당 하는 일반적인 명령에 대 한 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-357">Use hello following table toofind equivalents for common commands:</span></span>

| <span data-ttu-id="369c6-358">*Azure 모바일* 명령</span><span class="sxs-lookup"><span data-stu-id="369c6-358">*Azure Mobile* Command</span></span> | <span data-ttu-id="369c6-359">해당하는 *Azure 사이트* 명령</span><span class="sxs-lookup"><span data-stu-id="369c6-359">Equivalent *Azure Site* command</span></span> |
|:--- |:--- |
| <span data-ttu-id="369c6-360">모바일 위치</span><span class="sxs-lookup"><span data-stu-id="369c6-360">mobile locations</span></span> |<span data-ttu-id="369c6-361">사이트 위치 목록</span><span class="sxs-lookup"><span data-stu-id="369c6-361">site location list</span></span> |
| <span data-ttu-id="369c6-362">모바일 목록</span><span class="sxs-lookup"><span data-stu-id="369c6-362">mobile list</span></span> |<span data-ttu-id="369c6-363">사이트 목록</span><span class="sxs-lookup"><span data-stu-id="369c6-363">site list</span></span> |
| <span data-ttu-id="369c6-364">mobile show *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-364">mobile show *name*</span></span> |<span data-ttu-id="369c6-365">site show *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-365">site show *name*</span></span> |
| <span data-ttu-id="369c6-366">mobile restart *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-366">mobile restart *name*</span></span> |<span data-ttu-id="369c6-367">site restart *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-367">site restart *name*</span></span> |
| <span data-ttu-id="369c6-368">mobile redeploy *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-368">mobile redeploy *name*</span></span> |<span data-ttu-id="369c6-369">site deployment redeploy *commitId* *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-369">site deployment redeploy *commitId* *name*</span></span> |
| <span data-ttu-id="369c6-370">mobile key set *name* *type* *value*</span><span class="sxs-lookup"><span data-stu-id="369c6-370">mobile key set *name* *type* *value*</span></span> |<span data-ttu-id="369c6-371">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-371">site appsetting delete *key* *name*</span></span> <br/> <span data-ttu-id="369c6-372">site appsetting add *key*=*value* *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-372">site appsetting add *key*=*value* *name*</span></span> |
| <span data-ttu-id="369c6-373">mobile config list *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-373">mobile config list *name*</span></span> |<span data-ttu-id="369c6-374">site appsetting list *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-374">site appsetting list *name*</span></span> |
| <span data-ttu-id="369c6-375">mobile config get *name* *key*</span><span class="sxs-lookup"><span data-stu-id="369c6-375">mobile config get *name* *key*</span></span> |<span data-ttu-id="369c6-376">site appsetting show *key* *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-376">site appsetting show *key* *name*</span></span> |
| <span data-ttu-id="369c6-377">mobile config set *name* *key*</span><span class="sxs-lookup"><span data-stu-id="369c6-377">mobile config set *name* *key*</span></span> |<span data-ttu-id="369c6-378">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-378">site appsetting delete *key* *name*</span></span> <br/> <span data-ttu-id="369c6-379">site appsetting add *key*=*value* *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-379">site appsetting add *key*=*value* *name*</span></span> |
| <span data-ttu-id="369c6-380">mobile domain list *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-380">mobile domain list *name*</span></span> |<span data-ttu-id="369c6-381">site domain list *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-381">site domain list *name*</span></span> |
| <span data-ttu-id="369c6-382">mobile domain add *name* *domain*</span><span class="sxs-lookup"><span data-stu-id="369c6-382">mobile domain add *name* *domain*</span></span> |<span data-ttu-id="369c6-383">site domain add *domain* *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-383">site domain add *domain* *name*</span></span> |
| <span data-ttu-id="369c6-384">mobile domain delete *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-384">mobile domain delete *name*</span></span> |<span data-ttu-id="369c6-385">site domain delete *domain* *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-385">site domain delete *domain* *name*</span></span> |
| <span data-ttu-id="369c6-386">mobile scale show *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-386">mobile scale show *name*</span></span> |<span data-ttu-id="369c6-387">site show *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-387">site show *name*</span></span> |
| <span data-ttu-id="369c6-388">mobile scale change *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-388">mobile scale change *name*</span></span> |<span data-ttu-id="369c6-389">site scale mode *mode* *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-389">site scale mode *mode* *name*</span></span> <br /> <span data-ttu-id="369c6-390">site scale instances *instances* *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-390">site scale instances *instances* *name*</span></span> |
| <span data-ttu-id="369c6-391">mobile appsetting list *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-391">mobile appsetting list *name*</span></span> |<span data-ttu-id="369c6-392">site appsetting list *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-392">site appsetting list *name*</span></span> |
| <span data-ttu-id="369c6-393">mobile appsetting add *name* *key* *value*</span><span class="sxs-lookup"><span data-stu-id="369c6-393">mobile appsetting add *name* *key* *value*</span></span> |<span data-ttu-id="369c6-394">site appsetting add *key*=*value* *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-394">site appsetting add *key*=*value* *name*</span></span> |
| <span data-ttu-id="369c6-395">mobile appsetting delete *name* *key*</span><span class="sxs-lookup"><span data-stu-id="369c6-395">mobile appsetting delete *name* *key*</span></span> |<span data-ttu-id="369c6-396">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-396">site appsetting delete *key* *name*</span></span> |
| <span data-ttu-id="369c6-397">mobile appsetting show *name* *key*</span><span class="sxs-lookup"><span data-stu-id="369c6-397">mobile appsetting show *name* *key*</span></span> |<span data-ttu-id="369c6-398">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="369c6-398">site appsetting delete *key* *name*</span></span> |

<span data-ttu-id="369c6-399">인증 또는 푸시 알림 설정을 업데이트 하 여 적절 한 응용 프로그램 설정 hello를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-399">Update authentication or push notification settings by updating hello appropriate Application Setting.</span></span>
<span data-ttu-id="369c6-400">ftp 또는 git를 통해 파일을 편집하고 사이트를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-400">Edit files and publish your site via ftp or git.</span></span>

### <span data-ttu-id="369c6-401"><a name="diagnostics"></a>진단 및 로깅</span><span class="sxs-lookup"><span data-stu-id="369c6-401"><a name="diagnostics"></a>Diagnostics and Logging</span></span>
<span data-ttu-id="369c6-402">Azure 앱 서비스에서 정상적으로 진단 로깅을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-402">Diagnostic Logging is normally disabled in an Azure App Service.</span></span>  <span data-ttu-id="369c6-403">tooenable 진단 로깅:</span><span class="sxs-lookup"><span data-stu-id="369c6-403">tooenable diagnostic logging:</span></span>

1. <span data-ttu-id="369c6-404">Toohello 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-404">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="369c6-405">선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-405">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="369c6-406">기본적으로 hello 설정 블레이드에서가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-406">hello Settings blade opens by default.</span></span>
4. <span data-ttu-id="369c6-407">선택 **진단 로그** hello 기능 메뉴.</span><span class="sxs-lookup"><span data-stu-id="369c6-407">Select **Diagnostic Logs** under hello FEATURES menu.</span></span>
5. <span data-ttu-id="369c6-408">클릭 **ON** hello 다음 로그에 대 한: **응용 프로그램 로깅 (파일 시스템)**, **자세한 오류 메시지**, 및 **실패 한 요청 추적**</span><span class="sxs-lookup"><span data-stu-id="369c6-408">Click **ON** for hello following logs: **Application Logging (Filesystem)**, **Detailed error messages**, and **Failed request tracing**</span></span>
6. <span data-ttu-id="369c6-409">웹 서버 로깅에서 **파일 시스템** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-409">Click **File System** for Web server logging</span></span>
7. <span data-ttu-id="369c6-410">페이지 맨 아래에 있는 **저장**</span><span class="sxs-lookup"><span data-stu-id="369c6-410">Click **Save**</span></span>

<span data-ttu-id="369c6-411">tooview hello 로그:</span><span class="sxs-lookup"><span data-stu-id="369c6-411">tooview hello logs:</span></span>

1. <span data-ttu-id="369c6-412">Toohello 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-412">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="369c6-413">선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-413">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="369c6-414">Hello 클릭 **도구** 단추</span><span class="sxs-lookup"><span data-stu-id="369c6-414">Click hello **Tools** button</span></span>
4. <span data-ttu-id="369c6-415">선택 **로그 스트림** hello 관찰 메뉴.</span><span class="sxs-lookup"><span data-stu-id="369c6-415">Select **Log Stream** under hello OBSERVE menu.</span></span>

<span data-ttu-id="369c6-416">로그는 생성 될 때 hello 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-416">Logs are displayed in hello window as they are generated.</span></span>  <span data-ttu-id="369c6-417">배포 자격 증명을 사용 하 여 나중에 분석에 대 한 hello 로그를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-417">You can also download hello logs for later analysis using your deployment credentials.</span></span> <span data-ttu-id="369c6-418">자세한 내용은 참조 hello [로깅] 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-418">For more information, see hello [Logging] documentation.</span></span>

## <span data-ttu-id="369c6-419"><a name="known-issues"></a>알려진 문제</span><span class="sxs-lookup"><span data-stu-id="369c6-419"><a name="known-issues"></a>Known Issues</span></span>
### <a name="deleting-a-migrated-mobile-app-clone-causes-a-site-outage"></a><span data-ttu-id="369c6-420">마이그레이션된 모바일 앱 복제를 삭제하면 사이트 중단이 발생함</span><span class="sxs-lookup"><span data-stu-id="369c6-420">Deleting a Migrated Mobile App Clone causes a site outage</span></span>
<span data-ttu-id="369c6-421">Azure PowerShell delete hello 복제를 사용 하 여 마이그레이션된 모바일 서비스를 복제 하면 hello 프로덕션 서비스에 대 한 DNS 항목이 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-421">If you clone your migrated mobile service using Azure PowerShell, then delete hello clone, hello DNS entry for your production service is removed.</span></span>  <span data-ttu-id="369c6-422">사이트는 hello 인터넷에서에서 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-422">Your site is no longer be accessible from hello Internet.</span></span>  

<span data-ttu-id="369c6-423">해결 방법: 사이트 tooclone을 원할 경우 그렇게 hello 포털을 통해.</span><span class="sxs-lookup"><span data-stu-id="369c6-423">Resolution: If you wish tooclone your site, do so through hello portal.</span></span>

### <a name="changing-webconfig-does-not-work"></a><span data-ttu-id="369c6-424">Web.config를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-424">Changing Web.config does not work</span></span>
<span data-ttu-id="369c6-425">ASP.NET 사이트를 사용 하는 경우 변경 toohello `Web.config` 파일 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-425">If you have an ASP.NET site, changes toohello `Web.config` file do not get applied.</span></span>  <span data-ttu-id="369c6-426">Azure 앱 서비스 hello 적절 한 빌드 `Web.config` 시작 toosupport hello 모바일 서비스 런타임에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-426">hello Azure App Service builds a suitable `Web.config` file during startup toosupport hello Mobile Services runtime.</span></span>  <span data-ttu-id="369c6-427">XML 변환 파일을 사용하여 특정 설정(예: 사용자 지정 헤더)를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-427">You can override certain settings (such as custom headers) by using an XML transform file.</span></span>  <span data-ttu-id="369c6-428">파일 만들기에 호출 `applicationHost.xdt` -hello에이 파일 끝나야 `D:\home\site` 디렉터리 hello Azure 서비스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-428">Create a file in called `applicationHost.xdt` - this file must end up in hello `D:\home\site` directory on hello Azure Service.</span></span>  <span data-ttu-id="369c6-429">사용자 지정 배포 스크립트를 통하거나 Kudu를 사용하여 `applicationHost.xdt` 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-429">Upload the `applicationHost.xdt` file via a custom deployment script or directly using Kudu.</span></span>  <span data-ttu-id="369c6-430">hello 다음 예제에서는 문서를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-430">hello following shows an example document:</span></span>

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

<span data-ttu-id="369c6-431">자세한 내용은 참조 hello [XDT 변환 샘플] GitHub에 대 한 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-431">For more information, see hello [XDT Transform Samples] documentation on GitHub.</span></span>

### <a name="migrated-mobile-services-cannot-be-added-tootraffic-manager"></a><span data-ttu-id="369c6-432">마이그레이션된 모바일 서비스 tooTraffic 관리자를 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-432">Migrated Mobile Services cannot be added tooTraffic Manager</span></span>
<span data-ttu-id="369c6-433">트래픽 관리자 프로필을 만들 때 마이그레이션된 모바일 서비스 toohello 프로필을 직접 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-433">When you create a Traffic Manager profile, you cannot directly choose a migrated mobile service toohello profile.</span></span>  <span data-ttu-id="369c6-434">"외부 끝점"을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-434">Use an "external endpoint."</span></span>  <span data-ttu-id="369c6-435">PowerShell을 통해서만 외부 끝점을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-435">The external endpoint can only be added through PowerShell.</span></span>  <span data-ttu-id="369c6-436">자세한 내용은 [Traffic Manager 자습서](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-436">For more information, see the [Traffic Manager tutorial](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/).</span></span>

## <span data-ttu-id="369c6-437"><a name="next-steps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="369c6-437"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="369c6-438">이제 응용 프로그램 마이그레이션된 tooApp 서비스, 했으므로 더 많은 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-438">Now that your application is migrated tooApp Service, there are even more features you can use:</span></span>

* <span data-ttu-id="369c6-439">배포 [스테이징 슬롯] toostage 변경 tooyour 사이트를 허용 하 고 수행 A / B 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-439">Deployment [staging slots] allow you toostage changes tooyour site and perform A/B testing.</span></span>
* <span data-ttu-id="369c6-440">[WebJobs] 은 요청 시 예약된 작업을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-440">[WebJobs] provide a replacement for On-demand scheduled jobs.</span></span>
* <span data-ttu-id="369c6-441">있습니다 수 [지속적으로 배포] 사이트 tooGitHub, TFS 또는 Mercurial 연결 하 여 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-441">You can [continuously deploy] your site by linking your site tooGitHub, TFS, or Mercurial.</span></span>
* <span data-ttu-id="369c6-442">사용할 수 있습니다 [Application Insights] toomonitor 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-442">You can use [Application Insights] toomonitor your site.</span></span>
* <span data-ttu-id="369c6-443">웹 사이트는 서버와 모바일 API에서 동일한 코드를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-443">Serve a website and a Mobile API from hello same code.</span></span>

### <span data-ttu-id="369c6-444"><a name="upgrading-your-site"></a>모바일 서비스 사이트 tooAzure 모바일 앱 SDK를 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-444"><a name="upgrading-your-site"></a>Upgrading your Mobile Services site tooAzure Mobile Apps SDK</span></span>
* <span data-ttu-id="369c6-445">Node.js 기반 서버 프로젝트에 대 한 hello 새로운 [모바일 앱 Node.js SDK] 몇 가지 새로운 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-445">For Node.js-based server projects, hello new [Mobile Apps Node.js SDK] provides several new features.</span></span> <span data-ttu-id="369c6-446">예를 들어 이제 로컬 개발 및 디버깅을 수행하고 0.10 이후의 모든 Node.js 버전을 사용할 수 있으며 원하는 Express.js 미들웨어로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-446">For instance, you can now do local development and debugging, use any Node.js version above 0.10, and customize with any Express.js middleware.</span></span>
* <span data-ttu-id="369c6-447">에 대 한 .NET 기반 서버 프로젝트를 새로운 hello [모바일 앱 SDK NuGet 패키지](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) NuGet 종속성에 더 많은 유연성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-447">For .NET-based server projects, hello new [Mobile Apps SDK NuGet packages](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) have more flexibility on NuGet dependencies.</span></span>  <span data-ttu-id="369c6-448">이러한 패키지는 hello 새 앱 서비스 인증을 지원 하 고 ASP.NET 프로젝트 작성.</span><span class="sxs-lookup"><span data-stu-id="369c6-448">These packages support hello new App Service authentication, and compose with any ASP.NET project.</span></span> <span data-ttu-id="369c6-449">업그레이드에 대 한 자세한 참조 [업그레이드 하면 기존.NET 모바일 서비스 tooApp 서비스](app-service-mobile-net-upgrading-from-mobile-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="369c6-449">To learn more about upgrading, see [Upgrade your existing .NET Mobile Service tooApp Service](app-service-mobile-net-upgrading-from-mobile-services.md).</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-migrating-from-mobile-services/migrate-to-app-service-button.PNG
[1]: ./media/app-service-mobile-migrating-from-mobile-services/migration-activity-monitor.png
[2]: ./media/app-service-mobile-migrating-from-mobile-services/triggering-job-with-postman.png

<!-- Links -->
[앱 서비스 가격]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[Application Insights]: ../application-insights/app-insights-overview.md
[자동 크기 조정]: ../app-service-web/web-sites-scale.md
[Azure 앱 서비스]: ../app-service/app-service-value-prop-what-is.md
[Azure 앱 서비스 배포 설명서]: ../app-service-web/web-sites-deploy.md
[Azure 클래식 포털]: https://manage.windowsazure.com
[Azure 포털]: https://portal.azure.com
[Azure Region]: https://azure.microsoft.com/en-us/regions/
[Azure 스케줄러 계획]: ../scheduler/scheduler-plans-billing.md
[지속적으로 배포]: ../app-service-web/app-service-continuous-deployment.md
[혼합 네임스페이스를 변환]: https://azure.microsoft.com/en-us/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/
[curl]: http://curl.haxx.se/
[사용자 지정 도메인 이름]: ../app-service-web/web-sites-custom-domain-name.md
[Fiddler]: http://www.telerik.com/fiddler
[Azure 앱 서비스의 일반적인 가용성]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/
[하이브리드 연결]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[로깅]: ../app-service-web/web-sites-enable-diagnostic-log.md
[모바일 앱 Node.js SDK]: https://github.com/azure/azure-mobile-apps-node
[모바일 서비스 vs. App Service]: app-service-mobile-value-prop-migration-from-mobile-services.md
[알림 허브]: ../notification-hubs/notification-hubs-push-notification-overview.md
[성능 모니터링]: ../app-service-web/web-sites-monitor.md
[Postman]: http://www.getpostman.com/
[스테이징 슬롯]: ../app-service-web/web-sites-staged-publishing.md
[VNet]: ../app-service-web/web-sites-integrate-with-vnet.md
[WebJobs]: ../app-service-web/websites-webjobs-resources.md
[XDT 변환 샘플]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples
[Functions]: ../azure-functions/functions-overview.md
