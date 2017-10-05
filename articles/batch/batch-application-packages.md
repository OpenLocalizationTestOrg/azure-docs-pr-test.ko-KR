---
title: "계산 노드에 응용 프로그램 패키지 설치 - Azure Batch | Microsoft Docs"
description: "Azure Batch의 응용 프로그램 패키지 기능을 사용하여 Batch 계산 노드에 설치할 여러 응용 프로그램 및 버전을 간편하게 관리하세요."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: afcc04c80ec15872a22de5d5969a7ef6a583562f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-applications-to-compute-nodes-with-batch-application-packages"></a><span data-ttu-id="1c9f8-103">응용 프로그램을 배포하여 Batch 응용 프로그램 패키지에서 노드 계산</span><span class="sxs-lookup"><span data-stu-id="1c9f8-103">Deploy applications to compute nodes with Batch application packages</span></span>

<span data-ttu-id="1c9f8-104">Azure Batch의 응용 프로그램 패키지 기능은 풀의 계산 노드에 태스크 응용 프로그램 및 해당 배포를 간편하게 관리할 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-104">The application packages feature of Azure Batch provides easy management of task applications and their deployment to the compute nodes in your pool.</span></span> <span data-ttu-id="1c9f8-105">응용 프로그램 패키지를 사용하여 지원 파일을 비롯하여 태스크에서 실행하는 여러 응용 프로그램 버전을 업로드하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-105">With application packages, you can upload and manage multiple versions of the applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="1c9f8-106">풀의 계산 노드에 이러한 응용 프로그램을 하나 이상 자동으로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-106">You can then automatically deploy one or more of these applications to the compute nodes in your pool.</span></span>

<span data-ttu-id="1c9f8-107">이 문서에서는 Azure portal을 사용하여 응용 프로그램 패키지를 업로드하고 관리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-107">In this article, you will learn how to upload and manage application packages in the Azure portal.</span></span> <span data-ttu-id="1c9f8-108">[Batch .NET][api_net] 라이브러리를 사용하여 풀의 계산 노드에 설치하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-108">You will then learn how to install them on a pool's compute nodes with the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="1c9f8-109">응용 프로그램 패키지는 2017년 7월 5일 이후에 만들어진 모든 Batch 풀에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="1c9f8-110">2016년 3월 10일에서 2017년 7월 5일 사이에 만들어진 Batch 풀에서는 Cloud Service 구성을 사용하여 풀을 만든 경우에만 이러한 패키지가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="1c9f8-111">2016년 3월 10일 이전에 만들어진 Batch 풀은 응용 프로그램 패키지를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-111">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="1c9f8-112">응용 프로그램 패키지를 만들고 관리하는 API는 [Batch Management .NET][[api_net_mgmt]] 라이브러리의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-112">The APIs for creating and managing application packages are part of the [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="1c9f8-113">계산 노드에서 응용 프로그램 패키지를 설치하는 API는 [Batch .NET][api_net] 라이브러리의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-113">The APIs for installing application packages on a compute node are part of the [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="1c9f8-114">여기서 설명하는 응용 프로그램 패키지 기능은 이전 버전의 서비스에서 사용할 수 있는 Batch 앱 기능을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-114">The application packages feature described here supersedes the Batch Apps feature available in previous versions of the service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="1c9f8-115">응용 프로그램 패키지 요구 사항</span><span class="sxs-lookup"><span data-stu-id="1c9f8-115">Application package requirements</span></span>
<span data-ttu-id="1c9f8-116">응용 프로그램 패키지를 사용하려면 Batch 계정에 [Azure Storage 계정을 연결](#link-a-storage-account)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-116">To use application packages, you need to [link an Azure Storage account](#link-a-storage-account) to your Batch account.</span></span>

<span data-ttu-id="1c9f8-117">이 기능은 [Batch REST API][api_rest] 버전 2015-12-01.2.2 및 해당 [Batch .NET][api_net] 라이브러리 버전 3.1.0에서 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and the corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="1c9f8-118">Batch를 사용할 때에는 항상 최신 API 버전을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-118">We recommend that you always use the latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="1c9f8-119">응용 프로그램 패키지는 2017년 7월 5일 이후에 만들어진 모든 Batch 풀에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="1c9f8-120">2016년 3월 10일에서 2017년 7월 5일 사이에 만들어진 Batch 풀에서는 Cloud Service 구성을 사용하여 풀을 만든 경우에만 이러한 패키지가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="1c9f8-121">2016년 3월 10일 이전에 만들어진 Batch 풀은 응용 프로그램 패키지를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-121">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="1c9f8-122">응용 프로그램 및 응용 프로그램 패키지 정보</span><span class="sxs-lookup"><span data-stu-id="1c9f8-122">About applications and application packages</span></span>
<span data-ttu-id="1c9f8-123">Azure Batch 내에서 *응용 프로그램* 이란 풀의 계산 노드에 자동으로 다운로드할 수 있는 버전이 지정된 이진 파일의 집합을 말합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-123">Within Azure Batch, an *application* refers to a set of versioned binaries that can be automatically downloaded to the compute nodes in your pool.</span></span> <span data-ttu-id="1c9f8-124">*응용 프로그램 패키지*는 이러한 이진 파일의 *특정 집합*을 말하며, 지정된 응용 프로그램 *버전*을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-124">An *application package* refers to a *specific set* of those binaries and represents a given *version* of the application.</span></span>

<span data-ttu-id="1c9f8-125">![응용 프로그램 및 응용 프로그램 패키지에 대한 개략적인 다이어그램][1]</span><span class="sxs-lookup"><span data-stu-id="1c9f8-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="1c9f8-126">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="1c9f8-126">Applications</span></span>
<span data-ttu-id="1c9f8-127">Batch에서 응용 프로그램은 하나 이상의 응용 프로그램을 포함하거나 응용 프로그램에 대한 구성 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-127">An application in Batch contains one or more application packages and specifies configuration options for the application.</span></span> <span data-ttu-id="1c9f8-128">예를 들어 응용 프로그램은 계산 노드에 설치할 기본 응용 프로그램 패키지 버전, 응용 프로그램 패키지를 업데이트할지 아니면 삭제할 것인지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-128">For example, an application can specify the default application package version to install on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="1c9f8-129">응용 프로그램 패키지</span><span class="sxs-lookup"><span data-stu-id="1c9f8-129">Application packages</span></span>
<span data-ttu-id="1c9f8-130">응용 프로그램 패키지는 태스크가 응용 프로그램을 실행하는 데 필요한 응용 프로그램 이진 파일 및 지원 파일이 포함된 .zip 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-130">An application package is a .zip file that contains the application binaries and supporting files that are required for your tasks to run the application.</span></span> <span data-ttu-id="1c9f8-131">각 응용 프로그램 패키지는 응용 프로그램의 특정 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-131">Each application package represents a specific version of the application.</span></span>

<span data-ttu-id="1c9f8-132">풀 및 태스크 수준에서 응용 프로그램 패키지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-132">You can specify application packages at the pool and task levels.</span></span> <span data-ttu-id="1c9f8-133">풀 또는 태스크를 만들 때 이러한 패키지 및 버전(선택 사항)을 하나 이상 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="1c9f8-134">**풀 응용 프로그램 패키지** 는 *모든* 노드에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-134">**Pool application packages** are deployed to *every* node in the pool.</span></span> <span data-ttu-id="1c9f8-135">응용 프로그램은 노드가 풀을 조인하고 재부팅되거나 이미지를 다시 설치할 때 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="1c9f8-136">풀 응용 프로그램 패키지는 풀에 있는 모든 노드가 작업의 태스크를 실행할 때 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="1c9f8-137">풀을 만들 때 하나 이상의 응용 프로그램 패키지를 지정할 수 있으며 기존 풀의 패키지를 추가하거나 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="1c9f8-138">기존 풀의 응용 프로그램 패키지를 업데이트하는 경우 새 패키지를 설치하려면 해당 노드를 다시 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-138">If you update an existing pool's application packages, you must restart its nodes to install the new package.</span></span>
* <span data-ttu-id="1c9f8-139">**태스크 응용 프로그램 패키지** 는 태스크의 명령줄을 실행하기 바로 전에 태스크를 실행하도록 예약된 계산 노드에만 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-139">**Task application packages** are deployed only to a compute node scheduled to run a task, just before running the task's command line.</span></span> <span data-ttu-id="1c9f8-140">지정된 응용 프로그램 패키지 및 버전이 노드에 이미 있는 경우 다시 배포되지 않으며 기존 패키지가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-140">If the specified application package and version is already on the node, it is not redeployed and the existing package is used.</span></span>
  
    <span data-ttu-id="1c9f8-141">태스크 응용 프로그램 패키지는 공유 풀 환경에서 유용하며 여기서는 다른 작업이 하나의 풀에서 실행되고 작업이 완료될 때 풀이 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and the pool is not deleted when a job is completed.</span></span> <span data-ttu-id="1c9f8-142">작업에 있는 태스크가 풀에 있는 노드보다 적은 경우 태스크를 실행하는 노드에만 응용 프로그램을 배포하므로 태스크 응용 프로그램 패키지는 데이터 전송을 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-142">If your job has fewer tasks than nodes in the pool, task application packages can minimize data transfer since your application is deployed only to the nodes that run tasks.</span></span>
  
    <span data-ttu-id="1c9f8-143">태스크 응용 프로그램 패키지를 활용할 수 있는 다른 시나리오는 큰 응용 프로그램을 실행하지만 태스크 수는 적은 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="1c9f8-144">예를 들어 전처리 또는 병합 응용 프로그램이 대규모인 전처리 단계나 병합 태스크는 태스크 응용 프로그램 패키지를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-144">For example, a pre-processing stage or a merge task, where the pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c9f8-145">Batch 계정 내 응용 프로그램 및 응용 프로그램 패키지 수와 응용 프로그램 패키지의 최대 크기에 대한 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-145">There are restrictions on the number of applications and application packages within a Batch account and on the maximum application package size.</span></span> <span data-ttu-id="1c9f8-146">이러한 제한에 대한 자세한 내용은 [Azure Batch 서비스에 대한 할당량 및 제한](batch-quota-limit.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-146">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="1c9f8-147">응용 프로그램 패키지의 이점</span><span class="sxs-lookup"><span data-stu-id="1c9f8-147">Benefits of application packages</span></span>
<span data-ttu-id="1c9f8-148">응용 프로그램 패키지는 Batch 솔루션의 코드를 단순화하고, 태스크에서 실행하는 응용 프로그램을 관리하는 데 필요한 오버헤드를 낮출 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-148">Application packages can simplify the code in your Batch solution and lower the overhead required to manage the applications that your tasks run.</span></span>

<span data-ttu-id="1c9f8-149">응용 프로그램 패키지를 사용하면 풀의 시작 태스크가 노드에 설치할 개별 리소스 파일의 긴 목록을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-149">With application packages, your pool's start task doesn't have to specify a long list of individual resource files to install on the nodes.</span></span> <span data-ttu-id="1c9f8-150">Azure Storage 또는 노드에서 응용 프로그램 파일의 여러 버전을 수동으로 관리할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-150">You don't have to manually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="1c9f8-151">저장소 계정의 파일에 대한 액세스 권한을 제공하기 위해 [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 을 생성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-151">And, you don't need to worry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to provide access to the files in your Storage account.</span></span> <span data-ttu-id="1c9f8-152">Batch는 Azure Storage와 함께 백그라운드에서 작동하여 응용 프로그램 패키지를 저장하고 계산 노드에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-152">Batch works in the background with Azure Storage to store application packages and deploy them to compute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="1c9f8-153">리소스 파일 및 환경 변수를 포함한 시작 태스크의 전체 크기는 32768자 이하여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-153">The total size of a start task must be less than or equal to 32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="1c9f8-154">시작 태스크가 이 제한을 초과하는 경우 응용 프로그램 패키지 사용은 또 다른 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="1c9f8-155">리소스 파일을 포함하는 압축된 보관 파일을 만들어 Blob으로 Azure Storage에 업로드한 다음 시작 태스크의 명령줄에서 압축을 풀 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-155">You can also create a zipped archive containing your resource files, upload it as a blob to Azure Storage, and then unzip it from the command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="1c9f8-156">응용 프로그램 업로드 및 관리</span><span class="sxs-lookup"><span data-stu-id="1c9f8-156">Upload and manage applications</span></span>
<span data-ttu-id="1c9f8-157">[Azure portal][portal] 또는 [Batch 관리 .NET](batch-management-dotnet.md)라이브러리를 사용하여 Batch 계정에서 응용 프로그램 패키지를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-157">You can use the [Azure portal][portal] or the [Batch Management .NET](batch-management-dotnet.md) library to manage the application packages in your Batch account.</span></span> <span data-ttu-id="1c9f8-158">다음 섹션에서는 먼저 저장소 계정을 연결하는 방법을 보여 준 다음 응용 프로그램 및 패키지를 추가하고 포털에서 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-158">In the next few sections, we first show how to link a Storage account, then discuss adding applications and packages and managing them with the portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="1c9f8-159">저장소 계정 연결</span><span class="sxs-lookup"><span data-stu-id="1c9f8-159">Link a Storage account</span></span>
<span data-ttu-id="1c9f8-160">응용 프로그램 패키지를 사용하려면 먼저 Azure Storage 계정을 Batch 계정에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-160">To use application packages, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="1c9f8-161">저장소 계정을 아직 구성하지 않은 경우 **Batch 계정** 블레이드에서 **응용 프로그램** 타일을 처음으로 클릭하면 Azure Portal에서 경고를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-161">If you have not yet configured a Storage account, the Azure portal displays a warning the first time you click the **Applications** tile in the **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c9f8-162">Batch는 현재 [Azure storage 계정 정보](../storage/common/storage-create-storage-account.md)의 5단계 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)에 설명된 대로 **범용** 저장소 계정 유형*만* 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-162">Batch currently supports *only* the **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="1c9f8-163">Azure Storage 계정을 Batch 계정에 연결할 경우 **범용** 저장소 계정*만* 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-163">When you link an Azure Storage account to your Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="1c9f8-164">![Azure Portal의 '저장소 계정이 구성되지 않음' 경고][9]</span><span class="sxs-lookup"><span data-stu-id="1c9f8-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="1c9f8-165">Batch 서비스는 연결된 저장소 계정을 사용하여 응용 프로그램 패키지를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-165">The Batch service uses the associated Storage account to store your application packages.</span></span> <span data-ttu-id="1c9f8-166">계정 두 개를 연결한 후에 Batch는 연결된 저장소 계정에 저장된 패키지를 계산 노드에 자동으로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-166">After you've linked the two accounts, Batch can automatically deploy the packages stored in the linked Storage account to your compute nodes.</span></span> <span data-ttu-id="1c9f8-167">저장소 계정을 Batch 계정에 연결하려면 **경고** 블레이드에서 **저장소 계정 설정**을 클릭한 다음 **저장소 계정** 블레이드에서 **저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-167">To link a Storage account to your Batch account, click **Storage account settings** on the **Warning** blade, and then click **Storage Account** on the **Storage Account** blade.</span></span>

<span data-ttu-id="1c9f8-168">![Azure portal에서 저장소 계정 블레이드 선택][10]</span><span class="sxs-lookup"><span data-stu-id="1c9f8-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="1c9f8-169">*특별히* Batch 계정과 함께 사용할 저장소 계정을 만들었으면 여기에서 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="1c9f8-170">저장소 계정을 만드는 방법에 대한 자세한 내용은 [Azure storage 계정 정보](../storage/common/storage-create-storage-account.md)의 "저장소 계정 만들기"를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-170">For details about how to create a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="1c9f8-171">저장소 계정을 만든 후에 **저장소 계정** 블레이드를 사용하여 Batch 계정에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-171">After you've created a Storage account, you can then link it to your Batch account by using the **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="1c9f8-172">Batch 서비스는 Azure Storage를 사용하여 응용 프로그램 패키지를 블록 Blob으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-172">The Batch service uses Azure Storage to store your application packages as block blobs.</span></span> <span data-ttu-id="1c9f8-173">블록 Blob 데이터에 대한 [요금이 정상적으로 청구][storage_pricing]됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-173">You are [charged as normal][storage_pricing] for the block blob data.</span></span> <span data-ttu-id="1c9f8-174">비용을 최소화할 수 있도록 응용 프로그램 패키지의 크기와 숫자에 신경 쓰고, 사용하지 않는 패키지를 주기적으로 제거해 주세요.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-174">Be sure to consider the size and number of your application packages, and periodically remove deprecated packages to minimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="1c9f8-175">현재 응용 프로그램 보기</span><span class="sxs-lookup"><span data-stu-id="1c9f8-175">View current applications</span></span>
<span data-ttu-id="1c9f8-176">Batch 계정의 응용 프로그램을 보려면 **Batch 계정** 블레이드 왼쪽에 있는 메뉴의 **응용 프로그램** 메뉴 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-176">To view the applications in your Batch account, click the **Applications** menu item in the left menu while viewing the **Batch account** blade.</span></span>

<span data-ttu-id="1c9f8-177">![응용 프로그램 타일][2]</span><span class="sxs-lookup"><span data-stu-id="1c9f8-177">![Applications tile][2]</span></span>

<span data-ttu-id="1c9f8-178">이 메뉴 옵션을 선택하면 **응용 프로그램** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-178">Selecting this menu option opens the **Applications** blade:</span></span>

<span data-ttu-id="1c9f8-179">![응용 프로그램 나열][3]</span><span class="sxs-lookup"><span data-stu-id="1c9f8-179">![List applications][3]</span></span>

<span data-ttu-id="1c9f8-180">**응용 프로그램** 블레이드는 계정의 각 응용 프로그램 ID 및 다음 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-180">The **Applications** blade displays the ID of each application in your account and the following properties:</span></span>

* <span data-ttu-id="1c9f8-181">**패키지**: 이 응용 프로그램과 연결된 버전 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-181">**Packages**: The number of versions associated with this application.</span></span>
* <span data-ttu-id="1c9f8-182">**기본 버전**: 풀에 대해 응용 프로그램을 지정할 때 버전을 표시하지 않으면 설치되는 응용 프로그램 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-182">**Default version**: The application version installed if you do not indicate a version when you specify the application for a pool.</span></span> <span data-ttu-id="1c9f8-183">이 설정은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-183">This setting is optional.</span></span>
* <span data-ttu-id="1c9f8-184">**업데이트 허용**: 패키지의 업데이트, 삭제 및 추가 기능을 허용하는지 여부를 지정하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-184">**Allow updates**: The value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="1c9f8-185">이 값을 **아니요**로 설정하면 응용 프로그램에 패키지 업데이트 및 삭제를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-185">If this is set to **No**, package updates and deletions are disabled for the application.</span></span> <span data-ttu-id="1c9f8-186">새 응용 프로그램 패키지 버전만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-186">Only new application package versions can be added.</span></span> <span data-ttu-id="1c9f8-187">기본값은 **예**입니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-187">The default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="1c9f8-188">응용 프로그램 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="1c9f8-188">View application details</span></span>
<span data-ttu-id="1c9f8-189">응용 프로그램에 대한 세부 정보가 포함된 블레이드를 열려면 **응용 프로그램** 블레이드에서 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-189">To open the blade that includes the details for an application, select the application in the **Applications** blade.</span></span>

<span data-ttu-id="1c9f8-190">![응용 프로그램 세부 정보][4]</span><span class="sxs-lookup"><span data-stu-id="1c9f8-190">![Application details][4]</span></span>

<span data-ttu-id="1c9f8-191">응용 프로그램 세부 정보 블레이드에서 응용 프로그램에 대해 다음 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-191">In the application details blade, you can configure the following settings for your application.</span></span>

* <span data-ttu-id="1c9f8-192">**업데이트 허용**: 해당 응용 프로그램 패키지를 업데이트하거나 삭제할 수 있는지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="1c9f8-193">이 문서에서 아래의 "응용 프로그램 패키지 업데이트 또는 삭제"를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="1c9f8-194">**기본 버전**: 계산 노드에 배포할 기본 응용 프로그램 패키지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-194">**Default version**: Specify a default application package to deploy to compute nodes.</span></span>
* <span data-ttu-id="1c9f8-195">**표시 이름**: Batch를 통해 고객에게 제공하는 서비스 UI처럼, Batch 솔루션이 응용 프로그램에 대한 정보를 표시할 때 사용할 수 있는 친숙한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about the application, for example, in the UI of a service that you provide to your customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="1c9f8-196">새 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="1c9f8-196">Add a new application</span></span>
<span data-ttu-id="1c9f8-197">새 응용 프로그램을 만들려면 응용 프로그램 패키지를 추가하고 고유한 새 응용 프로그램 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-197">To create a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="1c9f8-198">새 응용 프로그램 ID를 사용하여 추가하는 첫 번째 응용 프로그램 패키지도 새 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-198">The first application package that you add with the new application ID also creates the new application.</span></span>

<span data-ttu-id="1c9f8-199">**응용 프로그램** 블레이드에서 **추가**를 클릭하여 **새 응용 프로그램** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-199">Click **Add** on the **Applications** blade to open the **New application** blade.</span></span>

<span data-ttu-id="1c9f8-200">![Azure portal의 새 응용 프로그램 블레이드][5]</span><span class="sxs-lookup"><span data-stu-id="1c9f8-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="1c9f8-201">**새 응용 프로그램** 블레이드는 새 응용 프로그램 및 응용 프로그램 패키지의 설정을 지정하는 다음 필드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-201">The **New application** blade provides the following fields to specify the settings of your new application and application package.</span></span>

<span data-ttu-id="1c9f8-202">**응용 프로그램 ID**</span><span class="sxs-lookup"><span data-stu-id="1c9f8-202">**Application id**</span></span>

<span data-ttu-id="1c9f8-203">이 필드는 새 응용 프로그램의 ID를 지정하며, 표준 Azure Batch ID 유효성 검사 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-203">This field specifies the ID of your new application, which is subject to the standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="1c9f8-204">응용 프로그램 ID를 제공하는 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-204">The rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="1c9f8-205">Windows 노드에서 ID에는 영숫자, 하이픈 및 밑줄의 모든 조합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-205">On Windows nodes, the ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="1c9f8-206">Linux 노드에서는 영숫자와 밑줄만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="1c9f8-207">포함할 수 있는 최대 문자는 64자입니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="1c9f8-208">Batch 계정 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-208">Must be unique within the Batch account.</span></span>
* <span data-ttu-id="1c9f8-209">대/소문자를 유지하고 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="1c9f8-210">**버전**</span><span class="sxs-lookup"><span data-stu-id="1c9f8-210">**Version**</span></span>

<span data-ttu-id="1c9f8-211">이 필드는 사용자가 업로드하는 응용 프로그램 패키지의 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-211">This field specifies the version of the application package you are uploading.</span></span> <span data-ttu-id="1c9f8-212">버전 문자열은 다음 유효성 검사 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-212">Version strings are subject to the following validation rules:</span></span>

* <span data-ttu-id="1c9f8-213">Windows 노드에서 버전 문자열에는 영숫자, 하이픈, 밑줄 및 마침표의 모든 조합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-213">On Windows nodes, the version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="1c9f8-214">Linux 노드에서는 버전 문자열에 영숫자와 밑줄만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-214">On Linux nodes, the version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="1c9f8-215">포함할 수 있는 최대 문자는 64자입니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="1c9f8-216">응용 프로그램 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-216">Must be unique within the application.</span></span>
* <span data-ttu-id="1c9f8-217">대/소문자를 유지하고 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="1c9f8-218">**응용 프로그램 패키지**</span><span class="sxs-lookup"><span data-stu-id="1c9f8-218">**Application package**</span></span>

<span data-ttu-id="1c9f8-219">이 필드는 응용 프로그램 실행에 필요한 응용 프로그램 이진 파일 및 모든 지원 파일을 포함하는 .zip 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-219">This field specifies the .zip file that contains the application binaries and supporting files that are required to execute the application.</span></span> <span data-ttu-id="1c9f8-220">**파일 선택** 상자 또는 폴더 아이콘을 클릭하여 응용 프로그램의 파일이 포함된 .zip 파일을 찾고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-220">Click the **Select a file** box or the folder icon to browse to and select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="1c9f8-221">파일을 선택했으면 **확인** 을 클릭하여 Azure Storage에 업로드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-221">After you've selected a file, click **OK** to begin the upload to Azure Storage.</span></span> <span data-ttu-id="1c9f8-222">업로드 작업이 완료되면 포털에서 알림을 표시하고 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-222">When the upload operation is complete, the portal displays a notification and closes the blade.</span></span> <span data-ttu-id="1c9f8-223">업로드하는 파일의 크기 및 네트워크 연결 속도에 따라 작업 시간이 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-223">Depending on the size of the file that you are uploading and the speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="1c9f8-224">업로드 작업이 완료되기 전에 **새 응용 프로그램** 블레이드를 닫지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-224">Do not close the **New application** blade before the upload operation is complete.</span></span> <span data-ttu-id="1c9f8-225">만약 닫으면 업로드 프로세스가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-225">Doing so will stop the upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="1c9f8-226">새 응용 프로그램 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="1c9f8-226">Add a new application package</span></span>
<span data-ttu-id="1c9f8-227">기존 응용 프로그램에 대한 새 응용 프로그램 패키지 버전을 추가하려면 **응용 프로그램** 블레이드에서 응용 프로그램을 선택하고, **패키지**를 클릭한 다음 **추가**를 클릭하여 **패키지 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-227">To add a new application package version for an existing application, select an application in the **Applications** blade, click **Packages**, then click **Add** to open the **Add package** blade.</span></span>

<span data-ttu-id="1c9f8-228">![Azure portal의 응용 프로그램 패키지 추가 블레이드][8]</span><span class="sxs-lookup"><span data-stu-id="1c9f8-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="1c9f8-229">여기서 볼 수 있듯이 필드가 **새 응용 프로그램** 블레이드의 필드와 일치하지만 **응용 프로그램 ID** 상자는 비활성화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-229">As you can see, the fields match those of the **New application** blade, but the **Application id** box is disabled.</span></span> <span data-ttu-id="1c9f8-230">새 응용 프로그램에서 수행한 대로 새 패키지의 **버전**을 지정하고, **응용 프로그램 패키지** .zip 파일을 찾은 다음 **확인**을 클릭하여 패키지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-230">As you did for the new application, specify the **Version** for your new package, browse to your **Application package** .zip file, then click **OK** to upload the package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="1c9f8-231">응용 프로그램 패키지 업데이트 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="1c9f8-231">Update or delete an application package</span></span>
<span data-ttu-id="1c9f8-232">기존 응용 프로그램 패키지를 업데이트하거나 삭제하려면 해당 응용 프로그램의 세부 정보 블레이드를 연 다음 **패키지**를 클릭하여 **패키지** 블레이드를 열고, 수정하려는 응용 프로그램 패키지의 행에서 **...(줄임표)**를 클릭하여 수행할 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-232">To update or delete an existing application package, open the details blade for the application, click **Packages** to open the **Packages** blade, click the **ellipsis** in the row of the application package that you want to modify, and select the action that you want to perform.</span></span>

<span data-ttu-id="1c9f8-233">![Azure portal에서 패키지 업데이트 또는 삭제][7]</span><span class="sxs-lookup"><span data-stu-id="1c9f8-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="1c9f8-234">**업데이트**</span><span class="sxs-lookup"><span data-stu-id="1c9f8-234">**Update**</span></span>

<span data-ttu-id="1c9f8-235">**업데이트**를 클릭하면 *패키지 업데이트* 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-235">When you click **Update**, the *Update package* blade is displayed.</span></span> <span data-ttu-id="1c9f8-236">이 블레이드는 *새 응용 프로그램 패키지* 블레이드와 비슷하지만, 패키지 선택 필드만 활성화되므로 업로드할 새 ZIP 파일을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-236">This blade is similar to the *New application package* blade, however only the package selection field is enabled, allowing you to specify a new ZIP file to upload.</span></span>

<span data-ttu-id="1c9f8-237">![Azure portal의 패키지 업데이트 블레이드][11]</span><span class="sxs-lookup"><span data-stu-id="1c9f8-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="1c9f8-238">**삭제**</span><span class="sxs-lookup"><span data-stu-id="1c9f8-238">**Delete**</span></span>

<span data-ttu-id="1c9f8-239">**삭제**를 클릭하면 패키지 버전을 삭제할 것인지 묻는 메시지가 나타나고, Batch가 Azure Storage에서 패키지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-239">When you click **Delete**, you are asked to confirm the deletion of the package version, and Batch deletes the package from Azure Storage.</span></span> <span data-ttu-id="1c9f8-240">응용 프로그램의 기본 버전을 삭제하면 해당 응용 프로그램의 **기본 버전** 설정이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-240">If you delete the default version of an application, the **Default version** setting is removed for the application.</span></span>

<span data-ttu-id="1c9f8-241">![응용 프로그램 삭제][12]</span><span class="sxs-lookup"><span data-stu-id="1c9f8-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="1c9f8-242">계산 노드에 응용 프로그램 설치</span><span class="sxs-lookup"><span data-stu-id="1c9f8-242">Install applications on compute nodes</span></span>
<span data-ttu-id="1c9f8-243">Azure Portal을 사용하여 응용 프로그램 패키지를 관리하는 방법을 살펴보았으며 응용 프로그램 패키지를 계산 노드에 배포하고 Batch 작업을 사용하여 실행하는 방법에 대해 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-243">Now that you've learned how to manage application packages with the Azure portal, we can discuss how to deploy them to compute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="1c9f8-244">풀 응용 프로그램 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="1c9f8-244">Install pool application packages</span></span>
<span data-ttu-id="1c9f8-245">풀의 모든 계산 노드에 응용 프로그램 패키지를 설치하려면 풀에 대해 응용 프로그램 패키지 *참조* 를 하나 이상 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-245">To install an application package on all compute nodes in a pool, specify one or more application package *references* for the pool.</span></span> <span data-ttu-id="1c9f8-246">노드가 풀에 조인되거나 재부팅 또는 이미지로 다시 설치되는 경우 풀에 대해 지정하는 응용 프로그램 패키지는 각 계산 노드에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-246">The application packages that you specify for a pool are installed on each compute node when that node joins the pool, and when the node is rebooted or reimaged.</span></span>

<span data-ttu-id="1c9f8-247">Batch .NET에서, 새 풀을 만들 때 또는 기존 풀에 [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref]를 하나 이상 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="1c9f8-248">[ApplicationPackageReference][net_pkgref] 클래스는 풀의 계산 노드에 설치할 응용 프로그램 ID 및 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-248">The [ApplicationPackageReference][net_pkgref] class specifies an application ID and version to install on a pool's compute nodes.</span></span>

```csharp
// Create the unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify the application and version to install on the compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit the pool so that it's created in the Batch service. As the nodes join
// the pool, the specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="1c9f8-249">어떤 이유로든 응용 프로그램 패키지 배포가 실패하고 Batch 서비스에서 노드를 [사용할 수 없음][net_nodestate]으로 표시하면 해당 노드에서 실행되도록 예약된 작업이 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-249">If an application package deployment fails for any reason, the Batch service marks the node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="1c9f8-250">이 경우에 노드를 **다시 시작** 하여 패키지 배포를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-250">In this case, you should **restart** the node to reinitiate the package deployment.</span></span> <span data-ttu-id="1c9f8-251">또한 노드를 다시 시작하면 노드에서 작업을 다시 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-251">Restarting the node also enables task scheduling again on the node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="1c9f8-252">태스크 응용 프로그램 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="1c9f8-252">Install task application packages</span></span>
<span data-ttu-id="1c9f8-253">풀과 마찬가지로 태스크에 대해 응용 프로그램 패키지 *참조* 를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-253">Similar to a pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="1c9f8-254">노드에서 실행하도록 태스크가 예약된 경우 태스크의 명령줄이 실행되기 바로 전에 패키지가 다운로드 및 추출됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-254">When a task is scheduled to run on a node, the package is downloaded and extracted just before the task's command line is executed.</span></span> <span data-ttu-id="1c9f8-255">지정된 패키지 및 버전이 노드에 이미 설치되어 있는 경우 패키지는 다운로드되지 않으며 기존 패키지가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-255">If a specified package and version is already installed on the node, the package is not downloaded and the existing package is used.</span></span>

<span data-ttu-id="1c9f8-256">태스크 응용 프로그램 패키지를 설치하려면 태스크의 [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-256">To install a task application package, configure the task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-the-installed-applications"></a><span data-ttu-id="1c9f8-257">설치된 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="1c9f8-257">Execute the installed applications</span></span>
<span data-ttu-id="1c9f8-258">풀 또는 태스크에 대해 지정한 패키지가 노드의 `AZ_BATCH_ROOT_DIR` 내에 있는 명명된 디렉터리에 다운로드되어 추출됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-258">The packages that you've specified for a pool or task are downloaded and extracted to a named directory within the `AZ_BATCH_ROOT_DIR` of the node.</span></span> <span data-ttu-id="1c9f8-259">또한 Batch는 명명된 디렉터리에 대한 경로가 포함된 환경 변수를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-259">Batch also creates an environment variable that contains the path to the named directory.</span></span> <span data-ttu-id="1c9f8-260">태스크 명령줄은 노드에서 응용 프로그램을 참조할 때 이 환경 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-260">Your task command lines use this environment variable when referencing the application on the node.</span></span> 

<span data-ttu-id="1c9f8-261">Windows 노드에서는 변수가 다음과 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-261">On Windows nodes, the variable is in the following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="1c9f8-262">Linux 노드에서는 형식이 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-262">On Linux nodes, the format is slightly different.</span></span> <span data-ttu-id="1c9f8-263">마침표(.), 하이픈(-) 및 숫자 기호(#)가 환경 변수에서 밑줄로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-263">Periods (.), hypens (-) and number signs (#) are flattened to underscores in the environment variable.</span></span> <span data-ttu-id="1c9f8-264">예:</span><span class="sxs-lookup"><span data-stu-id="1c9f8-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="1c9f8-265">`APPLICATIONID` 및 `version`은 배포를 위해 지정한 응용 프로그램 및 패키지 버전에 해당하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-265">`APPLICATIONID` and `version` are values that correspond to the application and package version you've specified for deployment.</span></span> <span data-ttu-id="1c9f8-266">예를 들어 Windows 노드에 *blender* 응용 프로그램의 2.7 버전을 설치하도록 지정하면 태스크 명령줄은 다음 환경 변수를 사용하여 해당 파일에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable to access its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="1c9f8-267">Linux 노드에서는 환경 변수를 다음 형식으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-267">On Linux nodes, specify the environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="1c9f8-268">응용 프로그램 패키지를 업로드할 때 계산 노드에 배포할 기본 버전을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-268">When you upload an application package, you can specify a default version to deploy to your compute nodes.</span></span> <span data-ttu-id="1c9f8-269">응용 프로그램의 기본 버전을 지정하면 응용 프로그램 참조 시 버전 접미사를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-269">If you have specified a default version for an application, you can omit the version suffix when you reference the application.</span></span> <span data-ttu-id="1c9f8-270">[응용 프로그램 업로드 및 관리](#upload-and-manage-applications)에서 표시된 것처럼 Azure Portal의 응용 프로그램 블레이드에서 기본 응용 프로그램 버전을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-270">You can specify the default application version in the Azure portal, on the Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="1c9f8-271">예를 들어 *blender* 응용 프로그램에 대해 기본 버전으로 "2.7"을 설정한 경우 태스크가 다음 환경 변수를 참조하면 Windows 노드에서 버전 2.7을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-271">For example, if you set "2.7" as the default version for application *blender*, and your tasks reference the following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="1c9f8-272">다음 코드 조각은 기본 버전의 *blender* 응용 프로그램을 실행하는 태스크 명령줄의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-272">The following code snippet shows an example task command line that launches the default version of the *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="1c9f8-273">계산 노드 환경 설정에 대한 자세한 내용은 [Batch 기능 개요](batch-api-basics.md)의 [태스크 환경 설정](batch-api-basics.md#environment-settings-for-tasks)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in the [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="1c9f8-274">풀의 응용 프로그램 패키지 업데이트</span><span class="sxs-lookup"><span data-stu-id="1c9f8-274">Update a pool's application packages</span></span>
<span data-ttu-id="1c9f8-275">기존 풀이 이미 응용 프로그램 패키지를 통해 구성된 경우 해당 풀에 대해 새 패키지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-275">If an existing pool has already been configured with an application package, you can specify a new package for the pool.</span></span> <span data-ttu-id="1c9f8-276">풀에 대한 새 패키지 참조를 지정하면 다음이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-276">If you specify a new package reference for a pool, the following apply:</span></span>

* <span data-ttu-id="1c9f8-277">Batch 서비스는 풀에 조인하는 모든 새 노드와 다시 부팅되거나 이미지로 다시 설치되는 기존 노드에 새로 지정된 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-277">The Batch service installs the newly specified package on all new nodes that join the pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="1c9f8-278">패키지 참조를 업데이트할 때 이미 풀에 있는 계산 노드는 새 응용 프로그램 패키지를 자동으로 설치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-278">Compute nodes that are already in the pool when you update the package references do not automatically install the new application package.</span></span> <span data-ttu-id="1c9f8-279">이러한 계산 노드를 재부팅하거나 이미지로 다시 설치하여 새 패키지를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-279">These compute nodes must be rebooted or reimaged to receive the new package.</span></span>
* <span data-ttu-id="1c9f8-280">새 패키지가 배포될 때 만들어진 환경 변수는 새 응용 프로그램 패키지 참조를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-280">When a new package is deployed, the created environment variables reflect the new application package references.</span></span>

<span data-ttu-id="1c9f8-281">이 예에서는 기존 풀의 *blender* 응용 프로그램 2.7 버전이 [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] 중 하나로 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-281">In this example, the existing pool has version 2.7 of the *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="1c9f8-282">풀의 노드를 2.76b 버전으로 업데이트하려면 새 버전을 사용하여 [ApplicationPackageReference][net_pkgref]를 지정하고 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-282">To update the pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with the new version, and commit the change.</span></span>

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

<span data-ttu-id="1c9f8-283">새 버전이 구성되었으므로 Batch 서비스는 풀에 조인하는 모든 *새* 노드에 2.76b 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-283">Now that the new version has been configured, the Batch service installs version 2.76b to any *new* node that joins the pool.</span></span> <span data-ttu-id="1c9f8-284">*이미* 풀에 있는 노드에 2.76b 버전을 설치하려면 노드를 재부팅하거나 이미지로 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-284">To install 2.76b on the nodes that are *already* in the pool, reboot or reimage them.</span></span> <span data-ttu-id="1c9f8-285">다시 부팅된 노드는 이전 패키지 배포의 파일을 보존합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-285">Note that rebooted nodes retain the files from previous package deployments.</span></span>

## <a name="list-the-applications-in-a-batch-account"></a><span data-ttu-id="1c9f8-286">Batch 계정의 응용 프로그램 나열</span><span class="sxs-lookup"><span data-stu-id="1c9f8-286">List the applications in a Batch account</span></span>
<span data-ttu-id="1c9f8-287">[ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] 메서드를 사용하여 Batch 계정의 응용 프로그램 및 응용 프로그램 패키지를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-287">You can list the applications and their packages in a Batch account by using the [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List the applications and their application packages in the Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a><span data-ttu-id="1c9f8-288">마무리</span><span class="sxs-lookup"><span data-stu-id="1c9f8-288">Wrap up</span></span>
<span data-ttu-id="1c9f8-289">응용 프로그램 패키지를 사용하면 고객이 작업에 대한 응용 프로그램을 선택하고 Batch 지원 서비스를 통해 작업을 처리할 때 사용할 정확한 버전을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-289">With application packages, you can help your customers select the applications for their jobs and specify the exact version to use when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="1c9f8-290">또한 고객이 서비스에서 자신의 고유한 응용 프로그램을 업로드 및 추적하는 기능을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-290">You might also provide the ability for your customers to upload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c9f8-291">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1c9f8-291">Next steps</span></span>
* <span data-ttu-id="1c9f8-292">또한 [Batch REST API][api_rest]는 응용 프로그램 패키지로 작업하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-292">The [Batch REST API][api_rest] also provides support to work with application packages.</span></span> <span data-ttu-id="1c9f8-293">예를 들어 REST API를 사용하여 설치할 패키지를 지정하는 방법에 대한 자세한 내용은 [계정에 풀 추가][rest_add_pool]에서 [applicationPackageReferences][rest_add_pool_with_packages] 요소를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-293">For example, see the [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool to an account][rest_add_pool] for information about how to specify packages to install by using the REST API.</span></span> <span data-ttu-id="1c9f8-294">Batch REST API를 사용하여 응용 프로그램 정보를 얻는 방법에 대한 자세한 내용은 [응용 프로그램][rest_applications]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-294">See [Applications][rest_applications] for details about how to obtain application information by using the Batch REST API.</span></span>
* <span data-ttu-id="1c9f8-295">프로그래밍 방식으로 [Batch 관리 .NET으로 Azure Batch 계정 및 할당량 관리](batch-management-dotnet.md)를 수행하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-295">Learn how to programmatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="1c9f8-296">[Batch 관리.NET][api_net_mgmt] 라이브러리는 Batch 응용 프로그램 또는 서비스에 대한 계정 만들기 및 삭제 기능을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c9f8-296">The [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "응용 프로그램 패키지에 대한 개략적인 다이어그램"
[2]: ./media/batch-application-packages/app_pkg_02.png "Azure portal의 응용 프로그램 타일"
[3]: ./media/batch-application-packages/app_pkg_03.png "Azure portal의 응용 프로그램 블레이드"
[4]: ./media/batch-application-packages/app_pkg_04.png "Azure portal의 응용 프로그램 세부 정보 블레이드"
[5]: ./media/batch-application-packages/app_pkg_05.png "Azure portal의 새 응용 프로그램 블레이드"
[7]: ./media/batch-application-packages/app_pkg_07.png "Azure portal의 패키지 업데이트 또는 삭제 드롭다운"
[8]: ./media/batch-application-packages/app_pkg_08.png "Azure portal의 새 응용 프로그램 패키지 블레이드"
[9]: ./media/batch-application-packages/app_pkg_09.png "연결된 저장소 계정 없음 경고"
[10]: ./media/batch-application-packages/app_pkg_10.png "포털에서 저장소 계정 블레이드 선택"
[11]: ./media/batch-application-packages/app_pkg_11.png "Azure portal의 패키지 업데이트 블레이드"
[12]: ./media/batch-application-packages/app_pkg_12.png "Azure portal의 패키지 삭제 확인 대화 상자"
