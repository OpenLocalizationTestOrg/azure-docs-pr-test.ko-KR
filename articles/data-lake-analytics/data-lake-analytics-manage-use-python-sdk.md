---
title: "Python을 사용하여 Azure Data Lake Analytics 관리 | Microsoft Docs"
description: "Python을 사용하여 Data Lake Store 계정을 만들고 작업을 제출하는 방법을 알아봅니다. "
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: d4213a19-4d0f-49c9-871c-9cd6ed7cf731
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 31326a32f8748e6cfb8bfe24cda46c511ab59352
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-azure-data-lake-analytics-using-python"></a><span data-ttu-id="72e67-103">Python을 사용하여 Azure Data Lake Analytics 관리</span><span class="sxs-lookup"><span data-stu-id="72e67-103">Manage Azure Data Lake Analytics using Python</span></span>

## <a name="python-versions"></a><span data-ttu-id="72e67-104">Python 버전</span><span class="sxs-lookup"><span data-stu-id="72e67-104">Python versions</span></span>

* <span data-ttu-id="72e67-105">Python의 64비트 버전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-105">Use a 64-bit version of Python.</span></span>
* <span data-ttu-id="72e67-106">**[Python.org 다운로드](https://www.python.org/downloads/)**에서 찾을 수 있는 표준 Python 배포를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-106">You can use the standard Python distribution found at **[Python.org downloads](https://www.python.org/downloads/)**.</span></span> 
* <span data-ttu-id="72e67-107">대부분의 개발자는 **[Anaconda Python 배포](https://www.continuum.io/downloads)** 사용을 편리하게 여깁니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-107">Many developers find it convenient to use the **[Anaconda Python distribution](https://www.continuum.io/downloads)**.</span></span>  
* <span data-ttu-id="72e67-108">이 문서는 표준 Python 배포의 Python 버전 3.6을 사용하여 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-108">This article was written using Python version 3.6 from the standard Python distribution</span></span>

## <a name="install-azure-python-sdk"></a><span data-ttu-id="72e67-109">Azure Python SDK 설치</span><span class="sxs-lookup"><span data-stu-id="72e67-109">Install Azure Python SDK</span></span>

<span data-ttu-id="72e67-110">다음 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-110">Install the following modules:</span></span>

* <span data-ttu-id="72e67-111">**azure-mgmt-resource** 모듈에는 Active Directory에 대한 다른 Azure 모듈이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-111">The **azure-mgmt-resource** module includes other Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="72e67-112">**azure-mgmt-datalake-store** 모듈에는 Azure Data Lake Store 계정 관리 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-112">The **azure-mgmt-datalake-store** module includes the Azure Data Lake Store account management operations.</span></span>
* <span data-ttu-id="72e67-113">**azure-datalake-store** 모듈에는 Azure Data Lake Store 파일 시스템 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-113">The **azure-datalake-store** module includes the Azure Data Lake Store filesystem operations.</span></span> 
* <span data-ttu-id="72e67-114">**azure-datalake-analytics** 모듈에는 Azure Data Lake Analytics 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-114">The **azure-datalake-analytics** module includes the Azure Data Lake Analytics operations.</span></span> 

<span data-ttu-id="72e67-115">먼저 다음 명령을 실행하여 최신 `pip`가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-115">First, ensure you have the latest `pip` by running the following command:</span></span>

```
python -m pip install --upgrade pip
```

<span data-ttu-id="72e67-116">이 문서는 `pip version 9.0.1`을 사용하여 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-116">This document was written using `pip version 9.0.1`.</span></span>

<span data-ttu-id="72e67-117">다음 `pip` 명령을 사용하여 명령줄에서 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-117">Use the following `pip` commands to install the modules from the commandline:</span></span>

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a><span data-ttu-id="72e67-118">새 Python 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="72e67-118">Create a new Python script</span></span>

<span data-ttu-id="72e67-119">다음 코드를 스크립트에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-119">Paste the following code into the script:</span></span>

```python
## Use this only for Azure AD service-to-service authentication
#from azure.common.credentials import ServicePrincipalCredentials

## Use this only for Azure AD end-user authentication
#from azure.common.credentials import UserPassCredentials

## Required for Azure Resource Manager
from azure.mgmt.resource.resources import ResourceManagementClient
from azure.mgmt.resource.resources.models import ResourceGroup

## Required for Azure Data Lake Store account management
from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
from azure.mgmt.datalake.store.models import DataLakeStoreAccount

## Required for Azure Data Lake Store filesystem management
from azure.datalake.store import core, lib, multithread

## Required for Azure Data Lake Analytics account management
from azure.mgmt.datalake.analytics.account import DataLakeAnalyticsAccountManagementClient
from azure.mgmt.datalake.analytics.account.models import DataLakeAnalyticsAccount, DataLakeStoreAccountInfo

## Required for Azure Data Lake Analytics job management
from azure.mgmt.datalake.analytics.job import DataLakeAnalyticsJobManagementClient
from azure.mgmt.datalake.analytics.job.models import JobInformation, JobState, USqlJobProperties

## Required for Azure Data Lake Analytics catalog management
from azure.mgmt.datalake.analytics.catalog import DataLakeAnalyticsCatalogManagementClient

## Use these as needed for your application
import logging, getpass, pprint, uuid, time
```

<span data-ttu-id="72e67-120">이 스크립트를 실행하여 모듈을 가져올 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-120">Run this script to verify that the modules can be imported.</span></span>

## <a name="authentication"></a><span data-ttu-id="72e67-121">인증</span><span class="sxs-lookup"><span data-stu-id="72e67-121">Authentication</span></span>

### <a name="interactive-user-authentication-with-a-pop-up"></a><span data-ttu-id="72e67-122">팝업 항목으로 대화형 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="72e67-122">Interactive user authentication with a pop-up</span></span>

<span data-ttu-id="72e67-123">이 메서드는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-123">This method is not supported.</span></span>

### <a name="interactive-user-authentication-with-a-device-code"></a><span data-ttu-id="72e67-124">장치 코드로 대화형 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="72e67-124">Interactive user authentication with a device code</span></span>

```python
user = input('Enter the user to authenticate with that has permission to subscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a><span data-ttu-id="72e67-125">SPI 및 암호로 비대화형 인증</span><span class="sxs-lookup"><span data-stu-id="72e67-125">Noninteractive authentication with SPI and a secret</span></span>

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a><span data-ttu-id="72e67-126">API 및 인증서로 비대화형 인증</span><span class="sxs-lookup"><span data-stu-id="72e67-126">Noninteractive authentication with API and a certificate</span></span>

<span data-ttu-id="72e67-127">이 메서드는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-127">This method is not supported.</span></span>

## <a name="common-script-variables"></a><span data-ttu-id="72e67-128">일반 스크립트 변수</span><span class="sxs-lookup"><span data-stu-id="72e67-128">Common script variables</span></span>

<span data-ttu-id="72e67-129">이러한 변수는 샘플에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-129">These variables are used in the samples.</span></span>

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-the-clients"></a><span data-ttu-id="72e67-130">클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="72e67-130">Create the clients</span></span>

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="72e67-131">Azure 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="72e67-131">Create an Azure Resource Group</span></span>

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="72e67-132">데이터 레이크 분석 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="72e67-132">Create Data Lake Analytics account</span></span>

<span data-ttu-id="72e67-133">먼저 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-133">First create a store account.</span></span>

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```
<span data-ttu-id="72e67-134">그런 다음 해당 저장소를 사용하는 ADLA 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-134">Then create an ADLA account that uses that store.</span></span>

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```

## <a name="submit-a-job"></a><span data-ttu-id="72e67-135">작업 제출</span><span class="sxs-lookup"><span data-stu-id="72e67-135">Submit a job</span></span>

```python
script = """
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
"""

jobId = str(uuid.uuid4())
jobResult = adlaJobClient.job.create(
    adla,
    jobId,
    JobInformation(
        name='Sample Job',
        type='USql',
        properties=USqlJobProperties(script=script)
    )
)
```

## <a name="wait-for-a-job-to-end"></a><span data-ttu-id="72e67-136">작업이 종료될 때까지 대기</span><span class="sxs-lookup"><span data-stu-id="72e67-136">Wait for a job to end</span></span>

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a><span data-ttu-id="72e67-137">파이프라인 및 되풀이 나열</span><span class="sxs-lookup"><span data-stu-id="72e67-137">List pipelines and recurrences</span></span>
<span data-ttu-id="72e67-138">작업에 파이프라인 또는 되풀이 메타데이터가 첨부되어 있는지에 따라, 파이프라인 및 되풀이를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-138">Depending whether your jobs have pipeline or recurrence metadata attached, you can list pipelines and recurrences.</span></span>

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a><span data-ttu-id="72e67-139">계산 정책 관리</span><span class="sxs-lookup"><span data-stu-id="72e67-139">Manage compute policies</span></span>

<span data-ttu-id="72e67-140">DataLakeAnalyticsAccountManagementClient 개체는 Data Lake Analytics 계정에 대한 계산 정책을 관리하는 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-140">The DataLakeAnalyticsAccountManagementClient object provides methods for managing the compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="72e67-141">계산 정책 나열</span><span class="sxs-lookup"><span data-stu-id="72e67-141">List compute policies</span></span>

<span data-ttu-id="72e67-142">다음 코드는 Data Lake Analytics 계정에 대한 계산 정책 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-142">The following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="72e67-143">새 계산 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="72e67-143">Create a new compute policy</span></span>

<span data-ttu-id="72e67-144">다음 코드는 지정된 사용자가 사용할 수 있는 최대 AU를 50으로, 최소 작업 우선 순위를 250으로 설정하는, Data Lake Analytics 계정에 대한 새 계산 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-144">The following code creates a new compute policy for a Data Lake Analytics account, setting the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a><span data-ttu-id="72e67-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="72e67-145">Next steps</span></span>

- <span data-ttu-id="72e67-146">다른 도구를 사용하여 같은 자습서를 보려면 페이지 맨 위의 탭 선택기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="72e67-146">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
- <span data-ttu-id="72e67-147">U-SQL을 알아보려면 [Azure Data Lake Analytics U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="72e67-147">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
- <span data-ttu-id="72e67-148">관리 작업을 보려면 [Azure Portal을 사용하여 Azure Data Lake Analytics 관리](data-lake-analytics-manage-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="72e67-148">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>

