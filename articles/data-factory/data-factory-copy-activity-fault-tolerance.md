---
title: "aaaAdd 내결함성 Azure 데이터 팩터리 복사 작업에서 호환 되지 않는 행을 건너뛰는 여 | Microsoft Docs"
description: "어떻게 tooadd 내결함성 Azure 데이터 팩터리 복사 작업에 복사 하는 동안 호환 되지 않는 행을 건너뛰는 여 알아봅니다"
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
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="91d84-103">호환되지 않는 행을 건너뛰어 복사 작업에 내결함성 추가</span><span class="sxs-lookup"><span data-stu-id="91d84-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="91d84-104">Azure Data Factory [복사 작업](data-factory-data-movement-activities.md) 원본 및 싱크 데이터 저장소 간에 데이터를 복사 하는 경우 두 가지 방법으로 toohandle 호환 되지 않는 행을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways toohandle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="91d84-105">중단 하 고 hello 복사 실패 작업에서 데이터가 호환 되지 않는 경우에 (기본 동작) 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-105">You can abort and fail hello copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="91d84-106">Toocopy 계속 내결함성 추가 호환 되지 않는 데이터 행을 건너뛰는 hello 데이터의 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-106">You can continue toocopy all of hello data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="91d84-107">또한 Azure Blob 저장소에 hello 호환 되지 않는 행을 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-107">In addition, you can log hello incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="91d84-108">다음 검사 hello 실패에 대 한 hello 로그 toolearn hello 원인, hello 데이터 원본에 대해 hello 데이터를 수정 하 고 수 hello 복사 작업을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="91d84-108">You can then examine hello log toolearn hello cause for hello failure, fix hello data on hello data source, and retry hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="91d84-109">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="91d84-109">Supported scenarios</span></span>
<span data-ttu-id="91d84-110">복사 작업은 호환되지 않는 데이터의 검색, 건너뛰기 및 로깅에 대한 다음 세 가지 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="91d84-111">**Hello 원본 데이터 형식과 hello 싱크 네이티브 형식 간의 비 호환성**</span><span class="sxs-lookup"><span data-stu-id="91d84-111">**Incompatibility between hello source data type and hello sink native type**</span></span>

    <span data-ttu-id="91d84-112">예: Blob 저장소 tooa SQL에서에서 CSV 파일에서 데이터 복사 데이터베이스 세 개 포함 하는 스키마 정의로 **INT** 유형 열입니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-112">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="91d84-113">와 같은 숫자 데이터를 포함 하는 CSV 파일 행 hello `123,456,789` 성공적으로 복사 됩니다 toohello 싱크 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-113">hello CSV file rows that contain numeric data, such as `123,456,789` are copied successfully toohello sink store.</span></span> <span data-ttu-id="91d84-114">그러나 같은 숫자가 아닌 값을 포함 하는 행을 hello `123,456,abc` 호환 되지 않음으로 감지 하 고는 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-114">However, hello rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="91d84-115">**Hello hello 원본 및 싱크 hello 사이 열 수가 일치 하지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="91d84-115">**Mismatch in hello number of columns between hello source and hello sink**</span></span>

    <span data-ttu-id="91d84-116">예: 6 개의 열이 포함 된 스키마 정의와 함께 데이터베이스에서 Blob 저장소 tooa SQL CSV 파일에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-116">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="91d84-117">hello 6 개의 열이 포함 된 행은 CSV 파일 복사 성공적으로 toohello 싱크 저장소.</span><span class="sxs-lookup"><span data-stu-id="91d84-117">hello CSV file rows that contain six columns are copied successfully toohello sink store.</span></span> <span data-ttu-id="91d84-118">hello CSV 파일 행 수를 늘리거나 6 개 미만의 열이 포함 된 호환 되지 않는 것으로 확인 된 및 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-118">hello CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="91d84-119">**기본 키 위반 tooa 관계형 데이터베이스에 쓸 때**</span><span class="sxs-lookup"><span data-stu-id="91d84-119">**Primary key violation when writing tooa relational database**</span></span>

    <span data-ttu-id="91d84-120">예: SQL server tooa SQL 데이터베이스에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-120">For example: Copy data from a SQL server tooa SQL database.</span></span> <span data-ttu-id="91d84-121">Hello 싱크 SQL 데이터베이스에 기본 키가 정의 하지만 이러한 기본 키 hello 원본 SQL server에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-121">A primary key is defined in hello sink SQL database, but no such primary key is defined in hello source SQL server.</span></span> <span data-ttu-id="91d84-122">hello 원본에 존재 하는 hello 중복 행 복사 toohello 싱크 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-122">hello duplicated rows that exist in hello source cannot be copied toohello sink.</span></span> <span data-ttu-id="91d84-123">복사 활동 hello 싱크 hello 원본 데이터의 첫 번째 행 hello만 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-123">Copy Activity copies only hello first row of hello source data into hello sink.</span></span> <span data-ttu-id="91d84-124">hello 중복 hello 기본 키 값을 포함 하는 후속 소스 행 호환 되지 않는 것으로 검색 되 고은 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-124">hello subsequent source rows that contain hello duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="91d84-125">구성</span><span class="sxs-lookup"><span data-stu-id="91d84-125">Configuration</span></span>
<span data-ttu-id="91d84-126">hello 다음 예에서는 hello 복사 작업에서 호환 되지 않는 행을 건너뛰는 JSON 정의 tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="91d84-126">hello following example provides a JSON definition tooconfigure skipping hello incompatible rows in Copy Activity:</span></span>

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

| <span data-ttu-id="91d84-127">속성</span><span class="sxs-lookup"><span data-stu-id="91d84-127">Property</span></span> | <span data-ttu-id="91d84-128">설명</span><span class="sxs-lookup"><span data-stu-id="91d84-128">Description</span></span> | <span data-ttu-id="91d84-129">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="91d84-129">Allowed values</span></span> | <span data-ttu-id="91d84-130">필수</span><span class="sxs-lookup"><span data-stu-id="91d84-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="91d84-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="91d84-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="91d84-132">복사 중 호환되지 않는 행을 건너뛸지 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="91d84-133">True</span><span class="sxs-lookup"><span data-stu-id="91d84-133">True</span></span><br/><span data-ttu-id="91d84-134">False(기본값)</span><span class="sxs-lookup"><span data-stu-id="91d84-134">False (default)</span></span> | <span data-ttu-id="91d84-135">아니요</span><span class="sxs-lookup"><span data-stu-id="91d84-135">No</span></span> |
| <span data-ttu-id="91d84-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="91d84-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="91d84-137">될 수 있는 속성의 그룹이 toolog hello 호환 되지 않는 행을 할 때 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-137">A group of properties that can be specified when you want toolog hello incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="91d84-138">아니요</span><span class="sxs-lookup"><span data-stu-id="91d84-138">No</span></span> |
| <span data-ttu-id="91d84-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="91d84-139">**linkedServiceName**</span></span> | <span data-ttu-id="91d84-140">hello는 hello 건너뛴 행이 포함 된 Azure 저장소 toostore hello 로그의 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-140">hello linked service of Azure Storage toostore hello log that contains hello skipped rows.</span></span> | <span data-ttu-id="91d84-141">hello 이름은 [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) 또는 [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) toouse toostore hello 로그 파일을 사용 하지 않겠다고 toohello 저장소 인스턴스가 참조 하는 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-141">hello name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers toohello storage instance that you want toouse toostore hello log file.</span></span> | <span data-ttu-id="91d84-142">아니요</span><span class="sxs-lookup"><span data-stu-id="91d84-142">No</span></span> |
| <span data-ttu-id="91d84-143">**path**</span><span class="sxs-lookup"><span data-stu-id="91d84-143">**path**</span></span> | <span data-ttu-id="91d84-144">hello 경로 hello를 포함 하는 hello 로그 파일의 행을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-144">hello path of hello log file that contains hello skipped rows.</span></span> | <span data-ttu-id="91d84-145">Hello toouse toolog hello 호환 되지 않는 데이터를 지정 하는 Blob 저장소 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-145">Specify hello Blob storage path that you want toouse toolog hello incompatible data.</span></span> <span data-ttu-id="91d84-146">경로 제공 하지 않으면 hello 서비스 사용자에 대 한 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-146">If you do not provide a path, hello service creates a container for you.</span></span> | <span data-ttu-id="91d84-147">아니요</span><span class="sxs-lookup"><span data-stu-id="91d84-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="91d84-148">모니터링</span><span class="sxs-lookup"><span data-stu-id="91d84-148">Monitoring</span></span>
<span data-ttu-id="91d84-149">Hello 복사 작업 실행이 완료 되 면 hello hello 보고서는 모니터링 섹션의에서 건너뛴된 행 수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-149">After hello copy activity run completes, you can see hello number of skipped rows in hello monitoring section:</span></span>

![건너뛰는 호환되지 않는 행 모니터링](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="91d84-151">Toolog hello 호환 되지 않는 행을 구성 하는 경우에이 경로에 hello 로그 파일을 찾을 수 있습니다: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` hello 로그 파일에 해당 하는 hello 행 파악 하 고 hello 비 호환성의 근본 원인을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-151">If you configure toolog hello incompatible rows, you can find hello log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In hello log file, you can see hello rows that were skipped and hello root cause of hello incompatibility.</span></span>

<span data-ttu-id="91d84-152">Hello 원래 데이터와 해당 오류 hello hello 파일에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-152">Both hello original data and hello corresponding error are logged in hello file.</span></span> <span data-ttu-id="91d84-153">Hello 로그 파일 콘텐츠의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-153">An example of hello log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="91d84-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="91d84-154">Next steps</span></span>
<span data-ttu-id="91d84-155">Azure 데이터 팩터리 복사 작업에 대해 자세히 toolearn 참조 [복사 작업을 사용 하 여 데이터를 이동](data-factory-data-movement-activities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="91d84-155">toolearn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>
