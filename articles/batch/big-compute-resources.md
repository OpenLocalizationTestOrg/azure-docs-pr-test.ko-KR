---
title: "HPC 및 일괄 처리에 대 한 Azure 클라우드 hello에 aaaResources | Microsoft Docs"
description: "대규모 병렬, 일괄 처리 및 고성능 컴퓨팅 Azure에서 (HPC) 작업을 실행 하는 기술 리소스 toohelp를 나열 합니다."
services: batch, cloud-services, virtual-machines
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 6f8be911-c841-41ae-88d3-3bcfc029eb7f
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 03/17/2017
ms.author: danlep
ms.openlocfilehash: ab8ba24678bd7ec090306b501d29ca63c4fb83ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a><span data-ttu-id="031e0-103">Azure에서의 큰 계산: 배치 및 고성능 컴퓨팅에 대한 기술 리소스</span><span class="sxs-lookup"><span data-stu-id="031e0-103">Big Compute in Azure: Technical resources for batch and high-performance computing</span></span>
<span data-ttu-id="031e0-104">Azure에서 대규모 병렬, 일괄 처리 및 HPC ()를 계산 하는 고성능 워크 로드를 실행 하는 가이드 tootechnical 리소스 toohelp입니다.</span><span class="sxs-lookup"><span data-stu-id="031e0-104">This is a guide tootechnical resources toohelp you run your large-scale parallel, batch, and high-performance computing (HPC) workloads in Azure.</span></span> <span data-ttu-id="031e0-105">기존 일괄 처리 또는 HPC 작업 toohello Azure 클라우드 늘리거나 한 Azure 서비스를 사용 하 여 새 큰 계산 솔루션을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="031e0-105">Extend your existing batch or HPC workloads toohello Azure cloud, or build new Big Compute solutions using a range of Azure services.</span></span>

## <a name="solutions-options"></a><span data-ttu-id="031e0-106">솔루션 옵션</span><span class="sxs-lookup"><span data-stu-id="031e0-106">Solutions options</span></span>
<span data-ttu-id="031e0-107">Azure의 큰 계산 옵션에 대 한 확인 하 고 hello 적합 한 접근 방식을 작업 및 비즈니스 요구 사항에 대 한 선택 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="031e0-107">Learn about Big Compute options in Azure, and choose hello right approach for your workload and business need.</span></span>

* [<span data-ttu-id="031e0-108">배치 및 HPC 솔루션</span><span class="sxs-lookup"><span data-stu-id="031e0-108">Batch and HPC solutions</span></span>](batch-hpc-solutions.md)
* [<span data-ttu-id="031e0-109">비디오: Azure 및 HPC hello 클라우드에서 큰 계산</span><span class="sxs-lookup"><span data-stu-id="031e0-109">Video: Big Compute in hello cloud with Azure and HPC</span></span>](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a><span data-ttu-id="031e0-110">Azure 배치</span><span class="sxs-lookup"><span data-stu-id="031e0-110">Azure Batch</span></span>
<span data-ttu-id="031e0-111">[일괄 처리](https://azure.microsoft.com/services/batch/) 는 Linux 및 Windows 응용 프로그램 및 실행된 작업을 설정 하 고 클러스터 및 작업 스케줄러를 관리 하지 않고 쉽게 toocloud 사용 하는 플랫폼 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="031e0-111">[Batch](https://azure.microsoft.com/services/batch/) is a platform service that makes it easy toocloud-enable your Linux and Windows applications and run jobs without setting up and managing a cluster and job scheduler.</span></span> <span data-ttu-id="031e0-112">Azure 일괄 처리와 hello SDK toointegrate 클라이언트 응용 프로그램을 사용 하 여 다양 한 언어, 단계 데이터 tooAzure 통해 및 파이프라인을 실행 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="031e0-112">Use hello SDK toointegrate client applications with Azure Batch through various languages, stage data tooAzure, and build job execution pipelines.</span></span>

* [<span data-ttu-id="031e0-113">설명서</span><span class="sxs-lookup"><span data-stu-id="031e0-113">Documentation</span></span>](https://azure.microsoft.com/documentation/services/batch/)
* <span data-ttu-id="031e0-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/) 및 [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API 참조</span><span class="sxs-lookup"><span data-stu-id="031e0-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), and [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API reference</span></span>
* <span data-ttu-id="031e0-115">[배치 관리 .NET 라이브러리](https://msdn.microsoft.com/library/mt463120.aspx) 참조</span><span class="sxs-lookup"><span data-stu-id="031e0-115">[Batch management .NET library](https://msdn.microsoft.com/library/mt463120.aspx) reference</span></span>
* <span data-ttu-id="031e0-116">자습서: [.NET용 Azure 배치 라이브러리](batch-dotnet-get-started.md) 및 [배치 Python 클라이언트](batch-python-tutorial.md) 시작하기</span><span class="sxs-lookup"><span data-stu-id="031e0-116">Tutorials: Get started with [Azure Batch library for .NET](batch-dotnet-get-started.md) and [Batch Python client](batch-python-tutorial.md)</span></span>
* [<span data-ttu-id="031e0-117">배치 포럼</span><span class="sxs-lookup"><span data-stu-id="031e0-117">Batch forum</span></span>](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [<span data-ttu-id="031e0-118">배치 비디오</span><span class="sxs-lookup"><span data-stu-id="031e0-118">Batch videos</span></span>](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a><span data-ttu-id="031e0-119">HPC 클러스터 솔루션</span><span class="sxs-lookup"><span data-stu-id="031e0-119">HPC cluster solutions</span></span>
<span data-ttu-id="031e0-120">배포 또는 사용자 기존 Windows 또는 Linux HPC 클러스터 tooAzure toorun 계산 집약적인 작업을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="031e0-120">Deploy or extend your existing Windows or Linux HPC cluster tooAzure toorun your compute intensive workloads.</span></span>  

### <a name="microsoft-hpc-pack"></a><span data-ttu-id="031e0-121">Microsoft HPC 팩</span><span class="sxs-lookup"><span data-stu-id="031e0-121">Microsoft HPC Pack</span></span>
<span data-ttu-id="031e0-122">HPC Pack은 Microsoft Azure 및 Windows Server 기술로 구축된 무료 HPC 솔루션으로, Windows와 Linux HPC 작업을 모두 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="031e0-122">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies, capable of running Windows and Linux HPC workloads.</span></span>  

* [<span data-ttu-id="031e0-123">HPC Pack 2016 R2 다운로드</span><span class="sxs-lookup"><span data-stu-id="031e0-123">Download HPC Pack 2016</span></span>](https://www.microsoft.com/download/details.aspx?id=54507)
* [<span data-ttu-id="031e0-124">HPC 팩 2012 R2 업데이트 3 다운로드(영문)</span><span class="sxs-lookup"><span data-stu-id="031e0-124">Download HPC Pack 2012 R2 Update 3</span></span>](https://www.microsoft.com/download/details.aspx?id=49922)
* [<span data-ttu-id="031e0-125">설명서</span><span class="sxs-lookup"><span data-stu-id="031e0-125">Documentation</span></span>](https://technet.microsoft.com/library/jj899572.aspx)
* <span data-ttu-id="031e0-126">Azure의 HPC Pack 클러스터 옵션: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 및 [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="031e0-126">HPC Pack cluster options in Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span> 
* [<span data-ttu-id="031e0-127">HPC Pack을 사용한 tooAzure 작업자 인스턴스 버스트</span><span class="sxs-lookup"><span data-stu-id="031e0-127">Burst tooAzure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="031e0-128">버스트 tooAzure HPC Pack을 사용한 일괄 처리</span><span class="sxs-lookup"><span data-stu-id="031e0-128">Burst tooAzure  Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)
* [<span data-ttu-id="031e0-129">Windows HPC 포럼</span><span class="sxs-lookup"><span data-stu-id="031e0-129">Windows HPC forums</span></span>](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a><span data-ttu-id="031e0-130">Linux 및 OSS 클러스터 솔루션</span><span class="sxs-lookup"><span data-stu-id="031e0-130">Linux and OSS cluster solutions</span></span>
<span data-ttu-id="031e0-131">이러한 Azure 템플릿 toodeploy Linux HPC 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="031e0-131">Use these Azure templates toodeploy Linux HPC clusters.</span></span>

* <span data-ttu-id="031e0-132">[SLURM 클러스터 스핀업](https://azure.microsoft.com/documentation/templates/slurm/) 및 [블로그 게시물](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="031e0-132">[Spin up a SLURM cluster](https://azure.microsoft.com/documentation/templates/slurm/) and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span></span>
* [<span data-ttu-id="031e0-133">토크 클러스터 스핀업</span><span class="sxs-lookup"><span data-stu-id="031e0-133">Spin up a Torque cluster</span></span>](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [<span data-ttu-id="031e0-134">PBS Professional을 사용한 계산 그리드 템플릿</span><span class="sxs-lookup"><span data-stu-id="031e0-134">Compute grid templates with PBS Professional</span></span>](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a><span data-ttu-id="031e0-135">HPC 저장소</span><span class="sxs-lookup"><span data-stu-id="031e0-135">HPC storage</span></span>
* [<span data-ttu-id="031e0-136">Azure의 HPC 저장소를 위한 병렬 파일 시스템</span><span class="sxs-lookup"><span data-stu-id="031e0-136">Parallel file systems for HPC storage on Azure</span></span>](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [<span data-ttu-id="031e0-137">Lustre 소프트웨어용 Intel 클라우드 버전 - Eval</span><span class="sxs-lookup"><span data-stu-id="031e0-137">Intel Cloud Edition for Lustre Software - Eval</span></span>](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [<span data-ttu-id="031e0-138">CentOS 7.2 템플릿의 BeeGFS</span><span class="sxs-lookup"><span data-stu-id="031e0-138">BeeGFS on CentOS 7.2 template</span></span>](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a><span data-ttu-id="031e0-139">Microsoft MPI</span><span class="sxs-lookup"><span data-stu-id="031e0-139">Microsoft MPI</span></span>
<span data-ttu-id="031e0-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) hello 메시지 전달 인터페이스 표준을 개발 하 고 hello Windows 플랫폼에서 실행 중인 병렬 응용 프로그램의 Microsoft 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="031e0-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) is a Microsoft implementation of hello Message Passing Interface standard for developing and running parallel applications on hello Windows platform.</span></span>

* [<span data-ttu-id="031e0-141">MS-MPI 다운로드</span><span class="sxs-lookup"><span data-stu-id="031e0-141">Download MS-MPI</span></span>](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [<span data-ttu-id="031e0-142">MS-MPI 참조(영문)</span><span class="sxs-lookup"><span data-stu-id="031e0-142">MS-MPI reference</span></span>](https://msdn.microsoft.com/library/dn473458.aspx)
* [<span data-ttu-id="031e0-143">MPI 포럼</span><span class="sxs-lookup"><span data-stu-id="031e0-143">MPI forum</span></span>](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a><span data-ttu-id="031e0-144">계산 집약적 인스턴스</span><span class="sxs-lookup"><span data-stu-id="031e0-144">Compute-intensive instances</span></span>
<span data-ttu-id="031e0-145">Azure 제안의 [VM의 범위 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 포함 하 여 [계산 집약적인 H 시리즈](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 인스턴스 tooa 백 엔드 RDMA 네트워크 toorun Linux 및 Windows HPC 작업을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="031e0-145">Azure offers a [range of VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), including [compute-intensive H-series](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instances capable of connecting tooa back-end RDMA network, toorun your Linux and Windows HPC workloads.</span></span> 

* [<span data-ttu-id="031e0-146">Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="031e0-146">Set up a Linux RDMA cluster toorun MPI applications</span></span>](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="031e0-147">Microsoft HPC Pack toorun MPI 응용 프로그램을 사용 하 여 Windows RDMA 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="031e0-147">Set up a Windows RDMA cluster with Microsoft HPC Pack toorun MPI applications</span></span>](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

<span data-ttu-id="031e0-148">GPU가 많이 사용되는 워크로드의 경우 [NC 및 NV 크기](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="031e0-148">For GPU-intensive workloads, check out [NC and NV sizes](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span></span>

## <a name="samples-and-demos"></a><span data-ttu-id="031e0-149">샘플 및 데모</span><span class="sxs-lookup"><span data-stu-id="031e0-149">Samples and demos</span></span>
* [<span data-ttu-id="031e0-150">Azure 배치 C# 및 Python 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="031e0-150">Azure Batch C# and Python code samples</span></span>](https://github.com/Azure/azure-batch-samples)
* <span data-ttu-id="031e0-151">[대형 조선소 일괄 처리](https://azure.github.io/batch-shipyard/) 일괄 처리 스타일 Dockerized 작업 tooAzure 일괄 처리의 간편한 배포를 위해 도구 키트</span><span class="sxs-lookup"><span data-stu-id="031e0-151">[Batch Shipyard](https://azure.github.io/batch-shipyard/) toolkit for easy deployment of batch-style Dockerized workloads tooAzure Batch</span></span>
* <span data-ttu-id="031e0-152">Azure Batch를 기반으로 구축된 [doAzureParallel](http://www.github.com/Azure/doAzureParallel) R 패키지</span><span class="sxs-lookup"><span data-stu-id="031e0-152">[doAzureParallel](http://www.github.com/Azure/doAzureParallel) R package, built on top of Azure Batch</span></span>
* [<span data-ttu-id="031e0-153">HPC용 SUSE Linux Enterprise Server 시험 사용</span><span class="sxs-lookup"><span data-stu-id="031e0-153">Test drive SUSE Linux Enterprise Server for HPC</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a><span data-ttu-id="031e0-154">관련 Azure 서비스</span><span class="sxs-lookup"><span data-stu-id="031e0-154">Related Azure services</span></span>
* [<span data-ttu-id="031e0-155">데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="031e0-155">Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)
* [<span data-ttu-id="031e0-156">기계 학습</span><span class="sxs-lookup"><span data-stu-id="031e0-156">Machine Learning</span></span>](https://azure.microsoft.com/documentation/services/machine-learning/)
* [<span data-ttu-id="031e0-157">HDInsight</span><span class="sxs-lookup"><span data-stu-id="031e0-157">HDInsight</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="031e0-158">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="031e0-158">Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="031e0-159">가상 컴퓨터 확장 집합</span><span class="sxs-lookup"><span data-stu-id="031e0-159">Virtual Machine Scale Sets</span></span>](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [<span data-ttu-id="031e0-160">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="031e0-160">Cloud Services</span></span>](https://azure.microsoft.com/documentation/services/cloud-services/)
* [<span data-ttu-id="031e0-161">앱 서비스</span><span class="sxs-lookup"><span data-stu-id="031e0-161">App Service</span></span>](https://azure.microsoft.com/documentation/services/app-service/)
* [<span data-ttu-id="031e0-162">미디어 서비스</span><span class="sxs-lookup"><span data-stu-id="031e0-162">Media Services</span></span>](https://azure.microsoft.com/documentation/services/media-services/)
* [<span data-ttu-id="031e0-163">함수</span><span class="sxs-lookup"><span data-stu-id="031e0-163">Functions</span></span>](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a><span data-ttu-id="031e0-164">아키텍처 청사진</span><span class="sxs-lookup"><span data-stu-id="031e0-164">Architecture blueprints</span></span>
* <span data-ttu-id="031e0-165">[Azure Batch 및 Azure Data Factory를 사용하여 HPC 및 데이터 오케스트레이션](http://go.microsoft.com/fwlink/?linkid=717686)(PDF) 및 [문서](../data-factory/data-factory-data-processing-using-batch.md)</span><span class="sxs-lookup"><span data-stu-id="031e0-165">[HPC and data orchestration using Azure Batch and Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) and [article](../data-factory/data-factory-data-processing-using-batch.md)</span></span>

## <a name="industry-solutions"></a><span data-ttu-id="031e0-166">업계 솔루션</span><span class="sxs-lookup"><span data-stu-id="031e0-166">Industry solutions</span></span>
* [<span data-ttu-id="031e0-167">뱅킹 및 자금 시장</span><span class="sxs-lookup"><span data-stu-id="031e0-167">Banking and capital markets</span></span>](https://finance.azure.com/)
* [<span data-ttu-id="031e0-168">엔지니어링 시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="031e0-168">Engineering simulations</span></span>](https://simulation.azure.com/) 

## <a name="customer-stories"></a><span data-ttu-id="031e0-169">고객 사례</span><span class="sxs-lookup"><span data-stu-id="031e0-169">Customer stories</span></span>
* [<span data-ttu-id="031e0-170">ANEO</span><span class="sxs-lookup"><span data-stu-id="031e0-170">ANEO</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [<span data-ttu-id="031e0-171">d3View</span><span class="sxs-lookup"><span data-stu-id="031e0-171">d3View</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [<span data-ttu-id="031e0-172">Ludwig Institute of Cancer Research</span><span class="sxs-lookup"><span data-stu-id="031e0-172">Ludwig Institute of Cancer Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [<span data-ttu-id="031e0-173">Microsoft Research</span><span class="sxs-lookup"><span data-stu-id="031e0-173">Microsoft Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [<span data-ttu-id="031e0-174">Milliman</span><span class="sxs-lookup"><span data-stu-id="031e0-174">Milliman</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [<span data-ttu-id="031e0-175">Mitsubishi UFJ Securities International</span><span class="sxs-lookup"><span data-stu-id="031e0-175">Mitsubishi UFJ Securities International</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [<span data-ttu-id="031e0-176">Schlumberger</span><span class="sxs-lookup"><span data-stu-id="031e0-176">Schlumberger</span></span>](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [<span data-ttu-id="031e0-177">Towers Watson</span><span class="sxs-lookup"><span data-stu-id="031e0-177">Towers Watson</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [<span data-ttu-id="031e0-178">UberCloud</span><span class="sxs-lookup"><span data-stu-id="031e0-178">UberCloud</span></span>](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a><span data-ttu-id="031e0-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="031e0-179">Next steps</span></span>
* <span data-ttu-id="031e0-180">에 대 한 hello 최신 알림을 참조 hello [Microsoft HPC 및 일괄 처리 팀 블로그](http://blogs.technet.com/b/windowshpc/) 및 hello [Azure 블로그](https://azure.microsoft.com/blog/tag/hpc/)합니다.</span><span class="sxs-lookup"><span data-stu-id="031e0-180">For hello latest announcements, see hello [Microsoft HPC and Batch team blog](http://blogs.technet.com/b/windowshpc/) and hello [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).</span></span>
* <span data-ttu-id="031e0-181">또한 참조 [일괄 처리의 새로운 기능](https://azure.microsoft.com/updates/?service=batch) toohello 구독 또는 [RSS 피드](https://azure.microsoft.com/updates/feed/?service=batch)합니다.</span><span class="sxs-lookup"><span data-stu-id="031e0-181">Also see [what's new in Batch](https://azure.microsoft.com/updates/?service=batch) or subscribe toohello [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).</span></span>

