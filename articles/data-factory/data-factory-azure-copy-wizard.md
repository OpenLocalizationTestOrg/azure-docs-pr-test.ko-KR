---
title: "Azure Data Factory 복사 마법사 | Microsoft 문서"
description: "Data Factory Azure 복사 마법사를 사용하여 지원되는 데이터 소스의 데이터를 싱크로 복사하는 방법에 대해 알아보세요."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 0974eb40-db98-4149-a50d-48db46817076
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 53eaa650308979bc0953a6403baf1fd1b86f7420
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-factory-copy-wizard"></a><span data-ttu-id="fa9d8-103">Azure Data Factory 복사 마법사</span><span class="sxs-lookup"><span data-stu-id="fa9d8-103">Azure Data Factory Copy Wizard</span></span>
<span data-ttu-id="fa9d8-104">Azure Data Factory 복사 마법사는 일반적으로 종단 간 데이터 통합 시나리오의 첫 번째 단계인 데이터 수집 프로세스를 용이하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-104">The Azure Data Factory Copy Wizard eases the process of ingesting data, which is usually a first step in an end-to-end data integration scenario.</span></span> <span data-ttu-id="fa9d8-105">Azure Data Factory 복사 마법사를 진행할 때는 연결된 서비스, 데이터 집합 및 파이프라인에 대한 JSON 정의를 이해할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-105">When going through the Azure Data Factory Copy Wizard, you do not need to understand any JSON definitions for linked services, data sets, and pipelines.</span></span> <span data-ttu-id="fa9d8-106">선택한 데이터 원본에서 선택한 대상으로 데이터를 복사하는 파이프라인이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-106">The wizard automatically creates a pipeline to copy data from the selected data source to the selected destination.</span></span> <span data-ttu-id="fa9d8-107">또한 복사 마법사는 만들 때 수집된 데이터의 유효성을 검사하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-107">In addition, the Copy Wizard helps you to validate the data being ingested at the time of authoring.</span></span> <span data-ttu-id="fa9d8-108">이렇게 하면 특히 데이터 원본에서 처음으로 데이터를 처리할 때 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-108">This saves time, especially when you are ingesting data for the first time from the data source.</span></span> <span data-ttu-id="fa9d8-109">복사 마법사를 시작하려면 Data Factory 홈 페이지에서 **데이터 복사** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-109">To start the Copy Wizard, click the **Copy data** tile on the home page of your data factory.</span></span>

![복사 마법사](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="designed-for-big-data"></a><span data-ttu-id="fa9d8-111">빅 데이터를 위한 설계</span><span class="sxs-lookup"><span data-stu-id="fa9d8-111">Designed for big data</span></span>
<span data-ttu-id="fa9d8-112">이 마법사를 사용하면 다양한 원본에서 대상으로 데이터를 몇 분만에 쉽게 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-112">This wizard allows you to easily move data from a wide variety of sources to destinations in minutes.</span></span> <span data-ttu-id="fa9d8-113">마법사를 완료하면 종속 Data Factory 엔터티(연결된 서비스 및 데이터 집합)와 함께 복사 작업을 포함한 파이프라인이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-113">After you go through the wizard, a pipeline with a copy activity is automatically created for you, along with dependent Data Factory entities (linked services and data sets).</span></span> <span data-ttu-id="fa9d8-114">파이프라인을 만드는 데 필요한 추가 단계는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-114">No additional steps are required to create the pipeline.</span></span>   

![데이터 원본 선택](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> <span data-ttu-id="fa9d8-116">Azure Blob에서 Azure SQL Database 테이블로 데이터를 복사하기 위한 샘플 파이프라인을 만드는 단계별 지침은 [복사 마법사 자습서](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-116">For step-by-step instructions to create a sample pipeline to copy data from an Azure blob to an Azure SQL Database table, see the [Copy Wizard tutorial](data-factory-copy-data-wizard-tutorial.md).</span></span>
>
>

<span data-ttu-id="fa9d8-117">마법사는 처음부터 빅 데이터를 염두에 두고 설계되었으며 다양한 데이터 및 개체 유형을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-117">The wizard is designed with big data in mind from the start, with support for diverse data and object types.</span></span> <span data-ttu-id="fa9d8-118">수백 개의 폴더, 파일 또는 테이블을 이동하는 Data Factory 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-118">You can author Data Factory pipelines that move hundreds of folders, files, or tables.</span></span> <span data-ttu-id="fa9d8-119">이 마법사는 자동 데이터 미리 보기, 스키마 캡처 및 매핑, 데이터 필터링을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-119">The wizard supports automatic data preview, schema capture and mapping, and data filtering.</span></span>

## <a name="automatic-data-preview"></a><span data-ttu-id="fa9d8-120">자동 데이터 미리 보기</span><span class="sxs-lookup"><span data-stu-id="fa9d8-120">Automatic data preview</span></span>
<span data-ttu-id="fa9d8-121">복사할 데이터인지 확인하기 위해 선택한 데이터 원본에서 데이터의 일부를 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-121">You can preview part of the data from the selected data source in order to validate whether the data is what you want to copy.</span></span> <span data-ttu-id="fa9d8-122">또한 원본 데이터가 텍스트 파일에 있는 경우 복사 마법사는 텍스트 파일을 구문 분석하여 행 및 열 구분 기호와 스키마를 자동으로 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-122">In addition, if the source data is in a text file, the Copy Wizard parses the text file to learn the row and column delimiters and schema automatically.</span></span>

![파일 형식 설정](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a><span data-ttu-id="fa9d8-124">스키마 캡처 및 매핑</span><span class="sxs-lookup"><span data-stu-id="fa9d8-124">Schema capture and mapping</span></span>
<span data-ttu-id="fa9d8-125">입력 데이터의 스키마는 경우에 따라 출력 데이터의 스키마와 일치하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-125">The schema of input data may not match the schema of output data in some cases.</span></span> <span data-ttu-id="fa9d8-126">이 시나리오에서는 원본 스키마의 열을 대상 스키마의 열에 매핑해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-126">In this scenario, you need to map columns from the source schema to columns from the destination schema.</span></span>

> [!TIP]
> <span data-ttu-id="fa9d8-127">SQL Server 또는 Azure SQL Database에서 Azure SQL Data Warehouse로 데이터를 복사할 때 테이블이 대상 저장소에 없을 경우 Data Factory는 원본의 스키마를 사용하여 자동 테이블 만들기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-127">When copying data from SQL Server or Azure SQL Database into Azure SQL Data Warehouse, if the table does not exist in the destination store, Data Factory support auto table creation using source's schema.</span></span> <span data-ttu-id="fa9d8-128">[Azure Data Factory를 사용하여 Azure SQL Data Warehouse 간 데이터 이동](./data-factory-azure-sql-data-warehouse-connector.md)에서 자세히 알아 보십시오.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-128">Learn more from [Move data to and from Azure SQL Data Warehouse using Azure Data Factory](./data-factory-azure-sql-data-warehouse-connector.md).</span></span>
>

<span data-ttu-id="fa9d8-129">드롭다운 목록을 사용하여 원본 스키마에서 대상 스키마의 열에 매핑할 열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-129">Use a drop-down list to select a column from the source schema to map to a column in the destination schema.</span></span> <span data-ttu-id="fa9d8-130">복사 마법사는 열 매핑에 대한 패턴을 파악하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-130">The Copy Wizard tries to understand your pattern for column mapping.</span></span> <span data-ttu-id="fa9d8-131">나머지 열에도 동일한 패턴을 적용하므로 스키마 매핑을 완료하기 위해 각 열을 개별적으로 선택할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-131">It applies the same pattern to the rest of the columns, so that you do not need to select each of the columns individually to complete the schema mapping.</span></span> <span data-ttu-id="fa9d8-132">원하는 경우 드롭다운 목록을 사용하여 열을 하나씩 매핑하면 이러한 매핑을 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-132">If you prefer, you can override these mappings by using the drop-down lists to map the columns one by one.</span></span> <span data-ttu-id="fa9d8-133">열을 더 많이 매핑할수록 패턴이 더 정확하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-133">The pattern becomes more accurate as you map more columns.</span></span> <span data-ttu-id="fa9d8-134">복사 마법사는 패턴을 지속적으로 업데이트하고, 궁극적으로는 도달하려는 열 매핑의 올바른 패턴에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-134">The Copy Wizard constantly updates the pattern, and ultimately reaches the right pattern for the column mapping you want to achieve.</span></span>     

![스키마 매핑](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a><span data-ttu-id="fa9d8-136">데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="fa9d8-136">Filtering data</span></span>
<span data-ttu-id="fa9d8-137">싱크 데이터 저장소에 복사해야 하는 데이터만 선택하도록 원본 데이터를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-137">You can filter source data to select only the data that needs to be copied to the sink data store.</span></span> <span data-ttu-id="fa9d8-138">필터링하면 싱크 데이터 저장소에 복사할 데이터 양이 줄고 이에 따라 복사 작업의 처리량이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-138">Filtering reduces the volume of the data to be copied to the sink data store and therefore enhances the throughput of the copy operation.</span></span> <span data-ttu-id="fa9d8-139">마법사에서는 SQL 쿼리 언어를 사용하여 관계형 데이터베이스의 데이터를 필터링하거나 [Data Factory 함수 및 변수](data-factory-functions-variables.md)를 사용하여 Azure Blob 폴더의 파일을 필터링할 수 있는 유연한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-139">It provides a flexible way to filter data in a relational database by using the SQL query language, or files in an Azure blob folder by using [Data Factory functions and variables](data-factory-functions-variables.md).</span></span>   

### <a name="filtering-of-data-in-a-database"></a><span data-ttu-id="fa9d8-140">데이터베이스 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="fa9d8-140">Filtering of data in a database</span></span>
<span data-ttu-id="fa9d8-141">다음 스크린샷은 `Text.Format` 함수와 `WindowStart` 변수를 사용하는 SQL 쿼리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-141">The following screenshot shows a SQL query using the `Text.Format` function and `WindowStart` variable.</span></span>

![식 유효성 검사](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a><span data-ttu-id="fa9d8-143">Azure Blob 폴더의 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="fa9d8-143">Filtering of data in an Azure blob folder</span></span>
<span data-ttu-id="fa9d8-144">폴더 경로의 변수를 사용하여 [시스템 변수](data-factory-functions-variables.md#data-factory-system-variables)를 기반으로 런타임 시 결정되는 폴더의 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-144">You can use variables in the folder path to copy data from a folder that is determined at runtime based on [system variables](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="fa9d8-145">지원되는 변수는 **{year}**, **{month}**, **{day}**, **{hour}**, **{minute}** 및 **{custom}**입니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-145">The supported variables are: **{year}**, **{month}**, **{day}**, **{hour}**, **{minute}**, and **{custom}**.</span></span> <span data-ttu-id="fa9d8-146">예를 들어 inputfolder/{year}/{month}/{day}와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-146">For example: inputfolder/{year}/{month}/{day}.</span></span>

<span data-ttu-id="fa9d8-147">다음과 같은 형식의 입력 폴더가 있다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-147">Suppose that you have input folders in the following format:</span></span>

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

<span data-ttu-id="fa9d8-148">**파일 또는 폴더**의 **찾아보기** 단추를 클릭하여 이러한 폴더(예: 2016->03->01->02)중 하나를 찾아서 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-148">Click the **Browse** button for **File or folder**, browse to one of these folders (for example, 2016->03->01->02), and click **Choose**.</span></span> <span data-ttu-id="fa9d8-149">텍스트 상자에 `2016/03/01/02`가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-149">You should see `2016/03/01/02` in the text box.</span></span> <span data-ttu-id="fa9d8-150">이제 **2016**을 **{year}**로, **03**을 **{month}**로, **01**을 **{day}**로, **02**를 **{hour}**로 바꾼 다음 **탭** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-150">Now, replace **2016** with **{year}**, **03** with **{month}**, **01** with **{day}**, and **02** with **{hour}**, and press the **Tab** key.</span></span> <span data-ttu-id="fa9d8-151">이러한 네 가지 변수의 형식을 선택하는 드롭다운 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-151">You should see drop-down lists to select the format for these four variables:</span></span>

![시스템 변수 사용](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

<span data-ttu-id="fa9d8-153">다음 스크린샷에 표시된 것처럼 **사용자 지정** 변수 및 모든 [지원되는 형식 문자열](https://msdn.microsoft.com/library/8kb3ddd4.aspx)도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-153">As shown in the following screenshot, you can also use a **custom** variable and any [supported format strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx).</span></span> <span data-ttu-id="fa9d8-154">해당 구조의 폴더를 선택하려면 먼저 **찾아보기** 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-154">To select a folder with that structure, use the **Browse** button first.</span></span> <span data-ttu-id="fa9d8-155">그런 다음 값을 **{custom}**으로 바꾸고, **탭** 키를 누르면 형식 문자열을 입력할 수 있는 텍스트 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-155">Then replace a value with **{custom}**, and press the **Tab** key to see the text box where you can type the format string.</span></span>     

![사용자 지정 변수 사용](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="scheduling-options"></a><span data-ttu-id="fa9d8-157">일정 옵션</span><span class="sxs-lookup"><span data-stu-id="fa9d8-157">Scheduling options</span></span>
<span data-ttu-id="fa9d8-158">복사 작업을 한 번만 또는 일정에 따라(시간별, 일별, 등) 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-158">You can run the copy operation once or on a schedule (hourly, daily, and so on).</span></span> <span data-ttu-id="fa9d8-159">이 두 가지 옵션은 온-프레미스, 클라우드 및 로컬 데스크톱 복사본을 포함한 환경의 다양한 커넥터에 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-159">Both of these options can be used for the breadth of the connectors across environments, including on-premises, cloud, and local desktop copy.</span></span>

<span data-ttu-id="fa9d8-160">일 회 복사 작업을 통해 원본에서 대상으로 한 번만 데이터를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-160">A one-time copy operation enables data movement from a source to a destination only once.</span></span> <span data-ttu-id="fa9d8-161">이는 모든 크기 및 지원되는 형식의 데이터에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-161">It applies to data of any size and any supported format.</span></span> <span data-ttu-id="fa9d8-162">예약 복사를 통해 미리 정해진 반복 주기에 따라 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-162">The scheduled copy allows you to copy data on a prescribed recurrence.</span></span> <span data-ttu-id="fa9d8-163">다양한 설정(예: 재시도, 시간 제한, 경고 등)을 사용하여 예약 복사를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-163">You can use rich settings (like retry, timeout, and alerts) to configure the scheduled copy.</span></span>

![일정 속성](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a><span data-ttu-id="fa9d8-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fa9d8-165">Next steps</span></span>
<span data-ttu-id="fa9d8-166">Data Factory 복사 마법사를 사용하여 복사 작업이 있는 파이프라인을 만드는 방법은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa9d8-166">For a quick walkthrough of using the Data Factory Copy Wizard to create a pipeline with Copy Activity, see [Tutorial: Create a pipeline using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>
