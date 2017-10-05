---
title: "자습서 - Node.js용 Azure Batch 클라이언트 라이브러리 사용 | Microsoft Docs"
description: "Azure Batch의 기본 개념을 알아보고 Node.js를 사용하여 간단한 솔루션을 빌드합니다."
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
ms.openlocfilehash: c48171d8634a651718a0775183414f463c6a468c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a><span data-ttu-id="929ce-103">Node.js용 Batch SDK 시작</span><span class="sxs-lookup"><span data-stu-id="929ce-103">Get started with Batch SDK for Node.js</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="929ce-104">.NET</span><span class="sxs-lookup"><span data-stu-id="929ce-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="929ce-105">Python</span><span class="sxs-lookup"><span data-stu-id="929ce-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="929ce-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="929ce-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="929ce-107">[Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/)를 사용하여 Node.js로 Batch 클라이언트를 빌드하는 기본 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-107">Learn the basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span></span> <span data-ttu-id="929ce-108">일괄 처리 응용 프로그램에 대한 시나리오를 단계별로 이해한 다음 Node.js 클라이언트를 사용하여 설정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-108">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="929ce-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="929ce-109">Prerequisites</span></span>
<span data-ttu-id="929ce-110">이 문서에서는 사용자가 Node.js에 대한 작업 지식을 갖고 있으며 Linux에 익숙하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-110">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span></span> <span data-ttu-id="929ce-111">또한 Batch 및 Storage 서비스를 만들 액세스 권한이 있는 Azure 계정을 갖고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-111">It also assumes that you have an Azure account setup with access rights to create Batch and Storage services.</span></span>

<span data-ttu-id="929ce-112">이 문서에 설명된 단계를 진행하기 전에 [Azure Batch 기술 개요](batch-technical-overview.md)를 읽어 보시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-112">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through the steps outlined this article.</span></span>

## <a name="the-tutorial-scenario"></a><span data-ttu-id="929ce-113">자습서 시나리오</span><span class="sxs-lookup"><span data-stu-id="929ce-113">The tutorial scenario</span></span>
<span data-ttu-id="929ce-114">일괄 처리 워크플로 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-114">Let us understand the batch workflow scenario.</span></span> <span data-ttu-id="929ce-115">Azure Blob Storage 컨테이너에서 모든 csv 파일을 다운로드하여 JSON으로 변환하는 Python으로 작성된 간단한 스크립트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-115">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them to JSON.</span></span> <span data-ttu-id="929ce-116">여러 저장소 계정 컨테이너를 병렬로 처리하려면 스크립트를 Azure Batch 작업으로 배포하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-116">To process multiple storage account containers in parallel, we can deploy the script as an Azure Batch job.</span></span>

## <a name="azure-batch-architecture"></a><span data-ttu-id="929ce-117">Azure Batch 아키텍처</span><span class="sxs-lookup"><span data-stu-id="929ce-117">Azure Batch Architecture</span></span>
<span data-ttu-id="929ce-118">다음 다이어그램은 Azure Batch 및 Node.js 클라이언트를 사용하여 Python 스크립트를 확장하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-118">The following diagram depicts how we can scale the Python script using Azure Batch and a Node.js client.</span></span>

![Azure Batch 시나리오](./media/batch-nodejs-get-started/BatchScenario.png)

<span data-ttu-id="929ce-120">Node.js 클라이언트는 저장소 계정에 있는 컨테이너의 수에 따라 준비 작업(나중에 자세히 설명)과 작업 집합을 사용하여 일괄 처리 작업을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-120">The node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on the number of containers in the storage account.</span></span> <span data-ttu-id="929ce-121">github 리포지토리에서 스크립트를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-121">You can download the scripts from the github repository.</span></span>

* [<span data-ttu-id="929ce-122">Node.js 클라이언트</span><span class="sxs-lookup"><span data-stu-id="929ce-122">Node.js client</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [<span data-ttu-id="929ce-123">준비 작업 셸 스크립트</span><span class="sxs-lookup"><span data-stu-id="929ce-123">Preparation task shell scripts</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [<span data-ttu-id="929ce-124">Python csv-JSON 프로세서</span><span class="sxs-lookup"><span data-stu-id="929ce-124">Python csv to JSON processor</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> <span data-ttu-id="929ce-125">지정된 링크의 Node.js 클라이언트는 Azure 함수 앱으로 배포될 특정 코드를 포함하고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-125">The Node.js client in the link specified does not contain specific code to be deployed as an Azure function app.</span></span> <span data-ttu-id="929ce-126">만드는 방법에 대한 지침은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="929ce-126">You can refer to the following links for instructions to create one.</span></span>
> - [<span data-ttu-id="929ce-127">함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="929ce-127">Create function app</span></span>](../azure-functions/functions-create-first-azure-function.md)
> - [<span data-ttu-id="929ce-128">타이머 트리거 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="929ce-128">Create timer trigger function</span></span>](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-the-application"></a><span data-ttu-id="929ce-129">응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="929ce-129">Build the application</span></span>

<span data-ttu-id="929ce-130">이제 단계별 프로세스에 따라 Node.js 클라이언트를 빌드하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-130">Now, let us follow the process step by step into building the Node.js client:</span></span>

### <a name="step-1-install-azure-batch-sdk"></a><span data-ttu-id="929ce-131">1단계: Azure Batch SDK 설치</span><span class="sxs-lookup"><span data-stu-id="929ce-131">Step 1: Install Azure Batch SDK</span></span>

<span data-ttu-id="929ce-132">npm install 명령을 사용하여 Node.js용 Azure Batch SDK를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-132">You can install Azure Batch SDK for Node.js using the npm install command.</span></span>

`npm install azure-batch`

<span data-ttu-id="929ce-133">이 명령은 최신 버전의 azure-batch 노드 SDK를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-133">This command installs the latest version of azure-batch node SDK.</span></span>

>[!Tip]
> <span data-ttu-id="929ce-134">Azure 함수 앱의 Azure 함수 설정 탭에서 "Kudu 콘솔"로 이동하여 npm install 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-134">In an Azure Function app, you can go to "Kudu Console" in the Azure function's Settings tab to run the npm install commands.</span></span> <span data-ttu-id="929ce-135">이 예에서는 Node.js용 Azure Batch SDK를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-135">In this case to install Azure Batch SDK for Node.js.</span></span>
>
>

### <a name="step-2-create-an-azure-batch-account"></a><span data-ttu-id="929ce-136">2단계: Azure Batch 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="929ce-136">Step 2: Create an Azure Batch account</span></span>

<span data-ttu-id="929ce-137">[Azure Portal](batch-account-create-portal.md) 또는 명령줄([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview))에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-137">You can create it from the [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span></span>

<span data-ttu-id="929ce-138">다음은 Azure CLI를 통해 계정을 만드는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-138">Following are the commands to create one through Azure CLI.</span></span>

<span data-ttu-id="929ce-139">Batch 계정을 만들 리소스가 이미 있는 경우 리소스 그룹을 만들고 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-139">Create a Resource Group, skip this step if you already have one where you want to create the Batch Account:</span></span>

`az group create -n "<resource-group-name>" -l "<location>"`

<span data-ttu-id="929ce-140">다음으로 Azure Batch 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-140">Next, create an Azure Batch account.</span></span>

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="929ce-141">각 Batch 계정에는 해당하는 액세스 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-141">Each Batch account has its corresponding access keys.</span></span> <span data-ttu-id="929ce-142">이러한 키는 Azure Batch 계정에 추가 리소스를 만드는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-142">These keys are needed to create further resources in Azure batch account.</span></span> <span data-ttu-id="929ce-143">프로덕션 환경의 경우 Azure Key Vault를 사용하여 이러한 키를 저장하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-143">A good practice for production environment is to use Azure Key Vault to store these keys.</span></span> <span data-ttu-id="929ce-144">그런 다음 응용 프로그램의 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-144">You can then create a Service principal for the application.</span></span> <span data-ttu-id="929ce-145">이 서비스 주체를 사용하여 응용 프로그램에서 Key Vault의 키에 액세스하는 OAuth 토큰을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-145">Using this service principal the application can create an OAuth token to access keys from the key vault.</span></span>

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="929ce-146">후속 단계에서 사용할 키를 복사하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-146">Copy and store the key to be used in the subsequent steps.</span></span>

### <a name="step-3-create-an-azure-batch-service-client"></a><span data-ttu-id="929ce-147">3단계: Azure Batch 서비스 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="929ce-147">Step 3: Create an Azure Batch service client</span></span>
<span data-ttu-id="929ce-148">다음 코드 조각은 azure-batch Node.js 모듈을 가져온 후 Batch 서비스 클라이언트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-148">Following code snippet first imports the azure-batch Node.js module and then creates a Batch Service client.</span></span> <span data-ttu-id="929ce-149">먼저 이전 단계에서 복사한 Batch 계정 키로 SharedKeyCredentials 개체를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-149">You need to first create a SharedKeyCredentials object with the Batch account key copied from the previous step.</span></span>

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

<span data-ttu-id="929ce-150">Azure Batch URI는 Azure Portal의 개요 탭에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-150">The Azure Batch URI can be found in the Overview tab of the Azure portal.</span></span> <span data-ttu-id="929ce-151">다음과 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-151">It is of the format:</span></span>

`https://accountname.location.batch.azure.com`

<span data-ttu-id="929ce-152">스크린샷을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="929ce-152">Refer to the screenshot:</span></span>

![Azure batch uri](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a><span data-ttu-id="929ce-154">4단계: Azure Batch 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="929ce-154">Step 4: Create an Azure Batch pool</span></span>
<span data-ttu-id="929ce-155">Azure Batch 풀은 여러 VM(Batch 노드라고도 함)으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-155">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span></span> <span data-ttu-id="929ce-156">Azure Batch 서비스는 이러한 노드에 작업을 배포하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-156">Azure Batch service deploys the tasks on these nodes and manages them.</span></span> <span data-ttu-id="929ce-157">풀에 대해 다음 구성 매개 변수를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-157">You can define the following configuration parameters for your pool.</span></span>

* <span data-ttu-id="929ce-158">가상 컴퓨터 이미지의 유형</span><span class="sxs-lookup"><span data-stu-id="929ce-158">Type of Virtual Machine image</span></span>
* <span data-ttu-id="929ce-159">가상 컴퓨터 노드의 크기</span><span class="sxs-lookup"><span data-stu-id="929ce-159">Size of Virtual Machine nodes</span></span>
* <span data-ttu-id="929ce-160">가상 컴퓨터 노드의 수</span><span class="sxs-lookup"><span data-stu-id="929ce-160">Number of Virtual Machine nodes</span></span>

> [!Tip]
> <span data-ttu-id="929ce-161">가상 컴퓨터 노드의 크기와 수는 병렬로 실행하려는 작업의 수와 작업 자체에 따라 크게 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-161">The size and number of Virtual Machine nodes largely depend on the number of tasks you want to run in parallel and also the task itself.</span></span> <span data-ttu-id="929ce-162">테스트를 통해 이상적인 수와 크기를 결정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-162">We recommend testing to determine the ideal number and size.</span></span>
>
>

<span data-ttu-id="929ce-163">다음은 구성 매개 변수 개체를 만드는 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-163">The following code snippet creates the configuration parameter objects.</span></span>

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating the VM configuration object with the SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting the VM size to Standard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in the pool to 4
var numVMs = 4
```

> [!Tip]
> <span data-ttu-id="929ce-164">Azure Batch 및 SKU ID에 사용할 수 있는 Linux VM 이미지 목록은 [가상 컴퓨터 이미지 목록](batch-linux-nodes.md#list-of-virtual-machine-images)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="929ce-164">For the list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span>
>
>

<span data-ttu-id="929ce-165">풀 구성이 정의되면 Azure Batch 풀을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-165">Once the pool configuration is defined, you can create the Azure Batch pool.</span></span> <span data-ttu-id="929ce-166">Batch 풀 명령은 Azure 가상 컴퓨터 노드를 만들고, 실행할 작업을 수신할 수 있도록 노드를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-166">The Batch pool command creates Azure Virtual Machine nodes and prepares them to be ready to receive tasks to execute.</span></span> <span data-ttu-id="929ce-167">각 풀에는 후속 단계에서 참조할 고유 ID가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-167">Each pool should have a unique ID for reference in subsequent steps.</span></span>

<span data-ttu-id="929ce-168">다음은 Azure Batch 풀을 만드는 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-168">The following code snippet creates an Azure Batch pool.</span></span>

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating the Pool for the specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

<span data-ttu-id="929ce-169">생성된 풀의 상태를 확인하고, 해당 풀에 작업을 제출하여 계속 진행하기 전에 상태를 "활성"으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-169">You can check the status of the pool created and ensure that the state is in "active" before going ahead with submission of a Job to that pool.</span></span>

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

<span data-ttu-id="929ce-170">다음은 pool.get 함수에서 반환하는 샘플 결과 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-170">Following is a sample result object returned by the pool.get function.</span></span>

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


### <a name="step-4-submit-an-azure-batch-job"></a><span data-ttu-id="929ce-171">4단계: Azure Batch 작업 제출</span><span class="sxs-lookup"><span data-stu-id="929ce-171">Step 4: Submit an Azure Batch job</span></span>
<span data-ttu-id="929ce-172">Azure Batch 작업은 유사한 작업의 논리적 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-172">An Azure Batch job is a logical group of similar tasks.</span></span> <span data-ttu-id="929ce-173">이 시나리오에서는 "csv를 JSON으로 처리"입니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-173">In our scenario, it is "Process csv to JSON."</span></span> <span data-ttu-id="929ce-174">여기의 각 작업은 각 Azure Storage 컨테이너에 있는 csv 파일을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-174">Each task here could be processing csv files present in each Azure Storage container.</span></span>

<span data-ttu-id="929ce-175">이러한 작업은 Azure Batch 서비스를 통해 병렬로 실행되어 여러 노드에 배포되고 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-175">These tasks would run in parallel and deployed across multiple nodes, orchestrated by the Azure Batch service.</span></span>

> [!Tip]
> <span data-ttu-id="929ce-176">[maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) 속성을 사용하여 단일 노드에서 동시에 실행할 수 있는 최대 작업 수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-176">You can use the [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property to specify maximum number of tasks that can run concurrently on a single node.</span></span>
>
>

#### <a name="preparation-task"></a><span data-ttu-id="929ce-177">준비 작업</span><span class="sxs-lookup"><span data-stu-id="929ce-177">Preparation task</span></span>

<span data-ttu-id="929ce-178">생성된 VM 노드는 빈 Ubuntu 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-178">The VM nodes created are blank Ubuntu nodes.</span></span> <span data-ttu-id="929ce-179">필수 구성 요소로 프로그램 집합을 설치해야 하는 경우가 자주 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-179">Often, you need to install a set of programs as prerequisites.</span></span>
<span data-ttu-id="929ce-180">일반적으로 Linux 노드의 경우 실제 작업이 실행되기 전에 필수 구성 요소를 설치하는 셸 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-180">Typically, for Linux nodes you can have a shell script that installs the prerequisites before the actual tasks run.</span></span> <span data-ttu-id="929ce-181">그러나 프로그래밍 방식의 실행 파일일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-181">However it could be any programmable executable.</span></span>
<span data-ttu-id="929ce-182">이 예제의 [셸 스크립트](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh)는 Python-pip 및 Python용 Azure Storage SDK를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-182">The [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and the Azure Storage SDK for Python.</span></span>

<span data-ttu-id="929ce-183">Azure Storage 계정에 스크립트를 업로드하고 해당 스크립트에 액세스하는 SAS URI를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-183">You can upload the script on an Azure Storage Account and generate a SAS URI to access the script.</span></span> <span data-ttu-id="929ce-184">Azure Storage Node.js SDK를 사용하여 이 프로세스를 자동화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-184">This process can also be automated using the Azure Storage Node.js SDK.</span></span>

> [!Tip]
> <span data-ttu-id="929ce-185">작업에 대한 준비 작업은 특정 작업을 실행해야 하는 VM 노드에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-185">A preparation task for a job runs only on the VM nodes where the specific task needs to run.</span></span> <span data-ttu-id="929ce-186">노드에서 실행되는 태스크와 관계없이 모든 노드에 필수 구성 요소를 설치하도록 하려면 풀을 추가하는 동안 [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) 속성을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-186">If you want prerequisites to be installed on all nodes irrespective of the tasks that run on it, you can use the [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span></span> <span data-ttu-id="929ce-187">다음 준비 작업 정의를 참조에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-187">You can use the following preparation task definition for reference.</span></span>
>
>

<span data-ttu-id="929ce-188">준비 작업은 Azure Batch 작업이 제출되는 동안 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-188">A preparation task is specified during the submission of Azure Batch job.</span></span> <span data-ttu-id="929ce-189">다음은 준비 작업 구성 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-189">Following are the preparation task configuration parameters:</span></span>

* <span data-ttu-id="929ce-190">**ID**: 준비 작업의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="929ce-190">**ID**: A unique identifier for the preparation task</span></span>
* <span data-ttu-id="929ce-191">**commandLine**: 작업 실행 파일을 실행하는 명령줄</span><span class="sxs-lookup"><span data-stu-id="929ce-191">**commandLine**: Command line to execute the task executable</span></span>
* <span data-ttu-id="929ce-192">**resourceFiles**: 이 작업을 실행하려면 다운로드해야 하는 파일의 세부 정보를 제공하는 개체 배열.</span><span class="sxs-lookup"><span data-stu-id="929ce-192">**resourceFiles**: Array of objects that provide details of files needed to be downloaded for this task to run.</span></span>  <span data-ttu-id="929ce-193">다음은 해당 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-193">Following are its options</span></span>
    - <span data-ttu-id="929ce-194">blobSource: 파일의 SAS URI</span><span class="sxs-lookup"><span data-stu-id="929ce-194">blobSource: The SAS URI of the file</span></span>
    - <span data-ttu-id="929ce-195">filePath: 파일을 다운로드하여 저장할 로컬 경로</span><span class="sxs-lookup"><span data-stu-id="929ce-195">filePath: Local path to download and save the file</span></span>
    - <span data-ttu-id="929ce-196">fileMode: Linux 노드에만 적용되는 fileMode는 8진수 형식이며 기본값은 0770</span><span class="sxs-lookup"><span data-stu-id="929ce-196">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span></span>
* <span data-ttu-id="929ce-197">**waitForSuccess**: true로 설정하면 준비 작업이 실패할 경우 작업이 실행되지 않음</span><span class="sxs-lookup"><span data-stu-id="929ce-197">**waitForSuccess**: If set to true, the task does not run on preparation task failures</span></span>
* <span data-ttu-id="929ce-198">**runElevated**: 작업을 실행하려면 상승된 권한이 필요한 경우 true로 설정.</span><span class="sxs-lookup"><span data-stu-id="929ce-198">**runElevated**: Set it to true if elevated privileges are needed to run the task.</span></span>

<span data-ttu-id="929ce-199">다음 코드 조각은 준비 작업 스크립트 구성 샘플을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-199">Following code snippet shows the preparation task script configuration sample:</span></span>

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

<span data-ttu-id="929ce-200">작업을 실행하기 위해 설치해야 할 필수 구성 요소가 없는 경우 준비 작업을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-200">If there are no prerequisites to be installed for your tasks to run, you can skip the preparation tasks.</span></span> <span data-ttu-id="929ce-201">다음 코드는 표시 이름이 "csv 파일 처리"인 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-201">Following code creates a job with display name "process csv files."</span></span>

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job to the pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a><span data-ttu-id="929ce-202">5단계: 작업에 대한 Azure Batch 작업 제출</span><span class="sxs-lookup"><span data-stu-id="929ce-202">Step 5: Submit Azure Batch tasks for a job</span></span>

<span data-ttu-id="929ce-203">csv 처리 작업을 만들었으니, 해당 작업에 대한 작업을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-203">Now that our process csv job is created, let us create tasks for that job.</span></span> <span data-ttu-id="929ce-204">컨테이너가 4개 있다고 가정하고, 각 컨테이너에 하나씩 총 4개의 작업을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-204">Assuming we have four containers, we have to create four tasks, one for each container.</span></span>

<span data-ttu-id="929ce-205">[Python 스크립트](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py)를 살펴보면, 두 개의 매개 변수가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-205">If we look at the [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span></span>

* <span data-ttu-id="929ce-206">컨테이너 이름: 파일을 다운로드할 Storage 컨테이너</span><span class="sxs-lookup"><span data-stu-id="929ce-206">container name: The Storage container to download files from</span></span>
* <span data-ttu-id="929ce-207">패턴: 파일 이름 패턴의 선택적 매개 변수</span><span class="sxs-lookup"><span data-stu-id="929ce-207">pattern: An optional parameter of file name pattern</span></span>

<span data-ttu-id="929ce-208">"con1", "con2", "con3", "con4" 총 4개의 컨테이너가 있다고 가정할 때, 다음 코드는 앞에서 만든 Azure 일괄 처리 작업 "csv 처리"에 작업을 제출하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-208">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks to the Azure batch job "process csv" we created earlier.</span></span>

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

<span data-ttu-id="929ce-209">이 코드는 풀에 여러 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-209">The code adds multiple tasks to the pool.</span></span> <span data-ttu-id="929ce-210">각 작업은 앞에서 만든 VM의 풀에 있는 노드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-210">And each of the tasks is executed on a node in the pool of VMs created.</span></span> <span data-ttu-id="929ce-211">작업 수가 풀의 VM 수 또는 maxTasksPerNode 속성을 초과할 경우 노드를 사용할 수 있게 될 때까지 작업이 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-211">If the number of tasks exceeds the number of VMs in a pool or the maxTasksPerNode property, the tasks wait until a node is made available.</span></span> <span data-ttu-id="929ce-212">이 오케스트레이션은 Azure Batch에서 자동으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-212">This orchestration is handled by Azure Batch automatically.</span></span>

<span data-ttu-id="929ce-213">포털에 가면 구체적인 작업 상태 보기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-213">The portal has detailed views on the tasks and job statuses.</span></span> <span data-ttu-id="929ce-214">Azure Node SDK에서 목록을 사용하여 함수를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-214">You can also use the list and get functions in the Azure Node SDK.</span></span> <span data-ttu-id="929ce-215">자세한 내용은 설명서 [링크](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html)에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-215">Details are provided in the documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="929ce-216">다음 단계</span><span class="sxs-lookup"><span data-stu-id="929ce-216">Next steps</span></span>

- <span data-ttu-id="929ce-217">이 서비스를 처음 사용하는 경우 [Azure Batch 기능 개요](batch-api-basics.md) 문서를 검토하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="929ce-217">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
- <span data-ttu-id="929ce-218">Batch API에 대한 내용은 [Batch Node.js 참조](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/)를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="929ce-218">See the [Batch Node.js reference](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) to explore the Batch API.</span></span>

