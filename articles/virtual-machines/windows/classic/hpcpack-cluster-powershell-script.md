---
title: "Windows HPC 클러스터를 배포하기 위한 PowerShell 스크립트 | Microsoft Docs"
description: "PowerShell 스크립트를 실행하여 Azure 가상 컴퓨터에 Windows HPC Pack 2012 R2 클러스터 배포"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 286b2be8-2533-40df-b02a-26156b1f1133
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 85b125ab19671b61d2541af6378c95feb88bf952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="21437-103">HPC Pack IaaS 배포 스크립트를 사용하여 Windows HPC(고성능 컴퓨팅) 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="21437-103">Create a Windows high-performance computing (HPC) cluster with the HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="21437-104">HPC Pack IaaS 배포 PowerShell 스크립트를 실행하여 Azure 가상 컴퓨터에 완전한 Windows 워크로드용 HPC Pack 2012 R2 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="21437-104">Run the HPC Pack IaaS deployment PowerShell script to deploy a complete HPC Pack 2012 R2 cluster for Windows workloads in Azure virtual machines.</span></span> <span data-ttu-id="21437-105">클러스터는 Windows Server, Microsoft HPC 팩 및 지정한 추가 Windows 계산 리소스를 실행하는 Active Directory 가입 헤드 노드로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="21437-105">The cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and additional Windows compute resources you specify.</span></span> <span data-ttu-id="21437-106">Azure에서 Linux 워크로드용 HPC Pack 클러스터를 배포하려면 [HPC Pack IaaS 배포 스크립트를 사용하여 Linux HPC 클러스터 만들기](../../linux/classic/hpcpack-cluster-powershell-script.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21437-106">If you want to deploy an HPC Pack cluster in Azure for Linux workloads, see [Create a Linux HPC cluster with the HPC Pack IaaS deployment script](../../linux/classic/hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="21437-107">Azure 리소스 관리자 템플릿을 사용하여 HPC 팩 클러스터를 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21437-107">You can also use an Azure Resource Manager template to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="21437-108">예제는 [HPC 클러스터 만들기](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) 및 [사용자 지정 계산 노드 이미지로 HPC 클러스터 만들기](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21437-108">For examples, see [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) and [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="21437-109">이 문서에 설명된 PowerShell 스크립트는 클래식 배포 모델을 사용하여 Azure에 Microsoft HPC Pack 2012 R2 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21437-109">The PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using the classic deployment model.</span></span> <span data-ttu-id="21437-110">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="21437-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="21437-111">또한 이 문서에 설명된 스크립트는 HPC Pack 2016을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="21437-111">In addition, the script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a><span data-ttu-id="21437-112">예제 구성 파일</span><span class="sxs-lookup"><span data-stu-id="21437-112">Example configuration files</span></span>
<span data-ttu-id="21437-113">다음 예제에서 구독 이름과 계정 및 서비스 이름을 고유한 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="21437-113">In the following examples, substitute your own values for your subscription Id or name and the account and service names.</span></span>

### <a name="example-1"></a><span data-ttu-id="21437-114">예 1</span><span class="sxs-lookup"><span data-stu-id="21437-114">Example 1</span></span>
<span data-ttu-id="21437-115">다음 구성 파일은 로컬 데이터베이스를 사용하는 1개 헤드 노드와 Windows Server 2012 R2 운영 체제를 실행하는 5개 계산 노드가 있는 HPC 팩 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="21437-115">The following configuration file deploys an HPC Pack cluster that has a head node with local databases and five compute nodes running the Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="21437-116">모든 클라우드 서비스는 미국 서부 위치에서 직접 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="21437-116">All the cloud services are created directly in the West US location.</span></span> <span data-ttu-id="21437-117">헤드 노드는 도메인 포리스트의 도메인 컨트롤러의 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="21437-117">The head node acts as domain controller of the domain forest.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionId>08701940-C02E-452F-B0B1-39D50119F267</SubscriptionId>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%1000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>5</NodeCount>
    <OSVersion>WindowsServer2012R2</OSVersion>
  </ComputeNodes>
</IaaSClusterConfig>
```

### <a name="example-2"></a><span data-ttu-id="21437-118">예 2</span><span class="sxs-lookup"><span data-stu-id="21437-118">Example 2</span></span>
<span data-ttu-id="21437-119">다음 구성 파일은 기존 도메인 포리스트에 HPC 팩 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="21437-119">The following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="21437-120">클러스터에는 로컬 데이터베이스가 포함된 1개 헤드와 BGInfo VM 확장이 적용된 12개 계산 노드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21437-120">The cluster has 1 head node with local databases and 12 compute nodes with the BGInfo VM extension applied.</span></span>
<span data-ttu-id="21437-121">도메인 포리스트의 모든 VM에 대해 Windows 업데이트 자동 설치를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="21437-121">Automatic installation of Windows updates is disabled for all the VMs in the domain forest.</span></span> <span data-ttu-id="21437-122">모든 클라우드 서비스는 동아시아 위치에서 직접 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="21437-122">All the cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="21437-123">계산 노드는 3개 클라우드 서비스와 3개 저장소 계정에 생성됩니다(*MyHPCCNService01* 및 *mycnstorage01*에서 *MyHPCCN-0001* - *MyHPCCN-0005*, *MyHPCCNService02* 및 *mycnstorage02*에서 *MyHPCCN-0006* - *MyHPCCN0010*, *MyHPCCNService03* 및 *mycnstorage03*에서 *MyHPCCN-0011* - *MyHPCCN-0012*).</span><span class="sxs-lookup"><span data-stu-id="21437-123">The compute nodes are created in three cloud services and three storage accounts: *MyHPCCN-0001* to *MyHPCCN-0005* in *MyHPCCNService01* and *mycnstorage01*; *MyHPCCN-0006* to *MyHPCCN0010* in *MyHPCCNService02* and *mycnstorage02*; and *MyHPCCN-0011* to *MyHPCCN-0012* in *MyHPCCNService03* and *mycnstorage03*).</span></span> <span data-ttu-id="21437-124">계산 노드는 계산 노드에서 캡처된 기존 개인 이미지에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="21437-124">The compute nodes are created from an existing private image captured from a compute node.</span></span> <span data-ttu-id="21437-125">자동 증가 및 축소 서비스를 사용하며 기본 증가 및 축소 간격이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="21437-125">The auto grow and shrink service is enabled with default grow and shrink intervals.</span></span>

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
     <NoWindowsAutoUpdate />
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
  </Certificates>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0001%</VMNamePattern>
<ServiceNamePattern>MyHPCCNService%01%</ServiceNamePattern>
<MaxNodeCountPerService>5</MaxNodeCountPerService>
<StorageAccountNamePattern>mycnstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>12</NodeCount>
    <ImageName HPCPackInstalled=”true”>MyHPCComputeNodeImage</ImageName>
    <VMExtensions>
       <VMExtension>
          <ExtensionName>BGInfo</ExtensionName>
          <Publisher>Microsoft.Compute</Publisher>
          <Version>1.*</Version>
       </VMExtension>
    </VMExtensions>
  </ComputeNodes>
  <AutoGrowShrink>
    <CertificateId>1</CertificateId>
  </AutoGrowShrink>
</IaaSClusterConfig>

```

### <a name="example-3"></a><span data-ttu-id="21437-126">예 3</span><span class="sxs-lookup"><span data-stu-id="21437-126">Example 3</span></span>
<span data-ttu-id="21437-127">다음 구성 파일은 기존 도메인 포리스트에 HPC 팩 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="21437-127">The following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="21437-128">클러스터에는 1개 헤드 노드, 500GB의 데이터 디스크가 포함된 1개 데이터베이스 서버, Windows Server 2012 R2 운영 체제를 실행하는 2개 broker 노드, Windows Server 2012 R2 운영 체제를 실행하는 5개 계산 노드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21437-128">The cluster contains one head node, one database server with a 500 GB data disk, two broker nodes running the Windows Server 2012 R2 operating system, and five compute nodes running the Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="21437-129">클라우드 서비스인 MyHPCCNService는 선호도 그룹 *MyIBAffinityGroup*에 만들어지며 기타 클라우드 서비스는 선호도 그룹 *MyAffinityGroup*에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="21437-129">The cloud service MyHPCCNService is created in the affinity group *MyIBAffinityGroup*, and the other cloud services are created in the affinity group *MyAffinityGroup*.</span></span> <span data-ttu-id="21437-130">헤드 노드에서 HPC 작업 스케줄러 REST API 및 HPC 웹 포털을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="21437-130">The HPC Job Scheduler REST API and HPC web portal are enabled on the head node.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>    
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>NewRemoteDB</DBOption>
    <DBVersion>SQLServer2014_Enterprise</DBVersion>
    <DBServer>
      <VMName>MyDBServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>ExtraLarge</VMSize>
      <DataDiskSizeInGB>500</DataDiskSizeInGB>
    </DBServer>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>A8</VMSize>
<NodeCount>5</NodeCount>
<AffinityGroup>MyIBAffinityGroup</AffinityGroup>
  </ComputeNodes>
  <BrokerNodes>
    <VMNamePattern>MyHPCBN-%0000%</VMNamePattern>
    <ServiceName>MyHPCBNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>2</NodeCount>
  </BrokerNodes>
</IaaSClusterConfig>
```



### <a name="example-4"></a><span data-ttu-id="21437-131">예제 4</span><span class="sxs-lookup"><span data-stu-id="21437-131">Example 4</span></span>
<span data-ttu-id="21437-132">다음 구성 파일은 기존 도메인 포리스트에 HPC 팩 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="21437-132">The following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="21437-133">클러스터에는 로컬 데이터베이스를 사용하는 2개 헤드 노드가 포함되어 있으며, 2개 Azure 노드 템플릿이 만들어지고, Azure 노드 템플릿 *AzureTemplate1*에 대해 3개 중간 크기 Azure 노드가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="21437-133">The cluster has two head node with local databases, two Azure node templates are created, and three size Medium Azure nodes are created for Azure node template *AzureTemplate1*.</span></span> <span data-ttu-id="21437-134">헤드 노드가 구성된 다음 헤드 노드에 스크립트 파일이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="21437-134">A script file runs on the head node after the head node is configured.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
<VMSize>ExtraLarge</VMSize>
    <PostConfigScript>c:\MyHNPostActions.ps1</PostConfigScript>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
    <Certificate>
      <Id>2</Id>
      <PfxFile>d:\mytestcert2.pfx</PfxFile>
    </Certificate>    
  </Certificates>
  <AzureBurst>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate1</TemplateName>
      <SubscriptionId>bb9252ba-831f-4c9d-ae14-9a38e6da8ee4</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc1</ServiceName>
      <StorageAccount>myteststorage1</StorageAccount>
      <NodeCount>3</NodeCount>
      <RoleSize>Medium</RoleSize>
    </AzureNodeTemplate>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate2</TemplateName>
      <SubscriptionId>ad4b9f9f-05f2-4c74-a83f-f2eb73000e0b</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc2</ServiceName>
      <StorageAccount>myteststorage2</StorageAccount>
      <Proxy>
        <UsesStaticProxyCount>false</UsesStaticProxyCount>     
        <ProxyRatio>100</ProxyRatio>
        <ProxyRatioBase>400</ProxyRatioBase>
      </Proxy>
      <OSVersion>WindowsServer2012</OSVersion>
    </AzureNodeTemplate>
  </AzureBurst>
</IaaSClusterConfig>
```

## <a name="troubleshooting"></a><span data-ttu-id="21437-135">문제 해결</span><span class="sxs-lookup"><span data-stu-id="21437-135">Troubleshooting</span></span>
* <span data-ttu-id="21437-136">**"VNet이 없음" 오류** - 스크립트를 실행하여 하나의 구독으로 Azure에 여러 클러스터를 배포할 경우 하나 이상의 배포가 실패하고 "VNet *VNet\_Name* 없음" 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="21437-136">**“VNet doesn’t exist” error** - If you run the script to deploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with the error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="21437-137">이 오류가 발생할 경우 실패한 배포에 대해 스크립트를 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="21437-137">If this error occurs, run the script again for the failed deployment.</span></span>
* <span data-ttu-id="21437-138">**Azure 가상 네트워크에서 인터넷에 액세스할 수 없는 문제** - 배포 스크립트를 사용하여 새 도메인 컨트롤러로 클러스터를 만들거나 헤드 노드 VM을 도메인 컨트롤러로 수동으로 승격할 경우 VM에서 인터넷으로 연결할 때 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21437-138">**Problem accessing the Internet from the Azure virtual network** - If you create a cluster with a new domain controller by using the deployment script, or you manually promote a head node VM to domain controller, you may experience problems connecting the VMs to the Internet.</span></span> <span data-ttu-id="21437-139">이러한 문제는 전달자 DNS 서버가 도메인 컨트롤러에 자동으로 구성되어 있고 이 전달자 DNS 서버가 올바르게 확인되지 않을 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21437-139">This problem can occur if a forwarder DNS server is automatically configured on the domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="21437-140">이 문제를 해결하려면 도메인 컨트롤러에 로그인하고 전달자 구성 설정을 제거하거나 유효한 전달자 DNS 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="21437-140">To work around this problem, log on to the domain controller and either remove the forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="21437-141">이 설정을 구성하려면 서버 관리자에서 **도구** >
    **DNS**를 클릭하여 DNS 관리자를 연 다음 **전달자**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="21437-141">To configure this setting, in Server Manager click **Tools** >
    **DNS** to open DNS Manager, and then double-click **Forwarders**.</span></span>
* <span data-ttu-id="21437-142">**계산 집약적 VM에서 RDMA 네트워크에 액세스하지 못하는 문제** - RDMA 지원 크기(예: A8 또는 A9)를 사용하여 Windows Server 계산 노드 또는 broker 노드 VM를 추가할 경우 이러한 VM에서 RDMA 응용 프로그램 네트워크에 연결하지 못하는 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21437-142">**Problem accessing RDMA network from compute-intensive VMs** - If you add Windows Server compute or broker node VMs using an RDMA-capable size such as A8 or A9, you may experience problems connecting those VMs to the RDMA application network.</span></span> <span data-ttu-id="21437-143">이러한 문제가 발생하는 원인 중 하나는 클러스터에 VM을 추가할 때 HpcVmDrivers 확장이 올바르게 설치되지 않았기 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21437-143">One reason this problem occurs is if the HpcVmDrivers extension is not properly installed when the VMs are added to the cluster.</span></span> <span data-ttu-id="21437-144">예를 들어 확장이 설치 상태에서 정지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21437-144">For example, the extension might be stuck in the installing state.</span></span>
  
    <span data-ttu-id="21437-145">이 문제를 해결하려면 가장 먼저 VM에서 확장 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="21437-145">To work around this problem, first check the state of the extension in the VMs.</span></span> <span data-ttu-id="21437-146">확장이 올바르게 설치되지 않은 경우 HPC 클러스터에서 노드를 제거한 다음 노드를 다시 추가해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="21437-146">If the extension is not properly installed, try removing the nodes from the HPC cluster and then add the nodes again.</span></span> <span data-ttu-id="21437-147">예를 들어 헤드 노드에서 Add-HpcIaaSNode.ps1 스크립트를 실행하여 계산 노드 VM을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21437-147">For example, you can add compute node VMs by running the Add-HpcIaaSNode.ps1 script on the head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21437-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="21437-148">Next steps</span></span>
* <span data-ttu-id="21437-149">클러스터에서 테스트 워크로드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="21437-149">Try running a test workload on the cluster.</span></span> <span data-ttu-id="21437-150">예를 보려면 HPC 팩 [시작하기 가이드](https://technet.microsoft.com/library/jj884144)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21437-150">For an example, see the HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>
* <span data-ttu-id="21437-151">클러스터 배포를 스크립트로 작성하고 HPC 워크로드를 실행하는 자습서를 보려면 [Azure에서 Excel 및 SOA 워크로드를 실행할 HPC Pack 클러스터 시작하기](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21437-151">For a tutorial to script the cluster deployment and run an HPC workload, see [Get started with an HPC Pack cluster in Azure to run Excel and SOA workloads](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="21437-152">사용자가 만든 클러스터에서 계산 노드를 시작, 중지, 추가, 제거하는 HPC 팩의 도구.</span><span class="sxs-lookup"><span data-stu-id="21437-152">Try HPC Pack's tools to start, stop, add, and remove compute nodes from a cluster you create.</span></span> <span data-ttu-id="21437-153">[Azure에서 HPC Pack 클러스터의 계산 노드 관리](hpcpack-cluster-node-manage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21437-153">See [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md).</span></span>
* <span data-ttu-id="21437-154">로컬 컴퓨터에서 클러스터에 작업 제출을 시작하려면 [온-프레미스 컴퓨터에서 Azure의 HPC 팩 클러스터로 HPC 작업 제출](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="21437-154">To get set up to submit jobs to the cluster from a local computer, see [Submit HPC jobs from an on-premises computer to an HPC Pack cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

