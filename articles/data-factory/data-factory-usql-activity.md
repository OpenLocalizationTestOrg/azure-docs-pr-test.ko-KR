---
title: "U-SQL 스크립트-Azure를 사용 하 여 aaaTransform 데이터 | Microsoft Docs"
description: "Azure Data Lake 분석 U-SQL 스크립트를 실행 하 여 tooprocess 또는 변환 데이터 서비스를 계산 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="895fa-103">Azure Data Lake Analytics에서 U-SQL 스크립트를 실행하여 데이터 변환</span><span class="sxs-lookup"><span data-stu-id="895fa-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="895fa-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="895fa-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="895fa-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="895fa-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="895fa-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="895fa-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="895fa-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="895fa-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="895fa-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="895fa-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="895fa-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="895fa-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="895fa-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="895fa-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="895fa-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="895fa-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="895fa-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="895fa-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="895fa-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="895fa-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="895fa-114">Azure 데이터 팩터리의 파이프라인은 연결된 저장소 서비스의 데이터를 연결된 계산 서비스를 사용하여 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="895fa-115">파이프라인에는 일련의 작업이 포함되며 각 작업에서는 특정 처리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="895fa-116">이 문서에서는 hello 설명 **데이터 레이크 분석 U-SQL 작업** 를 실행 하는 **U-SQL** 스크립트는 **Azure 데이터 레이크 분석** 계산 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-116">This article describes hello **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="895fa-117">Data Lake Analytics U-SQL 작업이 포함된 파이프라인을 만들기 전에 Azure Data Lake Analytics 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="895fa-118">Azure Data Lake 분석에 대 한 toolearn 참조 [Azure Data Lake 분석 시작](../data-lake-analytics/data-lake-analytics-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-118">toolearn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="895fa-119">검토 hello [첫 번째 파이프라인 자습서 빌드하](data-factory-build-your-first-pipeline.md) 연결 된 서비스, 데이터 집합 및 파이프라인에 대 한 자세한 단계 toocreate 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-119">Review hello [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps toocreate a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="895fa-120">데이터 팩터리 편집기 또는 Visual Studio 또는 Azure PowerShell toocreate Data Factory 엔터티에 JSON 조각을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell toocreate Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="895fa-121">지원되는 인증 형식</span><span class="sxs-lookup"><span data-stu-id="895fa-121">Supported authentication types</span></span>
<span data-ttu-id="895fa-122">U-SQL 작업은 Data Lake Analytics에 대해 아래 인증 유형을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="895fa-123">서비스 주체 인증</span><span class="sxs-lookup"><span data-stu-id="895fa-123">Service principal authentication</span></span>
* <span data-ttu-id="895fa-124">사용자 자격 증명(OAuth) 인증</span><span class="sxs-lookup"><span data-stu-id="895fa-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="895fa-125">특히 예약된 U-SQL 실행의 경우 서비스 주체 인증을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="895fa-126">사용자 자격 증명 인증의 경우 토큰 만료 동작이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="895fa-127">구성 세부 정보 참조 hello [연결 된 서비스 속성](#azure-data-lake-analytics-linked-service) 섹션.</span><span class="sxs-lookup"><span data-stu-id="895fa-127">For configuration details, see hello [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="895fa-128">Azure 데이터 레이크 분석 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="895fa-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="895fa-129">만들 프로그램 **Azure 데이터 레이크 분석** 서비스 toolink Azure Data Lake 분석 계산 서비스 tooan Azure 데이터 팩터리에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-129">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory.</span></span> <span data-ttu-id="895fa-130">데이터 레이크 분석 U-SQL 작업 hello 파이프라인의 hello toothis 연결 된 서비스를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-130">hello Data Lake Analytics U-SQL activity in hello pipeline refers toothis linked service.</span></span> 

<span data-ttu-id="895fa-131">hello 다음 표에서 hello에 대 한 설명을 hello JSON 정의에서 사용 되는 일반 속성.</span><span class="sxs-lookup"><span data-stu-id="895fa-131">hello following table provides descriptions for hello generic properties used in hello JSON definition.</span></span> <span data-ttu-id="895fa-132">서비스 주체와 사용자 자격 증명 인증 중에서 추가로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="895fa-133">속성</span><span class="sxs-lookup"><span data-stu-id="895fa-133">Property</span></span> | <span data-ttu-id="895fa-134">설명</span><span class="sxs-lookup"><span data-stu-id="895fa-134">Description</span></span> | <span data-ttu-id="895fa-135">필수</span><span class="sxs-lookup"><span data-stu-id="895fa-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="895fa-136">**type**</span><span class="sxs-lookup"><span data-stu-id="895fa-136">**type**</span></span> |<span data-ttu-id="895fa-137">hello type 속성이로 설정 해야: **AzureDataLakeAnalytics**합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-137">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="895fa-138">예</span><span class="sxs-lookup"><span data-stu-id="895fa-138">Yes</span></span> |
| <span data-ttu-id="895fa-139">**accountName**</span><span class="sxs-lookup"><span data-stu-id="895fa-139">**accountName**</span></span> |<span data-ttu-id="895fa-140">Azure 데이터 레이크 분석 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="895fa-141">예</span><span class="sxs-lookup"><span data-stu-id="895fa-141">Yes</span></span> |
| <span data-ttu-id="895fa-142">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="895fa-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="895fa-143">Azure 데이터 레이크 분석 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="895fa-144">아니요</span><span class="sxs-lookup"><span data-stu-id="895fa-144">No</span></span> |
| <span data-ttu-id="895fa-145">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="895fa-145">**subscriptionId**</span></span> |<span data-ttu-id="895fa-146">Azure 구독 ID</span><span class="sxs-lookup"><span data-stu-id="895fa-146">Azure subscription id</span></span> |<span data-ttu-id="895fa-147">아니요 (지정 하지 않으면 데이터 팩터리에 사용 되는 hello의 구독) 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="895fa-147">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="895fa-148">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="895fa-148">**resourceGroupName**</span></span> |<span data-ttu-id="895fa-149">Azure 리소스 그룹 이름</span><span class="sxs-lookup"><span data-stu-id="895fa-149">Azure resource group name</span></span> |<span data-ttu-id="895fa-150">아니요 (지정 하지 않으면 리소스 그룹의 데이터 팩터리에 사용 되는 hello) 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="895fa-150">No (If not specified, resource group of hello data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="895fa-151">서비스 주체 인증(권장)</span><span class="sxs-lookup"><span data-stu-id="895fa-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="895fa-152">toouse 서비스 보안 주체 인증 레지스터 것 hello Azure Active Directory (Azure AD) 및 권한 부여의 응용 프로그램 엔터티 tooData 레이크 스토어에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-152">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="895fa-153">자세한 단계는 [서비스 간 인증](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="895fa-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="895fa-154">사용 되는 값을 다음 hello 기록 toodefine hello 연결 된 서비스:</span><span class="sxs-lookup"><span data-stu-id="895fa-154">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="895fa-155">응용 프로그램 UI</span><span class="sxs-lookup"><span data-stu-id="895fa-155">Application ID</span></span>
* <span data-ttu-id="895fa-156">응용 프로그램 키</span><span class="sxs-lookup"><span data-stu-id="895fa-156">Application key</span></span> 
* <span data-ttu-id="895fa-157">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="895fa-157">Tenant ID</span></span>

<span data-ttu-id="895fa-158">Hello 다음과 같은 속성을 지정 하 여 서비스 사용자 인증을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-158">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="895fa-159">속성</span><span class="sxs-lookup"><span data-stu-id="895fa-159">Property</span></span> | <span data-ttu-id="895fa-160">설명</span><span class="sxs-lookup"><span data-stu-id="895fa-160">Description</span></span> | <span data-ttu-id="895fa-161">필수</span><span class="sxs-lookup"><span data-stu-id="895fa-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="895fa-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="895fa-162">**servicePrincipalId**</span></span> | <span data-ttu-id="895fa-163">Hello 응용 프로그램의 클라이언트 ID를 지정</span><span class="sxs-lookup"><span data-stu-id="895fa-163">Specify hello application's client ID.</span></span> | <span data-ttu-id="895fa-164">예</span><span class="sxs-lookup"><span data-stu-id="895fa-164">Yes</span></span> |
| <span data-ttu-id="895fa-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="895fa-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="895fa-166">Hello 응용 프로그램의 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-166">Specify hello application's key.</span></span> | <span data-ttu-id="895fa-167">예</span><span class="sxs-lookup"><span data-stu-id="895fa-167">Yes</span></span> |
| <span data-ttu-id="895fa-168">**테넌트**</span><span class="sxs-lookup"><span data-stu-id="895fa-168">**tenant**</span></span> | <span data-ttu-id="895fa-169">응용 프로그램에 속한 아래 hello 테 넌 트 정보 (도메인 이름 또는 테 넌 트 ID)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-169">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="895fa-170">Hello Azure 포털의 오른쪽 위 모서리 hello에에서 hello 마우스 호버 하 여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-170">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="895fa-171">예</span><span class="sxs-lookup"><span data-stu-id="895fa-171">Yes</span></span> |

<span data-ttu-id="895fa-172">**예제: 서비스 주체 인증**</span><span class="sxs-lookup"><span data-stu-id="895fa-172">**Example: Service principal authentication**</span></span>
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

### <a name="user-credential-authentication"></a><span data-ttu-id="895fa-173">사용자 자격 증명 인증</span><span class="sxs-lookup"><span data-stu-id="895fa-173">User credential authentication</span></span>
<span data-ttu-id="895fa-174">또는 hello 다음과 같은 속성을 지정 하 여 Data Lake 분석에 대 한 사용자 자격 증명 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying hello following properties:</span></span>

| <span data-ttu-id="895fa-175">속성</span><span class="sxs-lookup"><span data-stu-id="895fa-175">Property</span></span> | <span data-ttu-id="895fa-176">설명</span><span class="sxs-lookup"><span data-stu-id="895fa-176">Description</span></span> | <span data-ttu-id="895fa-177">필수</span><span class="sxs-lookup"><span data-stu-id="895fa-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="895fa-178">**권한 부여**</span><span class="sxs-lookup"><span data-stu-id="895fa-178">**authorization**</span></span> | <span data-ttu-id="895fa-179">Hello 클릭 **Authorize** hello 데이터 팩터리 편집기 단추를 선택한 hello 자동 생성 된 권한 부여 URL toothis 속성을 할당 하 여 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-179">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="895fa-180">예</span><span class="sxs-lookup"><span data-stu-id="895fa-180">Yes</span></span> |
| <span data-ttu-id="895fa-181">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="895fa-181">**sessionId**</span></span> | <span data-ttu-id="895fa-182">Hello OAuth 권한 부여 세션에서 OAuth 세션 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-182">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="895fa-183">각 세션 ID는 고유하고 한 번만 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="895fa-184">이 설정은 hello 데이터 팩터리 편집기를 사용 하는 경우 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-184">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="895fa-185">예</span><span class="sxs-lookup"><span data-stu-id="895fa-185">Yes</span></span> |

<span data-ttu-id="895fa-186">**예제: 사용자 자격 증명 인증**</span><span class="sxs-lookup"><span data-stu-id="895fa-186">**Example: User credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="895fa-187">토큰 만료</span><span class="sxs-lookup"><span data-stu-id="895fa-187">Token expiration</span></span>
<span data-ttu-id="895fa-188">hello를 사용 하 여 생성 하는 인증 코드를 hello **Authorize** 단추 잠시 후에 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-188">hello authorization code you generated by using hello **Authorize** button expires after sometime.</span></span> <span data-ttu-id="895fa-189">다음 표에 다양 한 유형의 사용자 계정에 대 한 만료 시간 hello에 대 한 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="895fa-189">See hello following table for hello expiration times for different types of user accounts.</span></span> <span data-ttu-id="895fa-190">Hello 다음과 같은 오류 메시지가 표시 될 수 있습니다 때 인증 hello **토큰이 만료 된**: 작업 오류를 자격 증명: invalid_grant-AADSTS70002: 자격 증명 유효성 검사 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-190">You may see hello following error message when hello authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="895fa-191">AADSTS70008: hello 액세스 권한 부여가 만료 되었거나 해지 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-191">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="895fa-192">추적 ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 상관관계 ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 타임스탬프: 2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="895fa-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="895fa-193">사용자 유형</span><span class="sxs-lookup"><span data-stu-id="895fa-193">User type</span></span> | <span data-ttu-id="895fa-194">다음 시간 후에 만료</span><span class="sxs-lookup"><span data-stu-id="895fa-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="895fa-195">Azure Active Directory에서 관리되지 않는 사용자 계정(@hotmail.com, @live.com 등)</span><span class="sxs-lookup"><span data-stu-id="895fa-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="895fa-196">12시간</span><span class="sxs-lookup"><span data-stu-id="895fa-196">12 hours</span></span> |
| <span data-ttu-id="895fa-197">AAD(Azure Active Directory)에서 관리되는 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="895fa-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="895fa-198">hello 마지막 조각 실행 한 후 14 일입니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-198">14 days after hello last slice run.</span></span> <br/><br/><span data-ttu-id="895fa-199">OAuth 기반 연결된 서비스를 기반으로 하는 조각이 14일마다 한 번 이상 실행된 경우 90일</span><span class="sxs-lookup"><span data-stu-id="895fa-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="895fa-200">tooavoid/resolve이 오류를 hello를 사용 하 여 권한을 다시 부여 **Authorize** 때 hello 단추 **토큰이 만료 되** hello 연결 된 서비스를 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-200">tooavoid/resolve this error, reauthorize using hello **Authorize** button when hello **token expires** and redeploy hello linked service.</span></span> <span data-ttu-id="895fa-201">다음과 같은 코드를 사용하여 프로그래밍 방식으로 **sessionId** 및 **권한 부여** 속성의 값을 생성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

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

<span data-ttu-id="895fa-202">참조 [AzureDataLakeStoreLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), 및 [AuthorizationSessionGetResponse 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) 세부 정보에 대 한 항목 hello Data Factory 클래스 hello 코드에 사용 정보 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about hello Data Factory classes used in hello code.</span></span> <span data-ttu-id="895fa-203">에 대 한 참조 추가: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll hello WindowsFormsWebAuthenticationDialog 클래스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for hello WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="895fa-204">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="895fa-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="895fa-205">다음 JSON 코드 조각은 hello 파이프라인 데이터 레이크 분석 U-SQL 작업을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-205">hello following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="895fa-206">hello 활동 정의 참조 toohello 앞에서 만든 연결 된 Azure Data Lake 분석 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-206">hello activity definition has a reference toohello Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
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

<span data-ttu-id="895fa-207">hello 다음 표에서 설명 특정 toothis이 작동 하는 속성의 이름 및 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-207">hello following table describes names and descriptions of properties that are specific toothis activity.</span></span> 

| <span data-ttu-id="895fa-208">속성</span><span class="sxs-lookup"><span data-stu-id="895fa-208">Property</span></span> | <span data-ttu-id="895fa-209">설명</span><span class="sxs-lookup"><span data-stu-id="895fa-209">Description</span></span> | <span data-ttu-id="895fa-210">필수</span><span class="sxs-lookup"><span data-stu-id="895fa-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="895fa-211">type</span><span class="sxs-lookup"><span data-stu-id="895fa-211">type</span></span> |<span data-ttu-id="895fa-212">너무 hello 유형 속성을 설정 해야**DataLakeAnalyticsU SQL**합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-212">hello type property must be set too**DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="895fa-213">예</span><span class="sxs-lookup"><span data-stu-id="895fa-213">Yes</span></span> |
| <span data-ttu-id="895fa-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="895fa-214">scriptPath</span></span> |<span data-ttu-id="895fa-215">Hello U-SQL 스크립트를 포함 하는 경로 toofolder 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-215">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="895fa-216">Hello 파일의 이름은 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-216">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="895fa-217">아니요(스크립트를 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="895fa-217">No (if you use script)</span></span> |
| <span data-ttu-id="895fa-218">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="895fa-218">scriptLinkedService</span></span> |<span data-ttu-id="895fa-219">Hello 스크립트 toohello 데이터 팩터리를 포함 하는 hello 저장소를 연결 하는 연결 된 서비스</span><span class="sxs-lookup"><span data-stu-id="895fa-219">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="895fa-220">아니요(스크립트를 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="895fa-220">No (if you use script)</span></span> |
| <span data-ttu-id="895fa-221">script</span><span class="sxs-lookup"><span data-stu-id="895fa-221">script</span></span> |<span data-ttu-id="895fa-222">scriptPath 및 scriptLinkedService를 지정하는 대신 인라인 스크립트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="895fa-223">예: `"script": "CREATE DATABASE test"`</span><span class="sxs-lookup"><span data-stu-id="895fa-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="895fa-224">아니요(scriptPath 및 scriptLinkedService를 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="895fa-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="895fa-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="895fa-225">degreeOfParallelism</span></span> |<span data-ttu-id="895fa-226">hello 최대 노드 수는 동시에 toorun hello 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-226">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="895fa-227">아니요</span><span class="sxs-lookup"><span data-stu-id="895fa-227">No</span></span> |
| <span data-ttu-id="895fa-228">우선 순위</span><span class="sxs-lookup"><span data-stu-id="895fa-228">priority</span></span> |<span data-ttu-id="895fa-229">먼저 어떤 작업에서 대기 중인 모든 선택한 toorun 해야를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-229">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="895fa-230">hello 낮은 hello 수치로 hello hello 우선 순위가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-230">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="895fa-231">아니요</span><span class="sxs-lookup"><span data-stu-id="895fa-231">No</span></span> |
| <span data-ttu-id="895fa-232">매개 변수</span><span class="sxs-lookup"><span data-stu-id="895fa-232">parameters</span></span> |<span data-ttu-id="895fa-233">Hello U-SQL 스크립트의 매개 변수</span><span class="sxs-lookup"><span data-stu-id="895fa-233">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="895fa-234">아니요</span><span class="sxs-lookup"><span data-stu-id="895fa-234">No</span></span> |
| <span data-ttu-id="895fa-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="895fa-235">runtimeVersion</span></span> | <span data-ttu-id="895fa-236">Hello U-SQL 엔진 toouse의 런타임 버전</span><span class="sxs-lookup"><span data-stu-id="895fa-236">Runtime version of hello U-SQL engine toouse</span></span> | <span data-ttu-id="895fa-237">아니요</span><span class="sxs-lookup"><span data-stu-id="895fa-237">No</span></span> | 
| <span data-ttu-id="895fa-238">compilationMode</span><span class="sxs-lookup"><span data-stu-id="895fa-238">compilationMode</span></span> | <p><span data-ttu-id="895fa-239">U-SQL의 컴파일 모드</span><span class="sxs-lookup"><span data-stu-id="895fa-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="895fa-240">다음 값 중 하나여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="895fa-241">**의미 체계:** 의미 체계 검사 및 필수 온전성 검사만 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="895fa-242">**전체:** 구문 검사, 최적화, 코드 생성 등을 포함 하 여 hello 전체 컴파일을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-242">**Full:** Perform hello full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="895fa-243">**SingleBox:** TargetType 설정 tooSingleBox와 hello 전체 컴파일을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-243">**SingleBox:** Perform hello full compilation, with TargetType setting tooSingleBox.</span></span></li></ul><p><span data-ttu-id="895fa-244">이 속성에 대 한 값을 지정 하지 않으면, hello 서버 hello 최적의 컴파일 모드를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-244">If you don't specify a value for this property, hello server determines hello optimal compilation mode.</span></span> </p>| <span data-ttu-id="895fa-245">아니요</span><span class="sxs-lookup"><span data-stu-id="895fa-245">No</span></span> | 

<span data-ttu-id="895fa-246">참조 [SearchLogProcessing.txt 스크립트 정의](#sample-u-sql-script) hello 스크립트 정의 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for hello script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="895fa-247">샘플 입력 및 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="895fa-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="895fa-248">입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="895fa-248">Input dataset</span></span>
<span data-ttu-id="895fa-249">이 예제에서는 hello 입력된 데이터는 Azure 데이터 레이크 저장소 (SearchLog.tsv hello datalake/입력 폴더에 파일)에 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-249">In this example, hello input data resides in an Azure Data Lake Store (SearchLog.tsv file in hello datalake/input folder).</span></span> 

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

### <a name="output-dataset"></a><span data-ttu-id="895fa-250">출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="895fa-250">Output dataset</span></span>
<span data-ttu-id="895fa-251">이 예제에서는 hello U-SQL 스크립트에서 생성 하는 hello 출력 데이터는 Azure 데이터 레이크 저장소 (datalake/출력 폴더)에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-251">In this example, hello output data produced by hello U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

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

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="895fa-252">샘플 Azure Data Lake Store 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="895fa-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="895fa-253">Azure 데이터 레이크 저장소 연결 된 hello 입/출력 데이터 집합에서 사용 하는 서비스는 hello 샘플의 hello 정의 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-253">Here is hello definition of hello sample Azure Data Lake Store linked service used by hello input/output datasets.</span></span> 

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

<span data-ttu-id="895fa-254">참조 [Azure 데이터 레이크 저장소에서 데이터 tooand 이동](data-factory-azure-datalake-connector.md) 문서 JSON 속성에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-254">See [Move data tooand from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="895fa-255">샘플 U-SQL 스크립트</span><span class="sxs-lookup"><span data-stu-id="895fa-255">Sample U-SQL Script</span></span>

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
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="895fa-256">에 대 한 값을 hello  **@in**  및  **@out**  hello U-SQL 스크립트의 매개 변수는 전달 되 동적으로 ADF hello 'parameters' 섹션을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-256">hello values for **@in** and **@out** parameters in hello U-SQL script are passed dynamically by ADF using hello ‘parameters’ section.</span></span> <span data-ttu-id="895fa-257">Hello 파이프라인 정의 hello 'parameters' 섹션을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-257">See hello ‘parameters’ section in hello pipeline definition.</span></span>

<span data-ttu-id="895fa-258">Hello Azure Data Lake 분석 서비스에서 실행 되는 hello 작업에 대 한 파이프라인 정의에 degreeOfParallelism 및 우선 순위와 같은 기타 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for hello jobs that run on hello Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="895fa-259">동적 매개 변수</span><span class="sxs-lookup"><span data-stu-id="895fa-259">Dynamic parameters</span></span>
<span data-ttu-id="895fa-260">시작 및 종료 hello 샘플 파이프라인 정의에서 매개 변수 하드 코드 된 값으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-260">In hello sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="895fa-261">호스팅하려는 가능한 toouse 동적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-261">It is possible toouse dynamic parameters instead.</span></span> <span data-ttu-id="895fa-262">예:</span><span class="sxs-lookup"><span data-stu-id="895fa-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="895fa-263">이 경우 hello /datalake/input 폴더에서 입력된 파일은 여전히 획득 하 고 hello /datalake/output 폴더에 출력 파일이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-263">In this case, input files are still picked up from hello /datalake/input folder and output files are generated in hello /datalake/output folder.</span></span> <span data-ttu-id="895fa-264">hello 파일 이름은 hello 조각 시작 시간에 기반 하는 동적입니다.</span><span class="sxs-lookup"><span data-stu-id="895fa-264">hello file names are dynamic based on hello slice start time.</span></span>  

