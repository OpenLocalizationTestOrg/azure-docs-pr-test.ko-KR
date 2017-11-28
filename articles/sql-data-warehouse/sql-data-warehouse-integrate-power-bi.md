---
title: "SQL Data Warehouse와 함께 Power BI 사용 | Microsoft Docs"
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
ms.openlocfilehash: 4b7609fc5d6ce7bf0e3bd3ebf6d8f52e93a40a75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="6e8f2-103">SQL 데이터 웨어하우스와 함께 Power BI 사용</span><span class="sxs-lookup"><span data-stu-id="6e8f2-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="6e8f2-104">Azure SQL 데이터베이스와 함께, SQL 데이터 웨어하우스 직접 연결을 사용하면 사용자는 Power BI의 분석 기능과 함께 강력한 논리 푸시 다운을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user to leverage powerful logical pushdown alongside the analytical capabilities of Power BI.</span></span>  <span data-ttu-id="6e8f2-105">직접 연결을 사용하여 쿼리는 데이터를 탐색할 때 실시간으로 Azure SQL 데이터 웨어하우스로 다시 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-105">With Direct Connect, queries are sent back to your Azure SQL Data Warehouse in real time as you explore the data.</span></span>  <span data-ttu-id="6e8f2-106">SQL 데이터 웨어하우스의 크기와 결합되어 사용자는 테라바이트 규모의 데이터에 대해 동적 보고서를 몇 분 내에 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-106">This, combined with the scale of SQL Data Warehouse, enables users to create dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="6e8f2-107">또한 Power BI 단추에서 열기 소개를 사용하면 사용자는 Azure의 다른 부분에서 정보를 수집하지 않고 Power BI를 직접 SQL 데이터 웨어하우스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-107">In addition, the introduction of the Open in Power BI button allows users to directly connect Power BI to their SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="6e8f2-108">직접 연결을 사용하는 경우 다음을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="6e8f2-109">연결할 때 정규화된 서버 이름을 지정합니다(자세한 내용은 아래 참조).</span><span class="sxs-lookup"><span data-stu-id="6e8f2-109">Specify the fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="6e8f2-110">데이터베이스에 대한 방화벽 규칙은 "Azure 서비스에 액세스 허용"으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-110">Ensure firewall rules for the database are configured to "Allow access to Azure services".</span></span>
* <span data-ttu-id="6e8f2-111">열 선택 또는 필터 추가와 같은 모든 작업은 데이터 웨어하우스에 직접 쿼리됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-111">Every action such as selecting a column or adding a filter will  directly query the data warehouse</span></span>
* <span data-ttu-id="6e8f2-112">타일은 약 15분 마다 새로 고쳐집니다(새로 고침은 예약하지 않아도 됨).</span><span class="sxs-lookup"><span data-stu-id="6e8f2-112">Tiles are refreshed approximately every 15 minutes (refresh does not need to be scheduled)</span></span>
* <span data-ttu-id="6e8f2-113">Q&A는 직접 연결 데이터 집합에 대해 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="6e8f2-114">스키마 변경 내용은 자동으로 선택되지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="6e8f2-115">모든 직접 연결 쿼리는 2분 후에 시간 초과됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="6e8f2-116">계속 환경이 개선되면서 이 제한 사항 및 참고 사항은 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-116">These restrictions and notes may change as we continue to improve the experiences.</span></span> <span data-ttu-id="6e8f2-117">연결 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-117">The steps to connect are detailed below.</span></span>  

## <a name="using-the-open-in-power-bi-button"></a><span data-ttu-id="6e8f2-118">'Power BI에서 열기' 단추 사용</span><span class="sxs-lookup"><span data-stu-id="6e8f2-118">Using the ‘Open in Power BI’ button</span></span>
<span data-ttu-id="6e8f2-119">SQL 데이터 웨어하우스와 Power BI 간에 이동 하는 가장 쉬운 방법은 Power BI에서 열기 단추를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-119">The easiest way to move between your SQL Data Warehouse and Power BI is with the Open in Power BI button.</span></span> <span data-ttu-id="6e8f2-120">이 단추를 사용하면 원활하게 Power BI에서 새 대시보드 만들기를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-120">This button allows you to seamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="6e8f2-121">시작하려면 Azure 클래식 포털에서 SQL 데이터 웨어하우스 인스턴스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-121">To get started navigate to your SQL Data Warehouse instance in the Azure Classic Portal.</span></span>
2. <span data-ttu-id="6e8f2-122">'Power BI에서 열기' 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-122">Click the 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="6e8f2-123">직접 로그인 할 수 없거나 Power BI 계정이 없는 경우 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-123">If we are not able to sign you in directly, or if you do not have a Power BI account, you will need to sign-in.</span></span>  
4. <span data-ttu-id="6e8f2-124">미리 완성된 SQL 데이터 웨어하우스의 정보를 사용하여 SQL 데이터 웨어하우스 연결 페이지로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-124">You will be directed to the SQL Data Warehouse connection page, with the information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="6e8f2-125">자격 증명을 입력하면, SQL 데이터 웨어하우스에 완전히 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-125">After entering your credentials you will be fully connected to your SQL Data Warehouse.</span></span>

## <a name="connecting-through-the-power-bi-portal"></a><span data-ttu-id="6e8f2-126">Power BI 포털을 통해 연결</span><span class="sxs-lookup"><span data-stu-id="6e8f2-126">Connecting through the Power BI portal</span></span>
<span data-ttu-id="6e8f2-127">Power BI에서 열기 단추를 사용 하는 것 외에도 사용자는 Power BI 포털을 통해 해당 SQL 데이터 웨어하우스에 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-127">In addition to using the Open in Power BI button, users can also connect to their SQL Data Warehouse through the Power BI Portal.</span></span>

1. <span data-ttu-id="6e8f2-128">탐색 창의 맨 아래에서 '데이터 가져오기'를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-128">Click 'Get Data' at the bottom of the navigation pane.</span></span>
2. <span data-ttu-id="6e8f2-129">'데이터베이스'를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="6e8f2-130">데이터베이스 페이지에서 'Azure SQL 데이터 웨어하우스'를 선택하고 '연결'을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-130">Once on the Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="6e8f2-131">필요한 연결 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-131">Enter the necessary connection information.</span></span>  <span data-ttu-id="6e8f2-132">서버 이름과 데이터베이스 이름을 Azure 포털에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-132">Your server name and database name can be found in the Azure Portal.</span></span>
5. <span data-ttu-id="6e8f2-133">Power BI의 기본 페이지로 리디렉션되며, 연결된 후 '데이터 집합' 아래에 해당 인스턴스 이름의 새 항목이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-133">You will be directed back to the main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with the name of your instance.</span></span>  
6. <span data-ttu-id="6e8f2-134">새 데이터 집합을 클릭하여 데이터베이스의 모든 테이블 및 뷰를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-134">You can click on the new dataset to explore all of the tables and views in your database.</span></span> <span data-ttu-id="6e8f2-135">열을 선택하면 소스에 다시 쿼리를 전송하여 비주얼을 동적으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-135">Selecting a column will send a query back to the source, dynamically creating your visual.</span></span> <span data-ttu-id="6e8f2-136">이 비주얼은 새 보고서에 저장되며 대시보드로 다시 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8f2-136">These visuals can be saved in a new report and pinned back to your dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
