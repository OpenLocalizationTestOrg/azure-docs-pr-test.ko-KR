---
title: "Linux RDMA 클러스터 toorun MPI 응용 프로그램을 aaaSet | Microsoft Docs"
description: "Hello Azure RDMA 네트워크 toorun MPI 응용 프로그램의 크기 H16r, H16mr, A8 또는 A9 Vm toouse Linux 클러스터 만들기"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a><span data-ttu-id="fd086-103">Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="fd086-103">Set up a Linux RDMA cluster toorun MPI applications</span></span>
<span data-ttu-id="fd086-104">Tooset Linux RDMA를 사용 하 여 Azure에 클러스터 되는 방법을 알아보려면 [VM 크기를 계산 하는 고성능](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun 병렬 인터페이스 MPI (Message Passing) 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-104">Learn how tooset up a Linux RDMA cluster in Azure with [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun parallel Message Passing Interface (MPI) applications.</span></span> <span data-ttu-id="fd086-105">이 문서의 단계 tooprepare Linux HPC 이미지 toorun Intel MPI 클러스터에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-105">This article provides steps tooprepare a Linux HPC image toorun Intel MPI on a cluster.</span></span> <span data-ttu-id="fd086-106">준비, 후이 이미지와 hello RDMA 가능 Azure VM 크기 (현재 H16r, H16mr, A8 또는 A9) 중 하나를 사용 하 여 Vm의 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-106">After preparation, you deploy a cluster of VMs using this image and one of hello RDMA-capable Azure VM sizes (currently H16r, H16mr, A8, or A9).</span></span> <span data-ttu-id="fd086-107">Hello 클러스터 toorun MPI 응용 프로그램 원격 직접 메모리 액세스 (RDMA) 기술을 기반으로 하는 낮은 대기 시간, 처리량이 높은 네트워크를 통해 효율적으로 통신 하는 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-107">Use hello cluster toorun MPI applications that communicate efficiently over a low-latency, high-throughput network based on remote direct memory access (RDMA) technology.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd086-108">Azure에는 리소스를 만들고 사용하기 위한 별도의 두 가지 배포 모델, 즉 [Azure Resource Manager](../../../resource-manager-deployment-model.md)와 클래식 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-108">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="fd086-109">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="fd086-110">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

## <a name="cluster-deployment-options"></a><span data-ttu-id="fd086-111">클러스터 배포 옵션</span><span class="sxs-lookup"><span data-stu-id="fd086-111">Cluster deployment options</span></span>
<span data-ttu-id="fd086-112">다음은 방법을 작업 스케줄러 유무 toocreate RDMA Linux 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-112">Following are methods you can use toocreate a Linux RDMA cluster with or without a job scheduler.</span></span>

* <span data-ttu-id="fd086-113">**Azure CLI 스크립트**: hello를 사용 하 여이 문서의 뒷부분에 나와 있는 것 처럼 [Azure 명령줄 인터페이스](../../../cli-install-nodejs.md) (CLI) tooscript hello RDMA 가능 Vm의 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-113">**Azure CLI scripts**: As shown later in this article, use hello [Azure command-line interface](../../../cli-install-nodejs.md) (CLI) tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span> <span data-ttu-id="fd086-114">서비스 관리 모드에서 CLI hello를 만들므로 hello 클러스터 노드에 순차적으로 hello 클래식 배포 모델에 많은 계산 노드를 배포 하면 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-114">hello CLI in Service Management mode creates hello cluster nodes serially in hello classic deployment model, so deploying many compute nodes might take several minutes.</span></span> <span data-ttu-id="fd086-115">tooenable hello hello 클래식 배포 모델을 사용 하는 경우 RDMA 네트워크 연결 hello Vm 배포 hello에서 동일한 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-115">tooenable hello RDMA network connection when you use hello classic deployment model, deploy hello VMs in hello same cloud service.</span></span>
* <span data-ttu-id="fd086-116">**Azure 리소스 관리자 템플릿**: hello 리소스 관리자 배포 모델 toodeploy toohello RDMA 네트워크 연결 하는 RDMA 가능 Vm의 클러스터를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-116">**Azure Resource Manager templates**: You can also use hello Resource Manager deployment model toodeploy a cluster of RDMA-capable VMs that connects toohello RDMA network.</span></span> <span data-ttu-id="fd086-117">할 수 있습니다 [사용자 고유의 템플릿을 만들](../../../resource-group-authoring-templates.md), hello 확인 또는 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/) 가 Microsoft 소프트웨어 또는 hello 커뮤니티 toodeploy hello 추가할 솔루션을 제공 하는 서식 파일에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-117">You can [create your own template](../../../resource-group-authoring-templates.md), or check hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/) for templates contributed by Microsoft or hello community toodeploy hello solution you want.</span></span> <span data-ttu-id="fd086-118">리소스 관리자 템플릿을 신속 하 고 안정적인 방식으로 toodeploy Linux 클러스터를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-118">Resource Manager templates can provide a fast and reliable way toodeploy a Linux cluster.</span></span> <span data-ttu-id="fd086-119">hello에 hello Vm을 배포 하는 tooenable hello RDMA 네트워크 연결 hello 리소스 관리자 배포 모델을 사용 하는 경우 동일한 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-119">tooenable hello RDMA network connection when you use hello Resource Manager deployment model, deploy hello VMs in hello same availability set.</span></span>
* <span data-ttu-id="fd086-120">**HPC Pack**: Azure에 Microsoft HPC Pack 클러스터를 만들고 지원 되는 Linux 배포 tooaccess hello RDMA 네트워크를 실행 하는 RDMA 가능 계산 노드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-120">**HPC Pack**: Create a Microsoft HPC Pack cluster in Azure and add RDMA-capable compute nodes that run a supported Linux distribution tooaccess hello RDMA network.</span></span> <span data-ttu-id="fd086-121">자세한 내용은 [Azure에서 HPC Pack 클러스터의 Linux 계산 노드 시작](hpcpack-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fd086-121">For more information, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="sample-deployment-steps-in-hello-classic-model"></a><span data-ttu-id="fd086-122">Hello 클래식 모델에 샘플 배포 단계</span><span class="sxs-lookup"><span data-stu-id="fd086-122">Sample deployment steps in hello classic model</span></span>
<span data-ttu-id="fd086-123">hello 다음 단계 어떻게 toouse hello Azure CLI toodeploy hello Azure Marketplace에서에서 SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM 사용자 지정 및 표시 사용자 지정 VM 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-123">hello following steps show how toouse hello Azure CLI toodeploy a SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM from hello Azure Marketplace, customize it, and create a custom VM image.</span></span> <span data-ttu-id="fd086-124">RDMA 가능 Vm의 클러스터의 hello 이미지 tooscript hello 배포를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-124">Then you can use hello image tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span>

> [!TIP]
> <span data-ttu-id="fd086-125">유사한 단계 toodeploy hello Azure Marketplace에서에서 HPC CentOS 기반 이미지를 기반으로 RDMA 가능 Vm의 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-125">Use similar steps toodeploy a cluster of RDMA-capable VMs based on CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="fd086-126">일부 단계가 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-126">Some steps differ slightly, as noted.</span></span> 
>
>

### <a name="prerequisites"></a><span data-ttu-id="fd086-127">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fd086-127">Prerequisites</span></span>
* <span data-ttu-id="fd086-128">**클라이언트 컴퓨터**: Azure와 Mac, Linux 또는 Windows 클라이언트 컴퓨터 toocommunicate 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-128">**Client computer**: You need a Mac, Linux, or Windows client computer toocommunicate with Azure.</span></span> <span data-ttu-id="fd086-129">이러한 단계는 Linux 클라이언트를 사용하는 것을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-129">These steps assume you are using a Linux client.</span></span>
* <span data-ttu-id="fd086-130">**Azure 구독** - 구독이 없는 경우 몇 분 내에 [무료 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-130">**Azure subscription**: If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span> <span data-ttu-id="fd086-131">대규모 클러스터의 경우, 종량제 구독이나 다른 구매 옵션을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="fd086-131">For larger clusters, consider a pay-as-you-go subscription or other purchase options.</span></span>
* <span data-ttu-id="fd086-132">**VM 크기 가용성**: 인스턴스 크기를 다음 hello는 RDMA 가능: H16r, H16mr, A8 및 A9 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-132">**VM size availability**: hello following instance sizes are RDMA capable: H16r, H16mr, A8, and A9.</span></span> <span data-ttu-id="fd086-133">[지역별 사용 가능한 제품](https://azure.microsoft.com/regions/services/) 에서 Azure 지역의 가용성을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="fd086-133">Check [Products available by region](https://azure.microsoft.com/regions/services/) for availability in Azure regions.</span></span>
* <span data-ttu-id="fd086-134">**코어 할당량**: tooincrease hello 할당량의 코어 toodeploy 계산 집약적인 Vm의 클러스터 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-134">**Cores quota**: You might need tooincrease hello quota of cores toodeploy a cluster of compute-intensive VMs.</span></span> <span data-ttu-id="fd086-135">예를 들어 8 toodeploy A9 Vm이이 문서에 나와 있는 것 처럼 원하는 최소한 128 코어가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-135">For example, you need at least 128 cores if you want toodeploy 8 A9 VMs as shown in this article.</span></span> <span data-ttu-id="fd086-136">구독은 hello hello H 시리즈를 포함 하 여 특정 VM 크기 제품군에서 배포할 수 있는 코어 수가 제한도 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-136">Your subscription might also limit hello number of cores you can deploy in certain VM size families, including hello H-series.</span></span> <span data-ttu-id="fd086-137">toorequest 할당량 증가 [온라인 고객 지원 요청을 개시](../../../azure-supportability/how-to-create-azure-support-request.md) 비용 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-137">toorequest a quota increase, [open an online customer support request](../../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
* <span data-ttu-id="fd086-138">**Azure CLI**: [설치](../../../cli-install-nodejs.md) hello Azure CLI 및 [tooyour Azure 구독 연결](../../../xplat-cli-connect.md) hello 클라이언트 컴퓨터에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-138">**Azure CLI**: [Install](../../../cli-install-nodejs.md) hello Azure CLI and [connect tooyour Azure subscription](../../../xplat-cli-connect.md) from hello client computer.</span></span>

### <a name="provision-an-sles-12-sp1-hpc-vm"></a><span data-ttu-id="fd086-139">SLES 12 SP1 HPC VM 프로비전</span><span class="sxs-lookup"><span data-stu-id="fd086-139">Provision an SLES 12 SP1 HPC VM</span></span>
<span data-ttu-id="fd086-140">TooAzure hello Azure CLI로 로그인 한 후 실행 `azure config list` 출력 hello tooconfirm 서비스 관리 모드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-140">After signing in tooAzure with hello Azure CLI, run `azure config list` tooconfirm that hello output shows Service Management mode.</span></span> <span data-ttu-id="fd086-141">그렇지 않은 경우이 명령을 실행 하 여 hello 모드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-141">If it does not, set hello mode by running this command:</span></span>

    azure config mode asm


<span data-ttu-id="fd086-142">모든 hello 구독 권한이 부여 된 toouse는 hello toolist 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-142">Type hello following toolist all hello subscriptions you are authorized toouse:</span></span>

    azure account list

<span data-ttu-id="fd086-143">hello 현재 활성 구독으로 식별 되는지를 `Current` 도`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-143">hello current active subscription is identified with `Current` set too`true`.</span></span> <span data-ttu-id="fd086-144">이 구독 hello 없으면 하나 원하는 toouse toocreate hello 클러스터를 hello 활성 구독으로 hello 적절 한 구독 ID를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-144">If this subscription isn't hello one you want toouse toocreate hello cluster, set hello appropriate subscription ID as hello active subscription:</span></span>

    azure account set <subscription-Id>

<span data-ttu-id="fd086-145">toosee hello Azure, hello 따르면 같은 명령을 실행할 셸 환경 지원 가정의 공개적으로 사용할 수 SLES 12 SP1 HPC 이미지 **grep**:</span><span class="sxs-lookup"><span data-stu-id="fd086-145">toosee hello publicly available SLES 12 SP1 HPC images in Azure, run a command like hello following, assuming your shell environment supports **grep**:</span></span>

    azure vm image list | grep "suse.*hpc"

<span data-ttu-id="fd086-146">Hello 다음과 같은 명령을 실행 하 여 SLES 12 SP1 HPC 이미지를 사용 하는 RDMA 가능 VM을 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-146">Provision an RDMA-capable VM with a SLES 12 SP1 HPC image by running a command like hello following:</span></span>

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

<span data-ttu-id="fd086-147">여기서,</span><span class="sxs-lookup"><span data-stu-id="fd086-147">Where:</span></span>

* <span data-ttu-id="fd086-148">hello 크기 (이 예제의 A9) hello RDMA 가능 VM 크기 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-148">hello size (A9 in this example) is one of hello RDMA-capable VM sizes.</span></span>
* <span data-ttu-id="fd086-149">hello 외부 SSH 포트 번호 (이 예제는 hello SSH 기본 22)에 모든 유효한 포트 번호가입니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-149">hello external SSH port number (22 in this example, which is hello SSH default) is any valid port number.</span></span> <span data-ttu-id="fd086-150">SSH 포트 번호를 내부 hello too22를 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-150">hello internal SSH port number is set too22.</span></span>
* <span data-ttu-id="fd086-151">새 클라우드 서비스는 hello 위치에 따라 지정 된 Azure 영역이 hello에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-151">A new cloud service is created in hello Azure region specified by hello location.</span></span> <span data-ttu-id="fd086-152">선택한 크기는 사용할 수 있는 hello VM의에서 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-152">Specify a location in which hello VM size you choose is available.</span></span>
* <span data-ttu-id="fd086-153">(발생 하는 추가 요금이) SUSE 우선 순위 지원에 대 한 hello SLES 12 SP1 이미지 이름을 현재 될 수 있습니다 이러한 두 옵션 중 하나:</span><span class="sxs-lookup"><span data-stu-id="fd086-153">For SUSE priority support (which incurs additional charges), hello SLES 12 SP1 image name currently can be one of these two options:</span></span> 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a><span data-ttu-id="fd086-154">Hello VM 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="fd086-154">Customize hello VM</span></span>
<span data-ttu-id="fd086-155">Hello VM 프로 비전 완료 된 후 사용 하 여 SSH toohello VM VM의 외부 IP 주소 (또는 DNS 이름) hello 및 hello 외부 포트 번호를 구성 하 고 사용자 지정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fd086-155">After hello VM finishes provisioning, SSH toohello VM by using hello VM's external IP address (or DNS name) and hello external port number you configured, and then customize it.</span></span> <span data-ttu-id="fd086-156">연결 세부 정보를 참조 하십시오. [어떻게 Linux를 실행 하는 tooa 가상 컴퓨터에서 toolog](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-156">For connection details, see [How toolog on tooa virtual machine running Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="fd086-157">루트 액세스가 필요한 toocomplete 단계 경우가 아니면 VM hello에 구성 된 hello 사용자로 명령을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-157">Perform commands as hello user you configured on hello VM, unless root access is required toocomplete a step.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd086-158">Microsoft Azure 루트 액세스 tooLinux Vm 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-158">Microsoft Azure does not provide root access tooLinux VMs.</span></span> <span data-ttu-id="fd086-159">toogain 관리 액세스를 사용 하 여 명령을 실행 하는 사용자 toohello VM으로 연결 된 경우 `sudo`합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-159">toogain administrative access when connected as a user toohello VM, run commands by using `sudo`.</span></span>
>
>

* <span data-ttu-id="fd086-160">**업데이트** - zypper를 사용하여 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-160">**Updates**: Install updates by using zypper.</span></span> <span data-ttu-id="fd086-161">Tooinstall NFS 유틸리티 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-161">You might also want tooinstall NFS utilities.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="fd086-162">SLES 12 SP1 HPC VM에서 문제가 발생할 수 있습니다 hello Linux RDMA 드라이버는 커널 업데이트를 적용 하지 않으면 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-162">In a SLES 12 SP1 HPC VM, we recommend that you don't apply kernel updates, which can cause issues with hello Linux RDMA drivers.</span></span>
  >
  >
* <span data-ttu-id="fd086-163">**인텔 MPI**: hello 다음 명령을 실행 하 여 hello SLES 12 SP1 HPC VM에 Intel MPI hello 설치를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-163">**Intel MPI**: Complete hello installation of Intel MPI on hello SLES 12 SP1 HPC VM by running hello following command:</span></span>

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* <span data-ttu-id="fd086-164">**메모리를 잠글**: MPI 코드 toolock hello에 사용 가능한 메모리 RDMA, 추가 또는 hello 다음 hello /etc/security/limits.conf 파일의 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-164">**Lock memory**: For MPI codes toolock hello memory available for RDMA, add or change hello following settings in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="fd086-165">루트 액세스 tooedit이이 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-165">You need root access tooedit this file.</span></span>

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > <span data-ttu-id="fd086-166">테스트를 위해 memlock toounlimited를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-166">For testing purposes, you can also set memlock toounlimited.</span></span> <span data-ttu-id="fd086-167">예: `<User or group name>    hard    memlock unlimited`</span><span class="sxs-lookup"><span data-stu-id="fd086-167">For example: `<User or group name>    hard    memlock unlimited`.</span></span> <span data-ttu-id="fd086-168">자세한 내용은 [가장 잘 알려진 잠금 메모리 크기 설정 방법](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fd086-168">For more information, see [Best known methods for setting locked memory size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span></span>
  >
  >
* <span data-ttu-id="fd086-169">**SLES Vm에 대 한 SSH 키**: MPI 작업을 실행할 때 생성 SSH 키 tooestablish 신뢰 hello 간에 사용자 계정에 대 한 hello SLES 클러스터의 노드를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-169">**SSH keys for SLES VMs**: Generate SSH keys tooestablish trust for your user account among hello compute nodes in hello SLES cluster when running MPI jobs.</span></span> <span data-ttu-id="fd086-170">CentOS 기반 HPC VM을 배포한 경우 이 단계를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-170">If you deployed a CentOS-based HPC VM, don't follow this step.</span></span> <span data-ttu-id="fd086-171">Hello 이미지를 캡처할 hello 클러스터를 배포한 후이 문서 tooset hello 클러스터 노드 간에 passwordless SSH 트러스트를의 뒷부분에 나오는 지침을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fd086-171">See instructions later in this article tooset up passwordless SSH trust among hello cluster nodes after you capture hello image and deploy hello cluster.</span></span>

    <span data-ttu-id="fd086-172">toocreate SSH 키를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-172">toocreate SSH keys, run hello following command.</span></span> <span data-ttu-id="fd086-173">입력에 대 한 메시지가 나타나면 선택 **Enter** toogenerate hello 키 암호를 설정 하지 않고 hello 기본 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-173">When you are prompted for input, select **Enter** toogenerate hello keys in hello default location without setting a password.</span></span>

        ssh-keygen

    <span data-ttu-id="fd086-174">알려진된 공개 키에 대 한 hello 공개 키 toohello authorized_keys 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-174">Append hello public key toohello authorized_keys file for known public keys.</span></span>

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    <span data-ttu-id="fd086-175">Hello ~/.ssh 디렉터리에서 편집 하거나 hello 구성 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-175">In hello ~/.ssh directory, edit or create hello config file.</span></span> <span data-ttu-id="fd086-176">(이 예제의 10.32.0.0/16) Azure에서 toouse 계획 hello 개인 네트워크의 hello IP 주소 범위를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-176">Provide hello IP address range of hello private network that you plan toouse in Azure (10.32.0.0/16 in this example):</span></span>

        host 10.32.0.*
        StrictHostKeyChecking no

    <span data-ttu-id="fd086-177">또는 다음과 같은 클러스터의 각 VM의 hello 개인 네트워크 IP 주소를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-177">Alternatively, list hello private network IP address of each VM in your cluster as follows:</span></span>

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > <span data-ttu-id="fd086-178">`StrictHostKeyChecking no`를 구성하면 특정 IP 주소 또는 범위를 지정하지 않은 경우 잠재적인 보안 위험이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-178">Configuring `StrictHostKeyChecking no` can create a potential security risk when a specific IP address or range is not specified.</span></span>
  >
  >
* <span data-ttu-id="fd086-179">**응용 프로그램**: hello 이미지를 포착 하기 전에 다른 사용자 지정을 수행 하거나 필요한 응용 프로그램을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-179">**Applications**: Install any applications you need or perform other customizations before you capture hello image.</span></span>

### <a name="capture-hello-image"></a><span data-ttu-id="fd086-180">Hello 이미지 캡처</span><span class="sxs-lookup"><span data-stu-id="fd086-180">Capture hello image</span></span>
<span data-ttu-id="fd086-181">먼저 hello hello Linux VM에서 다음 명령을 실행 하 여 toocapture hello 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-181">toocapture hello image, first run hello following command on hello Linux VM.</span></span> <span data-ttu-id="fd086-182">이 명령은 VM hello deprovisions 하지만 사용자 계정 및 SSH 키를 설정 하는 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-182">This command deprovisions hello VM but maintains user accounts and SSH keys that you set up.</span></span>

```
sudo waagent -deprovision
```

<span data-ttu-id="fd086-183">클라이언트 컴퓨터에서 다음 Azure CLI 명령을 toocapture hello 이미지 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-183">From your client computer, run hello following Azure CLI commands toocapture hello image.</span></span> <span data-ttu-id="fd086-184">자세한 내용은 참조 [어떻게 toocapture 클래식 Linux 가상 컴퓨터를 이미지로](capture-image.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-184">For more information, see [How toocapture a classic Linux virtual machine as an image](capture-image.md).</span></span>  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

<span data-ttu-id="fd086-185">이러한 명령을 실행 한 후 사용에 대 한 hello VM 이미지가 캡처된 및 hello VM 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-185">After you run these commands, hello VM image is captured for your use and hello VM is deleted.</span></span> <span data-ttu-id="fd086-186">이제 사용자 지정 이미지 준비 toodeploy 클러스터가 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-186">Now you have your custom image ready toodeploy a cluster.</span></span>

### <a name="deploy-a-cluster-with-hello-image"></a><span data-ttu-id="fd086-187">Hello 이미지를 사용 하 여 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="fd086-187">Deploy a cluster with hello image</span></span>
<span data-ttu-id="fd086-188">사용자 환경에 대 한 적절 한 값으로 Bash 스크립트를 다음 hello를 수정 하 고 클라이언트 컴퓨터에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-188">Modify hello following Bash script with appropriate values for your environment and run it from your client computer.</span></span> <span data-ttu-id="fd086-189">Azure hello 클래식 배포 모델에서 연속으로 hello Vm을 배포 하기 때문에 toodeploy hello 8 개의 A9 Vm이이 스크립트에서 제안 하는 몇 분 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-189">Because Azure deploys hello VMs serially in hello classic deployment model, it takes a few minutes toodeploy hello eight A9 VMs suggested in this script.</span></span>

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a><span data-ttu-id="fd086-190">CentOS HPC 클러스터에 대한 고려 사항</span><span class="sxs-lookup"><span data-stu-id="fd086-190">Considerations for a CentOS HPC cluster</span></span>
<span data-ttu-id="fd086-191">Tooset HPC에 대 한 hello SLES 12가 아닌 Azure Marketplace의에서 hello CentOS 기반 HPC 이미지 중 하나에 따라 클러스터를 hello hello 섹션 앞의 일반 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fd086-191">If you want tooset up a cluster based on one of hello CentOS-based HPC images in hello Azure Marketplace instead of SLES 12 for HPC, follow hello general steps in hello preceding section.</span></span> <span data-ttu-id="fd086-192">참고 hello를 프로 비전 하 고 hello VM 구성 시 차이점을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-192">Note hello following differences when you provision and configure hello VM:</span></span>

- <span data-ttu-id="fd086-193">Intel MPI가 CentOS 기반 HPC 이미지에서 프로비전된 VM에 이미 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-193">Intel MPI is already installed on a VM provisioned from a CentOS-based HPC image.</span></span>
- <span data-ttu-id="fd086-194">잠금 메모리 설정이 hello VM /etc/security/limits.conf 파일에 이미 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-194">Lock memory settings are already added in hello VM's /etc/security/limits.conf file.</span></span>
- <span data-ttu-id="fd086-195">캡처에 대 한 hello 프로 비전 하는 VM에 SSH 키를 생성 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-195">Do not generate SSH keys on hello VM you provision for capture.</span></span> <span data-ttu-id="fd086-196">대신, hello 클러스터를 배포한 후 사용자 기반 인증 설정이 끝났습니다 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-196">Instead, we recommend setting up user-based authentication after you deploy hello cluster.</span></span> <span data-ttu-id="fd086-197">자세한 내용은 다음 단원을 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="fd086-197">For more information, see hello following section.</span></span>  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a><span data-ttu-id="fd086-198">Hello 클러스터에서 passwordless SSH 트러스트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-198">Set up passwordless SSH trust on hello cluster</span></span>
<span data-ttu-id="fd086-199">CentOS 기반 HPC 클러스터에는 hello 계산 노드 간에 트러스트를 설정 하기 위한 두 가지 방법: 호스트 기반 인증 및 사용자 기반 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-199">On a CentOS-based HPC cluster, there are two methods for establishing trust between hello compute nodes: host-based authentication and user-based authentication.</span></span> <span data-ttu-id="fd086-200">호스트 기반 인증이이 문서의 hello 범위 외부에서 이며 일반적으로 중에 수행 해야 확장 스크립트를 통해 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-200">Host-based authentication is outside of hello scope of this article and generally must be done through an extension script during deployment.</span></span> <span data-ttu-id="fd086-201">사용자 기반 인증 배포 후 신뢰를 설정 하는 데 편리 고 hello 세대 가상 컴퓨터와 공유 hello 간에 SSH 키의 계산 hello 클러스터 노드에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-201">User-based authentication is convenient for establishing trust after deployment and requires hello generation and sharing of SSH keys among hello compute nodes in hello cluster.</span></span> <span data-ttu-id="fd086-202">이 메서드는 일반적으로 암호 없는 SSH 로그인이라고 알려졌으며 MPI 작업을 실행하는 경우에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-202">This method is commonly known as passwordless SSH login and is required when running MPI jobs.</span></span>

<span data-ttu-id="fd086-203">Hello 커뮤니티에서 제공 하는 샘플 스크립트는에서 사용할 수 있는 [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) CentOS 기반 HPC 클러스터에 tooenable 쉬운 사용자 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-203">A sample script contributed from hello community is available on [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable easy user authentication on a CentOS-based HPC cluster.</span></span> <span data-ttu-id="fd086-204">다운로드 하 여 단계를 수행 하는 hello를 사용 하 여이 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-204">Download and use this script by using hello following steps.</span></span> <span data-ttu-id="fd086-205">이 스크립트를 수정 하거나 기타 메서드 tooestablish passwordless SSH 인증 hello 클러스터 계산 노드 사이 사용 하 여 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-205">You can also modify this script or use any other method tooestablish passwordless SSH authentication between hello cluster compute nodes.</span></span>

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

<span data-ttu-id="fd086-206">toorun hello 스크립트 해야 tooknow hello 접두사 서브넷 IP 주소에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-206">toorun hello script, you need tooknow hello prefix for your subnet IP addresses.</span></span> <span data-ttu-id="fd086-207">Hello hello 클러스터 노드 중 하나에서 다음 명령을 실행 하 여 hello 접두사를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-207">Get hello prefix by running hello following command on one of hello cluster nodes.</span></span> <span data-ttu-id="fd086-208">출력은 비슷해야 10.1.3.5, 및 hello 접두사는 hello 10.1.3 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-208">Your output should look something like 10.1.3.5, and hello prefix is hello 10.1.3 portion.</span></span>

    ifconfig eth0 | grep -w inet | awk '{print $2}'

<span data-ttu-id="fd086-209">이제 세 개의 매개 변수를 사용 하 여 hello 스크립트 실행: hello hello 일반 사용자 이름이 계산 노드, hello 공통 암호 hello에서 해당 사용자의 계산 노드 및 hello 서브넷 접두사는에서 반환 된 hello 이전 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-209">Now run hello script using three parameters: hello common user name on hello compute nodes, hello common password for that user on hello compute nodes, and hello subnet prefix that was returned from hello previous command.</span></span>

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

<span data-ttu-id="fd086-210">이 스크립트는 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="fd086-210">This script does hello following:</span></span>

* <span data-ttu-id="fd086-211">Hello 호스트 노드 passwordless 로그인에 대 한 필요한.ssh, 라는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-211">Creates a directory on hello host node named .ssh, which is required for passwordless login.</span></span>
* <span data-ttu-id="fd086-212">Hello 클러스터의 모든 노드에서 passwordless 로그인 tooallow 로그인을 지정 하는 hello.ssh 디렉터리에 구성 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-212">Creates a configuration file in hello .ssh directory that instructs passwordless login tooallow login from any node in hello cluster.</span></span>
* <span data-ttu-id="fd086-213">Hello 노드 이름 및 hello 클러스터의 모든 hello 노드에 대 한 노드 IP 주소를 포함 하는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-213">Creates files containing hello node names and node IP addresses for all hello nodes in hello cluster.</span></span> <span data-ttu-id="fd086-214">이러한 파일은 나중에 참조할 hello 스크립트를 실행 한 후 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-214">These files are left after hello script is run for later reference.</span></span>
* <span data-ttu-id="fd086-215">(포함 hello 호스트 노드) 각 클러스터 노드에 대 한 개인 및 공개 키 쌍을 만들고 hello authorized_keys 파일에 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-215">Creates a private and public key pair for each cluster node (including hello host node) and creates entries in hello authorized_keys file.</span></span>

> [!WARNING]
> <span data-ttu-id="fd086-216">이 스크립트를 실행하면 잠재적인 보안 위협이 생길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-216">Running this script can create a potential security risk.</span></span> <span data-ttu-id="fd086-217">Hello 공개 키 정보 ~/.ssh에 배포 되지 않는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-217">Ensure that hello public key information in ~/.ssh is not distributed.</span></span>
>
>

## <a name="configure-intel-mpi"></a><span data-ttu-id="fd086-218">Intel MPI 구성</span><span class="sxs-lookup"><span data-stu-id="fd086-218">Configure Intel MPI</span></span>
<span data-ttu-id="fd086-219">tooconfigure 해야 Azure Linux RDMA에 toorun MPI 응용 프로그램, 특정 환경 변수 특정 tooIntel MPI 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-219">toorun MPI applications on Azure Linux RDMA, you need tooconfigure certain environment variables specific tooIntel MPI.</span></span> <span data-ttu-id="fd086-220">여기서는 샘플 Bash 스크립트 tooconfigure hello 필요한 변수 toorun 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-220">Here is a sample Bash script tooconfigure hello variables needed toorun an application.</span></span> <span data-ttu-id="fd086-221">Intel MPI의 설치에 필요한 hello 경로 toompivars.sh를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-221">Change hello path toompivars.sh as needed for your installation of Intel MPI.</span></span>

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

<span data-ttu-id="fd086-222">hello hello 호스트 파일의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-222">hello format of hello host file is as follows.</span></span> <span data-ttu-id="fd086-223">클러스터의 각 노드에 대해 한 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-223">Add one line for each node in your cluster.</span></span> <span data-ttu-id="fd086-224">Hello 가상 네트워크에서 개인 IP 주소 정의 DNS 이름이 아니라 이전에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-224">Specify private IP addresses from hello virtual network defined earlier, not DNS names.</span></span> <span data-ttu-id="fd086-225">예를 들어 hello 파일 10.32.0.1 및 10.32.0.2 IP 주소를 가진 두 명의 호스트에 대 한 hello 다음이 포함:</span><span class="sxs-lookup"><span data-stu-id="fd086-225">For example, for two hosts with IP addresses 10.32.0.1 and 10.32.0.2, hello file contains hello following:</span></span>

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a><span data-ttu-id="fd086-226">기본 2 노드 클러스터에서 MPI 실행</span><span class="sxs-lookup"><span data-stu-id="fd086-226">Run MPI on a basic two-node cluster</span></span>
<span data-ttu-id="fd086-227">아직 이미 하지 않은 경우 먼저 hello 환경을 설정 Intel MPI에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-227">If you haven't already done so, first set up hello environment for Intel MPI.</span></span>

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a><span data-ttu-id="fd086-228">MPI 명령 실행</span><span class="sxs-lookup"><span data-stu-id="fd086-228">Run an MPI command</span></span>
<span data-ttu-id="fd086-229">두 개 이상의 계산 노드 간 MPI 제대로 설치 되어 있고 통신할 수 있는 hello 계산 노드 tooshow 중 하나에서 MPI 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-229">Run an MPI command on one of hello compute nodes tooshow that MPI is installed properly and can communicate between at least two compute nodes.</span></span> <span data-ttu-id="fd086-230">hello 다음 **mpirun** 명령은 실행 hello **호스트 이름** 명령에서 두 개의 노드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-230">hello following **mpirun** command runs hello **hostname** command on two nodes.</span></span>

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
<span data-ttu-id="fd086-231">출력에 대 한 입력으로 전달 하는 모든 hello 노드의 hello 이름을 나열 해야 `-hosts`합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-231">Your output should list hello names of all hello nodes that you passed as input for `-hosts`.</span></span> <span data-ttu-id="fd086-232">예를 들어 한 **mpirun** 두 노드를 사용 하 여 명령을 hello 다음과 같은 출력을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-232">For example, an **mpirun** command with two nodes returns output like hello following:</span></span>

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a><span data-ttu-id="fd086-233">MPI 벤치마크 실행</span><span class="sxs-lookup"><span data-stu-id="fd086-233">Run an MPI benchmark</span></span>
<span data-ttu-id="fd086-234">다음 Intel MPI 명령을 hello pingpong 벤치 마크 tooverify hello 클러스터 구성 및 연결 toohello RDMA 네트워크를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-234">hello following Intel MPI command runs a pingpong benchmark tooverify hello cluster configuration and connection toohello RDMA network.</span></span>

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

<span data-ttu-id="fd086-235">두 개의 노드가 있는 클러스터 작업에서 hello 다음과 같은 출력이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-235">On a working cluster with two nodes, you should see output like hello following.</span></span> <span data-ttu-id="fd086-236">Hello Azure RDMA 네트워크 too512 바이트를 메시지 크기에 대 한 3 마이크로초 이하로 대기 시간을 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-236">On hello Azure RDMA network, expect latency at or below 3 microseconds for message sizes up too512 bytes.</span></span>

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a><span data-ttu-id="fd086-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fd086-237">Next steps</span></span>
* <span data-ttu-id="fd086-238">Linux 클러스터에 Linux MPI 응용 프로그램을 배포하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-238">Deploy and run your Linux MPI applications on your Linux cluster.</span></span>
* <span data-ttu-id="fd086-239">Hello 참조 [Intel MPI 라이브러리 설명서](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) Intel MPI에 대 한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-239">See hello [Intel MPI Library documentation](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) for guidance on Intel MPI.</span></span>
* <span data-ttu-id="fd086-240">시도 [퀵 스타트 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate Intel Lustre HPC CentOS 기반 이미지를 사용 하 여 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="fd086-240">Try a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate an Intel Lustre cluster by using a CentOS-based HPC image.</span></span> <span data-ttu-id="fd086-241">자세한 내용은 [Microsoft Azure에서 Intel Cloud Edition for Lustre 배포](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fd086-241">For details, see [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span></span>
