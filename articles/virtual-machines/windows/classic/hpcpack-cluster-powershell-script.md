---
title: "aaaPowerShell 스크립트 toodeploy Windows HPC 클러스터 | Microsoft Docs"
description: "Azure 가상 컴퓨터에서 PowerShell 스크립트 toodeploy Windows HPC Pack 2012 R2 클러스터를 실행 합니다."
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
ms.openlocfilehash: 10ce1e9bc4e98954b955549bd72aaaf6106c69fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="09efd-103">Hello HPC Pack IaaS 배포 스크립트와 함께 Windows 고성능 HPC (컴퓨팅) 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="09efd-103">Create a Windows high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="09efd-104">Azure 가상 컴퓨터의 hello HPC Pack IaaS 배포 PowerShell 스크립트 toodeploy Windows 작업에 대 한 전체 HPC Pack 2012 R2 클러스터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Windows workloads in Azure virtual machines.</span></span> <span data-ttu-id="09efd-105">추가 창 계산 지정한 리소스 및 Windows Server 및 Microsoft HPC Pack을 실행 하는 Active Directory에 가입 된 헤드 노드 hello 클러스터 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and additional Windows compute resources you specify.</span></span> <span data-ttu-id="09efd-106">Azure에서 HPC Pack 클러스터 toodeploy Linux 작업에 대 한 경우 참조 [HPC Pack IaaS 배포 스크립트 hello로 Linux HPC 클러스터 만들기](../../linux/classic/hpcpack-cluster-powershell-script.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-106">If you want toodeploy an HPC Pack cluster in Azure for Linux workloads, see [Create a Linux HPC cluster with hello HPC Pack IaaS deployment script](../../linux/classic/hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="09efd-107">Azure 리소스 관리자 템플릿 toodeploy HPC Pack 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="09efd-108">예제는 [HPC 클러스터 만들기](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) 및 [사용자 지정 계산 노드 이미지로 HPC 클러스터 만들기](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09efd-108">For examples, see [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) and [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="09efd-109">이 문서에 설명 된 PowerShell 스크립트 hello hello 클래식 배포 모델을 사용 하 여 Azure에 Microsoft HPC Pack 2012 R2 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="09efd-110">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="09efd-111">또한이 문서에 설명 된 hello 스크립트는 HPC 팩 2016을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a><span data-ttu-id="09efd-112">예제 구성 파일</span><span class="sxs-lookup"><span data-stu-id="09efd-112">Example configuration files</span></span>
<span data-ttu-id="09efd-113">Hello 다음 예제에서는 사용자 고유의 구독 Id에 대 한 값 또는 이름 및 hello 계정 및 서비스 이름을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-113">In hello following examples, substitute your own values for your subscription Id or name and hello account and service names.</span></span>

### <a name="example-1"></a><span data-ttu-id="09efd-114">예 1</span><span class="sxs-lookup"><span data-stu-id="09efd-114">Example 1</span></span>
<span data-ttu-id="09efd-115">hello 다음 구성 파일 배포 로컬 데이터베이스가 있는 헤드 노드 및 hello Windows Server 2012 R2 운영 체제를 실행 하는 5 개의 계산 노드가 있는 HPC Pack 클러스터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-115">hello following configuration file deploys an HPC Pack cluster that has a head node with local databases and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="09efd-116">모든 hello 클라우드 서비스는 hello West US 위치에 직접 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-116">All hello cloud services are created directly in hello West US location.</span></span> <span data-ttu-id="09efd-117">헤드 노드 hello hello 도메인 포리스트의 도메인 컨트롤러 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-117">hello head node acts as domain controller of hello domain forest.</span></span>

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

### <a name="example-2"></a><span data-ttu-id="09efd-118">예 2</span><span class="sxs-lookup"><span data-stu-id="09efd-118">Example 2</span></span>
<span data-ttu-id="09efd-119">다음 구성 파일 hello 기존 도메인 포리스트에 HPC Pack 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-119">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="09efd-120">hello 클러스터에 로컬 데이터베이스가 있는 헤드 노드 1 및 계산 노드 VM BGInfo 확장이 적용 hello로 12입니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-120">hello cluster has 1 head node with local databases and 12 compute nodes with hello BGInfo VM extension applied.</span></span>
<span data-ttu-id="09efd-121">Windows 업데이트 자동 설치는 모든 hello hello 도메인 포리스트에 Vm에 대 한 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-121">Automatic installation of Windows updates is disabled for all hello VMs in hello domain forest.</span></span> <span data-ttu-id="09efd-122">모든 hello 클라우드 서비스는 동아시아 지역에 직접 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-122">All hello cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="09efd-123">hello 계산 노드는 3 개의 클라우드 서비스 및 3 개 저장소 계정에서 생성 됩니다: *MyHPCCN 0001* 너무*MyHPCCN 0005* 에 *MyHPCCNService01* 및  *mycnstorage01*; *MyHPCCN 0006* 너무*MyHPCCN0010* 에 *MyHPCCNService02* 및 *mycnstorage02*; 및  *MyHPCCN-0011* 너무*MyHPCCN 0012* 에 *MyHPCCNService03* 및 *mycnstorage03*).</span><span class="sxs-lookup"><span data-stu-id="09efd-123">hello compute nodes are created in three cloud services and three storage accounts: *MyHPCCN-0001* too*MyHPCCN-0005* in *MyHPCCNService01* and *mycnstorage01*; *MyHPCCN-0006* too*MyHPCCN0010* in *MyHPCCNService02* and *mycnstorage02*; and *MyHPCCN-0011* too*MyHPCCN-0012* in *MyHPCCNService03* and *mycnstorage03*).</span></span> <span data-ttu-id="09efd-124">hello 계산 노드가 계산 노드에서 캡처된 기존 개인 이미지에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-124">hello compute nodes are created from an existing private image captured from a compute node.</span></span> <span data-ttu-id="09efd-125">hello 자동 확장 및 축소 이며 기본값은 서비스를 사용 하는 확장 및 간격을 축소 합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-125">hello auto grow and shrink service is enabled with default grow and shrink intervals.</span></span>

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

### <a name="example-3"></a><span data-ttu-id="09efd-126">예 3</span><span class="sxs-lookup"><span data-stu-id="09efd-126">Example 3</span></span>
<span data-ttu-id="09efd-127">다음 구성 파일 hello 기존 도메인 포리스트에 HPC Pack 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-127">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="09efd-128">hello 클러스터 hello Windows Server 2012 R2 운영 체제 및 hello Windows Server 2012 R2 운영 체제를 실행 하는 5 개의 계산 노드를 실행 하는 두 개의 브로커 노드 하나 헤드 노드, 500GB 데이터 디스크와 데이터베이스 서버를 하나 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-128">hello cluster contains one head node, one database server with a 500 GB data disk, two broker nodes running hello Windows Server 2012 R2 operating system, and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="09efd-129">클라우드 서비스 MyHPCCNService hello 선호도 그룹에서 생성 된 hello *MyIBAffinityGroup*, hello 다른 클라우드 서비스에서에서 만들어진 hello 선호도 그룹 및 *MyAffinityGroup*합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-129">hello cloud service MyHPCCNService is created in hello affinity group *MyIBAffinityGroup*, and hello other cloud services are created in hello affinity group *MyAffinityGroup*.</span></span> <span data-ttu-id="09efd-130">hello HPC 작업 스케줄러 REST API 및 HPC 웹 포털은 헤드 노드 hello에 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-130">hello HPC Job Scheduler REST API and HPC web portal are enabled on hello head node.</span></span>

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



### <a name="example-4"></a><span data-ttu-id="09efd-131">예제 4</span><span class="sxs-lookup"><span data-stu-id="09efd-131">Example 4</span></span>
<span data-ttu-id="09efd-132">다음 구성 파일 hello 기존 도메인 포리스트에 HPC Pack 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-132">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="09efd-133">hello 클러스터에 로컬 데이터베이스가 있는 헤드 노드를 두 개, 두 개의 Azure 노드 템플릿을 만들고 Azure 노드 템플릿에 대 한 세 가지 크기 보통 Azure 노드가 만들어집니다 *AzureTemplate1*합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-133">hello cluster has two head node with local databases, two Azure node templates are created, and three size Medium Azure nodes are created for Azure node template *AzureTemplate1*.</span></span> <span data-ttu-id="09efd-134">Hello 헤드 노드를 구성한 후 hello 헤드 노드에서 스크립트 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-134">A script file runs on hello head node after hello head node is configured.</span></span>

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

## <a name="troubleshooting"></a><span data-ttu-id="09efd-135">문제 해결</span><span class="sxs-lookup"><span data-stu-id="09efd-135">Troubleshooting</span></span>
* <span data-ttu-id="09efd-136">**"VNet 존재 하지 않습니다." 오류** -하나 이상의 배포를 실행 하면 hello 스크립트 toodeploy 여러 클러스터 Azure에서 동시에 하나의 구독으로 hello 오류가 발생할 수 있습니다 "VNet *VNet\_이름* 하지 않습니다 "존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-136">**“VNet doesn’t exist” error** - If you run hello script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="09efd-137">이 오류가 발생 하면 실패 하는 hello 배포에 대 한 다시 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-137">If this error occurs, run hello script again for hello failed deployment.</span></span>
* <span data-ttu-id="09efd-138">**Hello Azure 가상 네트워크에서에서 인터넷 hello 문제 액세스** -hello 배포 스크립트를 사용 하 여 새 도메인 컨트롤러를 가진 클러스터를 만들 또는 수동으로 헤드 노드 VM toodomain 컨트롤러를 승격 하 고, 문제가 발생할 수 있습니다 하는 경우 hello Vm toohello 인터넷 연결을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-138">**Problem accessing hello Internet from hello Azure virtual network** - If you create a cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs toohello Internet.</span></span> <span data-ttu-id="09efd-139">이 문제는 전달자 DNS 서버가 hello 도메인 컨트롤러에서 자동으로 구성 되 고이 전달자 DNS 서버가 제대로 확인 되지 않습니다 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-139">This problem can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="09efd-140">이 문제를 해결 toowork toohello 도메인 컨트롤러와 제거 hello 전달자 구성 설정 하거나 로그온 하거나 유효한 전달자 DNS 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-140">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="09efd-141">서버 관리자에서이 설정을 클릭 tooconfigure **도구** >
    **DNS** tooopen DNS 관리자를 두 번 클릭 하 고 **전달자**합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-141">tooconfigure this setting, in Server Manager click **Tools** >
    **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>
* <span data-ttu-id="09efd-142">**계산 집약적인 Vm에서 RDMA 네트워크에 액세스 하는 문제** -Windows Server 계산을 추가 또는 A8 또는 A9 등 브로커 노드는 RDMA 가능을 사용 하 여 Vm 크기, 이러한 Vm toohello RDMA 응용 프로그램 네트워크 연결 문제가 발생할 수 있습니다 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="09efd-142">**Problem accessing RDMA network from compute-intensive VMs** - If you add Windows Server compute or broker node VMs using an RDMA-capable size such as A8 or A9, you may experience problems connecting those VMs toohello RDMA application network.</span></span> <span data-ttu-id="09efd-143">이 문제가 발생 하는 한 가지 이유는 경우 hello HpcVmDrivers 확장이 제대로 설치 되지 않았습니다 hello Vm이 toohello 클러스터를 추가 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="09efd-143">One reason this problem occurs is if hello HpcVmDrivers extension is not properly installed when hello VMs are added toohello cluster.</span></span> <span data-ttu-id="09efd-144">예를 들어 확장 상태를 설치 하는 hello 멈춰 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-144">For example, the extension might be stuck in hello installing state.</span></span>
  
    <span data-ttu-id="09efd-145">toowork 첫 번째 hello Vm에서 hello 확장의 hello 상태 확인이이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-145">toowork around this problem, first check hello state of hello extension in hello VMs.</span></span> <span data-ttu-id="09efd-146">Hello 확장이 제대로 설치 되지 않은 경우 hello 노드 hello HPC 클러스터에서 제거를 시도 하 고 hello 노드를 다시 추가 하십시오.</span><span class="sxs-lookup"><span data-stu-id="09efd-146">If hello extension is not properly installed, try removing hello nodes from hello HPC cluster and then add hello nodes again.</span></span> <span data-ttu-id="09efd-147">예를 들어 hello 헤드 노드에서 hello Add-hpciaasnode.ps1 스크립트를 실행 하 여 계산 노드 Vm을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-147">For example, you can add compute node VMs by running hello Add-HpcIaaSNode.ps1 script on hello head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09efd-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="09efd-148">Next steps</span></span>
* <span data-ttu-id="09efd-149">Hello 클러스터에서 테스트 작업을 실행 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="09efd-149">Try running a test workload on hello cluster.</span></span> <span data-ttu-id="09efd-150">예를 들어 hello HPC Pack을 참조 하십시오. [시작 가이드](https://technet.microsoft.com/library/jj884144)합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-150">For an example, see hello HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>
* <span data-ttu-id="09efd-151">자습서 tooscript hello 클러스터 배포를 실행 하는 HPC 작업에 대 한 참조 [Azure toorun Excel 및 SOA 작업에서 HPC Pack 클러스터 시작](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-151">For a tutorial tooscript hello cluster deployment and run an HPC workload, see [Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="09efd-152">HPC Pack 도구 toostart 시도, 중지, 추가 및 만들면 클러스터에서 계산 노드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-152">Try HPC Pack's tools toostart, stop, add, and remove compute nodes from a cluster you create.</span></span> <span data-ttu-id="09efd-153">[Azure에서 HPC Pack 클러스터의 계산 노드 관리](hpcpack-cluster-node-manage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09efd-153">See [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md).</span></span>
* <span data-ttu-id="09efd-154">로컬 컴퓨터에서 toosubmit 작업 toohello 클러스터를 설정 하는 tooget 참조 [제출 HPC 작업은 온-프레미스 컴퓨터 tooan HPC Pack에서에서 Azure에 있는 클러스터](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="09efd-154">tooget set up toosubmit jobs toohello cluster from a local computer, see [Submit HPC jobs from an on-premises computer tooan HPC Pack cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

