---
title: "HPC 팩 클러스터의 Linux 계산 VM | Microsoft Docs"
description: "Azure에서 Linux HPC(고성능 컴퓨팅) 워크로드에 대한 HPC Pack 클러스터를 만들고 사용하는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 809d3944311badf265117d353b65642e044d900c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="e1a71-103">Azure에서 HPC Pack 클러스터의 Linux 계산 노드 시작</span><span class="sxs-lookup"><span data-stu-id="e1a71-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="e1a71-104">Windows Server를 실행하는 헤드 노드 및 지원되는 Linux 배포를 실행하는 여러 컴퓨터 노드를 포함하는 Azure의 [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) 클러스터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="e1a71-105">클러스터의 Windows 헤드 노드와 Linux 노드 간에 데이터를 이동하는 옵션을 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-105">Explore options to move data among the Linux nodes and the Windows head node of the cluster.</span></span> <span data-ttu-id="e1a71-106">Linux HPC 작업을 클러스터에 제출하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-106">Learn how to submit Linux HPC jobs to the cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="e1a71-107">다음 다이어그램은 만들고 작업하려는 HPC Pack 클러스터를 개략적으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-107">At a high level, the following diagram shows the HPC Pack cluster you create and work with.</span></span>

![Linux 노드가 포함된 HPC Pack 클러스터][scenario]

<span data-ttu-id="e1a71-109">Azure에서 Linux HPC 워크로드를 실행하기 위한 다른 옵션을 보려면 [배치 및 고성능 컴퓨팅에 대한 기술 리소스](../../../batch/big-compute-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-109">For other options to run Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="e1a71-110">Linux 계산 노드가 포함된 HPC Pack 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="e1a71-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="e1a71-111">이 문서에서는 Azure에서 Linux 계산 노드와 함께 HPC Pack 클러스터를 배포하기 위한 두 가지 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-111">This article shows you two options to deploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="e1a71-112">두 방법 모두 HPC Pack과 함께 Windows Server의 마켓플레이스 이미지를 사용하여 헤드 노드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-112">Both methods use a Marketplace image of Windows Server with HPC Pack to create the head node.</span></span> 

* <span data-ttu-id="e1a71-113">**Azure Resource Manager 템플릿** - Azure 마켓플레이스의 템플릿 또는 커뮤니티의 빠른 시작 템플릿을 사용하여 Resource Manager 배포 모델에서 클러스터 만들기를 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-113">**Azure Resource Manager template** - Use a template from the Azure Marketplace, or a quickstart template from the community, to automate creation of the cluster in the Resource Manager deployment model.</span></span> <span data-ttu-id="e1a71-114">예를 들어 Azure 마켓플레이스의 [Linux 워크로드에 대한 HPC Pack 클러스터](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) 템플릿은 Linux HPC 워크로드에 대한 완전한 HPC Pack 클러스터 인프라를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-114">For example, the [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in the Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="e1a71-115">**PowerShell 스크립트** - [Microsoft HPC Pack IaaS 배포 스크립트](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)(**New-HpcIaaSCluster.ps1**)를 사용하여 클래식 배포 모델의 완전한 클러스터 배포를 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-115">**PowerShell script** - Use the [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) to automate a complete cluster deployment in the classic deployment model.</span></span> <span data-ttu-id="e1a71-116">이 Azure PowerShell 스크립트는 빠른 배포를 위해 Azure 마켓플레이스의 HPC Pack VM 이미지를 사용하며 Linux 컴퓨터 노드 배포를 위한 포괄적인 구성 매개 변수 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-116">This Azure PowerShell script uses an HPC Pack VM image in the Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters to deploy Linux compute nodes.</span></span>

<span data-ttu-id="e1a71-117">Azure의 HPC Pack 클러스터 배포 옵션에 대한 자세한 내용은 [Microsoft HPC Pack을 사용하여 Azure에서 HPC(고성능 컴퓨팅) 클러스터를 만들고 관리하는 옵션](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-117">For more information about HPC Pack cluster deployment options in Azure, see [Options to create and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e1a71-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e1a71-118">Prerequisites</span></span>
* <span data-ttu-id="e1a71-119">**Azure 구독** - Azure Global 또는 Azure China 서비스의 구독을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-119">**Azure subscription** - You can use a subscription in either the Azure Global or Azure China service.</span></span> <span data-ttu-id="e1a71-120">계정이 없는 경우 몇 분 안에 [무료 계정](https://azure.microsoft.com/pricing/free-trial/) 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="e1a71-121">**코어 할당량** - 멀티 코어 VM 크기를 사용하여 여러 클러스터 노드를 배포하려는 경우 특히 코어 할당량을 늘려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-121">**Cores quota** - You might need to increase the quota of cores, especially if you choose to deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="e1a71-122">할당량을 늘리려면 무료로 온라인 고객 지원 요청을 개설합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-122">To increase a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="e1a71-123">**Linux 배포판** - 현재 HPC Pack은 컴퓨터 노드에 대한 다음 Linux 배포판을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-123">**Linux distributions** - Currently HPC Pack supports the following Linux distributions for compute nodes.</span></span> <span data-ttu-id="e1a71-124">이러한 사용 가능한 배포판의 마켓플레이스 버전을 사용하거나 사용자 자체 버전을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="e1a71-125">**CentOS 기반**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span><span class="sxs-lookup"><span data-stu-id="e1a71-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="e1a71-126">**Red Hat Enterprise Linux** 6.7, 6.8, 7.2</span><span class="sxs-lookup"><span data-stu-id="e1a71-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="e1a71-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12(Premium), SLES 12 SP1, SLES 12 SP1(Premium), SLES 12 for HPC, SLES 12 for HPC(Premium)</span><span class="sxs-lookup"><span data-stu-id="e1a71-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="e1a71-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="e1a71-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="e1a71-129">RDMA 지원 VM 크기 중 하나에서 Azure RDMA 네트워크를 사용하려면 Azure 마켓플레이스에서 SUSE Linux Enterprise Server 12 HPC 또는 CentOS 기반 HPC 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-129">To use the Azure RDMA network with one of the RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from the Azure Marketplace.</span></span> <span data-ttu-id="e1a71-130">자세한 내용은 [고성능 계산 VM 크기](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="e1a71-131">HPC Pack IaaS 배포 스크립트를 사용하여 클러스터를 배포하는 경우 추가 필수 조건은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-131">Additional prerequisites to deploy the cluster by using the HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="e1a71-132">**클라이언트 컴퓨터** - 클러스터 배포 스크립트를 실행할 Windows 기반 클라이언트 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-132">**Client computer** - You need a Windows-based client computer to run the cluster deployment script.</span></span>
* <span data-ttu-id="e1a71-133">**Azure PowerShell** - [Azure PowerShell(버전 0.8.10 이상)을 설치 및 구성](/powershell/azure/overview) 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="e1a71-134">**HPC 팩 IaaS 배포 스크립트** - [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=44949)에서 최신 버전의 스크립트를 다운로드하고 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-134">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="e1a71-135">`.\New-HPCIaaSCluster.ps1 –Version`을 실행하여 스크립트 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-135">You can check the version of the script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="e1a71-136">이 문서는 4.4.1 이상 버전의 스크립트를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-136">This article is based on version 4.4.1 or later of the script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="e1a71-137">배포 옵션 1.</span><span class="sxs-lookup"><span data-stu-id="e1a71-137">Deployment option 1.</span></span> <span data-ttu-id="e1a71-138">Resource Manager 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="e1a71-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="e1a71-139">Azure 마켓플레이스의 [Linux 워크로드용 HPC Pack 클러스터](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) 템플릿으로 이동하여 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-139">Go to the [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in the Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="e1a71-140">Azure 포털에서 정보를 검토한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-140">In the Azure portal, review the information and then click **Create**.</span></span>
   
    ![포털 만들기][portal]
3. <span data-ttu-id="e1a71-142">**기본 사항** 블레이드에서 클러스터에 대한 이름을 입력합니다(이는 헤드 노드 VM의 이름도 지정하게 됨).</span><span class="sxs-lookup"><span data-stu-id="e1a71-142">On the **Basics** blade, enter a name for the cluster, which also names the head node VM.</span></span> <span data-ttu-id="e1a71-143">기존 리소스 그룹을 선택하거나 사용할 수 있는 위치에 배포용 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-143">You can choose an existing resource group or create a group for the deployment in a location that's available to you.</span></span> <span data-ttu-id="e1a71-144">이 위치는 특정 VM 크기 및 기타 Azure 서비스의 가용성에 영향을 줍니다([하위 지역별 사용 가능한 제품](https://azure.microsoft.com/regions/services/) 참조).</span><span class="sxs-lookup"><span data-stu-id="e1a71-144">The location affects the availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="e1a71-145">**헤드 노드 설정** 블레이드에서 첫 번째 배포의 경우 일반적으로 기본 설정을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-145">On the **Head node settings** blade, for a first deployment, you can generally accept the default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e1a71-146">**사후 구성 스크립트 URL** 은 실행 후 헤드 노드 VM에서 실행할 공개적으로 사용 가능한 Windows PowerShell 스크립트를 지정하는 선택적 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-146">The **Post-configuration script URL** is an optional setting to specify a publicly available Windows PowerShell script that you want to run on the head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="e1a71-147">**컴퓨터 노드 설정** 블레이드에서 노드용 명명 패턴, 노드의 수와 크기, 배포할 Linux 배포판을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-147">On the **Compute node settings** blade, select a naming pattern for the nodes, the number and size of the nodes, and the Linux distribution to deploy.</span></span>
6. <span data-ttu-id="e1a71-148">**인프라 설정** 블레이드에서 가상 네트워크 및 Active Directory 도메인의 이름, 도메인 및 VM 관리자 자격 증명, 저장소 계정용 명명 패턴을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-148">On the **Infrastructure settings** blade, enter names for the virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for the storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e1a71-149">HPC Pack에서는 Active Directory 도메인을 사용하여 클러스터 사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-149">HPC Pack uses the Active Directory domain to authenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="e1a71-150">유효성 검사 테스트가 실행되고 사용 약관을 검토한 후에는 **구매**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-150">After the validation tests run and you review the terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-the-iaas-deployment-script"></a><span data-ttu-id="e1a71-151">배포 옵션 2.</span><span class="sxs-lookup"><span data-stu-id="e1a71-151">Deployment option 2.</span></span> <span data-ttu-id="e1a71-152">IaaS 배포 스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="e1a71-152">Use the IaaS deployment script</span></span>
<span data-ttu-id="e1a71-153">HPC Pack IaaS 배포 스크립트를 사용하여 클러스터를 배포하는 경우 추가 필수 조건은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-153">Following are additional prerequisites to deploy the cluster by using the HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="e1a71-154">**클라이언트 컴퓨터** - 클러스터 배포 스크립트를 실행할 Windows 기반 클라이언트 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-154">**Client computer** - You need a Windows-based client computer to run the cluster deployment script.</span></span>
* <span data-ttu-id="e1a71-155">**Azure PowerShell** - [Azure PowerShell(버전 0.8.10 이상)을 설치 및 구성](/powershell/azure/overview) 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="e1a71-156">**HPC 팩 IaaS 배포 스크립트** - [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=44949)에서 최신 버전의 스크립트를 다운로드하고 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-156">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="e1a71-157">`.\New-HPCIaaSCluster.ps1 –Version`을 실행하여 스크립트 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-157">You can check the version of the script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="e1a71-158">이 문서는 4.4.1 이상 버전의 스크립트를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-158">This article is based on version 4.4.1 or later of the script.</span></span>

<span data-ttu-id="e1a71-159">**XML 구성 파일**</span><span class="sxs-lookup"><span data-stu-id="e1a71-159">**XML configuration file**</span></span>

<span data-ttu-id="e1a71-160">HPC Pack IaaS 배포 스크립트는 XML 구성 파일을 입력으로 사용하여 HPC 클러스터에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-160">The HPC Pack IaaS deployment script uses an XML configuration file as input to describe the  HPC cluster.</span></span> <span data-ttu-id="e1a71-161">다음 샘플 구성 파일은 HPC Pack 헤드 노드와 두 가지 크기의 A7 CentOS 7.0 Linux 컴퓨터 노드로 구성된 작은 클러스터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-161">The following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="e1a71-162">환경 및 원하는 클러스터 구성의 필요에 따라 파일을 수정하고 HPCDemoConfig.xml 등의 이름을 지정하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-162">Modify the file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="e1a71-163">예를 들어 구독 이름 및 고유 저장소 계정 이름과 클라우드 서비스 이름을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-163">For example, you need to supply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="e1a71-164">또한 계산 노드에 대해 지원되는 다른 Linux 이미지를 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-164">Additionally, you might want to choose a different supported Linux image for the compute nodes.</span></span> <span data-ttu-id="e1a71-165">구성 파일의 요소에 대한 자세한 내용은 스크립트 폴더의 Manual.rtf 파일과 [HPC 팩 IaaS 배포 스크립트를 사용하여 HPC 클러스터 만들기](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-165">For more information about the elements in the configuration file, see the Manual.rtf file in the script folder and [Create an HPC cluster with the HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="e1a71-166">**HPC Pack IaaS 배포 스크립트를 실행하려면**</span><span class="sxs-lookup"><span data-stu-id="e1a71-166">**To run the HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="e1a71-167">관리자 권한으로 클라이언트 컴퓨터에서 Windows PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-167">Open Windows PowerShell on the client computer as an administrator.</span></span>
2. <span data-ttu-id="e1a71-168">디렉터리를 스크립트가 설치되는 폴더(이 예제에서는 E:\IaaSClusterScript)로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-168">Change directory to the folder where the script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="e1a71-169">다음 명령을 실행하여 HPC Pack 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-169">Run the following command to deploy the HPC Pack cluster.</span></span> <span data-ttu-id="e1a71-170">이 예제에서는 구성 파일이 E:\HPCDemoConfig.xml에 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-170">This example assumes that the configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="e1a71-171">a.</span><span class="sxs-lookup"><span data-stu-id="e1a71-171">a.</span></span> <span data-ttu-id="e1a71-172">앞의 명령에서 **AdminPassword** 가 지정되지 않았으므로 사용자 *MyAdminName*에 대한 암호를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-172">Because the **AdminPassword** is not specified in the preceding command, you are prompted to enter the password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="e1a71-173">b.</span><span class="sxs-lookup"><span data-stu-id="e1a71-173">b.</span></span> <span data-ttu-id="e1a71-174">스크립트에서 구성 파일의 유효성 검사를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-174">The script then starts to validate the configuration file.</span></span> <span data-ttu-id="e1a71-175">네트워크 연결에 따라 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-175">It can take up to several minutes depending on the network connection.</span></span>
   
    ![유효성 검사][validate]
   
    <span data-ttu-id="e1a71-177">c.</span><span class="sxs-lookup"><span data-stu-id="e1a71-177">c.</span></span> <span data-ttu-id="e1a71-178">유효성 검사를 통과하면 스크립트는 만들 클러스터 리소스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-178">After validations pass, the script lists the cluster resources to create.</span></span> <span data-ttu-id="e1a71-179">*Y* 를 입력하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-179">Enter *Y* to continue.</span></span>
   
    ![리소스][resources]
   
    <span data-ttu-id="e1a71-181">d.</span><span class="sxs-lookup"><span data-stu-id="e1a71-181">d.</span></span> <span data-ttu-id="e1a71-182">스크립트에서 HPC Pack 클러스터 배포를 시작하고 추가 수동 단계 없이 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-182">The script starts to deploy the HPC Pack cluster and completes the configuration without further manual steps.</span></span> <span data-ttu-id="e1a71-183">이 스크립트는 실행하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-183">The script can run for several minutes.</span></span>
   
    ![배포][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="e1a71-185">이 예제에서는 **-LogFile** 매개 변수가 지정되지 않았으므로 스크립트에서 자동으로 로그 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-185">In this example, the script generates a log file automatically since the **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="e1a71-186">로그는 실시간으로 작성되지 않지만 유효성 검사 및 배포가 끝날 때 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-186">The logs aren't written in real time, but are collected at the end of the validation and the deployment.</span></span> <span data-ttu-id="e1a71-187">스크립트가 실행되는 동안 PowerShell 프로세스가 중지되는 경우 일부 로그가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-187">If the PowerShell process is stopped while the script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-to-the-head-node"></a><span data-ttu-id="e1a71-188">헤드 노드에 연결</span><span class="sxs-lookup"><span data-stu-id="e1a71-188">Connect to the head node</span></span>
<span data-ttu-id="e1a71-189">Azure에서 HPC Pack 클러스터를 배포한 후에 클러스터를 배포할 때 제공한 도메인 자격 증명(예: *hpc\\clusteradmin*)을 사용하여 [원격 데스크톱을 통해 헤드 노드 VM에 연결](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-189">After you deploy the HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to the head node VM using the domain credentials you provided when you deployed the cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="e1a71-190">헤드 노드에서 클러스터를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-190">You manage the cluster from the head node.</span></span>

<span data-ttu-id="e1a71-191">헤드 노드에서 HPC 클러스터 관리자를 시작하여 HPC Pack 클러스터의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-191">On the head node, start HPC Cluster Manager to check the status of the HPC Pack cluster.</span></span> <span data-ttu-id="e1a71-192">Windows 계산 노드에서 작업하는 것과 동일한 방식으로 Linux 계산 노드를 관리 및 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-192">You can manage and monitor Linux compute nodes the same way you work with Windows compute nodes.</span></span> <span data-ttu-id="e1a71-193">예를 들어 **리소스 관리**에 나열된 Linux 노드가 표시됩니다(이러한 노드는 **LinuxNode** 템플릿으로 배포됨).</span><span class="sxs-lookup"><span data-stu-id="e1a71-193">For example, you see the Linux nodes listed in **Resource Management** (these nodes are deployed with the **LinuxNode** template).</span></span>

![노드 관리][management]

<span data-ttu-id="e1a71-195">또한 **열 지도** 보기에 Linux 노드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-195">You also see the Linux nodes in the **Heat Map** view.</span></span>

![열 지도][heatmap]

## <a name="how-to-move-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="e1a71-197">Linux 노드가 포함된 클러스터에서 데이터를 이동하는 방법</span><span class="sxs-lookup"><span data-stu-id="e1a71-197">How to move data in a cluster with Linux nodes</span></span>
<span data-ttu-id="e1a71-198">클러스터의 Windows 헤드 노드와 Linux 노드 간에 데이터를 이동하는 여러 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-198">You have several choices to move data among Linux nodes and the Windows head node of the cluster.</span></span> <span data-ttu-id="e1a71-199">다음은 세 가지 일반적인 방법으로, 다음 섹션에서 자세히 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-199">Here are three common methods, described in more detail in the following sections:</span></span>

* <span data-ttu-id="e1a71-200">**Azure 파일** - Azure 저장소에 데이터 파일을 저장할 관리 SMB 파일 공유를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-200">**Azure File** - Exposes a managed SMB file share to store data files in Azure storage.</span></span> <span data-ttu-id="e1a71-201">서로 다른 가상 네트워크에 배포된 경우에도 Windows 노드와 Linux 노드는 Azure 파일 공유를 드라이브 또는 폴더로 동시에 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at the same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="e1a71-202">**헤드 노드 SMB 공유** - Linux 노드에 헤드 노드의 표준 Windows 공유 폴더를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-202">**Head node SMB share** - Mounts a standard Windows shared folder of the head node on Linux nodes.</span></span>
* <span data-ttu-id="e1a71-203">**헤드 노드 NFS 서버** - Windows 및 Linux 혼합 환경에 대한 파일 공유 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="e1a71-204">Azure 파일 저장소</span><span class="sxs-lookup"><span data-stu-id="e1a71-204">Azure File storage</span></span>
<span data-ttu-id="e1a71-205">[Azure 파일](https://azure.microsoft.com/services/storage/files/) 서비스는 표준 SMB 2.1 프로토콜을 사용하여 파일 공유를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-205">The [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using the standard SMB 2.1 protocol.</span></span> <span data-ttu-id="e1a71-206">Azure VM 및 클라우드 서비스는 탑재된 공유를 통해 여러 응용 프로그램 구성 요소에서 파일 데이터를 공유할 수 있으며, 온-프레미스 응용 프로그램은 파일 저장소 API를 통해 공유의 파일 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through the File storage API.</span></span> 

<span data-ttu-id="e1a71-207">Azure 파일 공유를 만들고 헤드 노드에 탑재하는 세부 단계는 [Windows에서 Azure 파일 저장소 시작](../../../storage/files/storage-how-to-use-files-windows.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-207">For detailed steps to create an Azure File share and mount it on the head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="e1a71-208">Linux 노드에 Azure 파일 공유를 탑재하려면 [Linux에서 Azure File Storage를 사용하는 방법](../../../storage/files/storage-how-to-use-files-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-208">To mount the Azure File share on the Linux nodes, see [How to use Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="e1a71-209">영구적 연결을 설정하려면 [Microsoft Azure 파일에 대한 연결 유지](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-209">To set up persisting connections, see [Persisting connections to Microsoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="e1a71-210">다음 예제에서는 저장소 계정에 Azure 파일 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-210">In the following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="e1a71-211">헤드 노드에 공유를 탑재하려면 명령 프롬프트를 열고 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-211">To mount the share on the head node, open a Command Prompt and enter the following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="e1a71-212">이 예제에서 allvhdsje는 저장소 계정 이름이고, storageaccountkey는 저장소 계정 키이고, rdma는 Azure 파일 공유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is the Azure File share name.</span></span> <span data-ttu-id="e1a71-213">Azure 파일 공유는 헤드 노드에 Z:로 탑재됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-213">The Azure File share is mounted as Z: on the head node.</span></span>

<span data-ttu-id="e1a71-214">Linux 노드에 Azure 파일 공유를 탑재하려면 헤드 노드에서 **clusrun** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-214">To mount the Azure File share on Linux nodes, run a **clusrun** command on the head node.</span></span> <span data-ttu-id="e1a71-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** 은 여러 노드에서 관리 작업을 수행할 수 있는 유용한 HPC 팩 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool to carry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="e1a71-216">이 문서의 [Linux 노드에 대한 Clusrun](#Clusrun-for-Linux-nodes) 도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="e1a71-217">Windows PowerShell 창을 열고 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-217">Open a Windows PowerShell window and enter the following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="e1a71-218">첫 번째 명령은 LinuxNodes 그룹의 모든 노드에 /rdma라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-218">The first command creates a folder named /rdma on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="e1a71-219">두 번째 명령은 dir 및 파일 모드 비트를 777로 설정하여 Azure 파일 공유 allvhdsjw.file.core.windows.net/rdma를 /rdma 폴더에 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-219">The second command mounts the Azure File share allvhdsjw.file.core.windows.net/rdma onto the /rdma folder with dir and file mode bits set to 777.</span></span> <span data-ttu-id="e1a71-220">두 번째 명령에서 allvhdsje는 저장소 계정 이름이고 storageaccountkey는 저장소 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-220">In the second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="e1a71-221">두 번째 명령의 “\\`” 기호는 PowerShell의 이스케이프 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-221">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="e1a71-222">“\\`,”는 ","(쉼표)가 명령의 일부임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-222">“\\`,” means that the “,” (comma character) is a part of the command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="e1a71-223">헤드 노드 공유</span><span class="sxs-lookup"><span data-stu-id="e1a71-223">Head node share</span></span>
<span data-ttu-id="e1a71-224">또는 Linux 노드에 헤드 노드의 공유 폴더를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-224">Alternatively, mount a shared folder of the head node on Linux nodes.</span></span> <span data-ttu-id="e1a71-225">공유는 파일을 공유하는 가장 간단한 방법을 제공하지만 헤드 노드와 모든 Linux 노드를 동일한 가상 네트워크에 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-225">A share provides the simplest way to share files, but the head node and all Linux nodes must be deployed in the same virtual network.</span></span> <span data-ttu-id="e1a71-226">단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-226">Here are the steps.</span></span>

1. <span data-ttu-id="e1a71-227">헤드 노드에서 폴더를 만들고 읽기/쓰기 권한을 가진 모든 사용자에게 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-227">Create a folder on the head node and share it to Everyone with Read/Write permissions.</span></span> <span data-ttu-id="e1a71-228">예를 들어 헤드 노드의 D:\OpenFOAM을 \\CentOS7RDMA-HN\OpenFOAM으로 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-228">For example, share D:\OpenFOAM on the head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="e1a71-229">여기서 CentOS7RDMA-HN은 헤드 노드의 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-229">Here CentOS7RDMA-HN is the hostname of the head node.</span></span>
   
    ![파일 공유 권한][fileshareperms]
   
    ![파일 공유][filesharing]
2. <span data-ttu-id="e1a71-232">Windows PowerShell 창을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-232">Open a Windows PowerShell window and run the following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="e1a71-233">첫 번째 명령은 LinuxNodes 그룹의 모든 노드에 /openfoam이라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-233">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="e1a71-234">두 번째 명령은 dir 및 파일 모드 비트를 777로 설정하여 공유 폴더 //CentOS7RDMA-HN/OpenFOAM을 폴더에 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-234">The second command mounts the shared folder //CentOS7RDMA-HN/OpenFOAM onto the folder with dir and file mode bits set to 777.</span></span> <span data-ttu-id="e1a71-235">명령의 사용자 이름과 암호는 헤드 노드 클러스터 사용자의 사용자 이름과 암호여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-235">The username and password in the command should be the username and password of a cluster user on the head node.</span></span> <span data-ttu-id="e1a71-236">( [클러스터 사용자 추가 또는 제거](https://technet.microsoft.com/library/ff919330.aspx)참조)</span><span class="sxs-lookup"><span data-stu-id="e1a71-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="e1a71-237">두 번째 명령의 “\\`” 기호는 PowerShell의 이스케이프 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-237">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="e1a71-238">“\\`,”는 ","(쉼표)가 명령의 일부임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-238">“\\`,” means that the “,” (comma character) is a part of the command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="e1a71-239">NFS 서버</span><span class="sxs-lookup"><span data-stu-id="e1a71-239">NFS server</span></span>
<span data-ttu-id="e1a71-240">NFS 서비스를 사용하면 SMB 프로토콜을 사용하는 Windows Server 2012 운영 체제 실행 컴퓨터와 NFS 프로토콜을 사용하는 Linux 기반 컴퓨터 간에 파일을 공유하고 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-240">The NFS service enables you to share and migrate files between computers running the Windows Server 2012 operating system using the SMB protocol and Linux-based computers using the NFS protocol.</span></span> <span data-ttu-id="e1a71-241">NFS 서버 및 다른 모든 노드를 동일한 가상 네트워크에 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-241">The NFS server and all other nodes have to be deployed in the same virtual network.</span></span> <span data-ttu-id="e1a71-242">SMB 공유에 비해 Linux 노드와의 호환성이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="e1a71-243">예를 들어 파일 링크를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="e1a71-244">NFS 서버를 설치 및 설정하려면 [네트워크 파일 시스템 첫 번째 공유 종단 간에 대한 서버](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx)(영문)의 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-244">To install and set up an NFS server, follow the steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="e1a71-245">예를 들어 다음 속성이 설정된 nfs라는 NFS 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-245">For example, create an NFS share named nfs with the following properties:</span></span>
   
    ![NFS 권한 부여][nfsauth]
   
    ![NFS 공유 권한][nfsshare]
   
    ![NFS NTFS 사용 권한][nfsperm]
   
    ![NFS 관리 속성][nfsmanage]
2. <span data-ttu-id="e1a71-250">Windows PowerShell 창을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-250">Open a Windows PowerShell window and run the following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="e1a71-251">첫 번째 명령은 LinuxNodes 그룹의 모든 노드에 /nfsshared라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-251">The first command creates a folder named /nfsshared on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="e1a71-252">두 번째 명령은 NFS 공유 CentOS7RDMA-HN:/nfs를 폴더에 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-252">The second command mounts the NFS share CentOS7RDMA-HN:/nfs onto the folder.</span></span> <span data-ttu-id="e1a71-253">여기서 CentOS7RDMA-HN:/nfs는 NFS 공유의 원격 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-253">Here CentOS7RDMA-HN:/nfs is the remote path of your NFS share.</span></span>

## <a name="how-to-submit-jobs"></a><span data-ttu-id="e1a71-254">작업을 제출하는 방법</span><span class="sxs-lookup"><span data-stu-id="e1a71-254">How to submit jobs</span></span>
<span data-ttu-id="e1a71-255">HPC Pack 클러스터에 작업을 제출하는 방법에는 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-255">There are several ways to submit jobs to the HPC Pack cluster:</span></span>

* <span data-ttu-id="e1a71-256">HPC 클러스터 관리자 또는 HPC 작업 관리자 GUI</span><span class="sxs-lookup"><span data-stu-id="e1a71-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="e1a71-257">HPC 웹 포털</span><span class="sxs-lookup"><span data-stu-id="e1a71-257">HPC web portal</span></span>
* <span data-ttu-id="e1a71-258">REST API</span><span class="sxs-lookup"><span data-stu-id="e1a71-258">REST API</span></span>

<span data-ttu-id="e1a71-259">Azure에서 HPC Pack GUI 도구 및 HPC 웹 포털을 통해 클러스터에 작업을 제출하는 방법은 Windows 컴퓨터 노드의 경우와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-259">Job submission to the cluster in Azure via HPC Pack GUI tools and the HPC web portal are the same as for Windows compute nodes.</span></span> <span data-ttu-id="e1a71-260">[HPC Pack 작업 관리자](https://technet.microsoft.com/library/ff919691.aspx) 및 [온-프레미스 클라이언트 컴퓨터에서 작업을 제출하는 방법](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How to submit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="e1a71-261">REST API를 통해 작업을 제출하려면 [Microsoft HPC Pack의 REST API를 사용하여 작업 만들기 및 제출](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-261">To submit jobs via the REST API, refer to [Creating and Submitting Jobs by Using the REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="e1a71-262">또한 Linux 클라이언트에서 작업을 제출하려면 [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756)의 Python 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-262">To submit jobs from a Linux client, also refer to the Python sample in the [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="e1a71-263">Linux 노드에 대한 Clusrun</span><span class="sxs-lookup"><span data-stu-id="e1a71-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="e1a71-264">HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) 도구를 사용하여 명령 프롬프트 또는 HPC 클러스터 관리자를 통해 Linux 노드에서 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-264">The HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used to execute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="e1a71-265">다음은 몇 가지 기본적인 예입니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-265">Following are some basic examples.</span></span>

* <span data-ttu-id="e1a71-266">클러스터에 있는 모든 노드에 현재 사용자 이름을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-266">Show current user names on all nodes in the cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="e1a71-267">linuxnodes 그룹의 모든 노드에서 **yum**을 사용하여 **gdb** 디버거 도구를 설치하고 10분 후에 노드를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-267">Install the **gdb** debugger tool with **yum** on all nodes in the linuxnodes group and then restart the nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="e1a71-268">클러스터의 각 Linux 노드에서 1초에 대해 각각 숫자 1에서 10을 표시하는 셸 스크립트를 만들고 실행한 다음 노드에서 즉시 출력을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in the cluster, run it, and show output from the nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="e1a71-269">**clusrun** 명령에 특정 이스케이프 문자를 사용해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-269">You might need to use certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="e1a71-270">이 예와 같이 명령 프롬프트의 ^를 사용하여 ">" 기호를 이스케이프합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a71-270">As shown in this example, use ^ in a Command Prompt to escape the ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e1a71-271">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e1a71-271">Next steps</span></span>
* <span data-ttu-id="e1a71-272">클러스터의 노드 수를 확장하거나 클러스터에서 Linux 워크로드를 실행해 보세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-272">Try scaling up the cluster to a larger number of nodes, or try running a Linux workload on the cluster.</span></span> <span data-ttu-id="e1a71-273">예제는 [Azure의 Linux 계산 노드에서 Microsoft HPC 팩을 사용하여 NAMD 실행](hpcpack-cluster-namd.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="e1a71-274">[RDMA 지원, 계산 집약적 VM](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)이 있는 클러스터로 MPI 작업을 실행해 보세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to run MPI workloads.</span></span> <span data-ttu-id="e1a71-275">그에 대한 예는 [Azure의 Linux RDMA 클러스터에서 Microsoft HPC Pack을 사용하여 OpenFOAM 실행](hpcpack-cluster-openfoam.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="e1a71-276">온-프레미스 HPC Pack 클러스터의 Linux 노드를 사용한 작업에 관심이 있는 경우 [TechNet 지침](https://technet.microsoft.com/library/mt595803.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1a71-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see the [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
