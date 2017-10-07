---
title: "Node.js 용 hello Azure 배치 클라이언트 라이브러리 사용-aaaTutorial | Microsoft Docs"
description: "Azure 일괄 처리의 기본 개념 hello 알아보고 Node.js를 사용 하 여 간단한 솔루션을 구축 합니다."
services: batch
author: shwetams
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: nodejs
ms.topic: hero-article
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: shwetams
ms.openlocfilehash: d2b0ecbe764e7100affd7b02839aef3077b073cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a>Node.js용 Batch SDK 시작

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.JS](batch-nodejs-get-started.md)
>
>

Node.js를 사용 하 여 일괄 처리 클라이언트를 구축 hello 기본 사항 알아보기 [Azure 일괄 처리 Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/)합니다. 일괄 처리 응용 프로그램에 대한 시나리오를 단계별로 이해한 다음 Node.js 클라이언트를 사용하여 설정해 보겠습니다.  

## <a name="prerequisites"></a>필수 조건
이 문서에서는 사용자가 Node.js에 대한 작업 지식을 갖고 있으며 Linux에 익숙하다고 가정합니다. 또한 액세스 권한 toocreate 일괄 처리 및 저장소 서비스와 설정 된 Azure 계정 있다고 가정 합니다.

읽는 것이 좋습니다 [Azure 배치 기술 개요](batch-technical-overview.md) 을 통해 진행 하기 전에 hello 단계가이 문서를 설명 합니다.

## <a name="hello-tutorial-scenario"></a>hello 자습서 시나리오
Hello 일괄 처리 워크플로 시나리오를 살펴보겠습니다. 모든 csv 파일을 Azure Blob 저장소 컨테이너에서 tooJSON 변환 합니다. 다운로드 하는 Python에 작성 된 간단한 스크립트를 했습니다. tooprocess 여러 저장소 계정 컨테이너를 병렬로, Azure 일괄 작업으로 hello 스크립트를 배포할 수 있습니다.

## <a name="azure-batch-architecture"></a>Azure Batch 아키텍처
hello 다음 다이어그램은 어떻게 Azure 일괄 처리 및 Node.js 클라이언트를 사용 하 여 hello Python 스크립트를 확장할 수 있습니다.

![Azure Batch 시나리오](./media/batch-nodejs-get-started/BatchScenario.png)

hello node.js 클라이언트 (자세히 설명 되어 나중에) 준비 작업 및 hello hello 저장소 계정에서 컨테이너 수에 따라 작업 집합을 사용 하 여 일괄 작업을 배포 합니다. Hello github 리포지토리에서 hello 스크립트를 다운로드할 수 있습니다.

* [Node.js 클라이언트](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [준비 작업 셸 스크립트](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [Python csv tooJSON 프로세서](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> 지정 된 hello 링크에서 Node.js 클라이언트 hello Azure 함수 앱으로 배포 된 특정 코드 toobe를 포함 되지 않습니다. 지침 toocreate 하나에 대 한 링크를 따라 toohello를 참조할 수 있습니다.
> - [함수 앱 만들기](../azure-functions/functions-create-first-azure-function.md)
> - [타이머 트리거 함수 만들기](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a>Hello 응용 프로그램 빌드

이제 hello Node.js 클라이언트 작성을 수행 단계씩 hello 프로세스 알려 주세요.

### <a name="step-1-install-azure-batch-sdk"></a>1단계: Azure Batch SDK 설치

Hello npm 설치 명령을 사용 하 여 Node.js 용 Azure 일괄 처리 SDK를 설치할 수 있습니다.

`npm install azure-batch`

이 명령은 hello azure 배치 노드 SDK의 최신 버전을 설치합니다.

>[!Tip]
> Azure 함수 응용 프로그램에서 이동할 수 있습니다 "Kudu 콘솔" hello Azure 함수의 설정 탭 toorun hello npm 설치 명령을 너무 합니다. 이 사례 tooinstall Node.js 용 Azure 일괄 처리 SDK입니다.
>
>

### <a name="step-2-create-an-azure-batch-account"></a>2단계: Azure Batch 계정 만들기

Hello에서 만들 수 있습니다 [Azure 포털](batch-account-create-portal.md) 또는 명령줄에서 ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).

다음은 Azure CLI를 통해 하나 hello 명령을 toocreate 합니다.

리소스 그룹 만들기, 이미 있는 toocreate hello 일괄 처리 계정을 저장할 경우이 단계를 건너뜁니다.

`az group create -n "<resource-group-name>" -l "<location>"`

다음으로 Azure Batch 계정을 만듭니다.

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

각 Batch 계정에는 해당하는 액세스 키가 있습니다. 이러한 키는 Azure 배치 계정에 필요한 toocreate 추가 리소스입니다. 프로덕션 환경에는 것이 좋습니다 toouse Azure 키 자격 증명 모음 toostore 이러한 키가 있습니다. Hello 응용 프로그램에 대 한 주 서비스를 다음 만들 수 있습니다. 이 서비스 보안 주체 hello 응용 프로그램을 사용 하 여 hello 주요 자격 증명 모음에서 OAuth 토큰 tooaccess 키를 만들 수 있습니다.

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

복사 및 hello hello 후속 단계에서 사용 되는 키 toobe 저장.

### <a name="step-3-create-an-azure-batch-service-client"></a>3단계: Azure Batch 서비스 클라이언트 만들기
다음 코드 조각 먼저 hello azure 배치 Node.js 모듈을 가져오는 한 다음 일괄 처리 서비스 클라이언트를 만듭니다. Toofirst 필요한 hello 이전 단계에서 복사한 hello 일괄 처리 계정 키를 가진 SharedKeyCredentials 개체를 만듭니다.

```nodejs
// Initializing Azure Batch variables

var batch = require('azure-batch');

var accountName = '<azure-batch-account-name>';

var accountKey = '<account-key-downloaded>';

var accountUrl = '<account-url>'

// Create Batch credentials object using account name and account key

var credentials = new batch.SharedKeyCredentials(accountName,accountKey);

// Create Batch service client

var batch_client = new batch.ServiceClient(credentials,accountUrl);

```

Azure 일괄 처리 URI hello hello Azure 포털의 hello 개요 탭에서 찾을 수 있습니다. Hello 형식입니다.

`https://accountname.location.batch.azure.com`

Toohello 스크린 샷을 참조 하십시오.

![Azure batch uri](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a>4단계: Azure Batch 풀 만들기
Azure Batch 풀은 여러 VM(Batch 노드라고도 함)으로 구성됩니다. Azure 일괄 처리 서비스 이러한 노드에서 hello 작업 배포 및에서 자동으로 관리 합니다. Hello 수행 하면 풀에 대 한 구성 매개 변수를 정의할 수 있습니다.

* 가상 컴퓨터 이미지의 유형
* 가상 컴퓨터 노드의 크기
* 가상 컴퓨터 노드의 수

> [!Tip]
> hello 크기와 가상 컴퓨터 노드 수에는 원하는 작업에 toorun 그리고 병렬 hello 작업 자체 hello 번호에 따라 크게입니다. Toodetermine hello 이상적인 개수와 크기를 테스트 하는 것이 좋습니다.
>
>

hello 다음 코드 조각에서는 hello 구성 매개 변수 개체입니다.

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating hello VM configuration object with hello SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting hello VM size tooStandard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in hello pool too4
var numVMs = 4
```

> [!Tip]
> Azure 일괄 처리 및 SKU Id에 사용할 수 있는 Linux VM 이미지의 hello 목록에 대 한 참조 [가상 컴퓨터 이미지 목록을](batch-linux-nodes.md#list-of-virtual-machine-images)합니다.
>
>

Hello 풀 구성에서 정의 되 면 hello Azure 배치 풀을 만들 수 있습니다. 일괄 처리 풀 명령 hello Azure 가상 컴퓨터 노드가 만들고 toobe 준비 tooreceive 작업 tooexecute를 준비 합니다. 각 풀에는 후속 단계에서 참조할 고유 ID가 있어야 합니다.

다음 코드 조각 hello Azure 배치 풀을 만듭니다.

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

만든 hello 풀의 hello 상태를 확인할 수 있으며 hello 상태 인지 확인 "활성" 작업 toothat 풀의 제출으로 계속 진행 하기 전에 수 있습니다.

```nodejs
var cloudPool = batch_client.pool.get(poolid,function(error,result,request,response){
        if(error == null)
        {

            if(result.state == "active")
            {
                console.log("Pool is active");
            }
        }
        else
        {
            if(error.statusCode==404)
            {
                console.log("Pool not found yet returned 404...");    

            }
            else
            {
                console.log("Error occurred while retrieving pool data");
            }
        }
        });
```

다음은 예제 결과 hello pool.get 함수에서 반환 된 개체입니다.

```
{ id: 'processcsv_201721152',
  displayName: 'processcsv_201721152',
  url: 'https://<batch-account-name>.centralus.batch.azure.com/pools/processcsv_201721152',
  eTag: '<eTag>',
  lastModified: 2017-03-27T10:28:02.398Z,
  creationTime: 2017-03-27T10:28:02.398Z,
  state: 'active',
  stateTransitionTime: 2017-03-27T10:28:02.398Z,
  allocationState: 'resizing',
  allocationStateTransitionTime: 2017-03-27T10:28:02.398Z,
  vmSize: 'standard_a1',
  virtualMachineConfiguration:
   { imageReference:
      { publisher: 'Canonical',
        offer: 'UbuntuServer',
        sku: '14.04.2-LTS',
        version: 'latest' },
     nodeAgentSKUId: 'batch.node.ubuntu 14.04' },
  resizeTimeout:
   { [Number: 900000]
     _milliseconds: 900000,
     _days: 0,
     _months: 0,
     _data:
      { milliseconds: 0,
        seconds: 0,
        minutes: 15,
        hours: 0,
        days: 0,
        months: 0,
        years: 0 },
     _locale:
      Locale {
        _calendar: [Object],
        _longDateFormat: [Object],
        _invalidDate: 'Invalid date',
        ordinal: [Function: ordinal],
        _ordinalParse: /\d{1,2}(th|st|nd|rd)/,
        _relativeTime: [Object],
        _months: [Object],
        _monthsShort: [Object],
        _week: [Object],
        _weekdays: [Object],
        _weekdaysMin: [Object],
        _weekdaysShort: [Object],
        _meridiemParse: /[ap]\.?m?\.?/i,
        _abbr: 'en',
        _config: [Object],
        _ordinalParseLenient: /\d{1,2}(th|st|nd|rd)|\d{1,2}/ } },
  currentDedicated: 0,
  targetDedicated: 4,
  enableAutoScale: false,
  enableInterNodeCommunication: false,
  maxTasksPerNode: 1,
  taskSchedulingPolicy: { nodeFillType: 'Spread' } }
```


### <a name="step-4-submit-an-azure-batch-job"></a>4단계: Azure Batch 작업 제출
Azure Batch 작업은 유사한 작업의 논리적 그룹입니다. 이 시나리오는 편이 "프로세스 csv tooJSON" 여기의 각 작업은 각 Azure Storage 컨테이너에 있는 csv 파일을 처리할 수 있습니다.

이러한 작업은 병렬로 실행 하 고 hello Azure 배치 서비스에 의해 오케스트레이션 여러 노드 간에 배포.

> [!Tip]
> Hello를 사용할 수 있습니다 [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) 속성 toospecify 단일 노드에서 동시에 실행할 수 있는 작업의 최대 수입니다.
>
>

#### <a name="preparation-task"></a>준비 작업

만든 hello VM 노드는 빈 Ubuntu 노드입니다. 필수 구성 요소로 일련의 프로그램 tooinstall을 할 경우가 있습니다.
일반적으로 Linux 노드에 대 한 hello 실제 작업을 실행 하기 전에 hello 필수 구성 요소를 설치 하는 셸 스크립트를 사용할 수 있습니다. 그러나 프로그래밍 방식의 실행 파일일 수 있습니다.
hello [셸 스크립트](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) 이 예제에서는 Python pip와 설치 hello Azure 저장소 SDK for Python 합니다.

Hello로 스크립트를 Azure 저장소 계정에 업로드 및 SAS URI tooaccess hello 스크립트를 생성 합니다. Azure 저장소 Node.js SDK hello를 사용 하 여이 프로세스를 자동화할 수도 있습니다.

> [!Tip]
> 작업에 대 한 준비 작업에서 특정 작업 hello 필요한 toorun hello VM 노드로 에서만 실행 됩니다. 실행 되는 hello 작업에 관계 없이 모든 노드에 설치 필수 구성 요소 toobe 경우 hello를 사용할 수 있습니다 [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) 풀을 추가 하는 동안 속성입니다. 다음 참조에 대 한 작업 정의 준비 하는 hello를 사용할 수 있습니다.
>
>

준비 작업은 Azure 일괄 처리 작업의 hello 제출 하는 동안 지정 됩니다. 다음은 준비 작업에 대 한 구성 매개 변수를 hello:

* **ID**: hello 준비 작업에 대 한 고유 식별자
* **commandLine**: 명령줄 tooexecute hello 작업 실행
* **resourceFiles**: 파일의 세부 정보를 제공 하는 개체의 배열 toobe 작업 toorun이에 대 한 다운로드 필요 합니다.  다음은 해당 옵션입니다.
    - blobSource: hello hello 파일의 SAS URI
    - filePath: 로컬 경로 toodownload hello 파일 저장
    - fileMode: Linux 노드에만 적용되는 fileMode는 8진수 형식이며 기본값은 0770
* **waitForSuccess**: 집합 tootrue, hello 작업 준비 작업에 실패에서 실행 되지 않을 경우
* **runElevated**: 높은 권한이 필요한 toorun hello 작업 경우 tootrue을 설정 합니다.

다음 코드 조각 hello 준비 작업 스크립트 구성 샘플을 보여 줍니다.

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

작업 toorun에 대 한 설치 필수 구성 요소 toobe 없는 경우에 hello 준비 작업을 건너뛸 수 있습니다. 다음 코드는 표시 이름이 "csv 파일 처리"인 작업을 만듭니다.

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job toohello pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a>5단계: 작업에 대한 Azure Batch 작업 제출

csv 처리 작업을 만들었으니, 해당 작업에 대한 작업을 만들겠습니다. 4 개의 컨테이너 있다고 가정할 경우, 각 컨테이너에 대해 하나씩 toocreate 4 개 작업을 했습니다.

Hello 보면 [Python 스크립트](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), 두 개의 매개 변수를 허용 합니다.

* 컨테이너 이름: hello에서 저장소 컨테이너 toodownload 파일
* 패턴: 파일 이름 패턴의 선택적 매개 변수

있다고 가정해 봅시다 4 개의 컨테이너 "con1", "con2", "con3", "con4" 다음 코드 csv에 대 한 작업 toohello Azure 일괄 처리 작업"프로세스" 앞에서 만든 제출 합니다.

```nodejs
// storing container names in an array
var container_list = ["con1","con2","con3","con4"]
    container_list.forEach(function(val,index){           

           var container_name = val;
           var taskID = container_name + "_process";
           var task_config = {id:taskID,displayName:'process csv in ' + container_name,commandLine:'python processcsv.py --container ' + container_name,resourceFiles:[{'blobSource':'<blob SAS URI>','filePath':'processcsv.py'}]}
           var task = batch_client.task.add(poolid,task_config,function(error,result){
                if(error != null)
                {
                    console.log(error.response);     
                }
                else
                {
                    console.log("Task for container : " + container_name + "submitted successfully");
                }



           });

    });
```

hello 코드는 여러 작업 toohello 풀을 추가합니다. 고 hello 작업 각각 만든 Vm의 hello 풀의 노드에서 실행 됩니다. 작업 수가 hello hello 풀 또는 hello maxTasksPerNode 속성에서 Vm 수를 초과 하면 hello 작업 노드를 제공할 때까지 기다립니다. 이 오케스트레이션은 Azure Batch에서 자동으로 처리됩니다.

hello 포털에 hello 작업 및 작업 상태 보기를 설명 합니다. Hello 목록을 사용 하 고 hello Azure 노드 SDK에서에서 함수를 확인할 수도 있습니다. 세부 정보는 hello 설명서에 나와 있습니다 [링크](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html)합니다.

## <a name="next-steps"></a>다음 단계

- 검토 hello [Azure 배치 개요 기능](batch-api-basics.md) 아티클의 새 toohello 서비스 하는 경우는 것이 좋습니다.
- Hello 참조 [일괄 처리 Node.js 참조](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello API 일괄 처리 합니다.

