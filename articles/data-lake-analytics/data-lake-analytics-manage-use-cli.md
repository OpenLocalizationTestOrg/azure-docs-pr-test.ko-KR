---
title: "Azure 명령줄 인터페이스를 사용하여 Azure Data Lake Analytics 관리 | Microsoft Docs"
description: "Azure CLI를 사용하여 데이터 레이크 분석 계정, 데이터 원본, 작업, 사용자를 관리하는 방법을 알아봅니다."
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
ms.openlocfilehash: f90bada3572c0ed40b07d76ec02c1b499bbd1428
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="69c12-103">Azure 명령줄 인터페이스(CLI)를 사용하여 Azure 데이터 레이크 분석 관리</span><span class="sxs-lookup"><span data-stu-id="69c12-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="69c12-104">Azure CLI를 사용하여 Azure Data Lake Analytics 계정, 데이터 원본, 사용자 및 작업을 관리하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure CLI.</span></span> <span data-ttu-id="69c12-105">다른 도구를 사용하여 관리 항목을 보려면 위의 탭 선택을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-105">To see management topics using other tools, click the tab select above.</span></span>


<span data-ttu-id="69c12-106">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="69c12-106">**Prerequisites**</span></span>

<span data-ttu-id="69c12-107">이 자습서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-107">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="69c12-108">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="69c12-108">**An Azure subscription**.</span></span> <span data-ttu-id="69c12-109">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c12-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="69c12-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="69c12-110">**Azure CLI**.</span></span> <span data-ttu-id="69c12-111">[Azure CLI 설치 및 구성](../cli-install-nodejs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c12-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="69c12-112">이 데모를 완료하려면 **시험판** [Azure CLI 도구](https://github.com/MicrosoftBigData/AzureDataLake/releases) 를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-112">Download and install the **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order to complete this demo.</span></span>
* <span data-ttu-id="69c12-113">**인증**은 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-113">**Authentication**, using the following command:</span></span>
  
        azure login
    <span data-ttu-id="69c12-114">회사 또는 학교 계정을 사용하여 인증하는 방법에 대한 자세한 내용은 [Azure CLI에서 Azure 구독에 연결](../xplat-cli-connect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c12-114">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="69c12-115">**Azure Resource Manager 모드로 전환**은 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-115">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="69c12-116">**데이터 레이크 저장소 및 데이터 레이크 분석 명령을 나열하려면:**</span><span class="sxs-lookup"><span data-stu-id="69c12-116">**To list the Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="69c12-117">계정 관리</span><span class="sxs-lookup"><span data-stu-id="69c12-117">Manage accounts</span></span>
<span data-ttu-id="69c12-118">데이터 레이크 분석 작업을 실행하려면 데이터 레이크 분석 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="69c12-119">Azure HDInsight와 달리 작업을 실행하지 않는 경우 분석 계정에 대해 비용을 지불하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="69c12-120">작업이 실행되는 시간에 대해서만 비용을 지불합니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-120">You only pay for the time when it is running a job.</span></span>  <span data-ttu-id="69c12-121">자세한 내용은 [Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c12-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="69c12-122">계정 만들기</span><span class="sxs-lookup"><span data-stu-id="69c12-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="69c12-123">계정 업데이트</span><span class="sxs-lookup"><span data-stu-id="69c12-123">Update accounts</span></span>
<span data-ttu-id="69c12-124">다음 명령은 기존 데이터 레이크 분석 계정의 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-124">The following command updates the properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="69c12-125">계정 나열</span><span class="sxs-lookup"><span data-stu-id="69c12-125">List accounts</span></span>
<span data-ttu-id="69c12-126">데이터 레이크 분석 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="69c12-127">특정 리소스 그룹 내의 데이터 레이크 분석 계정 나열</span><span class="sxs-lookup"><span data-stu-id="69c12-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="69c12-128">특정 데이터 레이크 분석 계정의 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="69c12-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="69c12-129">데이터 레이크 분석 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="69c12-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="69c12-130">계정 데이터 원본 관리</span><span class="sxs-lookup"><span data-stu-id="69c12-130">Manage account data sources</span></span>
<span data-ttu-id="69c12-131">데이터 레이크 분석은 현재 다음 데이터 원본을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-131">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="69c12-132">Azure 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="69c12-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="69c12-133">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="69c12-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="69c12-134">분석 계정을 만들 때 Azure 데이터 레이크 저장소 계정이 기본 저장소 계정이 되도록 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account to be the default storage account.</span></span> <span data-ttu-id="69c12-135">기본 ADL 저장소 계정은 작업 메타데이터 및 작업 감사 로그를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-135">The default ADL storage account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="69c12-136">분석 계정을 만든 후 데이터 레이크 저장소 계정 및/또는 Azure 저장소 계정을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-the-default-adl-storage-account"></a><span data-ttu-id="69c12-137">기본 ADL 저장소 계정 찾기</span><span class="sxs-lookup"><span data-stu-id="69c12-137">Find the default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="69c12-138">properties:datalakeStoreAccount:name 아래에 값이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-138">The value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="69c12-139">Azure Blob 저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="69c12-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="69c12-140">Blob 저장소 짧은 이름만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="69c12-141">FQDN(예: “myblob.blob.core.windows.net”)을 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="69c12-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="69c12-142">데이터 레이크 저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="69c12-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="69c12-143">[-d]는 추가되는 데이터 레이크가 기본 데이터 레이크 계정인지를 나타내는 선택적 스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-143">[-d] is an optional switch to indicate whether the Data Lake being added is the default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="69c12-144">기존 데이터 원본 업데이트</span><span class="sxs-lookup"><span data-stu-id="69c12-144">Update existing data source</span></span>
<span data-ttu-id="69c12-145">기존 데이터 레이크 저장소 계정을 기본으로 설정하려면:</span><span class="sxs-lookup"><span data-stu-id="69c12-145">To set an existing Data Lake Store account to be the default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="69c12-146">기존 Blob 저장소 계정 키를 업데이트하려면:</span><span class="sxs-lookup"><span data-stu-id="69c12-146">To update an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="69c12-147">데이터 원본 나열:</span><span class="sxs-lookup"><span data-stu-id="69c12-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![데이터 레이크 분석은 데이터 원본을 나열합니다.](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="69c12-149">데이터 원본 삭제:</span><span class="sxs-lookup"><span data-stu-id="69c12-149">Delete data sources:</span></span>
<span data-ttu-id="69c12-150">데이터 레이크 저장소 계정을 삭제하려면:</span><span class="sxs-lookup"><span data-stu-id="69c12-150">To delete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="69c12-151">Blob 저장소 계정을 삭제하려면:</span><span class="sxs-lookup"><span data-stu-id="69c12-151">To delete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="69c12-152">작업 관리</span><span class="sxs-lookup"><span data-stu-id="69c12-152">Manage jobs</span></span>
<span data-ttu-id="69c12-153">작업을 만들려면 데이터 레이크 분석 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="69c12-154">자세한 내용은 [데이터 레이크 분석 계정 관리](#manage-accounts)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c12-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="69c12-155">작업 나열</span><span class="sxs-lookup"><span data-stu-id="69c12-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![데이터 레이크 분석은 데이터 원본을 나열합니다.](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="69c12-157">작업 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="69c12-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="69c12-158">작업 제출</span><span class="sxs-lookup"><span data-stu-id="69c12-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="69c12-159">작업의 기본 우선 순위는 1000이고 작업에 대한 기본 병렬 처리 수준은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-159">The default priority of a job is 1000, and the default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="69c12-160">작업 취소</span><span class="sxs-lookup"><span data-stu-id="69c12-160">Cancel jobs</span></span>
<span data-ttu-id="69c12-161">list 명령을 사용하여 Job ID를 찾은 후 cancel을 사용하여 작업을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-161">Use the list command to find the job id, and then use cancel to cancel the job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="69c12-162">카탈로그 관리</span><span class="sxs-lookup"><span data-stu-id="69c12-162">Manage catalog</span></span>
<span data-ttu-id="69c12-163">U-SQL 카탈로그는 U-SQL 스크립트에서 공유할 수 있도록 데이터 및 코드를 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-163">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="69c12-164">카탈로그를 사용하면 가능한 가장 높은 성능으로 Azure 데이터 레이크의 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-164">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="69c12-165">자세한 내용은 [U-SQL 카탈로그 사용](data-lake-analytics-use-u-sql-catalog.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c12-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="69c12-166">카탈로그 항목 나열</span><span class="sxs-lookup"><span data-stu-id="69c12-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="69c12-167">데이터베이스, 스키마, 어셈블리, 외부 데이터 소스, 테이블, 테이블 값 함수 또는 테이블 통계가 형식에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-167">The types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="69c12-168">ARM 그룹 사용</span><span class="sxs-lookup"><span data-stu-id="69c12-168">Use ARM groups</span></span>
<span data-ttu-id="69c12-169">응용 프로그램은 일반적으로 웹앱, 데이터베이스, 데이터베이스 서버, 저장소 및 타사 서비스 등 많은 구성 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="69c12-170">ARM(Azure 리소스 관리자)을 사용하면 Azure 리소스 그룹이라고 하는 그룹으로 응용 프로그램에서 리소스와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-170">Azure Resource Manager (ARM) enables you to work with the resources in your application as a group, referred to as an Azure Resource Group.</span></span> <span data-ttu-id="69c12-171">응용 프로그램에 대한 모든 리소스의 배포, 업데이트, 모니터링 또는 삭제를 조정된 단일 작업으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-171">You can deploy, update, monitor or delete all of the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="69c12-172">배포용 템플릿을 사용하고 이 템플릿을 테스트, 스테이징 및 프로덕션과 같은 여러 환경에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="69c12-173">전체 그룹에 대한 롤업 비용을 확인하여 조직에 요금 청구를 명확히 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-173">You can clarify billing for your organization by viewing the rolled-up costs for the entire group.</span></span> <span data-ttu-id="69c12-174">자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c12-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="69c12-175">데이터 레이크 분석 서비스는 다음 구성 요소를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-175">A Data Lake Analytics service can include the following components:</span></span>

* <span data-ttu-id="69c12-176">Azure 데이터 레이크 분석 계정</span><span class="sxs-lookup"><span data-stu-id="69c12-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="69c12-177">필수 기본 Azure 데이터 레이크 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="69c12-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="69c12-178">추가 Azure 데이터 레이크 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="69c12-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="69c12-179">추가 Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="69c12-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="69c12-180">이러한 모든 구성을 쉽게 관리할 수 있도록 하나의 ARM 그룹 아래 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-180">You can create all these components under one ARM group to make them easier to manage.</span></span>

![Azure 데이터 레이크 분석 계정 및 저장소](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="69c12-182">데이터 레이크 분석 계정 및 종속 저장소 계정은 동일한 Azure 데이터 센터에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-182">A Data Lake Analytics account and the dependent storage accounts must be placed in the same Azure data center.</span></span>
<span data-ttu-id="69c12-183">그러나 ARM 그룹은 다른 데이터 센터에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c12-183">The ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="69c12-184">참고 항목</span><span class="sxs-lookup"><span data-stu-id="69c12-184">See also</span></span>
* [<span data-ttu-id="69c12-185">Microsoft Azure 데이터 레이크 분석 개요</span><span class="sxs-lookup"><span data-stu-id="69c12-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="69c12-186">Azure 포털을 사용하여 데이터 레이크 분석 시작</span><span class="sxs-lookup"><span data-stu-id="69c12-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="69c12-187">Azure 포털을 사용하여 Azure 데이터 레이크 분석 관리</span><span class="sxs-lookup"><span data-stu-id="69c12-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="69c12-188">Azure 포털을 사용하여 Azure 데이터 레이크 분석 작업 모니터링 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="69c12-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

