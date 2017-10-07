---
title: "aaaSQL 서버 저장 프로시저 작업"
description: "SQL Server 저장 프로시저 작업 tooinvoke hello 데이터 팩토리 파이프라인에서 Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스 저장된 프로시저를 사용 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="255e8-103">SQL Server 저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="255e8-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="255e8-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="255e8-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="255e8-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="255e8-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="255e8-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="255e8-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="255e8-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="255e8-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="255e8-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="255e8-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="255e8-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="255e8-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="255e8-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="255e8-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="255e8-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="255e8-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="255e8-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="255e8-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="255e8-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="255e8-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="255e8-114">개요</span><span class="sxs-lookup"><span data-stu-id="255e8-114">Overview</span></span>
<span data-ttu-id="255e8-115">데이터 변환 작업을 사용 하 여 데이터 팩터리에서 [파이프라인](data-factory-create-pipelines.md) 예측 및 통찰력으로 원시 데이터 tootransform 및 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) tootransform and process raw data into predictions and insights.</span></span> <span data-ttu-id="255e8-116">hello 저장 프로시저 작업은 데이터 팩터리의 지원 hello 변환 활동 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-116">hello Stored Procedure Activity is one of hello transformation activities that Data Factory supports.</span></span> <span data-ttu-id="255e8-117">Hello를 기반으로 한이 문서 [데이터 변환 작업](data-factory-data-transformation-activities.md) 문서 데이터 변환 및 데이터 팩터리의 지원 hello 변환 작업에 대 한 일반적인 개요를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="255e8-118">기업에서 또는 Azure 가상 컴퓨터 (VM)에 같은 데이터가 hello 중 하나에 있는 저장된 프로시저를 저장 하는 hello 저장 프로시저 작업 tooinvoke를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-118">You can use hello Stored Procedure Activity tooinvoke a stored procedure in one of hello following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="255e8-119">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="255e8-119">Azure SQL Database</span></span>
- <span data-ttu-id="255e8-120">Azure SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="255e8-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="255e8-121">SQL Server 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="255e8-121">SQL Server Database.</span></span>  <span data-ttu-id="255e8-122">SQL Server를 사용 하는 경우 hello 호스트 데이터베이스 hello 또는 access toohello 데이터베이스 있는 별도 컴퓨터에서 동일한 컴퓨터에 데이터 관리 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-122">If you are using SQL Server, install Data Management Gateway on hello same machine that hosts hello database or on a separate machine that has access toohello database.</span></span> <span data-ttu-id="255e8-123">데이터 관리 게이트웨이는 온-프레미스/Azure VM에서 데이터 원본을 Cloud Services에 안전하고 관리되는 방식으로 연결하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="255e8-124">자세한 내용은 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="255e8-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="255e8-125">Azure SQL 데이터베이스 또는 SQL Server에 데이터를 복사할 때 hello를 구성할 수 있습니다 **SqlSink** 복사 활동 tooinvoke hello를 사용 하 여 저장된 프로시저에서에서 **sqlWriterStoredProcedureName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-125">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="255e8-126">자세한 내용은 [복사 작업에서 저장 프로시저 호출](data-factory-invoke-stored-procedure-from-copy-activity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="255e8-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="255e8-127">Hello 속성에 대 한 자세한 커넥터 문서를 다음을 참조: [Azure SQL 데이터베이스](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-127">For details about hello property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="255e8-128">복사 작업을 사용하여 Azure SQL Data Warehouse로 데이터를 복사하는 동안 저장 프로시저를 호출하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="255e8-129">그러나 SQL 데이터 웨어하우스에 hello 저장 프로시저 활동 tooinvoke 저장된 프로시저를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-129">But, you can use hello stored procedure activity tooinvoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="255e8-130">Azure SQL 데이터 웨어하우스 또는 SQL Server 나 Azure SQL 데이터베이스에서 데이터를 복사할 때 구성할 수 있습니다 **SqlSource** 복사 활동 tooinvoke hello를 사용 하 여 hello 원본 데이터베이스에서 저장된 프로시저 tooread 데이터에서에서  **sqlReaderStoredProcedureName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="255e8-131">자세한 내용은 hello 다음 커넥터 문서를 참조 하세요.: [Azure SQL 데이터베이스](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL 데이터 웨어하우스](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="255e8-131">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="255e8-132">연습에서는 다음 hello 파이프라인 tooinvoke Azure SQL 데이터베이스의 저장된 프로시저에서에서 저장 프로시저 작업 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-132">hello following walkthrough uses hello Stored Procedure Activity in a pipeline tooinvoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="255e8-133">연습</span><span class="sxs-lookup"><span data-stu-id="255e8-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="255e8-134">샘플 테이블 및 저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="255e8-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="255e8-135">Hello 다음 만들기 **테이블** SQL Server Management Studio 또는 다른 익숙한 도구를 사용 하 여 Azure SQL 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-135">Create hello following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="255e8-136">hello datetimestamp 열은 hello 날짜 및 시간을 해당 하는 hello ID 생성 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="255e8-136">hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    <span data-ttu-id="255e8-137">Id는 hello 고유한 식별 하 고 hello datetimestamp 열은 hello 날짜 및 시간 hello 해당 ID가 생성 되는 경우 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-137">Id is hello unique identified and hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>
    
    ![샘플 데이터](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="255e8-139">이 샘플에서는 Azure SQL 데이터베이스에서 hello 저장 프로시저는입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-139">In this sample, hello stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="255e8-140">Hello 저장된 프로시저에 있으면 Azure SQL 데이터 웨어하우스 및 SQL Server 데이터베이스, hello 방법은 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-140">If hello stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, hello approach is similar.</span></span> <span data-ttu-id="255e8-141">SQL Server Database의 경우 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="255e8-142">Hello 다음 만들기 **저장 프로시저** toohello에 데이터를 삽입 하는 **하세요**합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-142">Create hello following **stored procedure** that inserts data in toohello **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="255e8-143">**이름** 및 **대/소문자** hello의 매개 변수 (이 예제의 DateTime)와 일치 해야 hello 파이프라인/활동 JSON에에서 지정 된 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-143">**Name** and **casing** of hello parameter (DateTime in this example) must match that of parameter specified in hello pipeline/activity JSON.</span></span> <span data-ttu-id="255e8-144">저장된 프로시저 정의 hello 하 되도록  **@**  hello 매개 변수에 대 한 접두사로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-144">In hello stored procedure definition, ensure that **@** is used as a prefix for hello parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="255e8-145">데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-145">Create a data factory</span></span>
1. <span data-ttu-id="255e8-146">로그 너무[Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-146">Log in too[Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="255e8-147">클릭 **새로** hello 왼쪽된 메뉴를 클릭 **인텔리전스 + 분석**를 클릭 하 고 **Data Factory**합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-147">Click **NEW** on hello left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![새 data factory](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="255e8-149">Hello에 **새 데이터 팩터리** 블레이드에서 입력 **SProcDF** hello 이름에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-149">In hello **New data factory** blade, enter **SProcDF** for hello Name.</span></span> <span data-ttu-id="255e8-150">Azure Data Factory 이름은 **전역적으로 고유**합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="255e8-151">해당 이름의 hello 팩터리의 tooenable hello 성공적으로 만드는 hello 데이터 팩터리의 tooprefix hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-151">You need tooprefix hello name of hello data factory with your name, tooenable hello successful creation of hello factory.</span></span>

   ![새 data factory](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="255e8-153">Azure **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="255e8-154">에 대 한 **리소스 그룹**, hello 다음 단계 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-154">For **Resource Group**, do one of hello following steps:</span></span>
   1. <span data-ttu-id="255e8-155">클릭 **새로 만들기** hello 리소스 그룹에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-155">Click **Create new** and enter a name for hello resource group.</span></span>
   2. <span data-ttu-id="255e8-156">**기존 항목 사용**을 클릭하고 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="255e8-157">선택 hello **위치** hello 데이터 팩토리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-157">Select hello **location** for hello data factory.</span></span>
7. <span data-ttu-id="255e8-158">선택 **Pin toodashboard** 다음에 로그인 할 때 hello 대시보드에서 hello 데이터 팩터리를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-158">Select **Pin toodashboard** so that you can see hello data factory on hello dashboard next time you log in.</span></span>
8. <span data-ttu-id="255e8-159">클릭 **만들기** hello에 **새 데이터 팩터리** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-159">Click **Create** on hello **New data factory** blade.</span></span>
9. <span data-ttu-id="255e8-160">Hello에 생성 되 고 hello 데이터 팩터리 참조 **대시보드** hello Azure 포털의.</span><span class="sxs-lookup"><span data-stu-id="255e8-160">You see hello data factory being created in hello **dashboard** of hello Azure portal.</span></span> <span data-ttu-id="255e8-161">보여 주는 hello 데이터 팩터리 페이지를 참조 하는 hello 데이터 팩터리에서 만들어진 후에 성공적으로, hello 데이터 팩터리의 내용을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-161">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![Data Factory 홈페이지](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="255e8-163">Azure SQL 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="255e8-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="255e8-164">Hello 데이터 팩터리를 만든 후 hello 하세요 테이블 및 sp_sample 저장 프로시저, tooyour 데이터 팩터리를 포함 하 여 Azure SQL 데이터베이스를 연결 하는 Azure SQL 연결 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-164">After creating hello data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains hello sampletable table and sp_sample stored procedure, tooyour data factory.</span></span>

1. <span data-ttu-id="255e8-165">클릭 **작성자 및 배포** hello에 **Data Factory** 블레이드 **SProcDF** toolaunch hello 데이터 팩터리 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-165">Click **Author and deploy** on hello **Data Factory** blade for **SProcDF** toolaunch hello Data Factory Editor.</span></span>
2. <span data-ttu-id="255e8-166">클릭 **새 데이터 저장소** 명령 모음 hello 되 고 선택 **Azure SQL 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-166">Click **New data store** on hello command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="255e8-167">Hello Azure SQL을 만들기 위한 JSON 스크립트는 연결 된 서비스 hello 편집기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-167">You should see hello JSON script for creating an Azure SQL linked service in hello editor.</span></span>

   ![새 데이터 저장소](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="255e8-169">Hello JSON 스크립트에서에서 변경 내용을 따라 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-169">In hello JSON script, make hello following changes:</span></span>

   1. <span data-ttu-id="255e8-170">대체 `<servername>` hello Azure SQL 데이터베이스 서버 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-170">Replace `<servername>` with hello name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="255e8-171">대체 `<databasename>` hello 데이터베이스를 만든 hello 테이블과 hello와 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-171">Replace `<databasename>` with hello database in which you created hello table and hello stored procedure.</span></span>
   3. <span data-ttu-id="255e8-172">대체 `<username@servername>` toohello 데이터베이스 액세스를 가진 hello 사용자 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-172">Replace `<username@servername>` with hello user account that has access toohello database.</span></span>
   4. <span data-ttu-id="255e8-173">대체 `<password>` hello hello 사용자 계정의 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-173">Replace `<password>` with hello password for hello user account.</span></span>

      ![새 데이터 저장소](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="255e8-175">toodeploy hello 연결 된 서비스를 클릭 **배포** hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-175">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="255e8-176">Hello 왼쪽에서 볼 hello 트리에서 hello AzureSqlLinkedService 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-176">Confirm that you see hello AzureSqlLinkedService in hello tree view on hello left.</span></span>

    ![연결된 서비스와 트리 뷰](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="255e8-178">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="255e8-178">Create an output dataset</span></span>
<span data-ttu-id="255e8-179">저장된 프로시저 활동에 대 한 출력 데이터 집합 저장 프로시저를 hello 하는 경우에 생성 하지 않으므로 모든 데이터를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-179">You must specify an output dataset for a stored procedure activity even if hello stored procedure does not produce any data.</span></span> <span data-ttu-id="255e8-180">hello 출력 hello 활동 (얼마나 자주 hello 활동 실행-매시간, 매일, 등)의 일정을 hello를 구동 하는 데이터 집합 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-180">That's because it's hello output dataset that drives hello schedule of hello activity (how often hello activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="255e8-181">hello 출력 데이터 집합 사용 해야 합니다는 **연결 된 서비스** tooan Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스 또는 저장된 프로시저 toorun hello 하려는 SQL Server 데이터베이스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-181">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="255e8-182">hello 출력 데이터 집합으로 사용할 수는 방식으로 toopass hello 결과 후속 처리에 대 한 hello 저장 프로시저의 다른 활동에 의해 ([활동 체인](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) hello 파이프라인에서.</span><span class="sxs-lookup"><span data-stu-id="255e8-182">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="255e8-183">그러나 데이터 팩터리는 저장된 프로시저 toothis 데이터 집합의 hello 출력을 자동으로 기록 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-183">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="255e8-184">Hello 저장 프로시저 출력 데이터 집합 가리키는 hello 해당 쓰기 tooa SQL 테이블 이며</span><span class="sxs-lookup"><span data-stu-id="255e8-184">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="255e8-185">경우에 따라 hello 출력 데이터 집합 수는 **더미 데이터 집합** (hello의 출력을 실제로 포함 되지 않는 tooa 테이블을 가리키는 데이터 집합 저장 프로시저).</span><span class="sxs-lookup"><span data-stu-id="255e8-185">In some cases, hello output dataset can be a **dummy dataset** (a dataset that points tooa table that does not really hold output of hello stored procedure).</span></span> <span data-ttu-id="255e8-186">이 더미 데이터 집합 저장 프로시저 작업 hello를 실행 하기 위한 toospecify hello 일정만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-186">This dummy dataset is used only toospecify hello schedule for running hello stored procedure activity.</span></span> 

1. <span data-ttu-id="255e8-187">도구 모음에서 **... 더 많은** hello 도구 모음에서 **새 데이터 집합**를 클릭 하 고 **Azure SQL**합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-187">Click **... More** on hello toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="255e8-188">**새 데이터 집합** hello 명령 모음 및 선택에 **Azure SQL**합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-188">**New dataset** on hello command bar and select **Azure SQL**.</span></span>

    ![연결된 서비스와 트리 뷰](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="255e8-190">복사/붙여넣기 hello toohello JSON 편집기에서 JSON 스크립트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-190">Copy/paste hello following JSON script in toohello JSON editor.</span></span>

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="255e8-191">toodeploy hello 데이터 집합, 클릭 **배포** hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-191">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="255e8-192">Hello 트리 뷰에서 hello 데이터 집합에 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-192">Confirm that you see hello dataset in hello tree view.</span></span>

    ![연결된 서비스와 트리 뷰](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="255e8-194">SqlServerStoredProcedure 작업을 사용하여 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="255e8-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="255e8-195">이제 저장 프로시저 작업을 사용하여 파이프라인 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="255e8-196">Hello 다음과 같은 속성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-196">Notice hello following properties:</span></span> 

- <span data-ttu-id="255e8-197">hello **형식** 너무 속성이**SqlServerStoredProcedure**합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-197">hello **type** property is set too**SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="255e8-198">hello **storedProcedureName** 속성이 너무 설정 글꼴로**sp_sample** (저장 프로시저 hello의 이름).</span><span class="sxs-lookup"><span data-stu-id="255e8-198">hello **storedProcedureName** in type properties is set too**sp_sample** (name of hello stored procedure).</span></span>
- <span data-ttu-id="255e8-199">hello **storedProcedureParameters** 라는 하나의 매개 변수를 포함 하는 섹션 **DataTime**합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-199">hello **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="255e8-200">Hello 이름과 대/소문자 hello 저장 프로시저 정의에 hello 매개 변수의 이름 및 JSON의 hello 매개 변수는 대/소문자 구분 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-200">Name and casing of hello parameter in JSON must match hello name and casing of hello parameter in hello stored procedure definition.</span></span> <span data-ttu-id="255e8-201">매개 변수에 대해 null을 전달 해야 hello 구문을 사용 하 여: `"param1": null` (모두 소문자).</span><span class="sxs-lookup"><span data-stu-id="255e8-201">If you need pass null for a parameter, use hello syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="255e8-202">도구 모음에서 **... 더 많은** 명령 모음 hello 되 고 클릭 **새 파이프라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-202">Click **... More** on hello command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="255e8-203">다음 JSON 코드 조각은 복사/붙여넣기 hello:</span><span class="sxs-lookup"><span data-stu-id="255e8-203">Copy/paste hello following JSON snippet:</span></span>   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. <span data-ttu-id="255e8-204">toodeploy hello 파이프라인 클릭 **배포** hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-204">toodeploy hello pipeline, click **Deploy** on hello toolbar.</span></span>  

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="255e8-205">모니터 hello 파이프라인</span><span class="sxs-lookup"><span data-stu-id="255e8-205">Monitor hello pipeline</span></span>
1. <span data-ttu-id="255e8-206">클릭 **X** tooclose 데이터 팩터리 편집기 블레이드를 toonavigate toohello Data Factory 블레이드를 다시 마우스 클릭 **다이어그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-206">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![다이어그램 타일](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="255e8-208">Hello에 **다이어그램 보기**를 hello 파이프라인에 대 한 개요를 확인 하 고 데이터 집합에 사용 되는이 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-208">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![다이어그램 타일](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="255e8-210">다이어그램 보기 hello에서 hello 데이터 집합을 두 번 클릭 `sprocsampleout`합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-210">In hello Diagram View, double-click hello dataset `sprocsampleout`.</span></span> <span data-ttu-id="255e8-211">준비 상태에서 hello 조각이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-211">You see hello slices in Ready state.</span></span> <span data-ttu-id="255e8-212">조각이 hello 시작 시간과 종료 시간 hello JSON에서에서 사이의 각 시간에 대해 생성 되 있으므로 5 개의 분할 영역 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-212">There should be five slices because a slice is produced for each hour between hello start time and end time from hello JSON.</span></span>

    ![다이어그램 타일](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="255e8-214">이 분할 영역에 있을 때 **준비** 실행 상태는 `select * from sampletable` 데이터 hello hello Azure SQL 데이터베이스 tooverify에 대 한 쿼리를 hello 저장 프로시저를 통해 toohello 테이블에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-214">When a slice is in **Ready** state, run a `select * from sampletable` query against hello Azure SQL database tooverify that hello data was inserted in toohello table by hello stored procedure.</span></span>

   ![출력 데이터](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="255e8-216">참조 [모니터 hello 파이프라인](data-factory-monitor-manage-pipelines.md) Azure 데이터 팩터리 파이프라인을 모니터링 하는 방법에 대 한 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-216">See [Monitor hello pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="255e8-217">입력 데이터 집합 지정</span><span class="sxs-lookup"><span data-stu-id="255e8-217">Specify an input dataset</span></span>
<span data-ttu-id="255e8-218">Hello 연습에서는 저장된 프로시저 작업 모든 입력된 데이터 집합이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-218">In hello walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="255e8-219">입력된 데이터 집합을 지정 하면 hello 저장된 프로시저 작업까지 실행 되지 않습니다 (준비 상태)에서 입력된 데이터 집합의 조각을 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-219">If you specify an input dataset, hello stored procedure activity does not run until hello slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="255e8-220">hello 데이터 집합에는 외부 데이터 집합 수 (hello에 다른 활동에 의해 생성 되지 않습니다 동일한 파이프라인) 또는 업스트림 활동 (이 작업 이전에 실행 되 hello 활동)에서 생성 하는 내부 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-220">hello dataset can be an external dataset (that is not produced by another activity in hello same pipeline) or an internal dataset that is produced by an upstream activity (hello activity that runs before this activity).</span></span> <span data-ttu-id="255e8-221">Hello 저장 프로시저 작업에 대 한 여러 입력된 데이터 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-221">You can specify multiple input datasets for hello stored procedure activity.</span></span> <span data-ttu-id="255e8-222">이렇게 하면 hello 저장된 프로시저 작업 실행 모든 hello에 대 한 입력된 데이터 집합 분할 영역을 사용할 수 (준비 상태) 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-222">If you do so, hello stored procedure activity runs only when all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="255e8-223">hello 입력된 데이터 집합 매개 변수로 hello 저장 프로시저에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-223">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="255e8-224">시작 hello 저장 프로시저 작업 전에 것만 사용 되는 toocheck hello 종속성 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-224">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="255e8-225">다른 작업과 연결</span><span class="sxs-lookup"><span data-stu-id="255e8-225">Chaining with other activities</span></span>
<span data-ttu-id="255e8-226">Toochain는 업스트림 활동과이 활동을 사용 하도록 하려는 경우이 활동의 입력으로 hello 업스트림 활동의 hello 출력을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-226">If you want toochain an upstream activity with this activity, specify hello output of hello upstream activity as an input of this activity.</span></span> <span data-ttu-id="255e8-227">이렇게 하면 hello 저장된 프로시저 작업까지 실행 되지 않습니다 hello 업스트림 활동이 완료 되 고 hello 업스트림 활동의 hello 출력 데이터 집합 (준비 됨 상태)에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-227">When you do so, hello stored procedure activity does not run until hello upstream activity completes and hello output dataset of hello upstream activity is available (in Ready status).</span></span> <span data-ttu-id="255e8-228">Hello 저장 프로시저 작업의 입력된 데이터 집합으로 업스트림 여러 활동의 출력 데이터 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-228">You can specify output datasets of multiple upstream activities as input datasets of hello stored procedure activity.</span></span> <span data-ttu-id="255e8-229">작업을 수행 하면 hello 저장 프로시저 작업 하므로 모든 hello에 대 한 입력된 데이터 집합 분할 영역을 사용할 수 있는 경우에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-229">When you do so, hello stored procedure activity runs only when all hello input dataset slices are available.</span></span>  

<span data-ttu-id="255e8-230">다음 예제는 hello, hello 복사 작업의 hello 출력은: OutputDataset hello의 입력이 있는 저장 프로시저 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-230">In hello following example, hello output of hello copy activity is: OutputDataset, which is an input of hello stored procedure activity.</span></span> <span data-ttu-id="255e8-231">따라서 hello 저장된 프로시저 작업까지 실행 되지 않습니다 hello 복사 작업을 완료 되며 hello OutputDataset 분할 영역에서에서 사용할 수 (준비 상태).</span><span class="sxs-lookup"><span data-stu-id="255e8-231">Therefore, hello stored procedure activity does not run until hello copy activity completes and hello OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="255e8-232">여러 입력된 데이터 집합을 지정 하면 hello 저장된 프로시저 작업까지 실행 되지 않습니다 (준비 상태)에 사용할 수 있는 모든 hello 입력된 데이터 집합 슬라이스입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-232">If you specify multiple input datasets, hello stored procedure activity does not run until all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="255e8-233">hello 입력된 데이터 집합 매개 변수 toohello 저장 프로시저 작업으로 직접 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-233">hello input datasets cannot be used directly as parameters toohello stored procedure activity.</span></span> 

<span data-ttu-id="255e8-234">연결 작업에 대한 자세한 내용은 [파이프라인의 여러 작업](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="255e8-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

<span data-ttu-id="255e8-235">마찬가지로, toolink hello 저장 프로시저와 관련 된 활동 **다운스트림 작업** 으로 hello 저장 프로시저 작업의 hello 출력 데이터 집합을 지정 하는 (hello 활동 hello 저장된 프로시저 활동이 완료 된 후 실행 하는), 프로그램 hello 파이프라인의 hello 다운스트림 활동의 입력입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-235">Similarly, toolink hello store procedure activity with **downstream activities** (hello activities that run after hello stored procedure activity completes), specify hello output dataset of hello stored procedure activity as an input of hello downstream activity in hello pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="255e8-236">Azure SQL 데이터베이스 또는 SQL Server에 데이터를 복사할 때 hello를 구성할 수 있습니다 **SqlSink** 복사 활동 tooinvoke hello를 사용 하 여 저장된 프로시저에서에서 **sqlWriterStoredProcedureName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-236">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="255e8-237">자세한 내용은 [복사 작업에서 저장 프로시저 호출](data-factory-invoke-stored-procedure-from-copy-activity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="255e8-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="255e8-238">Hello 속성에 대 한 자세한 참조 커넥터 문서를 수행 하는 hello: [Azure SQL 데이터베이스](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-238">For details about hello property, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="255e8-239">Azure SQL 데이터 웨어하우스 또는 SQL Server 나 Azure SQL 데이터베이스에서 데이터를 복사할 때 구성할 수 있습니다 **SqlSource** 복사 활동 tooinvoke hello를 사용 하 여 hello 원본 데이터베이스에서 저장된 프로시저 tooread 데이터에서에서  **sqlReaderStoredProcedureName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="255e8-240">자세한 내용은 hello 다음 커넥터 문서를 참조 하세요.: [Azure SQL 데이터베이스](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL 데이터 웨어하우스](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="255e8-240">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="255e8-241">JSON 형식</span><span class="sxs-lookup"><span data-stu-id="255e8-241">JSON format</span></span>
<span data-ttu-id="255e8-242">저장 프로시저 작업을 정의 하기 위한 hello JSON 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-242">Here is hello JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="255e8-243">다음 표에서 hello 이러한 JSON 속성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-243">hello following table describes these JSON properties:</span></span>

| <span data-ttu-id="255e8-244">속성</span><span class="sxs-lookup"><span data-stu-id="255e8-244">Property</span></span> | <span data-ttu-id="255e8-245">설명</span><span class="sxs-lookup"><span data-stu-id="255e8-245">Description</span></span> | <span data-ttu-id="255e8-246">필수</span><span class="sxs-lookup"><span data-stu-id="255e8-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="255e8-247">name</span><span class="sxs-lookup"><span data-stu-id="255e8-247">name</span></span> | <span data-ttu-id="255e8-248">Hello 활동의 이름</span><span class="sxs-lookup"><span data-stu-id="255e8-248">Name of hello activity</span></span> |<span data-ttu-id="255e8-249">예</span><span class="sxs-lookup"><span data-stu-id="255e8-249">Yes</span></span> |
| <span data-ttu-id="255e8-250">설명</span><span class="sxs-lookup"><span data-stu-id="255e8-250">description</span></span> |<span data-ttu-id="255e8-251">어떤 hello 활동을 설명 하는 텍스트에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-251">Text describing what hello activity is used for</span></span> |<span data-ttu-id="255e8-252">아니요</span><span class="sxs-lookup"><span data-stu-id="255e8-252">No</span></span> |
| <span data-ttu-id="255e8-253">type</span><span class="sxs-lookup"><span data-stu-id="255e8-253">type</span></span> | <span data-ttu-id="255e8-254">**SqlServerStoredProcedure**로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="255e8-255">예</span><span class="sxs-lookup"><span data-stu-id="255e8-255">Yes</span></span> |
| <span data-ttu-id="255e8-256">inputs</span><span class="sxs-lookup"><span data-stu-id="255e8-256">inputs</span></span> | <span data-ttu-id="255e8-257">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-257">Optional.</span></span> <span data-ttu-id="255e8-258">입력된 데이터 집합을 지정 않습니다 ('준비' 상태)에서 사용할 수 있어야 hello에 대 한 저장 프로시저 활동 toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="255e8-259">hello 입력된 데이터 집합 매개 변수로 hello 저장 프로시저에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-259">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="255e8-260">시작 hello 저장 프로시저 작업 전에 것만 사용 되는 toocheck hello 종속성 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-260">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> |<span data-ttu-id="255e8-261">아니요</span><span class="sxs-lookup"><span data-stu-id="255e8-261">No</span></span> |
| <span data-ttu-id="255e8-262">outputs</span><span class="sxs-lookup"><span data-stu-id="255e8-262">outputs</span></span> | <span data-ttu-id="255e8-263">저장 프로시저 작업에 대한 출력 데이터 집합을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="255e8-264">출력 데이터 집합 지정 hello **일정** hello에 대 한 저장 프로시저 작업 (시간별, 매주, 매월, 등).</span><span class="sxs-lookup"><span data-stu-id="255e8-264">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="255e8-265">hello 출력 데이터 집합 사용 해야 합니다는 **연결 된 서비스** tooan Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스 또는 저장된 프로시저 toorun hello 하려는 SQL Server 데이터베이스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-265">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <br/><br/><span data-ttu-id="255e8-266">hello 출력 데이터 집합으로 사용할 수는 방식으로 toopass hello 결과 후속 처리에 대 한 hello 저장 프로시저의 다른 활동에 의해 ([활동 체인](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) hello 파이프라인에서.</span><span class="sxs-lookup"><span data-stu-id="255e8-266">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="255e8-267">그러나 데이터 팩터리는 저장된 프로시저 toothis 데이터 집합의 hello 출력을 자동으로 기록 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-267">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="255e8-268">Hello 저장 프로시저 출력 데이터 집합 가리키는 hello 해당 쓰기 tooa SQL 테이블 이며</span><span class="sxs-lookup"><span data-stu-id="255e8-268">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <br/><br/><span data-ttu-id="255e8-269">경우에 따라 hello 출력 데이터 집합 수는 **더미 데이터 집합**, hello를 실행 하기 위한 toospecify hello 일정 저장 프로시저 작업에만 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-269">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span> |<span data-ttu-id="255e8-270">예</span><span class="sxs-lookup"><span data-stu-id="255e8-270">Yes</span></span> |
| <span data-ttu-id="255e8-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="255e8-271">storedProcedureName</span></span> |<span data-ttu-id="255e8-272">Hello Azure SQL 데이터베이스 또는 출력 테이블 사용 hello hello 연결 된 서비스에 의해 표시 되는 Azure SQL 데이터 웨어하우스 또는 SQL Server 데이터베이스의 hello 저장 프로시저의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-272">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="255e8-273">예</span><span class="sxs-lookup"><span data-stu-id="255e8-273">Yes</span></span> |
| <span data-ttu-id="255e8-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="255e8-274">storedProcedureParameters</span></span> |<span data-ttu-id="255e8-275">저장 프로시저 매개 변수의 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="255e8-276">매개 변수에 대해 toopass을 null 필요 hello 구문 사용: "param1": null (모든 소문자).</span><span class="sxs-lookup"><span data-stu-id="255e8-276">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="255e8-277">이 속성을 사용 하는 방법에 대 한 샘플 toolearn 다음 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="255e8-277">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="255e8-278">아니요</span><span class="sxs-lookup"><span data-stu-id="255e8-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="255e8-279">정적 값 전달</span><span class="sxs-lookup"><span data-stu-id="255e8-279">Passing a static value</span></span>
<span data-ttu-id="255e8-280">이제 '샘플 문서' 라는 정적 값을 포함 하는 hello 테이블의 '시나리오' 라는 다른 열 추가 생각해 봅시다.</span><span class="sxs-lookup"><span data-stu-id="255e8-280">Now, let’s consider adding another column named ‘Scenario’ in hello table containing a static value called ‘Document sample’.</span></span>

![샘플 데이터 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="255e8-282">**테이블:**</span><span class="sxs-lookup"><span data-stu-id="255e8-282">**Table:**</span></span>

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

<span data-ttu-id="255e8-283">**저장 프로시저:**</span><span class="sxs-lookup"><span data-stu-id="255e8-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="255e8-284">이제, hello 통과 **시나리오** hello에서 매개 변수 및 hello 값 저장 프로시저 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="255e8-284">Now, pass hello **Scenario** parameter and hello value from hello stored procedure activity.</span></span> <span data-ttu-id="255e8-285">hello **typeProperties** hello 샘플 같습니다 hello 다음 코드 조각 앞의 섹션:</span><span class="sxs-lookup"><span data-stu-id="255e8-285">hello **typeProperties** section in hello preceding sample looks like hello following snippet:</span></span>

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

<span data-ttu-id="255e8-286">**Data Factory 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="255e8-286">**Data Factory dataset:**</span></span>

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="255e8-287">**Data Factory 파이프라인**</span><span class="sxs-lookup"><span data-stu-id="255e8-287">**Data Factory pipeline**</span></span>

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```