---
title: "Linux Vm에서 Microsoft HPC Pack을 사용한 aaaNAMD | Microsoft Docs"
description: "Azure에서 Microsoft HPC 팩을 배포하고 여러 Linux 컴퓨터 노드에서 charmrun으로 NAMD 시뮬레이션을 실행합니다."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a><span data-ttu-id="e7e25-103">Azure의 Linux 계산 노드에서 Microsoft HPC 팩을 사용하여 NAMD 실행</span><span class="sxs-lookup"><span data-stu-id="e7e25-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>
<span data-ttu-id="e7e25-104">이 문서에서는 한 가지 방법은 toorun Linux 고성능 HPC (컴퓨팅) 작업 부하 Azure 가상 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-104">This article shows you one way toorun a Linux high-performance computing (HPC) workload on Azure virtual machines.</span></span> <span data-ttu-id="e7e25-105">설정 하는 여기에서 [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) 실행 하 고 Azure에서 Linux 계산 노드가 있는 클러스터는 [NAMD](http://www.ks.uiuc.edu/Research/namd/) 시뮬레이션 toocalculate 및 큰 biomolecular 시스템의 hello 구조를 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation toocalculate and visualize hello structure of a large biomolecular system.</span></span>  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* <span data-ttu-id="e7e25-106">**NAMD** (Nanoscale 분자 Dynamics 프로그램용)는 고성능 큰 biomolecular 시스템을 시뮬레이션 하기 위한 병렬 분자 dynamics 패키지 들어 있는 원소 toomillions를 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up toomillions of atoms.</span></span> <span data-ttu-id="e7e25-107">이러한 시스템의 예로는 바이러스, 세포 구조, 거대한 단백질 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-107">Examples of these systems include viruses, cell structures, and large proteins.</span></span> <span data-ttu-id="e7e25-108">NAMD toohundreds 일반적인 시뮬레이션 및 가장 큰 시뮬레이션 hello에 대 한 코어 500, 000 개 보다 toomore에 대 한 코어의 배율을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-108">NAMD scales toohundreds of cores for typical simulations and toomore than 500,000 cores for hello largest simulations.</span></span>
* <span data-ttu-id="e7e25-109">**Microsoft HPC Pack** 기능 toorun 제공 대규모 HPC 및 온-프레미스 컴퓨터 또는 Azure 가상 컴퓨터의 클러스터에 있는 병렬 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-109">**Microsoft HPC Pack** provides features toorun large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span></span> <span data-ttu-id="e7e25-110">원래 Windows HPC 워크로드용 솔루션으로 개발된 HPC 팩은 이제 HPC 팩 클러스터에 배포된 Linux 계산 노드 VM에서 Linux HPC 응용 프로그램의 실행도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="e7e25-111">소개는 [Azure에서 HPC Pack 클러스터의 Linux 계산 노드 시작](hpcpack-cluster.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7e25-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span></span>

<span data-ttu-id="e7e25-112">다른 옵션 toorun Linux HPC에 대 한 Azure에서 작업 참조 [일괄 처리 및 고성능 컴퓨팅에 대 한 기술 리소스](../../../batch/batch-hpc-solutions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-112">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7e25-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e7e25-113">Prerequisites</span></span>
* <span data-ttu-id="e7e25-114">**Linux 계산 노드가 포함된 HPC 팩 클러스터** - [Azure Resource Manager 템플릿](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) 또는 [Azure PowerShell 스크립트](hpcpack-cluster-powershell-script.md)를 사용하여 Azure에서 Linux 계산 노드가 포함된 HPC 팩 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="e7e25-115">참조 [Azure에서 HPC Pack 클러스터에서 계산 노드 Linux 시작](hpcpack-cluster.md) hello 필수 구성 요소와 두 옵션 중 하나에 대 한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="e7e25-116">Hello PowerShell에서 스크립트 배포 옵션을 선택 하면이 문서의 hello 끝 hello 예제 파일의 hello 샘플 구성 파일을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e7e25-116">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="e7e25-117">이 파일은 Windows Server 2012 R2 헤드 노드 및 4개 크기의 대형 CentOS 6.6 계산 노드로 구성된 Azure 기반 HPC 팩 클러스터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span></span> <span data-ttu-id="e7e25-118">이 파일을 환경에 맞게 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-118">Customize this file as needed for your environment.</span></span>
* <span data-ttu-id="e7e25-119">**NAMD 소프트웨어 및 자습서 파일** -hello에서 Linux 용 소프트웨어를 다운로드 NAMD [NAMD](http://www.ks.uiuc.edu/Research/namd/) 사이트 (등록 필요).</span><span class="sxs-lookup"><span data-stu-id="e7e25-119">**NAMD software and tutorial files** - Download NAMD software for Linux from hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span></span> <span data-ttu-id="e7e25-120">이 문서는 NAMD, 2.10 버전을 기반으로 하 고 hello를 사용 하 여 [Linux-x86_64 (이더넷와 64 비트 Intel/AMD)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-120">This article is based on NAMD version 2.10, and uses hello [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span></span> <span data-ttu-id="e7e25-121">Hello를 다운로드할 수도 [NAMD 자습서 파일](http://www.ks.uiuc.edu/Training/Tutorials/#namd)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-121">Also download hello [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span></span> <span data-ttu-id="e7e25-122">hello 다운로드.tar 파일 및 hello 클러스터 헤드 노드에 Windows 도구 tooextract hello 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-122">hello downloads are .tar files, and you need a Windows tool tooextract hello files on hello cluster head node.</span></span> <span data-ttu-id="e7e25-123">tooextract hello 파일을이 문서의 뒷부분에 나오는 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-123">tooextract hello files, follow hello instructions later in this article.</span></span> 
* <span data-ttu-id="e7e25-124">**VMD** (선택 사항)-toosee hello 결과, NAMD 작업의 다운로드 및 설치 hello 분자 시각화 프로그램 [VMD](http://www.ks.uiuc.edu/Research/vmd/) 선택한 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-124">**VMD** (optional) - toosee hello results of your NAMD job, download and install hello molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span></span> <span data-ttu-id="e7e25-125">hello 현재 버전은 1.9.2입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-125">hello current version is 1.9.2.</span></span> <span data-ttu-id="e7e25-126">Hello VMD 다운로드 사이트 tooget 시작을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e7e25-126">See hello VMD download site tooget started.</span></span>  

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="e7e25-127">계산 노드 간 상호 트러스트 설정</span><span class="sxs-lookup"><span data-stu-id="e7e25-127">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="e7e25-128">Hello 노드 tootrust 서로 필요 하 여러 Linux 노드에 대해 노드 간 작업 실행 (여 **rsh** 또는 **ssh**).</span><span class="sxs-lookup"><span data-stu-id="e7e25-128">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="e7e25-129">Microsoft HPC Pack IaaS 배포 스크립트 hello로 hello HPC Pack 클러스터를 만들 때 hello 스크립트는 자동으로 지정 하는 hello 관리자 계정에 대 한 영구 상호 트러스트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-129">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="e7e25-130">Hello 클러스터의 도메인에서 만드는 관리자가 아닌 사용자를 위해 한 hello 노드 간에 상호 트러스트 임시를 tooset 작업 toothem 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-130">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem.</span></span> <span data-ttu-id="e7e25-131">그런 다음 hello 작업이 완료 된 후 hello 관계를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-131">Then, destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="e7e25-132">toodo 각 사용자에 대해이 제공 하는 RSA 키 쌍 toohello 클러스터는 HPC Pack tooestablish hello 트러스트 관계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-132">toodo this for each user, provide an RSA key pair toohello cluster which HPC Pack uses tooestablish hello trust relationship.</span></span> <span data-ttu-id="e7e25-133">지침이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-133">Instructions follow.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="e7e25-134">RSA 키 쌍 생성</span><span class="sxs-lookup"><span data-stu-id="e7e25-134">Generate an RSA key pair</span></span>
<span data-ttu-id="e7e25-135">공개 키와 개인 키를 포함 하는 RSA 키 쌍을 쉽게 toogenerate를 실행 하 여 Linux hello **붙여넣으세요** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-135">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="e7e25-136">Linux 컴퓨터 tooa에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-136">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="e7e25-137">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-137">Run hello following command:</span></span>
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="e7e25-138">키를 눌러 **Enter** hello 명령이 완료 될 때까지 toouse hello 기본 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-138">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="e7e25-139">여기에 암호를 입력하지 마십시오. 암호를 묻는 메시지가 표시되면 **Enter** 키만 누르십시오.</span><span class="sxs-lookup"><span data-stu-id="e7e25-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![RSA 키 쌍 생성][keygen]
3. <span data-ttu-id="e7e25-141">디렉터리 toohello ~/.ssh 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-141">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="e7e25-142">개인 키 hello id_rsa.pub id_rsa와 hello 공개 키에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-142">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![개인 및 공용 키][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="e7e25-144">Hello 키 쌍 toohello HPC Pack 클러스터 추가</span><span class="sxs-lookup"><span data-stu-id="e7e25-144">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="e7e25-145">[원격 데스크톱 연결](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 도메인 자격 증명 (예를 들어 hpc\clusteradmin) hello 클러스터를 배포할 때 제공한 hello 사용 하 여 toohello 헤드 노드 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, hpc\clusteradmin).</span></span> <span data-ttu-id="e7e25-146">Hello 헤드 노드에서 hello 클러스터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-146">You manage hello cluster from hello head node.</span></span>
2. <span data-ttu-id="e7e25-147">Hello 클러스터의 Active Directory 도메인에 표준 Windows Server 절차 toocreate 도메인 사용자 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-147">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="e7e25-148">예를 들어 hello 헤드 노드에서 hello Active Directory 사용자 및 컴퓨터 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-148">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="e7e25-149">이 문서의 hello 예제 hello hpclab 도메인 (hpclab\hpcuser) hpcuser 이라는 도메인 사용자를 만들면 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-149">hello examples in this article assume you create a domain user named hpcuser in hello hpclab domain (hpclab\hpcuser).</span></span>
3. <span data-ttu-id="e7e25-150">클러스터 사용자로 hello 도메인 사용자 toohello HPC Pack 클러스터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-150">Add hello domain user toohello HPC Pack cluster as a cluster user.</span></span> <span data-ttu-id="e7e25-151">지침은 [클러스터 사용자 추가 또는 제거](https://technet.microsoft.com/library/ff919330.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7e25-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span></span>
4. <span data-ttu-id="e7e25-152">C:\cred.xml 및 복사 hello RSA 키 데이터를 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-152">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="e7e25-153">예 hello에 hello이이 문서의 뒷부분에서 샘플 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-153">You can find an example in hello sample files at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. <span data-ttu-id="e7e25-154">명령 프롬프트를 열고 다음 명령을 tooset hello hello hpclab\hpcuser 계정에 대 한 데이터를 자격 증명 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-154">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="e7e25-155">Hello를 사용 하 여 **extendeddata** 매개 변수 toopass hello hello C:\cred.xml 만든 파일의 hello 키 데이터에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-155">You use hello **extendeddata** parameter toopass hello name of hello C:\cred.xml file you created for hello key data.</span></span>
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="e7e25-156">이 명령은 출력 없이 성공적으로 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-156">This command completes successfully without output.</span></span> <span data-ttu-id="e7e25-157">Toorun 작업 해야 하는 hello 사용자 계정에 대 한 hello 자격 증명을 설정한 후 hello cred.xml 파일을 안전한 위치에 저장 하거나 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-157">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
6. <span data-ttu-id="e7e25-158">Linux 노드 중 하나에서 hello RSA 키 쌍을 생성 한 경우 사용을 마친 후 toodelete hello 키를 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-158">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="e7e25-159">HPC 팩에서는 기존 id_rsa 파일 또는 id_rsa.pub 파일이 발견된 경우 상호 트러스트를 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7e25-160">म hello Linux 노드에서 hello 루트 계정에서 관리자가 제출 하는 작업 실행 되기 때문에 공유 클러스터에서 클러스터 관리자를 사용 하는 Linux 작업 실행 하는 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="e7e25-161">관리자가 아닌 사용자가 제출한 작업 이름과 같은 hello 작업 사용자로 이름을 hello로 로컬 Linux 사용자 계정에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-161">A job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="e7e25-162">이 경우 HPC Pack toohello 작업에 할당 된 모든 hello 노드에서이 Linux 사용자에 대 한 상호 트러스트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-162">In this case, HPC Pack sets up mutual trust for this Linux user across all hello nodes allocated toohello job.</span></span> <span data-ttu-id="e7e25-163">Hello 작업을 실행 하기 전에 hello Linux 노드에서 수동으로 hello Linux 사용자를 설정할 수 있습니다 또는 HPC 팩 hello 사용자 자동으로 만듭니다 hello 작업이 제출 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="e7e25-163">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="e7e25-164">HPC Pack hello 사용자를 만드는 경우 hello 작업이 완료 된 후 HPC Pack 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-164">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="e7e25-165">tooreduce 보안 위협, hello hello 노드에서 hello 작업이 완료 된 후 키가 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-165">tooreduce security threat, hello keys are removed after hello job completes on hello nodes.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="e7e25-166">사용자가 액세스할 파일 공유를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-166">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="e7e25-167">이제 SMB 파일 공유를 설정 하 고 모든 Linux 노드 tooallow hello Linux 노드 tooaccess NAMD 파일에는 일반적인 경로와 hello 공유 폴더에 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-167">Now set up an SMB file share, and mount hello shared folder on all Linux nodes tooallow hello Linux nodes tooaccess NAMD files with a common path.</span></span> <span data-ttu-id="e7e25-168">다음은 단계 toomount hello 헤드 노드에서 공유 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-168">Following are steps toomount a shared folder on hello head node.</span></span> <span data-ttu-id="e7e25-169">공유 현재 hello Azure 파일 서비스를 지원 하지 않는 CentOS 6.6 같은 분포에 대 한 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support hello Azure File service.</span></span> <span data-ttu-id="e7e25-170">Linux 노드에 있는 Azure 파일 공유를 지 원하는 경우 참조 [어떻게 toouse Azure 파일 저장소와 Linux](../../../storage/files/storage-how-to-use-files-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-170">If your Linux nodes support an Azure File share, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="e7e25-171">HPC 팩의 추가 파일 공유 옵션에 대해서는 [Azure에서 HPC 팩 클러스터의 Linux 계산 노드 시작](hpcpack-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7e25-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="e7e25-172">Hello 헤드 노드에 대 한 폴더를 만들고 읽기/쓰기 권한을 설정 하 여 tooEveryone을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-172">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="e7e25-173">이 예제에서는 \\ \\CentOS66HN\Namd hello 폴더, 여기서 CentOS66HN은 hello 헤드 노드의 호스트 이름을 hello hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-173">In this example, \\\\CentOS66HN\Namd is hello name of hello folder, where CentOS66HN is hello host name of hello head node.</span></span>
2. <span data-ttu-id="e7e25-174">Hello 공유 폴더에 namd2 라는 하위 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-174">Create a subfolder named namd2 in hello shared folder.</span></span> <span data-ttu-id="e7e25-175">namd2에 namdsample이라는 또 다른 하위 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-175">In namd2, create another subfolder named namdsample.</span></span>
3. <span data-ttu-id="e7e25-176">Windows 버전을 사용 하 여 hello 폴더의 hello NAMD 파일을 추출 **tar** 또는.tar 보관 파일에 작동 하는 다른 Windows 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-176">Extract hello NAMD files in hello folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span></span> 
   
   * <span data-ttu-id="e7e25-177">Hello NAMD tar 보관 너무 추출\\\\CentOS66HN\Namd\namd2 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-177">Extract hello NAMD tar archive too\\\\CentOS66HN\Namd\namd2.</span></span>
   * <span data-ttu-id="e7e25-178">Hello 자습서 파일에서 추출 \\ \\CentOS66HN\Namd\namd2\namdsample 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-178">Extract hello tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span></span>
4. <span data-ttu-id="e7e25-179">Windows PowerShell 창을 열고 명령 toomount hello hello Linux 노드에 있는 공유 폴더를 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-179">Open a Windows PowerShell window and run hello following commands toomount hello shared folder on hello Linux nodes.</span></span>
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="e7e25-180">첫 번째 명령은 hello hello LinuxNodes 그룹의 모든 노드에서 /namd2 라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-180">hello first command creates a folder named /namd2 on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="e7e25-181">두 번째 명령은 hello hello 공유 폴더 //CentOS66HN/Namd/namd2 dir_mode 및 file_mode 비트 집합 too777 hello 폴더에 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-181">hello second command mounts hello shared folder //CentOS66HN/Namd/namd2 onto hello folder with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="e7e25-182">hello *username* 및 *암호* hello 명령 hello 헤드 노드에 대 한 사용자의 hello 자격 증명 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-182">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="e7e25-183">hello "\\`" hello 두 번째 명령은의 기호는 PowerShell에 대 한 이스케이프 기호는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-183">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="e7e25-184">"\\`,"hello 의미"," (쉼표 문자)는 hello 명령의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-184">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a><span data-ttu-id="e7e25-185">Bash 스크립트 toorun NAMD 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="e7e25-185">Create a Bash script toorun a NAMD job</span></span>
<span data-ttu-id="e7e25-186">NAMD 작업 필요는 *nodelist* 파일에서 **charmrun** toodetermine 노드 toouse NAMD 프로세스를 시작할 때 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-186">Your NAMD job needs a *nodelist* file for **charmrun** toodetermine hello number of nodes toouse when starting NAMD processes.</span></span> <span data-ttu-id="e7e25-187">Hello nodelist 파일을 생성 하 고 실행 하는 Bash 스크립트를 사용 하면 **charmrun** nodelist 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-187">You use a Bash script that generates hello nodelist file and runs **charmrun** with this nodelist file.</span></span> <span data-ttu-id="e7e25-188">그런 다음 이 스크립트를 호출하는 HPC 클러스터 관리자에서 NAMD 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span></span>

<span data-ttu-id="e7e25-189">원하는 텍스트 편집기를 사용 하 여 hello NAMD 프로그램 파일을 포함 하는 hello /namd2 폴더에 Bash 스크립트를 만들고 hpccharmrun.sh 라는 이름을 지정 합니다. 빠른 개념 증명에 대 한 hello이이 문서의 뒷부분에서 제공 하는 hello 예제 hpccharmrun.sh 스크립트를 복사 하 고 너무 이동[NAMD 작업을 제출](#submit-a-namd-job)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-189">Using a text editor of your choice, create a Bash script in hello /namd2 folder containing hello NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy hello example hpccharmrun.sh script provided at hello end of this article and go too[Submit a NAMD job](#submit-a-namd-job).</span></span>

> [!TIP]
> <span data-ttu-id="e7e25-190">스크립트를 Linux 줄 끝(CR LF가 아닌 LF만)을 사용하여 텍스트 파일로 저장하십시오.</span><span class="sxs-lookup"><span data-stu-id="e7e25-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="e7e25-191">이렇게 하면 hello Linux 노드에에서 제대로 실행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-191">This ensures that it runs properly on hello Linux nodes.</span></span>
> 
> 

<span data-ttu-id="e7e25-192">아래에서는 이 Bash 스크립트가 수행하는 작업에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-192">Following are details about what this bash script does.</span></span> 

1. <span data-ttu-id="e7e25-193">일부 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-193">Define some variables.</span></span>
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. <span data-ttu-id="e7e25-194">Hello 환경 변수에서 노드 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-194">Get node information from hello environment variables.</span></span> <span data-ttu-id="e7e25-195">$NODESCORES는 $CCP_NODES_CORES의 분할 단어 목록을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span></span> <span data-ttu-id="e7e25-196">$COUNT은 $NODESCORES hello 크기를입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-196">$COUNT is hello size of $NODESCORES.</span></span>
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   <span data-ttu-id="e7e25-197">hello hello $CCP_NODES_CORES 변수의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-197">hello format for hello $CCP_NODES_CORES variable is as follows:</span></span>
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   <span data-ttu-id="e7e25-198">이 변수는 hello 노드, 노드 이름 및 각 노드에서 toohello 작업에 할당 되는 코어 수의 총 수를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-198">This variable lists hello total number of nodes, node names, and number of cores on each node that are allocated toohello job.</span></span> <span data-ttu-id="e7e25-199">예를 들어 hello 작업 10 코어 toorun 경우, $CCP_NODES_CORES hello 값은 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-199">For example, if hello job needs 10 cores toorun, hello value of $CCP_NODES_CORES is similar to:</span></span>
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. <span data-ttu-id="e7e25-200">Hello $CCP_NODES_CORES 변수를 설정 하지 않은 경우 시작 **charmrun** 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-200">If hello $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span></span> <span data-ttu-id="e7e25-201">(이러한 경우는 Linux 노드에서 이 스크립트를 직접 실행하는 경우에만 발생합니다.)</span><span class="sxs-lookup"><span data-stu-id="e7e25-201">(This should only occur when you run this script directly on your Linux nodes.)</span></span>
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. <span data-ttu-id="e7e25-202">또는 **charmrun**에 대한 nodelist 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-202">Or create a nodelist file for **charmrun**.</span></span>
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. <span data-ttu-id="e7e25-203">실행 **charmrun** hello nodelist 파일의 반환 상태를 가져오고 hello 끝 hello nodelist 파일을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-203">Run **charmrun** with hello nodelist file, get its return status, and remove hello nodelist file at hello end.</span></span>
   
   <span data-ttu-id="e7e25-204">${CCP_NUMCPUS}는 hello HPC Pack 헤드 노드에서 설정한 다른 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-204">${CCP_NUMCPUS} is another environment variable set by hello HPC Pack head node.</span></span> <span data-ttu-id="e7e25-205">Hello toothis 작업에 할당 된 총 코어 수를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-205">It stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="e7e25-206">사용할 수 프로세스 toospecify hello 수 charmrun에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-206">We use it toospecify hello number of processes for charmrun.</span></span>
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. <span data-ttu-id="e7e25-207">Hello로 종료 **charmrun** 상태를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-207">Exit with hello **charmrun** return status.</span></span>
   
   ```
   exit ${RTNSTS}
   ```

<span data-ttu-id="e7e25-208">다음은 어떤 hello 스크립트에서 생성 되는 hello nodelist 파일의 hello 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-208">Following is hello information in hello nodelist file, which hello script generates:</span></span>

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

<span data-ttu-id="e7e25-209">예:</span><span class="sxs-lookup"><span data-stu-id="e7e25-209">For example:</span></span>

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a><span data-ttu-id="e7e25-210">NAMD 작업 제출</span><span class="sxs-lookup"><span data-stu-id="e7e25-210">Submit a NAMD job</span></span>
<span data-ttu-id="e7e25-211">이제 준비 toosubmit NAMD HPC 클러스터 관리자에서 작업 하려고합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-211">Now you are ready toosubmit a NAMD job in HPC Cluster Manager.</span></span>

1. <span data-ttu-id="e7e25-212">Tooyour 클러스터 헤드 노드를 연결 하 고 HPC 클러스터 관리자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-212">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="e7e25-213">**리소스 관리**, hello Linux 계산 노드 hello에 있는지 확인 하세요 **온라인** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-213">In **Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="e7e25-214">온라인 상태가 아닌 경우 노드를 선택하고 **온라인 상태로 전환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-214">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="e7e25-215">**작업 관리**에서 **새 작업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-215">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="e7e25-216">작업 이름(예: *hpccharmrun*)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-216">Enter a name for job such as *hpccharmrun*.</span></span>
   
   ![새 HPC 작업][namd_job]
5. <span data-ttu-id="e7e25-218">Hello에 **작업 세부 정보** 페이지의 **작업 리소스**, hello 유형의 리소스 선택 **노드** 및 집합 hello **최소** too3 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-218">On hello **Job Details** page, under **Job Resources**, select hello type of resource as **Node** and set hello **Minimum** too3.</span></span> <span data-ttu-id="e7e25-219">를 3 개의 Linux 노드에서 hello 작업 실행 및 각 노드에 4 개의 코어입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-219">, we run hello job on three Linux nodes and each node has four cores.</span></span>
   
   ![작업 리소스][job_resources]
6. <span data-ttu-id="e7e25-221">클릭 **작업 편집** 왼쪽된 탐색 영역 hello와 클릭 **추가** tooadd 작업 toohello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-221">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span>    
7. <span data-ttu-id="e7e25-222">Hello에 **작업 세부 정보 및 리디렉션된 I/O 모드** 페이지에서 다음 값에는 집합 hello:</span><span class="sxs-lookup"><span data-stu-id="e7e25-222">On hello **Task Details and I/O Redirection** page, set hello following values:</span></span>
   
   * <span data-ttu-id="e7e25-223">**명령줄** -
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span><span class="sxs-lookup"><span data-stu-id="e7e25-223">**Command line** -
`/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span></span>
     
     > [!TIP]
     > <span data-ttu-id="e7e25-224">hello이 명령줄은 줄 바꿈 없이 단일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-224">hello preceding command line is a single command without line breaks.</span></span> <span data-ttu-id="e7e25-225">여러 줄 아래에 tooappear 래핑하 **명령줄**합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-225">It wraps tooappear on several lines under **Command line**.</span></span>
     > 
     > 
   * <span data-ttu-id="e7e25-226">**작업 디렉터리** - /namd2</span><span class="sxs-lookup"><span data-stu-id="e7e25-226">**Working directory** - /namd2</span></span>
   * <span data-ttu-id="e7e25-227">**최소** - 3</span><span class="sxs-lookup"><span data-stu-id="e7e25-227">**Minimum** - 3</span></span>
     
     ![태스크 세부 정보][task_details]
     
     > [!NOTE]
     > <span data-ttu-id="e7e25-229">여기에서 설정한 hello 작업 디렉터리 때문에 **charmrun** toonavigate toohello 시도 각 노드에서 동일한 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-229">You set hello working directory here because **charmrun** tries toonavigate toohello same working directory on each node.</span></span> <span data-ttu-id="e7e25-230">Hello 작업 디렉터리 설정 되지 않은 HPC 팩 hello Linux 노드 중 하나에서 생성 하는 임의로 지정 된 폴더에 hello 명령을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-230">If hello working directory isn't set, HPC Pack starts hello command in a randomly named folder created on one of hello Linux nodes.</span></span> <span data-ttu-id="e7e25-231">이 인해 hello hello에 다음 오류가 다른 노드에: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid이이 문제를 hello 작업 디렉터리와 모든 노드에 액세스할 수 있는 폴더 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-231">This causes hello following error on hello other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid this problem, specify a folder path that can be accessed by all nodes as hello working directory.</span></span>
     > 
     > 
8. <span data-ttu-id="e7e25-232">클릭 **확인** 클릭 하 고 **전송** toorun이이 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-232">Click **OK** and then click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="e7e25-233">HPC Pack 기본적으로 현재 로그온 한 사용자 계정으로 hello 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-233">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="e7e25-234">대화 상자 변수 tooenter hello 사용자 이름 및 암호 클릭 한 후 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-234">A dialog box might prompt you tooenter hello user name and password after you click **Submit**.</span></span>
   
   ![작업 자격 증명][creds]
   
   <span data-ttu-id="e7e25-236">어떤 조건 HPC Pack 하기 전에 입력 하 고이 대화 상자를 표시 하지 않는 hello 사용자 정보를 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-236">Under some conditions, HPC Pack remembers hello user information you input before and doesn't show this dialog box.</span></span> <span data-ttu-id="e7e25-237">다시 표시 하 고 hello 다음 명령 프롬프트에서 명령을 입력 한 다음 hello 작업을 제출 하는 HPC Pack toomake 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-237">toomake HPC Pack show it again, enter hello following command at a Command Prompt and then submit hello job.</span></span>
   
   ```command
   hpccred delcreds
   ```
9. <span data-ttu-id="e7e25-238">hello 작업은 몇 분 toofinish 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-238">hello job takes several minutes toofinish.</span></span>
10. <span data-ttu-id="e7e25-239">Hello 작업 로그에서 찾을 \\ <headnodeName>\Namd\namd2\namd2_hpccharmrun.log 및 hello에 대 한 출력 파일에 \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span><span class="sxs-lookup"><span data-stu-id="e7e25-239">Find hello job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and hello output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span></span>
11. <span data-ttu-id="e7e25-240">필요에 따라 VMD tooview 작업 결과 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-240">Optionally, start VMD tooview your job results.</span></span> <span data-ttu-id="e7e25-241">hello hello NAMD 출력 파일 (이 경우 물 범위의 ubiquitin 단백질 molecule)를 시각화 하는 단계는이 문서의 hello 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e25-241">hello steps for visualizing hello NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond hello scope of this article.</span></span> <span data-ttu-id="e7e25-242">자세한 내용은 [NAMD 자습서](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7e25-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span></span>
    
    ![작업 결과][vmd_view]

## <a name="sample-files"></a><span data-ttu-id="e7e25-244">샘플 파일</span><span class="sxs-lookup"><span data-stu-id="e7e25-244">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="e7e25-245">PowerShell 스크립트를 통한 클러스터 배포용 샘플 XML 구성 파일</span><span class="sxs-lookup"><span data-stu-id="e7e25-245">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>    
```

### <a name="sample-credxml-file"></a><span data-ttu-id="e7e25-246">샘플 cred.xml 파일</span><span class="sxs-lookup"><span data-stu-id="e7e25-246">Sample cred.xml file</span></span>
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

### <a name="sample-hpccharmrunsh-script"></a><span data-ttu-id="e7e25-247">샘플 hpccharmrun.sh 스크립트</span><span class="sxs-lookup"><span data-stu-id="e7e25-247">Sample hpccharmrun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
