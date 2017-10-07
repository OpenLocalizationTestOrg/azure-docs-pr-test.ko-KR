---
title: "aaaUse 사례-고객 프로 파일링"
description: "Azure 데이터 팩터리는 사용 되는 toocreate 데이터 기반 워크플로 (파이프라인) tooprofile 게임 고객 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: e07d55cf-8051-4203-9966-bdfa1035104b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 47f5e77242366c80cce2a2db65e3c696505b3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---customer-profiling"></a><span data-ttu-id="fe926-103">사용 사례 - 고객 프로파일링</span><span class="sxs-lookup"><span data-stu-id="fe926-103">Use Case - Customer Profiling</span></span>
<span data-ttu-id="fe926-104">Azure Data Factory에는 많은 사용 되는 서비스 tooimplement hello Cortana Intelligence solution accelerator 제품군 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-104">Azure Data Factory is one of many services used tooimplement hello Cortana Intelligence Suite of solution accelerators.</span></span>  <span data-ttu-id="fe926-105">Cortana Intelligence에 대한 자세한 내용은 [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe926-105">For more information about Cortana Intelligence, visit [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics).</span></span> <span data-ttu-id="fe926-106">이 문서에서는 간단한 사용 사례 toohelp 설명 시작에 대 한 Azure Data Factory 수 일반적인 분석 문제를 해결 하는 방법을 이해 하는 데 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-106">In this document, we describe a simple use case toohelp you get started with understanding how Azure Data Factory can solve common analytics problems.</span></span>

## <a name="scenario"></a><span data-ttu-id="fe926-107">시나리오</span><span class="sxs-lookup"><span data-stu-id="fe926-107">Scenario</span></span>
<span data-ttu-id="fe926-108">Contoso는 게임 콘솔, 핸드헬드 장치, PC(개인용 컴퓨터) 등 다양한 플랫폼용 게임을 만드는 게임 회사입니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-108">Contoso is a gaming company that creates games for multiple platforms: game consoles, hand held devices, and personal computers (PCs).</span></span> <span data-ttu-id="fe926-109">플레이어가 게임, 대로 사용 패턴, 게임 스타일 및 hello 사용자의 기본 설정을 추적 hello를 큰 볼륨의 로그 데이터가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-109">As players play these games, large volume of log data is produced that tracks hello usage patterns, gaming style, and preferences of hello user.</span></span>  <span data-ttu-id="fe926-110">인구 통계, 국가 함께 사용 하면 제품 데이터를 Contoso 분석 tooguide tooenhance 플레이어 발생 하 고 업그레이드를 위한 대상으로 지정 하는 방법에 고 게임을 수행할 수 있습니다 및 구입 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-110">When combined with demographic, regional, and product data, Contoso can perform analytics tooguide them about how tooenhance players’ experience and target them for upgrades and in-game purchases.</span></span> 

<span data-ttu-id="fe926-111">Contoso의 목표는 플레이어의 hello 게임 기록에 근거 tooidentify 상향 판매/교차 판매 기회의 뛰어난 기능 toodrive 비즈니스 성장 추가 및 보다 나은 경험 toocustomers 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-111">Contoso’s goal is tooidentify up-sell/cross-sell opportunities based on hello gaming history of its players and add compelling features toodrive business growth and provide a better experience toocustomers.</span></span> <span data-ttu-id="fe926-112">이 사용 사례의 경우 비즈니스의 예로 게임 회사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-112">For this use case, we use a gaming company as an example of a business.</span></span> <span data-ttu-id="fe926-113">hello 회사 toooptimize 플레이어의 동작에 따라 해당 게임을 원합니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-113">hello company wants toooptimize its games based on players’ behavior.</span></span> <span data-ttu-id="fe926-114">이러한 원칙 tooengage가 원하는 tooany 비즈니스 해당 고객의 제품 및 서비스에 게 적용 하 고 고객 경험을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-114">These principles apply tooany business that wants tooengage its customers around its goods and services and enhance their customers’ experience.</span></span>

<span data-ttu-id="fe926-115">이 솔루션에서는 Contoso 최근에 시작 된 마케팅 캠페인의 tooevaluate hello 효과 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-115">In this solution, Contoso wants tooevaluate hello effectiveness of a marketing campaign it has recently launched.</span></span> <span data-ttu-id="fe926-116">에서는 시작 hello 원시 게임 로그, 프로세스 및 지리적 위치 데이터와 함께를 보강, 광고의 참조 데이터와 조인 하며 마지막으로 Azure SQL 데이터베이스 tooanalyze hello 캠페인의 영향에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-116">We start with hello raw gaming logs, process and enrich them with geolocation data, join it with advertising reference data, and lastly copy them into an Azure SQL Database tooanalyze hello campaign’s impact.</span></span>

## <a name="deploy-solution"></a><span data-ttu-id="fe926-117">솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="fe926-117">Deploy Solution</span></span>
<span data-ttu-id="fe926-118">모든 필요한 tooaccess 이며이 간단한 사용 사례 아웃 시도 [Azure 구독](https://azure.microsoft.com/pricing/free-trial/), [Azure Blob 저장소 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account), 및 [Azure SQL 데이터베이스](../sql-database/sql-database-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-118">All you need tooaccess and try out this simple use case is an [Azure subscription](https://azure.microsoft.com/pricing/free-trial/), an [Azure Blob storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), and an [Azure SQL Database](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="fe926-119">Hello에서 파이프라인을 프로 파일링 하는 hello 고객 배포 **샘플 파이프라인** 데이터 팩터리의 hello 홈 페이지에 바둑판식으로 배열 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-119">You deploy hello customer profiling pipeline from hello **Sample pipelines** tile on hello home page of your data factory.</span></span>

1. <span data-ttu-id="fe926-120">데이터 팩터리를 만들거나 기존 데이터 팩터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-120">Create a data factory or open an existing data factory.</span></span> <span data-ttu-id="fe926-121">참조 [Blob 저장소 tooSQL 데이터 팩터리를 사용 하 여 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계 toocreate 데이터 팩터리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-121">See [Copy data from Blob Storage tooSQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for steps toocreate a data factory.</span></span>
2. <span data-ttu-id="fe926-122">Hello에 **DATA FACTORY** 블레이드 hello 데이터 팩토리에 대 한 클릭 hello **샘플 파이프라인** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-122">In hello **DATA FACTORY** blade for hello data factory, click hello **Sample pipelines** tile.</span></span>

    ![샘플 파이프라인 타일](./media/data-factory-samples/SamplePipelinesTile.png)
3. <span data-ttu-id="fe926-124">Hello에 **샘플 파이프라인** 블레이드에서 hello 클릭 **프로 파일링 하는 고객** toodeploy 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-124">In hello **Sample pipelines** blade, click hello **Customer profiling** that you want toodeploy.</span></span>

    ![샘플 파이프라인 블레이드](./media/data-factory-samples/SampleTile.png)
4. <span data-ttu-id="fe926-126">Hello 샘플에 대 한 구성 설정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-126">Specify configuration settings for hello sample.</span></span> <span data-ttu-id="fe926-127">예를 들어 Azure Storage 계정 이름과 키, Azure SQL Server 이름, 데이터베이스, 사용자 ID, 암호 등입니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-127">For example, your Azure storage account name and key, Azure SQL server name, database, User ID, and password.</span></span>

    ![샘플 블레이드](./media/data-factory-samples/SampleBlade.png)
5. <span data-ttu-id="fe926-129">Hello 구성 설정을 지정 하 여 완료 한 후 클릭 **만들기** 샘플 파이프라인 및 hello 파이프라인에서 사용 되는 연결 된 서비스/테이블 hello toocreate/배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-129">After you are done with specifying hello configuration settings, click **Create** toocreate/deploy hello sample pipelines and linked services/tables used by hello pipelines.</span></span>
6. <span data-ttu-id="fe926-130">이전 hello 클릭 hello 샘플 타일에서 배포의 hello 상태를 확인할 **샘플 파이프라인** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-130">You see hello status of deployment on hello sample tile you clicked earlier on hello **Sample pipelines** blade.</span></span>

    ![배포 상태](./media/data-factory-samples/DeploymentStatus.png)
7. <span data-ttu-id="fe926-132">Hello 표시 되 면 **배포 성공** hello 타일 hello 샘플을 닫기 hello 메시지 **샘플 파이프라인** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-132">When you see hello **Deployment succeeded** message on hello tile for hello sample, close hello **Sample pipelines** blade.</span></span>  
8. <span data-ttu-id="fe926-133">**DATA FACTORY** 블레이드에 표시 연결 된 서비스, 데이터 집합 및 파이프라인 tooyour 데이터 팩터리 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-133">On **DATA FACTORY** blade, you see that linked services, data sets, and pipelines are added tooyour data factory.</span></span>  

    ![데이터 팩터리 블레이드](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="solution-overview"></a><span data-ttu-id="fe926-135">솔루션 개요</span><span class="sxs-lookup"><span data-stu-id="fe926-135">Solution Overview</span></span>
<span data-ttu-id="fe926-136">이 간단한 사용 사례는 Azure 데이터 팩터리 tooingest를 사용 하 여, 준비, 변환, 분석 하는 방법을 데이터 게시의 한 예로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-136">This simple use case can be used as an example of how you can use Azure Data Factory tooingest, prepare, transform, analyze, and publish data.</span></span>

![종단 간 워크플로](./media/data-factory-customer-profiling-usecase/EndToEndWorkflow.png)

<span data-ttu-id="fe926-138">이 그림에서는 hello 데이터 파이프라인에서에서 어떻게 나타나는지 hello Azure 포털 배포 된 후에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-138">This Figure depicts how hello data pipelines appear in hello Azure portal after they have been deployed.</span></span>

1. <span data-ttu-id="fe926-139">hello **PartitionGameLogsPipeline** hello 원시 게임 이벤트를 읽은 다음 blob 저장소에서 연도, 월 및 일을 기반으로 파티션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-139">hello **PartitionGameLogsPipeline** reads hello raw game events from blob storage and creates partitions based on year, month, and day.</span></span>
2. <span data-ttu-id="fe926-140">hello **EnrichGameLogsPipeline** 분할된 게임 이벤트와 지역 코드 참조 데이터를 조인 하 고 IP 주소 toohello 해당 지리적 위치에 매핑하여 hello 데이터를 강화 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-140">hello **EnrichGameLogsPipeline** joins partitioned game events with geo code reference data and enriches hello data by mapping IP addresses toohello corresponding geo-locations.</span></span>
3. <span data-ttu-id="fe926-141">hello **AnalyzeMarketingCampaignPipeline** 파이프라인 hello 보강 한 데이터를 사용 하 고 데이터 toocreate hello 최종 출력 마케팅 캠페인 효과 포함 하는 광고 hello를 사용 하 여 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-141">hello **AnalyzeMarketingCampaignPipeline** pipeline uses hello enriched data and processes it with hello advertising data toocreate hello final output that contains marketing campaign effectiveness.</span></span>

<span data-ttu-id="fe926-142">이 예제에서는 데이터 팩터리의 입력된 데이터, 변환 및 프로세스 hello 데이터를 복사 하 고 hello 최종 데이터 tooan Azure SQL 데이터베이스를 출력 하는 사용 되는 tooorchestrate 활동 이지만</span><span class="sxs-lookup"><span data-stu-id="fe926-142">In this example, Data Factory is used tooorchestrate activities that copy input data, transform, and process hello data, and output hello final data tooan Azure SQL Database.</span></span>  <span data-ttu-id="fe926-143">데이터 파이프라인의 hello 네트워크를 시각화 하 고, 관리 다음 hello UI에서에서 해당 상태를 모니터링 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-143">You can also visualize hello network of data pipelines, manage them, and monitor their status from hello UI.</span></span>

## <a name="benefits"></a><span data-ttu-id="fe926-144">이점</span><span class="sxs-lookup"><span data-stu-id="fe926-144">Benefits</span></span>
<span data-ttu-id="fe926-145">해당 사용자 프로필 분석을 최적화 하 고 비즈니스 목표에 맞추어를 게임 회사 수 tooquickly 수집 사용 패턴은 하 고 해당 마케팅 캠페인의 hello 효과 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe926-145">By optimizing their user profile analytics and aligning it with business goals, gaming company is able tooquickly collect usage patterns, and analyze hello effectiveness of its marketing campaigns.</span></span>

