---
title: "많은 양의 오프 라인 메서드를 사용 하 여 데이터 레이크 저장소로 데이터를 aaaUpload | Microsoft Docs"
description: "사용 하 여 hello Azure 저장소에서 AdlCopy 도구 toocopy 데이터 레이크 저장소 tooData blob"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 45321f6a-179f-4ee4-b8aa-efa7745b8eb6
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 42ef75142a26ebfab05d89614782a54c244c4bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a><span data-ttu-id="5b73a-103">데이터 tooData 레이크 저장소의 오프 라인 복사본에 대 한 hello Azure 가져오기/내보내기 서비스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5b73a-103">Use hello Azure Import/Export service for offline copy of data tooData Lake Store</span></span>
<span data-ttu-id="5b73a-104">이 문서에서는 알아봅니다 toocopy 대규모 데이터 설정 하는 방법 (> 200GB) hello와 같은 오프 라인 복사 방법을 사용 하 여 Azure 데이터 레이크 저장소에 [Azure 가져오기/내보내기 서비스](../storage/common/storage-import-export-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-104">In this article, you'll learn how toocopy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like hello [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="5b73a-105">특히,이 문서의 예제로 사용 하는 hello 파일은 339,420,860,416 바이트 또는 디스크에 약 319 g B입니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-105">Specifically, hello file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="5b73a-106">이 파일을 319GB.tsv라고 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="5b73a-107">Azure 가져오기/내보내기 서비스 hello tootransfer 많은 양의 데이터를 안전 하 게 전달 하드 디스크에서 Blob 저장소 tooAzure 드라이브 tooan Azure 데이터 센터 보다 상세하게 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-107">hello Azure Import/Export service helps you tootransfer large amounts of data more securely tooAzure Blob storage by shipping hard disk drives tooan Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b73a-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5b73a-108">Prerequisites</span></span>
<span data-ttu-id="5b73a-109">시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-109">Before you begin, you must have hello following:</span></span>

* <span data-ttu-id="5b73a-110">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="5b73a-110">**An Azure subscription**.</span></span> <span data-ttu-id="5b73a-111">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b73a-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5b73a-112">**Azure Storage 계정**</span><span class="sxs-lookup"><span data-stu-id="5b73a-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="5b73a-113">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="5b73a-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="5b73a-114">방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5b73a-114">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-hello-data"></a><span data-ttu-id="5b73a-115">Hello 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="5b73a-115">Preparing hello data</span></span>
<span data-ttu-id="5b73a-116">나누기 hello 데이터 파일 toobe hello 가져오기/내보내기 서비스를 사용 하기 전에 전송 **200GB 미만 않은 복사본에** 크기에서입니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-116">Before using hello Import/Export service, break hello data file toobe transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="5b73a-117">200GB 보다 큰 파일 hello 가져오기 도구를 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-117">hello import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="5b73a-118">이 자습서에서는 각 100GB의 청크로 hello 파일을 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-118">In this tutorial, we split hello file into chunks of 100 GB each.</span></span> <span data-ttu-id="5b73a-119">[Cygwin](https://cygwin.com/install.html)을 사용하면 이렇게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="5b73a-120">Cygwin은 Linux 명령을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="5b73a-121">이 경우 다음 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-121">In this case, use hello following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="5b73a-122">hello split 작업 이름 다음 hello로 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-122">hello split operation creates files with hello following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="5b73a-123">데이터와 함께 디스크 준비</span><span class="sxs-lookup"><span data-stu-id="5b73a-123">Get disks ready with data</span></span>
<span data-ttu-id="5b73a-124">Hello 지침에 따라 [hello Azure 가져오기/내보내기 서비스를 사용 하 여](../storage/common/storage-import-export-service.md) (hello 아래 **드라이브를 준비** 섹션) tooprepare 하드 드라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-124">Follow hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Prepare your drives** section) tooprepare your hard drives.</span></span> <span data-ttu-id="5b73a-125">다음은 전체 순서 hello:</span><span class="sxs-lookup"><span data-stu-id="5b73a-125">Here's hello overall sequence:</span></span>

1. <span data-ttu-id="5b73a-126">Hello Azure 가져오기/내보내기 서비스에 사용 되는 hello 요구 사항 toobe 충족 하는 하드 디스크를 조달할 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-126">Procure a hard disk that meets hello requirement toobe used for hello Azure Import/Export service.</span></span>
2. <span data-ttu-id="5b73a-127">Azure 저장소 계정이 배송된 toohello Azure 데이터 센터 않아 hello 데이터 복사 될 위치를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-127">Identify an Azure storage account where hello data will be copied after it is shipped toohello Azure datacenter.</span></span>
3. <span data-ttu-id="5b73a-128">사용 하 여 hello [Azure 가져오기/내보내기 도구](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-128">Use hello [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="5b73a-129">Toouse 도구 hello 하는 방법을 보여 주는 샘플 코드 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-129">Here's a sample snippet that shows how toouse hello tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="5b73a-130">참조 [hello Azure 가져오기/내보내기 서비스를 사용 하 여](../storage/common/storage-import-export-service.md) 더 많은 샘플 조각에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-130">See [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="5b73a-131">hello 앞의 명령은 저널을 만듭니다는 hello에서 파일 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-131">hello preceding command creates a journal file at hello specified location.</span></span> <span data-ttu-id="5b73a-132">이 저널 파일 toocreate hello에서 가져오기 작업을 사용 하 여 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-132">Use this journal file toocreate an import job from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="5b73a-133">가져오기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="5b73a-133">Create an import job</span></span>
<span data-ttu-id="5b73a-134">지침에 hello를 사용 하 여 이제는 가져오기 작업을 만들 수 있습니다 [hello Azure 가져오기/내보내기 서비스를 사용 하 여](../storage/common/storage-import-export-service.md) (hello 아래 **hello 가져오기 작업 만들기** 섹션).</span><span class="sxs-lookup"><span data-stu-id="5b73a-134">You can now create an import job by using hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Create hello Import job** section).</span></span> <span data-ttu-id="5b73a-135">이 가져오기 작업에 대 한 기타 세부 정보 또한 제공할 hello 디스크 드라이브를 준비 하는 동안 만든 hello 저널 파일.</span><span class="sxs-lookup"><span data-stu-id="5b73a-135">For this import job, with other details, also provide hello journal file created while preparing hello disk drives.</span></span>

## <a name="physically-ship-hello-disks"></a><span data-ttu-id="5b73a-136">Hello 디스크 배달</span><span class="sxs-lookup"><span data-stu-id="5b73a-136">Physically ship hello disks</span></span>
<span data-ttu-id="5b73a-137">이제 hello 디스크 tooan Azure 데이터 센터를 물리적으로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-137">You can now physically ship hello disks tooan Azure datacenter.</span></span> <span data-ttu-id="5b73a-138">여기에 hello 데이터가 hello 가져오기 작업을 만드는 동안 제공한 toohello Azure 저장소 blob 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-138">There, hello data is copied over toohello Azure Storage blobs you provided while creating hello import job.</span></span> <span data-ttu-id="5b73a-139">또한 hello 작업을 만드는 동안 정보를 나중에 추적 tooprovide hello를 선택한 경우 이제 다시 할 수 있습니다 tooyour 가져오기 작업 및 update hello 추적 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-139">Also, while creating hello job, if you opted tooprovide hello tracking information later, you can now go back tooyour import job and update hello tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a><span data-ttu-id="5b73a-140">Azure 저장소 blob tooAzure 데이터 레이크 저장소에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-140">Copy data from Azure Storage blobs tooAzure Data Lake Store</span></span>
<span data-ttu-id="5b73a-141">Hello의 hello 상태 후 가져오기 작업이 완료 될, hello 데이터를 지정한 hello Azure 저장소 blob에 사용할 수 있는지 여부를 확인할 수 있습니다를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-141">After hello status of hello import job shows that it's completed, you can verify whether hello data is available in hello Azure Storage blobs you had specified.</span></span> <span data-ttu-id="5b73a-142">다양 한 메서드 toomove hello 데이터로 tooAzure 데이터 레이크 저장소 blob을 유도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-142">You can then use a variety of methods toomove that data from hello blobs tooAzure Data Lake Store.</span></span> <span data-ttu-id="5b73a-143">모든 데이터를 업로드 하기 위한 사용 가능한 옵션 hello, 참조 [데이터 레이크 저장소로 데이터를 수집 하는 방법](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-143">For all hello available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="5b73a-144">이 섹션에서는 제공 hello JSON 정의 데이터를 복사 하기 위한 toocreate Azure 데이터 팩터리 파이프라인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-144">In this section, we provide you with hello JSON definitions that you can use toocreate an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="5b73a-145">Hello에서 이러한 JSON 정의 사용할 수 있습니다 [Azure 포털](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), 또는 [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), 또는 [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-145">You can use these JSON definitions from hello [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="5b73a-146">원본에 연결된 서비스(Azure Storage Blob)</span><span class="sxs-lookup"><span data-stu-id="5b73a-146">Source linked service (Azure Storage blob)</span></span>
````
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
````

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="5b73a-147">대상에 연결된 서비스(Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="5b73a-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' tooallow this data factory and hello activities it runs tooaccess this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from hello OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="5b73a-148">입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="5b73a-148">Input data set</span></span>
````
{
    "name": "InputDataSet",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "importcontainer/vf1/"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
````
### <a name="output-data-set"></a><span data-ttu-id="5b73a-149">출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="5b73a-149">Output data set</span></span>
````
{
"name": "OutputDataSet",
"properties": {
  "published": false,
  "type": "AzureDataLakeStore",
  "linkedServiceName": "AzureDataLakeStoreLinkedService",
  "typeProperties": {
    "folderPath": "/importeddatafeb8job/"
    },
  "availability": {
    "frequency": "Hour",
    "interval": 1
    }
  }
}
````
### <a name="pipeline-copy-activity"></a><span data-ttu-id="5b73a-150">파이프라인(복사 작업)</span><span class="sxs-lookup"><span data-stu-id="5b73a-150">Pipeline (copy activity)</span></span>
````
{
    "name": "CopyImportedData",
    "properties": {
        "description": "Pipeline with copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "AzureDataLakeStoreSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity"
            }
        ],
        "start": "2016-02-08T22:00:00Z",
        "end": "2016-02-08T23:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
````
<span data-ttu-id="5b73a-151">자세한 내용은 참조 [Azure 저장소에서 데이터에는 Azure 데이터 팩터리를 사용 하 여 tooAzure 데이터 레이크 저장소 blob 이동](../data-factory/data-factory-azure-datalake-connector.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-151">For more information, see [Move data from Azure Storage blob tooAzure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a><span data-ttu-id="5b73a-152">Azure 데이터 레이크 저장소의 데이터 파일 hello를 다시 생성</span><span class="sxs-lookup"><span data-stu-id="5b73a-152">Reconstruct hello data files in Azure Data Lake Store</span></span>
<span data-ttu-id="5b73a-153">319 GB 였으며 중단 것 더 작은 크기의 파일로 hello Azure 가져오기/내보내기 서비스를 사용 하 여 전송할 수 있도록 하는 파일 시작 했습니다.입니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using hello Azure Import/Export service.</span></span> <span data-ttu-id="5b73a-154">Hello 데이터는 Azure 데이터 레이크 저장소에 했으므로 hello 파일 tooits 원래 크기를 다시 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-154">Now that hello data is in Azure Data Lake Store, we can reconstruct hello file tooits original size.</span></span> <span data-ttu-id="5b73a-155">따라서 Azure PowerShell cmldts toodo 다음 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-155">You can use hello following Azure PowerShell cmldts toodo so.</span></span>

````
# Login tooour account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch toohello subscription you want toowork with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  hello files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="5b73a-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5b73a-156">Next steps</span></span>
* [<span data-ttu-id="5b73a-157">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="5b73a-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="5b73a-158">Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="5b73a-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="5b73a-159">Azure HDInsight에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="5b73a-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
