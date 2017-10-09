---
title: "Azure SQL 데이터베이스에서 임시 테이블 시작 됨 aaaGetting | Microsoft Docs"
description: "Azure SQL 데이터베이스의 임시 테이블을 사용 하 여 tooget 시작 하는 방법에 대해 알아봅니다."
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: c8c0f232-0751-4a7f-a36e-67a0b29fa1b8
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 01/10/2017
ms.author: bonova
ms.openlocfilehash: 54f394b51df07aa2f9bb299f207e692171d23479
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="75f48-103">Azure SQL Database의 임시 테이블 시작</span><span class="sxs-lookup"><span data-stu-id="75f48-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="75f48-104">임시 테이블 tootrack 수 있는 Azure SQL 데이터베이스의 새로운 프로그래밍 기능 및 hello hello 사용자 지정 코딩이 필요 없이 데이터는 변경 내용의 전체 기록을 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you tootrack and analyze hello full history of changes in your data, without hello need for custom coding.</span></span> <span data-ttu-id="75f48-105">임시 테이블 데이터 밀접 한 관련이 tootime 컨텍스트 있도록 유지 저장 된 팩트를 해석 될 수 있는 유효한 것으로 hello 특정 기간 내 에서만.</span><span class="sxs-lookup"><span data-stu-id="75f48-105">Temporal Tables keep data closely related tootime context so that stored facts can be interpreted as valid only within hello specific period.</span></span> <span data-ttu-id="75f48-106">임시 테이블의 이 속성을 사용하면 효율적인 시간 기반 분석 및 데이터의 진화에서 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="75f48-107">임시 시나리오</span><span class="sxs-lookup"><span data-stu-id="75f48-107">Temporal Scenario</span></span>
<span data-ttu-id="75f48-108">이 문서에서는 응용 프로그램 시나리오에서는 hello 단계 tooutilize를 임시 테이블을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-108">This article illustrates hello steps tooutilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="75f48-109">사용자 작업 분석을 tooextend 되도록 기존 웹 사이트 또는 처음부터 새로 개발 되는 새 웹 사이트에서 사용자 동작을 tootrack 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-109">Suppose that you want tootrack user activity on a new website that is being developed from scratch or on an existing website that you want tooextend with user activity analytics.</span></span> <span data-ttu-id="75f48-110">이 간단한 예제에서는 일정 기간 동안 방문한 웹 페이지의 hello 숫자가 toobe 캡처되고 Azure SQL 데이터베이스에서 호스트 되는 hello 웹 사이트 데이터베이스에서 모니터링할 필요한 표시기 임을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-110">In this simplified example, we assume that hello number of visited web pages during a period of time is an indicator that needs toobe captured and monitored in hello website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="75f48-111">사용자 작업의 기록 분석 hello hello 목표는 tooget 입력 tooredesign 웹 사이트 및 hello 방문자에 대 한 더 나은 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-111">hello goal of hello historical analysis of user activity is tooget inputs tooredesign website and provide better experience for hello visitors.</span></span>

<span data-ttu-id="75f48-112">이 시나리오에 대 한 hello 데이터베이스 모델은 매우 간단-단일 정수 필드와 사용자 활동 메트릭이 표시 됩니다 **PageVisited**, 함께 hello 사용자 프로필에 대 한 기본 정보가 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-112">hello database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on hello user profile.</span></span> <span data-ttu-id="75f48-113">또한 시간 기반 분석을 위해 보관할 때 일련 각 사용자에 대 한 행의 모든 행이 특정 기간 내에서 특정 사용자가 방문 페이지 hello 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents hello number of pages a particular user visited within a specific period of time.</span></span>

![스키마](./media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="75f48-115">다행히 않아도 tooput 시도 앱 toomaintain에이 작업 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-115">Fortunately, you do not need tooput any effort in your app toomaintain this activity information.</span></span> <span data-ttu-id="75f48-116">된 임시 테이블에서이 프로세스 자동화-웹 사이트 설계와 자세한 시간 toofocus 자체 hello 데이터 분석에 동안 완벽 한 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time toofocus on hello data analysis itself.</span></span> <span data-ttu-id="75f48-117">toodo 있는 점은 tooensure만 hello를 **WebSiteInfo** 테이블으로 구성 된 [임시 시스템 버전 관리](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0)합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-117">hello only thing you have toodo is tooensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="75f48-118">이 시나리오에서는 hello 정확한 단계 tooutilize 임시 테이블에 대 한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-118">hello exact steps tooutilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="75f48-119">1단계: 임시로 테이블 구성</span><span class="sxs-lookup"><span data-stu-id="75f48-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="75f48-120">새로운 개발을 시작하거나 기존 응용 프로그램을 업그레이드하는 여부에 따라 임시 테이블을 만들거나 임시 특성을 추가하여 기존 템플릿을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="75f48-121">일반적인 경우 시나리오는 이러한 두 옵션을 혼합하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="75f48-122">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)(SSMS) [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx)(SSDT) 또는 기타 Transact-SQL 개발 도구를 사용하여 이러한 작업을 수행합니다</span><span class="sxs-lookup"><span data-stu-id="75f48-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75f48-123">항상 hello를 사용 하는 것이 좋습니다. 최신 버전 tooremain Management Studio의 Azure 및 SQL 데이터베이스 업데이트 tooMicrosoft와 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-123">It is recommended that you always use hello latest version of Management Studio tooremain synchronized with updates tooMicrosoft Azure and SQL Database.</span></span> <span data-ttu-id="75f48-124">[SQL Server Management Studio를 업데이트합니다](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="75f48-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="75f48-125">새 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="75f48-125">Create new table</span></span>
<span data-ttu-id="75f48-126">SSMS 개체 탐색기 tooopen hello 쿼리 편집기에서 상황에 맞는 메뉴 항목 "새 시스템 버전 테이블"을 사용 하 여 임시 테이블 템플릿 스크립트를 다음 toopopulate hello 서식 파일 "값에 대 한 템플릿 매개 변수 지정" (Ctrl + Shift + M).</span><span class="sxs-lookup"><span data-stu-id="75f48-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer tooopen hello query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) toopopulate hello template:</span></span>

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="75f48-128">SSDT의 새 항목 toohello 데이터베이스 프로젝트를 추가할 때 "임시 테이블 (시스템 버전 관리)" 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items toohello database project.</span></span> <span data-ttu-id="75f48-129">됩니다 열고 테이블 디자이너를 사용 하도록 설정한 있습니다 tooeasily 지정 hello 표 레이아웃:</span><span class="sxs-lookup"><span data-stu-id="75f48-129">That will open table designer and enable you tooeasily specify hello table layout:</span></span>

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="75f48-131">수도 있습니다 임시 테이블 만들기를 직접 hello TRANSACT-SQL 문을 지정 하 여 아래 hello 예에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-131">You can also a create temporal table by specifying hello Transact-SQL statements directly, as shown in hello example below.</span></span> <span data-ttu-id="75f48-132">모든 임시 테이블의 필수 요소 hello 참고는 hello 기간을 정 및 hello SYSTEM_VERSIONING 절 기록 행 버전을 저장할 참조 tooanother 사용자 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-132">Note that hello mandatory elements of every temporal table are hello PERIOD definition and hello SYSTEM_VERSIONING clause with a reference tooanother user table that will store historical row versions:</span></span>

````
CREATE TABLE WebsiteUserInfo 
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED 
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL 
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
````

<span data-ttu-id="75f48-133">시스템 버전 임시 테이블을 만들 때 hello hello 기본 구성 가진 기록 테이블을 함께 제공 된 자동 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-133">When you create system-versioned temporal table, hello accompanying history table with hello default configuration is automatically created.</span></span> <span data-ttu-id="75f48-134">hello 기본 기록 테이블이 페이지 압축 사용 시 hello 기간 열 (끝, 시작)에 클러스터형된 B-트리 인덱스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-134">hello default history table contains a clustered B-tree index on hello period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="75f48-135">이 구성은 hello 대부분의 임시 테이블 사용 되는 시나리오에 가장 적합 한 특히 [데이터 감사](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0)합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-135">This configuration is optimal for hello majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="75f48-136">이 예에서 म 목표 tooperform 추세 시간 기반 분석 긴 데이터 기록을 통해 및 큰 데이터 집합을 hello 기록 테이블에 hello 저장소 옵션은 클러스터형된 columnstore 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-136">In this particular case, we aim tooperform time-based trend analysis over a longer data history and with bigger data sets, so hello storage choice for hello history table is a clustered columnstore index.</span></span> <span data-ttu-id="75f48-137">클러스터된 columnstore는 분석 쿼리를 훌륭하게 압축하고 좋은 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="75f48-138">유연성 tooconfigure hello 현재 및 임시 테이블의 인덱스를 완전히 독립적으로 hello 임시 테이블 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-138">Temporal Tables give you hello flexibility tooconfigure indexes on hello current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="75f48-139">Columnstore 인덱스는 hello premium 서비스 계층에서 사용할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-139">Columnstore indexes are only available in hello premium service tier.</span></span>
>

<span data-ttu-id="75f48-140">다음 스크립트는 hello 기록 테이블에서 기본 인덱스 변경 된 toohello 클러스터형 columnstore를 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-140">hello following script shows how default index on history table can be changed toohello clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="75f48-141">임시 테이블은 기록 테이블은 자식 노드로 표시 되는 동안 hello 쉽게 식별할 수 있도록에 대 한 특정 아이콘으로 hello 개체 탐색기에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-141">Temporal Tables are represented in hello Object Explorer with hello specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a><span data-ttu-id="75f48-143">기존 테이블 tootemporal alter</span><span class="sxs-lookup"><span data-stu-id="75f48-143">Alter existing table tootemporal</span></span>
<span data-ttu-id="75f48-144">Hello 대체 시나리오에는 hello WebsiteUserInfo 테이블 이미 있지만 디자인 된 tookeep 변경 기록이 없습니다에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-144">Let’s cover hello alternative scenario in which hello WebsiteUserInfo table already exists, but was not designed tookeep a history of changes.</span></span> <span data-ttu-id="75f48-145">이 경우 hello 기존 테이블 toobecome hello 다음 예제에서에서와 같이 임시 단순히 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-145">In this case, you can simply extend hello existing table toobecome temporal, as shown in hello following example:</span></span>

````
ALTER TABLE WebsiteUserInfo 
ADD 
    ValidFrom datetime2 (0) GENERATED ALWAYS AS ROW START HIDDEN  
        constraint DF_ValidFrom DEFAULT DATEADD(SECOND, -1, SYSUTCDATETIME())
    , ValidTo datetime2 (0)  GENERATED ALWAYS AS ROW END HIDDEN   
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo); 

ALTER TABLE WebsiteUserInfo  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="75f48-146">2단계: 정기적으로 워크로드 실행</span><span class="sxs-lookup"><span data-stu-id="75f48-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="75f48-147">임시 테이블의 주요 장점은 hello에는 하지 toochange 필요 하거나 않는 조정 된 방식으로 tooperform 변경 내용 추적에 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-147">hello main advantage of Temporal Tables is that you do not need toochange or adjust your website in any way tooperform change tracking.</span></span> <span data-ttu-id="75f48-148">임시 테이블은 한 번 만들면 데이터에 수정 작업을 수행할 때마다 이전 행 버전을 분명하게 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="75f48-149">이 특정 시나리오에 대 한 주문 tooleverage 변경 내용 자동 추적을 보겠습니다 방금 업데이트 열 **PagesVisited** 될 때마다 사용자 hello 웹 사이트에서 her/his 세션을 종료 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="75f48-149">In order tooleverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on hello website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="75f48-150">업데이트 쿼리 hello toonotice hello 실제 작업이 발생 했을 때 또는 나중에 분석에 대 한 기록 데이터는 유지 됩니다 방법 tooknow hello 정확한 시간 필요 하지 않은 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-150">It is important toonotice that hello update query doesn’t need tooknow hello exact time when hello actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="75f48-151">두 측면 hello Azure SQL 데이터베이스에서 자동으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-151">Both aspects are automatically handled by hello Azure SQL Database.</span></span> <span data-ttu-id="75f48-152">hello 다음 다이어그램에서는 모든 업데이트에서 기록 데이터가 생성 되는 방법</span><span class="sxs-lookup"><span data-stu-id="75f48-152">hello following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="75f48-154">3단계: 과거 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="75f48-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="75f48-155">이제 임시 시스템 버전 기능을 사용하는 경우 과거 데이터 분석은 하나의 쿼리만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="75f48-156">이 문서에서는 컴퓨터 이름은 toolearn-일반적인 분석 시나리오를 처리 하는 몇 가지 예가 모든 세부 정보를 제공를 hello에 도입 된 다양 한 옵션을 탐색 [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) 절.</span><span class="sxs-lookup"><span data-stu-id="75f48-156">In this article, we will provide a few examples that address common analysis scenarios - toolearn all details, explore various options introduced with hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="75f48-157">이 쿼리를 실행 하는 toosee hello 상위 10 명의 사용자가 시간 전, 기준으로 방문한 웹 페이지의 hello 수로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-157">toosee hello top 10 users ordered by hello number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="75f48-158">이 쿼리를 쉽게 수정할 수 있습니다 tooanalyze hello 사이트 방문 하루 전를 기준으로 한 달 전 또는 원하는 어느 시점에서 지난 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-158">You can easily modify this query tooanalyze hello site visits as of a day ago, a month ago or at any point in hello past you wish.</span></span>

<span data-ttu-id="75f48-159">tooperform hello에 대 한 기본 통계 분석 이전 날짜에는 다음 예제는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-159">tooperform basic statistical analysis for hello previous day, use hello following example:</span></span>

````
DECLARE @twoDaysAgo datetime2 = DATEADD(DAY, -2, SYSUTCDATETIME());
DECLARE @aDayAgo datetime2 = DATEADD(DAY, -1, SYSUTCDATETIME());

SELECT UserID, SUM (PagesVisited) as TotalVisitedPages, AVG (PagesVisited) as AverageVisitedPages,
MAX (PagesVisited) AS MaxVisitedPages, MIN (PagesVisited) AS MinVisitedPages,
STDEV (PagesVisited) as StDevViistedPages
FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME BETWEEN @twoDaysAgo AND @aDayAgo
GROUP BY UserId
````

<span data-ttu-id="75f48-160">일정 기간을 사용 하 여 hello CONTAINED IN 절 내에서 특정 사용자의 활동에 대 한 toosearch:</span><span class="sxs-lookup"><span data-stu-id="75f48-160">toosearch for activities of a specific user, within a period of time, use hello CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="75f48-161">그래픽 시각화는 경향과 사용 패턴을 직관적인 방식으로 손쉽게 표시할 수 있기에 임시 쿼리에 특히 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="75f48-163">테이블 스키마 진화</span><span class="sxs-lookup"><span data-stu-id="75f48-163">Evolving table schema</span></span>
<span data-ttu-id="75f48-164">일반적으로 응용 프로그램 개발을 수행 하는 동안 toochange hello 임시 테이블 스키마가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-164">Typically, you will need toochange hello temporal table schema while you are doing app development.</span></span> <span data-ttu-id="75f48-165">이 위해 일반 ALTER TABLE 문을 실행 하기만 하면 및 Azure SQL 데이터베이스 변경 내용을 toohello 기록 테이블을 적절 하 게 전파 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes toohello history table.</span></span> <span data-ttu-id="75f48-166">hello 다음 스크립트는 추적에 대 한 추가 특성을 추가 하는 방법</span><span class="sxs-lookup"><span data-stu-id="75f48-166">hello following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="75f48-167">마찬가지로 워크로드가 활성 상태인 동안 열 정의를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="75f48-168">마지막으로 더 이상 필요하지 않은 열을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="75f48-169">또는 사용 하 여 최신 [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) 연결된 toohello 데이터베이스 (온라인 모드) 상태일 때 또는 hello 데이터베이스 프로젝트 (오프 라인 모드)의 일부로 toochange 임시 테이블 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange temporal table schema while you are connected toohello database (online mode) or as part of hello database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="75f48-170">과거 데이터의 보존 제어</span><span class="sxs-lookup"><span data-stu-id="75f48-170">Controlling retention of historical data</span></span>
<span data-ttu-id="75f48-171">시스템 버전 임시 테이블 hello 기록 테이블에는 일반 테이블 보다 데이터베이스 크기 hello 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-171">With system-versioned temporal tables, hello history table may increase hello database size more than regular tables.</span></span> <span data-ttu-id="75f48-172">크기가 크고 점점 증가 기록 테이블 인해 toopure 저장소 비용이 부과 한 성능 세금 임시 쿼리에 대 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-172">A large and ever-growing history table can become an issue both due toopure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="75f48-173">따라서, hello 기록 테이블에서 데이터를 관리 하기 위한 데이터 보존 정책을 개발 계획 및 모든 임시 테이블의 hello 수명 주기 관리의 중요 한 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-173">Hence, developing a data retention policy for managing data in hello history table is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="75f48-174">Azure SQL 데이터베이스를 사용한 다음 hello 임시 테이블에서 기록 데이터를 관리 하기 위한 방법 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-174">With Azure SQL Database, you have hello following approaches for managing historical data in hello temporal table:</span></span>

* [<span data-ttu-id="75f48-175">테이블 분할</span><span class="sxs-lookup"><span data-stu-id="75f48-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="75f48-176">사용자 지정 정리 스크립트</span><span class="sxs-lookup"><span data-stu-id="75f48-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="75f48-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75f48-177">Next steps</span></span>
<span data-ttu-id="75f48-178">임시 테이블에서 자세한 내용은 [MSDN 설명서](https://msdn.microsoft.com/library/dn935015.aspx)를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="75f48-179">방문 Channel 9 toohear는 [실제 고객 임시 구현 성공 사례인](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) 및 조사식은 [임시 데모 라이브](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016)합니다.</span><span class="sxs-lookup"><span data-stu-id="75f48-179">Visit Channel 9 toohear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

