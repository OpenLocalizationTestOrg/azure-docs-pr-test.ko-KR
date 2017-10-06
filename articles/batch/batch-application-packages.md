---
title: "계산 노드의-Azure 배치 aaaInstall 응용 프로그램 패키지 | Microsoft Docs"
description: "일괄 처리에는 설치에 대 한 버전 계산 노드 및 Azure 배치 tooeasily의 hello 응용 프로그램 패키지 기능 사용 하 여 여러 응용 프로그램을 관리 합니다."
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
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a><span data-ttu-id="bada9-103">일괄 처리 응용 프로그램 패키지와 응용 프로그램 toocompute 노드 배포</span><span class="sxs-lookup"><span data-stu-id="bada9-103">Deploy applications toocompute nodes with Batch application packages</span></span>

<span data-ttu-id="bada9-104">해당 배포 toohello 계산 풀의 노드 및 Azure 일괄 처리의 hello 응용 프로그램 패키지 기능 작업 응용 프로그램을 쉽게 관리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-104">hello application packages feature of Azure Batch provides easy management of task applications and their deployment toohello compute nodes in your pool.</span></span> <span data-ttu-id="bada9-105">응용 프로그램 패키지와 업로드 하 고 지원 파일 포함 하 여 작업을 실행 하는 hello 응용 프로그램의 여러 버전을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-105">With application packages, you can upload and manage multiple versions of hello applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="bada9-106">자동으로 배포할 수 하나 또는 이러한 응용 프로그램 toohello 중 계산 풀의 노드.</span><span class="sxs-lookup"><span data-stu-id="bada9-106">You can then automatically deploy one or more of these applications toohello compute nodes in your pool.</span></span>

<span data-ttu-id="bada9-107">이 문서에서는 살펴보겠습니다 어떻게 tooupload hello Azure 포털에서에서 응용 프로그램 패키지를 관리 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-107">In this article, you will learn how tooupload and manage application packages in hello Azure portal.</span></span> <span data-ttu-id="bada9-108">배웁니다 어떻게 tooinstall에 풀의 계산 노드를 hello [일괄 처리.NET] [ api_net] 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-108">You will then learn how tooinstall them on a pool's compute nodes with hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="bada9-109">응용 프로그램 패키지는 2017년 7월 5일 이후에 만들어진 모든 Batch 풀에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="bada9-110">클라우드 서비스 구성을 사용 하 여 hello 풀이 작성 되었습니다. 경우에 10 2016 년 3 월 사이의 5 년 7 월 2017 생성 되는 일괄 처리 풀에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="bada9-111">2016 년 3 월 이전 too10를 생성 하는 일괄 처리 풀에서 응용 프로그램 패키지를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-111">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="bada9-112">hello 만들고 응용 프로그램 패키지를 관리 하기 위한 Api의 일부인 hello [Batch Management.NET] [[api_net_mgmt]] 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-112">hello APIs for creating and managing application packages are part of hello [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="bada9-113">hello 계산 노드에서 응용 프로그램 패키지를 설치 하기 위한 Api의 일부인 hello [일괄 처리.NET] [ api_net] 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-113">hello APIs for installing application packages on a compute node are part of hello [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="bada9-114">여기에 설명 된 hello 응용 프로그램 패키지 기능에는 이전 버전의 hello 서비스에서 사용할 수 있는 hello 배치 앱 기능 보다 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-114">hello application packages feature described here supersedes hello Batch Apps feature available in previous versions of hello service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="bada9-115">응용 프로그램 패키지 요구 사항</span><span class="sxs-lookup"><span data-stu-id="bada9-115">Application package requirements</span></span>
<span data-ttu-id="bada9-116">toouse 응용 프로그램 패키지가 필요한 너무[Azure 저장소 계정 연결](#link-a-storage-account) tooyour 일괄 처리 계정.</span><span class="sxs-lookup"><span data-stu-id="bada9-116">toouse application packages, you need too[link an Azure Storage account](#link-a-storage-account) tooyour Batch account.</span></span>

<span data-ttu-id="bada9-117">이 기능에 도입 된 [배치 REST API] [ api_rest] 버전 2015-12-01.2.2 및 hello 해당 [일괄 처리.NET] [ api_net] 라이브러리 버전 3.1.0 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and hello corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="bada9-118">일괄 처리와 작업 하는 경우에 항상 hello 최신 API 버전을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-118">We recommend that you always use hello latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="bada9-119">응용 프로그램 패키지는 2017년 7월 5일 이후에 만들어진 모든 Batch 풀에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="bada9-120">클라우드 서비스 구성을 사용 하 여 hello 풀이 작성 되었습니다. 경우에 10 2016 년 3 월 사이의 5 년 7 월 2017 생성 되는 일괄 처리 풀에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="bada9-121">2016 년 3 월 이전 too10를 생성 하는 일괄 처리 풀에서 응용 프로그램 패키지를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-121">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="bada9-122">응용 프로그램 및 응용 프로그램 패키지 정보</span><span class="sxs-lookup"><span data-stu-id="bada9-122">About applications and application packages</span></span>
<span data-ttu-id="bada9-123">Azure 일괄 처리 내에서 한 *응용 프로그램* tooa 버전이 지정 된 이진 파일 집합을 통해 풀에서 자동으로 다운로드 한 toohello 계산 노드 수 있는 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-123">Within Azure Batch, an *application* refers tooa set of versioned binaries that can be automatically downloaded toohello compute nodes in your pool.</span></span> <span data-ttu-id="bada9-124">*응용 프로그램 패키지* tooa 참조 *특정 집합* 이진 파일 및 나타냅니다는 주어진 *버전* hello 응용 프로그램의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-124">An *application package* refers tooa *specific set* of those binaries and represents a given *version* of hello application.</span></span>

<span data-ttu-id="bada9-125">![응용 프로그램 및 응용 프로그램 패키지에 대한 개략적인 다이어그램][1]</span><span class="sxs-lookup"><span data-stu-id="bada9-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="bada9-126">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="bada9-126">Applications</span></span>
<span data-ttu-id="bada9-127">일괄 처리에서 응용 프로그램 하나를 포함 하거나 더 많은 응용 프로그램 패키지와 hello 응용 프로그램에 대 한 구성 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-127">An application in Batch contains one or more application packages and specifies configuration options for hello application.</span></span> <span data-ttu-id="bada9-128">예를 들어 응용 프로그램에 계산 노드 및 해당 패키지 업데이트 하거나 삭제할 수 있는지 여부 hello 기본 응용 프로그램 패키지 버전 tooinstall를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-128">For example, an application can specify hello default application package version tooinstall on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="bada9-129">응용 프로그램 패키지</span><span class="sxs-lookup"><span data-stu-id="bada9-129">Application packages</span></span>
<span data-ttu-id="bada9-130">응용 프로그램 패키지는 hello 응용 프로그램 이진 파일을 포함 하는.zip 파일 및 작업 toorun hello 응용 프로그램에 필요한 지원 파일에는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-130">An application package is a .zip file that contains hello application binaries and supporting files that are required for your tasks toorun hello application.</span></span> <span data-ttu-id="bada9-131">각 응용 프로그램 패키지 hello 응용 프로그램의 특정 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-131">Each application package represents a specific version of hello application.</span></span>

<span data-ttu-id="bada9-132">Hello 풀 및 작업 수준에서 응용 프로그램 패키지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-132">You can specify application packages at hello pool and task levels.</span></span> <span data-ttu-id="bada9-133">풀 또는 태스크를 만들 때 이러한 패키지 및 버전(선택 사항)을 하나 이상 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="bada9-134">**응용 프로그램 패키지 풀** 너무 배포*모든* hello 풀에서 노드.</span><span class="sxs-lookup"><span data-stu-id="bada9-134">**Pool application packages** are deployed too*every* node in hello pool.</span></span> <span data-ttu-id="bada9-135">응용 프로그램은 노드가 풀을 조인하고 재부팅되거나 이미지를 다시 설치할 때 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="bada9-136">풀 응용 프로그램 패키지는 풀에 있는 모든 노드가 작업의 태스크를 실행할 때 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="bada9-137">풀을 만들 때 하나 이상의 응용 프로그램 패키지를 지정할 수 있으며 기존 풀의 패키지를 추가하거나 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="bada9-138">기존 풀의 응용 프로그램 패키지를 업데이트 하면 해당 노드 tooinstall hello 새 패키지를 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-138">If you update an existing pool's application packages, you must restart its nodes tooinstall hello new package.</span></span>
* <span data-ttu-id="bada9-139">**응용 프로그램 패키지 작업** tooa 계산 노드 예약 toorun 작업 hello 작업의 명령줄을 실행 하기 직전에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-139">**Task application packages** are deployed only tooa compute node scheduled toorun a task, just before running hello task's command line.</span></span> <span data-ttu-id="bada9-140">Hello 지정 된 응용 프로그램 패키지 및 버전에 표시 되어 hello 노드, 다시 배포 되지 않습니다 및 hello 기존 패키지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-140">If hello specified application package and version is already on hello node, it is not redeployed and hello existing package is used.</span></span>
  
    <span data-ttu-id="bada9-141">작업 응용 프로그램 패키지는 다른 작업 한 풀에서 실행 되 고 작업이 완료 되 면 hello 풀 삭제 되지 않습니다 공유 풀 환경에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and hello pool is not deleted when a job is completed.</span></span> <span data-ttu-id="bada9-142">작업에 hello 풀 노드 보다 적은 작업 인 작업 응용 프로그램 패키지 응용 프로그램 작업을 실행 하는 배포 된 유일한 toohello 노드 이므로 데이터 전송을 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-142">If your job has fewer tasks than nodes in hello pool, task application packages can minimize data transfer since your application is deployed only toohello nodes that run tasks.</span></span>
  
    <span data-ttu-id="bada9-143">태스크 응용 프로그램 패키지를 활용할 수 있는 다른 시나리오는 큰 응용 프로그램을 실행하지만 태스크 수는 적은 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="bada9-144">예를 들어 전 전처리 단계 또는 hello 전처리 또는 병합 응용 프로그램 인 중량 병합 작업은 작업 응용 프로그램 패키지를 사용 하 여 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-144">For example, a pre-processing stage or a merge task, where hello pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bada9-145">hello 최대 응용 프로그램 패키지 크기와 응용 프로그램 및 일괄 처리 계정 내에서 응용 프로그램 패키지의 hello 수에 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-145">There are restrictions on hello number of applications and application packages within a Batch account and on hello maximum application package size.</span></span> <span data-ttu-id="bada9-146">참조 [할당량과 hello Azure 배치 서비스에 대 한 제한을](batch-quota-limit.md) 이러한 제한에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-146">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="bada9-147">응용 프로그램 패키지의 이점</span><span class="sxs-lookup"><span data-stu-id="bada9-147">Benefits of application packages</span></span>
<span data-ttu-id="bada9-148">응용 프로그램 패키지는 일괄 처리 솔루션 및 작업을 실행 하는 낮은 hello 오버 헤드가 필요한 toomanage hello 응용 프로그램의 hello 코드를 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-148">Application packages can simplify hello code in your Batch solution and lower hello overhead required toomanage hello applications that your tasks run.</span></span>

<span data-ttu-id="bada9-149">응용 프로그램 패키지와 풀의 시작 작업 없는 toospecify 개별 리소스 파일 tooinstall 목록이 긴 hello 노드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-149">With application packages, your pool's start task doesn't have toospecify a long list of individual resource files tooinstall on hello nodes.</span></span> <span data-ttu-id="bada9-150">노드 또는 Azure 저장소에서 응용 프로그램 파일의 여러 버전을 관리 하는 toomanually가 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-150">You don't have toomanually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="bada9-151">Tooworry 생성에 대 한 필요 하지 않습니다 [SAS Url](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide toohello 파일 저장소 계정에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-151">And, you don't need tooworry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide access toohello files in your Storage account.</span></span> <span data-ttu-id="bada9-152">Azure 저장소 toostore 응용 프로그램 패키지와 hello 백그라운드에서 작업 일괄 처리 및 toocompute 노드를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-152">Batch works in hello background with Azure Storage toostore application packages and deploy them toocompute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="bada9-153">hello 시작 태스크의 총 크기 해야 보다 작거나 같은 too32768 문자를 리소스 파일 및 환경 변수를 포함 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-153">hello total size of a start task must be less than or equal too32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="bada9-154">시작 태스크가 이 제한을 초과하는 경우 응용 프로그램 패키지 사용은 또 다른 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="bada9-155">리소스 파일을 포함 하는 압축 된 보관 파일을 만들 수도 blob tooAzure 저장소로 업로드 한 후 압축을 풀고 hello 시작 태스크의 명령줄에서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-155">You can also create a zipped archive containing your resource files, upload it as a blob tooAzure Storage, and then unzip it from hello command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="bada9-156">응용 프로그램 업로드 및 관리</span><span class="sxs-lookup"><span data-stu-id="bada9-156">Upload and manage applications</span></span>
<span data-ttu-id="bada9-157">Hello를 사용할 수 있습니다 [Azure 포털] [ portal] 또는 hello [Batch Management.NET](batch-management-dotnet.md) 일괄 처리 계정에 라이브러리 toomanage hello 응용 프로그램 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-157">You can use hello [Azure portal][portal] or hello [Batch Management .NET](batch-management-dotnet.md) library toomanage hello application packages in your Batch account.</span></span> <span data-ttu-id="bada9-158">몇 개 섹션 hello 옆에서, 어떻게 toolink 저장소 계정에는 다음 추가 응용 프로그램 설명 및 패키지 및 관리를 사용 하 여 hello 포털 처음 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-158">In hello next few sections, we first show how toolink a Storage account, then discuss adding applications and packages and managing them with hello portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="bada9-159">저장소 계정 연결</span><span class="sxs-lookup"><span data-stu-id="bada9-159">Link a Storage account</span></span>
<span data-ttu-id="bada9-160">toouse 응용 프로그램 패키지를 먼저 Azure 저장소 계정 tooyour 일괄 처리 계정을 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-160">toouse application packages, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="bada9-161">저장소 계정을 아직 구성 하지 않은 경우 hello Azure 포털에 표시 됩니다 경고 hello 처음 hello를 클릭 하면 **응용 프로그램** hello에 바둑판식으로 배열 **일괄 처리 계정을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-161">If you have not yet configured a Storage account, hello Azure portal displays a warning hello first time you click hello **Applications** tile in hello **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bada9-162">에서는 현재 일괄 처리 *만* hello **범용** 5 단계에 설명 된 대로 저장소 계정 유형은 [저장소 계정을 만드는](../storage/common/storage-create-storage-account.md#create-a-storage-account)에 [에 대 한 Azure 저장소 계정](../storage/common/storage-create-storage-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-162">Batch currently supports *only* hello **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="bada9-163">Azure 저장소 계정 tooyour 일괄 처리 계정에 연결 하면 연결 *만* 는 **범용** 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-163">When you link an Azure Storage account tooyour Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="bada9-164">![Azure Portal의 '저장소 계정이 구성되지 않음' 경고][9]</span><span class="sxs-lookup"><span data-stu-id="bada9-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="bada9-165">hello 일괄 처리 서비스는 hello 연결 된 저장소 계정 toostore 응용 프로그램 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-165">hello Batch service uses hello associated Storage account toostore your application packages.</span></span> <span data-ttu-id="bada9-166">Hello 두 개의 계정을 연결 일괄 처리는 hello 연결 된 저장소 계정 tooyour 계산 노드에 저장 된 hello 패키지를 자동으로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-166">After you've linked hello two accounts, Batch can automatically deploy hello packages stored in hello linked Storage account tooyour compute nodes.</span></span> <span data-ttu-id="bada9-167">저장소 계정 tooyour 일괄 처리 계정 toolink 클릭 **저장소 계정 설정을** hello에 **경고** 블레이드에서 하 고 클릭 한 다음 **저장소 계정** hello에**저장소 계정** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-167">toolink a Storage account tooyour Batch account, click **Storage account settings** on hello **Warning** blade, and then click **Storage Account** on hello **Storage Account** blade.</span></span>

<span data-ttu-id="bada9-168">![Azure portal에서 저장소 계정 블레이드 선택][10]</span><span class="sxs-lookup"><span data-stu-id="bada9-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="bada9-169">*특별히* Batch 계정과 함께 사용할 저장소 계정을 만들었으면 여기에서 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="bada9-170">방법에 대 한 세부 정보에 대 한 저장소 계정을 toocreate "저장소 계정 만들기"의 참조 [에 대 한 Azure 저장소 계정](../storage/common/storage-create-storage-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-170">For details about how toocreate a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="bada9-171">저장소 계정을 만든 후 다음을 연결할 수 있습니다 일괄 처리 계정 tooyour hello를 사용 하 여 **저장소 계정** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-171">After you've created a Storage account, you can then link it tooyour Batch account by using hello **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="bada9-172">hello 일괄 처리 서비스 블록 blob으로 Azure 저장소 toostore 응용 프로그램 패키지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-172">hello Batch service uses Azure Storage toostore your application packages as block blobs.</span></span> <span data-ttu-id="bada9-173">[정상적으로 청구] [ storage_pricing] hello 블록 blob 데이터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-173">You are [charged as normal][storage_pricing] for hello block blob data.</span></span> <span data-ttu-id="bada9-174">응용 프로그램 패키지의 있는지 tooconsider hello 크기 및 개수 되어 사용 되지 않는 패키지 toominimize 비용을 주기적으로 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-174">Be sure tooconsider hello size and number of your application packages, and periodically remove deprecated packages toominimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="bada9-175">현재 응용 프로그램 보기</span><span class="sxs-lookup"><span data-stu-id="bada9-175">View current applications</span></span>
<span data-ttu-id="bada9-176">일괄 처리 계정에 tooview hello 응용 프로그램 클릭 hello **응용 프로그램** hello를 보는 동안 hello 왼쪽된 메뉴에 메뉴 항목 **일괄 처리 계정을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-176">tooview hello applications in your Batch account, click hello **Applications** menu item in hello left menu while viewing hello **Batch account** blade.</span></span>

<span data-ttu-id="bada9-177">![응용 프로그램 타일][2]</span><span class="sxs-lookup"><span data-stu-id="bada9-177">![Applications tile][2]</span></span>

<span data-ttu-id="bada9-178">이 메뉴 옵션을 선택 하면 열립니다 hello **응용 프로그램** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="bada9-178">Selecting this menu option opens hello **Applications** blade:</span></span>

<span data-ttu-id="bada9-179">![응용 프로그램 나열][3]</span><span class="sxs-lookup"><span data-stu-id="bada9-179">![List applications][3]</span></span>

<span data-ttu-id="bada9-180">hello **응용 프로그램** 계정에 각 응용 프로그램의 ID를 hello 및 다음과 같은 속성 hello 블레이드 표시:</span><span class="sxs-lookup"><span data-stu-id="bada9-180">hello **Applications** blade displays hello ID of each application in your account and hello following properties:</span></span>

* <span data-ttu-id="bada9-181">**패키지**: hello이 응용 프로그램과 관련 된 버전의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-181">**Packages**: hello number of versions associated with this application.</span></span>
* <span data-ttu-id="bada9-182">**기본 버전**: hello 응용 프로그램 버전 hello 응용 프로그램 풀을 지정 하는 경우 버전이 표시 되지 않은 경우 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-182">**Default version**: hello application version installed if you do not indicate a version when you specify hello application for a pool.</span></span> <span data-ttu-id="bada9-183">이 설정은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-183">This setting is optional.</span></span>
* <span data-ttu-id="bada9-184">**업데이트 허용**: 여부 패키지 업데이트, 삭제 및 추가 기능을 지정 하는 hello 값이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-184">**Allow updates**: hello value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="bada9-185">이 너무 설정 되어 있으면**아니요**, 패키지 업데이트 및 삭제 hello 응용 프로그램에 대해 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-185">If this is set too**No**, package updates and deletions are disabled for hello application.</span></span> <span data-ttu-id="bada9-186">새 응용 프로그램 패키지 버전만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-186">Only new application package versions can be added.</span></span> <span data-ttu-id="bada9-187">hello 기본값은 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-187">hello default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="bada9-188">응용 프로그램 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="bada9-188">View application details</span></span>
<span data-ttu-id="bada9-189">hello에서 응용 프로그램을 선택 하는 hello 응용 프로그램에 대 한 hello 세부 정보를 포함 하는 tooopen hello 블레이드 **응용 프로그램** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-189">tooopen hello blade that includes hello details for an application, select hello application in hello **Applications** blade.</span></span>

<span data-ttu-id="bada9-190">![응용 프로그램 세부 정보][4]</span><span class="sxs-lookup"><span data-stu-id="bada9-190">![Application details][4]</span></span>

<span data-ttu-id="bada9-191">Hello 응용 프로그램 세부 정보 블레이드에서 hello 다음 응용 프로그램에 대 한 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-191">In hello application details blade, you can configure hello following settings for your application.</span></span>

* <span data-ttu-id="bada9-192">**업데이트 허용**: 해당 응용 프로그램 패키지를 업데이트하거나 삭제할 수 있는지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="bada9-193">이 문서에서 아래의 "응용 프로그램 패키지 업데이트 또는 삭제"를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bada9-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="bada9-194">**기본 버전**: 기본 응용 프로그램 패키지 toodeploy toocompute 노드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-194">**Default version**: Specify a default application package toodeploy toocompute nodes.</span></span>
* <span data-ttu-id="bada9-195">**표시 이름**: 솔루션 hello 일괄 처리를 통해 tooyour 고객을 제공 하는 서비스의 UI에서에서 예를 들어 hello 응용 프로그램에 대 한 정보를 표시할 때 사용할 수 있습니다 일괄 처리는 친숙 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about hello application, for example, in hello UI of a service that you provide tooyour customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="bada9-196">새 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="bada9-196">Add a new application</span></span>
<span data-ttu-id="bada9-197">응용 프로그램 패키지를 추가 하 고 고유한 새 응용 프로그램 ID를 지정 하는 toocreate 새 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="bada9-197">toocreate a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="bada9-198">hello 새 응용 프로그램 ID로 추가 하는 hello 첫 번째 응용 프로그램 패키지는 또한 hello 새 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-198">hello first application package that you add with hello new application ID also creates hello new application.</span></span>

<span data-ttu-id="bada9-199">클릭 **추가** hello에 **응용 프로그램** 블레이드 tooopen hello **새 응용 프로그램** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-199">Click **Add** on hello **Applications** blade tooopen hello **New application** blade.</span></span>

<span data-ttu-id="bada9-200">![Azure portal의 새 응용 프로그램 블레이드][5]</span><span class="sxs-lookup"><span data-stu-id="bada9-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="bada9-201">hello **새 응용 프로그램** 블레이드 hello 다음 새 응용 프로그램 및 응용 프로그램 패키지의 toospecify hello 설정을 필드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-201">hello **New application** blade provides hello following fields toospecify hello settings of your new application and application package.</span></span>

<span data-ttu-id="bada9-202">**응용 프로그램 ID**</span><span class="sxs-lookup"><span data-stu-id="bada9-202">**Application id**</span></span>

<span data-ttu-id="bada9-203">이 필드는 제목 toohello 표준 Azure 일괄 처리 ID 유효성 검사 규칙은 새 응용 프로그램의 hello ID를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-203">This field specifies hello ID of your new application, which is subject toohello standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="bada9-204">응용 프로그램 ID를 제공 하는 데 hello 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-204">hello rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="bada9-205">Windows 노드에서 hello ID 조합을 영숫자, 하이픈 및 밑줄만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-205">On Windows nodes, hello ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="bada9-206">Linux 노드에서는 영숫자와 밑줄만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="bada9-207">포함할 수 있는 최대 문자는 64자입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="bada9-208">Hello 일괄 처리 계정 내에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-208">Must be unique within hello Batch account.</span></span>
* <span data-ttu-id="bada9-209">대/소문자를 유지하고 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="bada9-210">**버전**</span><span class="sxs-lookup"><span data-stu-id="bada9-210">**Version**</span></span>

<span data-ttu-id="bada9-211">이 필드의 hello 응용 프로그램 패키지를 업로드 하는 hello 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-211">This field specifies hello version of hello application package you are uploading.</span></span> <span data-ttu-id="bada9-212">버전 문자열은 유효성 검사 규칙에 따라 주체 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-212">Version strings are subject toohello following validation rules:</span></span>

* <span data-ttu-id="bada9-213">Windows 노드에서 hello 버전 문자열에는 영숫자, 하이픈, 밑줄 및 마침표의 조합을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-213">On Windows nodes, hello version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="bada9-214">Linux 노드에 hello 버전 문자열 영숫자 문자와 밑줄을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-214">On Linux nodes, hello version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="bada9-215">포함할 수 있는 최대 문자는 64자입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="bada9-216">Hello 응용 프로그램 내에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-216">Must be unique within hello application.</span></span>
* <span data-ttu-id="bada9-217">대/소문자를 유지하고 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="bada9-218">**응용 프로그램 패키지**</span><span class="sxs-lookup"><span data-stu-id="bada9-218">**Application package**</span></span>

<span data-ttu-id="bada9-219">이 필드는 hello 응용 프로그램 이진 파일을 포함 하는 hello.zip 파일 및 필요한 tooexecute hello 응용 프로그램과 된 지원 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-219">This field specifies hello .zip file that contains hello application binaries and supporting files that are required tooexecute hello application.</span></span> <span data-ttu-id="bada9-220">Hello 클릭 **파일 선택** 상자나 hello 폴더 아이콘 toobrowse tooand 응용 프로그램의 파일이 포함 된.zip 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-220">Click hello **Select a file** box or hello folder icon toobrowse tooand select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="bada9-221">파일을 선택한 후 클릭 **확인** toobegin hello 업로드 tooAzure 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-221">After you've selected a file, click **OK** toobegin hello upload tooAzure Storage.</span></span> <span data-ttu-id="bada9-222">Hello 업로드 작업이 완료 되 면 hello 포털 알림을 표시 하 고 hello 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-222">When hello upload operation is complete, hello portal displays a notification and closes hello blade.</span></span> <span data-ttu-id="bada9-223">업로드 하 고 hello 네트워크 연결 속도 hello 파일의 hello 크기에 따라이 작업에는 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-223">Depending on hello size of hello file that you are uploading and hello speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="bada9-224">Hello를 닫지 마십시오 **새 응용 프로그램** 블레이드 hello 업로드 작업이 완료 되기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-224">Do not close hello **New application** blade before hello upload operation is complete.</span></span> <span data-ttu-id="bada9-225">이렇게 하면 hello 업로드 프로세스가 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-225">Doing so will stop hello upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="bada9-226">새 응용 프로그램 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="bada9-226">Add a new application package</span></span>
<span data-ttu-id="bada9-227">hello에 응용 프로그램을 선택 하는 기존 응용 프로그램에 대 한 새 응용 프로그램 패키지 버전 tooadd **응용 프로그램** 블레이드에서 클릭 **패키지**, 클릭 **추가** tooopen hello **패키지 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-227">tooadd a new application package version for an existing application, select an application in hello **Applications** blade, click **Packages**, then click **Add** tooopen hello **Add package** blade.</span></span>

<span data-ttu-id="bada9-228">![Azure portal의 응용 프로그램 패키지 추가 블레이드][8]</span><span class="sxs-lookup"><span data-stu-id="bada9-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="bada9-229">Hello 필드가 hello의 인수와 일치 하는 볼 수 있듯이 **새 응용 프로그램** 블레이드에서 하지만 hello **응용 프로그램 id** 상자는 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-229">As you can see, hello fields match those of hello **New application** blade, but hello **Application id** box is disabled.</span></span> <span data-ttu-id="bada9-230">Hello 새 응용 프로그램에 대해 수행한 것 처럼 지정 hello **버전** 새 패키지에 대 한 찾아보기 tooyour **응용 프로그램 패키지** .zip 파일을 다음 클릭 **확인** tooupload hello 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-230">As you did for hello new application, specify hello **Version** for your new package, browse tooyour **Application package** .zip file, then click **OK** tooupload hello package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="bada9-231">응용 프로그램 패키지 업데이트 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="bada9-231">Update or delete an application package</span></span>
<span data-ttu-id="bada9-232">기존 응용 프로그램 패키지를 열고 hello 세부 정보 블레이드에서 hello 응용 프로그램에 대 한 클릭 tooupdate 또는 delete **패키지** tooopen hello **패키지** 블레이드에서 hello 클릭 **줄임표**tooperform 원하는 hello 작업을 선택 하 고 toomodify를 지정 하는 hello 응용 프로그램 패키지의 hello 행에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-232">tooupdate or delete an existing application package, open hello details blade for hello application, click **Packages** tooopen hello **Packages** blade, click hello **ellipsis** in hello row of hello application package that you want toomodify, and select hello action that you want tooperform.</span></span>

<span data-ttu-id="bada9-233">![Azure portal에서 패키지 업데이트 또는 삭제][7]</span><span class="sxs-lookup"><span data-stu-id="bada9-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="bada9-234">**업데이트**</span><span class="sxs-lookup"><span data-stu-id="bada9-234">**Update**</span></span>

<span data-ttu-id="bada9-235">클릭할 때 **업데이트**, hello *업데이트 패키지* 블레이드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-235">When you click **Update**, hello *Update package* blade is displayed.</span></span> <span data-ttu-id="bada9-236">이 블레이드는 비슷한 toohello *새 응용 프로그램 패키지* 블레이드에서 있지만 hello 패키지 선택 필드를 사용할 새로운 ZIP 파일 tooupload toospecify 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-236">This blade is similar toohello *New application package* blade, however only hello package selection field is enabled, allowing you toospecify a new ZIP file tooupload.</span></span>

<span data-ttu-id="bada9-237">![Azure portal의 패키지 업데이트 블레이드][11]</span><span class="sxs-lookup"><span data-stu-id="bada9-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="bada9-238">**삭제**</span><span class="sxs-lookup"><span data-stu-id="bada9-238">**Delete**</span></span>

<span data-ttu-id="bada9-239">클릭할 때 **삭제**tooconfirm hello 삭제 hello 패키지 버전 요청, 및 일괄 처리를 Azure 저장소에서에서 hello 패키지를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-239">When you click **Delete**, you are asked tooconfirm hello deletion of hello package version, and Batch deletes hello package from Azure Storage.</span></span> <span data-ttu-id="bada9-240">응용 프로그램의 hello 기본 버전을 삭제 하면 hello **기본 버전** hello 응용 프로그램에 대 한 설정이 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-240">If you delete hello default version of an application, hello **Default version** setting is removed for hello application.</span></span>

<span data-ttu-id="bada9-241">![응용 프로그램 삭제][12]</span><span class="sxs-lookup"><span data-stu-id="bada9-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="bada9-242">계산 노드에 응용 프로그램 설치</span><span class="sxs-lookup"><span data-stu-id="bada9-242">Install applications on compute nodes</span></span>
<span data-ttu-id="bada9-243">Azure 포털 hello로 toomanage 응용 프로그램을 패키지 하는 방법을 배운, 했으므로 논의할 수 어떻게 toodeploy toocompute 노드에 해당 하 여 일괄 처리 작업으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-243">Now that you've learned how toomanage application packages with hello Azure portal, we can discuss how toodeploy them toocompute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="bada9-244">풀 응용 프로그램 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="bada9-244">Install pool application packages</span></span>
<span data-ttu-id="bada9-245">모든 응용 프로그램 패키지 tooinstall 풀의 계산 노드, 응용 프로그램 패키지를 하나 이상 지정 *참조* hello 풀에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-245">tooinstall an application package on all compute nodes in a pool, specify one or more application package *references* for hello pool.</span></span> <span data-ttu-id="bada9-246">풀에 대해 지정 하는 hello 응용 프로그램 패키지는 해당 노드의 hello 풀을 연결 및 hello 노드가 다시 부팅 되거나 이미지로 다시 설치 하는 경우 각 계산 노드가에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-246">hello application packages that you specify for a pool are installed on each compute node when that node joins hello pool, and when hello node is rebooted or reimaged.</span></span>

<span data-ttu-id="bada9-247">Batch .NET에서, 새 풀을 만들 때 또는 기존 풀에 [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref]를 하나 이상 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="bada9-248">hello [ApplicationPackageReference] [ net_pkgref] 클래스 응용 프로그램 ID 및 계산 노드는 풀에서 tooinstall 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-248">hello [ApplicationPackageReference][net_pkgref] class specifies an application ID and version tooinstall on a pool's compute nodes.</span></span>

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="bada9-249">Hello 일괄 처리 서비스 표시 노드 hello 어떤 이유로 든 실패 하면 응용 프로그램 패키지 배포 [사용할 수 없는][net_nodestate], 및 해당 노드에서 실행을 위해 예약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-249">If an application package deployment fails for any reason, hello Batch service marks hello node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="bada9-250">이 경우 수행 해야 **다시 시작** hello 노드 tooreinitiate hello 패키지 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-250">In this case, you should **restart** hello node tooreinitiate hello package deployment.</span></span> <span data-ttu-id="bada9-251">Hello 노드를 다시 시작 또한 hello 노드에서 작업을 다시 예약 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-251">Restarting hello node also enables task scheduling again on hello node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="bada9-252">태스크 응용 프로그램 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="bada9-252">Install task application packages</span></span>
<span data-ttu-id="bada9-253">응용 프로그램 패키지를 지정 비슷한 tooa 풀 *참조* 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-253">Similar tooa pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="bada9-254">작업 노드에서 예약 된 toorun 이면 hello 패키지 다운로드 되 고 hello 작업의 명령줄이 실행 되기 직전에 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-254">When a task is scheduled toorun on a node, hello package is downloaded and extracted just before hello task's command line is executed.</span></span> <span data-ttu-id="bada9-255">지정한 패키지 및 버전 hello 노드에 이미 설치 되어 있으면 hello 패키지는 다운로드 되지 않습니다 되며 hello 기존 패키지 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-255">If a specified package and version is already installed on hello node, hello package is not downloaded and hello existing package is used.</span></span>

<span data-ttu-id="bada9-256">hello 태스크를 구성 하는 작업 응용 프로그램 패키지를 tooinstall [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] 속성:</span><span class="sxs-lookup"><span data-stu-id="bada9-256">tooinstall a task application package, configure hello task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

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

## <a name="execute-hello-installed-applications"></a><span data-ttu-id="bada9-257">Hello 설치 된 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="bada9-257">Execute hello installed applications</span></span>
<span data-ttu-id="bada9-258">hello 풀 또는 작업에 대해 지정한 패키지 다운로드 되 고 추출 hello 내 디렉터리 라는 tooa `AZ_BATCH_ROOT_DIR` hello 노드의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-258">hello packages that you've specified for a pool or task are downloaded and extracted tooa named directory within hello `AZ_BATCH_ROOT_DIR` of hello node.</span></span> <span data-ttu-id="bada9-259">일괄 처리는 또한 hello 경로 toohello 라는 디렉터리를 포함 하는 환경 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-259">Batch also creates an environment variable that contains hello path toohello named directory.</span></span> <span data-ttu-id="bada9-260">작업 명령줄을 사용 하 여 hello 노드에서 hello 응용 프로그램을 참조할 때이 환경 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-260">Your task command lines use this environment variable when referencing hello application on hello node.</span></span> 

<span data-ttu-id="bada9-261">Windows 노드에서 hello 변수 형식에 따라 hello에입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-261">On Windows nodes, hello variable is in hello following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="bada9-262">Linux 노드에 hello 형식이 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-262">On Linux nodes, hello format is slightly different.</span></span> <span data-ttu-id="bada9-263">마침표 (.), 하이픈 (-) 및 숫자 기호 (#)는 hello 환경 변수에서 평면화 된 toounderscores 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-263">Periods (.), hypens (-) and number signs (#) are flattened toounderscores in hello environment variable.</span></span> <span data-ttu-id="bada9-264">예:</span><span class="sxs-lookup"><span data-stu-id="bada9-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="bada9-265">`APPLICATIONID`및 `version` 은 배포에 대 한 지정한 toohello 응용 프로그램 및 패키지 버전에 해당 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-265">`APPLICATIONID` and `version` are values that correspond toohello application and package version you've specified for deployment.</span></span> <span data-ttu-id="bada9-266">예를 들어, 응용 프로그램의 해당 버전 2.7을 지정한 경우 *블렌더* 설치 해야 Windows 노드에서 작업 명령줄을 사용 하 여 사용이 환경 변수 tooaccess 해당 파일:</span><span class="sxs-lookup"><span data-stu-id="bada9-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable tooaccess its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="bada9-267">Linux 노드에 hello 환경 변수를이 형식으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-267">On Linux nodes, specify hello environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="bada9-268">응용 프로그램 패키지를 업로드할 때 기본 버전 toodeploy tooyour 계산 노드를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-268">When you upload an application package, you can specify a default version toodeploy tooyour compute nodes.</span></span> <span data-ttu-id="bada9-269">응용 프로그램에 대 한 기본 버전을 지정한 경우에 hello 응용 프로그램을 참조 하는 경우 hello 버전 접미사를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-269">If you have specified a default version for an application, you can omit hello version suffix when you reference hello application.</span></span> <span data-ttu-id="bada9-270">에 표시 된 대로 hello hello 응용 프로그램 블레이드에서 Azure 포털에서에서 hello 기본 응용 프로그램 버전을 지정할 수 있습니다 [업로드 하 고 응용 프로그램 관리](#upload-and-manage-applications)합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-270">You can specify hello default application version in hello Azure portal, on hello Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="bada9-271">예를 들어, 응용 프로그램에 대 한 hello 기본 버전으로 "2.7"을 설정 하는 경우 *블렌더*, 작업 참조할 환경 변수 다음 hello 힙이고 Windows 노드 버전 2.7을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-271">For example, if you set "2.7" as hello default version for application *blender*, and your tasks reference hello following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="bada9-272">hello 만드는 코드는 작업 명령줄 예 hello 기본 버전의 hello 뜨는 *블렌더* 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="bada9-272">hello following code snippet shows an example task command line that launches hello default version of hello *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="bada9-273">참조 [작업에 대 한 환경 설정을](batch-api-basics.md#environment-settings-for-tasks) hello에 [배치 기능 개요](batch-api-basics.md) 계산 노드 환경 설정에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in hello [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="bada9-274">풀의 응용 프로그램 패키지 업데이트</span><span class="sxs-lookup"><span data-stu-id="bada9-274">Update a pool's application packages</span></span>
<span data-ttu-id="bada9-275">기존 풀 이미 응용 프로그램 패키지와 구성 된 경우에 hello 풀에 대 한 새 패키지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-275">If an existing pool has already been configured with an application package, you can specify a new package for hello pool.</span></span> <span data-ttu-id="bada9-276">풀에 대 한 새 패키지 참조를 지정 하는 경우에 hello 다음 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-276">If you specify a new package reference for a pool, hello following apply:</span></span>

* <span data-ttu-id="bada9-277">hello 일괄 처리 서비스는 hello 풀을 조인 하는 모든 새 노드 및 다시 부팅 하거나 이미지로 다시 설치 되는 모든 기존 노드에 hello 새로 지정 된 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-277">hello Batch service installs hello newly specified package on all new nodes that join hello pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="bada9-278">Hello 새 응용 프로그램 패키지를 자동으로 설치 하지 않고 hello 패키지 참조를 업데이트할 때 hello 풀에 이미 있는 노드를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-278">Compute nodes that are already in hello pool when you update hello package references do not automatically install hello new application package.</span></span> <span data-ttu-id="bada9-279">이러한 계산 노드를 다시 부팅 또는 이미지로 다시 설치 tooreceive 새 패키지를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-279">These compute nodes must be rebooted or reimaged tooreceive hello new package.</span></span>
* <span data-ttu-id="bada9-280">새 패키지를 배포할 때 만든 환경 변수는 hello hello 새 응용 프로그램 패키지 참조를 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-280">When a new package is deployed, hello created environment variables reflect hello new application package references.</span></span>

<span data-ttu-id="bada9-281">이 예제에서는 기존 풀 hello에 버전 2.7의 hello *블렌더* 중 하나로 구성 된 응용 프로그램이 해당 [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref]합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-281">In this example, hello existing pool has version 2.7 of hello *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="bada9-282">tooupdate hello 풀 노드 2.76b, 버전 지정 새 [ApplicationPackageReference] [ net_pkgref] hello 새 버전 및 커밋 hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-282">tooupdate hello pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with hello new version, and commit hello change.</span></span>

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

<span data-ttu-id="bada9-283">일괄 처리 서비스 hello 설치 버전 2.76b tooany hello 새 버전에 구성 된 했으므로 *새* hello 풀 연결 된 노드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-283">Now that hello new version has been configured, hello Batch service installs version 2.76b tooany *new* node that joins hello pool.</span></span> <span data-ttu-id="bada9-284">인 hello 노드에 2.76b tooinstall *이미* hello 풀에서 다시 부팅 하거나 해당 이미지를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-284">tooinstall 2.76b on hello nodes that are *already* in hello pool, reboot or reimage them.</span></span> <span data-ttu-id="bada9-285">Note 다시 부팅 된 노드가 이전 패키지 배포에서 hello 파일을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-285">Note that rebooted nodes retain hello files from previous package deployments.</span></span>

## <a name="list-hello-applications-in-a-batch-account"></a><span data-ttu-id="bada9-286">일괄 처리 계정에 hello 응용 프로그램을 나열</span><span class="sxs-lookup"><span data-stu-id="bada9-286">List hello applications in a Batch account</span></span>
<span data-ttu-id="bada9-287">Hello를 사용 하 여 hello 응용 프로그램 및 일괄 처리 계정에 해당 패키지를 나열할 수 [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] 메서드.</span><span class="sxs-lookup"><span data-stu-id="bada9-287">You can list hello applications and their packages in a Batch account by using hello [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List hello applications and their application packages in hello Batch account.
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

## <a name="wrap-up"></a><span data-ttu-id="bada9-288">마무리</span><span class="sxs-lookup"><span data-stu-id="bada9-288">Wrap up</span></span>
<span data-ttu-id="bada9-289">응용 프로그램 패키지와 고객이 자신의 작업에 대 한 hello 응용 프로그램을 선택 하 고 일괄 처리 사용이 가능한 서비스를 사용 하 여 작업을 처리할 때 hello 정확한 버전 toouse를 지정 도울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-289">With application packages, you can help your customers select hello applications for their jobs and specify hello exact version toouse when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="bada9-290">도 고객 tooupload에 대 한 hello 기능을 제공 하 고 자신의 응용 프로그램 서비스에 추적 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-290">You might also provide hello ability for your customers tooupload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bada9-291">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bada9-291">Next steps</span></span>
* <span data-ttu-id="bada9-292">hello [배치 REST API] [ api_rest] 도 응용 프로그램 패키지와 지원 toowork를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-292">hello [Batch REST API][api_rest] also provides support toowork with application packages.</span></span> <span data-ttu-id="bada9-293">예를 들어 hello 참조 [applicationPackageReferences] [ rest_add_pool_with_packages] 요소 [풀 tooan 계정 추가] [ rest_add_pool] 방법에 대 한 정보에 대 한 toospecify는 hello REST API를 사용 하 여 tooinstall을 패키징합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-293">For example, see hello [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool tooan account][rest_add_pool] for information about how toospecify packages tooinstall by using hello REST API.</span></span> <span data-ttu-id="bada9-294">참조 [응용 프로그램] [ rest_applications] tooobtain 응용 프로그램 정보를 사용 하 여 일괄 처리 REST API를 hello 하는 방법에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-294">See [Applications][rest_applications] for details about how tooobtain application information by using hello Batch REST API.</span></span>
* <span data-ttu-id="bada9-295">자세한 내용은 방법 tooprogrammatically [Batch Management.NET 할당량 및 Azure 배치 계정 관리](batch-management-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-295">Learn how tooprogrammatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="bada9-296">hello [Batch Management.NET][api_net_mgmt] 라이브러리 일괄 처리 응용 프로그램 또는 서비스에 대 한 계정 생성 및 삭제 기능을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bada9-296">hello [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

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
