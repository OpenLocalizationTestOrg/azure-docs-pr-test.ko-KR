---
title: "호환되지 않는 행을 건너뛰어 Azure Data Factory 복사 작업에 내결함성 추가 | Microsoft Docs"
description: "복사 중에 호환되지 않는 행을 건너뛰어 Azure Data Factory 복사 작업에 내결함성을 추가하는 방법 알아보기"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e2a108752259d5da3b401666c6bdbaad13b7ea90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="a4ef4-103">호환되지 않는 행을 건너뛰어 복사 작업에 내결함성 추가</span><span class="sxs-lookup"><span data-stu-id="a4ef4-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="a4ef4-104">Azure Data Factory [복사 작업](data-factory-data-movement-activities.md)은 원본 및 싱크 데이터 저장소 간에 데이터를 복사할 때 호환되지 않는 행을 처리하는 2가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways to handle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="a4ef4-105">호환되지 않는 데이터가 나타날 때 복사 작업을 중단하고 실패한 것으로 처리할 수 있습니다(기본 동작).</span><span class="sxs-lookup"><span data-stu-id="a4ef4-105">You can abort and fail the copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="a4ef4-106">내결함성을 추가하고 호환되지 않는 데이터 행을 건너뛰어 모든 데이터를 계속 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-106">You can continue to copy all of the data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="a4ef4-107">또한 Azure Blob Storage에 호환되지 않는 행을 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-107">In addition, you can log the incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="a4ef4-108">그런 후 로그를 검토하여 실패의 원인을 파악하고, 데이터 원본에서 데이터를 수정하고, 복사 작업을 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-108">You can then examine the log to learn the cause for the failure, fix the data on the data source, and retry the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="a4ef4-109">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="a4ef4-109">Supported scenarios</span></span>
<span data-ttu-id="a4ef4-110">복사 작업은 호환되지 않는 데이터의 검색, 건너뛰기 및 로깅에 대한 다음 세 가지 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="a4ef4-111">**원본 데이터 형식 및 싱크 원시 형식 간의 비호환성**</span><span class="sxs-lookup"><span data-stu-id="a4ef4-111">**Incompatibility between the source data type and the sink native type**</span></span>

    <span data-ttu-id="a4ef4-112">예제: 3가지 **INT** 형식 열을 포함하는 스키마 정의를 사용하여 Blob Storage에 있는 CSV 파일의 데이터를 SQL Database로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-112">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="a4ef4-113">`123,456,789`와 같은 숫자 데이터를 포함하는 CSV 파일 행은 싱크 저장소에 성공적으로 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-113">The CSV file rows that contain numeric data, such as `123,456,789` are copied successfully to the sink store.</span></span> <span data-ttu-id="a4ef4-114">그러나 `123,456,abc`와 같은 숫자가 아닌 값을 포함하는 행을 호환되지 않는 것으로 감지하고 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-114">However, the rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="a4ef4-115">**원본과 싱크 간의 열 수 불일치**</span><span class="sxs-lookup"><span data-stu-id="a4ef4-115">**Mismatch in the number of columns between the source and the sink**</span></span>

    <span data-ttu-id="a4ef4-116">예제: 6개의 열이 포함된 스키마 정의를 사용하여 Blob Storage에 있는 CSV 파일의 데이터를 SQL Database로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-116">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="a4ef4-117">6개의 열이 포함된 CSV 파일 행은 싱크 저장소에 성공적으로 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-117">The CSV file rows that contain six columns are copied successfully to the sink store.</span></span> <span data-ttu-id="a4ef4-118">6개보다 많거나 적은 열을 포함하는 CSV 파일 행을 호환되지 않는 것으로 감지하고 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-118">The CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="a4ef4-119">**관계형 데이터베이스에 쓰는 중 기본 키 위반**</span><span class="sxs-lookup"><span data-stu-id="a4ef4-119">**Primary key violation when writing to a relational database**</span></span>

    <span data-ttu-id="a4ef4-120">예제: SQL Server에서 SQL Database로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-120">For example: Copy data from a SQL server to a SQL database.</span></span> <span data-ttu-id="a4ef4-121">기본 키가 싱크 SQL Database에 정의되어 있지만 이러한 기본 키가 원본 SQL Server에 정의되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-121">A primary key is defined in the sink SQL database, but no such primary key is defined in the source SQL server.</span></span> <span data-ttu-id="a4ef4-122">원본에 있는 중복된 행을 싱크로 복사할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-122">The duplicated rows that exist in the source cannot be copied to the sink.</span></span> <span data-ttu-id="a4ef4-123">복사 작업은 원본 데이터의 첫 번째 행만 싱크에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-123">Copy Activity copies only the first row of the source data into the sink.</span></span> <span data-ttu-id="a4ef4-124">중복된 기본 키 값을 포함하는 후속 원본 행을 호환되지 않는 것으로 감지하고 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-124">The subsequent source rows that contain the duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="a4ef4-125">구성</span><span class="sxs-lookup"><span data-stu-id="a4ef4-125">Configuration</span></span>
<span data-ttu-id="a4ef4-126">다음 예제에서는 복사 작업에서 호환되지 않는 행을 건너뛰도록 구성하기 위한 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-126">The following example provides a JSON definition to configure skipping the incompatible rows in Copy Activity:</span></span>

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| <span data-ttu-id="a4ef4-127">속성</span><span class="sxs-lookup"><span data-stu-id="a4ef4-127">Property</span></span> | <span data-ttu-id="a4ef4-128">설명</span><span class="sxs-lookup"><span data-stu-id="a4ef4-128">Description</span></span> | <span data-ttu-id="a4ef4-129">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="a4ef4-129">Allowed values</span></span> | <span data-ttu-id="a4ef4-130">필수</span><span class="sxs-lookup"><span data-stu-id="a4ef4-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a4ef4-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="a4ef4-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="a4ef4-132">복사 중 호환되지 않는 행을 건너뛸지 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="a4ef4-133">True</span><span class="sxs-lookup"><span data-stu-id="a4ef4-133">True</span></span><br/><span data-ttu-id="a4ef4-134">False(기본값)</span><span class="sxs-lookup"><span data-stu-id="a4ef4-134">False (default)</span></span> | <span data-ttu-id="a4ef4-135">아니요</span><span class="sxs-lookup"><span data-stu-id="a4ef4-135">No</span></span> |
| <span data-ttu-id="a4ef4-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="a4ef4-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="a4ef4-137">호환되지 않는 행을 기록하려는 경우 지정할 수 있는 속성 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-137">A group of properties that can be specified when you want to log the incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="a4ef4-138">아니요</span><span class="sxs-lookup"><span data-stu-id="a4ef4-138">No</span></span> |
| <span data-ttu-id="a4ef4-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="a4ef4-139">**linkedServiceName**</span></span> | <span data-ttu-id="a4ef4-140">건너뛰는 행을 포함하는 로그를 저장하는 Azure Storage의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-140">The linked service of Azure Storage to store the log that contains the skipped rows.</span></span> | <span data-ttu-id="a4ef4-141">로그 파일을 저장하는 데 사용할 저장소 인스턴스를 참조하는 [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) 또는 [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) 연결된 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-141">The name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers to the storage instance that you want to use to store the log file.</span></span> | <span data-ttu-id="a4ef4-142">아니요</span><span class="sxs-lookup"><span data-stu-id="a4ef4-142">No</span></span> |
| <span data-ttu-id="a4ef4-143">**path**</span><span class="sxs-lookup"><span data-stu-id="a4ef4-143">**path**</span></span> | <span data-ttu-id="a4ef4-144">건너뛴 행을 포함하는 로그 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-144">The path of the log file that contains the skipped rows.</span></span> | <span data-ttu-id="a4ef4-145">호환되지 않는 데이터를 기록하는 데 사용하려는 Blob Storage 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-145">Specify the Blob storage path that you want to use to log the incompatible data.</span></span> <span data-ttu-id="a4ef4-146">경로를 지정하지 않으면 서비스가 대신 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-146">If you do not provide a path, the service creates a container for you.</span></span> | <span data-ttu-id="a4ef4-147">아니요</span><span class="sxs-lookup"><span data-stu-id="a4ef4-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="a4ef4-148">모니터링</span><span class="sxs-lookup"><span data-stu-id="a4ef4-148">Monitoring</span></span>
<span data-ttu-id="a4ef4-149">복사 작업 실행이 완료되면 모니터링 섹션에서 건너뛴 행의 수를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-149">After the copy activity run completes, you can see the number of skipped rows in the monitoring section:</span></span>

![건너뛰는 호환되지 않는 행 모니터링](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="a4ef4-151">호환되지 않는 행을 기록하도록 구성한 경우 `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` 경로에서 해당 로그 파일을 찾을 수 있습니다. 이 로그 파일에서 건너뛴 행과 비호환성의 근본 원인을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-151">If you configure to log the incompatible rows, you can find the log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In the log file, you can see the rows that were skipped and the root cause of the incompatibility.</span></span>

<span data-ttu-id="a4ef4-152">원본 데이터와 해당 오류가 파일에 모두 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-152">Both the original data and the corresponding error are logged in the file.</span></span> <span data-ttu-id="a4ef4-153">로그 파일 내용의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-153">An example of the log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' to type 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. The duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="a4ef4-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a4ef4-154">Next steps</span></span>
<span data-ttu-id="a4ef4-155">Azure Data Factory 복사 작업에 대해 자세히 알아보려면 [복사 작업을 사용하여 데이터 이동](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4ef4-155">To learn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>