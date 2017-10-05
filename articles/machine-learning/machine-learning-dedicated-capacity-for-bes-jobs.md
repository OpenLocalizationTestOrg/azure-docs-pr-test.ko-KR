---
title: "Machine Learning 배치 실행 서비스 작업에 대한 전용 용량 | Microsoft Docs"
description: "Machine Learning 작업에 대한 Azure 배치 서비스 개요입니다."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3879eb3d0c6fa9d74fff01b07f5c07d3991dfbbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="a8649-103">Machine Learning 작업에 대한 Azure 배치 서비스</span><span class="sxs-lookup"><span data-stu-id="a8649-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="a8649-104">Machine Learning Batch 풀 처리는 Azure Machine Learning Batch 실행 서비스의 고객 관리 규모를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-104">Machine Learning Batch Pool processing provides customer-managed scale for the Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="a8649-105">Machine Learning에 대한 클래식 Batch 처리는 제출할 수 있는 동시 작업 수를 제한하는 다중 테넌트 환경에서 수행되며, 작업은 선입 선출 기준으로 큐에 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits the number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="a8649-106">이 불확실성은 작업이 실행되는 시기를 예측할 수 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="a8649-107">Batch 풀 처리를 사용하면 배치 작업을 제출할 수 있는 풀을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-107">Batch Pool processing allows you to create pools on which you can submit batch jobs.</span></span> <span data-ttu-id="a8649-108">풀의 크기와 작업이 제출되는 풀을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-108">You control the size of the pool, and to which pool the job is submitted.</span></span> <span data-ttu-id="a8649-109">BES 작업은 예측 가능한 처리 성능과 제출한 처리 부하에 해당하는 리소스 풀을 만드는 기능을 제공하는 자체 처리 공간에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-109">Your BES job runs in its own processing space providing predictable processing performance and the ability to create resource pools that correspond to the processing load that you submit.</span></span>

## <a name="how-to-use-batch-pool-processing"></a><span data-ttu-id="a8649-110">배치 풀 처리를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="a8649-110">How to use Batch Pool processing</span></span>

<span data-ttu-id="a8649-111">Batch 풀 처리의 구성은 현재 Azure Portal을 통해 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-111">Configuration of Batch Pool Processing is not currently available through the Azure portal.</span></span> <span data-ttu-id="a8649-112">Batch 풀 처리를 사용하려면:</span><span class="sxs-lookup"><span data-stu-id="a8649-112">To use Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="a8649-113">Batch 풀 계정을 만들고 풀 서비스 URL 및 권한 부여 키를 가져오기 위해 CSS 호출</span><span class="sxs-lookup"><span data-stu-id="a8649-113">Call CSS to create a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="a8649-114">새 Resource Manager 기반 웹 서비스 및 청구 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="a8649-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="a8649-115">계정을 만들려면 Microsoft 고객 서비스 및 지원 센터(CSS)에 전화하여 구독 ID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-115">To create your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="a8649-116">CSS에서는 사용자와 협의하여 시나리오에 적합한 용량을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-116">CSS will work with you to determine the appropriate capacity for your scenario.</span></span> <span data-ttu-id="a8649-117">그런 다음 CSS에서 만들 수 있는 최대 풀 수와 각 풀에 배치할 수 있는 VM(가상 컴퓨터)의 최대 수를 사용하여 계정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-117">CSS then configures your account with the maximum number of pools you can create and the maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="a8649-118">계정이 구성되면 풀 서비스 URL과 인증 키가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="a8649-119">계정을 만든 후에 풀 서비스 URL과 인증 키를 사용하여 배치 풀에 대한 풀 관리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-119">After your account is created, you use the Pool Service URL and authorization key to perform pool management operations on your Batch Pool.</span></span>

![배치 풀 서비스 아키텍처](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="a8649-121">CSS에서 제공한 풀 서비스 URL에서 풀 만들기 작업을 호출하여 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-121">You create pools by calling the Create Pool operation on the pool service URL that CSS provided to you.</span></span> <span data-ttu-id="a8649-122">풀을 만들 때 새 Resource Manager 기반의 Machine Learning 웹 서비스의 swagger.json에 VM 수와 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-122">When you create a pool, specify the number of VMs and the URL of the swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="a8649-123">이 웹 서비스는 청구 연결을 설정하는 데 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-123">This web service is provided to establish the billing association.</span></span> <span data-ttu-id="a8649-124">배치 풀 서비스는 swagger.json을 사용하여 풀과 청구 계획을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-124">The Batch Pool service uses the swagger.json to associate the pool with a billing plan.</span></span> <span data-ttu-id="a8649-125">풀에서 선택한 BES 웹 서비스(새 Resource Manager 기반 서비스 및 클래식 서비스)는 모두 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-125">You can run any BES web service, both New Resource Manager based and classic, you choose on the pool.</span></span>

<span data-ttu-id="a8649-126">새 Resource Manager 기반 웹 서비스를 사용할 수 있지만, 작업에 대한 요금 청구가 해당 서비스와 연결된 청구 계획과 대조하여 부과된다는 점에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="a8649-126">You can use any New Resource Manager based web service, but be aware that the billing for the jobs are charged against the billing plan associated with that service.</span></span> <span data-ttu-id="a8649-127">특히 배치 풀 작업을 실행하기 위한 웹 서비스와 새로운 청구 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-127">You may want to create a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="a8649-128">웹 서비스 만들기에 대한 자세한 내용은 [Azure Machine Learning 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8649-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="a8649-129">풀을 생성하면 웹 서비스의 배치 요청 URL을 사용하여 BES 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-129">Once you have created a pool, you submit the BES job using the Batch Requests URL for the web service.</span></span> <span data-ttu-id="a8649-130">풀 또는 클래식 일괄 처리에 제출하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-130">You can choose to submit it to a pool or to classic batch processing.</span></span> <span data-ttu-id="a8649-131">배치 풀 처리에 작업을 제출하려면 작업 제출 요청 본문에 다음 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-131">To submit a job to Batch Pool processing, you add the following parameter to the job submission request body:</span></span>

<span data-ttu-id="a8649-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span><span class="sxs-lookup"><span data-stu-id="a8649-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="a8649-133">매개 변수를 추가하지 않으면 작업이 클래식 일괄 처리 환경에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-133">If you do not add the parameter, the job is run in the classic batch process environment.</span></span> <span data-ttu-id="a8649-134">풀에 사용 가능한 리소스가 있는 경우 작업이 즉시 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-134">If the pool has available resources, the job starts running immediately.</span></span> <span data-ttu-id="a8649-135">풀에 사용 가능한 리소스가 없는 경우 작업은 리소스를 사용할 수 있을 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-135">If the pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="a8649-136">정기적으로 풀 용량에 도달하고 용량을 늘려야 하는 경우 CSS에 전화하고 담당자와 협력하여 할당량을 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-136">If you find that you regularly reach the capacity of your pools, and you need increased capacity, you can call CSS and work with a representative to increase your quotas.</span></span>

<span data-ttu-id="a8649-137">요청 예제:</span><span class="sxs-lookup"><span data-stu-id="a8649-137">Example Request:</span></span>

<span data-ttu-id="a8649-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span><span class="sxs-lookup"><span data-stu-id="a8649-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="a8649-139">배치 풀 처리 사용 시 고려 사항</span><span class="sxs-lookup"><span data-stu-id="a8649-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="a8649-140">배치 풀 처리는 항상 청구 가능한 서비스이며, 이를 Resource Manager 기반 청구 계획과 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-140">Batch Pool Processing is an always-on billable service and that requires you to associate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="a8649-141">시간 풀에서 실행되는 작업 수에 관계 없이 해당 풀이 실행되는 계산 시간에 대해서만 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-141">You are only billed for the number of compute hours the pool is running; regardless of the number of jobs run during that time pool.</span></span> <span data-ttu-id="a8649-142">풀을 만드는 경우 풀에서 실행되는 일괄 처리 작업이 없더라도 해당 풀을 삭제할 때까지 풀에 있는 각 가상 컴퓨터의 계산 시간에 대해 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-142">If you create a pool, you are billed for the compute hours of each virtual machine in the pool until the pool is deleted, even if no batch jobs are running in the pool.</span></span> <span data-ttu-id="a8649-143">가상 컴퓨터에 대한 청구는 프로비전을 완료하면 시작되고, 해당 프로비전을 삭제하면 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-143">Billing for the virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="a8649-144">[Machine Learning 가격](https://azure.microsoft.com/pricing/details/machine-learning/) 페이지에 있는 계획 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-144">You can use any of the plans found on the [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="a8649-145">청구 예제:</span><span class="sxs-lookup"><span data-stu-id="a8649-145">Billing example:</span></span>

<span data-ttu-id="a8649-146">2개의 가상 컴퓨터로 배치 풀을 만들고 24시간 후에 삭제하는 경우 해당 기간 동안 실행된 작업 수에 관계 없이 48 계산 시간에 대한 청구 계획이 계상됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="a8649-147">4개의 가상 컴퓨터로 배치 풀을 만들고 12시간 후에 삭제하는 경우에도 48 계산 시간에 대한 청구 계획이 계상됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="a8649-148">작업 상태를 폴링하여 작업 완료 시기를 결정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-148">We recommend that you poll the job status to determine when jobs complete.</span></span> <span data-ttu-id="a8649-149">모든 작업의 실행을 완료하면 풀 크기 조정 작업을 호출하여 풀의 가상 컴퓨터 수를 0으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-149">When all your jobs have finished running, call the Resize Pool operation to set the number of virtual machines in the pool to zero.</span></span> <span data-ttu-id="a8649-150">예를 들어 풀 리소스가 부족하고 다른 청구 계획에 대해 청구하도록 새 풀을 만들어야 하는 경우 모든 작업의 실행을 완료하는 대신 해당 풀을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-150">If you are short on pool resources and you need to create a new pool, for example to bill against a different billing plan, you can delete the pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="a8649-151">**배치 풀 처리를 사용하는 경우**</span><span class="sxs-lookup"><span data-stu-id="a8649-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="a8649-152">**클래식 일괄 처리를 사용하는 경우**</span><span class="sxs-lookup"><span data-stu-id="a8649-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="a8649-153">많은 수의 작업을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-153">You need to run a large number of jobs</span></span><br><span data-ttu-id="a8649-154">또는</span><span class="sxs-lookup"><span data-stu-id="a8649-154">Or</span></span><br/><span data-ttu-id="a8649-155">자신의 작업이 즉시 실행된다는 것을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-155">You need to know that your jobs will run immediately</span></span><br/><span data-ttu-id="a8649-156">또는</span><span class="sxs-lookup"><span data-stu-id="a8649-156">Or</span></span><br/><span data-ttu-id="a8649-157">처리량을 보장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-157">You need guaranteed throughput.</span></span> <span data-ttu-id="a8649-158">예를 들어 지정된 시간 프레임 내에서 여러 작업을 실행해야 하며, 요구 사항에 맞게 컴퓨팅 리소스를 확장하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-158">For example, you need to run a number of jobs in a given time frame, and want to scale out your compute resources to meet your needs.</span></span>    | <span data-ttu-id="a8649-159">몇 가지 작업만 실행하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-159">You are running just a few jobs</span></span><br/><span data-ttu-id="a8649-160">and</span><span class="sxs-lookup"><span data-stu-id="a8649-160">And</span></span><br/> <span data-ttu-id="a8649-161">작업을 즉시 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8649-161">You don’t need the jobs to run immediately</span></span> |
