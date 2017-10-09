---
title: "hello 클라우드에서 aaaUse hello Azure 일괄 처리 렌더링 서비스 toorender | Microsoft Docs"
description: "Maya에서 직접 사용량 기준 과금으로 Azure 가상 컴퓨터의 작업을 렌더링합니다."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: tamram
ms.openlocfilehash: 3fb78d883311bbc3ab62743b7d1b111ffad177cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-rendering-service"></a><span data-ttu-id="b14a8-103">Hello 렌더링 하는 일괄 처리 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="b14a8-103">Get started with hello Batch Rendering service</span></span>

<span data-ttu-id="b14a8-104">hello Azure 일괄 처리 렌더링 서비스는 기본 사용 사용량 기준 과금 별로 클라우드 규모 렌더링 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-104">hello Azure Batch Rendering service offers cloud-scale rendering capabilities on a pay-per-use basis.</span></span> <span data-ttu-id="b14a8-105">hello 렌더링 하는 일괄 처리 서비스는 작업 일정 및 큐 관리 실패 및 다시 시도 시간 및 렌더링 작업에 대 한 자동 크기 조정 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-105">hello Batch Rendering service handles job scheduling and queueing, managing failures and retries, and auto-scaling for your render job.</span></span> <span data-ttu-id="b14a8-106">hello 렌더링 하는 일괄 처리 서비스 지원 3ds Autodesk 마 야 Max 및 Arnold 곧 제공 하는 다른 응용 프로그램에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="b14a8-106">hello Batch Rendering service supports Autodesk Maya, 3ds Max, and Arnold, with support for other applications coming soon.</span></span> <span data-ttu-id="b14a8-107">일괄 처리를 마 야 2017에 대 한 플러그 인 hello를 사용 하면 쉽게 toostart 렌더링 작업에 Azure 바탕 화면에서 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-107">hello Batch plug-in for Maya 2017 makes it easy toostart a rendering job on Azure right from your desktop.</span></span> 

## <a name="supported-applications"></a><span data-ttu-id="b14a8-108">지원되는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="b14a8-108">Supported applications</span></span>

<span data-ttu-id="b14a8-109">hello 렌더링 하는 일괄 처리 서비스는 현재 응용 프로그램을 다음 hello를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-109">hello Batch Rendering service currently supports hello following applications:</span></span>

- <span data-ttu-id="b14a8-110">Autodesk Maya</span><span class="sxs-lookup"><span data-stu-id="b14a8-110">Autodesk Maya</span></span>
- <span data-ttu-id="b14a8-111">Autodesk 3ds Max</span><span class="sxs-lookup"><span data-stu-id="b14a8-111">Autodesk 3ds Max</span></span>
- <span data-ttu-id="b14a8-112">Autodesk Arnold</span><span class="sxs-lookup"><span data-stu-id="b14a8-112">Autodesk Arnold</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b14a8-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b14a8-113">Prerequisites</span></span>

<span data-ttu-id="b14a8-114">toouse hello 렌더링 하는 일괄 처리 서비스를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-114">toouse hello Batch Rendering service, you need:</span></span>

- <span data-ttu-id="b14a8-115">[Azure 계정](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="b14a8-115">An [Azure account](https://azure.microsoft.com/free/).</span></span> 
- <span data-ttu-id="b14a8-116">**Azure Batch 계정.**</span><span class="sxs-lookup"><span data-stu-id="b14a8-116">**An Azure Batch account.**</span></span> <span data-ttu-id="b14a8-117">Hello Azure 포털에서에서 일괄 처리 계정 만들기에 대 한 지침을 참조 하십시오. [hello Azure 포털 일괄 처리 계정을 만들고](batch-account-create-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-117">For guidance on creating a Batch account in hello Azure portal, see [Create a Batch account with hello Azure portal](batch-account-create-portal.md).</span></span>
- <span data-ttu-id="b14a8-118">**Azure Storage 계정.**</span><span class="sxs-lookup"><span data-stu-id="b14a8-118">**An Azure Storage account.**</span></span> <span data-ttu-id="b14a8-119">hello 자산 렌더링 작업에 사용 되는 Azure 저장소에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-119">hello assets used for your rendering job are stored in Azure Storage.</span></span> <span data-ttu-id="b14a8-120">Batch 계정을 설정할 때 자동으로 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-120">You can create a storage account automatically when you set up your Batch account.</span></span> <span data-ttu-id="b14a8-121">기존 저장소 계정을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-121">You can also use an existing storage account.</span></span> <span data-ttu-id="b14a8-122">저장소 계정에 대해 자세히 toolearn 참조 [toocreate, 관리 또는 hello Azure 포털에서에서 저장소 계정을 삭제 방법을](https://docs.microsoft.com/azure/storage/storage-create-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-122">toolearn more about Storage accounts, see [How toocreate, manage, or delete a storage account in hello Azure portal](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

<span data-ttu-id="b14a8-123">toouse hello 일괄 처리 해야 마 야에 대 한 플러그 인:</span><span class="sxs-lookup"><span data-stu-id="b14a8-123">toouse hello Batch plug-in for Maya, you need:</span></span>

- <span data-ttu-id="b14a8-124">**Maya 2017**</span><span class="sxs-lookup"><span data-stu-id="b14a8-124">**Maya 2017**</span></span>
- <span data-ttu-id="b14a8-125">**Arnold for Maya**</span><span class="sxs-lookup"><span data-stu-id="b14a8-125">**Arnold for Maya**</span></span>

<span data-ttu-id="b14a8-126">Hello를 사용할 수도 있습니다 [Azure 포털](https://portal.azure.com) 마 야, 3ds로 미리 구성 되어 있는 가상 컴퓨터의 toocreate 풀 Max 및 Arnold 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-126">You can also use hello [Azure portal](https://portal.azure.com) toocreate pools of virtual machines that are pre-configured with Maya, 3ds Max, and Arnold.</span></span> <span data-ttu-id="b14a8-127">Hello 포털 toomonitor 작업 사용 수 있으며 응용 프로그램 로그를 다운로드 하 고 RDP 또는 SSH를 사용 하 여 tooindividual Vm에 원격으로 연결 하 여 실패 한 작업을 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-127">You can use hello portal toomonitor jobs and diagnose failed tasks by downloading application logs and by remotely connecting tooindividual VMs using RDP or SSH.</span></span>

## <a name="basic-batch-concepts"></a><span data-ttu-id="b14a8-128">기본 Batch 개념</span><span class="sxs-lookup"><span data-stu-id="b14a8-128">Basic Batch concepts</span></span>

<span data-ttu-id="b14a8-129">Hello 렌더링 하는 일괄 처리 서비스 사용을 시작 하기 전에 계산 노드, 풀 및 작업을 비롯 한 몇 가지 일괄 처리 개념을 이해 하는 것이 도움이 toobe 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-129">Before you begin using hello Batch Rendering service, it's helpful toobe familiar with a few Batch concepts, including compute nodes, pools, and jobs.</span></span> <span data-ttu-id="b14a8-130">일반적으로 Azure 일괄 처리에 대 한 자세한 참조 toolearn [일괄 처리를 사용 하 여 기본적으로 병렬 작업 실행](batch-technical-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-130">toolearn more about Azure Batch in general, see [Run intrinsically parallel workloads with Batch](batch-technical-overview.md).</span></span>

### <a name="pools"></a><span data-ttu-id="b14a8-131">풀</span><span class="sxs-lookup"><span data-stu-id="b14a8-131">Pools</span></span>

<span data-ttu-id="b14a8-132">Batch는 렌더링처럼 계산 집약적인 작업을 **계산 노드** **풀**에서 실행하기 위한 플랫폼 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-132">Batch is a platform service for running compute-intensive work, like rendering, on a **pool** of **compute nodes**.</span></span> <span data-ttu-id="b14a8-133">풀의 각 계산 노드는 Linux 또는 Windows에서 실행 중인 Azure VM(가상 컴퓨터)입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-133">Each compute node in a pool is an Azure virtual machine (VM) running either Linux or Windows.</span></span> 

<span data-ttu-id="b14a8-134">계산 노드 및 일괄 처리 풀에 대 한 자세한 내용은 참조 hello [풀](batch-api-basics.md#pool) 및 [계산 노드](batch-api-basics.md#compute-node) 섹션 [개발 대규모 병렬 일괄 처리를 사용 하 여 솔루션을 계산](batch-api-basics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-134">For more information about Batch pools and compute nodes, see hello [Pool](batch-api-basics.md#pool) and [Compute node](batch-api-basics.md#compute-node) sections in [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md).</span></span>

### <a name="jobs"></a><span data-ttu-id="b14a8-135">작업</span><span class="sxs-lookup"><span data-stu-id="b14a8-135">Jobs</span></span>

<span data-ttu-id="b14a8-136">일괄 처리 **작업** hello에서 실행 되는 작업 컬렉션의에서 계산 노드는 풀은 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-136">A Batch **job** is a collection of tasks that run on hello compute nodes in a pool.</span></span> <span data-ttu-id="b14a8-137">렌더링 작업을 제출 하면 일괄 처리 작업으로 hello 작업을 나누고 hello 풀 toorun hello 작업 toohello 계산 노드를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-137">When you submit a rendering job, Batch divides hello job into tasks and distributes hello tasks toohello compute nodes in hello pool toorun.</span></span>

<span data-ttu-id="b14a8-138">일괄 처리 작업에 대 한 자세한 내용은 참조 hello [작업](batch-api-basics.md#job) 섹션 [개발 대규모 병렬 일괄 처리를 사용 하 여 솔루션을 계산](batch-api-basics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-138">For more information about Batch jobs, see hello [Job](batch-api-basics.md#job) section in [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md).</span></span>

## <a name="use-hello-batch-plug-in-for-maya-toosubmit-a-render-job"></a><span data-ttu-id="b14a8-139">사용 하 여 hello 일괄 처리를 마 야 toosubmit 렌더링 작업에 대 한 플러그 인</span><span class="sxs-lookup"><span data-stu-id="b14a8-139">Use hello Batch plug-in for Maya toosubmit a render job</span></span>

<span data-ttu-id="b14a8-140">일괄 처리를 마 야에 대 한 플러그 인 hello로 작업 toohello 마 야에서 직접 렌더링 하는 일괄 처리 서비스를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-140">With hello Batch plug-in for Maya, you can submit a job toohello Batch Rendering service right from Maya.</span></span> <span data-ttu-id="b14a8-141">다음 섹션 hello tooconfigure이 hello hello 플러그 인에서 작업 하 고 전송 하는 것 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-141">hello following sections describe how tooconfigure hello job from hello plug-in and then submit it.</span></span> 

### <a name="load-hello-batch-plug-in-in-maya"></a><span data-ttu-id="b14a8-142">Hello 일괄 처리를 마 야에 플러그 인을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-142">Load hello Batch plug-in in Maya</span></span>

<span data-ttu-id="b14a8-143">hello 플러그 인 일괄 처리에서 사용할 수는 [GitHub](https://github.com/Azure/azure-batch-maya/releases)합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-143">hello Batch plug-in is available on [GitHub](https://github.com/Azure/azure-batch-maya/releases).</span></span> <span data-ttu-id="b14a8-144">사용자가 선택한 hello 보관 tooa 디렉터리로 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-144">Unzip hello archive tooa directory of your choice.</span></span> <span data-ttu-id="b14a8-145">Hello에서 직접 hello 플러그 인을 로드할 수 있습니다 *azure_batch_maya* 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-145">You can load hello plug-in directly from hello *azure_batch_maya* directory.</span></span>

<span data-ttu-id="b14a8-146">tooload hello 마 야에 플러그 인:</span><span class="sxs-lookup"><span data-stu-id="b14a8-146">tooload hello plug-in in Maya:</span></span>

1. <span data-ttu-id="b14a8-147">Maya를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-147">Run Maya.</span></span>
2. <span data-ttu-id="b14a8-148">**Window** > **설정/기본 설정** > **플러그 인 관리자**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-148">Open **Window** > **Settings/Preferences** > **Plug-in Manager**.</span></span>
3. <span data-ttu-id="b14a8-149">**찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-149">Click **Browse**.</span></span>
4. <span data-ttu-id="b14a8-150">Tooand 선택 이동 *azure_batch_maya/plug-in/AzureBatch.py*합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-150">Navigate tooand select *azure_batch_maya/plug-in/AzureBatch.py*.</span></span>

### <a name="authenticate-access-tooyour-batch-and-storage-accounts"></a><span data-ttu-id="b14a8-151">액세스 tooyour 일괄 처리 및 저장소 계정 인증</span><span class="sxs-lookup"><span data-stu-id="b14a8-151">Authenticate access tooyour Batch and Storage accounts</span></span>

<span data-ttu-id="b14a8-152">toouse hello 플러그 인, Azure 일괄 처리 및 Azure 저장소 계정 키를 사용 하 여 tooauthenticate가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-152">toouse hello plug-in, you need tooauthenticate using your Azure Batch and Azure Storage account keys.</span></span> <span data-ttu-id="b14a8-153">tooretrieve 계정 키:</span><span class="sxs-lookup"><span data-stu-id="b14a8-153">tooretrieve your account keys:</span></span>

1. <span data-ttu-id="b14a8-154">디스플레이 hello 마 야에서 플러그 인 및 선택 hello **Config** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-154">Display hello plug-in in Maya, and select hello **Config** tab.</span></span>
2. <span data-ttu-id="b14a8-155">Toohello 이동 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-155">Navigate toohello [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="b14a8-156">선택 **일괄 처리 계정** hello 왼쪽 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-156">Select **Batch Accounts** from hello left-hand menu.</span></span> <span data-ttu-id="b14a8-157">필요한 경우 **추가 서비스**를 클릭하고 _Batch_로 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-157">If necessary, click **More Services** and filter on _Batch_.</span></span>
4. <span data-ttu-id="b14a8-158">Hello 목록에서 원하는 hello 일괄 처리 계정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-158">Locate hello desired Batch account in hello list.</span></span>
5. <span data-ttu-id="b14a8-159">선택 hello **키** 메뉴 항목 toodisplay 계정 이름, 계정 URL 및 액세스 키:</span><span class="sxs-lookup"><span data-stu-id="b14a8-159">Select hello **Keys** menu item toodisplay your account name, account URL, and access keys:</span></span>
    - <span data-ttu-id="b14a8-160">Hello hello 일괄 처리 계정 URL을 붙여 **서비스** 필드 hello 플러그 인 일괄 처리에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-160">Paste hello Batch account URL into hello **Service** field in hello Batch plug-in.</span></span>
    - <span data-ttu-id="b14a8-161">Hello에 붙여넣기 hello 계정 이름을 **일괄 처리 계정** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-161">Paste hello account name into hello **Batch Account** field.</span></span>
    - <span data-ttu-id="b14a8-162">Hello에 hello 기본 계정 키 붙여넣기 **일괄 처리 키** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-162">Paste hello primary account key into hello **Batch Key** field.</span></span>
7. <span data-ttu-id="b14a8-163">Hello 왼쪽 메뉴에서 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-163">Select Storage Accounts from hello left-hand menu.</span></span> <span data-ttu-id="b14a8-164">필요한 경우 **추가 서비스**를 클릭하고 _Storage_로 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-164">If necessary, click **More Services** and filter on _Storage_.</span></span>
8. <span data-ttu-id="b14a8-165">Hello 목록에서 원하는 hello 저장소 계정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-165">Locate hello desired Storage account in hello list.</span></span>
9. <span data-ttu-id="b14a8-166">선택 hello **선택 키** 메뉴 항목 toodisplay hello 저장소 계정 이름 및 키입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-166">Select hello **Access Keys** menu item toodisplay hello storage account name and keys.</span></span>
    - <span data-ttu-id="b14a8-167">Hello에 붙여넣기 hello 저장소 계정 이름을 **저장소 계정** 필드 hello 플러그 인 일괄 처리에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-167">Paste hello Storage account name into hello **Storage Account** field in hello Batch plug-in.</span></span>
    - <span data-ttu-id="b14a8-168">Hello에 hello 기본 계정 키 붙여넣기 **저장소 키** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-168">Paste hello primary account key into hello **Storage Key** field.</span></span>
10. <span data-ttu-id="b14a8-169">클릭 **Authenticate** 플러그 인 hello tooensure 두 계정 모두에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-169">Click **Authenticate** tooensure that hello plug-in can access both accounts.</span></span>

<span data-ttu-id="b14a8-170">Hello 플러그 인 집합 상태 필드를 너무 hello 성공적으로 인증 되 면**인증 된**:</span><span class="sxs-lookup"><span data-stu-id="b14a8-170">Once you have successfully authenticated, hello plug-in sets hello status field too**Authenticated**:</span></span> 

![Batch 및 Storage 계정 인증](./media/batch-rendering-service/authentication.png)

### <a name="configure-a-pool-for-a-render-job"></a><span data-ttu-id="b14a8-172">렌더링 작업에 대한 풀 구성</span><span class="sxs-lookup"><span data-stu-id="b14a8-172">Configure a pool for a render job</span></span>

<span data-ttu-id="b14a8-173">Batch 및 Storage 계정을 인증한 후에는 렌더링 작업에 사용할 풀을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-173">After you have authenticated your Batch and Storage accounts, set up a pool for your rendering job.</span></span> <span data-ttu-id="b14a8-174">플러그 인 hello 세션 간에 선택 항목을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-174">hello plug-in saves your selections between sessions.</span></span> <span data-ttu-id="b14a8-175">기본 구성을 설정한 후 toomodify 필요 하지는 않습니다 것 변경 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-175">Once you've set up your preferred configuration, you won't need toomodify it unless it changes.</span></span>

<span data-ttu-id="b14a8-176">hello 다음 섹션에서는 과정을 단계별로 hello에서 사용할 수 있는 hello 사용 가능한 옵션 **전송** 탭:</span><span class="sxs-lookup"><span data-stu-id="b14a8-176">hello following sections walk you through hello available options, available on hello **Submit** tab:</span></span>

#### <a name="specify-a-new-or-existing-pool"></a><span data-ttu-id="b14a8-177">새 풀 또는 기존 풀 지정</span><span class="sxs-lookup"><span data-stu-id="b14a8-177">Specify a new or existing pool</span></span>

<span data-ttu-id="b14a8-178">toorun hello 렌더링 작업 (job)을 선택 하는 hello에 풀 toospecify **전송** 탭 합니다. 이 탭은 풀을 만들거나 기존 풀을 선택하는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-178">toospecify a pool on which toorun hello render job, select hello **Submit** tab. This tab offers options for creating a pool or selecting an existing pool:</span></span>

- <span data-ttu-id="b14a8-179">할 수 있습니다 **자동이이 작업에 대 한 풀 프로 비전** (hello 기본 옵션).</span><span class="sxs-lookup"><span data-stu-id="b14a8-179">You can **auto provision a pool for this job** (hello default option).</span></span> <span data-ttu-id="b14a8-180">이 옵션을 선택 하면 일괄 처리 hello 풀 hello 현재 작업에 대 한 단독으로 만들고 자동으로 삭제 hello 풀 hello 렌더링 작업은 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-180">When you choose this option, Batch creates hello pool exclusively for hello current job, and automatically deletes hello pool when hello render job is complete.</span></span> <span data-ttu-id="b14a8-181">단일 렌더링 작업 toocomplete 있는 경우이 옵션을 사용 하는이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-181">This option is best when you have a single render job toocomplete.</span></span>
- <span data-ttu-id="b14a8-182">**기존의 영구 풀을 다시 사용할 수 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="b14a8-182">You can **reuse an existing persistent pool**.</span></span> <span data-ttu-id="b14a8-183">기존 풀이 유휴 상태를 설정한 경우 hello 드롭다운에서 선택 하 여 실행 중인 hello 렌더링 작업에 대 한 해당 풀을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-183">If you have an existing pool that is idle, you can specify that pool for running hello render job by selecting it from hello dropdown.</span></span> <span data-ttu-id="b14a8-184">Hello 필요한 시간 tooprovision hello 풀을 저장 영구 기존 풀을 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-184">Reusing an existing persistent pool saves hello time required tooprovision hello pool.</span></span>  
- <span data-ttu-id="b14a8-185">**새 영구 풀을 만들 수 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="b14a8-185">You can **create a new persistent pool**.</span></span> <span data-ttu-id="b14a8-186">이 옵션을 선택 하면 hello 작업을 실행 하기 위한 새 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-186">Choosing this option creates a new pool for running hello job.</span></span> <span data-ttu-id="b14a8-187">이후의 작업을 쉽게 사용할 수 있도록 hello 작업이 완료 되 면 hello 풀을 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-187">It does not delete hello pool when hello job is complete, so that you can reuse it for future jobs.</span></span> <span data-ttu-id="b14a8-188">렌더링 작업 연속 필요 toorun 있는 경우이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-188">Select this option when you have a continuous need toorun render jobs.</span></span> <span data-ttu-id="b14a8-189">후속 작업에서 선택할 수 있습니다 **영구 기존 풀을 다시 사용할** toouse hello hello 첫 번째 작업에 대해 만든 영구 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-189">On subsequent jobs, you can select **reuse an existing persistent pool** toouse hello persistent pool that you created for hello first job.</span></span>

![풀, OS 이미지, VM 크기 및 라이선스 지정](./media/batch-rendering-service/submit.png)

<span data-ttu-id="b14a8-191">Azure Vm에 대 한 비용 발생 하는 방법에 대 한 자세한 내용은 참조 hello [Linux 가격 정보 FAQ](https://azure.microsoft.com/pricing/details/virtual-machines/linux/#faq) 및 [Windows 가격 정보 FAQ](https://azure.microsoft.com/pricing/details/virtual-machines/windows/#faq)합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-191">For more information on how charges accrue for Azure VMs, see hello [Linux Pricing FAQ](https://azure.microsoft.com/pricing/details/virtual-machines/linux/#faq) and [Windows Pricing FAQ](https://azure.microsoft.com/pricing/details/virtual-machines/windows/#faq).</span></span>

#### <a name="specify-hello-os-image-tooprovision"></a><span data-ttu-id="b14a8-192">Hello OS 이미지 tooprovision 지정</span><span class="sxs-lookup"><span data-stu-id="b14a8-192">Specify hello OS image tooprovision</span></span>

<span data-ttu-id="b14a8-193">Hello hello 풀에 hello 유형의 OS 이미지 toouse tooprovision 계산 노드를 지정할 수 있습니다 **Env** (환경)를 탭 합니다. 현재 일괄 처리 hello 다음 작업을 렌더링 하기 위한 이미지 옵션을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-193">You can specify hello type of OS image toouse tooprovision compute nodes in hello pool on hello **Env** (Environment) tab. Batch currently supports hello following image options for rendering jobs:</span></span>

|<span data-ttu-id="b14a8-194">운영 체제</span><span class="sxs-lookup"><span data-stu-id="b14a8-194">Operating System</span></span>  |<span data-ttu-id="b14a8-195">이미지</span><span class="sxs-lookup"><span data-stu-id="b14a8-195">Image</span></span>  |
|---------|---------|
|<span data-ttu-id="b14a8-196">Linux</span><span class="sxs-lookup"><span data-stu-id="b14a8-196">Linux</span></span>     |<span data-ttu-id="b14a8-197">Batch CentOS Preview</span><span class="sxs-lookup"><span data-stu-id="b14a8-197">Batch CentOS Preview</span></span> |
|<span data-ttu-id="b14a8-198">Windows</span><span class="sxs-lookup"><span data-stu-id="b14a8-198">Windows</span></span>     |<span data-ttu-id="b14a8-199">Batch Windows Preview</span><span class="sxs-lookup"><span data-stu-id="b14a8-199">Batch Windows Preview</span></span> |

#### <a name="choose-a-vm-size"></a><span data-ttu-id="b14a8-200">VM 크기 선택</span><span class="sxs-lookup"><span data-stu-id="b14a8-200">Choose a VM size</span></span>

<span data-ttu-id="b14a8-201">Hello에 hello v M 크기를 지정할 수 있습니다 **Env** 탭 합니다. 사용 가능한 VM 크기에 대한 자세한 내용은 [Azure에서 Linux VM 크기](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) 및 [Azure에서 Windows VM 크기](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b14a8-201">You can specify hello VM size on hello **Env** tab. For more information about available VM sizes, see [Linux VM sizes in Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) and [Windows VM sizes in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes).</span></span> 

![Hello Env 탭 hello VM OS 이미지와 크기를 지정 합니다.](./media/batch-rendering-service/environment.png)

#### <a name="specify-licensing-options"></a><span data-ttu-id="b14a8-203">라이선스 옵션 지정</span><span class="sxs-lookup"><span data-stu-id="b14a8-203">Specify licensing options</span></span>

<span data-ttu-id="b14a8-204">Hello toouse를 원하는 hello 라이선스를 지정할 수 있습니다 **Env** 탭 합니다. 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-204">You can specify hello licenses you wish toouse on hello **Env** tab. Options include:</span></span>

- <span data-ttu-id="b14a8-205">**Maya**, 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-205">**Maya**, which is enabled by default.</span></span>
- <span data-ttu-id="b14a8-206">**Arnold**, Arnold 마 야에 hello 활성 렌더링 엔진으로 검색 되 면 활성화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-206">**Arnold**, which is enabled if Arnold is detected as hello active render engine in Maya.</span></span>

 <span data-ttu-id="b14a8-207">사용자 고유 라이선스를 사용 하 여 toorender 원한다 면 hello 적절 한 환경 변수 toohello 테이블을 추가 하 여 라이선스 시작점과 끝점을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-207">If you wish toorender using your own license, you can configure your license end point by adding hello appropriate environment variables toohello table.</span></span> <span data-ttu-id="b14a8-208">이렇게 하면 있는지 toodeselect hello 기본 라이선스 옵션을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-208">Be sure toodeselect hello default licensing options if you do so.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b14a8-209">요금 지불 hello 라이선스 사용 Vm hello 풀에서 실행 되는 동안 Vm hello 렌더링을 위해 현재 사용 되지 않는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-209">You are billed for use of hello licenses while VMs are running in hello pool, even if hello VMs are not currently being used for rendering.</span></span> <span data-ttu-id="b14a8-210">tooavoid 추가 요금이 이동 toohello **풀** 탭 및 크기 조정 hello 풀 too0 노드 준비 toorun가 아닌 경우 다른 렌더링 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-210">tooavoid extra charges, navigate toohello **Pools** tab and resize hello pool too0 nodes until you are ready toorun another render job.</span></span> 
>
>

#### <a name="manage-persistent-pools"></a><span data-ttu-id="b14a8-211">영구 풀 관리</span><span class="sxs-lookup"><span data-stu-id="b14a8-211">Manage persistent pools</span></span>

<span data-ttu-id="b14a8-212">Hello에 영구 기존 풀을 관리할 수 있습니다 **풀** 탭 합니다. Hello 목록에서 풀을 선택 하면 hello hello 풀의 현재 상태가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-212">You can manage an existing persistent pool on hello **Pools** tab. Selecting a pool from hello list displays hello current state of hello pool.</span></span>

<span data-ttu-id="b14a8-213">Hello에서 **풀** 탭 hello 풀을 삭제 하 고 hello 번호 hello 풀에 있는 Vm의 크기를 조정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-213">From hello **Pools** tab, you can also delete hello pool and resize hello number of VMs in hello pool.</span></span> <span data-ttu-id="b14a8-214">작업 사이는 비용이 발생 하는 풀 too0 노드 tooavoid 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-214">You can resize a pool too0 nodes tooavoid incurring costs in between workloads.</span></span>

![풀 보기, 크기 조정 및 삭제](./media/batch-rendering-service/pools.png)

### <a name="configure-a-render-job-for-submission"></a><span data-ttu-id="b14a8-216">제출할 수 있도록 렌더링 작업 구성</span><span class="sxs-lookup"><span data-stu-id="b14a8-216">Configure a render job for submission</span></span>

<span data-ttu-id="b14a8-217">Hello 렌더링 작업을 실행 하는 hello 풀에 대 한 hello 매개 변수를 지정 하면 hello 작업 자체를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-217">Once you have specified hello parameters for hello pool that will run hello render job, configure hello job itself.</span></span> 

#### <a name="specify-scene-parameters"></a><span data-ttu-id="b14a8-218">장면 매개 변수 지정</span><span class="sxs-lookup"><span data-stu-id="b14a8-218">Specify scene parameters</span></span>

<span data-ttu-id="b14a8-219">hello 플러그 인 일괄 처리를 마 야에서 현재 사용 중인 어떤 렌더링 엔진을 검색 한 적절 한 표시 hello 렌더링 hello에 대 한 설정 **전송** 탭 합니다. 이러한 설정에는 hello 시작 프레임, 끝 프레임, 출력 접두사 및 프레임 단계가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-219">hello Batch plug-in detects which rendering engine you're currently using in Maya, and displays hello appropriate render settings on hello **Submit** tab. These settings include hello start frame, end frame, output prefix, and frame step.</span></span> <span data-ttu-id="b14a8-220">Hello 플러그 인에서 서로 다른 설정을 지정 하 여 hello 장면 파일 렌더링 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-220">You can override hello scene file render settings by specifying different settings in hello plug-in.</span></span> <span data-ttu-id="b14a8-221">변경 내용은 toohello 플러그 인 설정 되지 않으므로 지속형된 백 toohello 장면 파일 렌더링 설정을 tooreupload hello 장면 파일 필요 없이 작업에서 작업 별로 변경을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-221">Changes you make toohello plug-in settings are not persisted back toohello scene file render settings, so you can make changes on a job-by-job basis without needing tooreupload hello scene file.</span></span>

<span data-ttu-id="b14a8-222">hello 플러그 인 경고 hello 마 야에서 선택한 엔진을 렌더링 하는 경우 사용자가 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-222">hello plug-in warns you if hello render engine that you selected in Maya is not supported.</span></span>

<span data-ttu-id="b14a8-223">플러그 인 hello 열려 있는 동안 새 장면을 로드 하면 클릭 hello **새로 고침** 단추 toomake 있는지 hello 설정이 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-223">If you load a new scene while hello plug-in is open, click hello **Refresh** button toomake sure hello settings are updated.</span></span>

#### <a name="resolve-asset-paths"></a><span data-ttu-id="b14a8-224">자산 경로 확인</span><span class="sxs-lookup"><span data-stu-id="b14a8-224">Resolve asset paths</span></span>

<span data-ttu-id="b14a8-225">Hello 플러그 인을 로드 하는 경우 hello 장면 파일에 대 한 외부 파일 참조를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-225">When you load hello plug-in, it scans hello scene file for any external file references.</span></span> <span data-ttu-id="b14a8-226">이러한 참조는 hello에 표시 되는 **자산** 탭 합니다. 참조 경로 확인할 수 없는 경우 hello 플러그 인 포함 한 몇 가지 기본 위치에서 toolocate hello 파일을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-226">These references are displayed in hello **Assets** tab. If a referenced path cannot be resolved, hello plug-in attempts toolocate hello file in a few default locations, including:</span></span>

- <span data-ttu-id="b14a8-227">hello 장면 파일의 hello 위치</span><span class="sxs-lookup"><span data-stu-id="b14a8-227">hello location of hello scene file</span></span> 
- <span data-ttu-id="b14a8-228">hello 현재 프로젝트의 _sourceimages_ 디렉터리</span><span class="sxs-lookup"><span data-stu-id="b14a8-228">hello current project's _sourceimages_ directory</span></span>
- <span data-ttu-id="b14a8-229">hello 현재 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-229">hello current working directory.</span></span> 

<span data-ttu-id="b14a8-230">Hello 자산 여전히을 찾을 수 없는 경우에 경고 아이콘이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-230">If hello asset still cannot be located, it is listed with a warning icon:</span></span>

![누락된 자산이 경고 아이콘과 함께 표시됨](./media/batch-rendering-service/missing_assets.png)

<span data-ttu-id="b14a8-232">해결 되지 않은 파일 참조의 hello 위치를 알고 있는 경우 경고 메시지가 표시 tooadd 검색 경로 아이콘 toobe hello 클릭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-232">If you know hello location of an unresolved file reference, you can click hello warning icon toobe prompted tooadd a search path.</span></span> <span data-ttu-id="b14a8-233">hello 다음 플러그 인이 검색 경로 tooattempt tooresolve 누락 된 모든 자산을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-233">hello plug-in then uses this search path tooattempt tooresolve any missing assets.</span></span> <span data-ttu-id="b14a8-234">추가 검색 경로를 원하는 만큼 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-234">You can add any number of additional search paths.</span></span>

<span data-ttu-id="b14a8-235">참조가 확인되면 녹색 등 아이콘이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-235">When a reference is resolved, it is listed with a green light icon:</span></span>

![확인된 자산에 녹색 등 아이콘이 표시됨](./media/batch-rendering-service/found_assets.png)

<span data-ttu-id="b14a8-237">장면이 다른 파일이 필요한 경우 플러그 인에 해당 hello가 검색 되지 않은 추가 파일 또는 디렉터리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-237">If your scene requires other files that hello plug-in has not detected, you can add additional files or directories.</span></span> <span data-ttu-id="b14a8-238">사용 하 여 hello **파일 추가** 및 **디렉터리 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-238">Use hello **Add Files** and **Add Directory** buttons.</span></span> <span data-ttu-id="b14a8-239">플러그 인 hello 열려 있는 동안 새 장면을 로드 하면 수 있는지 tooclick **새로 고침** tooupdate hello 장면 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-239">If you load a new scene while hello plug-in is open, be sure tooclick **Refresh** tooupdate hello scene's references.</span></span>

#### <a name="upload-assets-tooan-asset-project"></a><span data-ttu-id="b14a8-240">자산 tooan 자산 프로젝트 업로드</span><span class="sxs-lookup"><span data-stu-id="b14a8-240">Upload assets tooan asset project</span></span>

<span data-ttu-id="b14a8-241">참조 된 hello에 표시 되는 파일을 제출할 때 렌더링 작업 hello **자산** 탭 자동으로 업로드 된 tooAzure 자산 프로젝트로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-241">When you submit a render job, hello referenced files displayed in hello **Assets** tab are automatically uploaded tooAzure Storage as an asset project.</span></span> <span data-ttu-id="b14a8-242">또한 hello를 사용 하 여 hello 자산 파일 렌더링 작업을 독립적으로 업로드할 수 있습니다 **업로드** hello 단추 **자산** hello에 탭 hello 자산 프로젝트 이름이 지정 된 **프로젝트**필드를 현재 마 야 프로젝트 hello 기본적으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-242">You can also upload hello asset files independently of a render job, using hello **Upload** button on hello **Assets** tab. hello asset project name is specified in hello **Project** field and is named after hello current Maya project by default.</span></span> <span data-ttu-id="b14a8-243">자산 파일 업로드 되 면 hello 로컬 파일 구조가 보존 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-243">When asset files are uploaded, hello local file structure is preserved.</span></span> 

<span data-ttu-id="b14a8-244">자산이 업로드되면 임의의 수의 렌더링 작업에서 자산을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-244">Once uploaded, assets can be referenced by any number of render jobs.</span></span> <span data-ttu-id="b14a8-245">모든 업로드 된 자산은 hello 자산 프로젝트를 참조 하는 사용 가능한 tooany 작업 hello 장면에 포함 된 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-245">All uploaded assets are available tooany job that references hello asset project, whether or not they are included in hello scene.</span></span> <span data-ttu-id="b14a8-246">hello에 hello 이름 변경, 다음 작업에서 참조 하는 toochange hello 자산 프로젝트용 **프로젝트** 필드 hello에 **자산** 탭 합니다. 참조 된 파일을 업로드 tooexclude 있으면 선택을 취소 hello 목록 옆의 녹색 hello 단추를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-246">toochange hello asset project referenced by your next job, change hello name in hello **Project** field in hello **Assets** tab. If there are referenced files that you wish tooexclude from uploading, unselect them using hello green button beside hello listing.</span></span>

#### <a name="submit-and-monitor-hello-render-job"></a><span data-ttu-id="b14a8-247">모니터 hello 렌더링 작업 및 제출</span><span class="sxs-lookup"><span data-stu-id="b14a8-247">Submit and monitor hello render job</span></span>

<span data-ttu-id="b14a8-248">Hello 플러그 인에 hello 렌더링 작업을 구성 하 고 나면 클릭 hello **작업 제출** hello 단추 **전송** toosubmit hello 작업 tooBatch 탭:</span><span class="sxs-lookup"><span data-stu-id="b14a8-248">After you have configured hello render job in hello plug-in, click hello **Submit Job** button on hello **Submit** tab toosubmit hello job tooBatch:</span></span>

![Hello 렌더링 작업을 제출](./media/batch-rendering-service/submit_job.png)

<span data-ttu-id="b14a8-250">Hello에서 진행 중인 작업을 모니터링할 수 있습니다 **작업** hello 플러그 인에 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-250">You can monitor a job that is in progress from hello **Jobs** tab on hello plug-in.</span></span> <span data-ttu-id="b14a8-251">Hello 목록 toodisplay hello 작업의 현재 상태 hello에서에서 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-251">Select a job from hello list toodisplay hello current state of hello job.</span></span> <span data-ttu-id="b14a8-252">이 탭 toocancel를 사용 하 고 삭제 작업으로 toodownload hello 출력 및 로그를 렌더링 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-252">You can also use this tab toocancel and delete jobs, as well as toodownload hello outputs and rendering logs.</span></span> 

<span data-ttu-id="b14a8-253">toodownload 출력 수정 hello **출력** 필드 tooset hello 원하는 대상 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-253">toodownload outputs, modify hello **Outputs** field tooset hello desired destination directory.</span></span> <span data-ttu-id="b14a8-254">Hello 기어 아이콘 toostart hello 작업을 감시 하 고 닫힘으로 출력을 다운로드 하는 백그라운드 프로세스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-254">Click hello gear icon toostart a background process that watches hello job and downloads outputs as it progresses:</span></span> 

![작업 상태 확인 및 출력 다운로드](./media/batch-rendering-service/jobs.png)

<span data-ttu-id="b14a8-256">Hello 다운로드 프로세스를 방해 하지 않고 마 야를 닫을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-256">You can close Maya without disrupting hello download process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b14a8-257">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b14a8-257">Next steps</span></span>

<span data-ttu-id="b14a8-258">일괄 처리에 대해 자세히 toolearn 참조 [일괄 처리를 사용 하 여 기본적으로 병렬 작업 실행](batch-technical-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a8-258">toolearn more about Batch, see [Run intrinsically parallel workloads with Batch](batch-technical-overview.md).</span></span>
