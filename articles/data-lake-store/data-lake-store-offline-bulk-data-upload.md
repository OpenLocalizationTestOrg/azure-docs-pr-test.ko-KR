---
title: "오프라인 방법을 사용하여 Data Lake Store에 대량 데이터 업로드| Microsoft 문서"
description: "AdlCopy 도구를 사용하여 Azure Storage Blobs에서 Data Lake Store로 데이터를 복사합니다."
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
ms.openlocfilehash: b469c0ebe9838a1ea986cff3043e3008941e9aa9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-importexport-service-for-offline-copy-of-data-to-data-lake-store"></a><span data-ttu-id="2e0e8-103">Azure Import/Export 서비스를 사용하여 Data Lake Store에 오프라인 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="2e0e8-103">Use the Azure Import/Export service for offline copy of data to Data Lake Store</span></span>
<span data-ttu-id="2e0e8-104">이 문서에서는 [Azure Import/Export 서비스](../storage/common/storage-import-export-service.md)와 같은 오프라인 복사 방법을 사용하여 대량 데이터 집합(200GB 초과)을 Azure Data Lake Store에 복사하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-104">In this article, you'll learn how to copy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like the [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="2e0e8-105">특히 이 문서에서 예제로 사용하는 파일의 크기는 디스크에서 339,420,860,416바이트(약 319GB)입니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-105">Specifically, the file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="2e0e8-106">이 파일을 319GB.tsv라고 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="2e0e8-107">Azure Import/Export 서비스를 사용하면 하드 디스크 드라이브를 Azure 데이터 센터에 제공하여 대량 데이터를 Azure Blob 저장소로 더 안전하게 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-107">The Azure Import/Export service helps you to transfer large amounts of data more securely to Azure Blob storage by shipping hard disk drives to an Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e0e8-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2e0e8-108">Prerequisites</span></span>
<span data-ttu-id="2e0e8-109">시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-109">Before you begin, you must have the following:</span></span>

* <span data-ttu-id="2e0e8-110">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-110">**An Azure subscription**.</span></span> <span data-ttu-id="2e0e8-111">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2e0e8-112">**Azure Storage 계정**</span><span class="sxs-lookup"><span data-stu-id="2e0e8-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="2e0e8-113">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="2e0e8-114">만드는 방법에 대한 지침은 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2e0e8-114">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-the-data"></a><span data-ttu-id="2e0e8-115">데이터 준비</span><span class="sxs-lookup"><span data-stu-id="2e0e8-115">Preparing the data</span></span>
<span data-ttu-id="2e0e8-116">Import/Export 서비스를 사용하려면 먼저 전송할 데이터 파일을 **200GB 미만의 복사본**으로 분할해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-116">Before using the Import/Export service, break the data file to be transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="2e0e8-117">200GB보다 큰 파일인 경우 가져오기 도구를 작동할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-117">The import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="2e0e8-118">이 자습서에서는 파일을 각각 100GB의 청크로 분할했습니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-118">In this tutorial, we split the file into chunks of 100 GB each.</span></span> <span data-ttu-id="2e0e8-119">[Cygwin](https://cygwin.com/install.html)을 사용하면 이렇게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="2e0e8-120">Cygwin은 Linux 명령을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="2e0e8-121">이 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-121">In this case, use the following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="2e0e8-122">분할 작업에서는 아래와 같은 이름의 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-122">The split operation creates files with the following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="2e0e8-123">데이터와 함께 디스크 준비</span><span class="sxs-lookup"><span data-stu-id="2e0e8-123">Get disks ready with data</span></span>
<span data-ttu-id="2e0e8-124">**드라이브 준비** 섹션의 [Azure Import/Export 서비스 사용](../storage/common/storage-import-export-service.md) 지침에 따라 하드 드라이브를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-124">Follow the instructions in [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (under the **Prepare your drives** section) to prepare your hard drives.</span></span> <span data-ttu-id="2e0e8-125">전체 시퀀스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-125">Here's the overall sequence:</span></span>

1. <span data-ttu-id="2e0e8-126">Auzre Import/Export 서비스에 사용할 요구 사항을 충족하는 하드 디스크를 확보합니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-126">Procure a hard disk that meets the requirement to be used for the Azure Import/Export service.</span></span>
2. <span data-ttu-id="2e0e8-127">하드 디스크가 Azure 데이터 센터에 제공된 후에 데이터를 복사할 Azure Storage 계정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-127">Identify an Azure storage account where the data will be copied after it is shipped to the Azure datacenter.</span></span>
3. <span data-ttu-id="2e0e8-128">[Azure Import/Export 도구](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409) 명령줄 유틸리티를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-128">Use the [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="2e0e8-129">이 도구를 사용하는 방법을 보여 주는 샘플 코드 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-129">Here's a sample snippet that shows how to use the tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="2e0e8-130">자세한 코드 조각에 대해서는 [Azure Import/Export 서비스 사용](../storage/common/storage-import-export-service.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-130">See [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="2e0e8-131">위 명령은 지정된 위치에 저널 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-131">The preceding command creates a journal file at the specified location.</span></span> <span data-ttu-id="2e0e8-132">이 저널 파일을 사용하여 [Azure 클래식 포털](https://manage.windowsazure.com)에서 가져오기 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-132">Use this journal file to create an import job from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="2e0e8-133">가져오기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="2e0e8-133">Create an import job</span></span>
<span data-ttu-id="2e0e8-134">이제 **가져오기 작업 만들기** 섹션의 [Azure Import/Export 서비스 사용](../storage/common/storage-import-export-service.md)의 지침에 따라 가져오기 작업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-134">You can now create an import job by using the instructions in [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (under the **Create the Import job** section).</span></span> <span data-ttu-id="2e0e8-135">이 가져오기 작업에 대해 다른 세부 정보를 사용하여 디스크 드라이브를 준비하는 동안 생성된 저널 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-135">For this import job, with other details, also provide the journal file created while preparing the disk drives.</span></span>

## <a name="physically-ship-the-disks"></a><span data-ttu-id="2e0e8-136">물리적 디스크 배송</span><span class="sxs-lookup"><span data-stu-id="2e0e8-136">Physically ship the disks</span></span>
<span data-ttu-id="2e0e8-137">이제 디스크를 Azure 데이터 센터에 물리적으로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-137">You can now physically ship the disks to an Azure datacenter.</span></span> <span data-ttu-id="2e0e8-138">여기서 데이터는 가져 오기 작업을 만드는 동안 사용자가 제공한 Azure Storage Blob으로 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-138">There, the data is copied over to the Azure Storage blobs you provided while creating the import job.</span></span> <span data-ttu-id="2e0e8-139">또한 작업을 만드는 동안 나중에 추적 정보를 제공하도록 선택한 경우 가져오기 작업으로 돌아가서 추적 번호를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-139">Also, while creating the job, if you opted to provide the tracking information later, you can now go back to your import job and update the tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-to-azure-data-lake-store"></a><span data-ttu-id="2e0e8-140">Azure Storage Blob에서 Azure Data Lake Store로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="2e0e8-140">Copy data from Azure Storage blobs to Azure Data Lake Store</span></span>
<span data-ttu-id="2e0e8-141">가져오기 작업의 상태가 완료되었다고 표시되면 지정한 Azure Storage Blob에서 데이터를 사용할 수 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-141">After the status of the import job shows that it's completed, you can verify whether the data is available in the Azure Storage blobs you had specified.</span></span> <span data-ttu-id="2e0e8-142">그런 다음 다양한 방법으로 Blob에서 Azure Data Lake Store로 해당 데이터를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-142">You can then use a variety of methods to move that data from the blobs to Azure Data Lake Store.</span></span> <span data-ttu-id="2e0e8-143">데이터를 업로드하는 데 사용 가능한 모든 옵션은 [Data Lake Store에 데이터 수집](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-143">For all the available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="2e0e8-144">이 섹션에서는 데이터 복사용 Azure Data Factory 파이프라인을 만드는 데 사용할 수 있는 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-144">In this section, we provide you with the JSON definitions that you can use to create an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="2e0e8-145">이러한 JSON 정의는 [Azure Portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-145">You can use these JSON definitions from the [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="2e0e8-146">원본에 연결된 서비스(Azure Storage Blob)</span><span class="sxs-lookup"><span data-stu-id="2e0e8-146">Source linked service (Azure Storage blob)</span></span>
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

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="2e0e8-147">대상에 연결된 서비스(Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="2e0e8-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' to allow this data factory and the activities it runs to access this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from the OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="2e0e8-148">입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="2e0e8-148">Input data set</span></span>
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
### <a name="output-data-set"></a><span data-ttu-id="2e0e8-149">출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="2e0e8-149">Output data set</span></span>
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
### <a name="pipeline-copy-activity"></a><span data-ttu-id="2e0e8-150">파이프라인(복사 작업)</span><span class="sxs-lookup"><span data-stu-id="2e0e8-150">Pipeline (copy activity)</span></span>
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
<span data-ttu-id="2e0e8-151">자세한 내용은 [Azure Data Factory를 사용하여 Azure Storage Blob에서 Azure Data Lake Store로 데이터 이동](../data-factory/data-factory-azure-datalake-connector.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-151">For more information, see [Move data from Azure Storage blob to Azure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-the-data-files-in-azure-data-lake-store"></a><span data-ttu-id="2e0e8-152">Azure Data Lake Store에서 데이터 파일 다시 생성</span><span class="sxs-lookup"><span data-stu-id="2e0e8-152">Reconstruct the data files in Azure Data Lake Store</span></span>
<span data-ttu-id="2e0e8-153">319GB의 파일로 시작하고 작은 크기의 파일로 분할하여 Azure Import/Export 서비스를 사용하여 파일을 전송할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using the Azure Import/Export service.</span></span> <span data-ttu-id="2e0e8-154">이제 데이터가 Azure Data Lake Store에 있으므로 파일을 원래 크기로 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-154">Now that the data is in Azure Data Lake Store, we can reconstruct the file to its original size.</span></span> <span data-ttu-id="2e0e8-155">다음 Azure PowerShell cmdlet을 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e0e8-155">You can use the following Azure PowerShell cmldts to do so.</span></span>

````
# Login to our account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch to the subscription you want to work with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  the files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="2e0e8-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2e0e8-156">Next steps</span></span>
* [<span data-ttu-id="2e0e8-157">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="2e0e8-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="2e0e8-158">Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="2e0e8-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="2e0e8-159">Azure HDInsight에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="2e0e8-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
