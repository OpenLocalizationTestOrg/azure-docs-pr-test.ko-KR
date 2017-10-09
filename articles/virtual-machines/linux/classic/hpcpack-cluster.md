---
title: "HPC Pack 클러스터에서 계산 Vm aaaLinux | Microsoft Docs"
description: "어떻게 toocreate 사용 HPC 팩 클러스터 및 Azure에서 Linux 고성능 (HPC) 작업을 컴퓨팅에 대 한 자세한 내용은"
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
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="378d5-103">Azure에서 HPC Pack 클러스터의 Linux 계산 노드 시작</span><span class="sxs-lookup"><span data-stu-id="378d5-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="378d5-104">Windows Server를 실행하는 헤드 노드 및 지원되는 Linux 배포를 실행하는 여러 컴퓨터 노드를 포함하는 Azure의 [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) 클러스터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="378d5-105">Hello Linux 노드와 hello Windows hello 클러스터의 헤드 노드 간에 옵션 toomove 데이터를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-105">Explore options toomove data among hello Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="378d5-106">Linux HPC toosubmit toohello 클러스터 작업 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-106">Learn how toosubmit Linux HPC jobs toohello cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="378d5-107">상위 수준 hello 다음 다이어그램에서는 hello HPC Pack 클러스터 만들기 및 작업</span><span class="sxs-lookup"><span data-stu-id="378d5-107">At a high level, hello following diagram shows hello HPC Pack cluster you create and work with.</span></span>

![Linux 노드가 포함된 HPC Pack 클러스터][scenario]

<span data-ttu-id="378d5-109">다른 옵션 toorun Linux HPC에 대 한 Azure에서 작업 참조 [일괄 처리 및 고성능 컴퓨팅에 대 한 기술 리소스](../../../batch/big-compute-resources.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-109">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="378d5-110">Linux 계산 노드가 포함된 HPC Pack 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="378d5-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="378d5-111">이 문서에서는 두 가지 옵션이 toodeploy HPC Pack 클러스터 Azure에서 Linux 계산 노드와 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-111">This article shows you two options toodeploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="378d5-112">두 가지 방법 toocreate hello 헤드 노드에 HPC Pack의 Windows Server 마켓플레이스 이미지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-112">Both methods use a Marketplace image of Windows Server with HPC Pack toocreate hello head node.</span></span> 

* <span data-ttu-id="378d5-113">**Azure 리소스 관리자 템플릿** -hello Azure Marketplace에서에서 템플릿을 또는 hello 커뮤니티, tooautomate hello 리소스 관리자 배포 모델에서 hello 클러스터 만들기 퀵 스타트 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-113">**Azure Resource Manager template** - Use a template from hello Azure Marketplace, or a quickstart template from hello community, tooautomate creation of hello cluster in hello Resource Manager deployment model.</span></span> <span data-ttu-id="378d5-114">예를 들어 hello [Linux 워크 로드에 대 한 HPC 팩 클러스터](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) hello Azure Marketplace에서에서 서식 파일을 만듭니다 전체 HPC 팩 클러스터 인프라 Linux HPC에 대 한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-114">For example, hello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="378d5-115">**PowerShell 스크립트** -사용 하 여 hello [Microsoft HPC Pack IaaS 배포 스크립트](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-hpciaascluster.ps1**) tooautomate hello 클래식 배포 모델에서 전체 클러스터 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-115">**PowerShell script** - Use hello [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate a complete cluster deployment in hello classic deployment model.</span></span> <span data-ttu-id="378d5-116">이 Azure PowerShell 스크립트는 hello Azure Marketplace의에서 HPC Pack VM 이미지를 사용 하 여 빠른 배포를 위한 하 고 다양 한 구성 매개 변수 toodeploy Linux 계산 노드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-116">This Azure PowerShell script uses an HPC Pack VM image in hello Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters toodeploy Linux compute nodes.</span></span>

<span data-ttu-id="378d5-117">Azure에서 HPC Pack 클러스터 배포 옵션에 대 한 자세한 내용은 참조 [toocreate 옵션 및 Microsoft HPC Pack을 사용 하 여 Azure에 있는 고성능 HPC (컴퓨팅) 클러스터 관리](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-117">For more information about HPC Pack cluster deployment options in Azure, see [Options toocreate and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="378d5-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="378d5-118">Prerequisites</span></span>
* <span data-ttu-id="378d5-119">**Azure 구독** -어느 hello Azure Global 또는 Azure China 서비스에서에서 구독을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-119">**Azure subscription** - You can use a subscription in either hello Azure Global or Azure China service.</span></span> <span data-ttu-id="378d5-120">계정이 없는 경우 몇 분 안에 [무료 계정](https://azure.microsoft.com/pricing/free-trial/) 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="378d5-121">**코어 할당량** -toodeploy 멀티 코어 VM 크기에 따라 여러 개의 클러스터 노드를 선택 하는 경우에 특히 tooincrease hello 할당량의 코어를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-121">**Cores quota** - You might need tooincrease hello quota of cores, especially if you choose toodeploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="378d5-122">할당량 tooincrease 비용 없이 온라인 고객 지원 요청을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-122">tooincrease a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="378d5-123">**Linux 배포판** -HPC Pack 현재 계산 노드에 대 한 Linux 배포를 수행 하는 hello를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-123">**Linux distributions** - Currently HPC Pack supports hello following Linux distributions for compute nodes.</span></span> <span data-ttu-id="378d5-124">이러한 사용 가능한 배포판의 마켓플레이스 버전을 사용하거나 사용자 자체 버전을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="378d5-125">**CentOS 기반**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span><span class="sxs-lookup"><span data-stu-id="378d5-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="378d5-126">**Red Hat Enterprise Linux** 6.7, 6.8, 7.2</span><span class="sxs-lookup"><span data-stu-id="378d5-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="378d5-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12(Premium), SLES 12 SP1, SLES 12 SP1(Premium), SLES 12 for HPC, SLES 12 for HPC(Premium)</span><span class="sxs-lookup"><span data-stu-id="378d5-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="378d5-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="378d5-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="378d5-129">RDMA 가능 hello VM 크기 중 하나를 사용 하 여 toouse hello Azure RDMA 네트워크 hello Azure Marketplace에서에서 SUSE Linux Enterprise Server 12 HPC 또는 HPC CentOS 기반 이미지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-129">toouse hello Azure RDMA network with one of hello RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from hello Azure Marketplace.</span></span> <span data-ttu-id="378d5-130">자세한 내용은 [고성능 계산 VM 크기](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="378d5-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="378d5-131">추가 필수 구성 요소 toodeploy hello hello HPC Pack IaaS 배포 스크립트를 사용 하 여 클러스터:</span><span class="sxs-lookup"><span data-stu-id="378d5-131">Additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="378d5-132">**클라이언트 컴퓨터** -Windows 기반 클라이언트 컴퓨터 toorun hello 클러스터 배포 스크립트를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-132">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="378d5-133">**Azure PowerShell** - [Azure PowerShell(버전 0.8.10 이상)을 설치 및 구성](/powershell/azure/overview) 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="378d5-134">**HPC Pack IaaS 배포 스크립트** -다운로드 하 고 hello hello에서 hello 스크립트의 최신 버전을 푸는 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=44949)합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-134">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="378d5-135">실행 하 여 hello 스크립트의 hello 버전을 확인 하면 `.\New-HPCIaaSCluster.ps1 –Version`합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-135">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="378d5-136">이 문서는 4.4.1 버전 또는 hello 스크립트의 나중에 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-136">This article is based on version 4.4.1 or later of hello script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="378d5-137">배포 옵션 1.</span><span class="sxs-lookup"><span data-stu-id="378d5-137">Deployment option 1.</span></span> <span data-ttu-id="378d5-138">Resource Manager 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="378d5-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="378d5-139">Toohello 이동 [Linux 워크 로드에 대 한 HPC 팩 클러스터](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) 에서 Azure 마켓플레이스 hello 템플릿과 클릭 **배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-139">Go toohello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="378d5-140">에 Azure 포털 hello hello 정보를 검토 하 고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-140">In hello Azure portal, review hello information and then click **Create**.</span></span>
   
    ![포털 만들기][portal]
3. <span data-ttu-id="378d5-142">Hello에 **기본 사항** 블레이드에서 hello 헤드 노드 VM의 이름도 지정 hello 클러스터에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-142">On hello **Basics** blade, enter a name for hello cluster, which also names hello head node VM.</span></span> <span data-ttu-id="378d5-143">기존 리소스 그룹을 선택 하거나 tooyou 사용할 수 있는 위치에 hello 배포에 대 한 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-143">You can choose an existing resource group or create a group for hello deployment in a location that's available tooyou.</span></span> <span data-ttu-id="378d5-144">hello 위치에 영향을 특정 VM 크기 및 기타 Azure 서비스의 가용성을 hello (참조 [지역에 따라 사용할 수 있는 제품](https://azure.microsoft.com/regions/services/)).</span><span class="sxs-lookup"><span data-stu-id="378d5-144">hello location affects hello availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="378d5-145">Hello에 **헤드 노드 설정을** 블레이드에서 hello 기본 설정을 수락 일반적으로 첫 번째 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-145">On hello **Head node settings** blade, for a first deployment, you can generally accept hello default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="378d5-146">hello **후 구성 스크립트 URL** 는 선택적 설정 하 고 toospecify 공개적으로 사용할 수 있는 Windows PowerShell 스크립트 실행 된 후 hello 헤드 노드 VM에 toorun 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-146">hello **Post-configuration script URL** is an optional setting toospecify a publicly available Windows PowerShell script that you want toorun on hello head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="378d5-147">Hello에 **계산 노드 설정을** 블레이드에서 hello 노드, hello 번호 및 hello 노드의 크기에 대 한 명명 패턴을 선택 하 고 Linux 배포 toodeploy hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-147">On hello **Compute node settings** blade, select a naming pattern for hello nodes, hello number and size of hello nodes, and hello Linux distribution toodeploy.</span></span>
6. <span data-ttu-id="378d5-148">Hello에 **인프라 설정** 블레이드에서 hello 가상 네트워크 및 Active Directory에 대 한 이름을 입력 합니다. 도메인, 도메인 및 VM 관리자 자격 증명 및 hello 저장소 계정에 대 한 명명 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-148">On hello **Infrastructure settings** blade, enter names for hello virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for hello storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="378d5-149">HPC 팩 hello Active Directory 도메인 tooauthenticate 클러스터 사용자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-149">HPC Pack uses hello Active Directory domain tooauthenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="378d5-150">Hello 유효성 검사 테스트를 실행 하 고 hello 사용 약관을 검토 한 후 클릭 **구매**합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-150">After hello validation tests run and you review hello terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a><span data-ttu-id="378d5-151">배포 옵션 2.</span><span class="sxs-lookup"><span data-stu-id="378d5-151">Deployment option 2.</span></span> <span data-ttu-id="378d5-152">Hello IaaS 배포 스크립트를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="378d5-152">Use hello IaaS deployment script</span></span>
<span data-ttu-id="378d5-153">다음은 hello HPC Pack IaaS 배포 스크립트를 사용 하 여 추가 필수 구성 요소 toodeploy hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-153">Following are additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="378d5-154">**클라이언트 컴퓨터** -Windows 기반 클라이언트 컴퓨터 toorun hello 클러스터 배포 스크립트를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-154">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="378d5-155">**Azure PowerShell** - [Azure PowerShell(버전 0.8.10 이상)을 설치 및 구성](/powershell/azure/overview) 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="378d5-156">**HPC Pack IaaS 배포 스크립트** -다운로드 하 고 hello hello에서 hello 스크립트의 최신 버전을 푸는 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=44949)합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-156">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="378d5-157">실행 하 여 hello 스크립트의 hello 버전을 확인 하면 `.\New-HPCIaaSCluster.ps1 –Version`합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-157">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="378d5-158">이 문서는 4.4.1 버전 또는 hello 스크립트의 나중에 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-158">This article is based on version 4.4.1 or later of hello script.</span></span>

<span data-ttu-id="378d5-159">**XML 구성 파일**</span><span class="sxs-lookup"><span data-stu-id="378d5-159">**XML configuration file**</span></span>

<span data-ttu-id="378d5-160">HPC Pack IaaS 배포 스크립트 hello 입력된 toodescribe hello HPC 클러스터도 XML 구성 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-160">hello HPC Pack IaaS deployment script uses an XML configuration file as input toodescribe hello  HPC cluster.</span></span> <span data-ttu-id="378d5-161">hello 다음 샘플 구성 파일을 지정 두 크기 A7 CentOS 7.0 Linux 계산 노드 및 HPC Pack 헤드 노드 구성 된 작은 클러스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-161">hello following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="378d5-162">사용자 환경 및 원하는 클러스터 구성에 대 한 필요에 따라 hello 파일을 수정 하 고 HPCDemoConfig.xml 같은 이름으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-162">Modify hello file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="378d5-163">예를 들어 구독 이름 및 고유 저장소 계정 이름 및 클라우드 서비스 이름 toosupply 필요.</span><span class="sxs-lookup"><span data-stu-id="378d5-163">For example, you need toosupply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="378d5-164">또한 다른 toochoose hello 계산 노드에 대 한 Linux 이미지를 지원 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-164">Additionally, you might want toochoose a different supported Linux image for hello compute nodes.</span></span> <span data-ttu-id="378d5-165">Hello 요소 hello 구성 파일에 대 한 자세한 내용은 참조 하십시오. hello 스크립트 폴더에 있는 Manual.rtf 파일 hello 및 [hello HPC Pack IaaS 배포 스크립트는 HPC 클러스터 만들기](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-165">For more information about hello elements in hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

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

<span data-ttu-id="378d5-166">**toorun hello HPC Pack IaaS 배포 스크립트**</span><span class="sxs-lookup"><span data-stu-id="378d5-166">**toorun hello HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="378d5-167">Hello 클라이언트 컴퓨터에서 관리자 권한으로 Windows PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-167">Open Windows PowerShell on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="378d5-168">변경 스크립트 hello가 디렉터리 toohello 폴더 (이 예제의 E:\IaaSClusterScript)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-168">Change directory toohello folder where hello script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="378d5-169">다음 명령 toodeploy hello HPC Pack 클러스터 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-169">Run hello following command toodeploy hello HPC Pack cluster.</span></span> <span data-ttu-id="378d5-170">이 예에서는 해당 hello 구성 파일은 E:\HPCDemoConfig.xml 가정</span><span class="sxs-lookup"><span data-stu-id="378d5-170">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="378d5-171">a.</span><span class="sxs-lookup"><span data-stu-id="378d5-171">a.</span></span> <span data-ttu-id="378d5-172">때문에 hello **AdminPassword** 지정 하지 않으면 사용자에 대 한 증명된 tooenter hello 암호 중인 hello 명령 앞, *MyAdminName*합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-172">Because hello **AdminPassword** is not specified in hello preceding command, you are prompted tooenter hello password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="378d5-173">b.</span><span class="sxs-lookup"><span data-stu-id="378d5-173">b.</span></span> <span data-ttu-id="378d5-174">hello 스크립트 toovalidate hello 구성 파일을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-174">hello script then starts toovalidate hello configuration file.</span></span> <span data-ttu-id="378d5-175">Hello 네트워크 연결에 따라 tooseveral 분까지 걸릴 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-175">It can take up tooseveral minutes depending on hello network connection.</span></span>
   
    ![유효성 검사][validate]
   
    <span data-ttu-id="378d5-177">c.</span><span class="sxs-lookup"><span data-stu-id="378d5-177">c.</span></span> <span data-ttu-id="378d5-178">유효성 검사를 통과 hello 클러스터 리소스 toocreate hello 스크립트에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-178">After validations pass, hello script lists hello cluster resources toocreate.</span></span> <span data-ttu-id="378d5-179">입력 *Y* toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-179">Enter *Y* toocontinue.</span></span>
   
    ![리소스][resources]
   
    <span data-ttu-id="378d5-181">d.</span><span class="sxs-lookup"><span data-stu-id="378d5-181">d.</span></span> <span data-ttu-id="378d5-182">toodeploy hello HPC Pack 클러스터를 시작 하 고 추가 수동 단계 없이 hello 구성을 완료 하는 hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-182">hello script starts toodeploy hello HPC Pack cluster and completes hello configuration without further manual steps.</span></span> <span data-ttu-id="378d5-183">몇 분 동안 hello 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-183">hello script can run for several minutes.</span></span>
   
    ![배포][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="378d5-185">이 예제에서는 hello 스크립트 로그 파일을 자동으로 생성 hello 이후 **-로그 파일** 매개 변수가 지정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-185">In this example, hello script generates a log file automatically since hello **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="378d5-186">hello 로그 실시간으로 기록 되지 않으며 hello 유효성 검사 및 hello 배포의 hello 끝에 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-186">hello logs aren't written in real time, but are collected at hello end of hello validation and hello deployment.</span></span> <span data-ttu-id="378d5-187">Hello 스크립트가 실행 중인 PowerShell 프로세스 hello 중지 되 면 일부 로그 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-187">If hello PowerShell process is stopped while hello script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-toohello-head-node"></a><span data-ttu-id="378d5-188">Toohello 헤드 노드를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-188">Connect toohello head node</span></span>
<span data-ttu-id="378d5-189">Azure의 hello HPC Pack 클러스터를 배포한 후 [여 원격 데스크톱 연결](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello 클러스터를 배포할 때 지정한 도메인 자격 증명을 hello toohello 헤드 노드 VM를 사용 하 여 (예를 들어 *hpc\\ clusteradmin*).</span><span class="sxs-lookup"><span data-stu-id="378d5-189">After you deploy hello HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="378d5-190">Hello 헤드 노드에서 hello 클러스터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-190">You manage hello cluster from hello head node.</span></span>

<span data-ttu-id="378d5-191">Hello 헤드 노드에서 HPC 클러스터 관리자 toocheck hello 상태의 hello HPC Pack 클러스터를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-191">On hello head node, start HPC Cluster Manager toocheck hello status of hello HPC Pack cluster.</span></span> <span data-ttu-id="378d5-192">관리 및 모니터링 Linux 계산 노드 수 hello 동일한 방식으로 Windows를 사용 하는 계산 노드.</span><span class="sxs-lookup"><span data-stu-id="378d5-192">You can manage and monitor Linux compute nodes hello same way you work with Windows compute nodes.</span></span> <span data-ttu-id="378d5-193">에 나열 된 hello Linux 노드를 참조 하는 예를 들어 **리소스 관리** (이러한 노드가 hello로 배포 **LinuxNode** 템플릿).</span><span class="sxs-lookup"><span data-stu-id="378d5-193">For example, you see hello Linux nodes listed in **Resource Management** (these nodes are deployed with hello **LinuxNode** template).</span></span>

![노드 관리][management]

<span data-ttu-id="378d5-195">Hello에 hello Linux 노드에 표시 **열 지도** 보기.</span><span class="sxs-lookup"><span data-stu-id="378d5-195">You also see hello Linux nodes in hello **Heat Map** view.</span></span>

![열 지도][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="378d5-197">어떻게 Linux 노드에 있는 클러스터의 toomove 데이터</span><span class="sxs-lookup"><span data-stu-id="378d5-197">How toomove data in a cluster with Linux nodes</span></span>
<span data-ttu-id="378d5-198">Linux 노드 및 hello Windows hello 클러스터의 헤드 노드 간에 여러 선택 항목 toomove 데이터 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-198">You have several choices toomove data among Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="378d5-199">Hello 다음 섹션에서에서 자세히 설명 하는 세 가지 일반적인 방법 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-199">Here are three common methods, described in more detail in hello following sections:</span></span>

* <span data-ttu-id="378d5-200">**Azure 파일** -Azure 저장소에 관리 되는 SMB 파일 공유 toostore 데이터 파일을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-200">**Azure File** - Exposes a managed SMB file share toostore data files in Azure storage.</span></span> <span data-ttu-id="378d5-201">Windows 노드 및 Linux 노드 드라이브 또는 폴더에 hello Azure 파일 공유를 탑재할 수 서로 다른 가상 네트워크에 배포 되는 경우에 이와 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at hello same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="378d5-202">**헤드 노드 SMB 공유** -Linux 노드에 hello 헤드 노드의 표준 Windows 공유 폴더를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-202">**Head node SMB share** - Mounts a standard Windows shared folder of hello head node on Linux nodes.</span></span>
* <span data-ttu-id="378d5-203">**헤드 노드 NFS 서버** - Windows 및 Linux 혼합 환경에 대한 파일 공유 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="378d5-204">Azure 파일 저장소</span><span class="sxs-lookup"><span data-stu-id="378d5-204">Azure File storage</span></span>
<span data-ttu-id="378d5-205">hello [Azure 파일](https://azure.microsoft.com/services/storage/files/) 서비스는 hello 표준 SMB 2.1 프로토콜을 사용 하 여 파일 공유를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-205">hello [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using hello standard SMB 2.1 protocol.</span></span> <span data-ttu-id="378d5-206">Azure Vm 및 클라우드 서비스를 통해 탑재 된 공유 응용 프로그램 구성 요소에서 파일 데이터를 공유할 수 및 온-프레미스 응용 프로그램이 hello 파일 저장소 API 통해 공유에 파일 데이터를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through hello File storage API.</span></span> 

<span data-ttu-id="378d5-207">자세한 단계 toocreate Azure 파일 공유 하 고 hello 헤드 노드에서 탑재에 대 한 참조 [Windows에서 Azure 파일 저장소 시작](../../../storage/files/storage-how-to-use-files-windows.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-207">For detailed steps toocreate an Azure File share and mount it on hello head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="378d5-208">hello Linux 노드에 toomount hello Azure 파일 공유 참조 [어떻게 toouse Azure 파일 저장소와 Linux](../../../storage/files/storage-how-to-use-files-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-208">toomount hello Azure File share on hello Linux nodes, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="378d5-209">영구 연결을 tooset 참조 [Persisting 연결 tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-209">tooset up persisting connections, see [Persisting connections tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="378d5-210">다음 예제는 hello, 저장소 계정에서 Azure 파일 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-210">In hello following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="378d5-211">toomount hello hello 헤드 노드를 열고 명령 프롬프트를 공유 하 고 hello 명령 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-211">toomount hello share on hello head node, open a Command Prompt and enter hello following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="378d5-212">이 예제에서는 allvhdsje 저장소 계정 이름 storageaccountkey 저장소 계정 키가 있고, rdma는 hello Azure 파일 공유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is hello Azure File share name.</span></span> <span data-ttu-id="378d5-213">hello Azure 파일 공유는 hello 헤드 노드에서 z:로 탑재 됩니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-213">hello Azure File share is mounted as Z: on hello head node.</span></span>

<span data-ttu-id="378d5-214">실행 되는 Linux 노드 toomount hello Azure 파일 공유는 **clusrun** hello 헤드 노드에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-214">toomount hello Azure File share on Linux nodes, run a **clusrun** command on hello head node.</span></span> <span data-ttu-id="378d5-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)**  여러 노드에서 관리 작업 유용한 HPC Pack 도구 toocarry 됩니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool toocarry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="378d5-216">이 문서의 [Linux 노드에 대한 Clusrun](#Clusrun-for-Linux-nodes) 도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="378d5-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="378d5-217">Windows PowerShell 창을 열고 다음 명령을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-217">Open a Windows PowerShell window and enter hello following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="378d5-218">첫 번째 명령은 hello hello LinuxNodes 그룹의 모든 노드에서 /rdma 라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-218">hello first command creates a folder named /rdma on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="378d5-219">두 번째 명령은 hello hello Azure 파일 공유 allvhdsjw.file.core.windows.net/rdma dir 및 파일 모드 비트 집합 too777 hello /rdma 폴더에 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-219">hello second command mounts hello Azure File share allvhdsjw.file.core.windows.net/rdma onto hello /rdma folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="378d5-220">Hello 두 번째 명령에서 allvhdsje은 저장소 계정 이름 및 storageaccountkey 저장소 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-220">In hello second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="378d5-221">hello "\\`" hello 두 번째 명령은의 기호는 PowerShell에 대 한 이스케이프 기호는 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-221">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="378d5-222">"\\`,"의미 해당 hello"," (쉼표 문자)는 hello 명령의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-222">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="378d5-223">헤드 노드 공유</span><span class="sxs-lookup"><span data-stu-id="378d5-223">Head node share</span></span>
<span data-ttu-id="378d5-224">Linux 노드에 헤드 노드 hello의 공유 폴더를 탑재 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-224">Alternatively, mount a shared folder of hello head node on Linux nodes.</span></span> <span data-ttu-id="378d5-225">공유 hello 가장 간단한 방법은 tooshare 파일을 제공 하지만 hello에 hello 헤드 노드 및 모든 Linux 노드를 배포 해야 동일한 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-225">A share provides hello simplest way tooshare files, but hello head node and all Linux nodes must be deployed in hello same virtual network.</span></span> <span data-ttu-id="378d5-226">Hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-226">Here are hello steps.</span></span>

1. <span data-ttu-id="378d5-227">Hello 헤드 노드에 폴더를 만들고 읽기/쓰기 권한을 가진 tooEveryone을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-227">Create a folder on hello head node and share it tooEveryone with Read/Write permissions.</span></span> <span data-ttu-id="378d5-228">예를 들어 hello 헤드 노드의 D:\OpenFOAM 공유 \\CentOS7RDMA HN\OpenFOAM 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-228">For example, share D:\OpenFOAM on hello head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="378d5-229">다음 CentOS7RDMA HN은 hello 헤드 노드의 hello 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-229">Here CentOS7RDMA-HN is hello hostname of hello head node.</span></span>
   
    ![파일 공유 권한][fileshareperms]
   
    ![파일 공유][filesharing]
2. <span data-ttu-id="378d5-232">Windows PowerShell 창을 열고 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-232">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="378d5-233">첫 번째 명령은 hello hello LinuxNodes 그룹의 모든 노드에서 /openfoam 라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-233">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="378d5-234">두 번째 명령은 hello hello 공유 폴더 //CentOS7RDMA-HN/OpenFOAM dir 및 파일 모드 비트 집합 too777 hello 폴더에 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-234">hello second command mounts hello shared folder //CentOS7RDMA-HN/OpenFOAM onto hello folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="378d5-235">hello 사용자 이름 및 암호 hello 명령에 해야 hello 사용자 이름 및 hello 헤드 노드에서 클러스터 사용자의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-235">hello username and password in hello command should be hello username and password of a cluster user on hello head node.</span></span> <span data-ttu-id="378d5-236">( [클러스터 사용자 추가 또는 제거](https://technet.microsoft.com/library/ff919330.aspx)참조)</span><span class="sxs-lookup"><span data-stu-id="378d5-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="378d5-237">hello "\\`" hello 두 번째 명령은의 기호는 PowerShell에 대 한 이스케이프 기호는 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-237">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="378d5-238">"\\`,"의미 해당 hello"," (쉼표 문자)는 hello 명령의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-238">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="378d5-239">NFS 서버</span><span class="sxs-lookup"><span data-stu-id="378d5-239">NFS server</span></span>
<span data-ttu-id="378d5-240">hello NFS 서비스 tooshare 있으며 hello SMB 프로토콜을 사용 하 여 hello Windows Server 2012 운영 체제를 실행 하는 컴퓨터와 hello NFS 프로토콜을 사용 하 여 Linux 기반 컴퓨터 간의 파일 마이그레이션할 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-240">hello NFS service enables you tooshare and migrate files between computers running hello Windows Server 2012 operating system using hello SMB protocol and Linux-based computers using hello NFS protocol.</span></span> <span data-ttu-id="378d5-241">hello NFS 서버와 다른 모든 노드에 있는 toobe hello에 배포 된 동일한 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-241">hello NFS server and all other nodes have toobe deployed in hello same virtual network.</span></span> <span data-ttu-id="378d5-242">SMB 공유에 비해 Linux 노드와의 호환성이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="378d5-243">예를 들어 파일 링크를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="378d5-244">NFS 서버를 설치한 집합과 tooinstall hello 단계에 따라 [네트워크 파일 시스템에 대 한 첫 번째 공유 종단에 대 한 서버](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-244">tooinstall and set up an NFS server, follow hello steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="378d5-245">예를 들어 다음과 같은 속성 hello로 nfs 라는 NFS 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-245">For example, create an NFS share named nfs with hello following properties:</span></span>
   
    ![NFS 권한 부여][nfsauth]
   
    ![NFS 공유 권한][nfsshare]
   
    ![NFS NTFS 사용 권한][nfsperm]
   
    ![NFS 관리 속성][nfsmanage]
2. <span data-ttu-id="378d5-250">Windows PowerShell 창을 열고 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-250">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="378d5-251">첫 번째 명령은 hello hello LinuxNodes 그룹의 모든 노드에서 /nfsshared 라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-251">hello first command creates a folder named /nfsshared on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="378d5-252">hello 두 번째 명령은 마운트 hello NFS 공유 CentOS7RDMA HN:에 nfs hello 폴더 / 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-252">hello second command mounts hello NFS share CentOS7RDMA-HN:/nfs onto hello folder.</span></span> <span data-ttu-id="378d5-253">여기 CentOS7RDMA HN: / nfs는 NFS 공유의 hello 원격 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-253">Here CentOS7RDMA-HN:/nfs is hello remote path of your NFS share.</span></span>

## <a name="how-toosubmit-jobs"></a><span data-ttu-id="378d5-254">어떻게 toosubmit 작업</span><span class="sxs-lookup"><span data-stu-id="378d5-254">How toosubmit jobs</span></span>
<span data-ttu-id="378d5-255">여러 가지 방법으로 toosubmit 작업 toohello HPC Pack 클러스터 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-255">There are several ways toosubmit jobs toohello HPC Pack cluster:</span></span>

* <span data-ttu-id="378d5-256">HPC 클러스터 관리자 또는 HPC 작업 관리자 GUI</span><span class="sxs-lookup"><span data-stu-id="378d5-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="378d5-257">HPC 웹 포털</span><span class="sxs-lookup"><span data-stu-id="378d5-257">HPC web portal</span></span>
* <span data-ttu-id="378d5-258">REST API</span><span class="sxs-lookup"><span data-stu-id="378d5-258">REST API</span></span>

<span data-ttu-id="378d5-259">Azure의 HPC 팩 GUI 도구 및 hello HPC 웹 포털을 통해 toohello 클러스터는 동일한 Windows 계산 노드: hello 작업 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-259">Job submission toohello cluster in Azure via HPC Pack GUI tools and hello HPC web portal are hello same as for Windows compute nodes.</span></span> <span data-ttu-id="378d5-260">참조 [HPC 팩 작업 관리자](https://technet.microsoft.com/library/ff919691.aspx) 및 [toosubmit 온-프레미스 클라이언트 컴퓨터에서 작업 하는 방법을](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How toosubmit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="378d5-261">hello REST API를 통해 toosubmit 작업 너무 참조[만들기 및 사용 하 여 작업을 제출 hello Microsoft HPC Pack에서 REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-261">toosubmit jobs via hello REST API, refer too[Creating and Submitting Jobs by Using hello REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="378d5-262">Linux 클라이언트에서 toosubmit 작업은 또한 toohello Python 샘플 hello에 참조할 [HPC 팩 SDK](https://www.microsoft.com/download/details.aspx?id=47756)합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-262">toosubmit jobs from a Linux client, also refer toohello Python sample in hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="378d5-263">Linux 노드에 대한 Clusrun</span><span class="sxs-lookup"><span data-stu-id="378d5-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="378d5-264">HPC Pack hello [clusrun](https://technet.microsoft.com/library/cc947685.aspx) 도구 명령 프롬프트 또는 HPC 클러스터 관리자를 통해 Linux 노드에 사용 되는 tooexecute 명령 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-264">hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used tooexecute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="378d5-265">다음은 몇 가지 기본적인 예입니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-265">Following are some basic examples.</span></span>

* <span data-ttu-id="378d5-266">Hello 클러스터의 모든 노드에서 현재 사용자 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-266">Show current user names on all nodes in hello cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="378d5-267">Hello 설치 **gdb** 사용 하는 디버거 도구 **yum** hello linuxnodes 그룹화 하 고 다음 10 분 후 hello 노드를 다시 시작의 모든 노드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-267">Install hello **gdb** debugger tool with **yum** on all nodes in hello linuxnodes group and then restart hello nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="378d5-268">Hello 클러스터의 각 숫자 1부터 각 Linux 노드 상의 1 초 동안 10 표시 하는 셸 스크립트를 만들고, 실행 hello 노드에서 출력을 즉시 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in hello cluster, run it, and show output from hello nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="378d5-269">Toouse 해야 특정 문자를 이스케이프 **clusrun** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-269">You might need toouse certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="378d5-270">이 예에서 볼 수 있듯이 사용 하 여 ^ 명령 프롬프트 tooescape hello에 ">" 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-270">As shown in this example, use ^ in a Command Prompt tooescape hello ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="378d5-271">다음 단계</span><span class="sxs-lookup"><span data-stu-id="378d5-271">Next steps</span></span>
* <span data-ttu-id="378d5-272">Hello 클러스터 tooa 많은 노드를 확장 하거나 hello 클러스터에서 Linux 워크 로드를 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="378d5-272">Try scaling up hello cluster tooa larger number of nodes, or try running a Linux workload on hello cluster.</span></span> <span data-ttu-id="378d5-273">예제는 [Azure의 Linux 계산 노드에서 Microsoft HPC 팩을 사용하여 NAMD 실행](hpcpack-cluster-namd.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="378d5-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="378d5-274">사용 하 여 클러스터 시도 [RDMA 가능, 계산 집약적인 Vm](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI workloads.</span></span> <span data-ttu-id="378d5-275">그에 대한 예는 [Azure의 Linux RDMA 클러스터에서 Microsoft HPC Pack을 사용하여 OpenFOAM 실행](hpcpack-cluster-openfoam.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="378d5-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="378d5-276">Linux 노드 온-프레미스 HPC Pack 클러스터에서 작업에 관심이 있는 경우 참조 hello [TechNet 설명서](https://technet.microsoft.com/library/mt595803.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="378d5-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see hello [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

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
