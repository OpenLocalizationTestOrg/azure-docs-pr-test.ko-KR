---
title: "SQL 데이터 웨어하우스를 사용 하 여 Power BI aaaUse | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스와 함께 Power BI 사용을 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="60518-103">SQL 데이터 웨어하우스와 함께 Power BI 사용</span><span class="sxs-lookup"><span data-stu-id="60518-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="60518-104">Azure SQL 데이터베이스와 마찬가지로 사용자 tooleverage 강력한 논리 푸시 다운 Power BI의 분석 기능 hello와 함께 통해 SQL 데이터 웨어하우스에 직접 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="60518-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user tooleverage powerful logical pushdown alongside hello analytical capabilities of Power BI.</span></span>  <span data-ttu-id="60518-105">직접 연결을 때 쿼리가 전송 됩니다 백 tooyour Azure SQL 데이터 웨어하우스를 실시간으로 hello 데이터를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="60518-105">With Direct Connect, queries are sent back tooyour Azure SQL Data Warehouse in real time as you explore hello data.</span></span>  <span data-ttu-id="60518-106">이 함께 SQL 데이터 웨어하우스를 통해 사용자의 hello 눈금 toocreate 동적 보고서까지 데이터를 상대로 몇 분 안에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60518-106">This, combined with hello scale of SQL Data Warehouse, enables users toocreate dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="60518-107">또한 Power BI 단추에 hello Open 도입 hello를 사용 하면 toodirectly Azure의 다른 부분에서 정보를 수집 하지 않고 Power BI tootheir SQL 데이터 웨어하우스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="60518-107">In addition, hello introduction of hello Open in Power BI button allows users toodirectly connect Power BI tootheir SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="60518-108">직접 연결을 사용하는 경우 다음을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="60518-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="60518-109">(자세한 내용은 아래 참조)을 연결 시 hello 정규화 된 서버 이름을 지정합니다</span><span class="sxs-lookup"><span data-stu-id="60518-109">Specify hello fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="60518-110">방화벽 규칙 hello 데이터베이스 구성에 대 한 너무 액세스 허용"tooAzure 서비스"를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="60518-110">Ensure firewall rules for hello database are configured too"Allow access tooAzure services".</span></span>
* <span data-ttu-id="60518-111">열 선택 또는 필터 추가 같은 모든 작업은 직접 hello 데이터 웨어하우스를 쿼리</span><span class="sxs-lookup"><span data-stu-id="60518-111">Every action such as selecting a column or adding a filter will  directly query hello data warehouse</span></span>
* <span data-ttu-id="60518-112">타일이 새로 고쳐집니다 약 15 분 간격 (새로 고침 예약 toobe를 필요 하지 않음)</span><span class="sxs-lookup"><span data-stu-id="60518-112">Tiles are refreshed approximately every 15 minutes (refresh does not need toobe scheduled)</span></span>
* <span data-ttu-id="60518-113">Q&A는 직접 연결 데이터 집합에 대해 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60518-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="60518-114">스키마 변경 내용은 자동으로 선택되지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60518-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="60518-115">모든 직접 연결 쿼리는 2분 후에 시간 초과됩니다.</span><span class="sxs-lookup"><span data-stu-id="60518-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="60518-116">이러한 제한 사항 및 참고 tooimprove hello 경험 진행 됨에 따라 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60518-116">These restrictions and notes may change as we continue tooimprove hello experiences.</span></span> <span data-ttu-id="60518-117">hello 단계 tooconnect 아래 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="60518-117">hello steps tooconnect are detailed below.</span></span>  

## <a name="using-hello-open-in-power-bi-button"></a><span data-ttu-id="60518-118">Hello 'Power BI에서 열기' 단추를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="60518-118">Using hello ‘Open in Power BI’ button</span></span>
<span data-ttu-id="60518-119">SQL 데이터 웨어하우스와 Power BI 간의 가장 쉬운 방법은 toomove hello Power BI 단추에 열기 hello에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60518-119">hello easiest way toomove between your SQL Data Warehouse and Power BI is with hello Open in Power BI button.</span></span> <span data-ttu-id="60518-120">이 단추를 사용 하면 tooseamlessly Power BI에서 새 대시보드 만들기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="60518-120">This button allows you tooseamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="60518-121">시작 tooget hello Azure 클래식 포털의에서 tooyour SQL 데이터 웨어하우스 인스턴스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="60518-121">tooget started navigate tooyour SQL Data Warehouse instance in hello Azure Classic Portal.</span></span>
2. <span data-ttu-id="60518-122">Hello 'Power BI에서 열기' 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="60518-122">Click hello 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="60518-123">Toosign 수 없는 경우에서 직접 또는 Power BI 계정이 없는 경우 toosign 옵트인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60518-123">If we are not able toosign you in directly, or if you do not have a Power BI account, you will need toosign-in.</span></span>  
4. <span data-ttu-id="60518-124">SQL 데이터 웨어하우스 연결 페이지에서 SQL 데이터 웨어하우스 로부터 hello 정보로 toohello 미리 데이터가 채워진 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60518-124">You will be directed toohello SQL Data Warehouse connection page, with hello information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="60518-125">자격 증명을 입력 한 후 완전히 연결 된 SQL 데이터 웨어하우스 tooyour 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60518-125">After entering your credentials you will be fully connected tooyour SQL Data Warehouse.</span></span>

## <a name="connecting-through-hello-power-bi-portal"></a><span data-ttu-id="60518-126">Hello Power BI 포털을 통해 연결</span><span class="sxs-lookup"><span data-stu-id="60518-126">Connecting through hello Power BI portal</span></span>
<span data-ttu-id="60518-127">Power BI 단추에 더하기 toousing hello Open, 사용자 Power BI 포털 hello를 통해 SQL 데이터 웨어하우스 tootheir를 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60518-127">In addition toousing hello Open in Power BI button, users can also connect tootheir SQL Data Warehouse through hello Power BI Portal.</span></span>

1. <span data-ttu-id="60518-128">Hello hello 탐색 창 맨 아래에 ' 데이터 가져오기 '를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="60518-128">Click 'Get Data' at hello bottom of hello navigation pane.</span></span>
2. <span data-ttu-id="60518-129">'데이터베이스'를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60518-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="60518-130">한 번 hello 데이터베이스 페이지에서 ' Azure SQL 데이터 웨어하우스 '를 선택 하 고 '연결'을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="60518-130">Once on hello Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="60518-131">Hello 필요한 연결 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="60518-131">Enter hello necessary connection information.</span></span>  <span data-ttu-id="60518-132">서버 이름과 데이터베이스 이름을 hello Azure 포털에서에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60518-132">Your server name and database name can be found in hello Azure Portal.</span></span>
5. <span data-ttu-id="60518-133">그러면 다시 연결 '데이터 집합' 아래에 새 항목을 설정한 후 및 Power BI의 기본 페이지 toohello 인스턴스 이름은 hello와 함께 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60518-133">You will be directed back toohello main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with hello name of your instance.</span></span>  
6. <span data-ttu-id="60518-134">새 데이터 집합 tooexplore hello 클릭할 수 있습니다 모든 hello 테이블 및 데이터베이스에 뷰가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60518-134">You can click on hello new dataset tooexplore all of hello tables and views in your database.</span></span> <span data-ttu-id="60518-135">열을 선택 하면 동적으로 시각 효과 만듭니다 쿼리 백 toohello 소스, 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="60518-135">Selecting a column will send a query back toohello source, dynamically creating your visual.</span></span> <span data-ttu-id="60518-136">이러한 시각 효과 새 보고서에 저장할 수 있습니다 및 tooyour 대시보드에 다시 고정할 합니다.</span><span class="sxs-lookup"><span data-stu-id="60518-136">These visuals can be saved in a new report and pinned back tooyour dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
