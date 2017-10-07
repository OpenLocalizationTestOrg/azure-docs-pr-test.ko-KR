---
title: "Azure 명령줄 인터페이스를 사용 하 여 Azure Data Lake 분석 aaaManage | Microsoft Docs"
description: "Toomanage Data Lake 분석 계정, 데이터 원본 작업 하는 방법 및 Azure CLI를 사용 하 여 사용자에 알아봅니다"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="c2e50-103">Azure 명령줄 인터페이스(CLI)를 사용하여 Azure 데이터 레이크 분석 관리</span><span class="sxs-lookup"><span data-stu-id="c2e50-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="c2e50-104">어떻게 toomanage Azure Data Lake 분석 계정, 데이터 원본, 사용자 및 사용 하 여 작업 hello Azure CLI에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure CLI.</span></span> <span data-ttu-id="c2e50-105">다른 도구를 사용 하 여 toosee 관리 항목을 클릭 하 여 위의 hello 탭 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-105">toosee management topics using other tools, click hello tab select above.</span></span>


<span data-ttu-id="c2e50-106">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="c2e50-106">**Prerequisites**</span></span>

<span data-ttu-id="c2e50-107">이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-107">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="c2e50-108">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="c2e50-108">**An Azure subscription**.</span></span> <span data-ttu-id="c2e50-109">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2e50-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c2e50-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="c2e50-110">**Azure CLI**.</span></span> <span data-ttu-id="c2e50-111">[Azure CLI 설치 및 구성](../cli-install-nodejs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2e50-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="c2e50-112">다운로드 및 설치 hello **시험판** [Azure CLI 도구](https://github.com/MicrosoftBigData/AzureDataLake/releases) 의 순서로 toocomplete이이 데모입니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-112">Download and install hello **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order toocomplete this demo.</span></span>
* <span data-ttu-id="c2e50-113">**인증**를 사용 하 여 다음 명령을 hello:</span><span class="sxs-lookup"><span data-stu-id="c2e50-113">**Authentication**, using hello following command:</span></span>
  
        azure login
    <span data-ttu-id="c2e50-114">회사 또는 학교 계정을 사용 하 여 인증에 대 한 자세한 내용은 참조 하십시오. [hello Azure CLI에서에서 tooan Azure 구독 연결](../xplat-cli-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-114">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="c2e50-115">**Toohello Azure Resource Manager 모드로 전환**를 사용 하 여 다음 명령을 hello:</span><span class="sxs-lookup"><span data-stu-id="c2e50-115">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="c2e50-116">**toolist hello 데이터 레이크 저장소 및 데이터 레이크 분석 명령:**</span><span class="sxs-lookup"><span data-stu-id="c2e50-116">**toolist hello Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="c2e50-117">계정 관리</span><span class="sxs-lookup"><span data-stu-id="c2e50-117">Manage accounts</span></span>
<span data-ttu-id="c2e50-118">데이터 레이크 분석 작업을 실행하려면 데이터 레이크 분석 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="c2e50-119">Azure HDInsight와 달리 작업을 실행하지 않는 경우 분석 계정에 대해 비용을 지불하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="c2e50-120">Hello 시간 작업을 실행 중인 경우에 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-120">You only pay for hello time when it is running a job.</span></span>  <span data-ttu-id="c2e50-121">자세한 내용은 [Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2e50-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="c2e50-122">계정 만들기</span><span class="sxs-lookup"><span data-stu-id="c2e50-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="c2e50-123">계정 업데이트</span><span class="sxs-lookup"><span data-stu-id="c2e50-123">Update accounts</span></span>
<span data-ttu-id="c2e50-124">hello 다음 명령을 hello의 속성을 업데이트는 기존 데이터 레이크 분석 계정</span><span class="sxs-lookup"><span data-stu-id="c2e50-124">hello following command updates hello properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="c2e50-125">계정 나열</span><span class="sxs-lookup"><span data-stu-id="c2e50-125">List accounts</span></span>
<span data-ttu-id="c2e50-126">데이터 레이크 분석 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="c2e50-127">특정 리소스 그룹 내의 데이터 레이크 분석 계정 나열</span><span class="sxs-lookup"><span data-stu-id="c2e50-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="c2e50-128">특정 데이터 레이크 분석 계정의 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="c2e50-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="c2e50-129">데이터 레이크 분석 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="c2e50-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="c2e50-130">계정 데이터 원본 관리</span><span class="sxs-lookup"><span data-stu-id="c2e50-130">Manage account data sources</span></span>
<span data-ttu-id="c2e50-131">Data Lake 분석에는 현재 데이터 원본 hello를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-131">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="c2e50-132">Azure 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="c2e50-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="c2e50-133">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="c2e50-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="c2e50-134">분석 계정을 만들 때 Azure 데이터 레이크 저장소 계정 toobe hello 기본 저장소 계정을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account toobe hello default storage account.</span></span> <span data-ttu-id="c2e50-135">hello 기본 ADL 저장소 계정이 사용 toostore 작업 메타 데이터 및 작업에 대 한 감사 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-135">hello default ADL storage account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="c2e50-136">분석 계정을 만든 후 데이터 레이크 저장소 계정 및/또는 Azure 저장소 계정을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-hello-default-adl-storage-account"></a><span data-ttu-id="c2e50-137">Hello 기본 ADL 저장소 계정 찾기</span><span class="sxs-lookup"><span data-stu-id="c2e50-137">Find hello default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="c2e50-138">hello 값 속성: datalakeStoreAccount:name 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-138">hello value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="c2e50-139">Azure Blob 저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="c2e50-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="c2e50-140">Blob 저장소 짧은 이름만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="c2e50-141">FQDN(예: “myblob.blob.core.windows.net”)을 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c2e50-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="c2e50-142">데이터 레이크 저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="c2e50-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="c2e50-143">[-d]은 선택적 스위치 tooindicate hello 추가 되는 데이터 레이크 hello 기본 데이터 레이크 계정 인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-143">[-d] is an optional switch tooindicate whether hello Data Lake being added is hello default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="c2e50-144">기존 데이터 원본 업데이트</span><span class="sxs-lookup"><span data-stu-id="c2e50-144">Update existing data source</span></span>
<span data-ttu-id="c2e50-145">기존 데이터 레이크 저장소 계정 toobe hello 기본값 tooset:</span><span class="sxs-lookup"><span data-stu-id="c2e50-145">tooset an existing Data Lake Store account toobe hello default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="c2e50-146">tooupdate 기존 Blob 저장소 계정 키:</span><span class="sxs-lookup"><span data-stu-id="c2e50-146">tooupdate an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="c2e50-147">데이터 원본 나열:</span><span class="sxs-lookup"><span data-stu-id="c2e50-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![데이터 레이크 분석은 데이터 원본을 나열합니다.](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="c2e50-149">데이터 원본 삭제:</span><span class="sxs-lookup"><span data-stu-id="c2e50-149">Delete data sources:</span></span>
<span data-ttu-id="c2e50-150">toodelete 데이터 레이크 저장소 계정:</span><span class="sxs-lookup"><span data-stu-id="c2e50-150">toodelete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="c2e50-151">toodelete Blob 저장소 계정:</span><span class="sxs-lookup"><span data-stu-id="c2e50-151">toodelete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="c2e50-152">작업 관리</span><span class="sxs-lookup"><span data-stu-id="c2e50-152">Manage jobs</span></span>
<span data-ttu-id="c2e50-153">작업을 만들려면 데이터 레이크 분석 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="c2e50-154">자세한 내용은 [데이터 레이크 분석 계정 관리](#manage-accounts)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2e50-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="c2e50-155">작업 나열</span><span class="sxs-lookup"><span data-stu-id="c2e50-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![데이터 레이크 분석은 데이터 원본을 나열합니다.](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="c2e50-157">작업 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="c2e50-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="c2e50-158">작업 제출</span><span class="sxs-lookup"><span data-stu-id="c2e50-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="c2e50-159">작업의 기본 우선 순위 hello은 1000으로 및 hello 기본 수준의 작업에 대 한 병렬 처리는 1입니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-159">hello default priority of a job is 1000, and hello default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="c2e50-160">작업 취소</span><span class="sxs-lookup"><span data-stu-id="c2e50-160">Cancel jobs</span></span>
<span data-ttu-id="c2e50-161">Hello 목록 명령 toofind hello 작업 id를 사용 하 고 toocancel hello 작업 취소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-161">Use hello list command toofind hello job id, and then use cancel toocancel hello job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="c2e50-162">카탈로그 관리</span><span class="sxs-lookup"><span data-stu-id="c2e50-162">Manage catalog</span></span>
<span data-ttu-id="c2e50-163">hello U-SQL 카탈로그 이므로 toostructure 사용 되는 데이터와 코드 U-SQL 스크립트에서 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-163">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="c2e50-164">hello 카탈로그에서 Azure 데이터 레이크 데이터 가능한 최고 성능을 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-164">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="c2e50-165">자세한 내용은 [U-SQL 카탈로그 사용](data-lake-analytics-use-u-sql-catalog.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2e50-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="c2e50-166">카탈로그 항목 나열</span><span class="sxs-lookup"><span data-stu-id="c2e50-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="c2e50-167">hello 유형은 데이터베이스, 스키마, 어셈블리, 외부 데이터 원본, 테이블, 테이블 반환 함수 또는 테이블 통계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-167">hello types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="c2e50-168">ARM 그룹 사용</span><span class="sxs-lookup"><span data-stu-id="c2e50-168">Use ARM groups</span></span>
<span data-ttu-id="c2e50-169">응용 프로그램은 일반적으로 웹앱, 데이터베이스, 데이터베이스 서버, 저장소 및 타사 서비스 등 많은 구성 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="c2e50-170">Azure 리소스 관리자 (ARM) toowork를 hello 리소스 그룹 참조 tooas Azure 리소스 그룹으로 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-170">Azure Resource Manager (ARM) enables you toowork with hello resources in your application as a group, referred tooas an Azure Resource Group.</span></span> <span data-ttu-id="c2e50-171">배포 업데이트 하거나 모니터링 단일, 통합 작업에서 응용 프로그램에 대 한 모든 hello 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-171">You can deploy, update, monitor or delete all of hello resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="c2e50-172">배포용 템플릿을 사용하고 이 템플릿을 테스트, 스테이징 및 프로덕션과 같은 여러 환경에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="c2e50-173">Hello 전체 그룹에 대 한 hello 겹쳐서 비용을 확인 하 여 조직에 대 한 요금 청구를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-173">You can clarify billing for your organization by viewing hello rolled-up costs for hello entire group.</span></span> <span data-ttu-id="c2e50-174">자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2e50-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="c2e50-175">Data Lake 분석 서비스는 다음과 같은 구성 요소가 hello를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-175">A Data Lake Analytics service can include hello following components:</span></span>

* <span data-ttu-id="c2e50-176">Azure 데이터 레이크 분석 계정</span><span class="sxs-lookup"><span data-stu-id="c2e50-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="c2e50-177">필수 기본 Azure 데이터 레이크 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="c2e50-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="c2e50-178">추가 Azure 데이터 레이크 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="c2e50-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="c2e50-179">추가 Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="c2e50-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="c2e50-180">하나의 ARM 그룹 toomake에서 이러한 모든 구성이 요소를 만들 수 있습니다에 보다 쉽게 toomanage 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-180">You can create all these components under one ARM group toomake them easier toomanage.</span></span>

![Azure 데이터 레이크 분석 계정 및 저장소](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="c2e50-182">Data Lake 분석 계정 및 hello 종속 저장소 계정에에서 배치 해야 hello 동일한 Azure 데이터 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-182">A Data Lake Analytics account and hello dependent storage accounts must be placed in hello same Azure data center.</span></span>
<span data-ttu-id="c2e50-183">그러나 hello ARM 그룹 다른 데이터 센터에 위치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2e50-183">hello ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="c2e50-184">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c2e50-184">See also</span></span>
* [<span data-ttu-id="c2e50-185">Microsoft Azure 데이터 레이크 분석 개요</span><span class="sxs-lookup"><span data-stu-id="c2e50-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="c2e50-186">Azure 포털을 사용하여 데이터 레이크 분석 시작</span><span class="sxs-lookup"><span data-stu-id="c2e50-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="c2e50-187">Azure 포털을 사용하여 Azure 데이터 레이크 분석 관리</span><span class="sxs-lookup"><span data-stu-id="c2e50-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="c2e50-188">Azure 포털을 사용하여 Azure 데이터 레이크 분석 작업 모니터링 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c2e50-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

