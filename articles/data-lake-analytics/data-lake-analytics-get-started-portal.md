---
title: "Azure 포털을 사용 하 여 Azure Data Lake 분석 시작 aaaGet | Microsoft Docs"
description: "Toouse hello Azure 포털 toocreate Data Lake 분석 계정 U SQL을 사용 하 여 데이터 레이크 분석 작업 만들기 하 고 hello 작업을 제출 하는 방법을 알아봅니다. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="0f0ad-103">Azure Portal을 사용하여 Azure Data Lake Analytics 시작</span><span class="sxs-lookup"><span data-stu-id="0f0ad-103">Get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="0f0ad-104">에 작업을 정의 어떻게 toouse hello Azure 포털 toocreate Azure Data Lake 분석 계정에 알아봅니다 [U-SQL](data-lake-analytics-u-sql-get-started.md), 및 toohello Data Lake 분석 서비스 작업을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-104">Learn how toouse hello Azure portal toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="0f0ad-105">데이터 레이크 분석에 대한 자세한 내용은 [Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f0ad-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0f0ad-106">Prerequisites</span></span>

<span data-ttu-id="0f0ad-107">이 자습서를 시작하기 전에 **Azure 구독**이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-107">Before you begin this tutorial, you must have an **Azure subscription**.</span></span> <span data-ttu-id="0f0ad-108">[Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="0f0ad-109">Data Lake 분석 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="0f0ad-109">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="0f0ad-110">이제 데이터 레이크 분석을 만들고 동일한 hello에 데이터 레이크 저장소 계정 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-110">Now, you will create a Data Lake Analytics and a Data Lake Store account at hello same time.</span></span>  <span data-ttu-id="0f0ad-111">이 단계는 간단 하 고 60 초 toofinish 초가 소요만 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-111">This step is simple and only takes about 60 seconds toofinish.</span></span>

1. <span data-ttu-id="0f0ad-112">Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-112">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0f0ad-113">**새로 만들기** >  **데이터 + 분석** > **Data Lake Analytics**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-113">Click **New** >  **Data + Analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="0f0ad-114">다음 항목 hello에 대 한 값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-114">Select values for hello following items:</span></span>
   * <span data-ttu-id="0f0ad-115">**이름**: Data Lake Analytics 계정의 이름을 지정합니다(소문자와 숫자만 허용).</span><span class="sxs-lookup"><span data-stu-id="0f0ad-115">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="0f0ad-116">**구독**: hello hello 분석 계정에 사용 되는 Azure 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-116">**Subscription**: Choose hello Azure subscription used for hello Analytics account.</span></span>
   * <span data-ttu-id="0f0ad-117">**리소스 그룹**.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-117">**Resource Group**.</span></span> <span data-ttu-id="0f0ad-118">기존 Azure 리소스 그룹을 선택하거나 리소스 그룹을 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-118">Select an existing Azure Resource Group or create a new one.</span></span>
   * <span data-ttu-id="0f0ad-119">**위치** -</span><span class="sxs-lookup"><span data-stu-id="0f0ad-119">**Location**.</span></span> <span data-ttu-id="0f0ad-120">Hello Data Lake 분석 계정에 대 한 Azure 데이터 센터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-120">Select an Azure data center for hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="0f0ad-121">**데이터 레이크 저장소**: hello 명령 toocreate 새 Data Lake 저장소 계정에 따라 하거나 기존 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-121">**Data Lake Store**: Follow hello instruction toocreate a new Data Lake Store account, or select an existing one.</span></span> 
4. <span data-ttu-id="0f0ad-122">필요에 따라 Data Lake Analytics 계정에 대한 가격 책정 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-122">Optionally, select a pricing tier for your Data Lake Analytics account.</span></span>
5. <span data-ttu-id="0f0ad-123">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-123">Click **Create**.</span></span> 


## <a name="your-first-u-sql-script"></a><span data-ttu-id="0f0ad-124">첫 번째 U-SQL 스크립트</span><span class="sxs-lookup"><span data-stu-id="0f0ad-124">Your first U-SQL script</span></span>

<span data-ttu-id="0f0ad-125">텍스트 다음 hello는 매우 간단한 U-SQL 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-125">hello following text is a very simple U-SQL script.</span></span> <span data-ttu-id="0f0ad-126">Hello 스크립트 내에서 작은 데이터 집합을 정의 하 고 다음 이라는 파일로 toohello 기본 데이터 레이크 저장소 아웃 해당 데이터 집합을 작성 하는 것이 전부 `/data.csv`합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-126">All it does is define a small dataset within hello script and then write that dataset out toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="0f0ad-127">U-SQL 작업 제출</span><span class="sxs-lookup"><span data-stu-id="0f0ad-127">Submit a U-SQL job</span></span>

1. <span data-ttu-id="0f0ad-128">Data Lake 분석 계정 hello에서 클릭 **새 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-128">From hello Data Lake Analytics account, click **New Job**.</span></span>
2. <span data-ttu-id="0f0ad-129">U-SQL 스크립트를 위에 표시 된 hello hello 텍스트에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-129">Paste in hello text of hello U-SQL script shown above.</span></span> 
3. <span data-ttu-id="0f0ad-130">**작업 제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-130">Click **Submit Job**.</span></span>   
4. <span data-ttu-id="0f0ad-131">너무 hello 작업 상태가 변경 될 때까지 기다렸다가**Succeeded**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-131">Wait until hello job status changes too**Succeeded**.</span></span>
5. <span data-ttu-id="0f0ad-132">Hello 작업에 실패 한 경우 참조 [모니터 데이터 레이크 분석 문제를 해결 하 고](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-132">If hello job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
6. <span data-ttu-id="0f0ad-133">Hello 클릭 **출력** 탭을 클릭 한 다음 `data.csv`합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-133">Click hello **Output** tab, and then click `data.csv`.</span></span> 

## <a name="see-also"></a><span data-ttu-id="0f0ad-134">참고 항목</span><span class="sxs-lookup"><span data-stu-id="0f0ad-134">See also</span></span>

* <span data-ttu-id="0f0ad-135">U-SQL 응용 프로그램 개발 시작 tooget 참조 [데이터 레이크 도구를 사용 하 여 Visual Studio에 대 한 개발 U-SQL 스크립트](data-lake-analytics-data-lake-tools-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-135">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="0f0ad-136">toolearn U SQL 참조 [Azure 데이터 레이크 분석 U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-136">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="0f0ad-137">관리 작업을 보려면 [Azure Portal을 사용하여 Azure Data Lake Analytics 관리](data-lake-analytics-manage-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f0ad-137">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
