---
title: "SQL Server와 함께 Azure 프리미엄 저장소 aaaUse | Microsoft Docs"
description: "이 문서는 hello 클래식 배포 모델을 사용 하 여 만든 리소스를 사용 하 고 Azure 프리미엄 저장소를 사용 하 여 Azure 가상 컴퓨터에서 실행 되는 SQL server에 대 한 지침을 제공 합니다."
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="738e8-103">가상 컴퓨터의 SQL Server에서 Azure 프리미엄 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="738e8-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="738e8-104">개요</span><span class="sxs-lookup"><span data-stu-id="738e8-104">Overview</span></span>
<span data-ttu-id="738e8-105">[Azure 프리미엄 저장소](../../../storage/common/storage-premium-storage.md) 차세대 짧은 대기 시간과 높은 처리량 IO 제공 하는 저장소의 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) is hello next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="738e8-106">IaaS [가상 컴퓨터](https://azure.microsoft.com/services/virtual-machines/)의 SQL Server와 같이 IO를 많이 사용하는 주요 워크로드에서 매우 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="738e8-107">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="738e8-108">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="738e8-109">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="738e8-110">이 문서에서는 계획 및 SQL Server toouse 프리미엄 저장소를 실행 하는 가상 컴퓨터를 마이그레이션하기 위한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server toouse Premium Storage.</span></span> <span data-ttu-id="738e8-111">여기에는 Azure 인프라(네트워킹, 저장소) 및 게스트 Windows VM 관련 단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="738e8-112">hello에 hello 예제 [부록](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) toomove 더 큰 Vm tootake 활용 향상 하는 방법의 전체 포괄적인 최종 tooend 마이그레이션이 로컬 표시 powershell SSD 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-112">hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end tooend migration of how toomove larger VMs tootake advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="738e8-113">IAAS Vm에 SQL Server와 함께 사용 하 여 Azure 프리미엄 저장소의 중요 한 toounderstand hello 종단 간 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-113">It is important toounderstand hello end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="738e8-114">다음 내용이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-114">This includes:</span></span>

* <span data-ttu-id="738e8-115">Hello 필수 구성 요소 toouse 프리미엄 저장소의 id입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-115">Identification of hello prerequisites toouse Premium Storage.</span></span>
* <span data-ttu-id="738e8-116">새 배포를 위해 IaaS tooPremium 저장소에 SQL Server 배포의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-116">Examples of deploying SQL Server on IaaS tooPremium Storage for new deployments.</span></span>
* <span data-ttu-id="738e8-117">기존 배포 환경(SQL Always On 가용성 그룹을 사용하는 배포와 독립 실행형 서버 배포)을 마이그레이션하는 예제</span><span class="sxs-lookup"><span data-stu-id="738e8-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="738e8-118">가능한 마이그레이션 방법</span><span class="sxs-lookup"><span data-stu-id="738e8-118">Possible migration approaches.</span></span>
* <span data-ttu-id="738e8-119">기존 Always On 구현을 hello 마이그레이션에 대 한 Azure, Windows 및 SQL Server 단계를 보여 주는 전체에 종단 간 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for hello migration of an existing Always On implementation.</span></span>

<span data-ttu-id="738e8-120">Azure 가상 컴퓨터의 SQL Server에 대한 추가 배경 정보는 [Azure 가상 컴퓨터의 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="738e8-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="738e8-121">**작성자:** Daniel Sol **기술 검토자:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span><span class="sxs-lookup"><span data-stu-id="738e8-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="738e8-122">프리미엄 저장소 사용을 위한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="738e8-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="738e8-123">프리미엄 저장소를 사용하려면 몇 가지 필수 구성 요소를 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="738e8-124">컴퓨터 크기</span><span class="sxs-lookup"><span data-stu-id="738e8-124">Machine size</span></span>
<span data-ttu-id="738e8-125">프리미엄 저장소를 사용 하 여 toouse DS 시리즈 VM (가상 컴퓨터) 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-125">For using Premium Storage you will need toouse DS series Virtual Machines (VM).</span></span> <span data-ttu-id="738e8-126">하기 전에 클라우드 서비스에서 컴퓨터를 DS 시리즈를 사용 하지 않은 경우 hello 기존 VM을 삭제, hello 연결 된 디스크 유지 하며 다음 VM 역할 크기 DS *으로 hello를 다시 만들기 전에 새 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-126">If you have not used DS Series machines in your cloud service before, you must delete hello existing VM, keep hello attached disks, and then create a new cloud service before recreating hello VM as DS* role size.</span></span> <span data-ttu-id="738e8-127">가상 컴퓨터 크기에 대한 자세한 내용은 [Azure를 위한 가상 컴퓨터 및 클라우드 서비스 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="738e8-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="738e8-128">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="738e8-128">Cloud services</span></span>
<span data-ttu-id="738e8-129">새 클라우드 서비스에서 VM을 만들 때는 프리미엄 저장소를 사용하는 DS* VM만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-129">You can only use DS* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="738e8-130">Azure에서 SQL Server Always On 사용 hello 항상 수신기는 클라우드 서비스와 연결 된 toohello Azure 내부 또는 외부 부하 분산 장치 IP 주소를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-130">If you are using SQL Server Always On in Azure, hello Always On Listener will refer toohello Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="738e8-131">이 문서는 방법을 중점적으로이 시나리오에서 가용성을 유지 하면서 toomigrate 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-131">This article focuses on how toomigrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="738e8-132">* DS 시리즈에 배포 된 toohello은 첫 번째 VM hello 해야 새 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-132">A DS* Series must be hello first VM that is deployed toohello new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="738e8-133">지역별 VNET</span><span class="sxs-lookup"><span data-stu-id="738e8-133">Regional VNETS</span></span>
<span data-ttu-id="738e8-134">DS Vm에 대 한 가상 네트워크 (VNET) 하면 Vm toobe 국가별 호스팅 hello를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-134">For DS* VMs you must configure hello Virtual Network (VNET) hosting your VMs toobe regional.</span></span> <span data-ttu-id="738e8-135">이 "확대" hello VNET은 tooallow hello 더 큰 Vm toobe 다른 클러스터에 프로 비전 및 간에 통신을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-135">This “widens” hello VNET is tooallow hello larger VMs toobe provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="738e8-136">다음 스크린 샷 hello, hello 강조 표시 된 위치를 표시 지역 Vnet 반면 hello 첫 번째 결과 "좁은" VNET은 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-136">In hello following screenshot, hello highlighted Location shows regional VNETs, whereas hello first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="738e8-138">Microsoft 지원 티켓 toomigrate tooa를 발생 시킬 수 지역 VNET, Microsoft는 변경 toocomplete hello 마이그레이션 tooregional Vnet hello 네트워크 구성에서 AffinityGroup hello 속성을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-138">You can raise a Microsoft support ticket toomigrate tooa regional VNET, Microsoft will make a change, then toocomplete hello migration tooregional VNETs, change hello property AffinityGroup in hello network configuration.</span></span> <span data-ttu-id="738e8-139">먼저 hello PowerShell의 네트워크 구성을 내보낸 다음 hello를 바꾸어야 **AffinityGroup** hello에 대 한 속성 **VirtualNetworkSite** 인 요소는 **위치** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-139">First export hello Network Configuration in PowerShell, and then replace hello **AffinityGroup** property in hello **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="738e8-140">이때 `Location = XXXX`를 지정합니다. 여기서 `XXXX`가 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="738e8-141">그런 다음 새 구성을 hello를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-141">Then import hello new configuration.</span></span>

<span data-ttu-id="738e8-142">예를 들어 고려 같은 VNET 구성이 hello:</span><span class="sxs-lookup"><span data-stu-id="738e8-142">For example, considering hello following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="738e8-143">toomove이이 tooa 서 부 유럽에서 지역 VNET hello 구성 toohello 다음 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-143">toomove this tooa regional VNET in West Europe, change hello configuration toohello following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="738e8-144">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="738e8-144">Storage accounts</span></span>
<span data-ttu-id="738e8-145">프리미엄 저장소 용으로 구성 된 새 저장소 계정을 toocreate가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-145">You will need toocreate a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="738e8-146">하지만 Note * DS 시리즈 VM을 사용 하는 경우 고급 도메인 및 표준 저장소 계정에서 VHD를 연결할 수 있습니다 프리미엄 저장소의 hello 사용은 개별 Vhd에 없는 hello 저장소 계정에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-146">Note that hello use of Premium Storage is set at hello storage account, not on individual VHDs, however when using a DS* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="738e8-147">Toohello 프리미엄 저장소 계정에 대 한 운영 체제 VHD tooplace hello 하지 않을 경우 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-147">You may consider this if you do not want tooplace hello OS VHD on toohello Premium Storage account.</span></span>

<span data-ttu-id="738e8-148">hello 다음 **새로 AzureStorageAccountPowerShell** "Premium_LRS" hello로 명령을 **형식** 프리미엄 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-148">hello following **New-AzureStorageAccountPowerShell** command with hello "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="738e8-149">VHD 캐시 설정</span><span class="sxs-lookup"><span data-stu-id="738e8-149">VHDs Cache Settings</span></span>
<span data-ttu-id="738e8-150">프리미엄 저장소 계정에 속한 디스크를 만들어 간의 hello 주요 차이점은 hello 디스크 캐시 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-150">hello main difference between creating disks that are part of a Premium Storage account is hello disk cache setting.</span></span> <span data-ttu-id="738e8-151">SQL Server 데이터 볼륨 디스크의 경우에는 ‘**Read Caching**’을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="738e8-152">트랜잭션 로그 볼륨에 대 한 hello 디스크 캐시 설정 해야 너무 '**None**'.</span><span class="sxs-lookup"><span data-stu-id="738e8-152">For Transaction log volumes, hello disk cache setting should be set too‘**None**’.</span></span> <span data-ttu-id="738e8-153">이 표준 저장소 계정에 대 한 권장 사항을 hello와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-153">This is different from hello recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="738e8-154">Hello Vhd를 연결 되 면 hello 캐시 설정을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-154">Once hello VHDs have been attached, hello cache setting cannot be altered.</span></span> <span data-ttu-id="738e8-155">Toodetach 해야 하는 hello VHD 업데이트 된 캐시 설정으로 다시 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-155">You would need toodetach and reattach hello VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="738e8-156">Windows 저장소 공간</span><span class="sxs-lookup"><span data-stu-id="738e8-156">Windows storage spaces</span></span>
<span data-ttu-id="738e8-157">사용할 수 있습니다 [Windows 저장소 공간](https://technet.microsoft.com/library/hh831739.aspx) 이전 표준 저장소에서와 마찬가지로 이렇게 하면 toomigrate 이미 저장소 공간을 활용 하는 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you toomigrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="738e8-158">hello 예제 [부록](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) Powershell 코드 tooextract hello 및 연결 된 vhd를 여러 개를 사용 하 여 VM 가져오기 (단계 9와 앞으로)을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-158">hello example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates hello Powershell code tooextract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="738e8-159">저장소 풀 표준 Azure 저장소 계정 tooenhance 처리량 함께 사용 된 하 고 대기 시간을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-159">Storage Pools were used with Standard Azure storage account tooenhance throughput and reduce latency.</span></span> <span data-ttu-id="738e8-160">새 배포의 경우 프리미엄 저장소에서도 저장소 풀을 사용해 볼 수 있습니다. 그러나 이렇게 하면 저장소 설정이 더 복잡해집니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a><span data-ttu-id="738e8-161">어떻게 toofind는 Azure 가상 디스크 toostorage 풀 매핑</span><span class="sxs-lookup"><span data-stu-id="738e8-161">How toofind which Azure Virtual Disks map toostorage pools</span></span>
<span data-ttu-id="738e8-162">연결 된 Vhd에 대 한 다양 한 캐시 설정을 권장 사항으로 toocopy hello Vhd tooa 프리미엄 저장소 계정을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-162">As there are different cache setting recommendations for attached VHDs, you might decide toocopy hello VHDs tooa Premium Storage account.</span></span> <span data-ttu-id="738e8-163">그러나를 다시 연결을 toohello 새 DS 시리즈 VM tooalter hello 캐시 설정을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-163">However, when you reattach them toohello new DS series VM, you might need tooalter hello cache settings.</span></span> <span data-ttu-id="738e8-164">것이 더 간단한 tooapply hello hello SQL 데이터 파일 및 로그 파일 (아니라 모두 포함 된 단일 VHD)에 대 한 별도 Vhd를 둘 때 프리미엄 저장소 권장 캐시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-164">It is simpler tooapply hello Premium Storage recommended cache settings when you have separate VHDs for hello SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="738e8-165">있는 경우 SQL Server 데이터 및 로그 파일에 hello 동일한 볼륨을 hello 캐싱 옵션을 선택 하면 데이터베이스 작업에 대 한 hello IO 액세스 패턴에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-165">If you have SQL Server data and log files on hello same volume, hello caching option you choose depends on hello IO access patterns for your database workloads.</span></span> <span data-ttu-id="738e8-166">테스트를 통해서만 이 시나리오에 가장 적합한 캐싱 옵션을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-166">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="738e8-167">구성 되는 여러 vhd에 toolook 해야 Windows 저장소 공간을 사용 하는 경우 Vhd를 연결 하 여 원래 스크립트 tooidentify 사항은 어떤 특정 풀에 있으므로 설정할 수 있습니다 hello 캐시 설정에 따라 각 디스크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need toolook at your original scripts tooidentify which attached VHDs are in what specific pool, so you can then set hello cache settings accordingly for each disk.</span></span>

<span data-ttu-id="738e8-168">원래 스크립트 사용 가능한 tooshow 하지 않은 경우 Vhd 매핑할 있습니다 toohello 저장소 풀 hello 다음 단계 toodetermine hello 디스크/저장소 풀 매핑을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-168">If you do not have original script available tooshow you which VHDs map toohello storage pool, you can use hello following steps toodetermine hello disk/storage pool mapping.</span></span>

<span data-ttu-id="738e8-169">각 디스크에 대 한 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-169">For each disk, use hello following steps:</span></span>

1. <span data-ttu-id="738e8-170">디스크의 목록을 가져옵니다 tooVM hello로 연결 된 **Get-azurevm** 명령:</span><span class="sxs-lookup"><span data-stu-id="738e8-170">Get list of disks attached tooVM with hello **Get-AzureVM** command:</span></span>

    <span data-ttu-id="738e8-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="738e8-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="738e8-172">참고 hello Diskname 및 LUN입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-172">Note hello Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="738e8-174">원격 데스크톱 hello VM 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-174">Remote desktop into hello VM.</span></span> <span data-ttu-id="738e8-175">이동 하 여 너무**컴퓨터 관리** | **장치 관리자** | **디스크 드라이브**합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-175">Then go too**Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="738e8-176">각 hello ' Microsoft 가상 디스크의 ' hello 속성을 보고</span><span class="sxs-lookup"><span data-stu-id="738e8-176">Look at hello properties of each of hello ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="738e8-178">hello LUN 번호를 여기에 hello VHD toohello VM을 연결할 때 지정한 참조 toohello LUN 숫자가입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-178">hello LUN number here is a reference toohello LUN number you specify when attaching hello VHD toohello VM.</span></span>
5. <span data-ttu-id="738e8-179">' Microsoft 가상 디스크 ' hello에 대 한 이동 toohello **세부 정보** hello 다음 탭 **속성** 목록에서 이동 너무**드라이버 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-179">For hello ‘Microsoft Virtual Disk’ go toohello **Details** tab, then in hello **Property** list, go too**Driver Key**.</span></span> <span data-ttu-id="738e8-180">Hello에 **값**, 참고 hello **오프셋**, 스크린 샷 다음 hello에 0002 변수인 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-180">In hello **Value**, note hello **Offset**, which is 0002 in hello following screenshot.</span></span> <span data-ttu-id="738e8-181">hello를 0002 hello를 PhysicalDisk2 hello 저장소 풀에 대 한 참조를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-181">hello 0002 denotes hello PhysicalDisk2 that hello storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="738e8-183">각 저장소 풀에 대 한 덤프 hello 아웃 연결 된 디스크가:</span><span class="sxs-lookup"><span data-stu-id="738e8-183">For each storage pool, dump out hello associated disks:</span></span>

    <span data-ttu-id="738e8-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="738e8-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="738e8-186">에서는 이제 정보 tooassociate이 연결 된 저장소 풀의 Vhd tooPhysical 디스크.</span><span class="sxs-lookup"><span data-stu-id="738e8-186">Now you can use this information tooassociate attached VHDs tooPhysical Disks in Storage Pools.</span></span>

<span data-ttu-id="738e8-187">Vhd tooPhysical 디스크 저장소 풀에 매핑한 후 다음 분리 및 tooa 프리미엄 저장소 계정에 다음 수를 설정 하는 hello 올바른 캐시와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-187">Once you have mapped VHDs tooPhysical Disks in Storage Pools you can then detach and copy them over tooa Premium Storage account, then attach them with hello correct cache setting.</span></span> <span data-ttu-id="738e8-188">Hello hello 예제를 참조 하십시오 [부록](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), 8-12 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-188">Please see hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="738e8-189">이러한 단계는 어떻게 tooextract VM에 연결 된 VHD 디스크 구성 tooa CSV 파일의 경우 hello Vhd를 복사, 변경 hello 디스크 구성 캐시 설정 하 고 마지막으로 모든 hello로 DS 시리즈 VM 디스크를 연결 hello VM을 다시 배포를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-189">These steps show how tooextract a VM-attached VHD disk configuration tooa CSV file, copy hello VHDs, alter hello disk configuration cache settings, and finally redeploy hello VM as a DS series VM with all hello attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="738e8-190">VM 저장소 대역폭 및 VHD 저장소 처리량</span><span class="sxs-lookup"><span data-stu-id="738e8-190">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="738e8-191">저장소 성능의 양이 hello hello 지정 되며 hello VHD 크기 DS VM 크기에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-191">hello amount of storage performance depends on hello DS* VM size specified and hello VHD sizes.</span></span> <span data-ttu-id="738e8-192">hello Vm hello 연결 하 고 최대 대역폭 (MB/s) 지원함 hello 가능한 Vhd 수에 대 한 다른 허용 한도 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-192">hello VMs have different allowances for hello number of VHDs that can be attached and hello maximum bandwidth they will support (MB/s).</span></span> <span data-ttu-id="738e8-193">Hello 특정 대역폭 번호에 대 한 참조 [가상 컴퓨터와 Azure 클라우드 서비스 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-193">For hello specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="738e8-194">디스크가 클수록 IOPS가 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-194">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="738e8-195">마이그레이션 경로를 고려할 때는 이 점에 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-195">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="738e8-196">자세한 내용은 [IOPS 및 디스크 유형에 대 한 hello 표를 참조 하세요.](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets)합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-196">For details, [see hello table for IOPS and Disk Types](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="738e8-197">마지막으로, VM이 연결된 모든 디스크에 대해 지원하는 최대 디스크 대역폭이 서로 다르다는 점도 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span></span> <span data-ttu-id="738e8-198">부하가 높거나 hello 해당 VM 역할 크기에 사용할 수 있는 최대 디스크 대역폭을 포화 상태로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-198">Under high load, you could saturate hello maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="738e8-199">예를 들어 한 Standard_DS14 too512MB/s;를 지원 합니다. 따라서 세 개의 P30 디스크와 hello VM의 hello 디스크 대역폭을 포화 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-199">For example a Standard_DS14 will support up too512MB/s; therefore, with three P30 disks you could saturate hello disk bandwidth of hello VM.</span></span> <span data-ttu-id="738e8-200">하지만이 예제에서는 hello 처리량 한도의 읽기 및 쓰기 IOs hello 조합에 따라 초과 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-200">But in this example, hello throughput limit could be exceeded depending on hello mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="738e8-201">새 배포</span><span class="sxs-lookup"><span data-stu-id="738e8-201">New deployments</span></span>
<span data-ttu-id="738e8-202">hello 다음 두 섹션에서는 SQL Server Vm tooPremium 저장소를 배포 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-202">hello next two sections demonstrate how you can deploy SQL Server VMs tooPremium Storage.</span></span> <span data-ttu-id="738e8-203">앞서 언급 했 듯이 반드시 불필요 tooplace hello OS 디스크 프리미엄 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-203">As mentioned before, you do not necessarily need tooplace hello OS disk onto Premium storage.</span></span> <span data-ttu-id="738e8-204">경우 선택할 수 있습니다 toodo이 아니도록 tooplace 모든 IO가 많은 작업용 hello OS VHD에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-204">You might choose toodo this if you are intending tooplace any intensive IO workloads on hello OS VHD.</span></span>

<span data-ttu-id="738e8-205">hello 첫 번째 예에서는 기존 Azure 갤러리 이미지를 사용 하 여 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-205">hello first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="738e8-206">hello 두 번째 예제에서는 어떻게 toouse 사용자 지정 VM 이미지는 기존 표준 저장소 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-206">hello second example shows how toouse a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="738e8-207">이러한 예제에서는 지역 VNET을 이미 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-207">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="738e8-208">갤러리 이미지를 사용하여 프리미엄 저장소에서 새 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="738e8-208">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="738e8-209">다음 예제에서는 hello tooplace 프리미엄 저장소에 운영 체제 VHD hello 하 고 프리미엄 저장소 Vhd를 연결 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-209">hello example below shows how tooplace hello OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="738e8-210">그러나 표준 저장소 계정에 hello OS 디스크를 배치할 수도 수 있으며 프리미엄 저장소 계정에 있는 Vhd를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-210">However, you can also place hello OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="738e8-211">여기서는 두 시나리오를 모두 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-211">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="738e8-212">1단계: 프리미엄 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="738e8-212">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="738e8-213">2단계: 새 클라우드 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="738e8-213">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="738e8-214">3단계: 클라우드 서비스 VIP 예약(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="738e8-214">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="738e8-215">4단계: VM 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="738e8-215">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="738e8-216">5단계: 표준 또는 프리미엄 저장소에 OS VHD 배치</span><span class="sxs-lookup"><span data-stu-id="738e8-216">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="738e8-217">6단계: VM 만들기</span><span class="sxs-lookup"><span data-stu-id="738e8-217">Step 6: Create VM</span></span>
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a><span data-ttu-id="738e8-218">사용자 지정 이미지를 사용 하 여 새 VM toouse 프리미엄 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="738e8-218">Create a new VM toouse Premium Storage with a custom image</span></span>
<span data-ttu-id="738e8-219">이 시나리오에서는 표준 저장소 계정에 기존의 사용자 지정된 이미지가 있는 경우를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="738e8-220">설명 했 듯이에서 tooplace hello OS VHD 원하는 toocopy 해야 하는 프리미엄 저장소는 hello hello 표준 저장소 계정에에서 있는 이미지를 하 고 사용 하려면 먼저 tooa 프리미엄 저장소 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-220">As mentioned if you want tooplace hello OS VHD on Premium Storage you will need toocopy hello image that exists in hello Standard Storage account and transfer them tooa Premium Storage before it can be used.</span></span> <span data-ttu-id="738e8-221">이미지 온-프레미스, 있습니다 수 있는 경우 또한 메서드 toocopy이를 사용 하 여 직접 toohello 프리미엄 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-221">If you have an image on-premises, you can also use this method toocopy that directly toohello Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="738e8-222">1단계: 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="738e8-222">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="738e8-223">2단계: 클라우드 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="738e8-223">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="738e8-224">3단계: 기존 이미지 사용</span><span class="sxs-lookup"><span data-stu-id="738e8-224">Step 3: Use existing image</span></span>
<span data-ttu-id="738e8-225">기존 이미지를 사용할 수 있으며</span><span class="sxs-lookup"><span data-stu-id="738e8-225">You can use an existing image.</span></span> <span data-ttu-id="738e8-226">[기존 컴퓨터의 이미지를 사용](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="738e8-227">참고 hello 컴퓨터를 이미지로 toobe DS * 컴퓨터는 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-227">Note hello machine you image does not have toobe DS* machine.</span></span> <span data-ttu-id="738e8-228">Hello 이미지를 만든 후 hello 단계 표시 방법을 따르는 toocopy 것 toohello hello로 프리미엄 저장소 계정 **시작 AzureStorageBlobCopy** PowerShell commandlet 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-228">Once you have hello image, hello following steps show how toocopy it toohello Premium Storage account with hello **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="738e8-229">4단계: 저장소 계정 간에 Blob 복사</span><span class="sxs-lookup"><span data-stu-id="738e8-229">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="738e8-230">5단계: 정기적으로 복사 상태 확인</span><span class="sxs-lookup"><span data-stu-id="738e8-230">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a><span data-ttu-id="738e8-231">6 단계: 이미지 디스크 tooAzure 디스크 저장소를 구독에 추가</span><span class="sxs-lookup"><span data-stu-id="738e8-231">Step 6: Add Image disk tooAzure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="738e8-232">hello 상태를 성공으로 보고 하는 경우에 여전히 오류가 나타날 수 있습니다는 디스크 임대를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-232">You may find that even though hello status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="738e8-233">이 경우 10분 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-233">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-hello-vm"></a><span data-ttu-id="738e8-234">7 단계: 빌드 hello VM</span><span class="sxs-lookup"><span data-stu-id="738e8-234">Step 7:  Build hello VM</span></span>
<span data-ttu-id="738e8-235">여기 작성 하는 hello VM 이미지 및 연결 하는 두 개의 프리미엄 저장소 Vhd에서:</span><span class="sxs-lookup"><span data-stu-id="738e8-235">Here you are building hello VM from your image and attaching two Premium Storage VHDs:</span></span>

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="738e8-236">Always On 가용성 그룹을 사용하지 않는 기존 배포</span><span class="sxs-lookup"><span data-stu-id="738e8-236">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="738e8-237">기존 배포에 대 한 hello 가장 먼저 표시 [필수 구성 요소](#prerequisites-for-premium-storage) 이 항목의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-237">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="738e8-238">Always On 가용성 그룹 사용 여부에 따라 SQL Server 배포 관련 고려 사항이 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="738e8-239">기존의 독립 실행형 SQL Server, 있고에서 항상 사용 하지 않는 경우에 새 클라우드 서비스와 저장소 계정을 사용 하 여 tooPremium 저장소를 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade tooPremium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="738e8-240">hello 다음 옵션을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-240">Consider hello following options:</span></span>

* <span data-ttu-id="738e8-241">**새 SQL Server VM 만들기**.</span><span class="sxs-lookup"><span data-stu-id="738e8-241">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="738e8-242">새 배포에서 설명하는 것처럼 프리미엄 저장소 계정을 사용하는 새 SQL Server VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="738e8-243">그런 후에 SQL Server 구성과 사용자 데이터베이스를 백업 및 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-243">Then backup and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="738e8-244">hello 진행 되는 업데이트 toobe tooreference hello 새 SQL Server 내부 또는 외부에서 액세스 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="738e8-244">hello application will need toobe updated tooreference hello new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="738e8-245">나란히 (SxS) SQL Server 마이그레이션 하 던 마치 toocopy 'db'에서 개체를 모두 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-245">You would need toocopy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="738e8-246">여기에는 로그인, 인증서, 연결된 서버 등의 개체도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-246">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="738e8-247">**기존 SQL Server VM 마이그레이션**.</span><span class="sxs-lookup"><span data-stu-id="738e8-247">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="738e8-248">이 SQL Server VM hello를 오프 라인 상태로 전환 후 해당 연결 된 Vhd toohello 프리미엄 저장소 계정의 모든 복사 포함 tooa 새 클라우드 서비스를 전송 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-248">This will require taking hello SQL Server VM offline, then transferring it tooa new cloud service, which includes copying all of its attached VHDs toohello Premium Storage account.</span></span> <span data-ttu-id="738e8-249">Hello VM 온라인 상태가 되 면 hello 응용 프로그램 하기 전에 hello 서버 호스트 이름으로 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-249">When hello VM comes online, hello application will reference hello server host name as before.</span></span> <span data-ttu-id="738e8-250">주의 hello 기존 디스크의 hello 크기 hello 성능 특성에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-250">Be aware that hello size of hello existing disk will affect hello performance characteristics.</span></span> <span data-ttu-id="738e8-251">예를 들어 400GB 디스크 tooa P20 반올림을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-251">For example, a 400 GB disk gets rounded up tooa P20.</span></span> <span data-ttu-id="738e8-252">디스크 성능에 주는 필요 하지 않은 경우, hello DS 시리즈 VM으로 VM을 다시 만드는 및 필요한 hello 크기/성능 사양의 프리미엄 저장소 Vhd 연결 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-252">If you know that you do not require that disk performance, then you could recreate hello VM as a DS Series VM, and attach Premium Storage VHDs of hello size/performance specification you require.</span></span> <span data-ttu-id="738e8-253">그런 다음 분리 하 고 hello SQL DB 파일 다시 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-253">Then you could detach and reattach hello SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="738e8-254">프리미엄 저장소 디스크 형식을 인해 hello 크기에 따라 hello 크기를 알고 있어야 하는 hello VHD 디스크를 복사 하는 경우에 해당, 디스크 성능 사양 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-254">When copying hello VHD disks you should be aware of hello size, depending on hello size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="738e8-255">400 50GB 디스크를 사용 하도록 설정한 경우이 반올림 되 tooa P20 하므로 라운드 azure는 디스크에 가장 가까운 toohello 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-255">Azure will round up toohello nearest disk size, so if you have a 400GB disk, this will be rounded up tooa P20.</span></span> <span data-ttu-id="738e8-256">필요에 따라 기존 IO hello OS VHD의 않아도 toomigrate이이 tooa 프리미엄 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-256">Depending on your existing IO requirements of hello OS VHD, you might not need toomigrate this tooa Premium Storage account.</span></span>
>
>

<span data-ttu-id="738e8-257">SQL Server 외부에서 액세스 하는 경우 클라우드 서비스 VIP hello 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-257">If your SQL Server is accessed externally, then hello cloud service VIP will change.</span></span> <span data-ttu-id="738e8-258">Tooupdate 끝점, Acl 및 DNS를 갖게 됩니다 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-258">You will also have tooupdate end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="738e8-259">Always On 가용성 그룹을 사용하는 기존 배포</span><span class="sxs-lookup"><span data-stu-id="738e8-259">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="738e8-260">기존 배포에 대 한 hello 가장 먼저 표시 [필수 구성 요소](#prerequisites-for-premium-storage) 이 항목의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-260">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="738e8-261">이 섹션에서는 먼저 Always On이 Azure 네트워킹과 상호 작용하는 방식을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="738e8-262">우리는 나눠서 tootwo 시나리오에서 마이그레이션: 마이그레이션 가동 중지 시간이 허용 될 수 및 마이그레이션을 최소한의 가동 중지 시간을 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-262">We will then break down migrations in tootwo scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="738e8-263">온-프레미스 SQL Server Always On 가용성 그룹은 하나 이상의 SQL Server 간에 공유되는 IP 주소와 함께 가상 DNS 이름을 등록하는 온-프레미스 수신기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="738e8-264">클라이언트가 연결할 때 hello 수신기 IP toohello 주 SQL Server를 통해 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-264">When clients connect they are routed through hello listener IP toohello Primary SQL Server.</span></span> <span data-ttu-id="738e8-265">그 당시 hello 항상 IP 리소스를 소유 하는 hello 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-265">This is hello server that owns hello Always On IP resource at that time.</span></span>

![DeploymentsUseAlways On][6]

<span data-ttu-id="738e8-267">Microsoft Azure에서 하나의 IP 주소 할당 tooa NIC VM hello에에 tooachieve hello 동일한 추상화 계층을 온-프레미스로, toohello 내부/외부 부하 분산 장치 (ILB/ELB) 할당 된 IP 주소를 hello를 활용 하는 Azure 주문 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-267">In Microsoft Azure you can have only one IP address assigned tooa NIC on hello VM, so in order tooachieve hello same layer of abstraction as on-premises, Azure utilizes hello IP address that is assigned toohello Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="738e8-268">hello 서버 간에 공유 되는 hello IP 리소스 toohello 설정 되어 hello ILB/ELB으로 동일한 IP입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-268">hello IP resource that is shared between hello servers is set toohello same IP as hello ILB/ELB.</span></span> <span data-ttu-id="738e8-269">이것은 hello DNS에에서 게시 및 hello ILB/ELB toohello 주 SQL Server 복제 데이터베이스를 통해 클라이언트 트래픽을 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-269">This is published in hello DNS, and client traffic is passed through hello ILB/ELB toohello Primary SQL Server replica.</span></span> <span data-ttu-id="738e8-270">ILB/ELB hello 프로브 tooprobe hello 항상 IP 리소스를 사용 하므로 SQL Server가 기본를 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-270">hello ILB/ELB knows which SQL Server is primary since it uses probes tooprobe hello Always On IP resource.</span></span> <span data-ttu-id="738e8-271">Hello 이전 예제에서는 hello ELB/ILB에서 참조 하는 끝점이 있는 각 노드를 검색, hello 주 SQL Server가 응답 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-271">In hello previous example, it probes each node that has an endpoint referenced by hello ELB/ILB, whichever responds is hello Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="738e8-272">hello ILB 및 ELB 둘 다 할당 tooa 특정 Azure 클라우드 서비스, 따라서 Azure에서 클라우드 마이그레이션을 대개 것을 의미 합니다 해당 hello 부하 분산 장치 IP가 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-272">hello ILB and ELB are both assigned tooa particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that hello Load Balancer IP will change.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="738e8-273">어느 정도의 가동 중지 시간이 발생해도 되는 Always On 배포 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="738e8-273">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="738e8-274">두 가지 전략 toomigrate Always On 하는 배포에 대 한 가동 중지 시간이 허용:</span><span class="sxs-lookup"><span data-stu-id="738e8-274">There are two strategies toomigrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="738e8-275">**기존 클러스터에서 항상 더 많은 보조 복제본 tooan 추가**</span><span class="sxs-lookup"><span data-stu-id="738e8-275">**Add more secondary replicas tooan existing Always On Cluster**</span></span>
2. <span data-ttu-id="738e8-276">**Tooa 마이그레이션 새 항상에 클러스터**</span><span class="sxs-lookup"><span data-stu-id="738e8-276">**Migrate tooa new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a><span data-ttu-id="738e8-277">1. 더 많은 보조 복제본 tooan 추가 기존 항상에 클러스터</span><span class="sxs-lookup"><span data-stu-id="738e8-277">1. Add more Secondary Replicas tooan Existing Always On Cluster</span></span>
<span data-ttu-id="738e8-278">한 가지 전략은 tooadd 더 많은 보조 toohello Always On 가용성 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-278">One strategy is tooadd more secondaries toohello Always On Availability Group.</span></span> <span data-ttu-id="738e8-279">이 필드는 새 클라우드 서비스를 tooadd 필요 하 고이 정보를 hello 새 부하 분산 장치 ip hello 수신기를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-279">You need tooadd these into a new cloud service and update hello listener with hello new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="738e8-280">가동 중지 시간 발생 시점:</span><span class="sxs-lookup"><span data-stu-id="738e8-280">Points of downtime:</span></span>
* <span data-ttu-id="738e8-281">클러스터 유효성 검사 시</span><span class="sxs-lookup"><span data-stu-id="738e8-281">Cluster Validation.</span></span>
* <span data-ttu-id="738e8-282">새 보조 복제본에 대해 Always On 장애 조치(failover) 테스트 시</span><span class="sxs-lookup"><span data-stu-id="738e8-282">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="738e8-283">IO 처리량이 늘어나며에 대 한 hello VM 내에서 Windows 저장소 풀을 사용 하는 경우 다음 이러한 오프 라인 전체 클러스터 유효성 검사 중입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-283">If you are using Windows Storage Pools within hello VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="738e8-284">hello 유효성 검사 테스트를 toohello 클러스터 노드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-284">hello validation test is required when you add nodes toohello cluster.</span></span> <span data-ttu-id="738e8-285">에서 테스트 해야이 대표 테스트 환경 tooget이 소요 될 경우 대략적인 시간이 있도록 toorun hello 테스트 hello 시간 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-285">hello time it takes toorun hello test can vary, so you should test this in your representative test environment tooget an approximate time of how long this will take.</span></span>

<span data-ttu-id="738e8-286">수동 장애 조치를 수행할 수 예상 대로 chaos 새로 hello에 대 한 테스트 추가 노드 tooensure Always On 고가용성 함수 시간 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-286">You should provision time where you can perform manual failover and chaos testing on hello newly added nodes tooensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="738e8-288">Hello 유효성 검사를 실행 하기 전에 hello 저장소 풀이 사용 되는 SQL Server의 모든 인스턴스를 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-288">You should stop all instances of SQL Server where hello Storage Pools are used before hello Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="738e8-289">대략적인 단계</span><span class="sxs-lookup"><span data-stu-id="738e8-289">High-level steps</span></span>
>

1. <span data-ttu-id="738e8-290">프리미엄 저장소가 연결된 새 클라우드 서비스에 SQL Server 두 개를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="738e8-291">**NORECOVERY**를 사용하여 전체 백업 및 복원을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-291">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="738e8-292">로그인 등의 사용자 DB 외부에 있는 종속 개체를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="738e8-293">새 ILB(내부 부하 분산 장치) 또는 ELB(외부 부하 분산 장치)를 만든 다음 두 새 노드에 모두 부하 분산된 끝점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="738e8-294">계속 하기 전에 모든 노드에 있는 hello 올바른 끝점 구성을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="738e8-294">Check all Nodes have hello correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="738e8-295">(저장소 풀을 사용 하 여) 하는 경우에 사용자/응용 프로그램 액세스 toohello SQL Server를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-295">Stop User/Application Access toohello SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="738e8-296">저장소 풀을 사용 중인 경우 모든 노드에서 SQL Server Engine Services를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="738e8-297">새 노드 toocluster를 추가 하 고 전체 유효성 검사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-297">Add new Nodes toocluster and run full validation.</span></span>
8. <span data-ttu-id="738e8-298">유효성 검사가 정상적으로 완료되면 모든 SQL Server 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-298">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="738e8-299">트랜잭션 로그를 백업하고 사용자 데이터베이스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-299">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="738e8-300">Hello Always On 가용성 그룹에 새 노드를 추가 하 고 복제에 놓으십시오 **동기**합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-300">Add new nodes into hello Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="738e8-301">추가 hello IP 주소 리소스의 hello 새 클라우드 서비스 ILB/ELB Always On에 대 한 PowerShell 통해 hello에 hello 다중 사이트 예제에 따라 [부록](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-301">Add hello IP address resource of hello new Cloud Service ILB/ELB through PowerShell for Always On based on hello Multi-site example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span> <span data-ttu-id="738e8-302">Windows 클러스터링에서 hello 설정 **가능한 소유자** 의 hello **IP 주소** 리소스 toohello 새 노드 이전 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-302">In Windows clustering, set hello **Possible owners** of hello **IP Address** resource toohello new nodes old.</span></span> <span data-ttu-id="738e8-303">Hello의 hello '동일한 서브넷에 IP 주소 리소스를 추가' 섹션을 참조 [부록](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-303">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="738e8-304">새 노드 hello tooone 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-304">Failover tooone of hello new nodes.</span></span>
13. <span data-ttu-id="738e8-305">새 노드 자동 장애 조치 파트너 hello를 확인 하 고 테스트 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-305">Make hello new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="738e8-306">가용성 그룹에서 원래 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-306">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="738e8-307">장점</span><span class="sxs-lookup"><span data-stu-id="738e8-307">Advantages</span></span>
* <span data-ttu-id="738e8-308">새 SQL Server 일 수 있습니다 (SQL Server와 응용 프로그램) tooAlways에 추가 하기 전에 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-308">New SQL Servers can be tested (SQL Server and Application) before they are added tooAlways On.</span></span>
* <span data-ttu-id="738e8-309">Hello VM 크기를 변경할 수 있으며 hello 저장소 tooyour 정확한 요구 사항을 사용자 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-309">You can change hello VM size and customize hello storage tooyour exact requirements.</span></span> <span data-ttu-id="738e8-310">그러나는 것이 유용한 tookeep 모든 hello SQL 파일 경로 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-310">However, it would be beneficial tookeep all hello SQL file paths hello same.</span></span>
* <span data-ttu-id="738e8-311">Hello DB 백업 toohello 보조 복제본의 hello 전송을 시작 시기를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-311">You can control when hello transfer of hello DB backups toohello Secondary Replicas are started.</span></span> <span data-ttu-id="738e8-312">Azure를 사용 하 여이 점에서 차이가 **시작 AzureStorageBlobCopy** commandlet toocopy Vhd 비동기 복사본 이므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet toocopy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="738e8-313">단점</span><span class="sxs-lookup"><span data-stu-id="738e8-313">Disadvantages</span></span>
* <span data-ttu-id="738e8-314">Windows 저장소 풀을 사용 하면 hello 새 노드를 추가할 hello 전체 클러스터 유효성 검사 하는 동안 클러스터 가동 중지 시간이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-314">When using Windows Storage Pools, there is Cluster downtime during hello Full Cluster Validation for hello new additional nodes.</span></span>
* <span data-ttu-id="738e8-315">SQL Server 버전 hello 및 보조 복제본의 hello 기존 수에 따라 있습니다 않을 수도 있습니다 수 tooadd 기존 보조 복제본을 제거 하지 않고 이상의 보조 복제본 수입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-315">Depending on hello SQL Server Version and hello existing number of secondary replicas, you might not be able tooadd more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="738e8-316">SQL 데이터 전송 시간이 hello 보조 데이터베이스를 설정 하는 동안 오래 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-316">There could be long SQL data transfer time while setting up hello secondaries.</span></span>
* <span data-ttu-id="738e8-317">새 컴퓨터를 병렬로 실행하면 마이그레이션 중에 추가 비용이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-317">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-tooa-new-always-on-cluster"></a><span data-ttu-id="738e8-318">2. Tooa 마이그레이션 새 항상에 클러스터</span><span class="sxs-lookup"><span data-stu-id="738e8-318">2. Migrate tooa new Always On Cluster</span></span>
<span data-ttu-id="738e8-319">새 클라우드 서비스 및 리디렉션 hello 클라이언트 toouse toocreate 새로운 항상에 노드가 있는 클러스터 새로운는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-319">Another strategy is toocreate a brand new Always On Cluster with brand new nodes in new cloud service and then redirect hello clients toouse it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="738e8-320">가동 중지 시간 발생 시점</span><span class="sxs-lookup"><span data-stu-id="738e8-320">Points of downtime</span></span>
<span data-ttu-id="738e8-321">응용 프로그램 및 사용자 toohello 새 Always On 수신기를 전송할 때 가동 중지 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-321">There is downtime when you transfer applications and users toohello new Always On listener.</span></span> <span data-ttu-id="738e8-322">hello 가동 중지 시간에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-322">hello downtime depends on:</span></span>

* <span data-ttu-id="738e8-323">새 서버에 toorestore 마지막 트랜잭션 로그 백업을 toodatabases를 사용한 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-323">hello time taken toorestore final transaction log backups toodatabases on new servers.</span></span>
* <span data-ttu-id="738e8-324">hello에 걸린 시간 tooupdate 클라이언트 응용 프로그램 toouse 새 Always On 수신기 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-324">hello time taken tooupdate client applications toouse new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="738e8-325">장점</span><span class="sxs-lookup"><span data-stu-id="738e8-325">Advantages</span></span>
* <span data-ttu-id="738e8-326">Hello 실제 프로덕션 환경에서는 SQL Server를 테스트할 수 있으며, OS 빌드 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-326">You can test hello actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="738e8-327">Hello 옵션 toocustomize hello 저장소 있고 toopotentially VM의 크기를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-327">You have hello option toocustomize hello storage and toopotentially reduce size of VM.</span></span> <span data-ttu-id="738e8-328">따라서 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-328">This could result in cost reduction.</span></span>
* <span data-ttu-id="738e8-329">이 과정에서 SQL Server 빌드 또는 버전을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-329">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="738e8-330">Hello 운영 체제를 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-330">You can also upgrade hello Operating System.</span></span>
* <span data-ttu-id="738e8-331">hello 이전 항상에 클러스터 단색 롤백 대상으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-331">hello previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="738e8-332">단점</span><span class="sxs-lookup"><span data-stu-id="738e8-332">Disadvantages</span></span>
* <span data-ttu-id="738e8-333">두 Always On 클러스터 모두 동시에 실행 하려는 경우 hello 수신기의 toochange hello DNS 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-333">You need toochange hello DNS name of hello listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="738e8-334">클라이언트 응용 프로그램 문자열 hello 새 수신기 이름을 반영 해야 관리 hello 마이그레이션하는 동안 오버 헤드가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-334">This adds administration overhead during hello migration as client application strings must reflect hello new Listener name.</span></span>
* <span data-ttu-id="738e8-335">Hello로 마이그레이션 시작 하기 전에 가능한 toominimize hello 최종 동기화 요구 사항으로 닫습니다는 두 개의 환경 tookeep 간의 동기화 메커니즘을 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-335">You must implement a synchronization mechanism between hello two environments tookeep them as close as possible toominimize hello final synchronization requirements before migration.</span></span>
* <span data-ttu-id="738e8-336">실행 하는 hello 새 환경을 사용 하는 동안 마이그레이션하는 동안 비용이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-336">There is added cost during migration while you have hello new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="738e8-337">가동 중지 시간을 최소화해야 하는 Always On 배포 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="738e8-337">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="738e8-338">가동 중지 시간을 최소화해야 하는 Always On 배포를 마이그레이션할 때는 두 가지 전략을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-338">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="738e8-339">**기존 보조 복제본 활용: 단일 사이트**</span><span class="sxs-lookup"><span data-stu-id="738e8-339">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="738e8-340">**기존 보조 복제본 활용: 다중 사이트**</span><span class="sxs-lookup"><span data-stu-id="738e8-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="738e8-341">1. 기존 보조 복제본 활용: 단일 사이트</span><span class="sxs-lookup"><span data-stu-id="738e8-341">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="738e8-342">최소한의 가동 중지 시간에 대 한 한 가지 전략 tootake 보조 기존 클라우드 이며 hello 현재 클라우드 서비스에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-342">One strategy for minimal downtime is tootake an existing cloud secondary and remove it from hello current cloud service.</span></span> <span data-ttu-id="738e8-343">다음 Vhd toohello 새 프리미엄 저장소 계정을 hello를 복사 하 고 hello 새 클라우드 서비스에서 VM hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-343">Then copy hello VHDs toohello new Premium Storage account, and create hello VM in hello new cloud service.</span></span> <span data-ttu-id="738e8-344">클러스터링 및 장애 조치 hello 수신기를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-344">Then update hello listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="738e8-345">가동 중지 시간 발생 시점</span><span class="sxs-lookup"><span data-stu-id="738e8-345">Points of downtime</span></span>
* <span data-ttu-id="738e8-346">Hello 부하 분산 된 끝점이 있는 hello 마지막 노드를 업데이트할 때 가동 중지 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-346">There is downtime when you update hello final node with hello Load Balanced endpoint.</span></span>
* <span data-ttu-id="738e8-347">클라이언트/DNS 구성에 따라 클라이언트 다시 연결이 지연될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="738e8-348">Tootake hello 항상 클러스터 그룹 오프 라인 tooswap hello IP 주소를 선택 하는 경우 작동 중단 시간이 추가로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-348">There is additional downtime if you choose tootake hello Always On Cluster group offline tooswap out hello IP addresses.</span></span> <span data-ttu-id="738e8-349">OR 종속성을 사용 하 여이 방지 하려면 및 가능한 소유자 hello에 대 한 IP 주소 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-349">You can avoid this by using an OR dependency and Possible Owners for hello added IP Address resource.</span></span> <span data-ttu-id="738e8-350">Hello의 hello '동일한 서브넷에 IP 주소 리소스를 추가' 섹션을 참조 [부록](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-350">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="738e8-351">항상에 장애 조치 파트너에 추가 된 노드가 toopartake hello를 원하는 Azure 부하 분산 된 설정 참조가 toohello 끝점 tooadd가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-351">When you want hello added node toopartake in as an Always On Failover Partner, you need tooadd an Azure Endpoint with a reference toohello Load Balanced Set.</span></span> <span data-ttu-id="738e8-352">Hello를 실행 하는 경우 **Add-azureendpoint** toodo 열려이, 현재 연결 tooremain 명령 되지만 새 연결 toohello 수신기 수 toobe hello 부하 분산 장치에 업데이트 될 때까지 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-352">When you run hello **Add-AzureEndpoint** command toodo this, current connections tooremain open, but new connections toohello listener will not be able toobe established until hello load balancer has updated.</span></span> <span data-ttu-id="738e8-353">이것이 표시 toolast 90 120seconds 테스트, 테스트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-353">In testing this was seen toolast 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="738e8-354">장점</span><span class="sxs-lookup"><span data-stu-id="738e8-354">Advantages</span></span>
* <span data-ttu-id="738e8-355">마이그레이션 중에 추가 비용이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-355">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="738e8-356">일대일 마이그레이션입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-356">A one-to-one migration.</span></span>
* <span data-ttu-id="738e8-357">복잡성이 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-357">Reduced complexity.</span></span>
* <span data-ttu-id="738e8-358">프리미엄 저장소 SKU에서 보다 높아진 IOPS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-358">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="738e8-359">디스크 hello VM에서에서 분리 되 고 toohello 새 클라우드 서비스를 복사 하는 hello 타사 도구는 더 높은 처리량을 제공 하는 사용 되는 tooincrease hello VHD 크기 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-359">When hello disks are detached from hello VM and copied toohello new cloud service, a 3rd party tool can be used tooincrease hello VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="738e8-360">VHD 크기를 늘리는 방법에 대한 자세한 내용은 이 [포럼 토론](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="738e8-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="738e8-361">단점</span><span class="sxs-lookup"><span data-stu-id="738e8-361">Disadvantages</span></span>
* <span data-ttu-id="738e8-362">마이그레이션 중에 HA 및 DR이 일시적으로 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-362">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="738e8-363">1:1 마이그레이션 이것이 지 원하는 Vhd 수가 수 toodownsize 수 있도록 Vm에 최소 VM 크기 toouse 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-363">As this is a 1:1 migration, you will have toouse a minimum VM size that will support your number of VHDs, so you might not be able toodownsize your VMs.</span></span>
* <span data-ttu-id="738e8-364">이 시나리오는 hello Azure를 사용 하 여 **시작 AzureStorageBlobCopy** 는 비동기적인 commandlet 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-364">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="738e8-365">복사 완료에 대한 SLA는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-365">There is no SLA on copy completion.</span></span> <span data-ttu-id="738e8-366">이 또한 데이터 tootransfer 양을 hello에 따라서도 달라질 큐에 대기에 따라 결정 하는 동안 hello 복사본의 hello 시간은 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-366">hello time of hello copies varies, while this depends on wait in queue it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="738e8-367">hello 복사 시간이 되는 경우 hello 전송 다른 지역에서 프리미엄 저장소를 지 원하는 tooanother Azure 데이터 센터에 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-367">hello copy time increases if hello transfer is going tooanother Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="738e8-368">노드 2 개를 방금 설정한 경우 hello 복사 테스트 보다 오래 걸리는 경우에 대비 가능한 완화를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-368">If you just have 2 nodes, consider a possible mitigation in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="738e8-369">여기에 다음 아이디어 hello를 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-369">This could include hello following ideas.</span></span>
  * <span data-ttu-id="738e8-370">HA에 대 한 가동 중지 시간을 합의 된 hello 마이그레이션을 시작 하기 전에 3 번째 임시 SQL Server 노드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-370">Add a temporary 3rd SQL Server node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="738e8-371">예약 된 유지 관리 Azure hello 마이그레이션을 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="738e8-371">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="738e8-372">클러스터 쿼럼을 올바르게 구성했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-372">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="738e8-373">대략적인 단계</span><span class="sxs-lookup"><span data-stu-id="738e8-373">High-level steps</span></span>
<span data-ttu-id="738e8-374">그러나이 문서는 완전 tooend 예를 보여 주지 않습니다 hello [부록](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) 이 tooperform 사용된 될 수 있는 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-374">This document does not demonstrate a complete end tooend example, however hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged tooperform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="738e8-376">수집 디스크 구성과 hello 노드 제거 (연결 된 Vhd를 삭제 하지 않음).</span><span class="sxs-lookup"><span data-stu-id="738e8-376">Gather disk configuration, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="738e8-377">프리미엄 저장소 계정을 만들고 hello 표준 저장소 계정에서에서 Vhd를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-377">Create a Premium Storage account and copy VHDs from hello Standard Storage account</span></span>
* <span data-ttu-id="738e8-378">새 클라우드 서비스를 만들고 해당 클라우드 서비스에 hello SQL2 VM을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-378">Create new cloud service and redeploy hello SQL2 VM in that cloud service.</span></span> <span data-ttu-id="738e8-379">Hello VM 만들기 hello를 사용 하 여 원래 운영 체제 VHD를 복사 하 고 Vhd 복사 hello를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-379">Create hello VM using hello copied original OS VHD and attaching hello copied VHDs.</span></span>
* <span data-ttu-id="738e8-380">ILB/ELB를 구성하고 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="738e8-380">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="738e8-381">다음 중 하나를 수행하여 수신기 업데이트</span><span class="sxs-lookup"><span data-stu-id="738e8-381">Update Listener by either:</span></span>
  * <span data-ttu-id="738e8-382">Always On 그룹 hello 라인 오프 라인 및 업데이트 hello 항상에 수신기 새 ilb / ELB IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-382">Taking hello Always On Group offline and updating hello Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="738e8-383">또는 hello IP 주소 리소스의 새 클라우드 서비스 ILB/ELB PowerShell 통해 Windows 클러스터링을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-383">Or adding hello IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="738e8-384">그런 다음 집합 hello hello IP 주소 리소스 toohello의 가능한 소유자 노드를 SQL2 마이그레이션되고이 OR 종속성에 hello 네트워크 이름으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-384">Then set hello Possible owners of hello IP Address resource toohello migrated node, SQL2, and set this as OR dependency in hello Network Name.</span></span> <span data-ttu-id="738e8-385">Hello의 hello '동일한 서브넷에 IP 주소 리소스를 추가' 섹션을 참조 [부록](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-385">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="738e8-386">DNS 구성/전파 toohello 클라이언트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-386">Check DNS configuration/propogation toohello clients.</span></span>
* <span data-ttu-id="738e8-387">SQL1 VM을 마이그레이션하고 2~4단계 수행</span><span class="sxs-lookup"><span data-stu-id="738e8-387">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="738e8-388">단계 5ii를 사용 하는 경우 다음 추가 SQL1 hello에 대 한 가능한 소유자 추가 IP 주소 리소스</span><span class="sxs-lookup"><span data-stu-id="738e8-388">If using steps 5ii, then add SQL1 as a Possible Owner for hello added IP Address Resource</span></span>
* <span data-ttu-id="738e8-389">장애 조치(failover) 테스트</span><span class="sxs-lookup"><span data-stu-id="738e8-389">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="738e8-390">2. 기존 보조 복제본 활용: 다중 사이트</span><span class="sxs-lookup"><span data-stu-id="738e8-390">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="738e8-391">둘 이상의 Azure 데이터 센터 (DC)에 노드가 있는 경우 나 하이브리드 환경을 사용 하는 경우이 환경 toominimize 가동 중지 시간이 Always On 구성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment toominimize downtime.</span></span>

<span data-ttu-id="738e8-392">toothat SQL Server를 통해 한 toochange hello에 항상 동기화 tooSynchronous hello 온-프레미스 또는 보조 Azure DC 및 장애 조치에 대 한 hello 방법은 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="738e8-392">hello approach is toochange hello Always On synchronization tooSynchronous for hello on-premises or secondary Azure DC, and then failover over toothat SQL Server.</span></span> <span data-ttu-id="738e8-393">그런 다음 hello Vhd tooa 프리미엄 저장소 계정을 복사한 새 클라우드 서비스에 hello 컴퓨터를 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-393">Then copy hello VHDs tooa Premium Storage account, and redeploy hello machine into a new cloud service.</span></span> <span data-ttu-id="738e8-394">Hello 수신기를 업데이트 하 고 다시 장애 복구 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-394">Update hello listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="738e8-395">가동 중지 시간 발생 시점</span><span class="sxs-lookup"><span data-stu-id="738e8-395">Points of downtime</span></span>
<span data-ttu-id="738e8-396">hello 가동 중지 시간 hello 시간 toofailover toohello 대체 DC 및 다시 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-396">hello downtime consists of hello time toofailover toohello alternative DC and back.</span></span> <span data-ttu-id="738e8-397">또한 클라이언트/DNS 구성에 따라서도 가동 중지 시간이 달라지며, 이로 인해 클라이언트 다시 연결이 지연될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="738e8-398">다음 예에서는 하이브리드 Always On 구성의 hello를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-398">Consider hello following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="738e8-400">장점</span><span class="sxs-lookup"><span data-stu-id="738e8-400">Advantages</span></span>
* <span data-ttu-id="738e8-401">기존 인프라를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-401">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="738e8-402">Hello 옵션 toopre 업그레이드 hello Azure 저장소에 있는 hello Azure DR DC 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-402">You have hello option toopre-upgrade hello Azure storage on hello DR Azure DC first.</span></span>
* <span data-ttu-id="738e8-403">hello Azure DR DC 저장소를 다시 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-403">hello DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="738e8-404">테스트 장애 조치(failover)를 제외하면 마이그레이션 중에 최소한 두 번의 장애 조치(failover)가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-404">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="738e8-405">백업 사용 하 여 SQL Server 데이터 toomove 필요 하지 않으며 복원 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-405">You do not need toomove SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="738e8-406">단점</span><span class="sxs-lookup"><span data-stu-id="738e8-406">Disadvantages</span></span>
* <span data-ttu-id="738e8-407">클라이언트 액세스 tooSQL 서버에 따라 있을 수 있습니다 대기 시간이 증가 대체 DC toohello 응용 프로그램에서 SQL Server가 실행 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="738e8-407">Depending on client access tooSQL Server, there might be increased latency when SQL Server is running in an alternative DC toohello application.</span></span>
* <span data-ttu-id="738e8-408">Vhd tooPremium 저장소의 hello 복사 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-408">hello copy time of VHDs tooPremium storage could be long.</span></span> <span data-ttu-id="738e8-409">Tookeep hello 가용성 그룹에서에서 노드를 hello 여부 결정에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-409">This might affect your decision on whether tookeep hello node in hello Availability Group.</span></span> <span data-ttu-id="738e8-410">로드 hello 마이그레이션 중에 실행 중인 로그 많은 작업이 필요한 경우, 이므로 hello 주 노드 tookeep 해당 트랜잭션 로그에 복제 되지 않은 트랜잭션을 hello에 대 한이 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-410">Consider this for when log intensive work loads are running during hello migration is required, since hello Primary node will have tookeep hello unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="738e8-411">따라서 로그의 크기가 대폭 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-411">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="738e8-412">이 시나리오는 hello Azure를 사용 하 여 **시작 AzureStorageBlobCopy** 는 비동기적인 commandlet 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-412">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="738e8-413">완료 시 SLA는 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-413">There is no SLA on completion.</span></span> <span data-ttu-id="738e8-414">hello hello 복사본의 시간 다릅니다이 큐에 대기에 따라 결정 하는 동안 데이터 tootransfer hello 작업량에도 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-414">hello time of hello copies varies, while this depends on wait in queue, it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="738e8-415">따라서 하기만 하면 한 노드에서 두 번째 데이터 센터에서 hello 복사 테스트 보다 오래 걸리는 경우에 완화 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="738e8-416">여기에 다음 아이디어 hello를 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-416">This could include hello following ideas.</span></span>
  * <span data-ttu-id="738e8-417">가동 중지 시간을 합의 된 hello 마이그레이션을 시작 하기 전에 HA에 대 한 두 번째 SQL 임시 노드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-417">Add a temporary 2nd SQL node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="738e8-418">예약 된 유지 관리 Azure hello 마이그레이션을 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="738e8-418">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="738e8-419">클러스터 쿼럼을 올바르게 구성했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-419">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="738e8-420">이 시나리오에서는 귀하의 설치를 문서화 해야 하 고 hello 저장소 최적의 디스크 캐시 설정에 대 한 변경 내용의 적용 순서 toomake에 매핑되는 방법을 알고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-420">This scenario assumes that you have documented your install and know how hello storage is mapped in order toomake changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="738e8-421">대략적인 단계</span><span class="sxs-lookup"><span data-stu-id="738e8-421">High-level steps</span></span>
![Multisite2][10]

* <span data-ttu-id="738e8-423">온-프레미스 hello / SQL Server 기본 Azure DC hello을 교대로 할당을 다른 자동 장애 조치 파트너 (AFP) hello 하 게 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="738e8-423">Make hello on-premises / alternate Azure DC hello SQL Server Primary, and make it hello other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="738e8-424">SQL2 및 hello 노드 제거 (연결 된 Vhd를 삭제 하지 않음) 디스크 구성 정보를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-424">Gather disk configuration information from SQL2, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="738e8-425">프리미엄 저장소 계정을 만들고 hello 표준 저장소 계정에서에서 Vhd를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-425">Create a Premium Storage account and copy VHDs from hello Standard Storage account.</span></span>
* <span data-ttu-id="738e8-426">새 클라우드 서비스와 연결 된 해당 Premiums 저장소 디스크와 hello SQL2 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-426">Create a new cloud service and create hello SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="738e8-427">ILB/ELB를 구성하고 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="738e8-427">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="738e8-428">업데이트 hello 항상에 수신기 새 ilb / ELB IP 주소와 테스트 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-428">Update hello Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="738e8-429">Hello DNS 구성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-429">Check hello DNS configuration.</span></span>
* <span data-ttu-id="738e8-430">Hello AFP tooSQL2 하 고 SQL1 마이그레이션할 바꾼 2 ~ 5 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="738e8-430">Change hello AFP tooSQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="738e8-431">장애 조치(failover) 테스트</span><span class="sxs-lookup"><span data-stu-id="738e8-431">Test failovers.</span></span>
* <span data-ttu-id="738e8-432">Hello AFP 백 tooSQL1 및 s q l 2 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-432">Switch hello AFP back tooSQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a><span data-ttu-id="738e8-433">부록: 멀티 사이트가 항상에 클러스터 tooPremium 저장소 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="738e8-433">Appendix: Migrating a Multisite Always On Cluster tooPremium Storage</span></span>
<span data-ttu-id="738e8-434">이 항목의 나머지 부분에서는 hello 클러스터 tooPremium 저장소 Always On 멀티 사이트를 변환의 자세한 예제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-434">hello remainder of this topic provides a detailed example of converting a multi-site Always On cluster tooPremium storage.</span></span> <span data-ttu-id="738e8-435">또한 hello 수신기에서 외부 부하 분산 장치 (ELB) tooan 내부 부하 분산 장치 ILB ()를 사용 하 여 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-435">It also converts hello Listener from using an external load balancer (ELB) tooan internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="738e8-436">Environment</span><span class="sxs-lookup"><span data-stu-id="738e8-436">Environment</span></span>
* <span data-ttu-id="738e8-437">Windows 2012/SQL 2012</span><span class="sxs-lookup"><span data-stu-id="738e8-437">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="738e8-438">SP의 DB 파일 하나</span><span class="sxs-lookup"><span data-stu-id="738e8-438">1 DB Files on SP</span></span>
* <span data-ttu-id="738e8-439">노드당 저장소 풀 2개</span><span class="sxs-lookup"><span data-stu-id="738e8-439">2 x Storage Pools per Node</span></span>

![Appendix1][11]

### <a name="vm"></a><span data-ttu-id="738e8-441">VM:</span><span class="sxs-lookup"><span data-stu-id="738e8-441">VM:</span></span>
<span data-ttu-id="738e8-442">이 예에서 ELB tooILB에서 이동 toodemonstrate를 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-442">In this example we are going toodemonstrate moving from an ELB tooILB.</span></span> <span data-ttu-id="738e8-443">ELB가 중 tooswitch toothis 마이그레이션 hello 하는 방법을 보여 줍니다 이므로 ILB의 경우 이전이 라 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-443">ELB was available before ILB, so this shows how tooswitch toothis during hello migration.</span></span>

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a><span data-ttu-id="738e8-445">이전 단계: tooSubscription 연결</span><span class="sxs-lookup"><span data-stu-id="738e8-445">Pre Steps: Connect tooSubscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="738e8-446">1단계: 새 저장소 계정 및 클라우드 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="738e8-446">Step 1: Create New Storage Account and Cloud Service</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a><span data-ttu-id="738e8-447">리소스에서 오류를 허용 하는 2 단계: 증가 hello<Optional></span><span class="sxs-lookup"><span data-stu-id="738e8-447">Step 2: Increase hello permitted failures on resources <Optional></span></span>
<span data-ttu-id="738e8-448">Tooyour Always On 가용성 그룹에 속해 있는 특정 리소스에 제한 되어 hello 클러스터 서비스는 toorestart hello 리소스 그룹을 시도 하는 여기서 기간 동안 발생할 수 있는 개수 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-448">On certain resources that belong tooyour Always On Availability Group there are limits on how many failures that can occur in a period, where hello cluster service will attempt toorestart hello resource group.</span></span> <span data-ttu-id="738e8-449">컴퓨터를 종료 하 여 장애 조치 및 트리거 장애 조치 닫기 toothis 제한을 가져올 수 있습니다 수동으로 지정 하지 않으면 이후이 프로시저를 통해 탐색 되는 동안 증가이 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close toothis limit.</span></span>

<span data-ttu-id="738e8-450">될 신중한 toodouble hello 오류 여유 toodo이 장애 조치 클러스터 관리자에서 toohello 속성 hello Always On 리소스 그룹의 이동은:</span><span class="sxs-lookup"><span data-stu-id="738e8-450">It would be prudent toodouble hello failure allowance, toodo this in Failover Cluster Manager, go toohello Properties of hello Always On resource group:</span></span>

![Appendix3][13]

<span data-ttu-id="738e8-452">최대 실패 too6 hello를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-452">Change hello Maximum Failures too6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="738e8-453">3단계: 클러스터 그룹에 IP 주소 리소스 추가 <Optional></span><span class="sxs-lookup"><span data-stu-id="738e8-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="738e8-454">조심 hello 클러스터 그룹에 대 한 IP 주소가 하나만 있고이 정렬 된 toohello 클라우드 서브넷 경우 실수로 맡 오프 라인 hello 클라우드의 모든 클러스터 노드 네트워크 다음 hello 클러스터 IP 리소스 고 클러스터 네트워크 이름 수 toocome 수 없게 됩니다 하는 경우 온라인.</span><span class="sxs-lookup"><span data-stu-id="738e8-454">If you have only one IP address for hello Cluster Group and this is aligned toohello cloud subnet, beware, if you accidentally take offline all cluster nodes in hello cloud on that network then hello Cluster IP resource and Cluster Network Name will not be able toocome online.</span></span> <span data-ttu-id="738e8-455">Hello 수 없게 됩니다이 이벤트는 tooother 클러스터 리소스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-455">In hello event of this it will prevent updates tooother cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="738e8-456">4단계: DNS 구성</span><span class="sxs-lookup"><span data-stu-id="738e8-456">Step 4: DNS configuration</span></span>
<span data-ttu-id="738e8-457">부드러운 전환이 가능해 집니다 DNS 되는 방식에 따라 달라 집니다 tooimplement 활용 하 고 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-457">tooimplement a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="738e8-458">Windows 클러스터 리소스 그룹을 만듭니다에 항상 설치 하는 경우 장애 조치 클러스터 관리자를 열면 최소한 세 가지 리소스 미치게 될, 문서 hello 두 hello tooare 참조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, hello two that hello document refers tooare:</span></span>

* <span data-ttu-id="738e8-459">가상 네트워크 이름 (VNN) –이 hello DNS 이름을 클라이언트 연결 toowhen tooconnect tooSQL Always On를 통해 서버를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-459">Virtual Network Name (VNN) – This is hello DNS name that client connect toowhen wanting tooconnect tooSQL Servers via Always On.</span></span>
* <span data-ttu-id="738e8-460">IP 주소 리소스 –이 IP 주소에 연결 된 VNN hello hello, 개 이상 사용할 수 있습니다 및 멀티 사이트 구성 사이트/서브넷 별 IP 주소를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-460">IP Address Resource – This is hello IP address that associated with hello VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span></span>

<span data-ttu-id="738e8-461">서버 hello SQL Server 클라이언트 드라이버 연결 tooSQL hello 수신기와 관련 된 hello DNS 레코드를 검색 하 고 tooconnect tooeach 시도 하는 경우 연결 된 IP 주소에 항상,이 영향을 주는 몇 가지 요소에서는 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-461">When connecting tooSQL Server, hello SQL Server Client driver will retrieve hello DNS records associated with hello listener and try tooconnect tooeach Always On associated IP address, below we discuss some factors that can influence this.</span></span>

<span data-ttu-id="738e8-462">hello hello 수신기 이름에 연관 된 동시 DNS 레코드의 수에 따라 달라 집니다 뿐만 아니라, 연결 된 IP 주소의 hello 수 있지만 hello ' hello 항상 ON VNN 리소스에 대 한 장애 조치 클러스터링에 RegisterAllIpProviders'setting 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-462">hello number of concurrent DNS records that are associated with hello listener name depends not only on hello number of IP addresses associated, but hello ‘RegisterAllIpProviders’setting in Failover Clustering for hello Always ON VNN resource.</span></span>

<span data-ttu-id="738e8-463">Always On Azure에 배포할 때 다른 단계가 toocreate hello 수신기 및 IP 주소, toomanually hello 'RegisterAllIpProviders' too1 구성을 이미 too1 설정 배포에서 항상 다른 tooan 온-프레미스입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-463">When you deploy Always On in Azure there are different steps toocreate hello Listener and IP Addresses, you have toomanually configure hello ‘RegisterAllIpProviders’ too1, this is different tooan on-premises Always On deployment where it is already set too1.</span></span>

<span data-ttu-id="738e8-464">'RegisterAllIpProviders'가 0, 하나 hello 수신기와 연결 된 DNS 레코드가 DNS에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with hello Listener:</span></span>

![Appendix4][14]

<span data-ttu-id="738e8-466">'RegisterAllIpProviders'가 1인 경우에는 다음 레코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-466">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Appendix5][15]

<span data-ttu-id="738e8-468">아래 hello 코드를 덤프 하 hello VNN 설정 되며 사용자에 대 한 설정, 하십시오 hello에 대 한 참고 tootake 효과 tootake hello VNN 오프 라인 및 온라인 다시 설정 해야 합니다, 그리고 변경이 기록이 hello 수신기 오프 라인 바꾸지 클라이언트 연결 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-468">hello code below will dump out hello VNN settings and set it for you, please note, for hello change tootake effect you will need tootake hello VNN offline and turn it back online, this taking hello Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="738e8-469">이후 마이그레이션 단계에서는 tooupdate hello Always On 수신기 부하 분산 장치를 참조 하는 업데이트 된 IP 주소 사용 해야 합니다, 그리고 IP 주소 리소스 제거와 더하기가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-469">In a later migration step you will need tooupdate hello Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span></span> <span data-ttu-id="738e8-470">Hello IP 업데이트 후 해야 tooensure hello 새 hello 클라이언트의 로컬 DNS 캐시의 업데이트 하는 고 IP 주소가 DNS 영역에서 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-470">After hello IP update, you need tooensure hello new IP address has been updated in DNS Zone and that hello clients are updating their local DNS cache.</span></span>

<span data-ttu-id="738e8-471">Tooconsider 어떤 일이 생기 DNS 영역 전송 하는 방법에 대 한 hello 마이그레이션하는 동안 hello 응용 프로그램 다시 연결 시간 제한이 적용 됩니다 클라이언트는 다른 네트워크 세그먼트에 있는 다른 DNS 서버를 참조할 경우 해야 hello 영역 전송 시간 이상으로 hello 수신기에 대 한 모든 새 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-471">If your clients reside in a different network segment and reference a different DNS server, you need tooconsider what happens about DNS Zone Transfer during hello migration, as hello application reconnect time will be constrained by at least hello Zone Transfer Time of any new IP addresses for hello listener.</span></span> <span data-ttu-id="738e8-472">인 경우 시간 제약 조건은 여기에서 논의 하 고 프로그램 Windows 팀과 함께 증분 영역 전송 강제 적용을 테스트 해야 고 hello DNS를 전환할 수도 호스트 레코드 tooa 줄이려면 tooLive TTL (Time), 이므로 hello 클라이언트 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put hello DNS host record tooa lower Time tooLive (TTL), so hello clients update.</span></span> <span data-ttu-id="738e8-473">자세한 내용은 [증분 영역 전송](https://technet.microsoft.com/library/cc958973.aspx) 및 [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="738e8-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span></span>

<span data-ttu-id="738e8-474">기본 hello hello에서 Always On Azure에서 수신기와 연결 된 DNS 레코드에 대 한 TTL으로 1200 초입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-474">By default hello TTL for DNS Record that is associated with hello Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="738e8-475">지정할 수 있습니다 tooreduce이 hello 수신기에 대 한 해당 DNS를 업데이트 하는 hello IP 주소 마이그레이션 tooensure hello 클라이언트 업데이트 하는 동안 시간 제약 조건을 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="738e8-475">You may wish tooreduce this if you are under time constraint during your migration tooensure hello clients update their DNS with hello updated IP address for hello listener.</span></span> <span data-ttu-id="738e8-476">참조 및 hello 구성의 VNN hello 덤프 하 여 hello 구성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-476">You can see and modify hello configuration by dumping out hello configuration of hello VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

<span data-ttu-id="738e8-477">하십시오 note, hello 낮은 hello 'HostRecordTTL' DNS 트래픽의 더 높은 값이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-477">Please note, hello lower hello ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="738e8-478">클라이언트 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="738e8-478">Client application settings</span></span>
<span data-ttu-id="738e8-479">SQL 클라이언트 응용 프로그램이 지 원하는.Net 4.5 hello 경우 SQLClient를 사용할 수 있습니다 ' MULTISUBNETFAILOVER = TRUE' 키워드는 것이 좋습니다 toobe 장애 조치 중 더 빠른 연결 tooSQL Always On 가용성 그룹에 대 한 수 있으므로 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-479">If your SQL client application supports hello .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended toobe applied as it allows for faster connection tooSQL Always On Availability Group during failover.</span></span> <span data-ttu-id="738e8-480">병렬로 hello Always On 수신기와 관련 된 모든 IP 주소를 통해 열거 하 고 장애 조치 중 보다 적극적으로 TCP 연결 시도 속도 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-480">It enumerates through all IP addresses associated with hello Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="738e8-481">위의 hello 설정에 대 한 자세한 내용은 참조 하십시오 [MultiSubnetFailover 키워드 및 기능 관련](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover)합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-481">For more information regarding hello settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="738e8-482">또한 [SqlClient의 고가용성 및 재해 복구 지원](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="738e8-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="738e8-483">5단계: 클러스터 쿼럼 설정</span><span class="sxs-lookup"><span data-stu-id="738e8-483">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="738e8-484">에 대 한 tooallow 고 파일 공유 감시 (FSW)에서 노드 2 개를 사용 하 hello 쿼럼 tooallow 노드 과반수를 설정 하 고 해야 동적 투표를 활용 경우에 hello 클러스터 쿼럼 설정을 수정 해야 toobe 한 번에 하나 이상의 SQL Server를 파괴 하는 것 처럼 단일 노드 tooremain 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-484">As you are going toobe taking out at least one SQL Server down at a time, you should modify hello cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set hello quorum tooallow node majority and utilize dynamic voting, and this is tooallow for a single node tooremain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="738e8-485">관리 및 hello 클러스터 쿼럼 구성에 대 한 자세한 내용은 참조 하십시오 [구성 및 관리에 Windows Server 2012 장애 조치 클러스터에서 쿼럼 hello](https://technet.microsoft.com/library/jj612870.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-485">For more information on managing and configuring hello cluster quorum, please see [Configure and Manage hello Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="738e8-486">6단계: 기존 끝점 및 ACL 추출</span><span class="sxs-lookup"><span data-stu-id="738e8-486">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="738e8-487">이러한 tooa 텍스트 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-487">Save these tooa text file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="738e8-488">7단계: 장애 조치(failover) 파트너 및 복제 모드 변경</span><span class="sxs-lookup"><span data-stu-id="738e8-488">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="738e8-489">SQL 서버 2 개 이상 있는 경우 다른 DC에서 다른 보조 복제본의 장애 조치 hello 변경할지 또는 온-프레미스 too'Synchronous' 하는 자동 장애 조치 파트너 (AFP)를 확인,이 작업은 변경 하는 동안에 HA를 유지 관리 되므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-489">If you have more than 2 SQL Servers, you should change hello failover of another secondary in another DC or on-premises too‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="738e8-490">SSMS를 통해 TSQL modify를 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-490">You can do this through TSQL of modify though SSMS:</span></span>

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="738e8-492">8단계: 클라우드 서비스에서 보조 VM 제거</span><span class="sxs-lookup"><span data-stu-id="738e8-492">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="738e8-493">클라우드 보조 노드 toomigrate 수립 해야 먼저 현재 기본 인 경우 수동 장애 조치 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-493">You should be planning toomigrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span></span>

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="738e8-494">9단계: CSV 파일에서 디스크 캐싱 설정 변경 및 저장</span><span class="sxs-lookup"><span data-stu-id="738e8-494">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="738e8-495">데이터 볼륨에 대 한 이러한 설정할 tooREADONLY입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-495">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="738e8-496">TLOG 볼륨에 대 한 이러한 설정할 tooNONE입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-496">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="738e8-498">10단계: VHD 복사</span><span class="sxs-lookup"><span data-stu-id="738e8-498">Step 10: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



<span data-ttu-id="738e8-499">프리미엄 저장소 계정의 hello Vhd toohello의 hello 복사 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-499">You can check hello copy status of hello VHDs toohello Premium Storage account:</span></span>

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix8][18]

<span data-ttu-id="738e8-501">모든 작업이 성공으로 기록될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-501">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="738e8-502">개별 Blob에 대한 정보를 확인하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-502">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="738e8-503">11단계: OS 디스크 등록</span><span class="sxs-lookup"><span data-stu-id="738e8-503">Step 11: Register OS disk</span></span>
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="738e8-504">12단계: 새 클라우드 서비스에 보조 복제본 가져오기</span><span class="sxs-lookup"><span data-stu-id="738e8-504">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="738e8-505">또한 사용 하 여 hello 추가 아래 hello 코드 옵션 여기 hello 컴퓨터를 가져오고 hello retainable VIP를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-505">hello code below also uses hello added option here you can import hello machine and use hello retainable VIP.</span></span>

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="738e8-506">13단계: 새 클라우드 서비스에서 ILB를 만들고 부하 분산된 끝점 및 ACL 추가</span><span class="sxs-lookup"><span data-stu-id="738e8-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a><span data-ttu-id="738e8-507">14단계: Always On 업데이트</span><span class="sxs-lookup"><span data-stu-id="738e8-507">Step 14: Update Always On</span></span>
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

<span data-ttu-id="738e8-509">이제 hello 이전 클라우드 서비스 IP 주소를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-509">Now remove hello old cloud service IP Address.</span></span>

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="738e8-511">15단계: DNS 업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="738e8-511">Step 15: DNS update check</span></span>
<span data-ttu-id="738e8-512">이제 SQL Server 클라이언트 네트워크에서 DNS 서버를 확인 하 고 클러스터링 hello 추가 있는지 확인 해야 hello에 대 한 추가 호스트 레코드 IP 주소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added hello extra host record for hello added IP address.</span></span> <span data-ttu-id="738e8-513">이러한 DNS 서버를 업데이트 하지 않았으면 하 고 DNS 영역 전송을 강제로 고려 hello 없어 서브넷의 클라이언트는 항상에 IP 주소 수 tooresolve tooboth,이 작업은 자동 DNS 복제에 대 한 toowait 않아도 되므로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that hello clients in there subnet are able tooresolve tooboth Always On IP Addresses, this is so you do not need toowait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="738e8-514">16단계: Always On 다시 구성</span><span class="sxs-lookup"><span data-stu-id="738e8-514">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="738e8-515">이 시점에서 마이그레이션된 toofully 있던 해당 노드 hello 온-프레미스 노드를 다시 동기화 및 복제 노드에서 toosynchronous 전환한 hello AFP 확인 보조 hello에 대 한 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-515">At this point you wait for hello secondary that node that was migrated toofully resynchronize with hello on-premises node and switch toosynchronous replication node and make it hello AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="738e8-516">17단계: 두 번째 노드 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="738e8-516">Step 17: Migrate second node</span></span>
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="738e8-517">18단계: CSV 파일에서 디스크 캐싱 설정 변경 및 저장</span><span class="sxs-lookup"><span data-stu-id="738e8-517">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="738e8-518">데이터 볼륨에 대 한 이러한 설정할 tooREADONLY입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-518">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="738e8-519">TLOG 볼륨에 대 한 이러한 설정할 tooNONE입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-519">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="738e8-521">19단계: 보조 노드에 대한 새 독립 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="738e8-521">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="738e8-522">20단계: VHD 복사</span><span class="sxs-lookup"><span data-stu-id="738e8-522">Step 20: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


<span data-ttu-id="738e8-523">모든 Vhd에 대 한 hello VHD 복사 상태를 확인할 수 있습니다. ($diskobjects에 $disk) ForEach {$lun $disk = 합니다. Lun $vhdname $disk.vhdname $cacheoption = $disk = 합니다. HostCaching $disklabel $disk = 합니다. DiskLabel $diskName $disk = 합니다. DiskName</span><span class="sxs-lookup"><span data-stu-id="738e8-523">You can check hello VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

<span data-ttu-id="738e8-525">모든 작업이 성공으로 기록될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-525">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="738e8-526">개별 Blob에 대한 정보를 확인하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-526">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="738e8-527">21단계: OS 디스크 등록</span><span class="sxs-lookup"><span data-stu-id="738e8-527">Step 21: Register OS disk</span></span>
    #change storage account toohello new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join tooexisting Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="738e8-528">22단계: 부하 분산된 끝점 및 ACL 추가</span><span class="sxs-lookup"><span data-stu-id="738e8-528">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="738e8-529">23단계: 장애 조치(failover) 테스트</span><span class="sxs-lookup"><span data-stu-id="738e8-529">Step 23: Test failover</span></span>
<span data-ttu-id="738e8-530">이제 hello 마이그레이션된 노드 hello 온-프레미스에 항상 노드와 동기화, toosynchronous 복제 모드로 및 동기화 될 때까지 대기 하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-530">You should now let hello migrated node synchronize with hello on-premises Always On node, place it in toosynchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="738e8-531">그런 다음 온-프레미스 toohello 첫 번째 노드 간에서 장애 조치가 마이그레이션됩니다, hello AFP.</span><span class="sxs-lookup"><span data-stu-id="738e8-531">Then failover from on-prem toohello first node migrated, which is hello AFP.</span></span> <span data-ttu-id="738e8-532">적 하 되 면 변경 hello는 마지막 노드 toohello AFP 마이그레이션됩니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-532">Once that has worked, change hello last migrated node toohello AFP.</span></span>

<span data-ttu-id="738e8-533">모든 노드 간에 장애 조치를 테스트 하 고 예상 대로 tooensure 장애 조치 작동 chaos 테스트 있지만 및 시기 적절 한 manor 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-533">You should test failovers between all nodes and run though chaos tests tooensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="738e8-534">24단계: 클러스터 쿼럼 설정/DNS TTL/장애 조치(failover) 파트너/동기화 설정 원래대로 변경</span><span class="sxs-lookup"><span data-stu-id="738e8-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="738e8-535">동일한 서브넷에 IP 주소 리소스 추가</span><span class="sxs-lookup"><span data-stu-id="738e8-535">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="738e8-536">경우 두 SQL Server 있고 toomigrate에 tooa 새로운 클라우드 서비스, 하지만 tookeep에 hello 동일한 서브넷, IP 주소에 항상 오프 라인 toodelete hello 원래 hello 수신기를 받지 않도록 하 고 hello 새 IP 주소를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-536">If you have only 2 SQL Servers and want toomigrate them tooa new cloud service, but want tookeep them on hello same subnet, you can avoid taking hello listener offline toodelete hello original Always On IP Address and add hello New IP Address.</span></span> <span data-ttu-id="738e8-537">Hello Vm tooanother 서브넷 필요는 없지만 toodo이 해당 서브넷을 참조 하는 추가 클러스터 네트워크 있을 마이그레이션하는 경우.</span><span class="sxs-lookup"><span data-stu-id="738e8-537">If you are migrating hello VMs tooanother subnet you will not need toodo this as there will be an additional cluster network that will reference that subnet.</span></span>

<span data-ttu-id="738e8-538">가져온 후 hello 보조 데이터베이스를 마이그레이션해야 하며 장애 조치 hello 기존 기본 전에 hello hello 새 클라우드 서비스에 대 한 새 IP 주소 리소스에 추가, hello 장애 조치 클러스터 관리자 내에서 이러한 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-538">Once you have brought up hello migrated secondary and added in hello new IP Address resource for hello new cloud service before failover hello existing Primary, you should take these steps within hello Cluster Failover Manager:</span></span>

<span data-ttu-id="738e8-539">IP 주소에 tooadd 참조 hello [부록](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), 14 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-539">tooadd in IP Address, see hello [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="738e8-540">현재 IP 주소 리소스 hello에 대 한 hello 가능한 소유자 too'Existing 주 SQL Server 변경 ', 'dansqlams4' 아래 hello 예제에서:</span><span class="sxs-lookup"><span data-stu-id="738e8-540">For hello current IP Address resource, change hello possible owner too‘Existing Primary SQL Server’, in hello example below, ‘dansqlams4’:</span></span>

    ![Appendix13][23]
2. <span data-ttu-id="738e8-542">변경 가능한 소유자 too'Migrated hello hello 새 IP 주소 리소스에 대 한 보조 SQL Server', 'dansqlams5' 아래 hello 예제에서:</span><span class="sxs-lookup"><span data-stu-id="738e8-542">For hello new IP Address resource, change hello possible owner too‘Migrated secondary SQL Server’, in hello example below, ‘dansqlams5’:</span></span>

    ![Appendix14][24]
3. <span data-ttu-id="738e8-544">이 설정 되 고 나면 장애 조치 한 hello 마지막 노드 마이그레이션하는 경우에 해당 노드를 가능한 소유자로 추가 됩니다 hello 가능한 소유자를 편집 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="738e8-544">Once this is set you can failover, and when hello last node is migrated hello Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Appendix15][25]

## <a name="additional-resources"></a><span data-ttu-id="738e8-546">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="738e8-546">Additional resources</span></span>
* [<span data-ttu-id="738e8-547">Azure 프리미엄 저장소</span><span class="sxs-lookup"><span data-stu-id="738e8-547">Azure Premium Storage</span></span>](../../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="738e8-548">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="738e8-548">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="738e8-549">Azure 가상 컴퓨터의 SQL Server</span><span class="sxs-lookup"><span data-stu-id="738e8-549">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
