---
title: "복사 마법사를 사용하여 데이터를 쉽게 복사 - Azure | Microsoft Docs"
description: "Data Factory 복사 마법사를 사용하여 지원되는 데이터 소스의 데이터를 싱크로 복사하는 방법에 대해 알아보세요."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f904972f-cd33-48db-9755-2b3196ae4168
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 282cb4484f8209e6bb36f2a02d7a897f1ba0aa8e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="copy-or-move-data-easily-with-azure-data-factory-copy-wizard"></a><span data-ttu-id="fc990-103">Azure Data Factory 복사 마법사를 사용하여 데이터를 쉽게 복사 또는 이동</span><span class="sxs-lookup"><span data-stu-id="fc990-103">Copy or move data easily with Azure Data Factory Copy Wizard</span></span>
<span data-ttu-id="fc990-104">Azure Data Factory Copy Wizard는 일반적으로 종단 간 데이터 통합 시나리오의 첫 번째 단계인 데이터 수집 프로세스를 용이하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-104">The Azure Data Factory Copy Wizard is to ease the process of ingesting data, which is usually a first step in an end-to-end data integration scenario.</span></span> <span data-ttu-id="fc990-105">Azure Data Factory Copy Wizard를 진행할 때는 연결된 서비스, 데이터 집합 및 파이프라인에 대한 JSON 정의를 이해할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-105">When going through the Azure Data Factory Copy Wizard, you do not need to understand any JSON definitions for linked services, datasets, and pipelines.</span></span> <span data-ttu-id="fc990-106">그러나 마법사의 모든 단계를 완료한 후 선택한 데이터 원본에서 선택한 대상으로 데이터를 복사하는 파이프라인이 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-106">However, after you complete all the steps in the wizard, the wizard automatically creates a pipeline to copy data from the selected data source to the selected destination.</span></span> <span data-ttu-id="fc990-107">또한 Copy Wizard를 사용하면 작성 당시에 수집 중인 데이터의 유효성을 검사할 수 있으므로 특히 데이터 원본에서 데이터를 처음 수집하는 경우 많은 시간이 절약됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-107">In addition, the Copy Wizard helps you to validate the data being ingested at the time of authoring, which saves much of your time, especially when you are ingesting data for the first time from the data source.</span></span> <span data-ttu-id="fc990-108">복사 마법사를 시작하려면 Data Factory 홈 페이지에서 **데이터 복사** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-108">To start the Copy Wizard, click the **Copy data** tile on the home page of your data factory.</span></span>

![복사 마법사](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="an-intuitive-wizard-for-copying-data"></a><span data-ttu-id="fc990-110">데이터를 복사할 수 있는 직관적인 마법사</span><span class="sxs-lookup"><span data-stu-id="fc990-110">An intuitive wizard for copying data</span></span>
<span data-ttu-id="fc990-111">이 마법사를 사용하면 다양한 원본에서 대상으로 몇 분만에 데이터를 쉽게 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-111">This wizard allows you to easily move data from a wide variety of sources to destinations in minutes.</span></span> <span data-ttu-id="fc990-112">마법사를 거친 후 종속 Data Factory 엔터티(연결된 서비스 및 데이터 집합)와 함께 복사 작업이 있는 파이프라인이 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-112">After going through the wizard, a pipeline with a copy activity is automatically created for you along with dependent Data Factory entities (linked services and datasets).</span></span> <span data-ttu-id="fc990-113">파이프라인을 만드는 데 필요한 추가 단계가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-113">No additional steps are required to create the pipeline.</span></span>   

![데이터 원본 선택](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> <span data-ttu-id="fc990-115">Azure Blob에서 Azure SQL Database 테이블로 데이터를 복사하기 위한 샘플 파이프라인을 만드는 단계별 지침은 [Copy Wizard 자습서](data-factory-copy-data-wizard-tutorial.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc990-115">See [Copy Wizard tutorial](data-factory-copy-data-wizard-tutorial.md) article for step-by-step instructions to create a sample pipeline to copy data from an Azure blob to an Azure SQL Database table.</span></span> 
> 
> 

<span data-ttu-id="fc990-116">이 마법사는 처음부터 빅 데이터를 염두에 두고 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-116">The wizard is designed with big data in mind from the start.</span></span> <span data-ttu-id="fc990-117">Copy Data Wizard를 사용하여 수백 개의 폴더, 파일 또는 테이블을 이동하는 Data Factory 파이프라인을 간단하고 효율적으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-117">It is simple and efficient to author Data Factory pipelines that move hundreds of folders, files, or tables using the Copy Data wizard.</span></span> <span data-ttu-id="fc990-118">이 마법사는 자동 데이터 미리 보기, 스키마 캡처 및 매핑, 데이터 필터링이라는 세 가지 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-118">The wizard supports the following three features: Automatic data preview, schema capture and mapping, and filtering data.</span></span> 

## <a name="automatic-data-preview"></a><span data-ttu-id="fc990-119">자동 데이터 미리 보기</span><span class="sxs-lookup"><span data-stu-id="fc990-119">Automatic data preview</span></span>
<span data-ttu-id="fc990-120">복사 마법사를 사용하면 선택한 데이터 원본에서 데이터의 일부를 검토하여 데이터가 복사하려는 올바른 데이터인지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-120">The copy wizard allows you to review part of the data from the selected data source for you to validate whether the data it is the right data you want to copy.</span></span> <span data-ttu-id="fc990-121">또한 원본 데이터가 텍스트 파일에 있는 경우 복사 마법사는 텍스트 파일을 구문 분석하여 행 및 열 구분 기호와 스키마를 자동으로 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-121">In addition, if the source data is in a text file, the copy wizard parses the text file to learn row and column delimiters, and schema automatically.</span></span> 

![파일 형식 설정](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a><span data-ttu-id="fc990-123">스키마 캡처 및 매핑</span><span class="sxs-lookup"><span data-stu-id="fc990-123">Schema capture and mapping</span></span>
<span data-ttu-id="fc990-124">입력 데이터의 스키마는 경우에 따라 출력 데이터의 스키마와 일치하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-124">The schema of input data may not match the schema of output data in some cases.</span></span> <span data-ttu-id="fc990-125">이 시나리오에서는 원본 스키마의 열을 대상 스키마의 열에 매핑해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-125">In this scenario, you need to map columns from the source schema to columns from the destination schema.</span></span> 

<span data-ttu-id="fc990-126">복사 마법사는 원본 스키마의 열을 대상 스키마의 열에 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-126">The copy wizard automatically maps columns in the source schema to columns in the destination schema.</span></span> <span data-ttu-id="fc990-127">드롭다운 목록을 사용하여 매핑을 재정의하거나 데이터를 복사하는 동안 열을 건너뛸지 여부를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-127">You can override the mappings by using the drop-down lists (or) specify whether a column needs to be skipped while copying the data.</span></span>   

![스키마 매핑](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a><span data-ttu-id="fc990-129">데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="fc990-129">Filtering data</span></span>
<span data-ttu-id="fc990-130">마법사를 통해 대상/싱크 데이터 저장소에 복사해야 하는 데이터만 선택하도록 원본 데이터를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-130">The wizard allows you to filter source data to select only the data that needs to be copied to the destination/sink data store.</span></span> <span data-ttu-id="fc990-131">필터링하면 싱크 데이터 저장소에 복사할 데이터의 양이 줄어들기 때문에 복사 작업의 처리량이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-131">Filtering reduces the volume of the data to be copied to the sink data store and therefore enhances the throughput of the copy operation.</span></span> <span data-ttu-id="fc990-132">마법사에서는 SQL 쿼리 언어를 사용하여 관계형 데이터베이스의 데이터를 필터링하거나 [Data Factory 함수 및 변수](data-factory-functions-variables.md)를 사용하여 Azure blob 폴더의 파일을 필터링할 수 있는 유연한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-132">It provides a flexible way to filter data in a relational database by using SQL query language (or) files in an Azure blob folder by using [Data Factory functions and variables](data-factory-functions-variables.md).</span></span>   

### <a name="filtering-of-data-in-a-database"></a><span data-ttu-id="fc990-133">데이터베이스의 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="fc990-133">Filtering of data in a database</span></span>
<span data-ttu-id="fc990-134">이 예제에서 SQL 쿼리는 `Text.Format` 함수 및 `WindowStart` 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-134">In the example, the SQL query uses the `Text.Format` function and `WindowStart` variable.</span></span> 

![식 유효성 검사](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a><span data-ttu-id="fc990-136">Azure Blob 폴더의 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="fc990-136">Filtering of data in an Azure blob folder</span></span>
<span data-ttu-id="fc990-137">폴더 경로의 변수를 사용하여 [시스템 변수](data-factory-functions-variables.md#data-factory-system-variables)를 기반으로 런타임 시 결정되는 폴더의 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-137">You can use variables in the folder path to copy data from a folder that is determined at runtime based on [system variables](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="fc990-138">지원되는 변수는 **{year}**, **{month}**, **{day}**, **{hour}**, **{minute}** 및 **{custom}**입니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-138">The supported variables are: **{year}**, **{month}**, **{day}**, **{hour}**, **{minute}**, and **{custom}**.</span></span> <span data-ttu-id="fc990-139">예: inputfolder/{year}/{month}/{day}.</span><span class="sxs-lookup"><span data-stu-id="fc990-139">Example: inputfolder/{year}/{month}/{day}.</span></span>

<span data-ttu-id="fc990-140">다음과 같은 형식의 입력 폴더가 있다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-140">Suppose that you have input folders in the following format:</span></span>

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

<span data-ttu-id="fc990-141">**파일 또는 폴더**의 **찾아보기** 단추를 클릭하여 이러한 폴더(예: 2016->03->01->02)중 하나를 찾아서 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-141">Click the **Browse** button for **File or folder**, browse to one of these folders (for example, 2016->03->01->02), and click **Choose**.</span></span> <span data-ttu-id="fc990-142">텍스트 상자에 `2016/03/01/02`가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-142">You should see `2016/03/01/02` in the text box.</span></span> <span data-ttu-id="fc990-143">이제 **2016**을 **{year}**로, **03**을 **{month}**로, **01**을 **{day}**로, **02**를 **{hour}**로 바꾸고 탭을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-143">Now, replace **2016** with **{year}**, **03** with **{month}**, **01** with **{day}**, and **02** with **{hour}**, and press Tab.</span></span> <span data-ttu-id="fc990-144">이러한 네 가지 변수의 형식을 선택하는 드롭다운 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-144">You should see drop-down lists to select the format for these four variables:</span></span>

![시스템 변수 사용](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

<span data-ttu-id="fc990-146">다음 스크린샷에 표시된 것처럼 **사용자 지정** 변수 및 모든 [지원되는 형식 문자열](https://msdn.microsoft.com/library/8kb3ddd4.aspx)도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-146">As shown in the following screenshot, you can also use a **custom** variable and any [supported format strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx).</span></span> <span data-ttu-id="fc990-147">해당 구조의 폴더를 선택하려면 먼저 **찾아보기** 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-147">To select a folder with that structure, use the **Browse** button first.</span></span> <span data-ttu-id="fc990-148">그런 다음 값을 **{custom}**으로 바꾸고, 탭을 누르면 형식 문자열을 입력할 수 있는 텍스트 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-148">Then replace a value with **{custom}**, and press Tab to see the text box where you can type the format string.</span></span>     

![사용자 지정 변수 사용](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="support-for-diverse-data-and-object-types"></a><span data-ttu-id="fc990-150">다양한 데이터 및 개체 유형 지원</span><span class="sxs-lookup"><span data-stu-id="fc990-150">Support for diverse data and object types</span></span>
<span data-ttu-id="fc990-151">복사 마법사를 사용하여 효율적으로 수백 개의 폴더, 파일 또는 테이블을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-151">By using the Copy Wizard, you can efficiently move hundreds of folders, files, or tables.</span></span>

![데이터를 복사할 테이블 선택](./media/data-factory-copy-wizard/select-tables-to-copy-data.png)

## <a name="scheduling-options"></a><span data-ttu-id="fc990-153">일정 옵션</span><span class="sxs-lookup"><span data-stu-id="fc990-153">Scheduling options</span></span>
<span data-ttu-id="fc990-154">복사 작업을 한 번만 또는 일정에 따라(시간별, 일별, 등) 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-154">You can run the copy operation once or on a schedule (hourly, daily, and so on).</span></span> <span data-ttu-id="fc990-155">온-프레미스, 클라우드 및 로컬 데스크톱 복사에 걸쳐 광범위한 커넥터에 이 두 옵션을 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-155">Both of these options can be used for the breadth of the connectors across on-premises, cloud, and local desktop copy.</span></span>

<span data-ttu-id="fc990-156">일 회 복사 작업을 통해 원본에서 대상으로 한 번만 데이터를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-156">A one-time copy operation enables data movement from a source to a destination only once.</span></span> <span data-ttu-id="fc990-157">이는 모든 크기 및 지원되는 형식의 데이터에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-157">It applies to data of any size and any supported format.</span></span> <span data-ttu-id="fc990-158">예약 복사를 통해 미리 정해진 반복 주기에 따라 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-158">The scheduled copy allows you to copy data on a prescribed recurrence.</span></span> <span data-ttu-id="fc990-159">다양한 설정(예: 재시도, 시간 제한, 경고 등)을 사용하여 예약 복사를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc990-159">You can use rich settings (like retry, timeout, and alerts) to configure the scheduled copy.</span></span>

![일정 속성](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a><span data-ttu-id="fc990-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fc990-161">Next steps</span></span>
<span data-ttu-id="fc990-162">Data Factory 복사 마법사를 사용하여 복사 작업이 있는 파이프라인을 만드는 방법은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc990-162">For a quick walkthrough of using the Data Factory Copy Wizard to create a pipeline with Copy Activity, see [Tutorial: Create a pipeline using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

