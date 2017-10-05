---
title: "SQL Server 저장 프로시저 작업"
description: "SQL Server 저장 프로시저 작업을 사용하여 데이터 팩터리 파이프라인으로 Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스에서 저장 프로시저를 호출하는 방법을 알아봅니다."
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
ms.openlocfilehash: 6505d9aa2c7ae003bd928e2fa82cd923a9615394
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="e0193-103">SQL Server 저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="e0193-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="e0193-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="e0193-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="e0193-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="e0193-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="e0193-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="e0193-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="e0193-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="e0193-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="e0193-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="e0193-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="e0193-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="e0193-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="e0193-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="e0193-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="e0193-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="e0193-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="e0193-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="e0193-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="e0193-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="e0193-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="e0193-114">개요</span><span class="sxs-lookup"><span data-stu-id="e0193-114">Overview</span></span>
<span data-ttu-id="e0193-115">Data Factory [파이프라인](data-factory-create-pipelines.md)의 데이터 변환 작업을 통해 원시 데이터를 변환 및 처리하여 예측 가능한, 통찰력 있는 정보로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) to transform and process raw data into predictions and insights.</span></span> <span data-ttu-id="e0193-116">저장 프로시저 작업은 Data Factory에서 지원하는 변환 작업 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-116">The Stored Procedure Activity is one of the transformation activities that Data Factory supports.</span></span> <span data-ttu-id="e0193-117">이 문서는 데이터 팩터리의 데이터 변환 및 지원되는 변환 활동의 일반적인 개요를 표시하는 [데이터 변환 활동](data-factory-data-transformation-activities.md) 문서에서 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="e0193-118">저장 프로시저 작업을 사용하여 엔터프라이즈 또는 Azure VM(Virtual Machine)의 다음 데이터 저장소 중 하나에서 저장 프로시저를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-118">You can use the Stored Procedure Activity to invoke a stored procedure in one of the following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="e0193-119">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="e0193-119">Azure SQL Database</span></span>
- <span data-ttu-id="e0193-120">Azure SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="e0193-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="e0193-121">SQL Server 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="e0193-121">SQL Server Database.</span></span>  <span data-ttu-id="e0193-122">SQL Server를 사용 중인 경우 데이터베이스를 호스트하는 동일한 컴퓨터 또는 데이터베이스에 대한 액세스 권한이 있는 별도 컴퓨터에서 데이터 관리 게이트웨이를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-122">If you are using SQL Server, install Data Management Gateway on the same machine that hosts the database or on a separate machine that has access to the database.</span></span> <span data-ttu-id="e0193-123">데이터 관리 게이트웨이는 온-프레미스/Azure VM에서 데이터 원본을 Cloud Services에 안전하고 관리되는 방식으로 연결하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="e0193-124">자세한 내용은 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0193-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0193-125">Azure SQL Database 또는 SQL Server로 데이터를 복사할 때 **sqlWriterStoredProcedureName** 속성을 사용하여 복사 작업에 저장 프로시저를 호출하도록 **SqlSink**를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-125">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="e0193-126">자세한 내용은 [복사 작업에서 저장 프로시저 호출](data-factory-invoke-stored-procedure-from-copy-activity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0193-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="e0193-127">이 속성에 대한 자세한 내용은 커넥터 문서 [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0193-127">For details about the property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="e0193-128">복사 작업을 사용하여 Azure SQL Data Warehouse로 데이터를 복사하는 동안 저장 프로시저를 호출하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="e0193-129">그러나 저장 프로시저 작업을 사용하여 SQL Data Warehouse의 저장 프로시저를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-129">But, you can use the stored procedure activity to invoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="e0193-130">Azure SQL Database, SQL Server 또는 Azure SQL Data Warehouse에서 데이터를 복사하는 경우 복사 작업에서 **sqlReaderStoredProcedureName** 속성을 사용하여 원본 데이터베이스에서 데이터를 읽는 저장 프로시저를 호출하도록 **SqlSource**를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="e0193-131">자세한 내용은 커넥터 문서 [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0193-131">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="e0193-132">다음 연습에서는 파이프라인에서 저장 프로시저 활동을 사용하여 Azure SQL Database에서 저장 프로시저를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-132">The following walkthrough uses the Stored Procedure Activity in a pipeline to invoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="e0193-133">연습</span><span class="sxs-lookup"><span data-stu-id="e0193-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="e0193-134">샘플 테이블 및 저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="e0193-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="e0193-135">SQL Server Management Studio 또는 익숙한 다른 도구를 사용하여 Azure SQL 데이터베이스에서 다음 **테이블** 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-135">Create the following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="e0193-136">datetimestamp 열은 해당 ID가 생성된 날짜와 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-136">The datetimestamp column is the date and time when the corresponding ID is generated.</span></span>

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
    <span data-ttu-id="e0193-137">Id는 고유 식별자이며 datetimestamp 열은 해당 ID가 생성된 날짜와 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-137">Id is the unique identified and the datetimestamp column is the date and time when the corresponding ID is generated.</span></span>
    
    ![샘플 데이터](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="e0193-139">이 샘플에서는 저장 프로시저가 Azure SQL Database에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-139">In this sample, the stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="e0193-140">저장 프로시저가 Azure SQL Data Warehouse 및 SQL Server Database에 있는 경우 접근 방법이 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-140">If the stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, the approach is similar.</span></span> <span data-ttu-id="e0193-141">SQL Server Database의 경우 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="e0193-142">**sampletable**에 데이터를 삽입하는 다음 **저장 프로시저**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-142">Create the following **stored procedure** that inserts data in to the **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="e0193-143">매개 변수(이 예에서는 DateTime)의 **이름** 및 **대/소문자**는 파이프라인/작업 JSON에서 지정된 매개 변수의 이름 및 대/소문자와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-143">**Name** and **casing** of the parameter (DateTime in this example) must match that of parameter specified in the pipeline/activity JSON.</span></span> <span data-ttu-id="e0193-144">저장 프로시저 정의에서 **@** 는 매개 변수에 대한 접두사로 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-144">In the stored procedure definition, ensure that **@** is used as a prefix for the parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="e0193-145">데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-145">Create a data factory</span></span>
1. <span data-ttu-id="e0193-146">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-146">Log in to [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e0193-147">왼쪽 메뉴에서 **새로 만들기**를 클릭하고 **인텔리전스 + 분석**을 클릭한 다음 **Data Factory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-147">Click **NEW** on the left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![새 data factory](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="e0193-149">**새 data factory** 블레이드에서 이름으로 **SProcDF**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-149">In the **New data factory** blade, enter **SProcDF** for the Name.</span></span> <span data-ttu-id="e0193-150">Azure Data Factory 이름은 **전역적으로 고유**합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="e0193-151">팩터리를 성공적으로 만들려면 데이터 팩터리의 이름의 접두사를 사용자의 이름으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-151">You need to prefix the name of the data factory with your name, to enable the successful creation of the factory.</span></span>

   ![새 data factory](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="e0193-153">Azure **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="e0193-154">**리소스 그룹**에 대해 다음 단계 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-154">For **Resource Group**, do one of the following steps:</span></span>
   1. <span data-ttu-id="e0193-155">**새로 만들기**를 클릭하고 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-155">Click **Create new** and enter a name for the resource group.</span></span>
   2. <span data-ttu-id="e0193-156">**기존 항목 사용**을 클릭하고 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="e0193-157">데이터 팩터리의 **위치** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-157">Select the **location** for the data factory.</span></span>
7. <span data-ttu-id="e0193-158">다음에 로그인할 때 대시보드에 Data Factory가 표시되도록 **대시보드에 고정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-158">Select **Pin to dashboard** so that you can see the data factory on the dashboard next time you log in.</span></span>
8. <span data-ttu-id="e0193-159">**새 Data Factory** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-159">Click **Create** on the **New data factory** blade.</span></span>
9. <span data-ttu-id="e0193-160">Azure Portal의 **대시보드** 에 생성된 데이터 팩터리가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-160">You see the data factory being created in the **dashboard** of the Azure portal.</span></span> <span data-ttu-id="e0193-161">데이터 팩터리 만들기를 완료한 후에는 데이터 팩터리 페이지가 표시되며 여기에 데이터 팩터리의 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-161">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![Data Factory 홈페이지](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="e0193-163">Azure SQL 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="e0193-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="e0193-164">데이터 팩터리를 만든 후 sampletable 테이블 및 sp_sample 저장 프로시저가 포함된 Azure SQL 데이터베이스를 데이터 팩터리에 연결하는 Azure SQL 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-164">After creating the data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains the sampletable table and sp_sample stored procedure, to your data factory.</span></span>

1. <span data-ttu-id="e0193-165">**SProcDF**에 대한 **Data Factory** 블레이드에서 **작성 및 배포**를 클릭하여 Data Factory 편집기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-165">Click **Author and deploy** on the **Data Factory** blade for **SProcDF** to launch the Data Factory Editor.</span></span>
2. <span data-ttu-id="e0193-166">명령 모음에서 **새 데이터 저장소**를 클릭하고 **Azure SQL Database**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-166">Click **New data store** on the command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="e0193-167">편집기에 Azure SQL 연결된 서비스를 만들기 위한 JSON 스크립트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-167">You should see the JSON script for creating an Azure SQL linked service in the editor.</span></span>

   ![새 데이터 저장소](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="e0193-169">JSON 스크립트에서 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-169">In the JSON script, make the following changes:</span></span>

   1. <span data-ttu-id="e0193-170">`<servername>`을 Azure SQL Database 서버의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-170">Replace `<servername>` with the name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="e0193-171">`<databasename>`을 테이블 및 저장 프로시저를 만든 데이터베이스로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-171">Replace `<databasename>` with the database in which you created the table and the stored procedure.</span></span>
   3. <span data-ttu-id="e0193-172">`<username@servername>`을 데이터베이스에 대한 액세스 권한이 있는 사용자 계정으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-172">Replace `<username@servername>` with the user account that has access to the database.</span></span>
   4. <span data-ttu-id="e0193-173">`<password>`를 사용자 계정의 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-173">Replace `<password>` with the password for the user account.</span></span>

      ![새 데이터 저장소](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="e0193-175">연결된 서비스를 배포하려면 명령 모음에서 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-175">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="e0193-176">왼쪽의 트리 뷰에 AzureSqlLinkedService가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-176">Confirm that you see the AzureSqlLinkedService in the tree view on the left.</span></span>

    ![연결된 서비스와 트리 뷰](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="e0193-178">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="e0193-178">Create an output dataset</span></span>
<span data-ttu-id="e0193-179">저장 프로시저가 어떠한 데이터도 생성하지 않는 경우에도 저장 프로시저 작업의 출력 데이터 집합을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-179">You must specify an output dataset for a stored procedure activity even if the stored procedure does not produce any data.</span></span> <span data-ttu-id="e0193-180">이는 출력 데이터 집합이 작업의 일정(작업 실행 빈도 즉, 매시간, 매일 등)을 지정하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-180">That's because it's the output dataset that drives the schedule of the activity (how often the activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="e0193-181">출력 데이터 집합은 Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스나 저장 프로시저를 실행하려는 SQL Server 데이터베이스를 참조하는 **연결된 서비스** 를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-181">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="e0193-182">출력 데이터 집합은 파이프라인에서 다른 활동을 통한 후속 처리([활동 체이닝](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline))를 위해 저장 프로시저의 결과를 전달하는 방법으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-182">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="e0193-183">그러나 Data Factory는 저장 프로시저의 출력을 이 데이터 집합에 자동으로 쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-183">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="e0193-184">출력 데이터 집합이 가리키는 SQL 테이블에 기록하는 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-184">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="e0193-185">경우에 따라 출력 데이터 집합은 **더미 데이터 집합**(저장 프로시저의 출력을 실제로 보관하고 있지 않은 테이블을 가리키는 데이터 집합)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-185">In some cases, the output dataset can be a **dummy dataset** (a dataset that points to a table that does not really hold output of the stored procedure).</span></span> <span data-ttu-id="e0193-186">더미 데이터 집합은 저장 프로시저 작업의 실행 일정을 지정하는 데에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-186">This dummy dataset is used only to specify the schedule for running the stored procedure activity.</span></span> 

1. <span data-ttu-id="e0193-187">단추가 표시되지 않는 경우 도구 모음에서 **... 추가**, **새 데이터 집합**, **Azure SQL**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-187">Click **... More** on the toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="e0193-188">명령 모음에서 **새 데이터 집합**을 클릭하고 **Azure SQL**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-188">**New dataset** on the command bar and select **Azure SQL**.</span></span>

    ![연결된 서비스와 트리 뷰](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="e0193-190">다음 JSON 스크립트를 복사하여 JSON 편집기에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-190">Copy/paste the following JSON script in to the JSON editor.</span></span>

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
3. <span data-ttu-id="e0193-191">데이터 집합을 배포하려면 명령 모음에서 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-191">To deploy the dataset, click **Deploy** on the command bar.</span></span> <span data-ttu-id="e0193-192">트리 뷰에 데이터 집합이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-192">Confirm that you see the dataset in the tree view.</span></span>

    ![연결된 서비스와 트리 뷰](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="e0193-194">SqlServerStoredProcedure 작업을 사용하여 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="e0193-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="e0193-195">이제 저장 프로시저 작업을 사용하여 파이프라인 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="e0193-196">다음 속성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-196">Notice the following properties:</span></span> 

- <span data-ttu-id="e0193-197">**type** 속성이 **SqlServerStoredProcedure**로 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-197">The **type** property is set to **SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="e0193-198">type 속성의 **storedProcedureName**은 **sp_sample**(저장 프로시저의 이름)로 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-198">The **storedProcedureName** in type properties is set to **sp_sample** (name of the stored procedure).</span></span>
- <span data-ttu-id="e0193-199">**storedProcedureParameters** 섹션에는 **DataTime** 매개 변수 하나가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-199">The **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="e0193-200">JSON에서 이 매개 변수의 이름 및 대/소문자는 저장 프로시저 정의에 있는 매개 변수의 이름 및 대/소문자와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-200">Name and casing of the parameter in JSON must match the name and casing of the parameter in the stored procedure definition.</span></span> <span data-ttu-id="e0193-201">매개 변수에 대해 null을 전달해야 하는 경우 구문: `"param1": null`(모두 소문자)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-201">If you need pass null for a parameter, use the syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="e0193-202">단추가 표시되지 않는 경우 도구 모음에서 **... 추가**를 클릭하고 **새 파이프라인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-202">Click **... More** on the command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="e0193-203">다음 JSON 코드 조각을 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-203">Copy/paste the following JSON snippet:</span></span>   

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
3. <span data-ttu-id="e0193-204">파이프라인을 배포하려면 도구 모음에서 **배포** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-204">To deploy the pipeline, click **Deploy** on the toolbar.</span></span>  

### <a name="monitor-the-pipeline"></a><span data-ttu-id="e0193-205">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="e0193-205">Monitor the pipeline</span></span>
1. <span data-ttu-id="e0193-206">**X**를 클릭하여 Data Factory 편집기 블레이드를 닫고 Data Factory 블레이드로 돌아가서 **다이어그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-206">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![다이어그램 타일](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="e0193-208">**다이어그램 보기**에 파이프라인의 개요와 이 자습서에 사용된 데이터 집합이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-208">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![다이어그램 타일](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="e0193-210">[다이어그램 보기]에서 `sprocsampleout` 데이터 집합을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-210">In the Diagram View, double-click the dataset `sprocsampleout`.</span></span> <span data-ttu-id="e0193-211">준비 상태의 조각이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-211">You see the slices in Ready state.</span></span> <span data-ttu-id="e0193-212">조각은 JSON에서 시작 시간 및 종료 시간 사이의 매시간 생성되므로 5개 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-212">There should be five slices because a slice is produced for each hour between the start time and end time from the JSON.</span></span>

    ![다이어그램 타일](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="e0193-214">조각이 **Ready** 상태일 때 Azure SQL Database에 대해 `select * from sampletable` 쿼리를 실행하여 저장 프로시저에 의해 데이터가 테이블에 삽입되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-214">When a slice is in **Ready** state, run a `select * from sampletable` query against the Azure SQL database to verify that the data was inserted in to the table by the stored procedure.</span></span>

   ![출력 데이터](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="e0193-216">Azure Data Factory 파이프라인 모니터링에 대한 자세한 내용은 [파이프라인 모니터링](data-factory-monitor-manage-pipelines.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0193-216">See [Monitor the pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="e0193-217">입력 데이터 집합 지정</span><span class="sxs-lookup"><span data-stu-id="e0193-217">Specify an input dataset</span></span>
<span data-ttu-id="e0193-218">이 연습에서는 저장 프로시저 작업에 입력 데이터 집합이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-218">In the walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="e0193-219">입력 데이터 집합을 지정하면 입력 데이터 집합의 조각을 사용할 수 있을 때까지(준비 상태) 저장 프로시저 작업이 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-219">If you specify an input dataset, the stored procedure activity does not run until the slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="e0193-220">데이터 집합은 (동일한 파이프라인의 다른 작업에서 생성하지 않은) 외부 데이터 집합 또는 업스트림 작업(이 작업 이전에 실행된 작업)에서 생성된 내부 데이터 집합일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-220">The dataset can be an external dataset (that is not produced by another activity in the same pipeline) or an internal dataset that is produced by an upstream activity (the activity that runs before this activity).</span></span> <span data-ttu-id="e0193-221">저장 프로시저 작업에 대해 입력 데이터 집합을 여러 개 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-221">You can specify multiple input datasets for the stored procedure activity.</span></span> <span data-ttu-id="e0193-222">이렇게 하면 모든 입력 데이터 집합 조각을 사용할 수 있는 경우에만(준비 상태) 저장 프로시저 작업이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-222">If you do so, the stored procedure activity runs only when all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="e0193-223">저장 프로시저에서 입력 데이터 집합을 매개 변수로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-223">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="e0193-224">저장 프로시저 작업을 시작하기 전에 종속성을 확인하는 데만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-224">It is only used to check the dependency before starting the stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="e0193-225">다른 작업과 연결</span><span class="sxs-lookup"><span data-stu-id="e0193-225">Chaining with other activities</span></span>
<span data-ttu-id="e0193-226">업스트림 작업을 이 작업과 연결하려는 경우 업스트림 작업의 출력을 이 작업의 입력으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-226">If you want to chain an upstream activity with this activity, specify the output of the upstream activity as an input of this activity.</span></span> <span data-ttu-id="e0193-227">이렇게 하면 업스트림 작업이 완료되고 업스트림 작업의 출력 데이터 집합을 사용할 수 있을 때까지(준비 상태) 저장 프로시저 작업이 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-227">When you do so, the stored procedure activity does not run until the upstream activity completes and the output dataset of the upstream activity is available (in Ready status).</span></span> <span data-ttu-id="e0193-228">여러 업스트림 작업의 출력 데이터 집합을 저장 프로시저 작업의 입력 데이터 집합으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-228">You can specify output datasets of multiple upstream activities as input datasets of the stored procedure activity.</span></span> <span data-ttu-id="e0193-229">이렇게 하면 모든 입력 데이터 집합 조각을 사용할 수 있는 경우에만 저장 프로시저 작업이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-229">When you do so, the stored procedure activity runs only when all the input dataset slices are available.</span></span>  

<span data-ttu-id="e0193-230">다음 예제에서 복사 작업의 출력은 OutputDataset으로, 저장 프로시저 작업의 입력입니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-230">In the following example, the output of the copy activity is: OutputDataset, which is an input of the stored procedure activity.</span></span> <span data-ttu-id="e0193-231">따라서 복사 작업이 완료되고 OutputDataset 조각이 사용할 수 있을 때까지(준비 상태) 저장 프로시저 작업이 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-231">Therefore, the stored procedure activity does not run until the copy activity completes and the OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="e0193-232">여러 입력 데이터 집합을 지정하면 입력 데이터 집합의 모든 조각을 사용할 수 있을 때까지(준비 상태) 저장 프로시저 작업이 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-232">If you specify multiple input datasets, the stored procedure activity does not run until all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="e0193-233">입력 데이터 집합은 저장 프로시저 작업에 대한 매개 변수로 직접 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-233">The input datasets cannot be used directly as parameters to the stored procedure activity.</span></span> 

<span data-ttu-id="e0193-234">연결 작업에 대한 자세한 내용은 [파이프라인의 여러 작업](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0193-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob to blob",
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

<span data-ttu-id="e0193-235">마찬가지로 저장 프로시저 작업을 **다운스트림 작업**(저장 프로시저 작업이 완료된 후 실행되는 작업)과 연결시키려면 저장 프로시저 작업의 출력 데이터 집합을 파이프라인 내 다운스트림 작업의 입력으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-235">Similarly, to link the store procedure activity with **downstream activities** (the activities that run after the stored procedure activity completes), specify the output dataset of the stored procedure activity as an input of the downstream activity in the pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0193-236">Azure SQL Database 또는 SQL Server로 데이터를 복사할 때 **sqlWriterStoredProcedureName** 속성을 사용하여 복사 작업에 저장 프로시저를 호출하도록 **SqlSink**를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-236">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="e0193-237">자세한 내용은 [복사 작업에서 저장 프로시저 호출](data-factory-invoke-stored-procedure-from-copy-activity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0193-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="e0193-238">이 속성에 대한 자세한 내용은 커넥터 문서 [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0193-238">For details about the property, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="e0193-239">Azure SQL Database, SQL Server 또는 Azure SQL Data Warehouse에서 데이터를 복사하는 경우 복사 작업에서 **sqlReaderStoredProcedureName** 속성을 사용하여 원본 데이터베이스에서 데이터를 읽는 저장 프로시저를 호출하도록 **SqlSource**를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="e0193-240">자세한 내용은 커넥터 문서 [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0193-240">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="e0193-241">JSON 형식</span><span class="sxs-lookup"><span data-stu-id="e0193-241">JSON format</span></span>
<span data-ttu-id="e0193-242">다음은 저장 프로시저 작업을 정의하기 위한 JSON 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-242">Here is the JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of the stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="e0193-243">다음 표에서는 이러한 JSON 속성에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-243">The following table describes these JSON properties:</span></span>

| <span data-ttu-id="e0193-244">속성</span><span class="sxs-lookup"><span data-stu-id="e0193-244">Property</span></span> | <span data-ttu-id="e0193-245">설명</span><span class="sxs-lookup"><span data-stu-id="e0193-245">Description</span></span> | <span data-ttu-id="e0193-246">필수</span><span class="sxs-lookup"><span data-stu-id="e0193-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e0193-247">name</span><span class="sxs-lookup"><span data-stu-id="e0193-247">name</span></span> | <span data-ttu-id="e0193-248">작업의 이름</span><span class="sxs-lookup"><span data-stu-id="e0193-248">Name of the activity</span></span> |<span data-ttu-id="e0193-249">예</span><span class="sxs-lookup"><span data-stu-id="e0193-249">Yes</span></span> |
| <span data-ttu-id="e0193-250">설명</span><span class="sxs-lookup"><span data-stu-id="e0193-250">description</span></span> |<span data-ttu-id="e0193-251">작업이 무엇에 사용되는지 설명하는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-251">Text describing what the activity is used for</span></span> |<span data-ttu-id="e0193-252">아니요</span><span class="sxs-lookup"><span data-stu-id="e0193-252">No</span></span> |
| <span data-ttu-id="e0193-253">type</span><span class="sxs-lookup"><span data-stu-id="e0193-253">type</span></span> | <span data-ttu-id="e0193-254">**SqlServerStoredProcedure**로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="e0193-255">예</span><span class="sxs-lookup"><span data-stu-id="e0193-255">Yes</span></span> |
| <span data-ttu-id="e0193-256">inputs</span><span class="sxs-lookup"><span data-stu-id="e0193-256">inputs</span></span> | <span data-ttu-id="e0193-257">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-257">Optional.</span></span> <span data-ttu-id="e0193-258">입력 데이터 집합을 지정하는 경우 실행할 저장 프로시저 작업에 사용할 수 있어야 합니다('Ready' 상태).</span><span class="sxs-lookup"><span data-stu-id="e0193-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="e0193-259">저장 프로시저에서 입력 데이터 집합을 매개 변수로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-259">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="e0193-260">저장 프로시저 작업을 시작하기 전에 종속성을 확인하는 데만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-260">It is only used to check the dependency before starting the stored procedure activity.</span></span> |<span data-ttu-id="e0193-261">아니요</span><span class="sxs-lookup"><span data-stu-id="e0193-261">No</span></span> |
| <span data-ttu-id="e0193-262">outputs</span><span class="sxs-lookup"><span data-stu-id="e0193-262">outputs</span></span> | <span data-ttu-id="e0193-263">저장 프로시저 작업에 대한 출력 데이터 집합을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="e0193-264">출력 데이터 집합은 저장 프로시저 작업에 대한 **일정** (매시간, 매주, 매월 등)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-264">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="e0193-265">출력 데이터 집합은 Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스나 저장 프로시저를 실행하려는 SQL Server 데이터베이스를 참조하는 **연결된 서비스** 를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-265">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <br/><br/><span data-ttu-id="e0193-266">출력 데이터 집합은 파이프라인에서 다른 활동을 통한 후속 처리([활동 체이닝](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline))를 위해 저장 프로시저의 결과를 전달하는 방법으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-266">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="e0193-267">그러나 Data Factory는 저장 프로시저의 출력을 이 데이터 집합에 자동으로 쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-267">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="e0193-268">출력 데이터 집합이 가리키는 SQL 테이블에 기록하는 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-268">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <br/><br/><span data-ttu-id="e0193-269">경우에 따라 출력 데이터 집합은 저장 프로시저 작업을 실행하는 일정을 지정하기 위해서만 사용되는 **더미 데이터 집합**일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-269">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span> |<span data-ttu-id="e0193-270">예</span><span class="sxs-lookup"><span data-stu-id="e0193-270">Yes</span></span> |
| <span data-ttu-id="e0193-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="e0193-271">storedProcedureName</span></span> |<span data-ttu-id="e0193-272">출력 테이블에서 사용하는 연결된 서비스로 표시되는 Azure SQL Database, Azure SQL Data Warehouse 또는 SQL Server Database의 저장 프로시저 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-272">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="e0193-273">예</span><span class="sxs-lookup"><span data-stu-id="e0193-273">Yes</span></span> |
| <span data-ttu-id="e0193-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="e0193-274">storedProcedureParameters</span></span> |<span data-ttu-id="e0193-275">저장 프로시저 매개 변수의 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="e0193-276">매개 변수에 대해 null을 전달해야 하는 경우 구문: "param1": null(모두 소문자)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-276">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="e0193-277">이 속성을 사용하는 방법에 대한 자세한 내용은 다음 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0193-277">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="e0193-278">아니요</span><span class="sxs-lookup"><span data-stu-id="e0193-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="e0193-279">정적 값 전달</span><span class="sxs-lookup"><span data-stu-id="e0193-279">Passing a static value</span></span>
<span data-ttu-id="e0193-280">'Document sample'라는 정적 값이 포함된 테이블에 'Scenario'라는 다른 열을 추가해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-280">Now, let’s consider adding another column named ‘Scenario’ in the table containing a static value called ‘Document sample’.</span></span>

![샘플 데이터 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="e0193-282">**테이블:**</span><span class="sxs-lookup"><span data-stu-id="e0193-282">**Table:**</span></span>

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

<span data-ttu-id="e0193-283">**저장 프로시저:**</span><span class="sxs-lookup"><span data-stu-id="e0193-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="e0193-284">이제 **Scenario** 매개 변수와 저장 프로시저 작업의 값을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-284">Now, pass the **Scenario** parameter and the value from the stored procedure activity.</span></span> <span data-ttu-id="e0193-285">위 샘플에서 **typeProperties** 섹션은 다음 코드 조각과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e0193-285">The **typeProperties** section in the preceding sample looks like the following snippet:</span></span>

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

<span data-ttu-id="e0193-286">**Data Factory 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="e0193-286">**Data Factory dataset:**</span></span>

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

<span data-ttu-id="e0193-287">**Data Factory 파이프라인**</span><span class="sxs-lookup"><span data-stu-id="e0193-287">**Data Factory pipeline**</span></span>

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