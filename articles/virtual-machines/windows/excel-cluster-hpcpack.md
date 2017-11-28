---
title: "Excel 및 SOA를 위한 HPC 팩 클러스터 | Microsoft Docs"
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
ms.openlocfilehash: 63babd94fdab15217cfb0757e4cd6efe458a628d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="e7927-103">Azure의 HPC Pack 클러스터에서 Excel 및 SOA 작업 실행 시작</span><span class="sxs-lookup"><span data-stu-id="e7927-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="e7927-104">이 문서에서는 Azure 빠른 시작 템플릿 또는 Azure PowerShell 배포 스크립트(선택 사항)를 사용하여 Azure 가상 컴퓨터에 Microsoft HPC Pack 2012 R2 클러스터를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-104">This article shows you how to deploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="e7927-105">이 클러스터는 HPC Pack을 사용하여 Microsoft Excel 또는 SOA(서비스 지향 아키텍처) 작업을 실행하도록 설계된 Azure Marketplace VM 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-105">The cluster uses Azure Marketplace VM images designed to run Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="e7927-106">클러스터를 사용하여 온-프레미스 클라이언트 컴퓨터에서 Excel HPC 및 SOA 서비스를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-106">You can use the cluster to run Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="e7927-107">Excel HPC 서비스에는 Excel 통합 문서 오프로딩 및 Excel 사용자 정의 함수, 즉 UDF가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-107">The Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e7927-108">이 문서는 HPC Pack 2012 R2의 기능, 템플릿 및 스크립트를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="e7927-109">이 시나리오는 현재 HPC Pack 2016에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="e7927-110">다음 다이어그램은 만들려는 HPC Pack 클러스터를 개략적으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-110">At a high level, the following diagram shows the HPC Pack cluster you create.</span></span>

![Excel 작업을 실행하는 노드가 있는 HPC 클러스터][scenario]

## <a name="prerequisites"></a><span data-ttu-id="e7927-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e7927-112">Prerequisites</span></span>
* <span data-ttu-id="e7927-113">**클라이언트 컴퓨터** -클러스터에 샘플 Excel 및 SOA 작업을 제출하기 위한 Windows 기반 클라이언트 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-113">**Client computer** - You need a Windows-based client computer to submit sample Excel and SOA jobs to the cluster.</span></span> <span data-ttu-id="e7927-114">또한 Azure PowerShell 클러스터 배포 방법을 선택하는 경우 해당 배포 스크립트를 실행하기 위한 Windows 컴퓨터도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-114">You also need a Windows computer to run the Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="e7927-115">**Azure 구독** - Azure 구독이 없는 경우 몇 분 만에 [무료 계정](https://azure.microsoft.com/pricing/free-trial/) 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="e7927-116">**코어 할당량** - 멀티 코어 VM 크기를 사용하여 여러 클러스터 노드를 배포하려는 경우 특히 코어 할당량을 늘려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-116">**Cores quota** - You might need to increase the quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="e7927-117">Azure 빠른 시작 템플릿을 사용하는 경우 Azure 지역별로 Resource Manager의 코어 할당량이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-117">If you are using an Azure quickstart template, the cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="e7927-118">이 경우 특정 지역의 할당량을 늘려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-118">In that case, you might need to increase the quota in a specific region.</span></span> <span data-ttu-id="e7927-119">[Azure 구독 제한, 할당량 및 제약 조건](../../azure-subscription-service-limits.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7927-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="e7927-120">할당량을 늘리려면 무료로 [온라인 고객 지원 요청을 개설](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-120">To increase a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="e7927-121">**Microsoft Office 라이선스** - Microsoft Excel과 함께 마켓플레이스 HPC Pack 2012 R2 VM 이미지를 사용하여 컴퓨터 노드를 배포하는 경우 30일 평가 버전의 Microsoft Excel Professional Plus 2013이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="e7927-122">평가 기간이 종료된 후에 작업을 계속 실행하기 위해 Excel을 정품 인증하려면 유효한 Microsoft Office 라이선스를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-122">After the evaluation period, you need to provide a valid Microsoft Office license to activate Excel to continue to run workloads.</span></span> <span data-ttu-id="e7927-123">이 문서의 뒷부분에 나오는 [Excel 활성화](#excel-activation) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7927-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="e7927-124">1단계.</span><span class="sxs-lookup"><span data-stu-id="e7927-124">Step 1.</span></span> <span data-ttu-id="e7927-125">Azure에서 HPC Pack 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="e7927-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="e7927-126">여기서는 HPC Pack 2012 R2 클러스터를 설정하는 두 가지 방법을 설명합니다. 첫 번째 방법은 Azure 빠른 시작 템플릿과 Azure 포털을 사용하는 것이고, 두 번째 방법은 Azure PowerShell 배포 스크립트를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-126">We show two options to set up the HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and the Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="e7927-127">옵션 1.</span><span class="sxs-lookup"><span data-stu-id="e7927-127">Option 1.</span></span> <span data-ttu-id="e7927-128">빠른 시작 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="e7927-128">Use a quickstart template</span></span>
<span data-ttu-id="e7927-129">Azure 빠른 시작 템플릿을 사용하여 Azure 포털에서 HPC Pack 클러스터를 빠르게 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-129">Use an Azure quickstart template to quickly deploy an HPC Pack cluster in the Azure portal.</span></span> <span data-ttu-id="e7927-130">포털에서 템플릿을 열면 클러스터에 대한 설정을 입력할 수 있는 간단한 UI가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-130">When you open the template in the portal, you get a simple UI where you enter the settings for your cluster.</span></span> <span data-ttu-id="e7927-131">단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-131">Here are the steps.</span></span> 

> [!TIP]
> <span data-ttu-id="e7927-132">원하는 경우 Excel 작업 전용으로 유사한 클러스터를 만드는 [Azure Marketplace 템플릿](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="e7927-133">단계는 다음과 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-133">The steps differ slightly from the following.</span></span>
> 
> 

1. <span data-ttu-id="e7927-134">[GitHub의 HPC 클러스터 만들기 템플릿 페이지](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-134">Visit the [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="e7927-135">원하는 경우 템플릿 및 소스 코드에 대한 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-135">If you want, review information about the template and the source code.</span></span>
2. <span data-ttu-id="e7927-136">Azure에 배포를 클릭하면 Azure 포털의 템플릿을 사용하여 **배포** 를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-136">Click **Deploy to Azure** to start a deployment with the template in the Azure portal.</span></span>
   
   ![Azure에 템플릿 배포][github]
3. <span data-ttu-id="e7927-138">포털에서 다음 단계에 따라 HPC 클러스터 템플릿에 대한 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-138">In the portal, follow these steps to enter the parameters for the HPC cluster template.</span></span>
   
   <span data-ttu-id="e7927-139">a.</span><span class="sxs-lookup"><span data-stu-id="e7927-139">a.</span></span> <span data-ttu-id="e7927-140">**매개 변수** 페이지에서 템플릿 매개 변수의 값을 입력하거나 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-140">On the **Parameters** page, enter or modify values for the template parameters.</span></span> <span data-ttu-id="e7927-141">도움말 정보를 보려면 각 설정 옆에 있는 아이콘을 클릭합니다. 다음 화면에는 샘플 값이 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-141">(Click the icon next to each setting for help information.) Sample values are shown in the following screen.</span></span> <span data-ttu-id="e7927-142">이 예제에서는 *hpc.local* 도메인에 헤드 노드 1개와 컴퓨터 노드 2개로 구성된 *hpc01*이라는 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-142">This example creates a cluster named *hpc01* in the *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="e7927-143">컴퓨터 노드는 Microsoft Excel을 포함하는 HPC Pack VM 이미지에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-143">The compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![매개 변수 입력][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="e7927-145">헤드 노드 VM은 Windows Server 2012 R2에서 HPC Pack 2012 R2의 [최신 마켓플레이스 이미지](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) 로부터 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-145">The head node VM is created automatically from the [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="e7927-146">현재 이미지는 HPC Pack 2012 R2 업데이트 3을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-146">Currently the image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="e7927-147">컴퓨터 노드 VM은 선택한 컴퓨터 노드 제품군의 최신 이미지로부터 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-147">Compute node VMs are created from the latest image of the selected compute node family.</span></span> <span data-ttu-id="e7927-148">Microsoft Excel Professional Plus 2013 평가 버전을 포함하는 최신 HPC 팩 계산 노드 이미지에 대해 **ComputeNodeWithExcel** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-148">Select the **ComputeNodeWithExcel** option for the latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="e7927-149">일반 SOA 세션 또는 Excel UDF 오프로딩용 클러스터를 배포하려면 Excel을 설치하지 않고 **ComputeNode** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-149">To deploy a cluster for general SOA sessions or for Excel UDF offloading, choose the **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="e7927-150">b.</span><span class="sxs-lookup"><span data-stu-id="e7927-150">b.</span></span> <span data-ttu-id="e7927-151">구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-151">Choose the subscription.</span></span>
   
   <span data-ttu-id="e7927-152">c.</span><span class="sxs-lookup"><span data-stu-id="e7927-152">c.</span></span> <span data-ttu-id="e7927-153">*hpc01RG*와 같은 클러스터용 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-153">Create a resource group for the cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="e7927-154">d.</span><span class="sxs-lookup"><span data-stu-id="e7927-154">d.</span></span> <span data-ttu-id="e7927-155">리소스 그룹의 위치(예: 미국 중부)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-155">Choose a location for the resource group, such as Central US.</span></span>
   
   <span data-ttu-id="e7927-156">e.</span><span class="sxs-lookup"><span data-stu-id="e7927-156">e.</span></span> <span data-ttu-id="e7927-157">**약관** 페이지에서 약관 내용을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-157">On the **Legal terms** page, review the terms.</span></span> <span data-ttu-id="e7927-158">해당 내용에 동의하는 경우 **구매**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="e7927-159">그런 다음 템플릿에 대한 값 설정을 마쳤으면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-159">Then, when you are finished setting the values for the template, click **Create**.</span></span>
4. <span data-ttu-id="e7927-160">배포가 완료되면(일반적으로 약 30분 소요) 클러스터 헤드 노드에서 클러스터 인증서 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-160">When the deployment completes (it typically takes around 30 minutes), export the cluster certificate file from the cluster head node.</span></span> <span data-ttu-id="e7927-161">이후 단계에서 보안 HTTP 바인딩을 위한 서버 쪽 인증을 제공하기 위해 클라이언트 컴퓨터에서 이 공용 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-161">In a later step, you import this public certificate on the client computer to provide the server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="e7927-162">a.</span><span class="sxs-lookup"><span data-stu-id="e7927-162">a.</span></span> <span data-ttu-id="e7927-163">Azure Portal에서 대시보드로 이동하여 헤드 노드를 선택하고, 원격 데스크톱을 사용하여 연결하려면 페이지 위쪽에 있는 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-163">In the Azure portal, go to the dashboard, select the head node, and click **Connect** at the top of the page to connect using Remote Desktop.</span></span>
   
    <!-- ![Connect to the head node][connect] -->
   
   <span data-ttu-id="e7927-164">b.</span><span class="sxs-lookup"><span data-stu-id="e7927-164">b.</span></span> <span data-ttu-id="e7927-165">인증서 관리자의 표준 절차에 따라 개인 키 없이 Cert:\LocalMachine\My 아래에 있는 헤드 노드 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-165">Use standard procedures in Certificate Manager to export the head node certificate (located under Cert:\LocalMachine\My) without the private key.</span></span> <span data-ttu-id="e7927-166">이 예제에서는 *CN = hpc01.eastus.cloudapp.azure.com*을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![인증서 내보내기][cert]

### <a name="option-2-use-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="e7927-168">옵션 2.</span><span class="sxs-lookup"><span data-stu-id="e7927-168">Option 2.</span></span> <span data-ttu-id="e7927-169">HPC Pack IaaS 배포 스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="e7927-169">Use the HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="e7927-170">HPC Pack IaaS 배포 스크립트는 HPC Pack 클러스터를 배포하는 다른 유용한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-170">The HPC Pack IaaS deployment script provides another versatile way to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="e7927-171">템플릿이 Azure Resource Manager 배포 모델을 사용하는 반면 클래식 배포 모델에서 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-171">It creates a cluster in the classic deployment model, whereas the template uses the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="e7927-172">또한 스크립트는 Azure Global 또는 Azure China 서비스의 구독과 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-172">Also, the script is compatible with a subscription in either the Azure Global or Azure China service.</span></span>

<span data-ttu-id="e7927-173">**추가 필수 조건**</span><span class="sxs-lookup"><span data-stu-id="e7927-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="e7927-174">**Azure PowerShell** - [Azure PowerShell(버전 0.8.10 이상)을 설치 및 구성](/powershell/azure/overview) 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="e7927-175">**HPC Pack IaaS 배포 스크립트** - [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=44949)에서 최신 버전의 스크립트를 다운로드하고 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-175">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="e7927-176">`New-HPCIaaSCluster.ps1 –Version`을 실행하여 스크립트 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-176">Check the version of the script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="e7927-177">이 문서는 4.5.0 이상 버전의 스크립트를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-177">This article is based on version 4.5.0 or later of the script.</span></span>

<span data-ttu-id="e7927-178">**구성 파일 만들기**</span><span class="sxs-lookup"><span data-stu-id="e7927-178">**Create the configuration file**</span></span>

 <span data-ttu-id="e7927-179">HPC Pack IaaS 배포 스크립트는 HPC 클러스터의 인프라를 설명하는 XML 구성 파일을 입력으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-179">The HPC Pack IaaS deployment script uses an XML configuration file as input that describes the infrastructure of the HPC cluster.</span></span> <span data-ttu-id="e7927-180">Microsoft Excel을 포함하는 컴퓨터 노드 이미지에서 만든 컴퓨터 노드 18개와 헤드 노드 1개로 구성된 클러스터를 배포하려면 다음 샘플 구성 파일에 해당 환경의 값을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-180">To deploy a cluster consisting of a head node and 18 compute nodes created from the compute node image that includes Microsoft Excel, substitute values for your environment into the following sample configuration file.</span></span> <span data-ttu-id="e7927-181">구성 파일에 대한 자세한 내용은 스크립트 폴더의 Manual.rtf 파일과 [HPC 팩 IaaS 배포 스크립트를 사용하여 HPC 클러스터 만들기](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7927-181">For more information about the configuration file, see the Manual.rtf file in the script folder and [Create an HPC cluster with the HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

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

<span data-ttu-id="e7927-182">**구성 파일에 대한 참고 사항**</span><span class="sxs-lookup"><span data-stu-id="e7927-182">**Notes about the configuration file**</span></span>

* <span data-ttu-id="e7927-183">헤드 노드의 **VMName**은 **ServiceName**과 **같아야** 합니다. 그렇지 않으면 SOA 작업이 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-183">The **VMName** of the head node **MUST** be the same as the **ServiceName**, or SOA jobs fail to run.</span></span>
* <span data-ttu-id="e7927-184">헤드 노드 인증서를 생성하고 내보내도록 **EnableWebPortal** 을 지정하세요.</span><span class="sxs-lookup"><span data-stu-id="e7927-184">Make sure you specify **EnableWebPortal** so that the head node certificate is generated and exported.</span></span>
* <span data-ttu-id="e7927-185">이 파일은 헤드 노드에서 실행되는 구성 후 PowerShell 스크립트 PostConfig.ps1을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-185">The file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on the head node.</span></span> <span data-ttu-id="e7927-186">다음 샘플 스크립트는 Azure Storage 연결 문자열을 구성하고, 헤드 노드에서 컴퓨터 노드 역할을 제거하고, 배포된 모든 노드를 온라인으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-186">THe following sample script configures the Azure storage connection string, removes the compute node role from the head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add the HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set the Azure storage connection string for the cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove the compute node role for head node to make sure the Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in the deployment including the head node and compute nodes, which should match the number specified in the XML configuration file
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

<span data-ttu-id="e7927-187">**스크립트 실행**</span><span class="sxs-lookup"><span data-stu-id="e7927-187">**Run the script**</span></span>

1. <span data-ttu-id="e7927-188">관리자 권한으로 클라이언트 컴퓨터에서 PowerShell 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-188">Open the PowerShell console on the client computer as an administrator.</span></span>
2. <span data-ttu-id="e7927-189">디렉터리를 스크립트 폴더(이 예제에서는 E:\IaaSClusterScript)로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-189">Change directory to the script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="e7927-190">HPC Pack 클러스터를 배포하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-190">To deploy the HPC Pack cluster, run the following command.</span></span> <span data-ttu-id="e7927-191">이 예제에서는 구성 파일이 E:\HPCDemoConfig.xml에 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-191">This example assumes that the configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="e7927-192">HPC Pack 배포 스크립트가 일정 시간 동안 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-192">The HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="e7927-193">스크립트에서 수행하는 작업 중 하나는 클러스터 인증서를 다운로드하여 클라이언트 컴퓨터에 있는 현재 사용자의 Documents 폴더에 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-193">One thing the script does is to export and download the cluster certificate and save it in the current user’s Documents folder on the client computer.</span></span> <span data-ttu-id="e7927-194">이 스크립트는 다음과 유사한 메시지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-194">The script generates a message similar to the following.</span></span> <span data-ttu-id="e7927-195">다음 단계에서는 해당 인증서 저장소의 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-195">In a following step, you import the certificate in the appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import the following certificate in the Trusted Root Certification Authorities certificate store on the computer where you are submitting job or accessing the HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="e7927-196">2단계.</span><span class="sxs-lookup"><span data-stu-id="e7927-196">Step 2.</span></span> <span data-ttu-id="e7927-197">온-프레미스 클라이언트에서 Excel 통합 문서 오프로드 및 UDF 실행</span><span class="sxs-lookup"><span data-stu-id="e7927-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="e7927-198">Excel 활성화</span><span class="sxs-lookup"><span data-stu-id="e7927-198">Excel activation</span></span>
<span data-ttu-id="e7927-199">프로덕션 작업에 대해 ComputeNodeWithExcel VM 이미지를 사용하는 경우 컴퓨터 노드에서 Excel을 정품 인증하려면 유효한 Microsoft Office 라이선스 키를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-199">When using the ComputeNodeWithExcel VM image for production workloads, you need to provide a valid Microsoft Office license key to activate Excel on the compute nodes.</span></span> <span data-ttu-id="e7927-200">이렇게 하지 않으면 평가 버전의 Excel은 30일 후에 만료되며 Excel 통합 문서 실행이 실패하고 COMException(0x800AC472)이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-200">Otherwise, the evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with the COMException (0x800AC472).</span></span> 

<span data-ttu-id="e7927-201">Excel의 평가 기간은 30일 연장할 수 있습니다. 이렇게 하려면 헤드 노드에 로그온한 다음 HPC 클러스터 관리자를 통해 모든 Excel 컴퓨터 노드에서 `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-201">You can rearm Excel for another 30 days of evaluation time: Log on to the head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="e7927-202">평가 기간은 2회까지 연장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="e7927-203">그 후에는 유효한 Office 라이선스 키를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="e7927-204">VM 이미지에 설치되어 있는 Office Professional Plus 2013은 GVLK(일반 볼륨 라이선스 키)를 사용하는 볼륨 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-204">The Office Professional Plus 2013 installed on the VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="e7927-205">KMS(키 관리 서비스)/AD-BA(Active Directory 기반 정품 인증) 또는 MAK(복수 정품 인증 키)를 통해 이 버전을 정품 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="e7927-206">KMS/AD-BA를 사용하려면 기존 KMS 서버를 사용하거나 Microsoft Office 2013 볼륨 라이선스 팩을 사용하여 새 서버를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-206">To use KMS/AD-BA, use an existing KMS server or set up a new one by using the Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="e7927-207">(원하는 경우 헤드 노드에서 서버를 설정합니다.) 그런 다음 인터넷이나 전화를 통해 KMS 호스트 키를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-207">(If you want to, set up the server on the head node.) Then, activate the KMS host key via the Internet or telephone.</span></span> <span data-ttu-id="e7927-208">그런 다음 clusrun `ospp.vbs`은 KMS 서버 및 포트를 설정하고 Excel 계산 노드의 Office를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-208">Then clusrun `ospp.vbs` to set the KMS server and port and activate Office on all the Excel compute nodes.</span></span> 

    * <span data-ttu-id="e7927-209">MAK를 사용하여 첫 번째 clusrun `ospp.vbs`은 키를 입력한 다음 인터넷이나 전화를 통해 모든 Excel 계산 노드를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-209">To use MAK, first clusrun `ospp.vbs` to input the key and then activate all the Excel compute nodes via the Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="e7927-210">Office Professsional Plus 2013용 정품 키를 이 VM 이미지에 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="e7927-211">이 Office Professional Plus 2013 볼륨 버전 이외의 Office 또는 Excel 버전용 설치 미디어와 유효한 키가 있는 경우에는 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="e7927-212">이렇게 하려면 먼저 이 볼륨 버전을 제거한 후에 소유 중인 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-212">First uninstall this volume edition and install the edition that you have.</span></span> <span data-ttu-id="e7927-213">다시 설치된 Excel 계산 노드를 대규모로 배포에서 사용할 사용자 지정 VM 이미지로 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-213">The reinstalled Excel compute node can be captured as a customized VM image to use in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="e7927-214">Excel 통합 문서 오프로드</span><span class="sxs-lookup"><span data-stu-id="e7927-214">Offload Excel workbooks</span></span>
<span data-ttu-id="e7927-215">Azure의 HPC Pack 클러스터에서 실행되도록 다음 단계에 따라 Excel 통합 문서를 오프로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-215">Follow these steps to offload an Excel workbook so that it runs on the HPC Pack cluster in Azure.</span></span> <span data-ttu-id="e7927-216">이렇게 하려면 Excel 2010 또는 2013이 클라이언트 컴퓨터에 이미 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-216">To do this, you must have Excel 2010 or 2013 already installed on the client computer.</span></span>

1. <span data-ttu-id="e7927-217">1단계의 옵션 중 하나를 사용하여 Excel 컴퓨터 노드 이미지로 HPC Pack 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-217">Use one of the options in Step 1 to deploy an HPC Pack cluster with the Excel compute node image.</span></span> <span data-ttu-id="e7927-218">클러스터 인증서 파일(.cer) 및 클러스터 사용자 이름과 암호를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-218">Obtain the cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="e7927-219">클라이언트 컴퓨터에서 Cert:\CurrentUser\Root 아래의 클러스터 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-219">On the client computer, import the cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="e7927-220">Excel이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-220">Make sure Excel is installed.</span></span> <span data-ttu-id="e7927-221">클라이언트 컴퓨터에서 Excel.exe와 동일한 폴더에 다음과 같은 내용으로 Excel.exe.config 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-221">Create an Excel.exe.config file with the following contents in the same folder as Excel.exe on the client computer.</span></span> <span data-ttu-id="e7927-222">이 단계를 수행하면 HPC Pack 2012 R2 Excel COM 추가 기능이 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-222">This step ensures that the HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="e7927-223">HPC Pack 클러스터에 작업을 제출하도록 클라이언트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-223">Set up the client to submit jobs to the HPC Pack cluster.</span></span> <span data-ttu-id="e7927-224">이렇게 설정하는 옵션 중 하나는 전체 [HPC Pack 2012 R2 업데이트 3 설치](http://www.microsoft.com/download/details.aspx?id=49922) 파일을 다운로드한 다음 HPC Pack 클라이언트를 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-224">One option is to download the full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install the HPC Pack client.</span></span> <span data-ttu-id="e7927-225">[HPC 팩 2012 R2 업데이트 3 클라이언트 유틸리티](https://www.microsoft.com/download/details.aspx?id=49923) 및 사용 중인 컴퓨터에 적합한 Visual C++ 2010 재배포 가능 패키지([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555))를 다운로드하여 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-225">Alternatively, download and install the [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and the appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="e7927-226">이 예제에서는 ConvertiblePricing_Complete.xlsb라는 샘플 Excel 통합 문서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="e7927-227">[여기](https://www.microsoft.com/en-us/download/details.aspx?id=2939)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="e7927-228">D:\Excel\Run과 같은 작업 폴더에 Excel 통합 문서를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-228">Copy the Excel workbook to a working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="e7927-229">Excel 통합 문서를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-229">Open the Excel workbook.</span></span> <span data-ttu-id="e7927-230">**개발** 리본에서 **COM 추가 기능**을 클릭하고 HPC 팩 Excel COM 추가 기능이 로드되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-230">On the **Develop** ribbon, click **COM Add-Ins** and confirm that the HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![HPC Pack용 Excel 추가 기능][addin]
8. <span data-ttu-id="e7927-232">주석으로 처리된 줄을 다음 스크립트와 같이 변경하여 Excel에서 VBA 매크로 HPCControlMacros를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-232">Edit the VBA macro HPCControlMacros in Excel by changing the commented lines as shown in the following script.</span></span> <span data-ttu-id="e7927-233">사용자 환경에 적절한 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-233">Substitute appropriate values for your environment.</span></span>
   
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
9. <span data-ttu-id="e7927-235">Excel 통합 문서를 D:\Excel\Upload와 같은 업로드 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-235">Copy the Excel workbook to an upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="e7927-236">이 디렉터리는 VBA 매크로의 HPC_DependsFiles 상수에 지정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-236">This directory is specified in the HPC_DependsFiles constant in the VBA macro.</span></span>
10. <span data-ttu-id="e7927-237">Azure의 클러스터에서 통합 문서를 실행하려면 워크시트의 **클러스터** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-237">To run the workbook on the cluster in Azure, click the **Cluster** button on the worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="e7927-238">Excel UDF 실행</span><span class="sxs-lookup"><span data-stu-id="e7927-238">Run Excel UDFs</span></span>
<span data-ttu-id="e7927-239">Excel UDF를 실행하려면 앞의 1-3단계에 따라 클라이언트 컴퓨터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-239">To run Excel UDFs, follow the preceding steps 1 – 3 to set up the client computer.</span></span> <span data-ttu-id="e7927-240">Excel UDF의 경우 컴퓨터 노드에 Excel 응용 프로그램을 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-240">For Excel UDFs, you don't need to have the Excel application installed on compute nodes.</span></span> <span data-ttu-id="e7927-241">따라서 클러스터 컴퓨터 노드를 만들 때 Excel이 포함된 컴퓨터 노드 이미지가 아닌 일반 컴퓨터 노드 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of the compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="e7927-242">Excel 2010 및 2013 클러스터 커넥터 대화 상자에는 34자 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-242">There is a 34 character limit in the Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="e7927-243">이 대화 상자를 사용하여 UDF를 실행하는 클러스터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-243">You use this dialog box to specify the cluster that runs the UDFs.</span></span> <span data-ttu-id="e7927-244">전체 클러스터 이름이 hpcexcelhn01.southeastasia.cloudapp.azure.com과 같이 제한보다 더 긴 경우에는 대화 상자에서 입력할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-244">If the full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in the dialog box.</span></span> <span data-ttu-id="e7927-245">이러한 문제를 해결하려면 긴 클러스터 이름의 값을 사용해 *CCP_IAASHN*과 같은 컴퓨터 전체 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-245">The workaround is to set a machine-wide variable such as *CCP_IAASHN* with the value of the long cluster name.</span></span> <span data-ttu-id="e7927-246">그런 다음 대화 상자에 *%CCP_IAASHN%*를 클러스터 헤드 노드 이름으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-246">Then, enter *%CCP_IAASHN%* in the dialog box as the cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="e7927-247">클러스터가 배포된 후 다음 단계를 계속 진행하여 샘플 기본 제공 Excel UDF를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-247">After the cluster is successfully deployed, continue with the following steps to run a sample built-in Excel UDF.</span></span> <span data-ttu-id="e7927-248">사용자 지정 Excel UDF의 경우 다음 [리소스](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) 를 참조하여 XLL을 빌드하고 IaaS 클러스터에 배포하세요.</span><span class="sxs-lookup"><span data-stu-id="e7927-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) to build the XLLs and deploy them on the IaaS cluster.</span></span>

1. <span data-ttu-id="e7927-249">새 Excel 통합 문서를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-249">Open a new Excel workbook.</span></span> <span data-ttu-id="e7927-250">**개발** 리본 메뉴에서 **추가 기능**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-250">On the **Develop** ribbon, click **Add-Ins**.</span></span> <span data-ttu-id="e7927-251">그런 다음 대화 상자에서 **찾아보기**를 클릭하고 %CCP_HOME%Bin\XLL32 폴더로 이동한 다음 샘플 ClusterUDF32.xll을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-251">Then, in the dialog box, click **Browse**, navigate to the %CCP_HOME%Bin\XLL32 folder, and select the sample ClusterUDF32.xll.</span></span> <span data-ttu-id="e7927-252">클라이언트 컴퓨터에 ClusterUDF32가 없는 경우 헤드 노드의 %CCP_HOME%Bin\XLL32폴더에서 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-252">If the ClusterUDF32 doesn't exist on the client machine, copy it from the %CCP_HOME%Bin\XLL32 folder on the head node.</span></span>
   
   ![UDF 선택][udf]
2. <span data-ttu-id="e7927-254">**파일** > **옵션** > **고급**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-254">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="e7927-255">**수식** 아래에서 **사용자 정의 XLL 함수가 계산 클러스터를 실행할 수 있도록 허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-255">Under **Formulas**, check **Allow user-defined XLL functions to run a compute cluster**.</span></span> <span data-ttu-id="e7927-256">그런 다음 **옵션**을 클릭하고 **클러스터 헤드 노드 이름**에 전체 클러스터 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-256">Then click **Options** and enter the full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="e7927-257">앞에서 언급한 대로 이 입력 상자는 34자로 제한되므로 긴 클러스터 이름은 맞지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-257">(As noted previously this input box is limited to 34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="e7927-258">여기서 긴 클러스터 이름에 대해 컴퓨터 전체 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-258">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![UDF 구성][options]
3. <span data-ttu-id="e7927-260">클러스터에서 UDF 계산을 실행하려면 값이 =XllGetComputerNameC()인 셀을 클릭하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-260">To run the UDF calculation on the cluster, click the cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="e7927-261">이 함수는 UDF가 실행되는 컴퓨터 노드의 이름만 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-261">The function simply retrieves the name of the compute node on which the UDF runs.</span></span> <span data-ttu-id="e7927-262">처음 실행하는 경우 자격 증명 대화 상자에 IaaS 클러스터에 연결할 사용자 이름 및 암호를 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-262">For the first run, a credentials dialog box prompts for the username and password to connect to the IaaS cluster.</span></span>
   
   ![UDF 실행][run]
   
   <span data-ttu-id="e7927-264">계산할 셀이 많은 경우 Alt+Shift+Ctrl+F9를 눌러 모든 셀에서 계산을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-264">When there are many cells to calculate, press Alt-Shift-Ctrl + F9 to run the calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="e7927-265">3단계.</span><span class="sxs-lookup"><span data-stu-id="e7927-265">Step 3.</span></span> <span data-ttu-id="e7927-266">온-프레미스 클라이언트에서 SOA 작업 실행</span><span class="sxs-lookup"><span data-stu-id="e7927-266">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="e7927-267">HPC Pack IaaS 클러스터에서 일반 SOA 응용 프로그램을 실행하려면 먼저 1단계에서 설명한 방법 중 하나를 사용하여 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-267">To run general SOA applications on the HPC Pack IaaS cluster, first use one of the methods in Step 1 to deploy the cluster.</span></span> <span data-ttu-id="e7927-268">컴퓨터 노드에는 Excel이 필요하지 않으므로 이 경우에는 일반 컴퓨터 노드 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-268">Specify a generic compute node image in this case, because you do not need Excel on the compute nodes.</span></span> <span data-ttu-id="e7927-269">이어서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-269">Then follow these steps.</span></span>

1. <span data-ttu-id="e7927-270">클러스터 인증서를 검색한 후 클라이언트 컴퓨터의 Cert:\CurrentUser\Root 아래로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-270">After retrieving the cluster certificate, import it on the client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="e7927-271">[HPC 팩 2012 R2 업데이트 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) 및 [HPC 팩 2012 R2 업데이트 3 클라이언트 유틸리티](https://www.microsoft.com/download/details.aspx?id=49923)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-271">Install the [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="e7927-272">이러한 도구를 사용하면 SOA 클라이언트 응용 프로그램을 개발하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-272">These tools enable you to develop and run SOA client applications.</span></span>
3. <span data-ttu-id="e7927-273">HelloWorldR2 [샘플 코드](https://www.microsoft.com/download/details.aspx?id=41633)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-273">Download the HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="e7927-274">Visual Studio 2010 또는 2012에서 HelloWorldR2.sln을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-274">Open the HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="e7927-275">(이 샘플은 보다 최신 버전의 Visual Studio와는 현재 호환되지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="e7927-275">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="e7927-276">먼저 EchoService 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-276">Build the EchoService project first.</span></span> <span data-ttu-id="e7927-277">그런 다음 온-프레미스 클러스터에 배포하는 것과 같은 방식으로 서비스를 IaaS 클러스터에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-277">Then, deploy the service to the IaaS cluster in the same way you deploy to an on-premises cluster.</span></span> <span data-ttu-id="e7927-278">자세한 단계는 HelloWordR2의 Readme.doc를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7927-278">For detailed steps, see the Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="e7927-279">다음 섹션의 설명에 따라 HelloWorldR2 및 기타 프로젝트를 수정하고 빌드하여 Azure IaaS 클러스터에서 실행되는 SOA 클라이언트 응용 프로그램을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-279">Modify and build the HellWorldR2 and other projects as described in the following section to generate the SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="e7927-280">Azure 저장소 큐와 함께 HTTP 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="e7927-280">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="e7927-281">Azure 저장소 큐와 함께 HTTP 바인딩을 사용하려면 샘플 코드를 일부 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-281">To use Http binding with an Azure storage queue, make a few changes to the sample code.</span></span>

* <span data-ttu-id="e7927-282">클러스터 이름을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-282">Update the cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="e7927-283">필요에 따라 SessionStartInfo에 기본 TransportScheme을 사용하거나 명시적으로 HTTP로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-283">Optionally, use the default TransportScheme in SessionStartInfo or explicitly set it to Http.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="e7927-284">BrokerClient에 대해 기본 바인딩을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-284">Use default binding for the BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="e7927-285">또는 basicHttpBinding을 사용하여 명시적으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-285">Or set explicitly using the basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="e7927-286">필요에 따라 SessionStartInfo에서 UseAzureQueue 플래그를 true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-286">Optionally, set the UseAzureQueue flag to true in SessionStartInfo.</span></span> <span data-ttu-id="e7927-287">설정되지 않은 경우 클러스터 이름에 Azure 도메인 접미사가 있고 TransportScheme이 HTTP인 경우 기본적으로 true로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-287">If not set, it will be set to true by default when the cluster name has Azure domain suffixes and the TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="e7927-288">Azure 저장소 큐 없이 HTTP 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="e7927-288">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="e7927-289">Azure Storage 큐 없이 HTTP 바인딩을 사용하려면 SessionStartInfo에서 명시적으로 UseAzureQueue 플래그를 false로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-289">To use Http binding without an Azure storage queue, explicitly set the UseAzureQueue flag to false in the SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="e7927-290">NetTcp 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="e7927-290">Use NetTcp binding</span></span>
<span data-ttu-id="e7927-291">NetTcp 바인딩을 사용하려면 구성이 온-프레미스 클러스터에 연결하는 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-291">To use NetTcp binding, the configuration is similar to connecting to an on-premises cluster.</span></span> <span data-ttu-id="e7927-292">헤드 노드 VM에서 몇 개의 끝점을 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-292">You need to open a few endpoints on the head node VM.</span></span> <span data-ttu-id="e7927-293">예를 들어 HPC Pack IaaS 배포 스크립트를 사용하여 클러스터를 만든 경우 다음과 같이 Azure Portal에서 끝점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-293">If you used the HPC Pack IaaS deployment script to create the cluster, for example, set the endpoints in the Azure portal as follows.</span></span>

1. <span data-ttu-id="e7927-294">VM을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-294">Stop the VM.</span></span>
2. <span data-ttu-id="e7927-295">세션, 브로커, 브로커 작업자 및 데이터 서비스에 대해 각각 TCP 포트 9090, 9087, 9091, 9094를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-295">Add the TCP ports 9090, 9087, 9091, 9094 for the Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![끝점 구성][endpoint-new-portal]
3. <span data-ttu-id="e7927-297">VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-297">Start the VM.</span></span>

<span data-ttu-id="e7927-298">헤드 이름을 IaaS 클러스터 전체 이름으로 변경하는 것을 제외하고 SOA 클라이언트 응용 프로그램에 필요한 변경 내용은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e7927-298">The SOA client application requires no changes except altering the head name to the IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7927-299">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e7927-299">Next steps</span></span>
* <span data-ttu-id="e7927-300">HPC 팩을 사용하여 Excel 작업을 실행하는 방법에 대한 자세한 내용은 [이러한 리소스](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7927-300">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="e7927-301">HPC 팩을 사용하여 SOA 서비스를 배포 및 관리하는 방법에 대한 자세한 내용은 [Microsoft HPC 팩에서 SOA 서비스 관리](https://technet.microsoft.com/library/ff919412.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7927-301">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

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
