---
title: "aaaWindows HPC 팩 클러스터 hello 클라우드에서 옵션 | Microsoft Docs"
description: "Microsoft HPC Pack toocreate와 옵션에 대해 알아보고는 Windows 고성능 컴퓨팅 hello Azure 클라우드에서에서 (HPC) 클러스터 관리"
services: virtual-machines-windows,cloud-services,batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 6158d9dd0cecda38b14f85a2b2080163f18e8cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a><span data-ttu-id="aaffb-103">HPC Pack toocreate와 옵션 및 Azure에서 Windows HPC 클러스터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaffb-103">Options with HPC Pack toocreate and manage a Windows HPC cluster in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="aaffb-104">이 문서에서는 옵션 toocreate HPC Pack 클러스터 toorun Windows 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="aaffb-104">This article focuses on options toocreate HPC Pack clusters toorun Windows workloads.</span></span> <span data-ttu-id="aaffb-105">또한 옵션에 대 한 사항이 만드는 HPC 팩 클러스터 toorun [Linux HPC 작업](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="aaffb-105">There are also options for creating HPC Pack clusters toorun [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="aaffb-106">Azure VM에서 HPC Pack 클러스터 실행</span><span class="sxs-lookup"><span data-stu-id="aaffb-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="aaffb-107">Azure 템플릿</span><span class="sxs-lookup"><span data-stu-id="aaffb-107">Azure templates</span></span>
* <span data-ttu-id="aaffb-108">(GitHub) [HPC 팩 2016 클러스터 템플릿](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="aaffb-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="aaffb-109">(마켓플레이스) [Windows 워크로드용 HPC 팩 클러스터](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span><span class="sxs-lookup"><span data-stu-id="aaffb-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span></span>
* <span data-ttu-id="aaffb-110">(마켓플레이스) [Excel 워크로드용 HPC 팩 클러스터](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span><span class="sxs-lookup"><span data-stu-id="aaffb-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span></span>
* <span data-ttu-id="aaffb-111">(퀵 스타트) [HPC 클러스터 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="aaffb-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="aaffb-112">(퀵 스타트) [사용자 지정 계산 노드 이미지로 HPC 클러스터 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="aaffb-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="aaffb-113">Azure VM 이미지</span><span class="sxs-lookup"><span data-stu-id="aaffb-113">Azure VM images</span></span>
* [<span data-ttu-id="aaffb-114">Windows Server 2016의 HPC Pack 2016 헤드 노드</span><span class="sxs-lookup"><span data-stu-id="aaffb-114">HPC Pack 2016 head node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="aaffb-115">Windows Server 2016의 HPC Pack 2016 계산 노드</span><span class="sxs-lookup"><span data-stu-id="aaffb-115">HPC Pack 2016 compute node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="aaffb-116">Windows Server 2012 R2의 HPC Pack 2016 헤드 노드</span><span class="sxs-lookup"><span data-stu-id="aaffb-116">HPC Pack 2016 head node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="aaffb-117">Windows Server 2012 R2의 HPC Pack 2016 계산 노드</span><span class="sxs-lookup"><span data-stu-id="aaffb-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="aaffb-118">Windows Server 2012 R2의 HPC Pack 2012 R2 헤드 노드</span><span class="sxs-lookup"><span data-stu-id="aaffb-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [<span data-ttu-id="aaffb-119">Windows Server 2012 R2의 HPC Pack 2012 R2 계산 노드</span><span class="sxs-lookup"><span data-stu-id="aaffb-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [<span data-ttu-id="aaffb-120">HPC Pack compute node with Excel on Windows Server 2012 R2(영문)</span><span class="sxs-lookup"><span data-stu-id="aaffb-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a><span data-ttu-id="aaffb-121">PowerShell 배포 스크립트</span><span class="sxs-lookup"><span data-stu-id="aaffb-121">PowerShell deployment script</span></span>
* [<span data-ttu-id="aaffb-122">Hello HPC Pack IaaS 배포 스크립트는 HPC 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="aaffb-122">Create an HPC cluster with hello HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="aaffb-123">자습서</span><span class="sxs-lookup"><span data-stu-id="aaffb-123">Tutorials</span></span>
* [<span data-ttu-id="aaffb-124">자습서: Azure에서 HPC 팩 2016 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="aaffb-124">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span></span>](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="aaffb-125">자습서: Azure toorun Excel에서에서 HPC Pack 클러스터 및 SOA 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaffb-125">Tutorial: Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a><span data-ttu-id="aaffb-126">Azure 포털 hello로 수동 배포</span><span class="sxs-lookup"><span data-stu-id="aaffb-126">Manual deployment with hello Azure portal</span></span>
* [<span data-ttu-id="aaffb-127">Azure VM에서 HPC Pack 클러스터의 헤드 노드 hello 설정</span><span class="sxs-lookup"><span data-stu-id="aaffb-127">Set up hello head node of an HPC Pack cluster in an Azure VM</span></span>](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="aaffb-128">클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="aaffb-128">Cluster management</span></span>
* [<span data-ttu-id="aaffb-129">Azure에서 HPC 팩 클러스터의 컴퓨터 노드 관리</span><span class="sxs-lookup"><span data-stu-id="aaffb-129">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="aaffb-130">HPC 팩 클러스터에서 Azure 계산 리소스 확장 및 축소</span><span class="sxs-lookup"><span data-stu-id="aaffb-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="aaffb-131">Azure의 tooan HPC Pack 클러스터 작업 제출</span><span class="sxs-lookup"><span data-stu-id="aaffb-131">Submit jobs tooan HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="aaffb-132">HPC Pack의 작업 관리</span><span class="sxs-lookup"><span data-stu-id="aaffb-132">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)
* [<span data-ttu-id="aaffb-133">Azure Active Directory로 Azure에서 HPC 팩 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="aaffb-133">Manage an HPC Pack cluster in Azure with Azure Active Directory</span></span>](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a><span data-ttu-id="aaffb-134">작업자 역할 노드 tooan HPC Pack 클러스터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaffb-134">Add worker role nodes tooan HPC Pack cluster</span></span>
* [<span data-ttu-id="aaffb-135">HPC Pack을 사용한 tooAzure 작업자 인스턴스 버스트</span><span class="sxs-lookup"><span data-stu-id="aaffb-135">Burst tooAzure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="aaffb-136">자습서: Azure에서 HPC 팩을 사용하여 하이브리드 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="aaffb-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [<span data-ttu-id="aaffb-137">Azure의 Azure "전환" 노드 tooan HPC Pack 헤드 노드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaffb-137">Add Azure "burst" nodes tooan HPC Pack head node in Azure</span></span>](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a><span data-ttu-id="aaffb-138">Azure 배치와의 통합</span><span class="sxs-lookup"><span data-stu-id="aaffb-138">Integrate with Azure Batch</span></span>
* [<span data-ttu-id="aaffb-139">버스트 tooAzure HPC Pack을 사용한 일괄 처리</span><span class="sxs-lookup"><span data-stu-id="aaffb-139">Burst tooAzure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="aaffb-140">MPI 작업에 대한 RDMA 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="aaffb-140">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="aaffb-141">HPC Pack toorun MPI 응용 프로그램을 사용 하 여 Windows RDMA 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="aaffb-141">Set up a Windows RDMA cluster with HPC Pack toorun MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

