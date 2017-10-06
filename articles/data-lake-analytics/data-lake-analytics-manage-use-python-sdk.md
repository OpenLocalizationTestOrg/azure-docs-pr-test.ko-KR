---
title: "Azure Data Lake 분석 aaaManage Python을 사용 하 여 | Microsoft Docs"
description: "데이터 레이크 저장 하는 Python toocreate toouse 방법에 대해 알아봅니다 계정을 한 작업을 제출 합니다. "
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
ms.openlocfilehash: 3c0fff155db7c4fd4e84c2562816995eb156be16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-python"></a>Python을 사용하여 Azure Data Lake Analytics 관리

## <a name="python-versions"></a>Python 버전

* Python의 64비트 버전을 사용합니다.
* Hello 표준 Python 배포에 사용할 수 있습니다  **[Python.org 다운로드](https://www.python.org/downloads/)**합니다. 
* 많은 개발자에 게 편리한 toouse hello 찾을  **[Anaconda Python 배포](https://www.continuum.io/downloads)**합니다.  
* Python 버전 3.6 hello 표준 Python 배포에서 사용 하 여이 문서가 작성 된

## <a name="install-azure-python-sdk"></a>Azure Python SDK 설치

Hello 다음 모듈을 설치 합니다.

* hello **azure mgmt 리소스** 모듈 등 Active Directory에 대 한 다른 Azure 모듈을 포함 합니다.
* hello **mgmt datalake 저장소 azure** 모듈 hello Azure 데이터 레이크 저장소 계정 관리 작업이 포함 됩니다.
* hello **azure datalake 저장소** 모듈 hello Azure 데이터 레이크 저장소 파일 시스템 작업이 포함 됩니다. 
* hello **azure datalake-분석** 모듈 hello Azure Data Lake 분석 작업이 포함 됩니다. 

먼저 확인 하 고 최신 버전의 hello 있는 `pip` hello 다음 명령을 실행 하 여:

```
python -m pip install --upgrade pip
```

이 문서는 `pip version 9.0.1`을 사용하여 작성되었습니다.

Hello 다음을 사용 하 여 `pip` tooinstall hello 모듈 hello 명령줄에서 명령:

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a>새 Python 스크립트 만들기

Hello를 hello 스크립트에 코드를 다음에 붙여 넣습니다.

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

이 스크립트 tooverify 모듈을 가져올 수 있는 해당 hello를 실행 합니다.

## <a name="authentication"></a>인증

### <a name="interactive-user-authentication-with-a-pop-up"></a>팝업 항목으로 대화형 사용자 인증

이 메서드는 지원되지 않습니다.

### <a name="interactive-user-authentication-with-a-device-code"></a>장치 코드로 대화형 사용자 인증

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a>SPI 및 암호로 비대화형 인증

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a>API 및 인증서로 비대화형 인증

이 메서드는 지원되지 않습니다.

## <a name="common-script-variables"></a>일반 스크립트 변수

이러한 변수는 hello 샘플에서 사용 됩니다.

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a>Hello 클라이언트를 만듭니다.

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a>Azure 리소스 그룹 만들기

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a>데이터 레이크 분석 계정 만들기

먼저 저장소 계정을 만듭니다.

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
그런 다음 해당 저장소를 사용하는 ADLA 계정을 만듭니다.

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

## <a name="submit-a-job"></a>작업 제출

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
    too"/data.csv"
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

## <a name="wait-for-a-job-tooend"></a>작업 tooend 때까지 대기

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a>파이프라인 및 되풀이 나열
작업에 파이프라인 또는 되풀이 메타데이터가 첨부되어 있는지에 따라, 파이프라인 및 되풀이를 나열할 수 있습니다.

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a>계산 정책 관리

hello DataLakeAnalyticsAccountManagementClient 개체 hello를 관리 하기 위한 메서드가 계산 Data Lake 분석 계정에 대 한 정책을 제공 합니다.

### <a name="list-compute-policies"></a>계산 정책 나열

hello 코드 다음에 Data Lake 분석 계정에 대 한 계산 정책의 목록을 검색 합니다.

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a>새 계산 정책 만들기

설정 hello 최대 AUs 사용 가능한 toohello 지정한 사용자 too50 및 hello 최소 작업 우선 순위 too250에 코드 다음 hello Data Lake 분석 계정에 대 한 새 계산 정책을 만듭니다.

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a>다음 단계

- toosee hello 같은 다른 도구를 사용 하 여 자습서 hello hello 페이지 위쪽에 hello 탭 선택기를 클릭 합니다.
- toolearn U SQL 참조 [Azure 데이터 레이크 분석 U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md)합니다.
- 관리 작업을 보려면 [Azure Portal을 사용하여 Azure Data Lake Analytics 관리](data-lake-analytics-manage-use-portal.md)를 참조하세요.

