---
title: "U-SQL 스크립트를 사용하여 데이터 변환 - Azure | Microsoft Docs"
description: "Azure Data Lake Analytics 계산 서비스에서 U-SQL 스크립트를 실행하여 데이터를 처리하거나 변환하는 방법을 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 49a809af92ed1bc6664fbdd3bf1aabf36afb8180
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="729ef-103">Azure Data Lake Analytics에서 U-SQL 스크립트를 실행하여 데이터 변환</span><span class="sxs-lookup"><span data-stu-id="729ef-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="729ef-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="729ef-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="729ef-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="729ef-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="729ef-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="729ef-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="729ef-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="729ef-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="729ef-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="729ef-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="729ef-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="729ef-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="729ef-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="729ef-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="729ef-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="729ef-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="729ef-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="729ef-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="729ef-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="729ef-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="729ef-114">Azure 데이터 팩터리의 파이프라인은 연결된 저장소 서비스의 데이터를 연결된 계산 서비스를 사용하여 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="729ef-115">파이프라인에는 일련의 작업이 포함되며 각 작업에서는 특정 처리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="729ef-116">이 문서는 **Azure Data Lake Analytics** 계산 연결된 서비스에서 **U-SQL** 스크립트를 실행하는 **Data Lake Analytics U-SQL 작업**에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-116">This article describes the **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="729ef-117">Data Lake Analytics U-SQL 작업이 포함된 파이프라인을 만들기 전에 Azure Data Lake Analytics 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="729ef-118">Azure Data Lake Analytics에 대해 알아보려면 [Azure Data Lake Analytics 시작](../data-lake-analytics/data-lake-analytics-get-started-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="729ef-118">To learn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="729ef-119">Data Factory, 연결된 서비스, 데이터 집합 및 파이프라인 만들기를 위한 자세한 단계는 [첫 파이프라인 빌드하기 자습서](data-factory-build-your-first-pipeline.md) 를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="729ef-119">Review the [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps to create a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="729ef-120">Data Factory 편집기, Visual Studio 또는 Azure PowerShell에서 JSON 조각을 사용하여 Data Factory 엔터티를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell to create Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="729ef-121">지원되는 인증 형식</span><span class="sxs-lookup"><span data-stu-id="729ef-121">Supported authentication types</span></span>
<span data-ttu-id="729ef-122">U-SQL 작업은 Data Lake Analytics에 대해 아래 인증 유형을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="729ef-123">서비스 주체 인증</span><span class="sxs-lookup"><span data-stu-id="729ef-123">Service principal authentication</span></span>
* <span data-ttu-id="729ef-124">사용자 자격 증명(OAuth) 인증</span><span class="sxs-lookup"><span data-stu-id="729ef-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="729ef-125">특히 예약된 U-SQL 실행의 경우 서비스 주체 인증을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="729ef-126">사용자 자격 증명 인증의 경우 토큰 만료 동작이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="729ef-127">구성 세부 정보에서 [연결된 서비스 속성](#azure-data-lake-analytics-linked-service) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="729ef-127">For configuration details, see the [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="729ef-128">Azure 데이터 레이크 분석 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="729ef-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="729ef-129">Azure 데이터 레이크 분석 계산 서비스와 Azure Data Factory에 연결하는 **Azure 데이터 레이크 분석** 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-129">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory.</span></span> <span data-ttu-id="729ef-130">파이프라인에서 데이터 레이크 분석 U-SQL 작업은 이 연결된 서비스를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-130">The Data Lake Analytics U-SQL activity in the pipeline refers to this linked service.</span></span> 

<span data-ttu-id="729ef-131">다음 표에는 JSON 정의에서 사용하는 일반 속성에 대한 설명이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-131">The following table provides descriptions for the generic properties used in the JSON definition.</span></span> <span data-ttu-id="729ef-132">서비스 주체와 사용자 자격 증명 인증 중에서 추가로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="729ef-133">속성</span><span class="sxs-lookup"><span data-stu-id="729ef-133">Property</span></span> | <span data-ttu-id="729ef-134">설명</span><span class="sxs-lookup"><span data-stu-id="729ef-134">Description</span></span> | <span data-ttu-id="729ef-135">필수</span><span class="sxs-lookup"><span data-stu-id="729ef-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="729ef-136">**type**</span><span class="sxs-lookup"><span data-stu-id="729ef-136">**type**</span></span> |<span data-ttu-id="729ef-137">type 속성은 **AzureDataLakeAnalytics**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-137">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="729ef-138">예</span><span class="sxs-lookup"><span data-stu-id="729ef-138">Yes</span></span> |
| <span data-ttu-id="729ef-139">**accountName**</span><span class="sxs-lookup"><span data-stu-id="729ef-139">**accountName**</span></span> |<span data-ttu-id="729ef-140">Azure 데이터 레이크 분석 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="729ef-141">예</span><span class="sxs-lookup"><span data-stu-id="729ef-141">Yes</span></span> |
| <span data-ttu-id="729ef-142">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="729ef-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="729ef-143">Azure 데이터 레이크 분석 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="729ef-144">아니요</span><span class="sxs-lookup"><span data-stu-id="729ef-144">No</span></span> |
| <span data-ttu-id="729ef-145">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="729ef-145">**subscriptionId**</span></span> |<span data-ttu-id="729ef-146">Azure 구독 ID</span><span class="sxs-lookup"><span data-stu-id="729ef-146">Azure subscription id</span></span> |<span data-ttu-id="729ef-147">아니요(지정하지 않으면 Data Factory의 구독이 사용됨).</span><span class="sxs-lookup"><span data-stu-id="729ef-147">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="729ef-148">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="729ef-148">**resourceGroupName**</span></span> |<span data-ttu-id="729ef-149">Azure 리소스 그룹 이름</span><span class="sxs-lookup"><span data-stu-id="729ef-149">Azure resource group name</span></span> |<span data-ttu-id="729ef-150">아니요(지정하지 않으면 Data Factory의 리소스 그룹이 사용됨).</span><span class="sxs-lookup"><span data-stu-id="729ef-150">No (If not specified, resource group of the data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="729ef-151">서비스 주체 인증(권장)</span><span class="sxs-lookup"><span data-stu-id="729ef-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="729ef-152">서비스 주체 인증을 사용하려면 Azure AD(Azure Active Directory)에서 응용 프로그램 엔터티를 등록한 후 Data Lake Store에서 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-152">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="729ef-153">자세한 단계는 [서비스 간 인증](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="729ef-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="729ef-154">연결된 서비스를 정의하는 데 사용되므로 다음 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-154">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="729ef-155">응용 프로그램 UI</span><span class="sxs-lookup"><span data-stu-id="729ef-155">Application ID</span></span>
* <span data-ttu-id="729ef-156">응용 프로그램 키</span><span class="sxs-lookup"><span data-stu-id="729ef-156">Application key</span></span> 
* <span data-ttu-id="729ef-157">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="729ef-157">Tenant ID</span></span>

<span data-ttu-id="729ef-158">다음 속성을 지정하여 서비스 주체 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-158">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="729ef-159">속성</span><span class="sxs-lookup"><span data-stu-id="729ef-159">Property</span></span> | <span data-ttu-id="729ef-160">설명</span><span class="sxs-lookup"><span data-stu-id="729ef-160">Description</span></span> | <span data-ttu-id="729ef-161">필수</span><span class="sxs-lookup"><span data-stu-id="729ef-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="729ef-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="729ef-162">**servicePrincipalId**</span></span> | <span data-ttu-id="729ef-163">응용 프로그램의 클라이언트 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-163">Specify the application's client ID.</span></span> | <span data-ttu-id="729ef-164">예</span><span class="sxs-lookup"><span data-stu-id="729ef-164">Yes</span></span> |
| <span data-ttu-id="729ef-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="729ef-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="729ef-166">응용 프로그램의 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-166">Specify the application's key.</span></span> | <span data-ttu-id="729ef-167">예</span><span class="sxs-lookup"><span data-stu-id="729ef-167">Yes</span></span> |
| <span data-ttu-id="729ef-168">**테넌트**</span><span class="sxs-lookup"><span data-stu-id="729ef-168">**tenant**</span></span> | <span data-ttu-id="729ef-169">응용 프로그램이 있는 테넌트 정보(도메인 이름 또는 테넌트 ID)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-169">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="729ef-170">Azure Portal의 오른쪽 위 모서리에 마우스를 이동하여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-170">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="729ef-171">예</span><span class="sxs-lookup"><span data-stu-id="729ef-171">Yes</span></span> |

<span data-ttu-id="729ef-172">**예제: 서비스 주체 인증**</span><span class="sxs-lookup"><span data-stu-id="729ef-172">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="729ef-173">사용자 자격 증명 인증</span><span class="sxs-lookup"><span data-stu-id="729ef-173">User credential authentication</span></span>
<span data-ttu-id="729ef-174">또는 다음 속성을 지정하여 Data Lake Analytics에 대해 사용자 자격 증명 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying the following properties:</span></span>

| <span data-ttu-id="729ef-175">속성</span><span class="sxs-lookup"><span data-stu-id="729ef-175">Property</span></span> | <span data-ttu-id="729ef-176">설명</span><span class="sxs-lookup"><span data-stu-id="729ef-176">Description</span></span> | <span data-ttu-id="729ef-177">필수</span><span class="sxs-lookup"><span data-stu-id="729ef-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="729ef-178">**권한 부여**</span><span class="sxs-lookup"><span data-stu-id="729ef-178">**authorization**</span></span> | <span data-ttu-id="729ef-179">Data Factory 편집기에서 **권한 부여** 단추를 클릭하고 자격 증명을 입력합니다. 그러면 자동 생성된 authorization URL이 이 속성에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-179">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="729ef-180">예</span><span class="sxs-lookup"><span data-stu-id="729ef-180">Yes</span></span> |
| <span data-ttu-id="729ef-181">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="729ef-181">**sessionId**</span></span> | <span data-ttu-id="729ef-182">OAuth 권한 부여 세션에서 가져온 OAuth 세션 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-182">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="729ef-183">각 세션 ID는 고유하고 한 번만 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="729ef-184">이 설정은 Data Factory 편집기를 사용하는 경우 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-184">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="729ef-185">예</span><span class="sxs-lookup"><span data-stu-id="729ef-185">Yes</span></span> |

<span data-ttu-id="729ef-186">**예제: 사용자 자격 증명 인증**</span><span class="sxs-lookup"><span data-stu-id="729ef-186">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="729ef-187">토큰 만료</span><span class="sxs-lookup"><span data-stu-id="729ef-187">Token expiration</span></span>
<span data-ttu-id="729ef-188">**권한 부여** 단추를 사용하여 생성된 인증 코드는 잠시 후 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-188">The authorization code you generated by using the **Authorize** button expires after sometime.</span></span> <span data-ttu-id="729ef-189">다양한 유형의 사용자 계정에 대한 만료 시간은 다음 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="729ef-189">See the following table for the expiration times for different types of user accounts.</span></span> <span data-ttu-id="729ef-190">인증 **토큰이 만료**되는 경우 다음과 같은 오류 메시지가 표시될 수 있습니다. 자격 증명 작업 오류: invalid_grant - AADSTS70002: 자격 증명 유효성 검사 오류.</span><span class="sxs-lookup"><span data-stu-id="729ef-190">You may see the following error message when the authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="729ef-191">"자격 증명 작업 오류: invalid_grant - AADSTS70002: 자격 증명의 유효성 검사 오류 AADSTS70008: 제공된 액세스 권한 부여가 만료되었거나 해지됩니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-191">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="729ef-192">추적 ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 상관관계 ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 타임스탬프: 2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="729ef-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="729ef-193">사용자 유형</span><span class="sxs-lookup"><span data-stu-id="729ef-193">User type</span></span> | <span data-ttu-id="729ef-194">다음 시간 후에 만료</span><span class="sxs-lookup"><span data-stu-id="729ef-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="729ef-195">Azure Active Directory에서 관리되지 않는 사용자 계정(@hotmail.com, @live.com 등)</span><span class="sxs-lookup"><span data-stu-id="729ef-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="729ef-196">12시간</span><span class="sxs-lookup"><span data-stu-id="729ef-196">12 hours</span></span> |
| <span data-ttu-id="729ef-197">AAD(Azure Active Directory)에서 관리되는 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="729ef-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="729ef-198">마지막 조각이 실행된 후 14일</span><span class="sxs-lookup"><span data-stu-id="729ef-198">14 days after the last slice run.</span></span> <br/><br/><span data-ttu-id="729ef-199">OAuth 기반 연결된 서비스를 기반으로 하는 조각이 14일마다 한 번 이상 실행된 경우 90일</span><span class="sxs-lookup"><span data-stu-id="729ef-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="729ef-200">이 오류를 방지/해결하려면 **토큰이 만료**되면 **권한 부여** 단추를 사용하여 다시 인증하고 연결된 서비스를 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-200">To avoid/resolve this error, reauthorize using the **Authorize** button when the **token expires** and redeploy the linked service.</span></span> <span data-ttu-id="729ef-201">다음과 같은 코드를 사용하여 프로그래밍 방식으로 **sessionId** 및 **권한 부여** 속성의 값을 생성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

<span data-ttu-id="729ef-202">코드에 사용되는 Data Factory 클래스에 대한 세부 정보는 [AzureDataLakeStoreLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx) 및 [AuthorizationSessionGetResponse 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="729ef-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about the Data Factory classes used in the code.</span></span> <span data-ttu-id="729ef-203">WindowsFormsWebAuthenticationDialog 클래스의 Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for the WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="729ef-204">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="729ef-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="729ef-205">다음 JSON 조각은 Data Lake Analytics U-SQL 작업이 포함된 파이프라인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-205">The following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="729ef-206">작업 정의에 앞에서 만든 Azure Data Lake Analytics 연결된 서비스에 대한 참조가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-206">The activity definition has a reference to the Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline to compute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="729ef-207">다음 표에는 이 작업과 관련된 속성 이름과 설명이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-207">The following table describes names and descriptions of properties that are specific to this activity.</span></span> 

| <span data-ttu-id="729ef-208">속성</span><span class="sxs-lookup"><span data-stu-id="729ef-208">Property</span></span> | <span data-ttu-id="729ef-209">설명</span><span class="sxs-lookup"><span data-stu-id="729ef-209">Description</span></span> | <span data-ttu-id="729ef-210">필수</span><span class="sxs-lookup"><span data-stu-id="729ef-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="729ef-211">형식</span><span class="sxs-lookup"><span data-stu-id="729ef-211">type</span></span> |<span data-ttu-id="729ef-212">type 속성은 **DataLakeAnalyticsU-SQL**로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-212">The type property must be set to **DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="729ef-213">예</span><span class="sxs-lookup"><span data-stu-id="729ef-213">Yes</span></span> |
| <span data-ttu-id="729ef-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="729ef-214">scriptPath</span></span> |<span data-ttu-id="729ef-215">U-SQL 스크립트가 포함된 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-215">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="729ef-216">파일 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-216">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="729ef-217">아니요(스크립트를 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="729ef-217">No (if you use script)</span></span> |
| <span data-ttu-id="729ef-218">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="729ef-218">scriptLinkedService</span></span> |<span data-ttu-id="729ef-219">스크립트가 포함된 저장소를 Data Factory에 연결하는 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-219">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="729ef-220">아니요(스크립트를 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="729ef-220">No (if you use script)</span></span> |
| <span data-ttu-id="729ef-221">script</span><span class="sxs-lookup"><span data-stu-id="729ef-221">script</span></span> |<span data-ttu-id="729ef-222">scriptPath 및 scriptLinkedService를 지정하는 대신 인라인 스크립트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="729ef-223">예: `"script": "CREATE DATABASE test"`</span><span class="sxs-lookup"><span data-stu-id="729ef-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="729ef-224">아니요(scriptPath 및 scriptLinkedService를 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="729ef-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="729ef-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="729ef-225">degreeOfParallelism</span></span> |<span data-ttu-id="729ef-226">작업을 실행하는 데 동시에 사용되는 최대 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-226">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="729ef-227">아니요</span><span class="sxs-lookup"><span data-stu-id="729ef-227">No</span></span> |
| <span data-ttu-id="729ef-228">우선 순위</span><span class="sxs-lookup"><span data-stu-id="729ef-228">priority</span></span> |<span data-ttu-id="729ef-229">대기열에 있는 모든 작업 중에서 먼저 실행해야 하는 작업을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-229">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="729ef-230">번호가 낮을수록 우선 순위가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-230">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="729ef-231">아니요</span><span class="sxs-lookup"><span data-stu-id="729ef-231">No</span></span> |
| <span data-ttu-id="729ef-232">매개 변수</span><span class="sxs-lookup"><span data-stu-id="729ef-232">parameters</span></span> |<span data-ttu-id="729ef-233">U-SQL 스크립트의 매개 변수</span><span class="sxs-lookup"><span data-stu-id="729ef-233">Parameters for the U-SQL script</span></span> |<span data-ttu-id="729ef-234">아니요</span><span class="sxs-lookup"><span data-stu-id="729ef-234">No</span></span> |
| <span data-ttu-id="729ef-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="729ef-235">runtimeVersion</span></span> | <span data-ttu-id="729ef-236">사용할 U-SQL 엔진의 런타임 버전</span><span class="sxs-lookup"><span data-stu-id="729ef-236">Runtime version of the U-SQL engine to use</span></span> | <span data-ttu-id="729ef-237">아니요</span><span class="sxs-lookup"><span data-stu-id="729ef-237">No</span></span> | 
| <span data-ttu-id="729ef-238">compilationMode</span><span class="sxs-lookup"><span data-stu-id="729ef-238">compilationMode</span></span> | <p><span data-ttu-id="729ef-239">U-SQL의 컴파일 모드</span><span class="sxs-lookup"><span data-stu-id="729ef-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="729ef-240">다음 값 중 하나여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="729ef-241">**의미 체계:** 의미 체계 검사 및 필수 온전성 검사만 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="729ef-242">**전체:** 구문 검사, 최적화, 코드 생성 등을 비롯하여 전체 컴파일을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-242">**Full:** Perform the full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="729ef-243">**SingleBox:** TargetType이 SingleBox로 설정된 상태에서 전체 컴파일을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-243">**SingleBox:** Perform the full compilation, with TargetType setting to SingleBox.</span></span></li></ul><p><span data-ttu-id="729ef-244">이 속성에 대한 값을 지정하지 않으면 서버가 최적의 컴파일 모드를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-244">If you don't specify a value for this property, the server determines the optimal compilation mode.</span></span> </p>| <span data-ttu-id="729ef-245">아니요</span><span class="sxs-lookup"><span data-stu-id="729ef-245">No</span></span> | 

<span data-ttu-id="729ef-246">스크립트 정의에 대해서는 [SearchLogProcessing.txt 스크립트 정의](#sample-u-sql-script) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="729ef-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for the script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="729ef-247">샘플 입력 및 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="729ef-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="729ef-248">입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="729ef-248">Input dataset</span></span>
<span data-ttu-id="729ef-249">이 예제에서 입력 데이터는 Azure Data Lake Store(datalake/input 폴더의 SearchLog.tsv 파일)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-249">In this example, the input data resides in an Azure Data Lake Store (SearchLog.tsv file in the datalake/input folder).</span></span> 

```json
{
    "name": "DataLakeTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a><span data-ttu-id="729ef-250">출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="729ef-250">Output dataset</span></span>
<span data-ttu-id="729ef-251">이 예제에서 U-SQL 스크립트에서 생성한 출력 데이터는 Azure Data Lake Store(datalake/output 폴더)에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-251">In this example, the output data produced by the U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="729ef-252">샘플 Azure Data Lake Store 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="729ef-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="729ef-253">다음은 입/출력 데이터 집합에서 사용되는 Azure Data Lake Store 연결된 서비스 샘플의 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-253">Here is the definition of the sample Azure Data Lake Store linked service used by the input/output datasets.</span></span> 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

<span data-ttu-id="729ef-254">JSON 속성에 대한 설명은 [Azure 데이터 레이크 저장소간 데이터 이동](data-factory-azure-datalake-connector.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="729ef-254">See [Move data to and from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="729ef-255">샘플 U-SQL 스크립트</span><span class="sxs-lookup"><span data-stu-id="729ef-255">Sample U-SQL Script</span></span>

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    TO @out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="729ef-256">U-SQL 스크립트의 **@in** 및 **@out** 매개 변수 값은 'parameters' 섹션을 사용하여 ADF를 통해 동적으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-256">The values for **@in** and **@out** parameters in the U-SQL script are passed dynamically by ADF using the ‘parameters’ section.</span></span> <span data-ttu-id="729ef-257">파이프라인 정의에서 ‘parameters’ 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="729ef-257">See the ‘parameters’ section in the pipeline definition.</span></span>

<span data-ttu-id="729ef-258">Azure Data Lake Analytics 서비스에서 실행되는 작업에 대한 파이프라인 정의뿐 아니라 degreeOfParallelism나 우선 순위와 같은 다른 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for the jobs that run on the Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="729ef-259">동적 매개 변수</span><span class="sxs-lookup"><span data-stu-id="729ef-259">Dynamic parameters</span></span>
<span data-ttu-id="729ef-260">샘플 파이프라인 정의에서 in 및 out 매개 변수는 하드 코드된 값으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-260">In the sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="729ef-261">동적 매개 변수를 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-261">It is possible to use dynamic parameters instead.</span></span> <span data-ttu-id="729ef-262">예:</span><span class="sxs-lookup"><span data-stu-id="729ef-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="729ef-263">이 경우 입력 파일은 여전히 /datalake/input 폴더에서 가져오며 출력 파일은 /datalake/output 폴더에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-263">In this case, input files are still picked up from the /datalake/input folder and output files are generated in the /datalake/output folder.</span></span> <span data-ttu-id="729ef-264">파일 이름은 조각 시작 시간에 따라 동적입니다.</span><span class="sxs-lookup"><span data-stu-id="729ef-264">The file names are dynamic based on the slice start time.</span></span>  

