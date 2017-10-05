---
title: "Azure CLI 2.0을 사용하여 Azure Data Lake Analytics 시작 | Microsoft Docs"
description: "Azure 명령줄 인터페이스 2.0을 사용하여 Data Lake Analytics 계정을 만들고, U-SQL을 사용하여 Data Lake Analytics 작업을 만들고, 작업을 제출하는 방법에 대해 알아봅니다. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: fe2b84aac718ff5eddd4d73b5dc2120362952c1e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a><span data-ttu-id="f0bc7-103">Azure CLI 2.0를 사용하여 Azure Data Lake Analytics 시작</span><span class="sxs-lookup"><span data-stu-id="f0bc7-103">Get started with Azure Data Lake Analytics using Azure CLI 2.0</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="f0bc7-104">이 자습서에서는 TSV(탭 분리 값) 파일을 읽고 CSV(쉼표로 구분된 값) 파일로 변환하는 작업을 개발합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-104">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated values (CSV) file.</span></span> <span data-ttu-id="f0bc7-105">지원되는 다른 도구를 사용하여 같은 자습서를 진행하려면 이 섹션의 맨 위에 있는 드롭다운 목록을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-105">To go through the same tutorial using other supported tools, use the dropdown list on the top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0bc7-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f0bc7-106">Prerequisites</span></span>
<span data-ttu-id="f0bc7-107">이 자습서를 시작하기 전에 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-107">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="f0bc7-108">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-108">**An Azure subscription**.</span></span> <span data-ttu-id="f0bc7-109">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f0bc7-110">**Azure CLI 2.0**.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-110">**Azure CLI 2.0**.</span></span> <span data-ttu-id="f0bc7-111">[Azure CLI 설치 및 구성](https://docs.microsoft.com/cli/azure/install-azure-cli)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="f0bc7-112">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="f0bc7-112">Log in to Azure</span></span>

<span data-ttu-id="f0bc7-113">Azure 구독에 로그인하려면</span><span class="sxs-lookup"><span data-stu-id="f0bc7-113">To log in to your Azure subscription:</span></span>

```
azurecli
az login
```

<span data-ttu-id="f0bc7-114">URL로 이동하여 인증 코드를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-114">You are requested to browse to a URL, and enter an authentication code.</span></span>  <span data-ttu-id="f0bc7-115">그런 다음 소개에 따라 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-115">And then follow the instructions to enter your credentials.</span></span>

<span data-ttu-id="f0bc7-116">로그인되면 로그인 명령에 구독이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-116">Once you have logged in, the login command lists your subscriptions.</span></span>

<span data-ttu-id="f0bc7-117">특정 구독을 사용하려면</span><span class="sxs-lookup"><span data-stu-id="f0bc7-117">To use a specific subscription:</span></span>

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="f0bc7-118">데이터 레이크 분석 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="f0bc7-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="f0bc7-119">모든 작업을 실행하기 전에 Data Lake Analytics 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-119">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="f0bc7-120">Data Lake Analytics 계정을 만들려면 다음 항목을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-120">To create a Data Lake Analytics account, you must specify the following items:</span></span>

* <span data-ttu-id="f0bc7-121">**Azure 리소스 그룹**.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-121">**Azure Resource Group**.</span></span> <span data-ttu-id="f0bc7-122">Azure 리소스 그룹 내에서 Data Lake Analytics 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-122">A Data Lake Analytics account must be created within an Azure Resource group.</span></span> <span data-ttu-id="f0bc7-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)를 사용하면 그룹으로 응용 프로그램에서 리소스와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you to work with the resources in your application as a group.</span></span> <span data-ttu-id="f0bc7-124">응용 프로그램에 대한 모든 리소스의 배포, 업데이트 또는 삭제를 조정된 단일 작업으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-124">You can deploy, update, or delete all of the resources for your application in a single, coordinated operation.</span></span>  

<span data-ttu-id="f0bc7-125">구독 중인 기존 리소스 그룹을 나열하려면</span><span class="sxs-lookup"><span data-stu-id="f0bc7-125">To list the existing resource groups under your subscription:</span></span>

```
az group list
```

<span data-ttu-id="f0bc7-126">새 리소스 그룹을 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-126">To create a new resource group:</span></span>

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* <span data-ttu-id="f0bc7-127">**Data Lake Analytics 계정 이름**.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-127">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="f0bc7-128">Data Lake Analytics 계정마다 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-128">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="f0bc7-129">**위치** -</span><span class="sxs-lookup"><span data-stu-id="f0bc7-129">**Location**.</span></span> <span data-ttu-id="f0bc7-130">Data Lake Analytics를 지원하는 Azure 데이터 센터 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-130">Use one of the Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="f0bc7-131">**기본 Data Lake Store 계정**: 각 Data Lake Analytics 계정에는 기본 Data Lake Store 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-131">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>

<span data-ttu-id="f0bc7-132">기존Data Lake Store 계정을 나열하려면</span><span class="sxs-lookup"><span data-stu-id="f0bc7-132">To list the existing Data Lake Store account:</span></span>

```
az dls account list
```

<span data-ttu-id="f0bc7-133">새 Data Lake Store 계정을 만들려면</span><span class="sxs-lookup"><span data-stu-id="f0bc7-133">To create a new Data Lake Store account:</span></span>

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

<span data-ttu-id="f0bc7-134">다음 구문을 사용하여 Data Lake Analytics 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-134">Use the following syntax to create a Data Lake Analytics account:</span></span>

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="f0bc7-135">계정을 만든 후 다음 명령을 사용하여 계정을 나열하고 계정 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-135">After creating an account, you can use the following commands to list the accounts and show account details:</span></span>

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-to-data-lake-store"></a><span data-ttu-id="f0bc7-136">데이터 레이크 저장소에 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="f0bc7-136">Upload data to Data Lake Store</span></span>
<span data-ttu-id="f0bc7-137">이 자습서에서는 몇 가지 검색 로그를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-137">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="f0bc7-138">검색 로그는 데이터 레이크 저장소 또는 Azure Blob 저장소에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-138">The search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="f0bc7-139">Azure Portal은 검색 로그 파일을 포함하는 기본 Data Lake Store 계정에 샘플 데이터 파일을 복사하는 사용자 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-139">The Azure portal provides a user interface for copying some sample data files to the default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="f0bc7-140">기본 데이터 레이크 저장소 계정에 데이터를 업로드하려면 [원본 데이터 준비](data-lake-analytics-get-started-portal.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-140">See [Prepare source data](data-lake-analytics-get-started-portal.md) to upload the data to the default Data Lake Store account.</span></span>

<span data-ttu-id="f0bc7-141">CLI 2.0를 사용하여 파일을 업로드하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-141">To upload files using CLI 2.0, use the following commands:</span></span>

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="f0bc7-142">데이터 레이크 분석은 Azure Blob 저장소에 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-142">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="f0bc7-143">Azure Blob 저장소에 데이터를 업로드하려면 [Azure 저장소와 Azure CLI 사용](../storage/common/storage-azure-cli.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-143">For uploading data to Azure Blob storage, see [Using the Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="f0bc7-144">데이터 레이크 분석 작업 제출</span><span class="sxs-lookup"><span data-stu-id="f0bc7-144">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="f0bc7-145">데이터 레이크 분석 작업은 U-SQL 언어로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-145">The Data Lake Analytics jobs are written in the U-SQL language.</span></span> <span data-ttu-id="f0bc7-146">U-SQL에 대한 자세한 내용은 [U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md) 및 [U-SQL 언어 참조](http://go.microsoft.com/fwlink/?LinkId=691348)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-146">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="f0bc7-147">**데이터 레이크 분석 작업 스크립트를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="f0bc7-147">**To create a Data Lake Analytics job script**</span></span>

<span data-ttu-id="f0bc7-148">다음 U-SQL 스크립트를 사용하여 텍스트 파일을 만들고 사용자의 워크스테이션에 텍스트 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-148">Create a text file with following U-SQL script, and save the text file to your workstation:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="f0bc7-149">이 U-SQL 스크립트는 **Extractors.Tsv()**를 사용하여 원본 데이터 파일을 읽은 다음 **Outputters.Csv()**를 사용하여 csv 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-149">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

<span data-ttu-id="f0bc7-150">원본 파일을 다른 위치에 복사하지 않는 한 두 경로를 수정하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-150">Don't modify the two paths unless you copy the source file into a different location.</span></span>  <span data-ttu-id="f0bc7-151">출력 폴더가 없는 경우 Data Lake Analytics에서 해당 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-151">Data Lake Analytics creates the output folder if it doesn't exist.</span></span>

<span data-ttu-id="f0bc7-152">기본 Data Lake Store 계정에 저장된 파일의 상대 경로를 사용하는 것이 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-152">It is simpler to use relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="f0bc7-153">절대 경로를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-153">You can also use absolute paths.</span></span>  <span data-ttu-id="f0bc7-154">예:</span><span class="sxs-lookup"><span data-stu-id="f0bc7-154">For example:</span></span>

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

<span data-ttu-id="f0bc7-155">연결된 저장소 계정의 파일에 액세스하려면 절대 경로를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-155">You must use absolute paths to access files in linked Storage accounts.</span></span>  <span data-ttu-id="f0bc7-156">연결된 Azure 저장소 계정에 저장된 파일에 대한 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-156">The syntax for files stored in linked Azure Storage account is:</span></span>

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> <span data-ttu-id="f0bc7-157">공용 Blob이 있는 Azure Blob 컨테이너는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-157">Azure Blob container with public blobs are not supported.</span></span>      
> <span data-ttu-id="f0bc7-158">공용 컨테이너가 있는 Azure Blob 컨테이너는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-158">Azure Blob container with public containers are not supported.</span></span>      
>

<span data-ttu-id="f0bc7-159">**작업을 제출하려면**</span><span class="sxs-lookup"><span data-stu-id="f0bc7-159">**To submit jobs**</span></span>

<span data-ttu-id="f0bc7-160">다음 구문을 사용하여 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-160">Use the following syntax to submit a job.</span></span>

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="f0bc7-161">예:</span><span class="sxs-lookup"><span data-stu-id="f0bc7-161">For example:</span></span>

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="f0bc7-162">**작업을 나열하고 작업 정보를 표시하려면**</span><span class="sxs-lookup"><span data-stu-id="f0bc7-162">**To list jobs and show job details**</span></span>

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="f0bc7-163">**작업을 취소하려면**</span><span class="sxs-lookup"><span data-stu-id="f0bc7-163">**To cancel jobs**</span></span>

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a><span data-ttu-id="f0bc7-164">작업 결과 검색</span><span class="sxs-lookup"><span data-stu-id="f0bc7-164">Retrieve job results</span></span>

<span data-ttu-id="f0bc7-165">작업이 완료된 후 다음 명령을 사용하여 출력 파일을 나열하고 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-165">After a job is completed, you can use the following commands to list the output files, and download the files:</span></span>

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="f0bc7-166">예:</span><span class="sxs-lookup"><span data-stu-id="f0bc7-166">For example:</span></span>

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="f0bc7-167">파이프라인 및 되풀이</span><span class="sxs-lookup"><span data-stu-id="f0bc7-167">Pipelines and recurrences</span></span>

<span data-ttu-id="f0bc7-168">**파이프라인 및 되풀이에 대한 정보 가져오기**</span><span class="sxs-lookup"><span data-stu-id="f0bc7-168">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="f0bc7-169">`az dla job pipeline` 명령을 사용하여 이전에 제출한 작업의 파이프라인 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-169">Use the `az dla job pipeline` commands to see the pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="f0bc7-170">`az dla job recurrence` 명령을 사용하여 이전에 제출한 작업의 되풀이 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-170">Use the `az dla job recurrence` commands to see the recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a><span data-ttu-id="f0bc7-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f0bc7-171">Next steps</span></span>

* <span data-ttu-id="f0bc7-172">Data Lake Analytics CLI 2.0 참조 문서를 보려면 [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-172">To see the Data Lake Analytics CLI 2.0 reference document, see [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="f0bc7-173">Data Lake Store CLI 2.0 참조 문서를 보려면 [Data Lake Store](https://docs.microsoft.com/cli/azure/dls)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-173">To see the Data Lake Store CLI 2.0 reference document, see [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="f0bc7-174">더 복잡한 쿼리를 보려면 [Azure Data Lake Analytics을 사용하여 웹 사이트 로그 분석](data-lake-analytics-analyze-weblogs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0bc7-174">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
