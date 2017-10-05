---
title: "Linux VM에서 HPC 팩으로 STAR-CCM+ 실행 | Microsoft Docs"
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
ms.openlocfilehash: b45fcfb981287035da02fda62eaf5f9436ec2379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="b3161-103">Azure의 Linux RDMA 클러스터에서 Microsoft HPC 팩으로 STAR-CCM+ 실행</span><span class="sxs-lookup"><span data-stu-id="b3161-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="b3161-104">이 문서에서는 Azure에 Microsoft HPC 팩 클러스터를 배포하고 InfiniBand와 상호 연결된 여러 Linux 계산 노드에서 [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) 작업을 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-104">This article shows you how to deploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="b3161-105">Microsoft HPC 팩에서는 MPI 응용 프로그램을 포함한 다양한 대규모 HPC 및 병렬 응용 프로그램을 Microsoft Azure 가상 컴퓨터의 클러스터에서 실행하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-105">Microsoft HPC Pack provides features to run a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="b3161-106">HPC 팩은 HPC 팩 클러스터에 배포된 Linux 계산 노드 VM에서 Linux HPC 응용 프로그램의 실행도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="b3161-107">HPC 팩으로 Linux 계산 노드 사용에 대한 소개는 [Azure에서 HPC 팩 클러스터의 Linux 계산 노드 시작](hpcpack-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3161-107">For an introduction to using Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="set-up-an-hpc-pack-cluster"></a><span data-ttu-id="b3161-108">HPC 팩 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="b3161-108">Set up an HPC Pack cluster</span></span>
<span data-ttu-id="b3161-109">[다운로드 센터](https://www.microsoft.com/en-us/download/details.aspx?id=44949)에서 HPC 팩 IaaS 배포 스크립트를 다운로드하고 로컬로 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-109">Download the HPC Pack IaaS deployment scripts from the [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span></span>

<span data-ttu-id="b3161-110">Azure PowerShell은 필수 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-110">Azure PowerShell is a prerequisite.</span></span> <span data-ttu-id="b3161-111">PowerShell이 로컬 컴퓨터에 구성되지 않은 경우 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3161-111">If PowerShell is not configured on your local machine, please read the article [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="b3161-112">이 문서를 작성할 당시 Azure 마켓플레이스의 Linux 이미지(Azure용 InfiniBand 포함)는 SLES 12, CentOS 6.5, CentOS 7.1용입니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-112">At the time of this writing, the Linux images from the Azure Marketplace (which contains the InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span></span> <span data-ttu-id="b3161-113">이 문서는 SLES 12 사용을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-113">This article is based on the usage of SLES 12.</span></span> <span data-ttu-id="b3161-114">마켓플레이스에서 HPC를 지원하는 모든 Linux 이미지의 이름을 검색하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-114">To retrieve the name of all Linux images that support HPC in the Marketplace, you can run the following PowerShell command:</span></span>

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

<span data-ttu-id="b3161-115">출력에는 이러한 이미지를 사용할 수 있는 위치와 향후 배포 템플릿에 사용할 이미지 이름(**ImageName**)이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-115">The output lists the location in which these images are available and the image name (**ImageName**) to be used in the deployment template later.</span></span>

<span data-ttu-id="b3161-116">클러스터를 배포하기 전에 HPC 팩 배포 템플릿 파일을 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-116">Before you deploy the cluster, you have to build an HPC Pack deployment template file.</span></span> <span data-ttu-id="b3161-117">소규모 클러스터를 대상으로 하기 때문에 헤드 노드는 도메인 컨트롤러가 되며 로컬 SQL 데이터베이스를 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-117">Because we're targeting a small cluster, the head node will be the domain controller and host a local SQL database.</span></span>

<span data-ttu-id="b3161-118">아래 템플릿은 이러한 헤드 노드를 배포하고 **MyCluster.xml**이라는 XML 파일을 만들고 **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, **ServiceName** 값을 사용하는 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-118">The following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace the values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span></span>

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

<span data-ttu-id="b3161-119">관리자 권한 명령 프롬프트에서 PowerShell 명령을 실행하여 헤드 노드 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-119">Start the head-node creation by running the PowerShell command in an elevated command prompt:</span></span>

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

<span data-ttu-id="b3161-120">20~30분 후에 헤드 노드가 준비됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-120">After 20 to 30 minutes, the head node should be ready.</span></span> <span data-ttu-id="b3161-121">가상 컴퓨터의 **연결** 아이콘을 클릭하여 Azure 포털에서 헤드 노드에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-121">You can connect to it from the Azure portal by clicking the **Connect** icon of the virtual machine.</span></span>

<span data-ttu-id="b3161-122">최종적으로 DNS 전달자를 수정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-122">You might eventually have to fix the DNS forwarder.</span></span> <span data-ttu-id="b3161-123">이 작업을 위해 DNS 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-123">To do so, start DNS Manager.</span></span>

1. <span data-ttu-id="b3161-124">DNS 관리자에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 **속성**, **전달자** 탭을 차례대로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-124">Right-click the server name in DNS Manager, select **Properties**, and then click the **Forwarders** tab.</span></span>
2. <span data-ttu-id="b3161-125">**편집** 단추를 클릭하여 모든 전달자를 제거한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-125">Click the **Edit** button to remove any forwarders, and then click **OK**.</span></span>
3. <span data-ttu-id="b3161-126">**전달자를 사용할 수 없으면 루트 힌트 사용** 확인란이 선택되어 있는지 확인하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-126">Make sure that the **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span></span>

## <a name="set-up-linux-compute-nodes"></a><span data-ttu-id="b3161-127">Linux 계산 노드 설정</span><span class="sxs-lookup"><span data-stu-id="b3161-127">Set up Linux compute nodes</span></span>
<span data-ttu-id="b3161-128">헤드 노드를 만들 때 사용한 것과 동일한 배포 템플릿을 사용하여 Linux 계산 노드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-128">You deploy the Linux compute nodes by using the same deployment template that you used to create the head node.</span></span>

<span data-ttu-id="b3161-129">로컬 컴퓨터에서 헤드 노드로 **MyCluster.xml** 파일을 복사하고 배포하려는 노드 수(20 이하)로 **NodeCount** 태그를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-129">Copy the file **MyCluster.xml** from your local machine to the head node, and update the **NodeCount** tag with the number of nodes that you want to deploy (<=20).</span></span> <span data-ttu-id="b3161-130">구독에서 각 A9 인스턴스는 16개의 코어를 사용하므로 Azure 할당량에 사용할 수 있는 코어가 충분해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-130">Be careful to have enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span></span> <span data-ttu-id="b3161-131">동일한 예산으로 더 많은 VM을 사용하려는 경우 A9 대신 A8 인스턴스(8개 코어)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-131">You can use A8 instances (8 cores) instead of A9 if you want to use more VMs in the same budget.</span></span>

<span data-ttu-id="b3161-132">헤드 노드에서 HPC 팩 IaaS 배포 스크립트를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-132">On the head node, copy the HPC Pack IaaS deployment scripts.</span></span>

<span data-ttu-id="b3161-133">관리자 권한 명령 프롬프트에서 다음의 Azure PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-133">Run the following Azure PowerShell commands in an elevated command prompt:</span></span>

1. <span data-ttu-id="b3161-134">**Add-AzureAccount** 를 실행하여 Azure 구독을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-134">Run **Add-AzureAccount** to connect to your Azure subscription.</span></span>
2. <span data-ttu-id="b3161-135">여러 구독이 있는 경우 **Get-AzureSubscription** 을 실행하여 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-135">If you have multiple subscriptions, run **Get-AzureSubscription** to list them.</span></span>
3. <span data-ttu-id="b3161-136">**Select-AzureSubscription -SubscriptionName xxxx -Default** 명령을 실행하여 기본 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-136">Set a default subscription by running the **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span></span>
4. <span data-ttu-id="b3161-137">**.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml**을 실행하여 Linux 계산 노드 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** to start deploying Linux compute nodes.</span></span>
   
   ![헤드 노드 배포 작업][hndeploy]

<span data-ttu-id="b3161-139">HPC 팩 클러스터 관리자 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-139">Open the HPC Pack Cluster Manager tool.</span></span> <span data-ttu-id="b3161-140">몇 분 후에 클러스터 계산 노드 목록에 Linux 계산 노드가 정기적으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span></span> <span data-ttu-id="b3161-141">클래식 배포 모드에서는 IaaS VM이 순차적으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-141">With the classic deployment mode, IaaS VMs are created sequentially.</span></span> <span data-ttu-id="b3161-142">따라서 노드 수가 중요할 경우 전체를 배포하려면 많은 시간이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-142">So if the number of nodes is important, getting them all deployed can take a significant amount of time.</span></span>

![HPC 팩 클러스터 관리자의 Linux 노드][clustermanager]

<span data-ttu-id="b3161-144">이제 모든 노드가 클러스터에서 실행 중이며 추가 인프라 설정을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-144">Now that all nodes are up and running in the cluster, there are additional infrastructure settings to make.</span></span>

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a><span data-ttu-id="b3161-145">Windows 및 Linux 노드에 대한 Azure 파일 공유 설정</span><span class="sxs-lookup"><span data-stu-id="b3161-145">Set up an Azure File share for Windows and Linux nodes</span></span>
<span data-ttu-id="b3161-146">Azure 파일 서비스를 사용하여 스크립트, 응용 프로그램 패키지, 데이터 파일을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-146">You can use the Azure File service to store scripts, application packages, and data files.</span></span> <span data-ttu-id="b3161-147">Azure 파일은 Azure Blob 저장소를 영구 저장소로 사용하면서 CIFS 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span></span> <span data-ttu-id="b3161-148">이것이 가장 확장성 있는 솔루션은 아니지만 가장 간단하며 전용 VM이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-148">Be aware that this is not the most scalable solution, but it is the simplest one and doesn’t require dedicated VMs.</span></span>

<span data-ttu-id="b3161-149">[Windows에서 Azure File storage 시작](../../../storage/files/storage-dotnet-how-to-use-files.md) 문서의 지침에 따라 Azure 파일 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-149">Create an Azure File share by following the instructions in the article [Get started with Azure File storage on Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="b3161-150">저장소 계정 이름 **saname**, 파일 공유 이름 **sharename** 및 저장소 계정 키 **sakey**를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-150">Keep the name of your storage account as **saname**, the file share name as **sharename**, and the storage account key as **sakey**.</span></span>

### <a name="mount-the-azure-file-share-on-the-head-node"></a><span data-ttu-id="b3161-151">헤드 노드에 Azure 파일 공유 탑재</span><span class="sxs-lookup"><span data-stu-id="b3161-151">Mount the Azure File share on the head node</span></span>
<span data-ttu-id="b3161-152">로컬 컴퓨터 자격 증명 모음에 자격 증명을 저장하려면 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-152">Open an elevated command prompt and run the following command to store the credentials in the local machine vault:</span></span>

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

<span data-ttu-id="b3161-153">그런 다음 Azure 파일 공유를 탑재하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-153">Then, to mount the Azure File share, run:</span></span>

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-the-azure-file-share-on-linux-compute-nodes"></a><span data-ttu-id="b3161-154">Linux 계산 노드에 Azure 파일 공유 탑재</span><span class="sxs-lookup"><span data-stu-id="b3161-154">Mount the Azure File share on Linux compute nodes</span></span>
<span data-ttu-id="b3161-155">HPC 팩에는 clusrun이라는 유용한 도구가 기본 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-155">One useful tool that comes with HPC Pack is the clusrun tool.</span></span> <span data-ttu-id="b3161-156">이 명령줄 도구를 사용하여 계산 노드 집합에서 동일한 명령을 동시에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-156">You can use this command-line tool to run the same command simultaneously on a set of compute nodes.</span></span> <span data-ttu-id="b3161-157">여기서는 Azure 파일 공유를 탑재하고 다시 부팅 후에도 탑재 공유를 유지하기 위해 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-157">In our case, it's used to mount the Azure File share and persist it to survive reboots.</span></span>
<span data-ttu-id="b3161-158">헤드 노드의 관리자 권한 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-158">In an elevated command prompt on the head node, run the following commands.</span></span>

<span data-ttu-id="b3161-159">탑재 디렉터리를 만들려면</span><span class="sxs-lookup"><span data-stu-id="b3161-159">To create the mount directory:</span></span>

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

<span data-ttu-id="b3161-160">Azure 파일 공유를 탑재하려면</span><span class="sxs-lookup"><span data-stu-id="b3161-160">To mount the Azure File share:</span></span>

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

<span data-ttu-id="b3161-161">탑재 공유를 유지하려면</span><span class="sxs-lookup"><span data-stu-id="b3161-161">To persist the mount share:</span></span>

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a><span data-ttu-id="b3161-162">STAR-CCM+ 설치</span><span class="sxs-lookup"><span data-stu-id="b3161-162">Install STAR-CCM+</span></span>
<span data-ttu-id="b3161-163">Azure VM 인스턴스 A8 및 A9는 InfiniBand 지원 및 RDMA 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span></span> <span data-ttu-id="b3161-164">이러한 기능을 구현하는 커널 드라이버는 Azure 마켓플레이스에서 Windows Server 2012 R2, SUSE 12, CentOS 6.5, CentOS 7.1 이미지에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-164">The kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in the Azure Marketplace.</span></span> <span data-ttu-id="b3161-165">Microsoft MPI 및 Intel MPI(릴리스 5.x)는 Azure에서 해당 드라이버를 지원하는 두 MPI 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-165">Microsoft MPI and Intel MPI (release 5.x) are the two MPI libraries that support those drivers in Azure.</span></span>

<span data-ttu-id="b3161-166">CD-adapco STAR-CCM+ 릴리스 11.x 이상은 Intel MPI 버전 5.x와 함께 제공되므로 Azure에 대한 InfiniBand 지원이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span></span>

<span data-ttu-id="b3161-167">[CD-adapco 포털](https://steve.cd-adapco.com)에서 Linux64 STAR-CCM+ 패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-167">Get the Linux64 STAR-CCM+ package from the [CD-adapco portal](https://steve.cd-adapco.com).</span></span> <span data-ttu-id="b3161-168">이 경우에는 혼합 정밀도의 버전 11.02.010을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-168">In our case, we used version 11.02.010 in mixed precision.</span></span>

<span data-ttu-id="b3161-169">헤드 노드의 **/hpcdata** Azure 파일 공유에서 다음 내용이 포함된 **setupstarccm.sh**라는 셸 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-169">On the head node, in the **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with the following content.</span></span> <span data-ttu-id="b3161-170">이 스크립트는 STAR-CCM+를 로컬로 설정하기 위해 각 계산 노드에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-170">This script will be run on each compute node to set up STAR-CCM+ locally.</span></span>

#### <a name="sample-setupstarcmsh-script"></a><span data-ttu-id="b3161-171">샘플 setupstarcm.sh 스크립트</span><span class="sxs-lookup"><span data-stu-id="b3161-171">Sample setupstarcm.sh script</span></span>
```
    #!/bin/bash
    # setupstarcm.sh to set up STAR-CCM+ locally

    # Create the CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy the STAR-CCM package from the file share to the local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract the package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without the FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
<span data-ttu-id="b3161-172">이제 모든 Linux 계산 노드에 STAR-CCM+를 설정하기 위해 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-172">Now, to set up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run the following command:</span></span>

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

<span data-ttu-id="b3161-173">명령이 실행되는 동안 클러스터 관리자의 열 지도를 사용하여 CPU 사용량을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-173">While the command is running, you can monitor the CPU usage by using the heat map of Cluster Manager.</span></span> <span data-ttu-id="b3161-174">몇 분 후 모든 노드가 올바르게 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-174">After few minutes, all nodes should be correctly set up.</span></span>

## <a name="run-star-ccm-jobs"></a><span data-ttu-id="b3161-175">STAR-CCM+ 작업 실행</span><span class="sxs-lookup"><span data-stu-id="b3161-175">Run STAR-CCM+ jobs</span></span>
<span data-ttu-id="b3161-176">HPC 팩은 STAR-CCM+ 작업을 실행하기 위한 작업 스케줄러 기능에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-176">HPC Pack is used for its job scheduler capabilities in order to run STAR-CCM+ jobs.</span></span> <span data-ttu-id="b3161-177">이렇게 하려면 작업을 시작하고 STAR-CCM+를 실행하는데 사용되는 몇 가지 스크립트에 대한 지원이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-177">To do so, we need the support of a few scripts that are used to start the job and run STAR-CCM+.</span></span> <span data-ttu-id="b3161-178">입력 데이터는 편의상 Azure 파일 공유에 먼저 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-178">The input data is kept on the Azure File share first for simplicity.</span></span>

<span data-ttu-id="b3161-179">다음 PowerShell 스크립트는 STAR-CCM+ 작업을 큐에 대기시키는 데 사용하며</span><span class="sxs-lookup"><span data-stu-id="b3161-179">The following PowerShell script is used to queue a STAR-CCM+ job.</span></span> <span data-ttu-id="b3161-180">3가지 인수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-180">It takes three arguments:</span></span>

* <span data-ttu-id="b3161-181">모델 이름</span><span class="sxs-lookup"><span data-stu-id="b3161-181">The model name</span></span>
* <span data-ttu-id="b3161-182">사용할 노드 수</span><span class="sxs-lookup"><span data-stu-id="b3161-182">The number of nodes to be used</span></span>
* <span data-ttu-id="b3161-183">각 노드에 사용할 코어 수</span><span class="sxs-lookup"><span data-stu-id="b3161-183">The number of cores on each node to be used</span></span>

<span data-ttu-id="b3161-184">STAR-CCM+는 메모리 대역폭을 초과할 수 있으므로 계산 노드당 적은 코어를 사용하고 새 노드를 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-184">Because STAR-CCM+ can fill the memory bandwidth, it's usually better to use fewer cores per compute nodes and add new nodes.</span></span> <span data-ttu-id="b3161-185">정확한 노드당 코어 수는 프로세서 제품군 및 상호 연결 속도에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-185">The exact number of cores per node will depend on the processor family and the interconnect speed.</span></span>

<span data-ttu-id="b3161-186">노드는 작업에 단독으로 할당되며 다른 작업과 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-186">The nodes are allocated exclusively for the job and can’t be shared with other jobs.</span></span> <span data-ttu-id="b3161-187">이 작업은 MPI 작업으로 직접 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-187">The job is not started as an MPI job directly.</span></span> <span data-ttu-id="b3161-188">**runstarccm.sh** 셸 스크립트에서 MPI 시작 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-188">The **runstarccm.sh** shell script will start the MPI launcher.</span></span>

<span data-ttu-id="b3161-189">입력 모델 및 **runstarccm.sh** 스크립트는 이전에 탑재된 **/hpcdata** 공유에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-189">The input model and the **runstarccm.sh** script are stored in the **/hpcdata** share that was previously mounted.</span></span>

<span data-ttu-id="b3161-190">로그 파일은 작업 ID로 이름이 지정되고 STAR-CCM+ 출력 파일과 함께 **/hpcdata 공유**에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-190">Log files are named with the job ID and are stored in the **/hpcdata share**, along with the STAR-CCM+ output files.</span></span>

#### <a name="sample-submitstarccmjobps1-script"></a><span data-ttu-id="b3161-191">샘플 SubmitStarccmJob.ps1 스크립트</span><span class="sxs-lookup"><span data-stu-id="b3161-191">Sample SubmitStarccmJob.ps1 script</span></span>
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us the job ID that's used to identify the name of the uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit the job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
<span data-ttu-id="b3161-192">**runner.java** 를 원하는 STAR-CCM+ java 모델 시작 관리자와 로깅 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span></span>

#### <a name="sample-runstarccmsh-script"></a><span data-ttu-id="b3161-193">샘플 runstarccm.sh 스크립트</span><span class="sxs-lookup"><span data-stu-id="b3161-193">Sample runstarccm.sh script</span></span>
```
    #!/bin/bash
    echo "start"
    # The path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set the mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create the hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into the hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with the hostfile argument
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

<span data-ttu-id="b3161-194">이 테스트에서는 Power-On-Demand 라이선스 토큰을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-194">In our test, we used a Power-On-Demand license token.</span></span> <span data-ttu-id="b3161-195">이 테스트에서는 **$CDLMD_LICENSE_FILE** 환경 변수를 **1999@flex.cd-adapco.com**으로 설정하고 명령줄의 **-podkey** 옵션에 키를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-195">For that token, you have to set the **$CDLMD_LICENSE_FILE** environment variable to **1999@flex.cd-adapco.com** and the key in the **-podkey** option of the command line.</span></span>

<span data-ttu-id="b3161-196">일부 초기화 후에는 스크립트가 HPC 팩이 설정하는 **$CCP_NODES_CORES** 환경 변수에서 노드 목록을 추출하여 MPI 시작 관리자가 사용하는 hostfile을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-196">After some initialization, the script extracts--from the **$CCP_NODES_CORES** environment variables that HPC Pack set--the list of nodes to build a hostfile that the MPI launcher uses.</span></span> <span data-ttu-id="b3161-197">이 hostfile에는 작업에 사용된 계산 노드 이름의 목록이 포함되며, 한 줄당 하나의 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-197">This hostfile will contain the list of compute node names that are used for the job, one name per line.</span></span>

<span data-ttu-id="b3161-198">**$CCP_NODES_CORES**의 형식은 이 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-198">The format of **$CCP_NODES_CORES** follows this pattern:</span></span>

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

<span data-ttu-id="b3161-199">여기서,</span><span class="sxs-lookup"><span data-stu-id="b3161-199">Where:</span></span>

* <span data-ttu-id="b3161-200">`<Number of nodes>` 는 이 작업에 할당된 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-200">`<Number of nodes>` is the number of nodes allocated to this job.</span></span>
* <span data-ttu-id="b3161-201">`<Name of node_n_...>` 은 이 작업에 할당된 각 노드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-201">`<Name of node_n_...>` is the name of each node allocated to this job.</span></span>
* <span data-ttu-id="b3161-202">`<Cores of node_n_...>` 은 이 작업에 할당된 노드의 코어 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-202">`<Cores of node_n_...>` is the number of cores on the node allocated to this job.</span></span>

<span data-ttu-id="b3161-203">코어 수(**$NBCORES**)도 노드 수(**$NBNODES**) 및 노드당 코어 수(매개 변수 **$NBCORESPERNODE**로 제공)를 기준으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-203">The number of cores (**$NBCORES**) is also calculated based on the number of nodes (**$NBNODES**) and the number of cores per node (provided as parameter **$NBCORESPERNODE**).</span></span>

<span data-ttu-id="b3161-204">Azure에서 Intel MPI와 함께 사용하는 MPI 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-204">For the MPI options, the ones that are used with Intel MPI on Azure are:</span></span>

* <span data-ttu-id="b3161-205">`-mpi intel` .</span><span class="sxs-lookup"><span data-stu-id="b3161-205">`-mpi intel` to specify Intel MPI.</span></span>
* <span data-ttu-id="b3161-206">`-fabric UDAPL` .</span><span class="sxs-lookup"><span data-stu-id="b3161-206">`-fabric UDAPL` to use Azure InfiniBand verbs.</span></span>
* <span data-ttu-id="b3161-207">`-cpubind bandwidth,v` .</span><span class="sxs-lookup"><span data-stu-id="b3161-207">`-cpubind bandwidth,v` to optimize bandwidth for MPI with STAR-CCM+.</span></span>
* <span data-ttu-id="b3161-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` .</span><span class="sxs-lookup"><span data-stu-id="b3161-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` to make Intel MPI work with Azure InfiniBand, and to set the required number of cores per node.</span></span>
* <span data-ttu-id="b3161-209">`-batch` .</span><span class="sxs-lookup"><span data-stu-id="b3161-209">`-batch` to start STAR-CCM+ in batch mode with no UI.</span></span>

<span data-ttu-id="b3161-210">마지막으로 작업을 시작하려면 노드가 실행 중이고 클러스터 관리자에서 온라인 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-210">Finally, to start a job, make sure that your nodes are up and running and are online in Cluster Manager.</span></span> <span data-ttu-id="b3161-211">그런 다음 PowerShell 명령 창에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-211">Then from a PowerShell command prompt, run this:</span></span>

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a><span data-ttu-id="b3161-212">노드 중지</span><span class="sxs-lookup"><span data-stu-id="b3161-212">Stop nodes</span></span>
<span data-ttu-id="b3161-213">나중에 테스트를 완료한 후 다음 HPC 팩 PowerShell 명령을 사용하여 노드를 중지하거나 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-213">Later on, after you're done with your tests, you can use the following HPC Pack PowerShell commands to stop and start nodes:</span></span>

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a><span data-ttu-id="b3161-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b3161-214">Next steps</span></span>
<span data-ttu-id="b3161-215">다른 Linux 워크로드를 실행해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b3161-215">Try running other Linux workloads.</span></span> <span data-ttu-id="b3161-216">예를 들어 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3161-216">For example, see:</span></span>

* [<span data-ttu-id="b3161-217">Azure의 Linux 계산 노드에서 Microsoft HPC 팩을 사용하여 NAMD 실행</span><span class="sxs-lookup"><span data-stu-id="b3161-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
* [<span data-ttu-id="b3161-218">Azure의 Linux RDMA 클러스터에서 Microsoft HPC 팩을 사용하여 OpenFOAM 실행</span><span class="sxs-lookup"><span data-stu-id="b3161-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
