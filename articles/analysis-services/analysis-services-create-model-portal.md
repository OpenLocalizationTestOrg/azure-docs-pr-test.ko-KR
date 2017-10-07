---
title: "hello Azure Analysis Services 웹 디자이너를 사용 하 여 테이블 형식 모델 aaaCreate | Microsoft Docs"
description: "Toocreate Azure Analysis Services 테이블 형식 모델 사용 하 여 Azure 포털에서 웹 디자이너 hello 하는 방법에 대해 알아봅니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a><span data-ttu-id="dbbd9-103">Azure Portal에서 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="dbbd9-103">Create a model in Azure portal</span></span>

<span data-ttu-id="dbbd9-104">Azure 포털의 hello Azure Analysis Services 웹 디자이너 (미리 보기) 기능 쉽고 빠르게 toocreate 제공 하 고 테이블 형식 모델 및 쿼리 모델 브라우저에서 직접 데이터를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-104">hello Azure Analysis Services web designer (preview) feature in Azure portal provides a quick and easy way toocreate and edit tabular models and query model data right in your browser.</span></span> 

<span data-ttu-id="dbbd9-105">염두에서에 둬야, hello 웹 디자이너는 **미리 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-105">Keep in mind, hello web designer is **preview**.</span></span> <span data-ttu-id="dbbd9-106">새로운 기능 미리 보기에서 모든 hello 시간을 추가 하는 기능이 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-106">While new functionality is being added all hello time, in preview, functionality is limited.</span></span> <span data-ttu-id="dbbd9-107">더 많은 고급 모델 개발 및 테스트에 대 한 최상의 toouse Visual Studio (SSDT) 및 SQL Server Management Studio (SSMS) 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-107">For more advanced model development and testing, it's best toouse Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbbd9-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dbbd9-108">Prerequisites</span></span>

- <span data-ttu-id="dbbd9-109">Hello Standard 또는 Developer 계층에서 사용 되는 Azure Analysis Services 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-109">An Azure Analysis Services server at hello Standard or Developer tier.</span></span> <span data-ttu-id="dbbd9-110">Hello 웹 디자이너를 사용 하 여 생성 하는 새 모델은 DirectQuery를 사용할 경우 이러한 계층 에서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-110">New models created by using hello Web designer are DirectQuery, supported only by these tiers.</span></span>
- <span data-ttu-id="dbbd9-111">데이터 원본으로 Azure SQL Database, Azure SQL Data Warehouse 또는 Power BI Desktop(.pbix) 파일.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-111">An Azure SQL Database, Azure SQL Data Warehouse, or Power BI Desktop (.pbix) file as a datasource.</span></span> <span data-ttu-id="dbbd9-112">Power BI Desktop 파일로 만드는 새 모델은 Azure SQL Database, Azure SQL Data Warehouse, Oracle 및 Teradata 데이터 원본을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-112">New models created from Power BI Desktop files support Azure SQL Database, Azure SQL Data Warehouse, Oracle, and Teradata data sources.</span></span>
- <span data-ttu-id="dbbd9-113">SQL Server 계정 및 tooAzure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스 데이터 원본에 연결 하기 위한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-113">A SQL Server account and password for connecting tooAzure SQL Database or Azure SQL Data Warehouse data sources.</span></span>

## <a name="toocreate-a-new-tabular-model"></a><span data-ttu-id="dbbd9-114">toocreate 새 테이블 형식 모델</span><span class="sxs-lookup"><span data-stu-id="dbbd9-114">toocreate a new tabular model</span></span>

1. <span data-ttu-id="dbbd9-115">서버의 **개요** 블레이드 > **웹 디자이너**에서 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-115">In your server's **Overview** blade > **Web designer**, click **Open**.</span></span>

    ![Azure Portal에서 모델 만들기](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. <span data-ttu-id="dbbd9-117">**웹 디자이너** > **모델**에서 **+ 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-117">In **Web designer** > **Models**, click **+ Add**.</span></span>

    ![Azure Portal에서 모델 만들기](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. <span data-ttu-id="dbbd9-119">**새 모델**에서 모델 이름을 입력한 다음 데이터 원본을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-119">In **New model**, type a model name, and then select a data source.</span></span>

    ![Azure Portal의 새 모델 대화 상자](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. <span data-ttu-id="dbbd9-121">**연결**, hello 연결 속성을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-121">In **Connect**, enter hello connection properties.</span></span> <span data-ttu-id="dbbd9-122">사용자 이름 및 암호는 SQL Server 계정이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-122">Username and password must be a SQL Server account.</span></span>

     ![Azure Portal의 연결 대화 상자](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. <span data-ttu-id="dbbd9-124">**테이블 및 뷰**hello 테이블 tooinclude에서 모델을 선택한 다음 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-124">In **Tables and views**, select hello tables tooinclude in your model, and then click **Create**.</span></span> <span data-ttu-id="dbbd9-125">키 쌍을 사용하여 테이블 간의 관계가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-125">Relationships are created automatically between tables with a key pair.</span></span>

     ![테이블 및 보기 선택](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

<span data-ttu-id="dbbd9-127">새 모델이 브라우저에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-127">Your new model appears in your browser.</span></span> <span data-ttu-id="dbbd9-128">여기서 다음과 같은 일을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-128">From here, you can:</span></span>   

- <span data-ttu-id="dbbd9-129">필드 toohello 쿼리 디자이너를 끌어서 필터를 추가 하 여 모델 데이터를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-129">Query model data by dragging fields toohello query designer and adding filters.</span></span>
- <span data-ttu-id="dbbd9-130">테이블에 새 측정값을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-130">Create new measures in tables.</span></span>
- <span data-ttu-id="dbbd9-131">Hello json 편집기를 사용 하 여 모델 메타 데이터를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-131">Edit model metadata by using hello json editor.</span></span>
- <span data-ttu-id="dbbd9-132">Visual Studio (SSDT), Power BI Desktop 또는 Excel에서 hello 모델을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-132">Open hello model in Visual Studio (SSDT), Power BI Desktop, or Excel.</span></span>

![테이블 및 보기 선택](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> <span data-ttu-id="dbbd9-134">모델 메타 데이터를 편집 하거나 브라우저에서 새 측정값을 만들 때 Azure에서 해당 변경 내용을 tooyour 모델을 저장 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-134">When you edit model metadata or create new measures in your browser, you're saving those changes tooyour model in Azure.</span></span> <span data-ttu-id="dbbd9-135">SSDT, Power BI Desktop 또는 Excel에서 모델을 작업하는 경우에도 모델이 동기화되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd9-135">If you're also working on your model in SSDT, Power BI Desktop, or Excel, your model can get out of sync.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dbbd9-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dbbd9-136">Next steps</span></span> 
[<span data-ttu-id="dbbd9-137">데이터베이스 역할 및 사용자 관리</span><span class="sxs-lookup"><span data-stu-id="dbbd9-137">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="dbbd9-138">Excel과 연결</span><span class="sxs-lookup"><span data-stu-id="dbbd9-138">Connect with Excel</span></span>](analysis-services-connect-excel.md)  


