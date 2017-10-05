---
title: "SQL Data Warehouse와 함께 Azure Stream Analytics 사용 | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스와 함께 Azure 스트림 분석 사용을 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 14783f0464764a11d7f03a5db1c2d63728a4cb50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="bdaa1-103">SQL 데이터 웨어하우스와 함께 Azure 스트림 분석 사용</span><span class="sxs-lookup"><span data-stu-id="bdaa1-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="bdaa1-104">Azure 스트림 분석은 완전히 관리되는 서비스로, 클라우드의 스트리밍 데이터에 대해 대기 시간이 짧고 확장성이 뛰어난 고가용성의 복합 이벤트 처리 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="bdaa1-105">[Azure Stream Analytics 소개][Introduction to Azure Stream Analytics]를 읽어 기본 사항을 배울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-105">You can learn the basics by reading [Introduction to Azure Stream Analytics][Introduction to Azure Stream Analytics].</span></span> <span data-ttu-id="bdaa1-106">[Azure Stream Analytics를 사용하여 시작][Get started using Azure Stream Analytics] 자습서에 따라 Stream Analytics로 종단간 솔루션을 만드는 방법에 대해 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-106">You can then learn how to create an end-to-end solution with Stream Analytics by following the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="bdaa1-107">이 문서에서 스크림 분석 작업에 대한 출력 싱크로 Azure SQL 데이터 웨어하우스 데이터베이스를 사용하는 방법에 대해 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-107">In this article, you will learn how to use your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdaa1-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="bdaa1-108">Prerequisites</span></span>
<span data-ttu-id="bdaa1-109">먼저, [Azure Stream Analytics를 사용하여 시작][Get started using Azure Stream Analytics] 자습서에서 다음 단계를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-109">First, run through the following steps in the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="bdaa1-110">이벤트 허브 입력 만들기</span><span class="sxs-lookup"><span data-stu-id="bdaa1-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="bdaa1-111">이벤트 생성기 응용 프로그램 구성 및 시작</span><span class="sxs-lookup"><span data-stu-id="bdaa1-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="bdaa1-112">스트림 분석 작업 프로비전</span><span class="sxs-lookup"><span data-stu-id="bdaa1-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="bdaa1-113">작업 입력 및 쿼리 지정</span><span class="sxs-lookup"><span data-stu-id="bdaa1-113">Specify job input and query</span></span>

<span data-ttu-id="bdaa1-114">그런 다음 SQL 데이터 웨어하우스 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="bdaa1-115">작업 출력 지정: Azure SQL 데이터 웨어하우스 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="bdaa1-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="bdaa1-116">1단계</span><span class="sxs-lookup"><span data-stu-id="bdaa1-116">Step 1</span></span>
<span data-ttu-id="bdaa1-117">Stream Analytics 작업에서 페이지 위쪽의 **출력**을 클릭한 다음 **출력 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-117">In your Stream Analytics job click **OUTPUT** from the top of the page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="bdaa1-118">2단계</span><span class="sxs-lookup"><span data-stu-id="bdaa1-118">Step 2</span></span>
<span data-ttu-id="bdaa1-119">SQL 데이터베이스를 선택하고 다음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="bdaa1-120">3단계</span><span class="sxs-lookup"><span data-stu-id="bdaa1-120">Step 3</span></span>
<span data-ttu-id="bdaa1-121">다음 페이지에 다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-121">Enter the following values on the next page:</span></span>

* <span data-ttu-id="bdaa1-122">*출력 별칭*: 이 작업 출력의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="bdaa1-123">*구독*:</span><span class="sxs-lookup"><span data-stu-id="bdaa1-123">*Subscription*:</span></span>
  * <span data-ttu-id="bdaa1-124">SQL 데이터 웨어하우스가 스트림 분석 작업과 동일한 구독 내에 있는 경우 현재 구독에서 SQL 데이터베이스 사용을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-124">If your SQL Data Warehouse database is in the same subscription as the Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="bdaa1-125">데이터베이스가 다른 구독에 있는 경우 다른 구독에서 SQL 데이터베이스 사용을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="bdaa1-126">*데이터베이스*: 대상 데이터베이스의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-126">*Database*: Specify the name of a destination database.</span></span>
* <span data-ttu-id="bdaa1-127">*서버 이름*: 방금 지정한 데이터베이스에 대한 서버 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-127">*Server Name*: Specify the server name for the database you just specified.</span></span> <span data-ttu-id="bdaa1-128">Azure 클래식 포털을 사용하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-128">You can use the Azure Classic Portal to find this.</span></span>

![][server-name]

* <span data-ttu-id="bdaa1-129">*사용자 이름*: 데이터베이스에 대한 쓰기 권한이 있는 계정의 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-129">*User Name*: Specify the user name of an account that has write permissions for the database.</span></span>
* <span data-ttu-id="bdaa1-130">*암호*: 지정된 사용자 계정에 대한 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-130">*Password*: Provide the password for the specified user account.</span></span>
* <span data-ttu-id="bdaa1-131">*테이블*: 데이터베이스에서 대상 테이블의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-131">*Table*: Specify the name of the target table in the database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="bdaa1-132">4단계</span><span class="sxs-lookup"><span data-stu-id="bdaa1-132">Step 4</span></span>
<span data-ttu-id="bdaa1-133">확인 단추를 클릭하여 이 작업 출력을 추가하고 스트림 분석이 데이터베이스에 성공적으로 연결될 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-133">Click the check button to add this job output and to verify that Stream Analytics can successfully connect to the database.</span></span>

![][test-connection]

<span data-ttu-id="bdaa1-134">데이터베이스에 대한 연결이 성공하면 포털의 맨 아래에 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-134">When the connection to the database succeeds, you will see a notification at the bottom of the portal.</span></span> <span data-ttu-id="bdaa1-135">아래의 연결 테스트를 클릭하여 데이터베이스에 대한 연결을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-135">You can click Test Connection at the bottom to test the connection to the database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdaa1-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bdaa1-136">Next steps</span></span>
<span data-ttu-id="bdaa1-137">통합 개요는 [SQL Data Warehouse 통합 개요][SQL Data Warehouse integration overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="bdaa1-138">더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bdaa1-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction to Azure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
