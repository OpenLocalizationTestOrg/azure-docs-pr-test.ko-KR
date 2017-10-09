---
title: "Excel 및 SOA aaaHPC 팩 클러스터 | Microsoft Docs"
description: "Azure의 HPC Pack 클러스터에서 대규모 Excel 및 SOA 워크로드 실행 시작"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="edc54-103">Azure의 HPC Pack 클러스터에서 Excel 및 SOA 작업 실행 시작</span><span class="sxs-lookup"><span data-stu-id="edc54-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="edc54-104">이 문서는 Azure 빠른 시작 템플릿 또는 필요에 따라 Azure PowerShell 배포 스크립트를 사용 하 여 toodeploy Microsoft HPC Pack 2012 R2 Azure 가상 컴퓨터를 클러스터링 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-104">This article shows you how toodeploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="edc54-105">hello 클러스터 HPC Pack을 사용한 Azure 마켓플레이스 VM 이미지 설계 toorun Microsoft Excel 또는 서비스 지향 아키텍처 (SOA) 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-105">hello cluster uses Azure Marketplace VM images designed toorun Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="edc54-106">Hello 클러스터 toorun Excel HPC 및 온-프레미스 클라이언트 컴퓨터에서 SOA 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-106">You can use hello cluster toorun Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="edc54-107">hello Excel HPC 서비스는 Excel 통합 문서 오프 로딩 및 Excel 사용자 정의 함수 또는 Udf 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-107">hello Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="edc54-108">이 문서는 HPC Pack 2012 R2의 기능, 템플릿 및 스크립트를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="edc54-109">이 시나리오는 현재 HPC Pack 2016에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="edc54-110">상위 수준 hello 다음 다이어그램 hello HPC Pack 클러스터 사용자가 만든 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-110">At a high level, hello following diagram shows hello HPC Pack cluster you create.</span></span>

![Excel 작업을 실행하는 노드가 있는 HPC 클러스터][scenario]

## <a name="prerequisites"></a><span data-ttu-id="edc54-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="edc54-112">Prerequisites</span></span>
* <span data-ttu-id="edc54-113">**클라이언트 컴퓨터** -Windows 기반 클라이언트 컴퓨터 toosubmit 샘플 Excel 및 SOA 작업 toohello 클러스터 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-113">**Client computer** - You need a Windows-based client computer toosubmit sample Excel and SOA jobs toohello cluster.</span></span> <span data-ttu-id="edc54-114">또한 Windows 컴퓨터 toorun hello Azure PowerShell 클러스터 배포 스크립트 (해당 배포 방법 선택) 하는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-114">You also need a Windows computer toorun hello Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="edc54-115">**Azure 구독** - Azure 구독이 없는 경우 몇 분 만에 [무료 계정](https://azure.microsoft.com/pricing/free-trial/) 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="edc54-116">**코어 할당량** -멀티 코어 VM 크기에 따라 여러 개의 클러스터 노드를 배포 하는 경우에 특히 tooincrease hello 할당량의 코어를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-116">**Cores quota** - You might need tooincrease hello quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="edc54-117">Azure 빠른 시작 템플릿을 사용 하는 경우 Azure 지역 별로 hello 코어 할당량 리소스 관리자에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-117">If you are using an Azure quickstart template, hello cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="edc54-118">이 경우에 특정 지역에서 tooincrease hello 할당량을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-118">In that case, you might need tooincrease hello quota in a specific region.</span></span> <span data-ttu-id="edc54-119">[Azure 구독 제한, 할당량 및 제약 조건](../../azure-subscription-service-limits.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edc54-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="edc54-120">할당량 tooincrease [온라인 고객 지원 요청을 개시](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) 비용 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-120">tooincrease a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="edc54-121">**Microsoft Office 라이선스** - Microsoft Excel과 함께 마켓플레이스 HPC Pack 2012 R2 VM 이미지를 사용하여 컴퓨터 노드를 배포하는 경우 30일 평가 버전의 Microsoft Excel Professional Plus 2013이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="edc54-122">Hello 평가 기간 후 tooprovide는 유효한 Microsoft Office 라이선스 tooactivate Excel toocontinue toorun 작업 부하는 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-122">After hello evaluation period, you need tooprovide a valid Microsoft Office license tooactivate Excel toocontinue toorun workloads.</span></span> <span data-ttu-id="edc54-123">이 문서의 뒷부분에 나오는 [Excel 활성화](#excel-activation) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edc54-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="edc54-124">1단계.</span><span class="sxs-lookup"><span data-stu-id="edc54-124">Step 1.</span></span> <span data-ttu-id="edc54-125">Azure에서 HPC Pack 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="edc54-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="edc54-126">두 옵션 tooset hello HPC Pack 2012 R2 클러스터를 매개 변수를 표시 합니다: Azure 빠른 시작 템플릿 및 Azure 포털; hello를 사용 하 여 첫 번째 및 Azure PowerShell 배포 스크립트를 사용 하 여 두 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-126">We show two options tooset up hello HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and hello Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="edc54-127">옵션 1.</span><span class="sxs-lookup"><span data-stu-id="edc54-127">Option 1.</span></span> <span data-ttu-id="edc54-128">빠른 시작 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="edc54-128">Use a quickstart template</span></span>
<span data-ttu-id="edc54-129">Azure 빠른 시작 템플릿 tooquickly를 사용 하 여 hello Azure 포털에서에서 HPC Pack 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-129">Use an Azure quickstart template tooquickly deploy an HPC Pack cluster in hello Azure portal.</span></span> <span data-ttu-id="edc54-130">Hello 포털에서 hello 서식 파일을 열 때 클러스터에 대 한 hello 설정을 입력할 수 있는 간단한 UI를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-130">When you open hello template in hello portal, you get a simple UI where you enter hello settings for your cluster.</span></span> <span data-ttu-id="edc54-131">Hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-131">Here are hello steps.</span></span> 

> [!TIP]
> <span data-ttu-id="edc54-132">원하는 경우 Excel 작업 전용으로 유사한 클러스터를 만드는 [Azure Marketplace 템플릿](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="edc54-133">hello 단계 hello 다음에서 약간 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-133">hello steps differ slightly from hello following.</span></span>
> 
> 

1. <span data-ttu-id="edc54-134">Hello 방문 [GitHub에서 HPC 클러스터 만들기 템플릿 페이지](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-134">Visit hello [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="edc54-135">원하는 경우 hello 템플릿과 hello 소스 코드에 대 한 정보를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-135">If you want, review information about hello template and hello source code.</span></span>
2. <span data-ttu-id="edc54-136">클릭 **tooAzure 배포** toostart hello Azure 포털에서에서 hello 템플릿 사용 하 여 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-136">Click **Deploy tooAzure** toostart a deployment with hello template in hello Azure portal.</span></span>
   
   ![템플릿 tooAzure 배포][github]
3. <span data-ttu-id="edc54-138">Hello 포털에서 이러한 hello HPC 클러스터 서식 파일에 대 한 단계 tooenter hello 매개 변수를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-138">In hello portal, follow these steps tooenter hello parameters for hello HPC cluster template.</span></span>
   
   <span data-ttu-id="edc54-139">a.</span><span class="sxs-lookup"><span data-stu-id="edc54-139">a.</span></span> <span data-ttu-id="edc54-140">Hello에 **매개 변수** 페이지를 입력 하거나 hello 템플릿 매개 변수 값을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-140">On hello **Parameters** page, enter or modify values for hello template parameters.</span></span> <span data-ttu-id="edc54-141">(도움말 정보에 대 한 hello 아이콘 다음 tooeach 설정을 클릭 합니다.) 샘플 값 hello 다음 화면에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-141">(Click hello icon next tooeach setting for help information.) Sample values are shown in hello following screen.</span></span> <span data-ttu-id="edc54-142">이 예에서는 라는 클러스터를 만들고 *hpc01* hello에 *hpc.local* 도메인 헤드 노드 및 2로 구성 된 노드를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-142">This example creates a cluster named *hpc01* in hello *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="edc54-143">Microsoft Excel을 포함 하는 HPC Pack VM 이미지에서 hello 계산 노드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-143">hello compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![매개 변수 입력][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="edc54-145">hello 헤드 노드 VM hello에서 자동으로 만들어집니다 [최신 마켓플레이스 이미지](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) Windows Server 2012 r 2에서 HPC Pack 2012 r 2의 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-145">hello head node VM is created automatically from hello [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="edc54-146">현재 hello 이미지의 HPC Pack 2012 R2 업데이트 3에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-146">Currently hello image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="edc54-147">계산 노드 Vm hello 선택한 hello 계산 노드 제품군의 최신 이미지에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-147">Compute node VMs are created from hello latest image of hello selected compute node family.</span></span> <span data-ttu-id="edc54-148">선택 hello **ComputeNodeWithExcel** Microsoft Excel Professional Plus 2013의 평가 버전을 포함 하는 hello 최신 HPC Pack 컴퓨터 노드 이미지에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-148">Select hello **ComputeNodeWithExcel** option for hello latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="edc54-149">Excel UDF 오프 로딩 또는 일반 SOA 세션에 대 한 클러스터 toodeploy 선택 hello **ComputeNode** (설치 하지 않고 Excel) 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-149">toodeploy a cluster for general SOA sessions or for Excel UDF offloading, choose hello **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="edc54-150">b.</span><span class="sxs-lookup"><span data-stu-id="edc54-150">b.</span></span> <span data-ttu-id="edc54-151">Hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-151">Choose hello subscription.</span></span>
   
   <span data-ttu-id="edc54-152">c.</span><span class="sxs-lookup"><span data-stu-id="edc54-152">c.</span></span> <span data-ttu-id="edc54-153">같은 hello 클러스터에 대 한 리소스 그룹을 만들 *hpc01RG*합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-153">Create a resource group for hello cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="edc54-154">d.</span><span class="sxs-lookup"><span data-stu-id="edc54-154">d.</span></span> <span data-ttu-id="edc54-155">미국 중남부 같은 hello 리소스 그룹에 대 한 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-155">Choose a location for hello resource group, such as Central US.</span></span>
   
   <span data-ttu-id="edc54-156">e.</span><span class="sxs-lookup"><span data-stu-id="edc54-156">e.</span></span> <span data-ttu-id="edc54-157">Hello에 **약관** 페이지 hello 용어를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-157">On hello **Legal terms** page, review hello terms.</span></span> <span data-ttu-id="edc54-158">해당 내용에 동의하는 경우 **구매**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="edc54-159">Hello 서식 파일에 대 한 hello 값을 설정 했으면 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-159">Then, when you are finished setting hello values for hello template, click **Create**.</span></span>
4. <span data-ttu-id="edc54-160">Hello 배포가 완료 되는 경우 (일반적으로 약 30 분 소요), hello 클러스터 헤드 노드에서 hello 클러스터 인증서 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-160">When hello deployment completes (it typically takes around 30 minutes), export hello cluster certificate file from hello cluster head node.</span></span> <span data-ttu-id="edc54-161">이후 단계에서 hello 클라이언트 컴퓨터 tooprovide hello 서버 쪽에 대 한 인증 보안 HTTP 바인딩에이 공용 인증서를 가져오세요.</span><span class="sxs-lookup"><span data-stu-id="edc54-161">In a later step, you import this public certificate on hello client computer tooprovide hello server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="edc54-162">a.</span><span class="sxs-lookup"><span data-stu-id="edc54-162">a.</span></span> <span data-ttu-id="edc54-163">Hello Azure 포털에서에서 이동 toohello 대시보드를 선택 하는 hello 헤드 노드를 클릭 **연결** 원격 데스크톱을 사용 하 여 hello 페이지 tooconnect hello 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-163">In hello Azure portal, go toohello dashboard, select hello head node, and click **Connect** at hello top of hello page tooconnect using Remote Desktop.</span></span>
   
    <!-- ![Connect toohello head node][connect] -->
   
   <span data-ttu-id="edc54-164">b.</span><span class="sxs-lookup"><span data-stu-id="edc54-164">b.</span></span> <span data-ttu-id="edc54-165">Hello 개인 키가 없는 인증서 관리자 tooexport hello 헤드 노드에서 인증서 (Cert: \LocalMachine\My 위치)의 표준 절차를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="edc54-165">Use standard procedures in Certificate Manager tooexport hello head node certificate (located under Cert:\LocalMachine\My) without hello private key.</span></span> <span data-ttu-id="edc54-166">이 예제에서는 *CN = hpc01.eastus.cloudapp.azure.com*을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![Hello 인증서 내보내기][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="edc54-168">옵션 2.</span><span class="sxs-lookup"><span data-stu-id="edc54-168">Option 2.</span></span> <span data-ttu-id="edc54-169">Hello HPC Pack IaaS 배포 스크립트를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="edc54-169">Use hello HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="edc54-170">hello HPC Pack IaaS 배포 스크립트는 HPC Pack 클러스터 다른 다양 한 방식으로 toodeploy를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-170">hello HPC Pack IaaS deployment script provides another versatile way toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="edc54-171">Hello 템플릿 hello Azure 리소스 관리자 배포 모델을 사용 하는 반면 hello 클래식 배포 모델에서 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-171">It creates a cluster in hello classic deployment model, whereas hello template uses hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="edc54-172">또한 hello 스크립트는 hello Azure Global 또는 Azure China 서비스에서 구독을와 호환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-172">Also, hello script is compatible with a subscription in either hello Azure Global or Azure China service.</span></span>

<span data-ttu-id="edc54-173">**추가 필수 조건**</span><span class="sxs-lookup"><span data-stu-id="edc54-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="edc54-174">**Azure PowerShell** - [Azure PowerShell(버전 0.8.10 이상)을 설치 및 구성](/powershell/azure/overview) 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="edc54-175">**HPC Pack IaaS 배포 스크립트** -다운로드 하 고 hello hello에서 hello 스크립트의 최신 버전을 푸는 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=44949)합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-175">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="edc54-176">Hello 버전의 hello 스크립트를 실행 하 여 확인 `New-HPCIaaSCluster.ps1 –Version`합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-176">Check hello version of hello script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="edc54-177">이 문서 버전 4.5.0 또는 hello 스크립트의 나중에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-177">This article is based on version 4.5.0 or later of hello script.</span></span>

<span data-ttu-id="edc54-178">**Hello 구성 파일 만들기**</span><span class="sxs-lookup"><span data-stu-id="edc54-178">**Create hello configuration file**</span></span>

 <span data-ttu-id="edc54-179">HPC Pack IaaS 배포 스크립트 hello hello HPC 클러스터의 hello 인프라를 설명 하는 입력으로는 XML 구성 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-179">hello HPC Pack IaaS deployment script uses an XML configuration file as input that describes hello infrastructure of hello HPC cluster.</span></span> <span data-ttu-id="edc54-180">18 및 헤드 노드 구성 된 클러스터 계산 노드 Microsoft Excel을 포함 하는 hello 계산 노드 이미지에서 만든 toodeploy hello 다음 샘플 구성 파일에 사용자 환경에 대 한 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-180">toodeploy a cluster consisting of a head node and 18 compute nodes created from hello compute node image that includes Microsoft Excel, substitute values for your environment into hello following sample configuration file.</span></span> <span data-ttu-id="edc54-181">Hello 구성 파일에 대 한 자세한 내용은 참조 하십시오. hello 스크립트 폴더에 있는 Manual.rtf 파일 hello 및 [hello HPC Pack IaaS 배포 스크립트는 HPC 클러스터 만들기](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-181">For more information about hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="edc54-182">**Hello 구성 파일에 대 한 참고 사항**</span><span class="sxs-lookup"><span data-stu-id="edc54-182">**Notes about hello configuration file**</span></span>

* <span data-ttu-id="edc54-183">hello **VMName** hello 헤드 노드의 **해야** hello로 동일 hello 수 **ServiceName**, 또는 SOA 작업 toorun 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-183">hello **VMName** of hello head node **MUST** be hello same as hello **ServiceName**, or SOA jobs fail toorun.</span></span>
* <span data-ttu-id="edc54-184">지정 했는지 확인 **EnableWebPortal** hello 헤드 노드에서 인증서가 생성 하 고 내보낼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-184">Make sure you specify **EnableWebPortal** so that hello head node certificate is generated and exported.</span></span>
* <span data-ttu-id="edc54-185">hello 파일 PostConfig.ps1 hello 헤드 노드에서 실행 되는 구성 후 PowerShell 스크립트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-185">hello file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on hello head node.</span></span> <span data-ttu-id="edc54-186">다음 샘플 스크립트는 hello hello Azure 저장소 연결 문자열을 구성 하 고, hello 헤드 노드에서 hello 계산 노드 역할을 제거, 배포 하는 경우 모든 노드를 온라인 상태로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-186">hello following sample script configures hello Azure storage connection string, removes hello compute node role from hello head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

<span data-ttu-id="edc54-187">**Hello 스크립트 실행**</span><span class="sxs-lookup"><span data-stu-id="edc54-187">**Run hello script**</span></span>

1. <span data-ttu-id="edc54-188">관리자 권한으로 hello 클라이언트 컴퓨터에서 hello PowerShell 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-188">Open hello PowerShell console on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="edc54-189">디렉터리 toohello 스크립트 폴더 (이 예제의 E:\IaaSClusterScript)를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-189">Change directory toohello script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="edc54-190">toodeploy hello HPC Pack 클러스터를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-190">toodeploy hello HPC Pack cluster, run hello following command.</span></span> <span data-ttu-id="edc54-191">이 예에서는 해당 hello 구성 파일은 E:\HPCDemoConfig.xml 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-191">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="edc54-192">hello HPC Pack 배포 스크립트를 일정 시간 동안 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-192">hello HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="edc54-193">한 가지 hello 스크립트 tooexport는 hello 클러스터 인증서를 다운로드 하 여 hello 클라이언트 컴퓨터에 hello 현재 사용자의 Documents 폴더에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-193">One thing hello script does is tooexport and download hello cluster certificate and save it in hello current user’s Documents folder on hello client computer.</span></span> <span data-ttu-id="edc54-194">hello 스크립트 메시지 유사한 toohello 다음을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-194">hello script generates a message similar toohello following.</span></span> <span data-ttu-id="edc54-195">다음 단계에서는 hello 적절 한 인증서 저장소에 hello 인증서를 가져오세요.</span><span class="sxs-lookup"><span data-stu-id="edc54-195">In a following step, you import hello certificate in hello appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="edc54-196">2단계.</span><span class="sxs-lookup"><span data-stu-id="edc54-196">Step 2.</span></span> <span data-ttu-id="edc54-197">온-프레미스 클라이언트에서 Excel 통합 문서 오프로드 및 UDF 실행</span><span class="sxs-lookup"><span data-stu-id="edc54-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="edc54-198">Excel 활성화</span><span class="sxs-lookup"><span data-stu-id="edc54-198">Excel activation</span></span>
<span data-ttu-id="edc54-199">Hello ComputeNodeWithExcel VM 이미지를 프로덕션 작업에 사용 하는 유효한 Microsoft Office 라이선스 키 tooactivate Excel hello 계산 노드에서 tooprovide가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-199">When using hello ComputeNodeWithExcel VM image for production workloads, you need tooprovide a valid Microsoft Office license key tooactivate Excel on hello compute nodes.</span></span> <span data-ttu-id="edc54-200">그렇지 않으면 hello 평가 버전의 Excel 30 일 후 만료 되 고 hello COMException (0x800AC472)로 실패 합니다 Excel 통합 문서를 실행.</span><span class="sxs-lookup"><span data-stu-id="edc54-200">Otherwise, hello evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with hello COMException (0x800AC472).</span></span> 

<span data-ttu-id="edc54-201">30 일의 평가 시간에 대 한 Excel 라이선스를 초기화할 수 있습니다: toohello 헤드 노드와 clusrun 로그온 `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` 모든 Excel에 HPC 클러스터 관리자를 통해 노드를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-201">You can rearm Excel for another 30 days of evaluation time: Log on toohello head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="edc54-202">평가 기간은 2회까지 연장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="edc54-203">그 후에는 유효한 Office 라이선스 키를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="edc54-204">Office Professional Plus 2013 hello VM 이미지에 설치 된 hello는 볼륨 버전으로는 제네릭 볼륨 라이선스 키 (GVLK).</span><span class="sxs-lookup"><span data-stu-id="edc54-204">hello Office Professional Plus 2013 installed on hello VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="edc54-205">KMS(키 관리 서비스)/AD-BA(Active Directory 기반 정품 인증) 또는 MAK(복수 정품 인증 키)를 통해 이 버전을 정품 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="edc54-206">toouse KMS/AD BA를 기존 KMS 서버를 사용 하거나 Microsoft Office 2013 볼륨 라이선스 팩 hello를 사용 하 여 새 것을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-206">toouse KMS/AD-BA, use an existing KMS server or set up a new one by using hello Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="edc54-207">(하려는 경우, 서버를 설정할 hello hello 헤드 노드에서.) 그런 다음 hello 인터넷을 통해 hello KMS 호스트 키 또는 전화를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-207">(If you want to, set up hello server on hello head node.) Then, activate hello KMS host key via hello Internet or telephone.</span></span> <span data-ttu-id="edc54-208">그런 다음 clusrun `ospp.vbs` tooset KMS 서버 쪽과 포트 hello 및 모든 hello Excel 계산 노드에서 Office를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-208">Then clusrun `ospp.vbs` tooset hello KMS server and port and activate Office on all hello Excel compute nodes.</span></span> 

    * <span data-ttu-id="edc54-209">MAK 첫 번째 clusrun toouse `ospp.vbs` tooinput 키 hello 한 다음 hello 인터넷 이나 전화를 통해 모든 hello Excel 계산 노드를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-209">toouse MAK, first clusrun `ospp.vbs` tooinput hello key and then activate all hello Excel compute nodes via hello Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="edc54-210">Office Professsional Plus 2013용 정품 키를 이 VM 이미지에 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="edc54-211">이 Office Professional Plus 2013 볼륨 버전 이외의 Office 또는 Excel 버전용 설치 미디어와 유효한 키가 있는 경우에는 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="edc54-212">먼저이 볼륨 버전을 제거 하 고 hello 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-212">First uninstall this volume edition and install hello edition that you have.</span></span> <span data-ttu-id="edc54-213">hello를 다시 설치 Excel 계산 노드는 대규모 배포에서 사용자 지정된 VM 이미지 toouse로 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-213">hello reinstalled Excel compute node can be captured as a customized VM image toouse in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="edc54-214">Excel 통합 문서 오프로드</span><span class="sxs-lookup"><span data-stu-id="edc54-214">Offload Excel workbooks</span></span>
<span data-ttu-id="edc54-215">Azure의 hello HPC Pack 클러스터에서 실행 되도록 이러한 단계가 toooffload Excel 통합 문서를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-215">Follow these steps toooffload an Excel workbook so that it runs on hello HPC Pack cluster in Azure.</span></span> <span data-ttu-id="edc54-216">toodo이를 Excel 2010 또는 2013 hello 클라이언트 컴퓨터에 이미 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-216">toodo this, you must have Excel 2010 or 2013 already installed on hello client computer.</span></span>

1. <span data-ttu-id="edc54-217">1 단계 toodeploy hello Excel로 HPC Pack 클러스터에서에서 hello 옵션 중 하나 사용 하 여 노드 이미지를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-217">Use one of hello options in Step 1 toodeploy an HPC Pack cluster with hello Excel compute node image.</span></span> <span data-ttu-id="edc54-218">Hello 클러스터 인증서 파일 (.cer) 및 클러스터 사용자 이름 및 암호를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-218">Obtain hello cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="edc54-219">Hello 클라이언트 컴퓨터의 Cert: \CurrentUser\Root 아래 hello 클러스터 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-219">On hello client computer, import hello cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="edc54-220">Excel이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-220">Make sure Excel is installed.</span></span> <span data-ttu-id="edc54-221">Hello hello에서 콘텐츠를 다음으로 Excel.exe.config 파일을 만들어 Excel.exe hello 클라이언트 컴퓨터에서 같은 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-221">Create an Excel.exe.config file with hello following contents in hello same folder as Excel.exe on hello client computer.</span></span> <span data-ttu-id="edc54-222">이 단계를 수행 하면 해당 hello HPC Pack 2012 R2 Excel COM 추가 기능에 성공적으로 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-222">This step ensures that hello HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="edc54-223">Hello 클라이언트 toosubmit 작업 toohello HPC Pack 클러스터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-223">Set up hello client toosubmit jobs toohello HPC Pack cluster.</span></span> <span data-ttu-id="edc54-224">한 가지 옵션은 전체 toodownload hello [HPC Pack 2012 R2 업데이트 3 설치](http://www.microsoft.com/download/details.aspx?id=49922) hello HPC Pack 클라이언트를 설치 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-224">One option is toodownload hello full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install hello HPC Pack client.</span></span> <span data-ttu-id="edc54-225">또는 다운로드 하 여 hello 설치 [HPC Pack 2012 R2 업데이트 3 클라이언트 유틸리티](https://www.microsoft.com/download/details.aspx?id=49923) Visual c + +의 적절 한 2010 재배포 가능 컴퓨터에 대 한 hello 및 ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span><span class="sxs-lookup"><span data-stu-id="edc54-225">Alternatively, download and install hello [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and hello appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="edc54-226">이 예제에서는 ConvertiblePricing_Complete.xlsb라는 샘플 Excel 통합 문서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="edc54-227">[여기](https://www.microsoft.com/en-us/download/details.aspx?id=2939)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="edc54-228">D:\Excel\Run 같은 hello Excel 통합 문서 tooa 작업 폴더를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-228">Copy hello Excel workbook tooa working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="edc54-229">Hello Excel 통합 문서를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-229">Open hello Excel workbook.</span></span> <span data-ttu-id="edc54-230">Hello에 **개발** 리본에서 클릭 **COM 추가 기능** 하 고 해당 hello HPC 팩 Excel COM 추가 기능에 성공적으로 로드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-230">On hello **Develop** ribbon, click **COM Add-Ins** and confirm that hello HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![HPC Pack용 Excel 추가 기능][addin]
8. <span data-ttu-id="edc54-232">Hello를 변경 하 여 편집 hello VBA 매크로 Excel에서 HPCControlMacros hello 스크립트 다음에 표시 된 대로 줄을 주석 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-232">Edit hello VBA macro HPCControlMacros in Excel by changing hello commented lines as shown in hello following script.</span></span> <span data-ttu-id="edc54-233">사용자 환경에 적절한 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-233">Substitute appropriate values for your environment.</span></span>
   
   ![HPC Pack용 Excel 매크로][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. <span data-ttu-id="edc54-235">D:\Excel\Upload 같은 hello Excel 통합 문서 tooan 업로드 디렉터리를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-235">Copy hello Excel workbook tooan upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="edc54-236">이 디렉터리는 hello VBA 매크로의 hello HPC_DependsFiles 상수에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-236">This directory is specified in hello HPC_DependsFiles constant in hello VBA macro.</span></span>
10. <span data-ttu-id="edc54-237">Azure의 hello 클러스터에서 toorun hello 통합 문서 클릭 hello **클러스터** hello 워크시트에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-237">toorun hello workbook on hello cluster in Azure, click hello **Cluster** button on hello worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="edc54-238">Excel UDF 실행</span><span class="sxs-lookup"><span data-stu-id="edc54-238">Run Excel UDFs</span></span>
<span data-ttu-id="edc54-239">Excel Udf toorun hello 클라이언트 컴퓨터를 1-3 tooset hello 이전 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-239">toorun Excel UDFs, follow hello preceding steps 1 – 3 tooset up hello client computer.</span></span> <span data-ttu-id="edc54-240">Excel Udf에 대 한 toohave hello Excel 응용 프로그램 계산 노드에 설치할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-240">For Excel UDFs, you don't need toohave hello Excel application installed on compute nodes.</span></span> <span data-ttu-id="edc54-241">때 클러스터를 만드는 계산 노드를 선택할 수 있도록 hello 대신 일반 컴퓨터 노드 이미지는 Excel 사용 하 여 노드 이미지를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of hello compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="edc54-242">34 문자 제한으로 hello Excel 2010 및 2013 클러스터 커넥터 대화 상자 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-242">There is a 34 character limit in hello Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="edc54-243">Hello Udf를 실행 하는이 대화 상자 toospecify hello 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-243">You use this dialog box toospecify hello cluster that runs hello UDFs.</span></span> <span data-ttu-id="edc54-244">Hello 전체 클러스터 이름이 긴 경우 (예를 들어 hpcexcelhn01.southeastasia.cloudapp.azure.com) hello 대화 상자에 맞지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-244">If hello full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in hello dialog box.</span></span> <span data-ttu-id="edc54-245">hello이 문제를 해결 tooset와 같은 시스템 수준의 변수 *CCP_IAASHN* hello 긴 클러스터 이름의 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-245">hello workaround is tooset a machine-wide variable such as *CCP_IAASHN* with hello value of hello long cluster name.</span></span> <span data-ttu-id="edc54-246">그런 다음 입력 *% CCP_IAASHN %* hello 클러스터 헤드 노드 이름으로 hello 대화 상자에서.</span><span class="sxs-lookup"><span data-stu-id="edc54-246">Then, enter *%CCP_IAASHN%* in hello dialog box as hello cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="edc54-247">Hello 클러스터 성공적으로 배포 된 후 계속 진행 단계 toorun 다음 hello 샘플 기본 제공 Excel UDF 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-247">After hello cluster is successfully deployed, continue with hello following steps toorun a sample built-in Excel UDF.</span></span> <span data-ttu-id="edc54-248">이러한 사용자 지정 된 Excel Udf 참조 [리소스](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild Xll hello 하 고 hello IaaS 클러스터에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLLs and deploy them on hello IaaS cluster.</span></span>

1. <span data-ttu-id="edc54-249">새 Excel 통합 문서를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-249">Open a new Excel workbook.</span></span> <span data-ttu-id="edc54-250">Hello에 **개발** 리본 메뉴를 클릭 **Add-ins**합니다. Hello 대화 상자에서 클릭 **찾아보기**toohello %CCP_HOME%Bin\XLL32 폴더를 찾아 hello 샘플 ClusterUDF32.xll를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-250">On hello **Develop** ribbon, click **Add-Ins**. Then, in hello dialog box, click **Browse**, navigate toohello %CCP_HOME%Bin\XLL32 folder, and select hello sample ClusterUDF32.xll.</span></span> <span data-ttu-id="edc54-251">Hello ClusterUDF32 존재 하지 않으면 hello가 클라이언트 컴퓨터에 hello 헤드 노드의 hello %CCP_HOME%Bin\XLL32 폴더에서 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-251">If hello ClusterUDF32 doesn't exist on hello client machine, copy it from hello %CCP_HOME%Bin\XLL32 folder on hello head node.</span></span>
   
   ![Hello UDF를 선택 합니다.][udf]
2. <span data-ttu-id="edc54-253">**파일** > **옵션** > **고급**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-253">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="edc54-254">아래 **수식**, 확인 **XLL 사용자 정의 함수 toorun 계산 클러스터 허용**합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-254">Under **Formulas**, check **Allow user-defined XLL functions toorun a compute cluster**.</span></span> <span data-ttu-id="edc54-255">클릭 **옵션** 에 hello 전체 클러스터 이름을 입력 하 고 **클러스터 헤드 노드 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-255">Then click **Options** and enter hello full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="edc54-256">(언급 하지 않는 이전에이 입력된 상자 이므로 제한 too34 문자 긴 클러스터 이름이 맞지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-256">(As noted previously this input box is limited too34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="edc54-257">여기서 긴 클러스터 이름에 대해 컴퓨터 전체 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-257">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![Hello UDF를 구성 합니다.][options]
3. <span data-ttu-id="edc54-259">toorun hello hello 클러스터에서 UDF 계산 값 =XllGetComputerNameC()를 사용 하 여 hello 셀을 클릭 하 고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-259">toorun hello UDF calculation on hello cluster, click hello cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="edc54-260">hello 함수는 단순히 UDF를 실행할는 hello hello 계산 노드의 hello 이름을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-260">hello function simply retrieves hello name of hello compute node on which hello UDF runs.</span></span> <span data-ttu-id="edc54-261">먼저 실행 하 여 hello에 대 한 hello 사용자 이름 및 암호 tooconnect toohello IaaS 클러스터에 대 한 자격 증명 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-261">For hello first run, a credentials dialog box prompts for hello username and password tooconnect toohello IaaS cluster.</span></span>
   
   ![UDF 실행][run]
   
   <span data-ttu-id="edc54-263">사용자가 셀 toocalculate 많은 경우 모든 셀에 대 Alt-Shift-Ctrl + F9 toorun hello 계산을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-263">When there are many cells toocalculate, press Alt-Shift-Ctrl + F9 toorun hello calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="edc54-264">3단계.</span><span class="sxs-lookup"><span data-stu-id="edc54-264">Step 3.</span></span> <span data-ttu-id="edc54-265">온-프레미스 클라이언트에서 SOA 작업 실행</span><span class="sxs-lookup"><span data-stu-id="edc54-265">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="edc54-266">toorun 일반 hello HPC Pack IaaS 클러스터에서 SOA 응용 프로그램 먼저 사용 hello 방법 중 하나에서 1 단계 toodeploy hello 클러스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-266">toorun general SOA applications on hello HPC Pack IaaS cluster, first use one of hello methods in Step 1 toodeploy hello cluster.</span></span> <span data-ttu-id="edc54-267">Excel hello 계산 노드에서 필요 하지 않으면이 예에서 일반 컴퓨터 노드 이미지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-267">Specify a generic compute node image in this case, because you do not need Excel on hello compute nodes.</span></span> <span data-ttu-id="edc54-268">이어서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-268">Then follow these steps.</span></span>

1. <span data-ttu-id="edc54-269">Hello 클러스터 인증서를 검색 한 후 Cert: \CurrentUser\Root 아래 hello 클라이언트 컴퓨터에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-269">After retrieving hello cluster certificate, import it on hello client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="edc54-270">Hello 설치 [HPC Pack 2012 R2 업데이트 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) 및 [HPC Pack 2012 R2 업데이트 3 클라이언트 유틸리티](https://www.microsoft.com/download/details.aspx?id=49923)합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-270">Install hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="edc54-271">이러한 도구는 toodevelop를 사용 하 고 SOA 클라이언트 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-271">These tools enable you toodevelop and run SOA client applications.</span></span>
3. <span data-ttu-id="edc54-272">Hello HelloWorldR2 다운로드 [샘플 코드](https://www.microsoft.com/download/details.aspx?id=41633)합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-272">Download hello HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="edc54-273">Visual Studio 2010에서 HelloWorldR2.sln hello 또는 2012를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-273">Open hello HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="edc54-274">(이 샘플은 보다 최신 버전의 Visual Studio와는 현재 호환되지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="edc54-274">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="edc54-275">먼저 hello EchoService 프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="edc54-275">Build hello EchoService project first.</span></span> <span data-ttu-id="edc54-276">그런 다음 hello 서비스 toohello IaaS 클러스터를 배포할 hello에 tooan 배포할 동일한 방식으로 온-프레미스 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-276">Then, deploy hello service toohello IaaS cluster in hello same way you deploy tooan on-premises cluster.</span></span> <span data-ttu-id="edc54-277">자세한 단계 HelloWordR2에 있으며 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="edc54-277">For detailed steps, see hello Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="edc54-278">수정 하 고 다음 섹션 toogenerate hello SOA 클라이언트 응용 프로그램을 Azure IaaS 클러스터에서를 실행 하는 hello에 설명 된 대로 HellWorldR2 hello 및 다른 프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="edc54-278">Modify and build hello HellWorldR2 and other projects as described in hello following section toogenerate hello SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="edc54-279">Azure 저장소 큐와 함께 HTTP 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="edc54-279">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="edc54-280">Azure 저장소 큐와 toouse Http 바인딩을 몇 가지 변경 toohello 샘플 코드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-280">toouse Http binding with an Azure storage queue, make a few changes toohello sample code.</span></span>

* <span data-ttu-id="edc54-281">Hello 클러스터 이름을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-281">Update hello cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="edc54-282">필요에 따라 hello 기본 TransportScheme SessionStartInfo에서 사용 하거나 tooHttp 명시적으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-282">Optionally, use hello default TransportScheme in SessionStartInfo or explicitly set it tooHttp.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="edc54-283">BrokerClient hello에 대 한 기본 바인딩을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-283">Use default binding for hello BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="edc54-284">또는 hello basicHttpBinding을 사용 하 여 명시적으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-284">Or set explicitly using hello basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="edc54-285">필요에 따라 SessionStartInfo에서 hello UseAzureQueue 플래그 tootrue를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-285">Optionally, set hello UseAzureQueue flag tootrue in SessionStartInfo.</span></span> <span data-ttu-id="edc54-286">그렇지 않으면 집합 설정 됩니다 tootrue 기본적으로 hello 클러스터 이름이 Azure 도메인 접미사를 포함 하 고 hello TransportScheme는 Http.</span><span class="sxs-lookup"><span data-stu-id="edc54-286">If not set, it will be set tootrue by default when hello cluster name has Azure domain suffixes and hello TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="edc54-287">Azure 저장소 큐 없이 HTTP 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="edc54-287">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="edc54-288">명시적으로 집합 hello UseAzureQueue 플래그 toofalse SessionStartInfo hello에는 Azure 저장소 큐를 사용 하지 않고 Http 바인딩을 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-288">toouse Http binding without an Azure storage queue, explicitly set hello UseAzureQueue flag toofalse in hello SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="edc54-289">NetTcp 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="edc54-289">Use NetTcp binding</span></span>
<span data-ttu-id="edc54-290">toouse NetTcp 바인딩 hello 구성은 tooconnecting tooan 온-프레미스 클러스터와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-290">toouse NetTcp binding, hello configuration is similar tooconnecting tooan on-premises cluster.</span></span> <span data-ttu-id="edc54-291">Hello 헤드 노드 VM의 몇 가지 끝점 tooopen 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-291">You need tooopen a few endpoints on hello head node VM.</span></span> <span data-ttu-id="edc54-292">Hello HPC Pack IaaS 배포 스크립트 toocreate hello 클러스터를 사용 하는 경우 예를 들어 hello 끝점 집합 hello Azure 포털 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-292">If you used hello HPC Pack IaaS deployment script toocreate hello cluster, for example, set hello endpoints in hello Azure portal as follows.</span></span>

1. <span data-ttu-id="edc54-293">Hello VM을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-293">Stop hello VM.</span></span>
2. <span data-ttu-id="edc54-294">Hello TCP 포트 9090, 9087, 추가, 9091 9094 hello 세션에 대 한 Broker, 작업자 및 데이터 서비스를 각각 Broker</span><span class="sxs-lookup"><span data-stu-id="edc54-294">Add hello TCP ports 9090, 9087, 9091, 9094 for hello Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![끝점 구성][endpoint-new-portal]
3. <span data-ttu-id="edc54-296">Hello VM을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-296">Start hello VM.</span></span>

<span data-ttu-id="edc54-297">hello SOA 클라이언트 응용 프로그램에는 hello 헤드 이름 toohello IaaS 클러스터 전체 이름을 변경 하는 제외 하 고 변경 하지 않고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="edc54-297">hello SOA client application requires no changes except altering hello head name toohello IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="edc54-298">다음 단계</span><span class="sxs-lookup"><span data-stu-id="edc54-298">Next steps</span></span>
* <span data-ttu-id="edc54-299">HPC 팩을 사용하여 Excel 작업을 실행하는 방법에 대한 자세한 내용은 [이러한 리소스](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edc54-299">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="edc54-300">HPC 팩을 사용하여 SOA 서비스를 배포 및 관리하는 방법에 대한 자세한 내용은 [Microsoft HPC 팩에서 SOA 서비스 관리](https://technet.microsoft.com/library/ff919412.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edc54-300">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
