---
title: "hello 클라우드에서 aaaLinux HPC 팩 클러스터 옵션 | Microsoft Docs"
description: "Microsoft HPC Pack toocreate와 옵션에 대해 알아보고는 Linux 고성능 컴퓨팅 hello Azure 클라우드에서에서 (HPC) 클러스터 관리"
services: virtual-machines-linux,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 60d093b466f44a0391815842c421c328e8c7a0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a><span data-ttu-id="f455f-103">HPC Pack toocreate와 옵션 및 Linux 작업을 위해 Azure의 HPC 클러스터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f455f-103">Options with HPC Pack toocreate and manage an HPC cluster in Azure for Linux workloads</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="f455f-104">이 문서 옵션 toouse HPC Pack toorun Linux 워크 로드에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f455f-104">This article focuses on options toouse HPC Pack toorun Linux workloads.</span></span> <span data-ttu-id="f455f-105">또한 [HPC 팩을 사용하여 Windows HPC 워크로드](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 실행할 때 사용 가능한 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f455f-105">There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="f455f-106">Azure VM에서 HPC Pack 클러스터 실행</span><span class="sxs-lookup"><span data-stu-id="f455f-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="f455f-107">Azure 템플릿</span><span class="sxs-lookup"><span data-stu-id="f455f-107">Azure templates</span></span>
* <span data-ttu-id="f455f-108">(GitHub) [HPC 팩 2016 클러스터 템플릿](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="f455f-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="f455f-109">(마켓플레이스) [Linux 워크로드용 HPC Pack 클러스터](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span><span class="sxs-lookup"><span data-stu-id="f455f-109">(Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span></span>
* <span data-ttu-id="f455f-110">(퀵 스타트) [Linux 계산 노드가 포함된 HPC 클러스터 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span><span class="sxs-lookup"><span data-stu-id="f455f-110">(Quickstart) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span></span>

### <a name="powershell-deployment-script"></a><span data-ttu-id="f455f-111">PowerShell 배포 스크립트</span><span class="sxs-lookup"><span data-stu-id="f455f-111">PowerShell deployment script</span></span>
* [<span data-ttu-id="f455f-112">HPC Pack IaaS 배포 스크립트 hello로 Linux HPC 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="f455f-112">Create a Linux HPC cluster with hello HPC Pack IaaS deployment script</span></span>](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="f455f-113">자습서</span><span class="sxs-lookup"><span data-stu-id="f455f-113">Tutorials</span></span>
* [<span data-ttu-id="f455f-114">자습서: Azure에서 HPC 팩 클러스터의 Linux 컴퓨터 노드 시작</span><span class="sxs-lookup"><span data-stu-id="f455f-114">Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="f455f-115">자습서: Azure의 Linux 계산 노드에서 Microsoft HPC 팩을 사용하여 NAMD 실행</span><span class="sxs-lookup"><span data-stu-id="f455f-115">Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="f455f-116">자습서: Azure의 Linux RDMA 클러스터에서 Microsoft HPC 팩을 사용하여 OpenFOAM 실행</span><span class="sxs-lookup"><span data-stu-id="f455f-116">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="f455f-117">자습서: Azure의 Linux RDMA 클러스터에서 Microsoft HPC 팩으로 STAR-CCM+ 실행</span><span class="sxs-lookup"><span data-stu-id="f455f-117">Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="f455f-118">클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="f455f-118">Cluster management</span></span>
* [<span data-ttu-id="f455f-119">Azure의 tooan HPC Pack 클러스터 작업 제출</span><span class="sxs-lookup"><span data-stu-id="f455f-119">Submit jobs tooan HPC Pack cluster in Azure</span></span>](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="f455f-120">HPC Pack의 작업 관리</span><span class="sxs-lookup"><span data-stu-id="f455f-120">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="f455f-121">MPI 작업에 대한 RDMA 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="f455f-121">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="f455f-122">자습서: Azure의 Linux RDMA 클러스터에서 Microsoft HPC 팩을 사용하여 OpenFOAM 실행</span><span class="sxs-lookup"><span data-stu-id="f455f-122">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="f455f-123">Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="f455f-123">Set up a Linux RDMA cluster toorun MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

