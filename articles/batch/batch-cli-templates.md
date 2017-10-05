---
title: "코드를 작성하지 않고 종단 간 Azure Batch 작업 실행(미리 보기) | Microsoft Docs"
description: "Azure CLI에 템플릿 파일을 만들어서 Batch 풀, 작업 및 태스크를 만듭니다."
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: 6b91466da46d1f4ca9f25bf1718be783603efc58
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="ae4de-103">Azure Batch CLI 템플릿 및 파일 전송 사용(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="ae4de-103">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="ae4de-104">Azure CLI를 사용하여 코드를 작성하지 않고 Batch 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-104">Using the Azure CLI it is possible to run Batch jobs without writing code.</span></span>

<span data-ttu-id="ae4de-105">템플릿 파일을 만들고 Batch 풀, 작업, 태스크를 만들 수 있는 Azure CLI에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-105">Template files can be created and used with the Azure CLI that allow Batch pools, jobs, and tasks to be created.</span></span> <span data-ttu-id="ae4de-106">작업 입력 파일은 다운로드한 Batch 계정 및 작업 출력 파일과 연결된 저장소 계정에 쉽게 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-106">Job input files can be easily uploaded to the storage account associated with the Batch account and job output files downloaded.</span></span>

## <a name="overview"></a><span data-ttu-id="ae4de-107">개요</span><span class="sxs-lookup"><span data-stu-id="ae4de-107">Overview</span></span>

<span data-ttu-id="ae4de-108">Azure CLI로 확장하면 개발자가 아닌 사용자가 종단 간 Batch를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-108">An extension to the Azure CLI enables Batch to be used end-to-end by users who are not developers.</span></span> <span data-ttu-id="ae4de-109">풀을 만들고, 입력 데이터를 업로드하고, 작업 및 관련된 태스크를 만들고, 결과 출력 데이터를 다운로드할 수 있습니다. 이를 위해 코드가 필요하지 않고 CLI를 직접 사용하거나 스크립트에 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-109">A pool can be created, input data uploaded, jobs and associated tasks created, and the resulting output data downloaded – no code required, the CLI being used directly or being integrated into scripts.</span></span>

<span data-ttu-id="ae4de-110">Batch 템플릿은 [Azure CLI의 기존 Batch 지원](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation)에 기반하여 빌드됩니다. 이를 통해 JSON 파일이 풀, 작업, 태스크 및 기타 항목을 생성하는 속성 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-110">Batch templates build on the [existing Batch support in the Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) that allows JSON files to specify property values for the creation of pools, jobs, tasks, and other items.</span></span> <span data-ttu-id="ae4de-111">Batch 템플릿에서는 JSON 파일에 가능한 기능을 넘어 다음과 같은 기능이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-111">With Batch templates, the following capabilities are added over what is possible with the JSON files:</span></span>

-   <span data-ttu-id="ae4de-112">매개 변수를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-112">Parameters can be defined.</span></span> <span data-ttu-id="ae4de-113">템플릿을 사용하는 경우 템플릿 본문에 지정된 다른 항목 속성 값을 사용하여 해당 항목을 만들도록 매개 변수 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-113">When the template is used, only the parameter values are specified to create the item, with other item property values being specified in the template body.</span></span> <span data-ttu-id="ae4de-114">Batch 및 Batch에서 실행하는 응용 프로그램을 이해하는 사용자는 템플릿을 만들고 풀, 작업 및 태스크 속성 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-114">A user who understands Batch and the applications to be run by Batch can create templates, specifying pool, job, and task property values.</span></span> <span data-ttu-id="ae4de-115">Batch 및/또는 응용 프로그램에 덜 익숙한 사용자는 정의된 매개 변수에 대한 값을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-115">A user less familiar with Batch and/or the applications only needs to specify the values for the defined parameters.</span></span>

-   <span data-ttu-id="ae4de-116">작업 태스크 팩터리는 작업과 연관된 하나 이상의 태스크를 만들고, 많은 작업 정의를 만들 필요없이 작업 제출 크게 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-116">Job task factories create one or more tasks associated with a job, avoiding the need for many task definitions to be created and significantly simplifying job submission.</span></span>


<span data-ttu-id="ae4de-117">입력 데이터 파일을 작업에 제공해야 하며 출력 데이터 파일이 종종 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-117">Input data files need to be supplied for jobs and output data files are often produced.</span></span> <span data-ttu-id="ae4de-118">저장소 계정은 기본적으로 각 Batch 계정과 연결되므로 파일은 코딩 및 저장소 자격 증명 없이 CLI를 사용하여 이 저장소 계정 간에 쉽게 전송될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-118">A storage account is associated, by default, with each Batch account and files can be easily transferred to and from this storage account using the CLI, with no coding and no storage credentials required.</span></span>

<span data-ttu-id="ae4de-119">예를 들어 [ffmpeg](http://ffmpeg.org/)는 오디오 및 비디오 파일을 처리하는 인기 있는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-119">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span></span> <span data-ttu-id="ae4de-120">Azure Batch CLI를 사용하여 원본 비디오 파일을 다른 해상도로 코드 변환하기 위해 ffmpeg를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-120">The Azure Batch CLI can be used to invoke ffmpeg to transcode source video files to different resolutions.</span></span>

-   <span data-ttu-id="ae4de-121">풀 템플릿을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-121">A pool template is created.</span></span> <span data-ttu-id="ae4de-122">템플릿을 만드는 사용자는 ffmpeg 응용 프로그램 및 요구 사항을 호출하는 방법을 알고 있습니다. 적절한 OS, VM 크기, ffmpeg 설치 방법(예: 응용 프로그램 패키지에서 또는 패키지 관리자를 사용하여) 및 기타 풀 속성 값을 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-122">The user creating the template knows how to call the ffmpeg application and its requirements; they specify the appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span></span> <span data-ttu-id="ae4de-123">매개 변수를 만들었으므로 템플릿이 사용될 경우 풀 ID와 VM의 수만을 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-123">Parameters are created so when the template is used, only the pool id and number of VMs need to be specified.</span></span>

-   <span data-ttu-id="ae4de-124">작업 템플릿을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-124">A job template is created.</span></span> <span data-ttu-id="ae4de-125">템플릿을 만드는 사용자는 ffmpeg를 호출하여 소스 비디오를 다른 해상도로 코드 변환하는 방법을 알고, 태스크 명령줄을 지정합니다. 또한 입력 파일당 필요한 태스크가 담긴 소스 비디오 파일을 포함하는 폴더가 있다는 것을 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-125">The user creating the template knows how ffmpeg needs to be invoked to transcode source video to a different resolution and specifies the task command line; they also know that there is a folder containing the source video files, with a task required per input file.</span></span>

-   <span data-ttu-id="ae4de-126">코드를 변환할 비디오 파일 집합이 있는 최종 사용자가 먼저 풀 템플릿을 사용하여 풀을 만들고 풀 ID와 필요한 VM 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-126">An end user with a set of video files to transcode first creates a pool using the pool template, specifying only the pool id and number of VMs required.</span></span> <span data-ttu-id="ae4de-127">코드 변환에 원본 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-127">They can then upload the source files to transcode.</span></span> <span data-ttu-id="ae4de-128">작업 템플릿을 사용하여 작업을 제출하고 풀 ID 및 업로드된 원본 파일의 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-128">A job can then be submitted using the job template, specifying only the pool id and location of the source files uploaded.</span></span> <span data-ttu-id="ae4de-129">입력 파일당 하나의 태스크가 있는 Batch 작업이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-129">The Batch job is created, with one task per input file being generated.</span></span> <span data-ttu-id="ae4de-130">마지막으로 코드 변환 출력 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-130">Finally, the transcoded output files can be download.</span></span>

## <a name="installation"></a><span data-ttu-id="ae4de-131">설치</span><span class="sxs-lookup"><span data-stu-id="ae4de-131">Installation</span></span>

<span data-ttu-id="ae4de-132">템플릿 및 파일 전송 기능은 확장을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-132">The template and file transfer capabilities require an extension to be installed.</span></span>

<span data-ttu-id="ae4de-133">Azure CLI를 설치하는 방법은 [Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae4de-133">For instructions on how to install the Azure CLI see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="ae4de-134">Azure CLI를 설치하면 Batch 확장은 다음 CLI 명령을 사용하여 설치될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-134">Once the Azure CLI has been installed, the Batch extension can be installed using the following CLI command:</span></span>

```azurecli
az component update --add batch-extensions --allow-third-party
```

<span data-ttu-id="ae4de-135">Batch 확장에 대한 자세한 내용은 [ Windows, Mac 및 Linux용 Microsoft Azure Batch CLI 확장](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae4de-135">For more information about the Batch extension, see [Microsoft Azure Batch CLI Extensions for Windows, Mac and Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span></span>

## <a name="templates"></a><span data-ttu-id="ae4de-136">템플릿</span><span class="sxs-lookup"><span data-stu-id="ae4de-136">Templates</span></span>

<span data-ttu-id="ae4de-137">Azure Batch CLI를 통해 속성 이름 및 값을 포함하는 JSON 파일을 지정하여 풀, 작업 및 태스크와 같은 항목을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-137">The Azure Batch CLI allows items such as pools, jobs, and tasks to be created by specifying a JSON file containing property names and values.</span></span> <span data-ttu-id="ae4de-138">예:</span><span class="sxs-lookup"><span data-stu-id="ae4de-138">For example:</span></span>

```azurecli
az batch pool create –-json-file AppPool.json
```

<span data-ttu-id="ae4de-139">Azure Batch 템플릿은 Azure Resource Manager 템플릿과 기능 및 구문 면에서 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-139">Azure Batch templates are similar to Azure Resource Manager templates, in functionality and syntax.</span></span> <span data-ttu-id="ae4de-140">항목 속성 이름 및 값을 포함하는 JSON 파일이지만 다음과 같은 주요 개념이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-140">They are JSON files that contain item property names and values, but add the following main concepts:</span></span>

-   <span data-ttu-id="ae4de-141">**매개 변수**</span><span class="sxs-lookup"><span data-stu-id="ae4de-141">**Parameters**</span></span>

    -   <span data-ttu-id="ae4de-142">템플릿이 사용될 때 제공해야 하는 매개 변수 값으로 속성 값을 본문 섹션에서 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-142">Allow property values to be specified in a body section, with only parameter values needing to be supplied when the template is used.</span></span> <span data-ttu-id="ae4de-143">예를 들어 풀에 대한 전체 정의를 본문에 배치하고 하나의 매개 변수만을 풀 ID에 정의할 수 있습니다. 따라서 풀을 만드는 데 풀 ID 문자열을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-143">For example, the complete definition for a pool could be placed in the body and only one parameter defined for pool id; only a pool id string therefore needs to be supplied to create a pool.</span></span>
        
    -   <span data-ttu-id="ae4de-144">Batch 및 Batch에서 실행할 응용 프로그램에 대한 지식이 있는 사용자가 템플릿 본문을 작성할 수 있습니다. 템플릿이 사용될 때 작성자 정의 매개 변수에 대한 값만을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-144">The template body can be authored by someone with knowledge of Batch and the applications to be run by Batch; only values for the author-defined parameters must be supplied when the template is used.</span></span> <span data-ttu-id="ae4de-145">따라서 깊이 있는 Batch 및/또는 응용 프로그램 지식이 없는 사용자는 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-145">A user without the in-depth Batch and/or application knowledge can therefore use the templates.</span></span>

-   <span data-ttu-id="ae4de-146">**변수**</span><span class="sxs-lookup"><span data-stu-id="ae4de-146">**Variables**</span></span>

    -   <span data-ttu-id="ae4de-147">간단하거나 복잡한 매개 변수 값을 한 곳에서 지정하거나 템플릿 본문에 있는 하나 이상의 위치에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-147">Allow simple or complex parameter values to be specified in one place and used in one or more places in the template body.</span></span> <span data-ttu-id="ae4de-148">변수는 템플릿의 크기를 단순화하고 줄일 뿐만 아니라 값이 변경될 수 있는 속성을 변경하도록 하나의 위치를 가지고 관리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-148">Variables can simplify and reduce the size of the template, as well as make it more maintainable by having one location to change properties whose value may change.</span></span>

-   <span data-ttu-id="ae4de-149">**더 높은 수준의 구문**</span><span class="sxs-lookup"><span data-stu-id="ae4de-149">**Higher-level constructs**</span></span>

    -   <span data-ttu-id="ae4de-150">일부 높은 수준의 구문은 아직 Batch API에서 사용할 수 없는 템플릿에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-150">Some higher-level constructs are available in the template that are not yet available in the Batch APIs.</span></span> <span data-ttu-id="ae4de-151">예를 들어 일반 태스크 정의를 사용하여 작업에 여러 태스크를 만드는 작업 템플릿에서 태스크 팩터리를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-151">For example, a task factory can be defined in a job template that creates multiple tasks for the job using a common task definition.</span></span> <span data-ttu-id="ae4de-152">예를 들어 이러한 구문은 패키지 관리자를 통해 응용 프로그램을 설치하는 스크립트 파일을 만들 뿐만 아니라 태스크당 하나의 파일과 같이 여러 JSON 파일을 동적으로 만들도록 코딩할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-152">These constructs avoid the need to code to dynamically create multiple JSON files, such as one file per task, as well as create script files to install applications via a package manager, for example.</span></span>

    -   <span data-ttu-id="ae4de-153">어느 시점에서 해당되는 경우 이러한 구문은 Batch 서비스에 추가되고 Batch API, UI 등에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-153">At some point, where applicable, these constructs may be added to the Batch service and available in the Batch APIs, UIs, etc.</span></span>

### <a name="pool-templates"></a><span data-ttu-id="ae4de-154">풀 템플릿</span><span class="sxs-lookup"><span data-stu-id="ae4de-154">Pool templates</span></span>

<span data-ttu-id="ae4de-155">매개 변수 및 변수의 표준 템플릿 기능 외에도 다음과 같은 더 높은 수준의 구문이 풀 템플릿에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-155">In addition to the standard template capabilities of parameters and variables, the following higher-level constructs are supported by the pool template:</span></span>

-   <span data-ttu-id="ae4de-156">**패키지 참조**</span><span class="sxs-lookup"><span data-stu-id="ae4de-156">**Package references**</span></span>

    -   <span data-ttu-id="ae4de-157">필요에 따라 패키지 관리자를 사용하여 소프트웨어를 풀 노드에 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-157">Optionally allows software to be copied to pool nodes by using package managers.</span></span> <span data-ttu-id="ae4de-158">패키지 관리자 및 패키지 ID가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-158">The package manager and package id are specified.</span></span> <span data-ttu-id="ae4de-159">하나 이상의 패키지를 선언할 수 있게 되면 필요한 패키지를 가져오고, 스크립트를 설치하고, 각 풀 노드에서 스크립트를 실행하는 스크립트를 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-159">Being able to declare one or more packages avoids the need to create a script that gets the required packages, install the script, and run the script on each pool node.</span></span>

<span data-ttu-id="ae4de-160">ffmpeg를 설치한 Linux VM의 풀을 만들고 사용할 풀 ID 문자열 및 VM 수를 제공해야 하는 템플릿의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-160">The following is an example of a template that creates a pool of Linux VMs with ffmpeg installed and only requires a pool id string and the number of VMs to be supplied to use:</span></span>

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "The number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "The pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

<span data-ttu-id="ae4de-161">템플릿 파일의 이름이 _pool-ffmpeg.json_으로 지정되면 템플릿은 다음과 같이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-161">If the template file was named _pool-ffmpeg.json_, then the template would be invoked as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a><span data-ttu-id="ae4de-162">작업 템플릿</span><span class="sxs-lookup"><span data-stu-id="ae4de-162">Job templates</span></span>

<span data-ttu-id="ae4de-163">매개 변수 및 변수의 표준 템플릿 기능 외에도 다음과 같은 더 높은 수준의 구문이 작업 템플릿에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-163">In addition to the standard template capabilities of parameters and variables, the following higher-level constructs are supported by the job template:</span></span>

-   <span data-ttu-id="ae4de-164">**태스크 팩터리**</span><span class="sxs-lookup"><span data-stu-id="ae4de-164">**Task factory**</span></span>

    -   <span data-ttu-id="ae4de-165">하나의 태스크 정의에서 작업에 여러 태스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-165">Creates multiple tasks for a job from one task definition.</span></span> <span data-ttu-id="ae4de-166">파라메트릭 스윕, 파일당 태스크 및 태스크 컬렉션이라는 세 가지 형식의 태스크 팩터리가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-166">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span></span>

<span data-ttu-id="ae4de-167">소스 비디오 파일당 작업을 생성하여 두 개 중 더 낮은 해상도로 MP4 비디오 파일을 코드 변환하는 ffmpeg를 사용하는 작업을 만드는 템플릿의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-167">The following is an example of a template that creates a job that uses ffmpeg to transcode MP4 video files to one of two lower resolutions, with one task created per source video file:</span></span>

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "The name of Azure Batch pool which runs the job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "The name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

<span data-ttu-id="ae4de-168">템플릿 파일의 이름이 _job-ffmpeg.json_으로 지정되면 템플릿은 다음과 같이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-168">If the template file was named _job-ffmpeg.json_, then the template would be invoked as follows:</span></span>

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a><span data-ttu-id="ae4de-169">파일 그룹 및 파일 전송</span><span class="sxs-lookup"><span data-stu-id="ae4de-169">File groups and file transfer</span></span>

<span data-ttu-id="ae4de-170">대부분의 작업 및 태스크에는 입력 파일이 필요하고 결과로 출력 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-170">Most jobs and tasks require input files and produce output files.</span></span> <span data-ttu-id="ae4de-171">입력 파일 및 출력 파일은 일반적으로 클라이언트에서 노드로, 또는 노드에서 클라이언트로 전송되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-171">Both input files and output files typically need to be transferred, either from the client to the node, or from the node to the client.</span></span> <span data-ttu-id="ae4de-172">Azure Batch CLI 확장은 파일 전송을 추상화하고 각 Batch 계정에 기본적으로 만든 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-172">The Azure Batch CLI extension abstracts away file transfer and utilizes the storage account that is created by default for each Batch account.</span></span>

<span data-ttu-id="ae4de-173">파일 그룹은 Azure Storage 계정에서 생성된 컨테이너와 동등합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-173">A file group equates to a container that is created in the Azure storage account.</span></span> <span data-ttu-id="ae4de-174">파일 그룹에는 하위 폴더가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-174">The file group may have subfolders.</span></span>

<span data-ttu-id="ae4de-175">Batch CLI 확장은 파일을 클라이언트에서 지정된 파일 그룹으로 업로드하고 지정된 파일 그룹에서 클라이언트로 다운로드하는 명령을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-175">The Batch CLI extension provides commands for uploading files from client to a specified file group and downloading files from the specified file group to a client.</span></span>

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

<span data-ttu-id="ae4de-176">풀 및 작업 템플릿을 통해 파일 그룹에 저장된 파일을 풀 노드에 복사하도록 지정하거나 풀 노드에서 파일 그룹에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-176">Pool and job templates allow files stored in file groups to be specified for copy onto pool nodes or off pool nodes back to a file group.</span></span> <span data-ttu-id="ae4de-177">예를 들어 이전에 지정한 작업 템플릿에서 파일 그룹 "ffmpeg-input"은 코드 변환을 위해 노드로 복사하는 소스 비디오 파일의 위치인 태스크 팩터리에 대해 지정됩니다. 파일 그룹 "ffmpeg-output"은 각 태스크를 실행하는 노드에서 복사된 코드 변환된 출력 파일이 복사되는 위치로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-177">For example, in the job template specified previously, the file group “ffmpeg-input” is specified for the task factory as the location of the source video files copied down onto the node for transcoding; the file group “ffmpeg-output” is used as the location where the transcoded output files are copied to from the node running each task.</span></span>

## <a name="summary"></a><span data-ttu-id="ae4de-178">요약</span><span class="sxs-lookup"><span data-stu-id="ae4de-178">Summary</span></span>

<span data-ttu-id="ae4de-179">템플릿 및 파일 전송 지원은 현재 Azure CLI에만 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-179">Template and file transfer support have currently been added only to the Azure CLI.</span></span> <span data-ttu-id="ae4de-180">목표는 연구원, IT 사용자와 같이 Batch API를 사용하여 코드를 개발할 필요가 없는 사용자로 Batch를 사용할 수 있는 대상 그룹을 확장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-180">The goal is to expand the audience that can use Batch to users who do not need to develop code using the Batch APIs, such as researchers, IT users, and so on.</span></span> <span data-ttu-id="ae4de-181">Azure, Batch 및 Batch에서 실행하는 응용 프로그램에 대한 지식이 사용자는 코딩 없이 풀 및 작업 생성을 위해 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-181">Without coding, users with knowledge of Azure, Batch, and the applications to be run by Batch can create templates for pool and job creation.</span></span> <span data-ttu-id="ae4de-182">Batch 및 응용 프로그램에 대한 세부 정보가 없는 사용자는 템플릿 매개 변수를 사용하여 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-182">With template parameters, users without detailed knowledge of Batch and the applications can use the templates.</span></span>

<span data-ttu-id="ae4de-183">Azure CLI에 Batch 확장을 사용해 보고 이 문서의 주석이나 [Azure Batch 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch)을 통해 피드백이나 의견을 제공해주세요.</span><span class="sxs-lookup"><span data-stu-id="ae4de-183">Try out the Batch extension for the Azure CLI and provide us with any feedback or suggestions, either in the comments for this article or via the [Azure Batch forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae4de-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae4de-184">Next steps</span></span>

- <span data-ttu-id="ae4de-185">Batch 템플릿 블로그 게시물인 [Azure CLI를 사용하여 Azure Batch 작업 실행 - 코드가 필요하지 않음](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae4de-185">See the Batch templates blog post: [Running Azure Batch jobs using the Azure CLI – no code required](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span></span>
- <span data-ttu-id="ae4de-186">자세한 설치 및 사용 설명서, 샘플 및 소스 코드는 [Azure GitHub 리포지토리](https://github.com/Azure/azure-batch-cli-extensions)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae4de-186">Detailed installation and usage documentation, samples, and source code are available in the [Azure GitHub repository](https://github.com/Azure/azure-batch-cli-extensions).</span></span>
