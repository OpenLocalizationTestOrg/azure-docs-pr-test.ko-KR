---
title: "Linux VM에서 HPC 팩으로 OpenFOAM 실행 | Microsoft Docs"
description: "Azure에서 Microsoft HPC Pack 클러스터를 배포하고 RDMA 네트워크 간의 여러 Linux 계산 노드에서 OpenFOAM 작업을 실행합니다."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: ef124a8983fa112d499252460bff9ed2fcccc02b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="b535e-103">Azure의 Linux RDMA 클러스터에서 Microsoft HPC 팩을 사용하여 OpenFoam 실행</span><span class="sxs-lookup"><span data-stu-id="b535e-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="b535e-104">이 문서에서는 Azure 가상 컴퓨터에서 OpenFoam을 실행하는 한 가지 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-104">This article shows you one way to run OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="b535e-105">여기서는 Azure에서 Linux 계산 노드를 사용하여 Microsoft HPC Pack 클러스터를 배포하고 Intel MPI를 사용하여 [OpenFoam](http://openfoam.com/) 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="b535e-106">계산 노드에 RDMA 지원 Azure VM을 사용할 수 있으므로 계산 노드는 Azure RDMA 네트워크를 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-106">You can use RDMA-capable Azure VMs for the compute nodes, so that the compute nodes communicate over the Azure RDMA network.</span></span> <span data-ttu-id="b535e-107">Azure에서 OpenFoam을 실행하는 다른 옵션으로는 마켓플레이스에서 제공되는 완전히 구성된 상용 이미지(예: UberCloud에서 제공하는 [CentOS 6의 OpenFoam 2.3](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)) 및 [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/)에서 실행되는 이미지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-107">Other options to run OpenFoam in Azure include fully configured commercial images available in the Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="b535e-108">OpenFOAM(오픈 필드 작업 및 조작에 대한)은 상업용 및 연구용 조직의 공학 및 과학에서 널리 사용되는 오픈 소스 CFD(컴퓨팅 유체 역학) 소프트웨어 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="b535e-109">Meshing, 특히 snappyHexMesh, 복잡한 CAD 기하학 및 전처리 및 후처리에 대한 병렬화된 메셔에 대한 도구를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="b535e-110">거의 모든 프로세스는 마음껏 컴퓨터 하드웨어를 모두 활용하도록 병렬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-110">Almost all processes run in parallel, enabling users to take full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="b535e-111">Microsoft HPC 팩에서는 MPI 응용 프로그램을 포함하는 대규모 HPC 및 병렬 응용 프로그램을 Microsoft Azure 가상 컴퓨터의 클러스터에서 실행하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-111">Microsoft HPC Pack provides features to run large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="b535e-112">HPC 팩은 HPC 팩 클러스터에 배포된 Linux 계산 노드 VM에서 Linux HPC 응용 프로그램의 실행도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="b535e-113">HPC 팩으로 Linux 계산 노드 사용에 대한 소개는 [Azure에서 HPC 팩 클러스터의 Linux 계산 노드 시작](hpcpack-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b535e-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction to using Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="b535e-114">이 문서에서는 HPC Pack을 사용하여 Linux MPI 워크로드를 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-114">This article illustrates how to run a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="b535e-115">또한 여기서는 Linux 시스템 관리 및 Linux 클러스터에서 실행 중인 MPI 작업에 대해 잘 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="b535e-116">이 문서에 표시된 것과 다른 MPI 및 OpenFOAM 버전을 사용하는 경우 일부 설치 및 구성 단계를 수정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-116">If you use versions of MPI and OpenFOAM different from the ones shown in this article, you might have to modify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b535e-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b535e-117">Prerequisites</span></span>
* <span data-ttu-id="b535e-118">**RDMA 지원 Linux 계산 노드가 포함된 HPC 팩 클러스터** - [Azure Resource Manager 템플릿](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) 또는 [Azure PowerShell 스크립트](hpcpack-cluster-powershell-script.md)를 사용하여 A8, A9, H16r 또는 H16rm 크기의 Linux 계산 노드가 포함된 HPC 팩 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="b535e-119">각 옵션 사용 시의 필수 구성 요소 및 단계는 [Azure에서 HPC 팩 클러스터의 Linux 계산 노드 시작](hpcpack-cluster.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b535e-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span></span> <span data-ttu-id="b535e-120">PowerShell 스크립트 배포 옵션을 선택하는 경우 이 문서 끝에 나오는 샘플 파일의 샘플 구성 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b535e-120">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span></span> <span data-ttu-id="b535e-121">이 구성을 사용하여 A8 크기 Windows Server 2012 R2 헤드 노드 1개 및 A8 크기 SUSE Linux Enterprise Server 12 계산 노드 2개로 구성되는 Azure 기반 HPC Pack 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-121">Use this configuration to deploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="b535e-122">구독 및 서비스 이름을 적절한 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="b535e-123">**알아야 할 추가 사항**</span><span class="sxs-lookup"><span data-stu-id="b535e-123">**Additional things to know**</span></span>
  
  * <span data-ttu-id="b535e-124">Azure의 Linux RDMA 네트워킹 필수 조건에 대한 자세한 내용은 [고성능 계산 VM 크기](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b535e-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="b535e-125">PowerShell 스크립트 배포 옵션을 사용하는 경우에는 단일 클라우드 서비스 내의 모든 Linux 계산 노드가 RDMA 네트워크 연결을 사용하도록 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-125">If you use the Powershell script deployment option, deploy all the Linux compute nodes within one cloud service to use the RDMA network connection.</span></span>
  * <span data-ttu-id="b535e-126">Linux 노드를 배포한 후 SSH에 연결하여 추가 관리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-126">After deploying the Linux nodes, connect by SSH to perform any additional administrative tasks.</span></span> <span data-ttu-id="b535e-127">Azure Portal에서 각 Linux VM에 대한 SSH 연결 세부 정보를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="b535e-127">Find the SSH connection details for each Linux VM in the Azure portal.</span></span>  
* <span data-ttu-id="b535e-128">**Intel MPI** - Azure의 SLES 12 HPC 계산 노드에서 OpenFOAM를 실행하려면 [Intel.com 사이트](https://software.intel.com/en-us/intel-mpi-library/)에서 Intel MPI Library 5 런타임을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-128">**Intel MPI** - To run OpenFOAM on SLES 12 HPC compute nodes in Azure, you need to install the Intel MPI Library 5 runtime from the [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="b535e-129">(Intel MPI 5는 CentOS 기반 HPC 이미지에 미리 설치되어 있습니다.)  이후 단계에서 필요한 경우 Linux 계산 노트에 Intel MPI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="b535e-130">이 단계를 준비하려면 Intel에 등록한 후 확인 전자 메일의 링크를 따라 관련 웹 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-130">To prepare for this step, after you register with Intel, follow the link in the confirmation email to the related web page.</span></span> <span data-ttu-id="b535e-131">그런 다음 해당 Intel MPI 버전에 대한 .tgz 파일의 다운로드 링크를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-131">Then, copy the download link for the .tgz file for the appropriate version of Intel MPI.</span></span> <span data-ttu-id="b535e-132">이 문서는 Intel MPI 5.0.3.048 버전을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="b535e-133">**OpenFOAM 소스 팩** - [OpenFOAM Foundation 사이트](http://openfoam.org/download/2-3-1-source/)에서 Linux용 OpenFOAM 소스 팩 소프트웨어를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-133">**OpenFOAM Source Pack** - Download the OpenFOAM Source Pack software for Linux from the [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="b535e-134">이 문서는 OpenFOAM-2.3.1.tgz로 다운로드할 수 있는 소스 팩 버전 2.3.1을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="b535e-135">Linux 계산 노드에서 OpenFOAM의 압축을 풀고 컴파일하려면 이 문서의 뒷부분에 나오는 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-135">Follow the instructions later in this article to unpack and compile OpenFOAM on the Linux compute nodes.</span></span>
* <span data-ttu-id="b535e-136">**EnSight** (선택 사항) - OpenFOAM 시뮬레이션의 결과를 확인하려면 [EnSight](https://www.ceisoftware.com/download/) 시각화 및 분석 프로그램을 다운로드 및 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-136">**EnSight** (optional) - To see the results of your OpenFOAM simulation, download and install the [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="b535e-137">라이선스 및 다운로드 정보는 EnSight 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-137">Licensing and download information are at the EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="b535e-138">계산 노드 간 상호 트러스트 설정</span><span class="sxs-lookup"><span data-stu-id="b535e-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="b535e-139">여러 Linux 노드에서 크로스 노드 작업을 실행하려면 노드가 서로 신뢰해야 합니다(**rsh** 또는 **ssh** 사용).</span><span class="sxs-lookup"><span data-stu-id="b535e-139">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="b535e-140">Microsoft HPC 팩 IaaS 배포 스크립트로 HPC 팩 클러스터를 만드는 경우 스크립트에서 사용자가 지정한 관리자 계정에 대해 영구 상호 트러스트를 자동으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-140">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span></span> <span data-ttu-id="b535e-141">클러스터의 도메인에 만든 관리자가 아닌 사용자의 경우 작업이 할당될 때 노드 간에 임시 상호 트러스트를 설정하고 작업이 완료된 후 관계를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-141">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them, and destroy the relationship after the job is complete.</span></span> <span data-ttu-id="b535e-142">각 사용자에 대해 트러스트를 설정하려면 HPC Pack에서 트러스트 관계에 사용하는 RSA 키 쌍을 클러스터에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-142">To establish trust for each user, provide an RSA key pair to the cluster that HPC Pack uses for the trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="b535e-143">RSA 키 쌍 생성</span><span class="sxs-lookup"><span data-stu-id="b535e-143">Generate an RSA key pair</span></span>
<span data-ttu-id="b535e-144">Linux **ssh-keygen** 명령을 실행하여 공개 키 및 개인 키를 포함하는 RSA 키 쌍을 간편하게 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-144">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="b535e-145">Linux 컴퓨터에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-145">Log on to a Linux computer.</span></span>
2. <span data-ttu-id="b535e-146">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-146">Run the following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="b535e-147">명령이 완료될 때까지 기본 설정을 사용하려면 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-147">Press **Enter** to use the default settings until the command is completed.</span></span> <span data-ttu-id="b535e-148">여기에 암호를 입력하지 마십시오. 암호를 묻는 메시지가 표시되면 **Enter** 키만 누르십시오.</span><span class="sxs-lookup"><span data-stu-id="b535e-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![RSA 키 쌍 생성][keygen]
3. <span data-ttu-id="b535e-150">디렉터리를 ~/.ssh 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-150">Change directory to the ~/.ssh directory.</span></span> <span data-ttu-id="b535e-151">개인 키는 id_rsa에 저장되고 공개 키는 id_rsa.pub에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-151">The private key is stored in id_rsa and the public key in id_rsa.pub.</span></span>
   
   ![개인 및 공용 키][keys]

### <a name="add-the-key-pair-to-the-hpc-pack-cluster"></a><span data-ttu-id="b535e-153">HPC 팩 클러스터에 키 쌍 추가</span><span class="sxs-lookup"><span data-stu-id="b535e-153">Add the key pair to the HPC Pack cluster</span></span>
1. <span data-ttu-id="b535e-154">HPC 팩 관리자 계정(배포 스크립트를 실행 할 때 설정한 관리자 계정)으로 헤드 노드에 원격 데스크톱 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-154">Make a Remote Desktop connection to your head node with your HPC Pack administrator account (the administrator account you set up when you ran the deployment script).</span></span>
2. <span data-ttu-id="b535e-155">표준 Windows Server 절차를 사용하여 클러스터의 Active Directory 도메인에 도메인 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-155">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span></span> <span data-ttu-id="b535e-156">예를 들어 헤드 노드에서 Active Directory 사용자 및 컴퓨터 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-156">For example, use the Active Directory User and Computers tool on the head node.</span></span> <span data-ttu-id="b535e-157">이 문서의 예에서는 hpclab\hpcuser라는 이름의 도메인 사용자를 만든다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-157">The examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="b535e-158">C:\cred.xml이라는 이름의 파일을 만들고 RSA 키 데이터를 여기에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-158">Create a file named C:\cred.xml and copy the RSA key data into it.</span></span> <span data-ttu-id="b535e-159">샘플 cred.xml 파일은 이 문서 끝에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-159">A sample cred.xml file is at the end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy the contents of private key here</PrivateKey>
     <PublicKey>Copy the contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="b535e-160">명령 프롬프트를 열고 다음 명령을 입력하여 hpclab\hpcuser 계정에 대한 자격 증명 데이터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-160">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span></span> <span data-ttu-id="b535e-161">키 데이터를 위해 만든 C:\cred.xml 파일의 이름을 전달하는 데 **extendeddata** 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-161">You use the **extendeddata** parameter to pass the name of C:\cred.xml file you created for the key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="b535e-162">이 명령은 출력 없이 성공적으로 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-162">This command completes successfully without output.</span></span> <span data-ttu-id="b535e-163">작업을 실행하는 데 필요한 사용자의 자격 증명을 설정한 후에 cred.xml 파일을 안전한 위치에 저장하거나 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-163">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="b535e-164">Linux 노드 중 하나에서 RSA 키 쌍을 생성한 경우 사용이 끝난 후 키를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-164">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span></span> <span data-ttu-id="b535e-165">HPC Pack은 기존 id_rsa 파일 또는 id_rsa.pub 파일을 찾으면 상호 트러스트를 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b535e-166">공유 클러스터에서 Linux 작업을 클러스터 관리자로 실행하지 않는 것이 좋습니다. 관리자가 제출한 작업이 Linux 노드에서 루트 계정으로 실행되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span></span> <span data-ttu-id="b535e-167">그러나 관리자가 아닌 사용자가 제출한 작업은 작업 사용자와 동일한 이름을 가진 로컬 Linux 사용자 계정에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-167">However, a job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span></span> <span data-ttu-id="b535e-168">이 경우 HPC Pack은 작업에 할당된 노드 간에 이 Linux 사용자에 대한 상호 트러스트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-168">In this case, HPC Pack sets up mutual trust for this Linux user across the nodes allocated to the job.</span></span> <span data-ttu-id="b535e-169">작업을 실행하기 전에 Linux 노드에서 Linux 사용자를 수동으로 설정할 수 있습니다. 또는 HPC 팩에서 작업이 제출될 때 사용자를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-169">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span></span> <span data-ttu-id="b535e-170">HPC 팩에서 사용자를 만드는 경우 HPC 팩은 작업이 완료된 후 사용자를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-170">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span></span> <span data-ttu-id="b535e-171">보안 위협을 줄이기 위해 HPC Pack은 작업이 완료된 후 이 키를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-171">To reduce security threats, HPC Pack removes the keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="b535e-172">사용자가 액세스할 파일 공유를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="b535e-173">이제 헤드 노드에서 폴더에 대한 표준 SMB 공유를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-173">Now set up a standard SMB share on a folder on the head node.</span></span> <span data-ttu-id="b535e-174">Linux 노드에서 일반 경로로 응용 프로그램 파일에 액세스할 수 있도록 하려면 Linux 노드에 공유 폴더를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-174">To allow the Linux nodes to access application files with a common path, mount the shared folder on the Linux nodes.</span></span> <span data-ttu-id="b535e-175">원하는 경우 여러 시나리오에서 권장되는 Azure 파일 공유 또는 NFS 공유와 같은 다른 파일 공유 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="b535e-176">[Azure에서 HPC 팩 클러스터의 Linux 계산 노드 시작](hpcpack-cluster.md)의 파일 공유 정보 및 자세한 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b535e-176">See the file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="b535e-177">헤드 노드에서 폴더를 만들고 읽기/쓰기 권한을 설정하여 모든 사용자에게 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-177">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span></span> <span data-ttu-id="b535e-178">예를 들어 헤드 노드의 C:\OpenFOAM을 \\\\SUSE12RDMA-HN\OpenFOAM으로 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-178">For example, share C:\OpenFOAM on the head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="b535e-179">여기에서 *SUSE12RDMA-HN* 은 헤드 노드의 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-179">Here, *SUSE12RDMA-HN* is the host name of the head node.</span></span>
2. <span data-ttu-id="b535e-180">Windows PowerShell 창을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-180">Open a Windows PowerShell window and run the following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="b535e-181">첫 번째 명령은 LinuxNodes 그룹의 모든 노드에 /openfoam이라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-181">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="b535e-182">두 번째 명령은 dir_mode 및 file_mode 비트를 777로 설정하여 공유 폴더 //SUSE12RDMA-HN/OpenFOAM을 Linux 노드에 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-182">The second command mounts the shared folder //SUSE12RDMA-HN/OpenFOAM on the Linux nodes with dir_mode and file_mode bits set to 777.</span></span> <span data-ttu-id="b535e-183">명령의 *username*과 *password*는 헤드 노드 사용자의 자격 증명이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-183">The *username* and *password* in the command should be the credentials of a user on the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="b535e-184">두 번째 명령의 “\\`” 기호는 PowerShell의 이스케이프 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-184">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="b535e-185">“\\`,”는 ","(쉼표)가 명령의 일부임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-185">“\\`,” means the “,” (comma character) is a part of the command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="b535e-186">MPI 및 OpenFOAM 설치</span><span class="sxs-lookup"><span data-stu-id="b535e-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="b535e-187">RDMA 네트워크에 MPI 작업으로 OpenFOAM을 실행하려면 Intel MPI 라이브러리를 사용하여 OpenFOAM을 컴파일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-187">To run OpenFOAM as an MPI job on the RDMA network, you need to compile OpenFOAM with the Intel MPI libraries.</span></span> 

<span data-ttu-id="b535e-188">먼저 여러 **clusrun** 명령을 실행하여 Linux 노드에 Intel MPI 라이브러리 및 OpenFOAM을 설치합니다(아직 설치하지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="b535e-188">First, run several **clusrun** commands to install Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="b535e-189">이전에 구성된 헤드 노드 공유를 사용하여 Linux 노드 간에 설치 파일을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-189">Use the head node share configured previously to share the installation files among the Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b535e-190">이러한 설치 및 컴파일 단계는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="b535e-191">종속 컴파일러 및 라이브러리를 올바르게 설치할 수 있도록 Linux 시스템 관리에 대해 어느 정도 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-191">You need some knowledge of Linux system administration to ensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="b535e-192">사용 중인 Intel MPI 및 OpenFOAM에 맞게 특정 환경 변수 또는 기타 설정을 수정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-192">You might need to modify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="b535e-193">자세한 내용은 사용 환경에 맞는 [Linux 설치 가이드용 Intel MPI 라이브러리](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) 및 [OpenFOAM 원본 팩 설치](http://openfoam.org/download/2-3-1-source/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b535e-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="b535e-194">Intel MPI 설치</span><span class="sxs-lookup"><span data-stu-id="b535e-194">Install Intel MPI</span></span>
<span data-ttu-id="b535e-195">Intel MPI에 대해 다운로드된 설치 패키지(이 예제에서 l_mpi_p_5.0.3.048.tgz)를 헤드 노드의 C:\OpenFoam에 저장하여 Linux 노드가 /openfoam에서 이 파일에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-195">Save the downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="b535e-196">그런 다음 **clusrun** 을 실행하여 모든 Linux 노드에 Intel MPI Library를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-196">Then run **clusrun** to install Intel MPI library on all the Linux nodes.</span></span>

1. <span data-ttu-id="b535e-197">다음 명령은 설치 패키지를 복사하고 각 노드의 /opt/intel에 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-197">The following commands copy the installation package and extract it to /opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="b535e-198">Intel MPI Library를 자동으로 설치하려면 silent.cfg 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-198">To install Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="b535e-199">이 문서의 끝에 있는 샘플 파일에서 예제를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-199">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="b535e-200">이 파일을 공유 폴더 /openfoam에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-200">Place this file in the shared folder /openfoam.</span></span> <span data-ttu-id="b535e-201">silent.cfg 파일에 대한 자세한 내용은 [Linux 설치 가이드용 Intel MPI Library - 자동 설치](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b535e-201">For details about the silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="b535e-202">silent.cfg 파일을 Linux 줄 끝(CR LF가 아닌 LF만)을 사용하여 텍스트 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="b535e-203">이 단계를 수행해야 Linux 노드에서 해당 작업이 제대로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-203">This step ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="b535e-204">자동 모드에서 Intel MPI Library를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="b535e-205">MPI 구성</span><span class="sxs-lookup"><span data-stu-id="b535e-205">Configure MPI</span></span>
<span data-ttu-id="b535e-206">테스트를 위해 각 Linux 노드에서 /etc/security/limits.conf에 다음 줄을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-206">For testing, you should add the following lines to the /etc/security/limits.conf on each of the Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="b535e-207">limits.conf 파일을 업데이트한 후 Linux 노드를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-207">Restart the Linux nodes after you update the limits.conf file.</span></span> <span data-ttu-id="b535e-208">예를 들어 다음 **clusrun** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-208">For example, use the following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="b535e-209">다시 시작한 후 공유 폴더가 /openfoam으로 탑재되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-209">After restarting, ensure that the shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="b535e-210">OpenFOAM 컴파일 및 설치</span><span class="sxs-lookup"><span data-stu-id="b535e-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="b535e-211">OpenFOAM 소스 팩에 대해 다운로드된 설치 패키지(이 예제에서 OpenFOAM-2.3.1.tgz)를 헤드 노드의 C:\OpenFoam에 저장하여 Linux 노드가 /openfoam에서 이 파일에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-211">Save the downloaded installation package for the OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) to C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="b535e-212">그런 다음 **clusrun** 명령을 실행하여 모든 Linux 노드의 OpenFOAM을 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-212">Then run **clusrun** commands to compile OpenFOAM on all the Linux nodes.</span></span>

1. <span data-ttu-id="b535e-213">각 Linux 노드에서 폴더 /opt/OpenFOAM을 만들고 이 폴더에 소스 패키지를 복사하고 거기에 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-213">Create a folder /opt/OpenFOAM on each Linux node, copy the source package to this folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="b535e-214">Intel MPI Library와 함께 OpenFOAM을 컴파일하려면 먼저 Intel MPI 및 OpenFOAM에 대한 몇 가지 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-214">To compile OpenFOAM with the Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="b535e-215">settings.sh라는 bash 스크립트를 사용하여 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-215">Use a bash script called settings.sh to set the variables.</span></span> <span data-ttu-id="b535e-216">이 문서의 끝에 있는 샘플 파일에서 예제를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-216">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="b535e-217">공유 폴더 /openfoam에 이 파일(Linux 줄 끝으로 저장됨)을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-217">Place this file (saved with Linux line endings) in the shared folder /openfoam.</span></span> <span data-ttu-id="b535e-218">이 파일에는 OpenFOAM 작업을 실행하기 위해 나중에 사용하는 MPI 및 OpenFOAM 런타임에 대한 설정이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-218">This file also contains settings for the MPI and OpenFOAM runtimes that you use later to run an OpenFOAM job.</span></span>
3. <span data-ttu-id="b535e-219">OpenFOAM을 컴파일하는 데 필요한 종속 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-219">Install dependent packages needed to compile OpenFOAM.</span></span> <span data-ttu-id="b535e-220">Linux 배포에 따라 리포지토리를 먼저 추가해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-220">Depending on your Linux distribution, you might first need to add a repository.</span></span> <span data-ttu-id="b535e-221">다음과 유사하게 **clusrun** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-221">Run **clusrun** commands similar to the following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="b535e-222">필요한 경우 제대로 실행하는지 확인하도록 각 Linux 노드에 SSH를 사용하여 명령을 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-222">If necessary, SSH to each Linux node to run the commands to confirm that they run properly.</span></span>
4. <span data-ttu-id="b535e-223">다음 명령을 실행하여 OpenFOAM을 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-223">Run the following command to compile OpenFOAM.</span></span> <span data-ttu-id="b535e-224">컴파일 프로세스를 완료하는 데 시간이 걸리며 표준 출력으로 많은 양의 로그 정보를 생성하므로 **/interleaved** 옵션을 사용하여 출력 인터리브를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-224">The compilation process takes some time to complete and generates a large amount of log information to standard output, so use the **/interleaved** option to display the output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="b535e-225">명령의 “\\`” 기호는 PowerShell의 이스케이프 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-225">The “\\`” symbol in the command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="b535e-226">“\\`&”는 "&"가 명령의 일부라는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-226">“\\`&” means the “&” is a part of the command.</span></span>
   > 
   > 

## <a name="prepare-to-run-an-openfoam-job"></a><span data-ttu-id="b535e-227">OpenFOAM 작업 실행 준비</span><span class="sxs-lookup"><span data-stu-id="b535e-227">Prepare to run an OpenFOAM job</span></span>
<span data-ttu-id="b535e-228">이제 2개의 Linux 노드에서 OpenFoam 샘플 중 하나인 sloshingTank3D라는 MPI 작업을 실행할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-228">Now get ready to run an MPI job called sloshingTank3D, which is one of the OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-the-runtime-environment"></a><span data-ttu-id="b535e-229">런타임 환경 설정</span><span class="sxs-lookup"><span data-stu-id="b535e-229">Set up the runtime environment</span></span>
<span data-ttu-id="b535e-230">Linux 노드에서 MPI 및 OpenFOAM에 대한 런타임 환경을 설정하려면 헤드 노드의 Windows PowerShell 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-230">To set up the runtime environments for MPI and OpenFOAM on the Linux nodes, run the following command in a Windows PowerShell window on the head node.</span></span> <span data-ttu-id="b535e-231">(이 명령은 SUSE Linux에 대해서만 유효합니다.)</span><span class="sxs-lookup"><span data-stu-id="b535e-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="b535e-232">샘플 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="b535e-232">Prepare sample data</span></span>
<span data-ttu-id="b535e-233">이전에 구성된 헤드 노드 공유를 사용하여 Linux 노드 간에 파일을 공유합니다(/openfoam으로 탑재됨).</span><span class="sxs-lookup"><span data-stu-id="b535e-233">Use the head node share you configured previously to share files among the Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="b535e-234">SSH에서 Linux 계산 노드 중 하나로.</span><span class="sxs-lookup"><span data-stu-id="b535e-234">SSH to one of your Linux compute nodes.</span></span>
2. <span data-ttu-id="b535e-235">아직 수행하지 않은 경우 다음 명령을 실행하여 OpenFOAM 런타임 환경 설정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-235">Run the following command to set up the OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="b535e-236">sloshingTank3D 샘플을 공유 폴더에 복사하고 공유 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-236">Copy the sloshingTank3D sample to the shared folder and navigate to it.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="b535e-237">이 샘플의 기본 매개 변수를 사용하면 실행하는 데 수십 분이 걸리므로 일부 매개 변수를 수정하여 더 빨리 실행하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-237">When you use the default parameters of this sample, it can take tens of minutes to run, so you might want to modify some parameters to make it run faster.</span></span> <span data-ttu-id="b535e-238">간단한 옵션 하나는 system/controlDict 파일에서 시간 단계 변수 deltaT 및 writeInterval을 수정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-238">One simple choice is to modify the time step variables deltaT and writeInterval in the system/controlDict file.</span></span> <span data-ttu-id="b535e-239">이 파일은 시간 제어 및 솔루션 데이터 읽기/쓰기와 관련된 모든 입력 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-239">This file stores all input data relating to the control of time and reading and writing solution data.</span></span> <span data-ttu-id="b535e-240">예를 들어 deltaT의 값을 0.05에서 0.5로 writeInterval의 값을 0.05에서 0.5로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-240">For example, you could change the value of deltaT from 0.05 to 0.5 and the value of writeInterval from 0.05 to 0.5.</span></span>
   
   ![단계 변수 수정][step_variables]
5. <span data-ttu-id="b535e-242">시스템/decomposeParDict 파일에서 변수에 대해 원하는 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-242">Specify desired values for the variables in the system/decomposeParDict file.</span></span> <span data-ttu-id="b535e-243">이 예제에서는 8개의 코어로 각각 2개의 Linux 노드를 사용하므로 numberOfSubdomains를 16으로 hierarchicalCoeffs의 n을 (1 1 16)으로 설정합니다. 이는 16개의 프로세스와 함께 병렬로 OpenFOAM을 실행하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains to 16 and n of hierarchicalCoeffs to (1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="b535e-244">자세한 내용은 [OpenFOAM 사용자 가이드: 3.4 병렬로 응용 프로그램 실행](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4)을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="b535e-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![프로세스 분해][decompose]
6. <span data-ttu-id="b535e-246">sloshingTank3D 디렉터리에서 다음 명령을 실행하여 샘플 데이터를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-246">Run the following commands from the sloshingTank3D directory to prepare the sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="b535e-247">헤드 노드에 샘플 데이터 파일이 C:\OpenFoam\sloshingTank3D로 복사된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-247">On the head node, you should see the sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="b535e-248">(C:\OpenFoam은 헤드 노드의 공유 폴더입니다.)</span><span class="sxs-lookup"><span data-stu-id="b535e-248">(C:\OpenFoam is the shared folder on the head node.)</span></span>
   
   ![헤드 노드의 데이터 파일][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="b535e-250">mpirun에 대한 호스트 파일</span><span class="sxs-lookup"><span data-stu-id="b535e-250">Host file for mpirun</span></span>
<span data-ttu-id="b535e-251">이 단계에서 **mpirun** 명령이 사용하는 호스트 파일(계산 노드 목록)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-251">In this step, you create a host file (a list of compute nodes) which the **mpirun** command uses.</span></span>

1. <span data-ttu-id="b535e-252">Linux 노드 중 하나에서 /openfoam 아래에 hostfile이라는 파일을 만들면 이 파일은 모든 Linux 노드에서 /openfoam/hostfile에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-252">On one of the Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="b535e-253">Linux 노드 이름을 이 파일에 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="b535e-254">이 예제에서 해당 파일에는 다음 이름이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-254">In this example, the file contains the following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="b535e-255">또한 이 파일을 헤드 노드의 C:\OpenFoam\hostfile에 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-255">You can also create this file at C:\OpenFoam\hostfile on the head node.</span></span> <span data-ttu-id="b535e-256">이 옵션을 선택하는 경우 Linux 줄 끝(CR LF가 아닌 LF만)을 사용하여 텍스트 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="b535e-257">이렇게 해야 Linux 노드에서 제대로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-257">This ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="b535e-258">**Bash 스크립트 래퍼**</span><span class="sxs-lookup"><span data-stu-id="b535e-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="b535e-259">많은 Linux 노드가 있고 그 중 일부에 대해서만 작업을 실행하려는 경우 어떤 노드가 작업에 할당되는지 모르므로 고정된 호스트 파일을 사용하는 것은 좋지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-259">If you have many Linux nodes and you want your job to run on only some of them, it’s not a good idea to use a fixed host file, because you don’t know which nodes will be allocated to your job.</span></span> <span data-ttu-id="b535e-260">이 경우 **mpirun** 에 대한 bash 스크립트 래퍼를 작성하여 호스트 파일을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-260">In this case, write a bash script wrapper for **mpirun** to create the host file automatically.</span></span> <span data-ttu-id="b535e-261">이 문서 끝에서 hpcimpirun.sh라는 예제 bash 스크립트 래퍼를 찾고 /openfoam/hpcimpirun.sh로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-261">You can find an example bash script wrapper called hpcimpirun.sh at the end of this article, and save it as /openfoam/hpcimpirun.sh.</span></span> <span data-ttu-id="b535e-262">이 예제 스크립트에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-262">This example script does the following:</span></span>
   
   1. <span data-ttu-id="b535e-263">**mpirun**및 일부 추가 명령 매개 변수에 대한 환경 변수를 설정하여 RDMA 네트워크를 통해 MPI 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-263">Sets up the environment variables for **mpirun**, and some addition command parameters to run the MPI job through the RDMA network.</span></span> <span data-ttu-id="b535e-264">이 경우 다음 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-264">In this case, it sets the following variables:</span></span>
      
      * <span data-ttu-id="b535e-265">I_MPI_FABRICS=shm:dapl</span><span class="sxs-lookup"><span data-stu-id="b535e-265">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="b535e-266">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span><span class="sxs-lookup"><span data-stu-id="b535e-266">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="b535e-267">I_MPI_DYNAMIC_CONNECTION=0</span><span class="sxs-lookup"><span data-stu-id="b535e-267">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="b535e-268">작업이 활성화될 때 HPC 헤드 노드로 설정되는 환경 변수 $CCP_NODES_CORES에 따라 호스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-268">Creates a host file according to the environment variable $CCP_NODES_CORES, which is set by the HPC head node when the job is activated.</span></span>
      
      <span data-ttu-id="b535e-269">$CCP_NODES_CORES의 형식은 이 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-269">The format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="b535e-270">여기서,</span><span class="sxs-lookup"><span data-stu-id="b535e-270">where</span></span>
      
      * <span data-ttu-id="b535e-271">`<Number of nodes>` - 이 작업에 할당된 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-271">`<Number of nodes>` - the number of nodes allocated to this job.</span></span>  
      * <span data-ttu-id="b535e-272">`<Name of node_n_...>` - 이 작업에 할당된 각 노드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-272">`<Name of node_n_...>` - the name of each node allocated to this job.</span></span>
      * <span data-ttu-id="b535e-273">`<Cores of node_n_...>` - 이 작업에 할당된 노드의 코어 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-273">`<Cores of node_n_...>` - the number of cores on the node allocated to this job.</span></span>
      
      <span data-ttu-id="b535e-274">예를 들어 작업에 실행할 노드가 2개 필요한 경우 $CCP_NODES_CORES는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-274">For example, if the job needs two nodes to run, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="b535e-275">**mpirun** 명령을 호출하고 명령줄에 2개의 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-275">Calls the **mpirun** command and appends two parameters to the command line.</span></span>
      
      * <span data-ttu-id="b535e-276">`--hostfile <hostfilepath>: <hostfilepath>` - 스크립트가 만드는 호스트 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-276">`--hostfile <hostfilepath>: <hostfilepath>` - the path of the host file the script creates</span></span>
      * <span data-ttu-id="b535e-277">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - 이 작업에 할당된 총 코어 수를 저장하는 HPC 팩 헤드 노드로 설정된 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-277">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by the HPC Pack head node, which stores the number of total cores allocated to this job.</span></span> <span data-ttu-id="b535e-278">이 경우 **mpirun**에 대한 프로세스의 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-278">In this case, it specifies the number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="b535e-279">OpenFOAM 작업 제출</span><span class="sxs-lookup"><span data-stu-id="b535e-279">Submit an OpenFOAM job</span></span>
<span data-ttu-id="b535e-280">이제 HPC 클러스터 관리자에서 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-280">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="b535e-281">작업 중 일부에 대한 명령줄의 스크립트 hpcimpirun.sh를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-281">You need to pass the script hpcimpirun.sh in the command lines for some of the job tasks.</span></span>

1. <span data-ttu-id="b535e-282">클러스터 헤드 노드에 연결하고 HPC 클러스터 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-282">Connect to your cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="b535e-283">**리소스 관리**에서 Linux 계산 노드가 **온라인** 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-283">**In Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span></span> <span data-ttu-id="b535e-284">온라인 상태가 아닌 경우 노드를 선택하고 **온라인 상태로 전환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-284">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="b535e-285">**작업 관리**에서 **새 작업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-285">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="b535e-286">작업 이름(예: *sloshingTank3D*)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-286">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![작업 세부 정보][job_details]
5. <span data-ttu-id="b535e-288">**작업 리소스**에서 리소스 유형을 “노드”로 선택하고 최소를 2로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-288">In **Job resources**, choose the type of resource as “Node” and set the Minimum to 2.</span></span> <span data-ttu-id="b535e-289">이 예제에서 이 구성은 각각이 8개의 코어를 포함하는 두 개의 Linux 노드에서 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-289">This configuration runs the job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![작업 리소스][job_resources]
6. <span data-ttu-id="b535e-291">왼쪽 탐색 영역에서 **작업 편집**을 클릭한 다음 **추가**를 클릭하여 작업(job)에 작업(task)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-291">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span></span> <span data-ttu-id="b535e-292">다음 명령줄과 설정을 사용하여 작업(job)에 4개 작업(task)을 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="b535e-292">Add four tasks to the job with the following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b535e-293">`source /openfoam/settings.sh` 실행으로 OpenFOAM 및 MPI 런타임 환경을 설정하면 다음 각 작업은 OpenFOAM 명령 전에 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-293">Running `source /openfoam/settings.sh` sets up the OpenFOAM and MPI runtime environments, so each of the following tasks calls it before the OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="b535e-294">**작업 1**.</span><span class="sxs-lookup"><span data-stu-id="b535e-294">**Task 1**.</span></span> <span data-ttu-id="b535e-295">**decomposePar**를 실행하여 병렬로 **interDyMFoam**을 실행하는 데이터 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-295">Run **decomposePar** to generate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="b535e-296">작업(task)에 1개의 노드 할당</span><span class="sxs-lookup"><span data-stu-id="b535e-296">Assign one node to the task</span></span>
     * <span data-ttu-id="b535e-297">**명령 줄** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="b535e-297">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="b535e-298">**작업 디렉터리** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="b535e-298">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="b535e-299">다음 그림을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b535e-299">See the following figure.</span></span> <span data-ttu-id="b535e-300">나머지 작업을 비슷하게 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-300">You configure the remaining tasks similarly.</span></span>
     
     ![작업 1 세부 정보][task_details1]
   * <span data-ttu-id="b535e-302">**작업 2**.</span><span class="sxs-lookup"><span data-stu-id="b535e-302">**Task 2**.</span></span> <span data-ttu-id="b535e-303">병렬로 **interDyMFoam** 을 실행하여 샘플을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-303">Run **interDyMFoam** in parallel to compute the sample.</span></span>
     
     * <span data-ttu-id="b535e-304">작업(task)에 2개의 노드 할당</span><span class="sxs-lookup"><span data-stu-id="b535e-304">Assign two nodes to the task</span></span>
     * <span data-ttu-id="b535e-305">**명령 줄** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="b535e-305">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="b535e-306">**작업 디렉터리** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="b535e-306">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="b535e-307">**작업 3**.</span><span class="sxs-lookup"><span data-stu-id="b535e-307">**Task 3**.</span></span> <span data-ttu-id="b535e-308">**reconstructPar**를 실행하여 각 processor_N_ 디렉터리에서 단일 집합으로 시간 디렉터리의 집합을 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-308">Run **reconstructPar** to merge the sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="b535e-309">작업(task)에 1개의 노드 할당</span><span class="sxs-lookup"><span data-stu-id="b535e-309">Assign one node to the task</span></span>
     * <span data-ttu-id="b535e-310">**명령 줄** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="b535e-310">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="b535e-311">**작업 디렉터리** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="b535e-311">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="b535e-312">**작업 4**.</span><span class="sxs-lookup"><span data-stu-id="b535e-312">**Task 4**.</span></span> <span data-ttu-id="b535e-313">병렬로 **foamToEnsight** 를 실행하여 OpenFOAM 결과 파일을 EnSight 형식으로 변환하고 사례 디렉터리의 EnSight라는 디렉터리에 EnSight 파일을 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-313">Run **foamToEnsight** in parallel to convert the OpenFOAM result files into EnSight format and place the EnSight files in a directory named Ensight in the case directory.</span></span>
     
     * <span data-ttu-id="b535e-314">작업(task)에 2개의 노드 할당</span><span class="sxs-lookup"><span data-stu-id="b535e-314">Assign two nodes to the task</span></span>
     * <span data-ttu-id="b535e-315">**명령 줄** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="b535e-315">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="b535e-316">**작업 디렉터리** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="b535e-316">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="b535e-317">오름차순 작업 순서로 이러한 작업에 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-317">Add dependencies to these tasks in ascending task order.</span></span>
   
   ![작업 종속성][task_dependencies]
8. <span data-ttu-id="b535e-319">**제출** 을 클릭하여 이 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-319">Click **Submit** to run this job.</span></span>
   
   <span data-ttu-id="b535e-320">기본적으로 HPC 팩은 현재 로그온한 사용자 계정으로 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-320">By default, HPC Pack submits the job as your current logged-on user account.</span></span> <span data-ttu-id="b535e-321">**제출**을 클릭한 후 사용자 이름 및 암호를 입력하라는 대화 상자가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-321">After you click **Submit**, you might see a dialog box prompting you to enter the user name and password.</span></span>
   
   ![작업 자격 증명][creds]
   
   <span data-ttu-id="b535e-323">일부 조건에서 HPC Pack이 사용자가 이전에 입력한 사용자 정보를 저장해 두어 이 대화 상자가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-323">Under some conditions, HPC Pack remembers the user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="b535e-324">HPC Pack에서 이 대화 상자를 다시 표시하려면 명령 프롬프트에 다음 명령을 입력한 후 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-324">To make HPC Pack show it again, enter the following command at a Command prompt and then submit the job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="b535e-325">샘플에 대해 설정한 매개 변수에 따라 수십 분에서 몇 시간까지 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-325">The job takes from tens of minutes to several hours according to the parameters you have set for the sample.</span></span> <span data-ttu-id="b535e-326">열 지도에 Linux 노드에서 실행 중인 작업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-326">In the heat map, you see the job running on the Linux nodes.</span></span> 
   
   ![열 지도][heat_map]
   
   <span data-ttu-id="b535e-328">각 노드에서 8개의 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-328">On each node, eight processes are started.</span></span>
   
   ![Linux 프로세스][linux_processes]
10. <span data-ttu-id="b535e-330">작업이 완료되면 C:\OpenFoam\sloshingTank3D 아래의 폴더에서 작업 결과 및 C:\OpenFoam에서 로그 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-330">When the job finishes, find the job results in folders under C:\OpenFoam\sloshingTank3D, and the log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="b535e-331">EnSight에서 결과 보기</span><span class="sxs-lookup"><span data-stu-id="b535e-331">View results in EnSight</span></span>
<span data-ttu-id="b535e-332">필요에 따라 [EnSight](https://www.ceisoftware.com/) 를 사용하여 OpenFOAM 작업의 결과를 시각화하고 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-332">Optionally use [EnSight](https://www.ceisoftware.com/) to visualize and analyze the results of the OpenFOAM job.</span></span> <span data-ttu-id="b535e-333">EnSight에서 시각화 및 애니메이션에 대한 자세한 내용은 이 [비디오 가이드](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b535e-333">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="b535e-334">헤드 노드에서 EnSight를 설치한 후 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-334">After you install EnSight on the head node, start it.</span></span>
2. <span data-ttu-id="b535e-335">C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-335">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="b535e-336">뷰어에서 탱크를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-336">You see a tank in the viewer.</span></span>
   
   ![EnSight의 탱크][tank]
3. <span data-ttu-id="b535e-338">**internalMesh**에서 **Isosurface**를 만든 다음 변수 **alpha_water**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-338">Create an **Isosurface** from **internalMesh**, and then choose the variable **alpha_water**.</span></span>
   
   ![isosurface 만들기][isosurface]
4. <span data-ttu-id="b535e-340">이전 단계에서 만든 **Isosurface_part**에 대한 색을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-340">Set the color for **Isosurface_part** created in the previous step.</span></span> <span data-ttu-id="b535e-341">예를 들어 워터 블루로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-341">For example, set it to water blue.</span></span>
   
   ![Isosurface 색상 편집][isosurface_color]
5. <span data-ttu-id="b535e-343">**부품** 패널에서 **벽**을 선택하여 **벽**에서 **Iso-volume**을 만들고 도구 모음에서 **Isosurfaces** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-343">Create an **Iso-volume** from **walls** by selecting **walls** in the **Parts** panel and click the **Isosurfaces** button in the toolbar.</span></span>
6. <span data-ttu-id="b535e-344">대화 상자에서 **형식**을 **Isovolume**으로 선택하고 **Isovolume 범위**의 최소값을 0.5로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-344">In the dialog box, select **Type** as **Isovolume** and set the Min of **Isovolume range** to 0.5.</span></span> <span data-ttu-id="b535e-345">isovolume을 만들려면 **선택한 부품으로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-345">To create the isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="b535e-346">이전 단계에서 만든 **Iso_volume_part**에 대한 색을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-346">Set the color for **Iso_volume_part** created in the previous step.</span></span> <span data-ttu-id="b535e-347">예를 들어 딥 워터 블루로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-347">For example, set it to deep water blue.</span></span>
8. <span data-ttu-id="b535e-348">**벽**에 대한 색을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-348">Set the color for **walls**.</span></span> <span data-ttu-id="b535e-349">예를 들어 투명 흰색으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-349">For example, set it to transparent white.</span></span>
9. <span data-ttu-id="b535e-350">이제 **재생** 을 클릭하여 시뮬레이션의 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b535e-350">Now click **Play** to see the results of the simulation.</span></span>
   
    ![탱크 결과][tank_result]

## <a name="sample-files"></a><span data-ttu-id="b535e-352">샘플 파일</span><span class="sxs-lookup"><span data-stu-id="b535e-352">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="b535e-353">PowerShell 스크립트를 통한 클러스터 배포용 샘플 XML 구성 파일</span><span class="sxs-lookup"><span data-stu-id="b535e-353">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a><span data-ttu-id="b535e-354">샘플 cred.xml 파일</span><span class="sxs-lookup"><span data-stu-id="b535e-354">Sample cred.xml file</span></span>
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```
### <a name="sample-silentcfg-file-to-install-mpi"></a><span data-ttu-id="b535e-355">MPI를 설치하는 샘플 silent.cfg 파일</span><span class="sxs-lookup"><span data-stu-id="b535e-355">Sample silent.cfg file to install MPI</span></span>
```
# Patterns used to check silent configuration file
#
# anythingpat - any string
# filepat     - the file location pattern (/file/location/to/license.lic)
# lspat       - the license server address pattern (0123@hostname)
# snpat       - the serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components to install, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path to the cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes to enable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes to update ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="b535e-356">샘플 settings.sh 스크립트</span><span class="sxs-lookup"><span data-stu-id="b535e-356">Sample settings.sh script</span></span>
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="b535e-357">샘플 hpcimpirun.sh 스크립트</span><span class="sxs-lookup"><span data-stu-id="b535e-357">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# The path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run the mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create the hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into the hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run the mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
