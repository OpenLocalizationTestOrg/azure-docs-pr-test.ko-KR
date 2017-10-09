---
title: "탄력적 데이터베이스 도구 aaaGet 시작 | Microsoft Docs"
description: "기본적인 실행 방식 샘플 앱을 포함 하 여 Azure SQL 데이터베이스의 hello 탄력적 데이터베이스 도구 기능은 설명 합니다."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: CarlRabeler
ms.assetid: b6911f8d-2bae-4d04-9fa8-f79a3db7129d
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: a84e05c39dffbaef440538602f898acee6e0483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-elastic-database-tools"></a><span data-ttu-id="6cdc0-103">탄력적 데이터베이스 도구 시작하기</span><span class="sxs-lookup"><span data-stu-id="6cdc0-103">Get started with elastic database tools</span></span>
<span data-ttu-id="6cdc0-104">이 문서에서는 toorun hello 샘플 응용 프로그램 수 있도록 하 여 toohello 개발자 환경을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-104">This document introduces you toohello developer experience by helping you toorun hello sample app.</span></span> <span data-ttu-id="6cdc0-105">hello 예제는 간단한 분할 응용 프로그램을 만듭니다 하 고 탄력적 데이터베이스 도구의 주요 기능을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-105">hello sample creates a simple sharded application and explores key capabilities of elastic database tools.</span></span> <span data-ttu-id="6cdc0-106">hello 샘플의 hello 함수를 보여 줍니다. [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-106">hello sample demonstrates functions of hello [elastic database client library](sql-database-elastic-database-client-library.md).</span></span>

<span data-ttu-id="6cdc0-107">tooinstall hello 라이브러리 너무 이동[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-107">tooinstall hello library, go too[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> <span data-ttu-id="6cdc0-108">hello 라이브러리 hello 다음 섹션에에서 설명 된 hello 샘플 응용 프로그램으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-108">hello library is installed with hello sample app that's described in hello following section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6cdc0-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6cdc0-109">Prerequisites</span></span>
* <span data-ttu-id="6cdc0-110">C#이 있는 Visual Studio 2012 이상.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-110">Visual Studio 2012 or later with C#.</span></span> <span data-ttu-id="6cdc0-111">[Visual Studio 다운로드](http://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)에서 무료 버전을 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-111">Download a free version at [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>
* <span data-ttu-id="6cdc0-112">NuGet 2.7 이상.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-112">NuGet 2.7 or later.</span></span> <span data-ttu-id="6cdc0-113">tooget hello 최신 버전 참조 [NuGet 설치](http://docs.nuget.org/docs/start-here/installing-nuget)합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-113">tooget hello latest version, see [Installing NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>

## <a name="download-and-run-hello-sample-app"></a><span data-ttu-id="6cdc0-114">다운로드 하 고 hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="6cdc0-114">Download and run hello sample app</span></span>
<span data-ttu-id="6cdc0-115">hello **시작-Azure sql 탄력적 DB 도구** 샘플 응용 프로그램 탄력적 데이터베이스 도구를 사용 하는 분할 응용 프로그램에 대 한 hello 개발 환경의 hello 가장 중요 한 측면을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-115">hello **Elastic DB Tools for Azure SQL - Getting Started** sample application illustrates hello most important aspects of hello development experience for sharded applications that use elastic database tools.</span></span> <span data-ttu-id="6cdc0-116">[분할 맵 관리](sql-database-elastic-scale-shard-map-management.md), [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md) 및 [다중 분할 쿼리](sql-database-elastic-scale-multishard-querying.md)의 주요 사용 사례를 중점적으로 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-116">It focuses on key use cases for [shard map management](sql-database-elastic-scale-shard-map-management.md), [data-dependent routing](sql-database-elastic-scale-data-dependent-routing.md), and [multi-shard querying](sql-database-elastic-scale-multishard-querying.md).</span></span> <span data-ttu-id="6cdc0-117">toodownload 및 실행된 hello 샘플에는 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-117">toodownload and run hello sample, follow these steps:</span></span> 

1. <span data-ttu-id="6cdc0-118">Hello 다운로드 [Getting Started 샘플-Azure sql 탄력적 DB 도구](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-a80d8dc6) MSDN에서.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-118">Download hello [Elastic DB Tools for Azure SQL - Getting Started sample](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-a80d8dc6) from MSDN.</span></span> <span data-ttu-id="6cdc0-119">사용자가 선택한 hello 샘플 tooa 위치를 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-119">Unzip hello sample tooa location that you choose.</span></span>

2. <span data-ttu-id="6cdc0-120">toocreate 프로젝트를 열고 hello **ElasticScaleStarterKit.sln** hello에서 솔루션 **C#** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-120">toocreate a project, open hello **ElasticScaleStarterKit.sln** solution from hello **C#** directory.</span></span>

3. <span data-ttu-id="6cdc0-121">Hello 샘플 프로젝트에 대 한 hello 솔루션을 열고 hello **app.config** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-121">In hello solution for hello sample project, open hello **app.config** file.</span></span> <span data-ttu-id="6cdc0-122">그런 다음 Azure SQL 데이터베이스 서버 이름 및 사용자 로그인 정보 (사용자 이름 및 암호) hello 파일 tooadd의 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-122">Then follow hello instructions in hello file tooadd your Azure SQL Database server name and your sign-in information (user name and password).</span></span>

4. <span data-ttu-id="6cdc0-123">빌드하고 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-123">Build and run hello application.</span></span> <span data-ttu-id="6cdc0-124">메시지가 표시 되 면 hello 솔루션의 Visual Studio toorestore hello NuGet 패키지를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-124">When prompted, enable Visual Studio toorestore hello NuGet packages of hello solution.</span></span> <span data-ttu-id="6cdc0-125">이 NuGet에서 hello hello 탄력적 데이터베이스 클라이언트 라이브러리의 최신 버전을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-125">This downloads hello latest version of hello elastic database client library from NuGet.</span></span>

5. <span data-ttu-id="6cdc0-126">Hello 클라이언트 라이브러리 기능에 대 한 다양 한 옵션 toolearn hello 사용해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-126">Experiment with hello different options toolearn more about hello client library capabilities.</span></span> <span data-ttu-id="6cdc0-127">참고 hello 단계 hello 콘솔 출력에서 응용 프로그램에서는 hello 및 hello 백그라운드 무료 tooexplore hello 코드 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-127">Note hello steps hello application takes in hello console output and feel free tooexplore hello code behind hello scenes.</span></span>
   
    ![진행][4]

<span data-ttu-id="6cdc0-129">축하합니다. 이제 SQL Database에서 Elastic Database 도구를 사용하는 첫 번째 분할 응용 프로그램을 빌드하고 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-129">Congratulations--you have successfully built and run your first sharded application by using elastic database tools on SQL Database.</span></span> <span data-ttu-id="6cdc0-130">Visual Studio 또는 SQL Server Management Studio tooconnect tooyour SQL 데이터베이스를 사용 하 고 빠르게 생성 하는 샘플 hello hello 분할 확인을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-130">Use Visual Studio or SQL Server Management Studio tooconnect tooyour SQL database and take a quick look at hello shards that hello sample created.</span></span> <span data-ttu-id="6cdc0-131">새 샘플 분할 데이터베이스 및 shard map manager 데이터베이스 알게 될 hello 예제를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-131">You will notice new sample shard databases and a shard map manager database that hello sample has created.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6cdc0-132">업데이트 tooAzure 및 SQL 데이터베이스와 계속 동기화 되도록에 항상 hello Management Studio의 최신 버전을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-132">We recommend that you always use hello latest version of Management Studio so that you stay synchronized with updates tooAzure and SQL Database.</span></span> <span data-ttu-id="6cdc0-133">[SQL Server Management Studio를 업데이트합니다](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="6cdc0-133">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="key-pieces-of-hello-code-sample"></a><span data-ttu-id="6cdc0-134">Hello 코드 샘플의 핵심 부분</span><span class="sxs-lookup"><span data-stu-id="6cdc0-134">Key pieces of hello code sample</span></span>
* <span data-ttu-id="6cdc0-135">**분할 된 데이터베이스 및 분할 관리 매핑합니다**: hello 코드를 보여 줍니다 방법을 분할 된 데이터베이스, 범위, hello 파일의 매핑와 toowork **ShardManagementUtils.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-135">**Managing shards and shard maps**: hello code illustrates how toowork with shards, ranges, and mappings in hello file **ShardManagementUtils.cs**.</span></span> <span data-ttu-id="6cdc0-136">자세한 내용은 참조 [hello shard map manager와 함께 데이터베이스 확장](http://go.microsoft.com/?linkid=9862595)합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-136">For more information, see [Scale out databases with hello shard map manager](http://go.microsoft.com/?linkid=9862595).</span></span>  

* <span data-ttu-id="6cdc0-137">**데이터 종속 라우팅**:에 표시 되어 트랜잭션 toohello 오른쪽 분할의 라우팅을 **DataDependentRoutingSample.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-137">**Data-dependent routing**: Routing of transactions toohello right shard is shown in **DataDependentRoutingSample.cs**.</span></span> <span data-ttu-id="6cdc0-138">자세한 내용은 [데이터 종속 라우팅](http://go.microsoft.com/?linkid=9862596)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-138">For more information, see [Data-dependent routing](http://go.microsoft.com/?linkid=9862596).</span></span> 

* <span data-ttu-id="6cdc0-139">**여러 분할 된 데이터베이스에서의 쿼리**: hello 파일에 설명 되어 분할 된 데이터베이스 간 쿼리 **MultiShardQuerySample.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-139">**Querying over multiple shards**: Querying across shards is illustrated in hello file **MultiShardQuerySample.cs**.</span></span> <span data-ttu-id="6cdc0-140">자세한 내용은 [다중 분할 쿼리](http://go.microsoft.com/?linkid=9862597)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-140">For more information, see [Multi-shard querying](http://go.microsoft.com/?linkid=9862597).</span></span>

* <span data-ttu-id="6cdc0-141">**빈 분할 영역이 추가**: hello 새로운 빈 분할의 추가 반복적인 hello 파일의 hello 코드에 의해 수행 됩니다 **CreateShardSample.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-141">**Adding empty shards**: hello iterative adding of new empty shards is performed by hello code in hello file **CreateShardSample.cs**.</span></span> <span data-ttu-id="6cdc0-142">자세한 내용은 참조 [hello shard map manager와 함께 데이터베이스 확장](http://go.microsoft.com/?linkid=9862595)합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-142">For more information, see [Scale out databases with hello shard map manager](http://go.microsoft.com/?linkid=9862595).</span></span>

### <a name="other-elastic-scale-operations"></a><span data-ttu-id="6cdc0-143">기타 탄력적인 확장 작업</span><span class="sxs-lookup"><span data-stu-id="6cdc0-143">Other elastic scale operations</span></span>
* <span data-ttu-id="6cdc0-144">**기존 분할 분할**: hello 기능 toosplit 분할 된 데이터베이스는 hello에서 제공 **분할 / 병합 도구**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-144">**Splitting an existing shard**: hello capability toosplit shards is provided by hello **split-merge tool**.</span></span> <span data-ttu-id="6cdc0-145">자세한 내용은 [확장된 클라우드 데이터베이스 간 데이터 이동](sql-database-elastic-scale-overview-split-and-merge.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-145">For more information, see [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

* <span data-ttu-id="6cdc0-146">**기존 분할 영역을 병합**: hello를 사용 하 여 분할 병합도 이루어집니다 **분할 / 병합 도구**합니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-146">**Merging existing shards**: Shard merges are also performed by using hello **split-merge tool**.</span></span> <span data-ttu-id="6cdc0-147">자세한 내용은 [확장된 클라우드 데이터베이스 간 데이터 이동](sql-database-elastic-scale-overview-split-and-merge.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-147">For more information, see [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>   

## <a name="cost"></a><span data-ttu-id="6cdc0-148">비용</span><span class="sxs-lookup"><span data-stu-id="6cdc0-148">Cost</span></span>
<span data-ttu-id="6cdc0-149">hello 탄력적 데이터베이스 도구는 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-149">hello elastic database tools are free.</span></span> <span data-ttu-id="6cdc0-150">탄력적 데이터베이스 도구를 사용 하는 경우에 Azure 사용 현황을 hello 비용 맨 위에 추가 요금이 모든 수신 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-150">When you use elastic database tools, you don't receive any additional charges on top of hello cost of your Azure usage.</span></span> 

<span data-ttu-id="6cdc0-151">예를 들어 hello 샘플 응용 프로그램은 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-151">For example, hello sample application creates new databases.</span></span> <span data-ttu-id="6cdc0-152">이 대 한 hello 비용 hello SQL 데이터베이스 버전을 선택 하면 hello 응용 프로그램의 Azure 사용량에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-152">hello cost for this depends on hello SQL Database edition you choose and hello Azure usage of your application.</span></span>

<span data-ttu-id="6cdc0-153">가격 책정 정보는 [SQL Database 가격 책정 정보](https://azure.microsoft.com/pricing/details/sql-database/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6cdc0-153">For pricing information, see [SQL Database pricing details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cdc0-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6cdc0-154">Next steps</span></span>
<span data-ttu-id="6cdc0-155">탄력적 데이터베이스 도구에 대 한 자세한 내용은 다음 페이지 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="6cdc0-155">For more information about elastic database tools, see hello following pages:</span></span>

* <span data-ttu-id="6cdc0-156">코드 샘플:</span><span class="sxs-lookup"><span data-stu-id="6cdc0-156">Code samples:</span></span> 
  * [<span data-ttu-id="6cdc0-157">Azure SQL용 Elastic DB 도구 - 시작</span><span class="sxs-lookup"><span data-stu-id="6cdc0-157">Elastic DB Tools for Azure SQL - Getting Started</span></span>](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-a80d8dc6?SRC=VSIDE)
  * [<span data-ttu-id="6cdc0-158">Azure SQL용 Elastic DB 도구 - Entity Framework 통합</span><span class="sxs-lookup"><span data-stu-id="6cdc0-158">Elastic DB Tools for Azure SQL - Entity Framework Integration</span></span>](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-bae904ba?SRC=VSIDE)
  * [<span data-ttu-id="6cdc0-159">스크립트 센터의 분할된 데이터베이스 탄력성</span><span class="sxs-lookup"><span data-stu-id="6cdc0-159">Shard Elasticity on Script Center</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Elastic-Scale-Shard-c9530cbe)
* <span data-ttu-id="6cdc0-160">블로그: [탄력적인 확장 발표](https://azure.microsoft.com/blog/2014/10/02/introducing-elastic-scale-preview-for-azure-sql-database/)</span><span class="sxs-lookup"><span data-stu-id="6cdc0-160">Blog: [Elastic Scale announcement](https://azure.microsoft.com/blog/2014/10/02/introducing-elastic-scale-preview-for-azure-sql-database/)</span></span>
* <span data-ttu-id="6cdc0-161">Microsoft Virtual Academy: [hello 탄력적 데이터베이스 클라이언트 라이브러리 비디오로 확장을 사용 하 여 분할 구현](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554?l=lWyQhF1fC_6306218965)</span><span class="sxs-lookup"><span data-stu-id="6cdc0-161">Microsoft Virtual Academy: [Implementing Scale-Out Using Sharding with hello Elastic Database Client Library Video](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554?l=lWyQhF1fC_6306218965)</span></span> 
* <span data-ttu-id="6cdc0-162">채널 9: [탄력적인 확장 개요 비디오](http://channel9.msdn.com/Shows/Data-Exposed/Azure-SQL-Database-Elastic-Scale)</span><span class="sxs-lookup"><span data-stu-id="6cdc0-162">Channel 9: [Elastic Scale overview video](http://channel9.msdn.com/Shows/Data-Exposed/Azure-SQL-Database-Elastic-Scale)</span></span>
* <span data-ttu-id="6cdc0-163">토론 포럼: [Azure SQL Database 포럼](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)</span><span class="sxs-lookup"><span data-stu-id="6cdc0-163">Discussion forum: [Azure SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)</span></span>
* <span data-ttu-id="6cdc0-164">toomeasure 성능: [shard map manager에 대 한 성능 카운터](sql-database-elastic-database-client-library.md)</span><span class="sxs-lookup"><span data-stu-id="6cdc0-164">toomeasure performance: [Performance counters for shard map manager](sql-database-elastic-database-client-library.md)</span></span>

<!--Anchors-->
[hello Elastic Scale Sample Application]: #The-Elastic-Scale-Sample-Application
[Download and Run hello Sample App]: #Download-and-Run-the-Sample-App
[Cost]: #Cost
[Next steps]: #next-steps

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-get-started/newProject.png
[2]: ./media/sql-database-elastic-scale-get-started/click-online.png
[3]: ./media/sql-database-elastic-scale-get-started/click-CSharp.png
[4]: ./media/sql-database-elastic-scale-get-started/output2.png

