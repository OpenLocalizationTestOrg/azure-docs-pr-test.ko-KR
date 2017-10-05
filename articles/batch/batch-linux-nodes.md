---
title: "가상 컴퓨터 계산 노드에서 Linux 실행 - Azure Batch | Microsoft Docs"
description: "Azure Batch의 Linux 가상 컴퓨터 풀에서 병렬 계산 워크로드를 처리하는 방법에 대해 알아봅니다."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9b2257917e2368478beb75957677de23d4157865
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a><span data-ttu-id="941ff-103">Batch 풀에서 Linux 계산 노드 프로비전</span><span class="sxs-lookup"><span data-stu-id="941ff-103">Provision Linux compute nodes in Batch pools</span></span>

<span data-ttu-id="941ff-104">Azure Batch를 사용하여 Linux 및 Windows 가상 컴퓨터에서 병렬 계산 워크로드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-104">You can use Azure Batch to run parallel compute workloads on both Linux and Windows virtual machines.</span></span> <span data-ttu-id="941ff-105">이 문서에서는 [Batch Python][py_batch_package] 및 [Batch .NET][api_net] 클라이언트 라이브러리를 모두 사용하여 Batch 서비스에서 Linux 계산 노드 풀을 만드는 방법에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-105">This article details how to create pools of Linux compute nodes in the Batch service by using both the [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span></span>

> [!NOTE]
> <span data-ttu-id="941ff-106">응용 프로그램 패키지는 2017년 7월 5일 이후에 만들어진 모든 Batch 풀에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-106">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="941ff-107">2016년 3월 10일에서 2017년 7월 5일 사이에 만들어진 Batch 풀에서는 Cloud Service 구성을 사용하여 풀을 만든 경우에만 이러한 패키지가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-107">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="941ff-108">2016년 3월 10일 이전에 만들어진 Batch 풀은 응용 프로그램 패키지를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-108">Batch pools created prior to 10 March 2016 do not support application packages.</span></span> <span data-ttu-id="941ff-109">응용 프로그램 패키지를 사용하여 Batch 노드에 응용 프로그램을 배포하는 방법에 대한 자세한 내용은 [Batch 응용 프로그램 패키지를 사용하여 계산 노드에 응용 프로그램 배포](batch-application-packages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="941ff-109">For more information about using application packages to deploy your applications to your Batch nodes, see [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>
>
>

## <a name="virtual-machine-configuration"></a><span data-ttu-id="941ff-110">가상 컴퓨터 구성</span><span class="sxs-lookup"><span data-stu-id="941ff-110">Virtual machine configuration</span></span>
<span data-ttu-id="941ff-111">Batch에서 계산 노드 풀을 만드는 경우 노드 크기와 운영 체제를 선택할 수 있는 두 가지 옵션인 Cloud Service 구성 및 가상 컴퓨터 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-111">When you create a pool of compute nodes in Batch, you have two options from which to select the node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span></span>

<span data-ttu-id="941ff-112">**Cloud Services 구성**은 Windows 계산 노드 *만*제공합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-112">**Cloud Services Configuration** provides Windows compute nodes *only*.</span></span> <span data-ttu-id="941ff-113">사용 가능한 계산 노드 크기는 [클라우드 서비스 크기](../cloud-services/cloud-services-sizes-specs.md)에 나열되고 사용 가능한 운영 체제는 [Azure 게스트 OS 릴리스 및 SDK 호환성 매트릭스](../cloud-services/cloud-services-guestos-update-matrix.md)에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-113">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in the [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="941ff-114">Azure Cloud Services 노드를 포함하는 풀을 만드는 경우 노드 크기 및 OS 제품군을 지정하며, 앞에서 언급한 문서에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-114">When you create a pool that contains Azure Cloud Services nodes, you specify the node size and the OS family, which are described in the previously mentioned articles.</span></span> <span data-ttu-id="941ff-115">Windows 계산 노드의 풀에는 Cloud Services가 가장 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-115">For pools of Windows compute nodes, Cloud Services is most commonly used.</span></span>

<span data-ttu-id="941ff-116">**가상 컴퓨터 구성** 은 계산 노드에 대한 Linux와 Windows 이미지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-116">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span></span> <span data-ttu-id="941ff-117">사용 가능한 계산 노드 크기는 [Azure에서 가상 컴퓨터에 대한 크기](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)(Linux) 및 [Azure에서 가상 컴퓨터에 대한 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)(Windows)에 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-117">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span></span> <span data-ttu-id="941ff-118">가상 컴퓨터 구성 노드를 포함하는 풀을 만들 때 노드 크기, 가상 컴퓨터 이미지 참조 및 노드에 설치할 Batch 노드 에이전트 SKU도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-118">When you create a pool that contains Virtual Machine Configuration nodes, you must specify the size of the nodes, the virtual machine image reference, and the Batch node agent SKU to be installed on the nodes.</span></span>

### <a name="virtual-machine-image-reference"></a><span data-ttu-id="941ff-119">가상 컴퓨터 이미지 참조</span><span class="sxs-lookup"><span data-stu-id="941ff-119">Virtual machine image reference</span></span>
<span data-ttu-id="941ff-120">Batch 서비스는 [가상 컴퓨터 확장 집합](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)을 사용하여 Linux 계산 노드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-120">The Batch service uses [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) to provide Linux compute nodes.</span></span> <span data-ttu-id="941ff-121">[Azure Marketplace][vm_marketplace]의 이미지를 지정하거나 준비한 사용자 지정 이미지를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-121">You can specify an image from the [Azure Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span> <span data-ttu-id="941ff-122">사용자 지정 이미지에 대한 자세한 내용은 [Batch를 사용하여 대규모 병렬 계산 솔루션 개발](batch-api-basics.md#pool)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="941ff-122">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

<span data-ttu-id="941ff-123">가상 컴퓨터 이미지 참조를 구성할 때 가상 컴퓨터 이미지의 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-123">When you configure a virtual machine image reference, you specify the properties of the virtual machine image.</span></span> <span data-ttu-id="941ff-124">가상 컴퓨터 이미지 참조를 만들 때 다음 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-124">The following properties are required when you create a virtual machine image reference:</span></span>

| <span data-ttu-id="941ff-125">**이미지 참조 속성**</span><span class="sxs-lookup"><span data-stu-id="941ff-125">**Image reference properties**</span></span> | <span data-ttu-id="941ff-126">**예제**</span><span class="sxs-lookup"><span data-stu-id="941ff-126">**Example**</span></span> |
| --- | --- |
| <span data-ttu-id="941ff-127">게시자</span><span class="sxs-lookup"><span data-stu-id="941ff-127">Publisher</span></span> |<span data-ttu-id="941ff-128">Canonical</span><span class="sxs-lookup"><span data-stu-id="941ff-128">Canonical</span></span> |
| <span data-ttu-id="941ff-129">제안</span><span class="sxs-lookup"><span data-stu-id="941ff-129">Offer</span></span> |<span data-ttu-id="941ff-130">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="941ff-130">UbuntuServer</span></span> |
| <span data-ttu-id="941ff-131">SKU</span><span class="sxs-lookup"><span data-stu-id="941ff-131">SKU</span></span> |<span data-ttu-id="941ff-132">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="941ff-132">14.04.4-LTS</span></span> |
| <span data-ttu-id="941ff-133">버전</span><span class="sxs-lookup"><span data-stu-id="941ff-133">Version</span></span> |<span data-ttu-id="941ff-134">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-134">latest</span></span> |

> [!TIP]
> <span data-ttu-id="941ff-135">이러한 속성 및 Marketplace 이미지를 나열하는 방법에 대한 자세한 내용은 [CLI 또는 PowerShell로 Azure의 Linux 가상 컴퓨터 이미지 이동 및 선택](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-135">You can learn more about these properties and how to list Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="941ff-136">일부 Marketplace 이미지가 현재 Batch와 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-136">Note that not all Marketplace images are currently compatible with Batch.</span></span> <span data-ttu-id="941ff-137">자세한 내용은 [노드 에이전트 SKU](#node-agent-sku)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="941ff-137">For more information, see [Node agent SKU](#node-agent-sku).</span></span>
>
>

### <a name="node-agent-sku"></a><span data-ttu-id="941ff-138">노드 에이전트 SKU</span><span class="sxs-lookup"><span data-stu-id="941ff-138">Node agent SKU</span></span>
<span data-ttu-id="941ff-139">Batch 노드 에이전트는 풀의 각 노드에서 실행되고 노드와 Batch 서비스 간의 명령 및 컨트롤 인터페이스를 제공하는 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-139">The Batch node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span></span> <span data-ttu-id="941ff-140">SKU라고 하는 노드 에이전트의 구현은 서로 다른 운영 체제에 대해 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-140">There are different implementations of the node agent, known as SKUs, for different operating systems.</span></span> <span data-ttu-id="941ff-141">기본적으로 가상 컴퓨터 구성을 만들 때 먼저 가상 컴퓨터 이미지 참조를 지정한 다음 이미지에 설치할 노드 에이전트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-141">Essentially, when you create a Virtual Machine Configuration, you first specify the virtual machine image reference, and then you specify the node agent to install on the image.</span></span> <span data-ttu-id="941ff-142">일반적으로 각 노드 에이전트 SKU는 여러 가상 컴퓨터 이미지와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-142">Typically, each node agent SKU is compatible with multiple virtual machine images.</span></span> <span data-ttu-id="941ff-143">다음은 노드 에이전트 SKU의 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-143">Here are a few examples of node agent SKUs:</span></span>

* <span data-ttu-id="941ff-144">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="941ff-144">batch.node.ubuntu 14.04</span></span>
* <span data-ttu-id="941ff-145">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="941ff-145">batch.node.centos 7</span></span>
* <span data-ttu-id="941ff-146">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="941ff-146">batch.node.windows amd64</span></span>

> [!IMPORTANT]
> <span data-ttu-id="941ff-147">Marketplace에서 사용 가능한 일부 가상 컴퓨터 이미지가 현재 사용 가능한 Batch 노드 에이전트와 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-147">Not all virtual machine images that are available in the Marketplace are compatible with the currently available Batch node agents.</span></span> <span data-ttu-id="941ff-148">Batch SDK를 사용하여 사용 가능한 노드 에이전트 SKU 및 호환되는 가상 컴퓨터 이미지를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-148">Use the Batch SDKs to list the available node agent SKUs and the virtual machine images with which they are compatible.</span></span> <span data-ttu-id="941ff-149">런타임에 유효한 이미지 목록을 검색하는 방법에 대한 자세한 내용 및 예제는 이 문서의 뒷부분에 있는 [가상 컴퓨터 이미지 목록](#list-of-virtual-machine-images)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="941ff-149">See the [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information and examples of how to retrieve a list of valid images at runtime.</span></span>
>
>

## <a name="create-a-linux-pool-batch-python"></a><span data-ttu-id="941ff-150">Linux 풀 만들기: Batch Python</span><span class="sxs-lookup"><span data-stu-id="941ff-150">Create a Linux pool: Batch Python</span></span>
<span data-ttu-id="941ff-151">다음 코드 조각은 [Python용 Microsoft Azure Batch 클라이언트 라이브러리][py_batch_package]를 사용하여 Ubuntu Server 계산 노드의 풀을 만드는 방법의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-151">The following code snippet shows an example of how to use the [Microsoft Azure Batch Client Library for Python][py_batch_package] to create a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="941ff-152">Batch Python 모듈에 대한 참조 설명서는 Read the Docs의 [azure.batch package][py_batch_docs]에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-152">Reference documentation for the Batch Python module can be found at [azure.batch package][py_batch_docs] on Read the Docs.</span></span>

<span data-ttu-id="941ff-153">이 코드 조각은 명시적으로 [ImageReference][py_imagereference]를 만들고 각 속성(게시자, 제품, SKU, 버전)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-153">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span></span> <span data-ttu-id="941ff-154">그러나 프로덕션 코드에서는 [list_node_agent_skus][py_list_skus]를 사용하여 런타임 시 사용 가능한 이미지 및 노드 에이전트 SKU 조합을 결정하고 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-154">In production code, however, we recommend that you use the [list_node_agent_skus][py_list_skus] method to determine and select from the available image and node agent SKU combinations at runtime.</span></span>

```python
# Import the required modules from the
# Azure Batch Client Library for Python
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify Batch account credentials
account = "<batch-account-name>"
key = "<batch-account-key>"
batch_url = "<batch-account-url>"

# Pool settings
pool_id = "LinuxNodesSamplePoolPython"
vm_size = "STANDARD_A1"
node_count = 1

# Initialize the Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create the unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure the start task for the pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies the Marketplace
# virtual machine image to install on the nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create the VirtualMachineConfiguration, specifying
# the VM image reference and the Batch node agent to
# be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign the virtual machine configuration to the pool
new_pool.virtual_machine_configuration = vmc

# Create pool in the Batch service
client.pool.add(new_pool)
```

<span data-ttu-id="941ff-155">이전에 언급한 대로 [ImageReference][py_imagereference]를 명시적으로 만드는 대신 현재 지원되는 노드 에이전트/Marketplace 이미지 조합에서 동적으로 선택하는 [list_node_agent_skus][py_list_skus] 메서드를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-155">As mentioned previously, we recommend that instead of creating the [ImageReference][py_imagereference] explicitly, you use the [list_node_agent_skus][py_list_skus] method to dynamically select from the currently supported node agent/Marketplace image combinations.</span></span> <span data-ttu-id="941ff-156">다음 Python 코드 조각에서는 이 메서드의 사용 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-156">The following Python snippet shows how to use this method.</span></span>

```python
# Get the list of node agents from the Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain the desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick the first image reference from the list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create the VirtualMachineConfiguration, specifying the VM image
# reference and the Batch node agent to be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a><span data-ttu-id="941ff-157">Linux 풀 만들기: Batch .NET</span><span class="sxs-lookup"><span data-stu-id="941ff-157">Create a Linux pool: Batch .NET</span></span>
<span data-ttu-id="941ff-158">다음 코드 조각은 [Batch .NET][nuget_batch_net] 클라이언트 라이브러리를 사용하여 Ubuntu Server 계산 노드의 풀을 만드는 방법의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-158">The following code snippet shows an example of how to use the [Batch .NET][nuget_batch_net] client library to create a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="941ff-159">MSDN에서 [Batch .NET 참조 설명서][api_net]를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-159">You can find the [Batch .NET reference documentation][api_net] on MSDN.</span></span>

<span data-ttu-id="941ff-160">다음 코드 조각에서는 [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] 메서드를 사용하여 현재 지원되는 Marketplace 이미지 및 노드 에이전트 SKU 조합의 목록에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-160">The following code snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to select from the list of currently supported Marketplace image and node agent SKU combinations.</span></span> <span data-ttu-id="941ff-161">지원되는 조합 목록이 언제든지 바뀔 수 있으므로 이 기술이 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-161">This technique is desirable because the list of supported combinations may change from time to time.</span></span> <span data-ttu-id="941ff-162">가장 일반적으로 지원되는 조합을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-162">Most commonly, supported combinations are added.</span></span>

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us to select from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of the VM image
// that we wish to use.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain the first node agent SKU in the collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create the VirtualMachineConfiguration for use when actually
// creating the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create the unbound pool object using the VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit the pool to the Batch service
await pool.CommitAsync();
```

<span data-ttu-id="941ff-163">이전의 코드 조각은 [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] 메서드를 사용하여 동적으로 나열하고 지원되는 이미지와 노드 에이전트 SKU 조합에서 선택(권장)하지만, [ImageReference][net_imagereference]를 명시적으로 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-163">Although the previous snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to dynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a><span data-ttu-id="941ff-164">가상 컴퓨터 이미지 목록</span><span class="sxs-lookup"><span data-stu-id="941ff-164">List of virtual machine images</span></span>
<span data-ttu-id="941ff-165">다음 표에는 이 문서가 마지막으로 업데이트되었을 때 사용 가능한 Batch 노드 에이전트와 호환되는 Marketplace 가상 컴퓨터 이미지가 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-165">The following table lists the Marketplace virtual machine images that are compatible with the available Batch node agents when this article was last updated.</span></span> <span data-ttu-id="941ff-166">이미지와 노드 에이전트는 언제든지 추가 또는 제거될 수 있기 때문에 이 목록은 확정적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-166">It is important to note that this list is not definitive because images and node agents may be added or removed at any time.</span></span> <span data-ttu-id="941ff-167">Batch 응용 프로그램 및 서비스에서는 현재 사용 가능한 SKU를 확인하고 선택하는[list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET)를 항상 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-167">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET) to determine and select from the currently available SKUs.</span></span>

> [!WARNING]
> <span data-ttu-id="941ff-168">다음 목록은 언제든지 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-168">The following list may change at any time.</span></span> <span data-ttu-id="941ff-169">항상 Batch API에서 사용 가능한 **list node agent SKU** 메서드를 사용하여 Batch 작업 실행 시 호환되는 가상 컴퓨터 및 노드 에이전트 SKU를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-169">Always use the **list node agent SKU** methods available in the Batch APIs to list the compatible virtual machine and node agent SKUs when you run your Batch jobs.</span></span>
>
>

| <span data-ttu-id="941ff-170">**게시자**</span><span class="sxs-lookup"><span data-stu-id="941ff-170">**Publisher**</span></span> | <span data-ttu-id="941ff-171">**제안**</span><span class="sxs-lookup"><span data-stu-id="941ff-171">**Offer**</span></span> | <span data-ttu-id="941ff-172">**이미지 SKU**</span><span class="sxs-lookup"><span data-stu-id="941ff-172">**Image SKU**</span></span> | <span data-ttu-id="941ff-173">**버전**</span><span class="sxs-lookup"><span data-stu-id="941ff-173">**Version**</span></span> | <span data-ttu-id="941ff-174">**노드 에이전트 SKU ID**</span><span class="sxs-lookup"><span data-stu-id="941ff-174">**Node agent SKU ID**</span></span> |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| <span data-ttu-id="941ff-175">Canonical</span><span class="sxs-lookup"><span data-stu-id="941ff-175">Canonical</span></span> | <span data-ttu-id="941ff-176">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="941ff-176">UbuntuServer</span></span> | <span data-ttu-id="941ff-177">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="941ff-177">14.04.5-LTS</span></span> | <span data-ttu-id="941ff-178">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-178">latest</span></span> | <span data-ttu-id="941ff-179">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="941ff-179">batch.node.ubuntu 14.04</span></span> |
| <span data-ttu-id="941ff-180">Canonical</span><span class="sxs-lookup"><span data-stu-id="941ff-180">Canonical</span></span> | <span data-ttu-id="941ff-181">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="941ff-181">UbuntuServer</span></span> | <span data-ttu-id="941ff-182">16.04.0-LTS</span><span class="sxs-lookup"><span data-stu-id="941ff-182">16.04.0-LTS</span></span> | <span data-ttu-id="941ff-183">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-183">latest</span></span> | <span data-ttu-id="941ff-184">batch.node.ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="941ff-184">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="941ff-185">Credativ</span><span class="sxs-lookup"><span data-stu-id="941ff-185">Credativ</span></span> | <span data-ttu-id="941ff-186">Debian</span><span class="sxs-lookup"><span data-stu-id="941ff-186">Debian</span></span> | <span data-ttu-id="941ff-187">8</span><span class="sxs-lookup"><span data-stu-id="941ff-187">8</span></span> | <span data-ttu-id="941ff-188">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-188">latest</span></span> | <span data-ttu-id="941ff-189">batch.node.debian 8</span><span class="sxs-lookup"><span data-stu-id="941ff-189">batch.node.debian 8</span></span> |
| <span data-ttu-id="941ff-190">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="941ff-190">OpenLogic</span></span> | <span data-ttu-id="941ff-191">CentOS</span><span class="sxs-lookup"><span data-stu-id="941ff-191">CentOS</span></span> | <span data-ttu-id="941ff-192">7.0</span><span class="sxs-lookup"><span data-stu-id="941ff-192">7.0</span></span> | <span data-ttu-id="941ff-193">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-193">latest</span></span> | <span data-ttu-id="941ff-194">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="941ff-194">batch.node.centos 7</span></span> |
| <span data-ttu-id="941ff-195">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="941ff-195">OpenLogic</span></span> | <span data-ttu-id="941ff-196">CentOS</span><span class="sxs-lookup"><span data-stu-id="941ff-196">CentOS</span></span> | <span data-ttu-id="941ff-197">7.1</span><span class="sxs-lookup"><span data-stu-id="941ff-197">7.1</span></span> | <span data-ttu-id="941ff-198">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-198">latest</span></span> | <span data-ttu-id="941ff-199">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="941ff-199">batch.node.centos 7</span></span> |
| <span data-ttu-id="941ff-200">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="941ff-200">OpenLogic</span></span> | <span data-ttu-id="941ff-201">CentOS-HPC</span><span class="sxs-lookup"><span data-stu-id="941ff-201">CentOS-HPC</span></span> | <span data-ttu-id="941ff-202">7.1</span><span class="sxs-lookup"><span data-stu-id="941ff-202">7.1</span></span> | <span data-ttu-id="941ff-203">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-203">latest</span></span> | <span data-ttu-id="941ff-204">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="941ff-204">batch.node.centos 7</span></span> |
| <span data-ttu-id="941ff-205">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="941ff-205">OpenLogic</span></span> | <span data-ttu-id="941ff-206">CentOS</span><span class="sxs-lookup"><span data-stu-id="941ff-206">CentOS</span></span> | <span data-ttu-id="941ff-207">7.2</span><span class="sxs-lookup"><span data-stu-id="941ff-207">7.2</span></span> | <span data-ttu-id="941ff-208">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-208">latest</span></span> | <span data-ttu-id="941ff-209">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="941ff-209">batch.node.centos 7</span></span> |
| <span data-ttu-id="941ff-210">Oracle</span><span class="sxs-lookup"><span data-stu-id="941ff-210">Oracle</span></span> | <span data-ttu-id="941ff-211">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="941ff-211">Oracle-Linux</span></span> | <span data-ttu-id="941ff-212">7.0</span><span class="sxs-lookup"><span data-stu-id="941ff-212">7.0</span></span> | <span data-ttu-id="941ff-213">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-213">latest</span></span> | <span data-ttu-id="941ff-214">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="941ff-214">batch.node.centos 7</span></span> |
| <span data-ttu-id="941ff-215">Oracle</span><span class="sxs-lookup"><span data-stu-id="941ff-215">Oracle</span></span> | <span data-ttu-id="941ff-216">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="941ff-216">Oracle-Linux</span></span> | <span data-ttu-id="941ff-217">7.2</span><span class="sxs-lookup"><span data-stu-id="941ff-217">7.2</span></span> | <span data-ttu-id="941ff-218">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-218">latest</span></span> | <span data-ttu-id="941ff-219">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="941ff-219">batch.node.centos 7</span></span> |
| <span data-ttu-id="941ff-220">SUSE</span><span class="sxs-lookup"><span data-stu-id="941ff-220">SUSE</span></span> | <span data-ttu-id="941ff-221">openSUSE</span><span class="sxs-lookup"><span data-stu-id="941ff-221">openSUSE</span></span> | <span data-ttu-id="941ff-222">13.2</span><span class="sxs-lookup"><span data-stu-id="941ff-222">13.2</span></span> | <span data-ttu-id="941ff-223">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-223">latest</span></span> | <span data-ttu-id="941ff-224">batch.node.opensuse 13.2</span><span class="sxs-lookup"><span data-stu-id="941ff-224">batch.node.opensuse 13.2</span></span> |
| <span data-ttu-id="941ff-225">SUSE</span><span class="sxs-lookup"><span data-stu-id="941ff-225">SUSE</span></span> | <span data-ttu-id="941ff-226">openSUSE-Leap</span><span class="sxs-lookup"><span data-stu-id="941ff-226">openSUSE-Leap</span></span> | <span data-ttu-id="941ff-227">42.1</span><span class="sxs-lookup"><span data-stu-id="941ff-227">42.1</span></span> | <span data-ttu-id="941ff-228">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-228">latest</span></span> | <span data-ttu-id="941ff-229">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="941ff-229">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="941ff-230">SUSE</span><span class="sxs-lookup"><span data-stu-id="941ff-230">SUSE</span></span> | <span data-ttu-id="941ff-231">SLES</span><span class="sxs-lookup"><span data-stu-id="941ff-231">SLES</span></span> | <span data-ttu-id="941ff-232">12-SP1</span><span class="sxs-lookup"><span data-stu-id="941ff-232">12-SP1</span></span> | <span data-ttu-id="941ff-233">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-233">latest</span></span> | <span data-ttu-id="941ff-234">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="941ff-234">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="941ff-235">SUSE</span><span class="sxs-lookup"><span data-stu-id="941ff-235">SUSE</span></span> | <span data-ttu-id="941ff-236">SLES-HPC</span><span class="sxs-lookup"><span data-stu-id="941ff-236">SLES-HPC</span></span> | <span data-ttu-id="941ff-237">12-SP1</span><span class="sxs-lookup"><span data-stu-id="941ff-237">12-SP1</span></span> | <span data-ttu-id="941ff-238">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-238">latest</span></span> | <span data-ttu-id="941ff-239">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="941ff-239">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="941ff-240">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="941ff-240">microsoft-ads</span></span> | <span data-ttu-id="941ff-241">linux-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="941ff-241">linux-data-science-vm</span></span> | <span data-ttu-id="941ff-242">linuxdsvm</span><span class="sxs-lookup"><span data-stu-id="941ff-242">linuxdsvm</span></span> | <span data-ttu-id="941ff-243">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-243">latest</span></span> | <span data-ttu-id="941ff-244">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="941ff-244">batch.node.centos 7</span></span> |
| <span data-ttu-id="941ff-245">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="941ff-245">microsoft-ads</span></span> | <span data-ttu-id="941ff-246">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="941ff-246">standard-data-science-vm</span></span> | <span data-ttu-id="941ff-247">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="941ff-247">standard-data-science-vm</span></span> | <span data-ttu-id="941ff-248">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-248">latest</span></span> | <span data-ttu-id="941ff-249">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="941ff-249">batch.node.windows amd64</span></span> |
| <span data-ttu-id="941ff-250">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="941ff-250">MicrosoftWindowsServer</span></span> | <span data-ttu-id="941ff-251">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="941ff-251">WindowsServer</span></span> | <span data-ttu-id="941ff-252">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="941ff-252">2008-R2-SP1</span></span> | <span data-ttu-id="941ff-253">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-253">latest</span></span> | <span data-ttu-id="941ff-254">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="941ff-254">batch.node.windows amd64</span></span> |
| <span data-ttu-id="941ff-255">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="941ff-255">MicrosoftWindowsServer</span></span> | <span data-ttu-id="941ff-256">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="941ff-256">WindowsServer</span></span> | <span data-ttu-id="941ff-257">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="941ff-257">2012-Datacenter</span></span> | <span data-ttu-id="941ff-258">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-258">latest</span></span> | <span data-ttu-id="941ff-259">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="941ff-259">batch.node.windows amd64</span></span> |
| <span data-ttu-id="941ff-260">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="941ff-260">MicrosoftWindowsServer</span></span> | <span data-ttu-id="941ff-261">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="941ff-261">WindowsServer</span></span> | <span data-ttu-id="941ff-262">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="941ff-262">2012-R2-Datacenter</span></span> | <span data-ttu-id="941ff-263">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-263">latest</span></span> | <span data-ttu-id="941ff-264">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="941ff-264">batch.node.windows amd64</span></span> |
| <span data-ttu-id="941ff-265">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="941ff-265">MicrosoftWindowsServer</span></span> | <span data-ttu-id="941ff-266">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="941ff-266">WindowsServer</span></span> | <span data-ttu-id="941ff-267">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="941ff-267">2016-Datacenter</span></span> | <span data-ttu-id="941ff-268">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-268">latest</span></span> | <span data-ttu-id="941ff-269">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="941ff-269">batch.node.windows amd64</span></span> |
| <span data-ttu-id="941ff-270">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="941ff-270">MicrosoftWindowsServer</span></span> | <span data-ttu-id="941ff-271">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="941ff-271">WindowsServer</span></span> | <span data-ttu-id="941ff-272">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="941ff-272">2016-Datacenter-with-Containers</span></span> | <span data-ttu-id="941ff-273">최신</span><span class="sxs-lookup"><span data-stu-id="941ff-273">latest</span></span> | <span data-ttu-id="941ff-274">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="941ff-274">batch.node.windows amd64</span></span> |

## <a name="connect-to-linux-nodes-using-ssh"></a><span data-ttu-id="941ff-275">SSH를 사용하여 Linux 노드에 연결</span><span class="sxs-lookup"><span data-stu-id="941ff-275">Connect to Linux nodes using SSH</span></span>
<span data-ttu-id="941ff-276">개발 또는 문제 해결 동안 풀의 노드에 로그인할 필요가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-276">During development or while troubleshooting, you may find it necessary to sign in to the nodes in your pool.</span></span> <span data-ttu-id="941ff-277">Windows 계산 노드와 달리 Linux 노드에 연결하기 위해 RDP(원격 데스크톱 프로토콜)를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-277">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) to connect to Linux nodes.</span></span> <span data-ttu-id="941ff-278">대신, Batch 서비스는 원격 연결을 위해 각 노드에서 SSH 액세스를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-278">Instead, the Batch service enables SSH access on each node for remote connection.</span></span>

<span data-ttu-id="941ff-279">다음 Python 코드 조각에서는 풀의 각 노드에서 사용자를 만들며 이는 원격 연결에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-279">The following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span></span> <span data-ttu-id="941ff-280">그런 다음 각 노드에 대한 SSH(secure shell) 연결 정보를 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-280">It then prints the secure shell (SSH) connection information for each node.</span></span>

```python
import datetime
import getpass
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify your own account credentials
batch_account_name = ''
batch_account_key = ''
batch_account_url = ''

# Specify the ID of an existing pool containing Linux nodes
# currently in the 'idle' state
pool_id = ''

# Specify the username and prompt for a password
username = 'linuxuser'
password = getpass.getpass()

# Create a BatchClient
credentials = batchauth.SharedKeyCredentials(
    batch_account_name,
    batch_account_key
)
batch_client = batch.BatchServiceClient(
        credentials,
        base_url=batch_account_url
)

# Create the user that will be added to each node in the pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get the list of nodes in the pool
nodes = batch_client.compute_node.list(pool_id)

# Add the user to each node in the pool and print
# the connection information for the node
for node in nodes:
    # Add the user to the node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for the node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print the connection info for the node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

<span data-ttu-id="941ff-281">다음은 4개의 Linux 노드를 포함하는 풀에 대한 이전 코드의 샘플 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-281">Here is sample output for the previous code for a pool that contains four Linux nodes:</span></span>

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

<span data-ttu-id="941ff-282">노드에 사용자를 만들 때 암호 대신 SSH 공개 키를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-282">Instead of a password, you can specify an SSH public key when you create a user on a node.</span></span> <span data-ttu-id="941ff-283">Python SDK에서는 [ComputeNodeUser][py_computenodeuser]에 **ssh_public_key** 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-283">In the Python SDK, use the **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span></span> <span data-ttu-id="941ff-284">.NET에서는 [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-284">In .NET, use the [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span></span>

## <a name="pricing"></a><span data-ttu-id="941ff-285">가격</span><span class="sxs-lookup"><span data-stu-id="941ff-285">Pricing</span></span>
<span data-ttu-id="941ff-286">Azure Batch는 Azure 클라우드 서비스 및 Azure 가상 컴퓨터 기술을 기반으로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-286">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span></span> <span data-ttu-id="941ff-287">Batch 서비스 자체는 무료로 제공됩니다. 즉, Batch 솔루션에서 사용하는 계산 리소스에 대해서만 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-287">The Batch service itself is offered at no cost, which means you are charged only for the compute resources that your Batch solutions consume.</span></span> <span data-ttu-id="941ff-288">**Cloud Services 구성**을 선택하는 경우 [Cloud Services 가격][cloud_services_pricing] 구조에 따라 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-288">When you choose **Cloud Services Configuration**, you are charged based on the [Cloud Services pricing][cloud_services_pricing] structure.</span></span> <span data-ttu-id="941ff-289">**가상 컴퓨터 구성**을 선택하는 경우 [Virtual Machines 가격][vm_pricing] 구조에 따라 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-289">When you choose **Virtual Machine Configuration**, you are charged based on the [Virtual Machines pricing][vm_pricing] structure.</span></span> 

<span data-ttu-id="941ff-290">[응용 프로그램 패키지](batch-application-packages.md)를 사용하여 Batch 노드에 응용 프로그램을 배포하는 경우에도 응용 프로그램 패키지에서 사용하는 Azure Storage 리소스에 대한 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-290">If you deploy applications to your Batch nodes using [application packages](batch-application-packages.md), you are also charged for the Azure Storage resources that your application packages consume.</span></span> <span data-ttu-id="941ff-291">일반적으로 Azure Storage 비용은 최소입니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-291">In general, the Azure Storage costs are minimal.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="941ff-292">다음 단계</span><span class="sxs-lookup"><span data-stu-id="941ff-292">Next steps</span></span>
### <a name="batch-python-tutorial"></a><span data-ttu-id="941ff-293">Batch Python 자습서</span><span class="sxs-lookup"><span data-stu-id="941ff-293">Batch Python tutorial</span></span>
<span data-ttu-id="941ff-294">Python을 사용하여 Batch로 작업하는 방법에 대한 자세한 자습서를 보려면 [Azure Batch Python 클라이언트 시작](batch-python-tutorial.md)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-294">For a more in-depth tutorial about how to work with Batch by using Python, check out [Get started with the Azure Batch Python client](batch-python-tutorial.md).</span></span> <span data-ttu-id="941ff-295">함께 제공되는 [코드 샘플][github_samples_pyclient]에는 가상 컴퓨터 구성을 가져오기 위한 다른 기법을 보여 주는 도우미 함수(`get_vm_config_for_distro`)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-295">Its companion [code sample][github_samples_pyclient] includes a helper function, `get_vm_config_for_distro`, that shows another technique to obtain a virtual machine configuration.</span></span>

### <a name="batch-python-code-samples"></a><span data-ttu-id="941ff-296">Batch Python 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="941ff-296">Batch Python code samples</span></span>
<span data-ttu-id="941ff-297">GitHub의 [azure-batch-samples][github_samples] 리포지토리에 있는 [Python 코드 샘플][github_samples_py]에는 풀, 작업 및 태스크 만들기와 같은 일반적인 Batch 작업 수행 방법을 보여 주는 스크립트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-297">The [Python code samples][github_samples_py] in the [azure-batch-samples][github_samples] repository on GitHub contain scripts that show you how to perform common Batch operations, such as pool, job, and task creation.</span></span> <span data-ttu-id="941ff-298">Python 샘플과 함께 제공되는 [추가 정보][github_py_readme]에는 필요한 패키지를 설치하는 방법에 대한 세부 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-298">The [README][github_py_readme] that accompanies the Python samples has details about how to install the required packages.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="941ff-299">Batch 포럼</span><span class="sxs-lookup"><span data-stu-id="941ff-299">Batch forum</span></span>
<span data-ttu-id="941ff-300">MSDN의 [Azure Batch 포럼][forum]은 Batch를 설명하고 서비스에 대한 질문을 하는 데 많은 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-300">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="941ff-301">유용한 "고정된" 게시물을 참조하고 Batch 솔루션을 빌드하는 동안 질문이 생기면 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="941ff-301">Read helpful "pinned" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[cloud_services_pricing]: https://azure.microsoft.com/pricing/details/cloud-services/
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_py_readme]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/README.md
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_py]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[github_samples_pyclient]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/python_tutorial_client.py
[portal]: https://portal.azure.com
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_computenodeuser]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.aspx
[net_imagereference]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.imagereference.aspx
[net_list_skus]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listnodeagentskus.aspx
[net_pool_ops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.aspx
[net_ssh_key]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.sshpublickey.aspx
[nuget_batch_net]: https://www.nuget.org/packages/Azure.Batch/
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_list_skus]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
[vm_pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/
