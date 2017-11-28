---
title: "aaaPowerShell 스크립트 toodeploy Linux HPC 클러스터 | Microsoft Docs"
description: "Azure 가상 컴퓨터에서 PowerShell 스크립트 toodeploy Linux HPC Pack 2012 R2 클러스터를 실행 합니다."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 885b03fa2fd604827dc388803fc21debab730979
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="bae61-103">Hello HPC Pack IaaS 배포 스크립트와 함께 Linux 고성능 HPC (컴퓨팅) 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="bae61-103">Create a Linux high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="bae61-104">Azure 가상 컴퓨터의 hello HPC Pack IaaS 배포 PowerShell 스크립트 toodeploy Linux 작업에 대 한 전체 HPC Pack 2012 R2 클러스터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Linux workloads in Azure virtual machines.</span></span> <span data-ttu-id="bae61-105">hello 클러스터가 HPC Pack에서 지 원하는 Linux 배포 hello 중 하나를 실행 하는 계산 노드 및 Windows Server 및 Microsoft HPC Pack을 실행 하는 Active Directory에 가입 된 헤드 노드 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and compute nodes that run one of hello Linux distributions supported by HPC Pack.</span></span> <span data-ttu-id="bae61-106">Windows Azure에 대 한 작업에서 HPC Pack 클러스터 toodeploy 참조 [hello HPC Pack IaaS 배포 스크립트 사용 Windows HPC 클러스터를 만들고](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-106">If you want toodeploy an HPC Pack cluster in Azure for Windows workloads, see [Create a Windows HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="bae61-107">Azure 리소스 관리자 템플릿 toodeploy HPC Pack 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="bae61-108">예제는 [Linux 계산 노드가 포함된 HPC 클러스터 만들기](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bae61-108">For an example, see [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="bae61-109">이 문서에 설명 된 PowerShell 스크립트 hello hello 클래식 배포 모델을 사용 하 여 Azure에 Microsoft HPC Pack 2012 R2 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="bae61-110">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="bae61-111">또한이 문서에 설명 된 hello 스크립트는 HPC 팩 2016을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a><span data-ttu-id="bae61-112">예제 구성 파일</span><span class="sxs-lookup"><span data-stu-id="bae61-112">Example configuration file</span></span>
<span data-ttu-id="bae61-113">hello 다음 구성 파일을 도메인 컨트롤러 및 도메인 포리스트 만들고 10 Linux 계산 노드 및 로컬 데이터베이스가 있는 헤드 노드 하나에 HPC Pack 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-113">hello following configuration file creates a domain controller and domain forest and deploys an HPC Pack cluster which has one head node with local databases and 10 Linux compute nodes.</span></span> <span data-ttu-id="bae61-114">모든 hello 클라우드 서비스는 hello 동아시아 지역에 직접 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-114">All hello cloud services are created directly in hello East Asia location.</span></span> <span data-ttu-id="bae61-115">hello Linux 계산 노드가 생성 되어 두 개의 클라우드 서비스 및 두 개의 저장소 계정에서 (즉, *MyLnxCN 0001* 를 *MyLnxCN 0005* 에 *MyLnxCNService01* 및 *mylnxstorage01*, 및 *MyLnxCN 0006* 를 *MyLnxCN 0010* 에 *MyLnxCNService02* 및 *mylnxstorage02* ).</span><span class="sxs-lookup"><span data-stu-id="bae61-115">hello Linux compute nodes are created in two cloud services and two storage accounts (that is, *MyLnxCN-0001* to *MyLnxCN-0005* in *MyLnxCNService01* and *mylnxstorage01*, and *MyLnxCN-0006* to *MyLnxCN-0010* in *MyLnxCNService02* and *mylnxstorage02*).</span></span> <span data-ttu-id="bae61-116">hello 계산 노드가 OpenLogic CentOS 버전 7.0 Linux 이미지에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-116">hello compute nodes are created from an OpenLogic CentOS version 7.0 Linux image.</span></span> 

<span data-ttu-id="bae61-117">구독 이름 및 hello 계정 및 서비스 이름에 대 한 고유한 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-117">Substitute your own values for your subscription name and hello account and service names.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
    </DomainController>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a><span data-ttu-id="bae61-118">문제 해결</span><span class="sxs-lookup"><span data-stu-id="bae61-118">Troubleshooting</span></span>
* <span data-ttu-id="bae61-119">**"VNet이 없음" 오류**.</span><span class="sxs-lookup"><span data-stu-id="bae61-119">**“VNet doesn’t exist” error**.</span></span> <span data-ttu-id="bae61-120">하나 이상의 배포를 실행 하면 hello HPC Pack IaaS 배포 스크립트 toodeploy 여러 클러스터 Azure에서 동시에 하나의 구독으로 hello 오류가 발생할 수 있습니다 "VNet *VNet\_이름* 존재 하지 않는"입니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-120">If you run hello HPC Pack IaaS deployment script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="bae61-121">이 오류가 발생 하면 실패 하는 hello 배포에 대 한 hello 스크립트를 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-121">If this error occurs, rerun hello script for hello failed deployment.</span></span>
* <span data-ttu-id="bae61-122">**Hello Azure 가상 네트워크에서에서 인터넷 hello 문제 액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-122">**Problem accessing hello Internet from hello Azure virtual network**.</span></span> <span data-ttu-id="bae61-123">헤드 노드 VM toodomain 컨트롤러를 수동으로 승격 이나 hello 배포 스크립트를 사용 하 여 새 도메인 컨트롤러와 HPC Pack 클러스터를 만들 때, hello Vm hello Azure 가상 네트워크 toohello 인터넷에에서 연결할 때 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-123">If you create an HPC Pack cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs in hello Azure virtual network toohello Internet.</span></span> <span data-ttu-id="bae61-124">이 전달자 DNS 서버가 hello 도메인 컨트롤러에서 자동으로 구성 되 고이 전달자 DNS 서버가 제대로 확인 되지 않습니다 하는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-124">This can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="bae61-125">이 문제를 해결 toowork toohello 도메인 컨트롤러와 제거 hello 전달자 구성 설정 하거나 로그온 하거나 유효한 전달자 DNS 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-125">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="bae61-126">서버 관리자에서이 클릭 toodo **도구** > **DNS** tooopen DNS 관리자를 두 번 클릭 하 고 **전달자**합니다.</span><span class="sxs-lookup"><span data-stu-id="bae61-126">toodo this, in Server Manager click **Tools** > **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bae61-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bae61-127">Next steps</span></span>
* <span data-ttu-id="bae61-128">참조 [Azure에서 HPC Pack 클러스터에서 계산 노드 Linux 시작](hpcpack-cluster.md) 지원 되는 Linux 배포판에 대 한 내용은 데이터를 이동 하 고 Linux로 tooan HPC Pack 클러스터 작업을 제출 하는 계산 노드.</span><span class="sxs-lookup"><span data-stu-id="bae61-128">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for information about supported Linux distributions, moving data, and submitting jobs tooan HPC Pack cluster with Linux compute nodes.</span></span>
* <span data-ttu-id="bae61-129">Hello 스크립트 toocreate 클러스터를 사용 하 고 Linux HPC 작업을 실행 하는 자습서를 보려면</span><span class="sxs-lookup"><span data-stu-id="bae61-129">For tutorials that use hello script toocreate a cluster and run a Linux HPC workload, see:</span></span>
  * [<span data-ttu-id="bae61-130">Azure의 Linux 계산 노드에서 Microsoft HPC 팩을 사용하여 NAMD 실행</span><span class="sxs-lookup"><span data-stu-id="bae61-130">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
  * [<span data-ttu-id="bae61-131">Azure의 Linux 계산 노드에서 Microsoft HPC 팩을 사용하여 OpenFOAM 실행</span><span class="sxs-lookup"><span data-stu-id="bae61-131">Run OpenFOAM with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-openfoam.md)
  * [<span data-ttu-id="bae61-132">Azure의 Linux 계산 노드에서 Microsoft HPC 팩을 사용하여 STAR-CCM+ 실행</span><span class="sxs-lookup"><span data-stu-id="bae61-132">Run STAR-CCM+ with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-starccm.md)

