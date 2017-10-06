---
title: "aaaRun 별-Linux Vm에서 HPC Pack을 사용한 CCM + | Microsoft Docs"
description: "Azure에서 Microsoft HPC Pack 클러스터를 배포하고 RDMA 네트워크 간의 여러 Linux 계산 노드에서 STAR-CCM+ 작업을 실행합니다."
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="e2a23-103">Azure의 Linux RDMA 클러스터에서 Microsoft HPC 팩으로 STAR-CCM+ 실행</span><span class="sxs-lookup"><span data-stu-id="e2a23-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="e2a23-104">이 문서에서는 Azure와 실행에 toodeploy Microsoft HPC Pack 클러스터 어떻게는 [CD adapco 별-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) InfiniBand와 상호 연결 되는 여러 Linux 계산 노드에서 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-104">This article shows you how toodeploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="e2a23-105">Microsoft HPC Pack 기능 toorun 다양 한 대규모 HPC 및 Microsoft Azure 가상 컴퓨터의 클러스터에서 MPI 응용 프로그램을 포함 하 여 병렬 응용 프로그램을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-105">Microsoft HPC Pack provides features toorun a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="e2a23-106">HPC 팩은 HPC 팩 클러스터에 배포된 Linux 계산 노드 VM에서 Linux HPC 응용 프로그램의 실행도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="e2a23-107">소개 toousing Linux 계산 노드 HPC Pack을 사용한, 참조 [Azure에서 HPC Pack 클러스터에서 계산 노드 Linux 시작](hpcpack-cluster.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-107">For an introduction toousing Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="set-up-an-hpc-pack-cluster"></a><span data-ttu-id="e2a23-108">HPC 팩 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="e2a23-108">Set up an HPC Pack cluster</span></span>
<span data-ttu-id="e2a23-109">Hello에서 hello HPC Pack IaaS 배포 스크립트를 다운로드 [다운로드 센터](https://www.microsoft.com/en-us/download/details.aspx?id=44949) 로컬로 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-109">Download hello HPC Pack IaaS deployment scripts from hello [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span></span>

<span data-ttu-id="e2a23-110">Azure PowerShell은 필수 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-110">Azure PowerShell is a prerequisite.</span></span> <span data-ttu-id="e2a23-111">로컬 컴퓨터에서 PowerShell 구성 되지 않은 경우 hello 문서를 참조 하세요 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-111">If PowerShell is not configured on your local machine, please read hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="e2a23-112">이 문서 작성 hello 시 hello Azure 마켓플레이스 (을 Azure에 대 한 hello InfiniBand 드라이버 포함)에서 hello Linux 이미지 SLES 12, CentOS 6.5 및 CentOS 7.1 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-112">At hello time of this writing, hello Linux images from hello Azure Marketplace (which contains hello InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span></span> <span data-ttu-id="e2a23-113">이 문서는 SLES 12 hello 사용을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-113">This article is based on hello usage of SLES 12.</span></span> <span data-ttu-id="e2a23-114">모든 Linux 이미지에서 지 원하는 HPC hello 마켓플레이스 tooretrieve hello 이름 hello 다음 PowerShell 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-114">tooretrieve hello name of all Linux images that support HPC in hello Marketplace, you can run hello following PowerShell command:</span></span>

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

<span data-ttu-id="e2a23-115">이러한 이미지 사용할 수 있는 및 이미지 이름 hello hello 위치를 나열 하는 hello 출력 (**ImageName**) toobe hello 배포 템플릿에 나중에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-115">hello output lists hello location in which these images are available and hello image name (**ImageName**) toobe used in hello deployment template later.</span></span>

<span data-ttu-id="e2a23-116">Hello 클러스터를 배포 하기 전에 해야 toobuild HPC Pack 배포 템플릿 파일.</span><span class="sxs-lookup"><span data-stu-id="e2a23-116">Before you deploy hello cluster, you have toobuild an HPC Pack deployment template file.</span></span> <span data-ttu-id="e2a23-117">작은 클러스터를 대상으로 하는 hello 헤드 노드 hello 도메인 컨트롤러일 되며 로컬 SQL 데이터베이스를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-117">Because we're targeting a small cluster, hello head node will be hello domain controller and host a local SQL database.</span></span>

<span data-ttu-id="e2a23-118">hello 다음 서식 파일은 헤드 노드를 배포, 라는 XML 파일을 만들고 **MyCluster.xml**, 및의 hello 값 바꾸기 **SubscriptionId**, **StorageAccount**,  **위치**, **VMName**, 및 **ServiceName** 기업과 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-118">hello following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace hello values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

<span data-ttu-id="e2a23-119">관리자 권한 명령 프롬프트에서 hello PowerShell 명령을 실행 하 여 hello 헤드 노드 만들기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-119">Start hello head-node creation by running hello PowerShell command in an elevated command prompt:</span></span>

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

<span data-ttu-id="e2a23-120">20 too30 분 hello 헤드 노드를 준비 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-120">After 20 too30 minutes, hello head node should be ready.</span></span> <span data-ttu-id="e2a23-121">Hello를 클릭 하 여 tooit hello Azure 포털에서에서 연결할 수 있습니다 **연결** hello 가상 컴퓨터의 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-121">You can connect tooit from hello Azure portal by clicking hello **Connect** icon of hello virtual machine.</span></span>

<span data-ttu-id="e2a23-122">결국 toofix hello DNS 전달자를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-122">You might eventually have toofix hello DNS forwarder.</span></span> <span data-ttu-id="e2a23-123">따라서 toodo DNS 관리자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-123">toodo so, start DNS Manager.</span></span>

1. <span data-ttu-id="e2a23-124">마우스 오른쪽 단추로 클릭 hello 서버 이름에 DNS 관리자를 선택 **속성**, hello를 클릭 한 다음 **전달자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-124">Right-click hello server name in DNS Manager, select **Properties**, and then click hello **Forwarders** tab.</span></span>
2. <span data-ttu-id="e2a23-125">Hello 클릭 **편집** tooremove 모든 전달자 단추를 선택한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-125">Click hello **Edit** button tooremove any forwarders, and then click **OK**.</span></span>
3. <span data-ttu-id="e2a23-126">해당 hello 있는지 확인 **없는 전달자를 사용할 수 있는 경우에 루트 힌트를 사용 하 여** 확인란을 선택한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-126">Make sure that hello **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span></span>

## <a name="set-up-linux-compute-nodes"></a><span data-ttu-id="e2a23-127">Linux 계산 노드 설정</span><span class="sxs-lookup"><span data-stu-id="e2a23-127">Set up Linux compute nodes</span></span>
<span data-ttu-id="e2a23-128">Hello를 사용 하 여 hello Linux 계산 노드를 배포할 toocreate hello 헤드 노드를 사용 하 여 동일한 배포 템플릿.</span><span class="sxs-lookup"><span data-stu-id="e2a23-128">You deploy hello Linux compute nodes by using hello same deployment template that you used toocreate hello head node.</span></span>

<span data-ttu-id="e2a23-129">Hello 파일 복사 **MyCluster.xml** 로컬 컴퓨터 toohello 헤드 노드 및 업데이트 hello **NodeCount** toodeploy 원하는 노드의 hello 번호로 태그 (< = 20).</span><span class="sxs-lookup"><span data-stu-id="e2a23-129">Copy hello file **MyCluster.xml** from your local machine toohello head node, and update hello **NodeCount** tag with hello number of nodes that you want toodeploy (<=20).</span></span> <span data-ttu-id="e2a23-130">때문일 신중 하 게 toohave Azure 할당량을 사용할 수 있는 충분 한 코어가 A9 인스턴스 각 구독에 코어 16 개를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-130">Be careful toohave enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span></span> <span data-ttu-id="e2a23-131">Toouse hello에 더 많은 Vm을 원하는 경우 A9 대신 A8 인스턴스 (8 코어)를 사용할 수 있습니다 동일한 예산 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-131">You can use A8 instances (8 cores) instead of A9 if you want toouse more VMs in hello same budget.</span></span>

<span data-ttu-id="e2a23-132">Hello 헤드 노드에서 hello HPC Pack IaaS 배포 스크립트를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-132">On hello head node, copy hello HPC Pack IaaS deployment scripts.</span></span>

<span data-ttu-id="e2a23-133">Hello Azure PowerShell 명령을 관리자 권한 명령 프롬프트에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-133">Run hello following Azure PowerShell commands in an elevated command prompt:</span></span>

1. <span data-ttu-id="e2a23-134">실행 **Add-azureaccount** tooconnect tooyour Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="e2a23-134">Run **Add-AzureAccount** tooconnect tooyour Azure subscription.</span></span>
2. <span data-ttu-id="e2a23-135">여러 구독이 있는 경우 실행 **Get-azuresubscription** toolist 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-135">If you have multiple subscriptions, run **Get-AzureSubscription** toolist them.</span></span>
3. <span data-ttu-id="e2a23-136">Hello를 실행 하 여 기본 구독 설정 **선택-SubscriptionName xxxx-기본** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-136">Set a default subscription by running hello **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span></span>
4. <span data-ttu-id="e2a23-137">실행 **.\New-HPCIaaSCluster.ps1-ConfigFile MyCluster.xml** toostart Linux 계산 노드를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** toostart deploying Linux compute nodes.</span></span>
   
   ![헤드 노드 배포 작업][hndeploy]

<span data-ttu-id="e2a23-139">Hello HPC 팩 클러스터 관리자 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-139">Open hello HPC Pack Cluster Manager tool.</span></span> <span data-ttu-id="e2a23-140">몇 분 후에 클러스터 계산 노드 목록에 Linux 계산 노드가 정기적으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span></span> <span data-ttu-id="e2a23-141">Hello 클래식 배포 모드에서 IaaS Vm 순차적으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-141">With hello classic deployment mode, IaaS VMs are created sequentially.</span></span> <span data-ttu-id="e2a23-142">따라서 노드 수가 hello 중요 한 경우 배포 된 모든 가져오기 상당한 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-142">So if hello number of nodes is important, getting them all deployed can take a significant amount of time.</span></span>

![HPC 팩 클러스터 관리자의 Linux 노드][clustermanager]

<span data-ttu-id="e2a23-144">이제 모든 노드가 실행 중에 hello 클러스터, 추가 인프라 설정 toomake가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-144">Now that all nodes are up and running in hello cluster, there are additional infrastructure settings toomake.</span></span>

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a><span data-ttu-id="e2a23-145">Windows 및 Linux 노드에 대한 Azure 파일 공유 설정</span><span class="sxs-lookup"><span data-stu-id="e2a23-145">Set up an Azure File share for Windows and Linux nodes</span></span>
<span data-ttu-id="e2a23-146">Hello Azure 파일 서비스 toostore 스크립트, 응용 프로그램 패키지 및 데이터 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-146">You can use hello Azure File service toostore scripts, application packages, and data files.</span></span> <span data-ttu-id="e2a23-147">Azure 파일은 Azure Blob 저장소를 영구 저장소로 사용하면서 CIFS 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span></span> <span data-ttu-id="e2a23-148">이 hello 가장 확장성이 뛰어난 솔루션을 아니라 hello 가장 간단한 하나 되 고 전용된 Vm 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-148">Be aware that this is not hello most scalable solution, but it is hello simplest one and doesn’t require dedicated VMs.</span></span>

<span data-ttu-id="e2a23-149">Hello hello 문서의 지침에 따라 Azure 파일 공유 만들기 [Windows에서 Azure 파일 저장소 시작](../../../storage/files/storage-dotnet-how-to-use-files.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-149">Create an Azure File share by following hello instructions in hello article [Get started with Azure File storage on Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="e2a23-150">사용자의 저장소 계정으로 hello 이름을 유지 **saname**, hello 파일 공유 이름으로 **sharename**, 및 hello 저장소 계정 키로 **sakey**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-150">Keep hello name of your storage account as **saname**, hello file share name as **sharename**, and hello storage account key as **sakey**.</span></span>

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a><span data-ttu-id="e2a23-151">Hello Azure 파일 공유 hello 헤드 노드에 탑재 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e2a23-151">Mount hello Azure File share on hello head node</span></span>
<span data-ttu-id="e2a23-152">관리자 권한 명령 프롬프트를 열고 hello 명령 toostore hello 자격 증명 hello 로컬 컴퓨터 자격 증명 모음에 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-152">Open an elevated command prompt and run hello following command toostore hello credentials in hello local machine vault:</span></span>

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

<span data-ttu-id="e2a23-153">그런 다음 toomount hello Azure 파일 공유를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-153">Then, toomount hello Azure File share, run:</span></span>

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a><span data-ttu-id="e2a23-154">Hello Azure 파일 공유 Linux 계산 노드에 탑재 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e2a23-154">Mount hello Azure File share on Linux compute nodes</span></span>
<span data-ttu-id="e2a23-155">HPC Pack과 함께 제공 되는 유용한 도구는 hello clusrun 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-155">One useful tool that comes with HPC Pack is hello clusrun tool.</span></span> <span data-ttu-id="e2a23-156">계산 노드 집합에 동일 명령이 명령줄 도구 toorun hello를 동시에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-156">You can use this command-line tool toorun hello same command simultaneously on a set of compute nodes.</span></span> <span data-ttu-id="e2a23-157">이 경우에이 클래스는 toomount hello Azure 파일 공유를 사용 하는 고 toosurvive 재부팅을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-157">In our case, it's used toomount hello Azure File share and persist it toosurvive reboots.</span></span>
<span data-ttu-id="e2a23-158">Hello 헤드 노드에서 관리자 권한 명령 프롬프트에서 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-158">In an elevated command prompt on hello head node, run hello following commands.</span></span>

<span data-ttu-id="e2a23-159">toocreate hello 탑재 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="e2a23-159">toocreate hello mount directory:</span></span>

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

<span data-ttu-id="e2a23-160">toomount hello Azure 파일 공유:</span><span class="sxs-lookup"><span data-stu-id="e2a23-160">toomount hello Azure File share:</span></span>

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

<span data-ttu-id="e2a23-161">toopersist hello 탑재 공유:</span><span class="sxs-lookup"><span data-stu-id="e2a23-161">toopersist hello mount share:</span></span>

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a><span data-ttu-id="e2a23-162">STAR-CCM+ 설치</span><span class="sxs-lookup"><span data-stu-id="e2a23-162">Install STAR-CCM+</span></span>
<span data-ttu-id="e2a23-163">Azure VM 인스턴스 A8 및 A9는 InfiniBand 지원 및 RDMA 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span></span> <span data-ttu-id="e2a23-164">이러한 기능을 사용 하는 hello 커널 드라이버는 Windows Server 2012 R2, SUSE 12, CentOS 6.5 및 CentOS 7.1 이미지 hello Azure 마켓플레이스를에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-164">hello kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in hello Azure Marketplace.</span></span> <span data-ttu-id="e2a23-165">Microsoft MPI 및 Intel MPI (5.x 릴리스)는 Azure에서 해당 드라이버를 지 hello 두 하는 MPI 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-165">Microsoft MPI and Intel MPI (release 5.x) are hello two MPI libraries that support those drivers in Azure.</span></span>

<span data-ttu-id="e2a23-166">CD-adapco STAR-CCM+ 릴리스 11.x 이상은 Intel MPI 버전 5.x와 함께 제공되므로 Azure에 대한 InfiniBand 지원이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span></span>

<span data-ttu-id="e2a23-167">Hello Linux64 가져오기 별-hello에서 CCM + 패키지 [CD adapco 포털](https://steve.cd-adapco.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-167">Get hello Linux64 STAR-CCM+ package from hello [CD-adapco portal](https://steve.cd-adapco.com).</span></span> <span data-ttu-id="e2a23-168">이 경우에는 혼합 정밀도의 버전 11.02.010을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-168">In our case, we used version 11.02.010 in mixed precision.</span></span>

<span data-ttu-id="e2a23-169">Hello에서 hello 헤드 노드 **/hpcdata** Azure 파일 공유, 라는 셸 스크립트를 만들고 **setupstarccm.sh** 콘텐츠를 다음 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-169">On hello head node, in hello **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with hello following content.</span></span> <span data-ttu-id="e2a23-170">각 계산 노드 tooset 별 구성에이 스크립트가 실행 될-CCM + 로컬로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-170">This script will be run on each compute node tooset up STAR-CCM+ locally.</span></span>

#### <a name="sample-setupstarcmsh-script"></a><span data-ttu-id="e2a23-171">샘플 setupstarcm.sh 스크립트</span><span class="sxs-lookup"><span data-stu-id="e2a23-171">Sample setupstarcm.sh script</span></span>
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
<span data-ttu-id="e2a23-172">이제 tooset 별을-CCM + 프로그램 모든 Linux에서 계산 노드, 관리자 권한 명령 프롬프트를 열고 및 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-172">Now, tooset up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run hello following command:</span></span>

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

<span data-ttu-id="e2a23-173">Hello 명령을 실행 하는 동안에 클러스터 관리자의 hello 열 지도 사용 하 여 hello CPU 사용량을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-173">While hello command is running, you can monitor hello CPU usage by using hello heat map of Cluster Manager.</span></span> <span data-ttu-id="e2a23-174">몇 분 후 모든 노드가 올바르게 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-174">After few minutes, all nodes should be correctly set up.</span></span>

## <a name="run-star-ccm-jobs"></a><span data-ttu-id="e2a23-175">STAR-CCM+ 작업 실행</span><span class="sxs-lookup"><span data-stu-id="e2a23-175">Run STAR-CCM+ jobs</span></span>
<span data-ttu-id="e2a23-176">HPC Pack 순서 toorun 별에에서 그 작업 스케줄러 기능에 사용 되-CCM + 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-176">HPC Pack is used for its job scheduler capabilities in order toorun STAR-CCM+ jobs.</span></span> <span data-ttu-id="e2a23-177">toodo, 사용 되는 toostart hello 작업 되 고 별표를 실행 하는 몇 가지 스크립트의 지원 hello 필요 म-CCM + 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-177">toodo so, we need hello support of a few scripts that are used toostart hello job and run STAR-CCM+.</span></span> <span data-ttu-id="e2a23-178">입력된 데이터 hello 편의 위해 첫 번째 hello Azure 파일 공유에 보관 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-178">hello input data is kept on hello Azure File share first for simplicity.</span></span>

<span data-ttu-id="e2a23-179">PowerShell 스크립트 뒤 hello가 사용 되는 tooqueue 별-CCM + 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-179">hello following PowerShell script is used tooqueue a STAR-CCM+ job.</span></span> <span data-ttu-id="e2a23-180">3가지 인수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-180">It takes three arguments:</span></span>

* <span data-ttu-id="e2a23-181">hello 모델 이름</span><span class="sxs-lookup"><span data-stu-id="e2a23-181">hello model name</span></span>
* <span data-ttu-id="e2a23-182">사용 되는 노드 toobe hello 수</span><span class="sxs-lookup"><span data-stu-id="e2a23-182">hello number of nodes toobe used</span></span>
* <span data-ttu-id="e2a23-183">hello 사용 되는 각 노드 toobe의 코어 수</span><span class="sxs-lookup"><span data-stu-id="e2a23-183">hello number of cores on each node toobe used</span></span>

<span data-ttu-id="e2a23-184">때문에 별-CCM + hello 메모리 대역폭을 채울 수 있는의 일반적으로 더 나은 toouse 당 코어 적은 계산 노드 및 새 노드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-184">Because STAR-CCM+ can fill hello memory bandwidth, it's usually better toouse fewer cores per compute nodes and add new nodes.</span></span> <span data-ttu-id="e2a23-185">노드당 코어 수를 정확 하 게 hello hello 프로세서 제품군 및 hello 상호 연결 속도에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-185">hello exact number of cores per node will depend on hello processor family and hello interconnect speed.</span></span>

<span data-ttu-id="e2a23-186">hello 노드 hello 작업에 대 한 단독으로 할당 되 고 다른 작업와 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-186">hello nodes are allocated exclusively for hello job and can’t be shared with other jobs.</span></span> <span data-ttu-id="e2a23-187">hello 작업 직접 MPI 작업으로 시작 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-187">hello job is not started as an MPI job directly.</span></span> <span data-ttu-id="e2a23-188">hello **runstarccm.sh** 셸 스크립트 hello MPI 시작 관리자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-188">hello **runstarccm.sh** shell script will start hello MPI launcher.</span></span>

<span data-ttu-id="e2a23-189">hello 입력 모델 및 hello **runstarccm.sh** hello에 스크립트 저장 **/hpcdata** 이전에 탑재 된 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-189">hello input model and hello **runstarccm.sh** script are stored in hello **/hpcdata** share that was previously mounted.</span></span>

<span data-ttu-id="e2a23-190">로그 파일 hello 작업 ID를 가진 명명 되 고 hello에 저장 된 **/hpcdata 공유**, 스타 hello 함께-CCM + 출력 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-190">Log files are named with hello job ID and are stored in hello **/hpcdata share**, along with hello STAR-CCM+ output files.</span></span>

#### <a name="sample-submitstarccmjobps1-script"></a><span data-ttu-id="e2a23-191">샘플 SubmitStarccmJob.ps1 스크립트</span><span class="sxs-lookup"><span data-stu-id="e2a23-191">Sample SubmitStarccmJob.ps1 script</span></span>
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
<span data-ttu-id="e2a23-192">**runner.java** 를 원하는 STAR-CCM+ java 모델 시작 관리자와 로깅 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span></span>

#### <a name="sample-runstarccmsh-script"></a><span data-ttu-id="e2a23-193">샘플 runstarccm.sh 스크립트</span><span class="sxs-lookup"><span data-stu-id="e2a23-193">Sample runstarccm.sh script</span></span>
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

<span data-ttu-id="e2a23-194">이 테스트에서는 Power-On-Demand 라이선스 토큰을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-194">In our test, we used a Power-On-Demand license token.</span></span> <span data-ttu-id="e2a23-195">이 토큰에 대 한 tooset hello 있는 **$CDLMD_LICENSE_FILE** 환경 변수 너무 **1999@flex.cd-adapco.com**  hello에 대 한 hello 키를 **-podkey** hello 명령줄 옵션 .</span><span class="sxs-lookup"><span data-stu-id="e2a23-195">For that token, you have tooset hello **$CDLMD_LICENSE_FILE** environment variable too**1999@flex.cd-adapco.com** and hello key in hello **-podkey** option of hello command line.</span></span>

<span data-ttu-id="e2a23-196">일부 초기화 된 후 hello 스크립트-에서 추출 hello **$CCP_NODES_CORES** HPC Pack 설정-환경 변수를 사용 하 여 MPI launcher hello는 hostfile 노드 toobuild 목록이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-196">After some initialization, hello script extracts--from hello **$CCP_NODES_CORES** environment variables that HPC Pack set--hello list of nodes toobuild a hostfile that hello MPI launcher uses.</span></span> <span data-ttu-id="e2a23-197">이 hostfile hello hello 작업을 한 줄에 하나의 이름에 사용 되는 계산 노드 이름 목록이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-197">This hostfile will contain hello list of compute node names that are used for hello job, one name per line.</span></span>

<span data-ttu-id="e2a23-198">hello 형식의 **$CCP_NODES_CORES** 이 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-198">hello format of **$CCP_NODES_CORES** follows this pattern:</span></span>

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

<span data-ttu-id="e2a23-199">여기서,</span><span class="sxs-lookup"><span data-stu-id="e2a23-199">Where:</span></span>

* <span data-ttu-id="e2a23-200">`<Number of nodes>`hello toothis 작업에 할당 된 노드 수가입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-200">`<Number of nodes>` is hello number of nodes allocated toothis job.</span></span>
* <span data-ttu-id="e2a23-201">`<Name of node_n_...>`hello toothis 작업에 할당 된 각 노드 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-201">`<Name of node_n_...>` is hello name of each node allocated toothis job.</span></span>
* <span data-ttu-id="e2a23-202">`<Cores of node_n_...>`hello hello 노드의 toothis 작업에 할당 된 코어 수가입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-202">`<Cores of node_n_...>` is hello number of cores on hello node allocated toothis job.</span></span>

<span data-ttu-id="e2a23-203">그러나 코어 수가 hello (**$NBCORES**) 노드 수에 따라 계산 된 hello 이기도 (**$NBNODES**) hello 노드당 코어 수 및 (매개 변수로 제공 **$NBCORESPERNODE**).</span><span class="sxs-lookup"><span data-stu-id="e2a23-203">hello number of cores (**$NBCORES**) is also calculated based on hello number of nodes (**$NBNODES**) and hello number of cores per node (provided as parameter **$NBCORESPERNODE**).</span></span>

<span data-ttu-id="e2a23-204">Hello MPI 옵션 hello Azure에서 MPI Intel 함께 사용 되는 것과 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-204">For hello MPI options, hello ones that are used with Intel MPI on Azure are:</span></span>

* <span data-ttu-id="e2a23-205">`-mpi intel`Intel MPI toospecify 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-205">`-mpi intel` toospecify Intel MPI.</span></span>
* <span data-ttu-id="e2a23-206">`-fabric UDAPL`Azure의 InfiniBand 동사를 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-206">`-fabric UDAPL` toouse Azure InfiniBand verbs.</span></span>
* <span data-ttu-id="e2a23-207">`-cpubind bandwidth,v`별이 있는 MPI에 대 한 toooptimize 대역폭-CCM + 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-207">`-cpubind bandwidth,v` toooptimize bandwidth for MPI with STAR-CCM+.</span></span>
* <span data-ttu-id="e2a23-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`Azure의 InfiniBand toomake Intel MPI 작업 및 tooset hello 필요한 노드당 코어 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` toomake Intel MPI work with Azure InfiniBand, and tooset hello required number of cores per node.</span></span>
* <span data-ttu-id="e2a23-209">`-batch`toostart 별-CCM + 일괄 처리 모드에서 ui 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-209">`-batch` toostart STAR-CCM+ in batch mode with no UI.</span></span>

<span data-ttu-id="e2a23-210">마지막으로, toostart 작업을 된 노드가 실행 중 이며 클러스터 관리자에서 온라인 상태 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-210">Finally, toostart a job, make sure that your nodes are up and running and are online in Cluster Manager.</span></span> <span data-ttu-id="e2a23-211">그런 다음 PowerShell 명령 창에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-211">Then from a PowerShell command prompt, run this:</span></span>

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a><span data-ttu-id="e2a23-212">노드 중지</span><span class="sxs-lookup"><span data-stu-id="e2a23-212">Stop nodes</span></span>
<span data-ttu-id="e2a23-213">나중에 테스트를 마친 후 HPC 팩 PowerShell 명령을 toostop 다음 hello를 사용 하 고 노드를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-213">Later on, after you're done with your tests, you can use hello following HPC Pack PowerShell commands toostop and start nodes:</span></span>

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a><span data-ttu-id="e2a23-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e2a23-214">Next steps</span></span>
<span data-ttu-id="e2a23-215">다른 Linux 워크로드를 실행해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e2a23-215">Try running other Linux workloads.</span></span> <span data-ttu-id="e2a23-216">예를 들어 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2a23-216">For example, see:</span></span>

* [<span data-ttu-id="e2a23-217">Azure의 Linux 계산 노드에서 Microsoft HPC 팩을 사용하여 NAMD 실행</span><span class="sxs-lookup"><span data-stu-id="e2a23-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
* [<span data-ttu-id="e2a23-218">Azure의 Linux RDMA 클러스터에서 Microsoft HPC 팩을 사용하여 OpenFOAM 실행</span><span class="sxs-lookup"><span data-stu-id="e2a23-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
