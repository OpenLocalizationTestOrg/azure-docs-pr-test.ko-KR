---
title: "Azure에서 Always On 가용성 그룹에 대한 ILB 수신기 구성 | Microsoft Docs"
description: "이 자습서에서는 클래식 배포 모델을 사용하여 만든 리소스를 사용하며, Azure에서 내부 부하 분산 장치를 사용하는 Always On 가용성 그룹 수신기를 만듭니다."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: fea70b389b1f1d6af963e3f14fdc48e8d857dd53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="fe279-103">Azure에서 Always On 가용성 그룹에 대한 ILB 수신기 구성</span><span class="sxs-lookup"><span data-stu-id="fe279-103">Configure an ILB listener for Always On availability groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe279-104">내부 수신기</span><span class="sxs-lookup"><span data-stu-id="fe279-104">Internal listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="fe279-105">외부 수신기</span><span class="sxs-lookup"><span data-stu-id="fe279-105">External listener</span></span>](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a><span data-ttu-id="fe279-106">개요</span><span class="sxs-lookup"><span data-stu-id="fe279-106">Overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe279-107">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델, 즉 [Azure Resource Manager 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md) 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fe279-108">이 문서에서는 클래식 배포 모델의 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-108">This article covers the use of the classic deployment model.</span></span> <span data-ttu-id="fe279-109">대부분의 새로운 배포에서는 Azure Resource Manager 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-109">We recommend that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="fe279-110">Resource Manager 모델에서 Always On 가용성 그룹에 대한 수신기를 구성하려면 [Azure에서 Always On 가용성 그룹에 대한 부하 분산 장치 구성](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe279-110">To configure a listener for an Always On availability group in the Resource Manager model, see [Configure a load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

<span data-ttu-id="fe279-111">가용성 그룹은 온-프레미스 전용, Azure 전용 또는 하이브리드 구성에 대한 온-프레미스와 Azure 모두에 걸쳐 있는 복제본을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-111">Your availability group can contain replicas that are on-premises only or Azure only, or that span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="fe279-112">Azure 복제본은 동일한 지역 내 또는 여러 가상 네트워크를 사용하는 여러 지역에 걸쳐 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-112">Azure replicas can reside within the same region or across multiple regions that use multiple virtual networks.</span></span> <span data-ttu-id="fe279-113">이 문서의 절차에서는 [가용성 그룹을 구성](../classic/portal-sql-alwayson-availability-groups.md)했지만 수신기는 아직 구성하지 않았다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-113">The procedures in this article assume that you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not yet configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-internal-listeners"></a><span data-ttu-id="fe279-114">내부 수신기에 대한 지침 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="fe279-114">Guidelines and limitations for internal listeners</span></span>
<span data-ttu-id="fe279-115">Azure에서 가용성 그룹 수신기에 ILB(내부 부하 분산 장치)를 사용하는 경우 다음과 같은 지침이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-115">The use of an internal load balancer (ILB) with an availability group listener in Azure is subject to the following guidelines:</span></span>

* <span data-ttu-id="fe279-116">가용성 그룹 수신기는 Windows Server 2008 R2, Windows Server 2012 및 Windows Server 2012 R2에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-116">The availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="fe279-117">수신기는 ILB로 구성되고 ILB는 클라우드 서비스당 하나만 있기 때문에 클라우드 서비스마다 하나의 내부 가용성 그룹 수신기만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-117">Only one internal availability group listener is supported for each cloud service, because the listener is configured to the ILB, and there is only one ILB for each cloud service.</span></span> <span data-ttu-id="fe279-118">그러나 외부 수신기는 여러 개를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-118">However, it is possible to create multiple external listeners.</span></span> <span data-ttu-id="fe279-119">자세한 내용은 [Azure에서 Always On 가용성 그룹에 대한 외부 수신기 구성](../classic/ps-sql-ext-listener.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe279-119">For more information, see [Configure an external listener for Always On availability groups in Azure](../classic/ps-sql-ext-listener.md).</span></span>

## <a name="determine-the-accessibility-of-the-listener"></a><span data-ttu-id="fe279-120">수신기의 액세스 가능 여부 확인</span><span class="sxs-lookup"><span data-stu-id="fe279-120">Determine the accessibility of the listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="fe279-121">이 문서에서는 ILB를 사용하는 수신기를 만드는 데 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-121">This article focuses on creating a listener that uses an ILB.</span></span> <span data-ttu-id="fe279-122">공용 또는 외부 수신기가 필요한 경우 [외부 수신기](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) 설정에 대해 설명하는 이 문서의 다른 버전을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe279-122">If you need an public or external listener, see the version of this article that discusses setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="fe279-123">직접 서버 반환이 있는 부하 분산 VM 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="fe279-123">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="fe279-124">이 섹션에서는 스크립트를 실행하여 ILB를 먼저 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-124">You first create an ILB by running the script later in this section.</span></span>

<span data-ttu-id="fe279-125">Azure 복제본을 호스트하는 각 VM에 대해 부하가 분산된 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-125">Create a load-balanced endpoint for each VM that hosts an Azure replica.</span></span> <span data-ttu-id="fe279-126">여러 지역에 복제본이 있는 경우 해당 지역에 대한 각 복제본은 동일한 Azure 가상 네트워크의 동일한 클라우드 서비스에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-126">If you have replicas in multiple regions, each replica for that region must be in the same cloud service in the same Azure virtual network.</span></span> <span data-ttu-id="fe279-127">여러 Azure 지역에 걸쳐 있는 가용성 그룹 복제본을 만들려면 여러 가상 네트워크를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-127">Creating availability group replicas that span multiple Azure regions requires configuring multiple virtual networks.</span></span> <span data-ttu-id="fe279-128">가상 네트워크 간의 연결을 구성하는 방법에 대한 정보는 [가상 네트워크 연결에 가상 네트워크 구성](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe279-128">For more information on configuring cross virtual network connectivity, see [Configure virtual network to virtual network connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="fe279-129">Azure Portal에서 세부 정보를 보려면 복제본을 호스팅하는 각 VM으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-129">In the Azure portal, go to each VM that hosts a replica to view the details.</span></span>

2. <span data-ttu-id="fe279-130">각 VM에 대한 **끝점** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-130">Click the **Endpoints** tab for each VM.</span></span>

3. <span data-ttu-id="fe279-131">사용할 수신기 끝점의 **이름** 및 **공용 포트**가 사용 중이지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-131">Verify that the **Name** and **Public Port** of the listener endpoint that you want to use are not already in use.</span></span> <span data-ttu-id="fe279-132">이 섹션의 예제에서는 이름이 *MyEndpoint*이고 포트는 *1433*입니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-132">In the example in this section, the name is *MyEndpoint*, and the port is *1433*.</span></span>

4. <span data-ttu-id="fe279-133">로컬 클라이언트에서 최신 [PowerShell 모듈](https://azure.microsoft.com/downloads/)을 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-133">On your local client, download and install the latest [PowerShell module](https://azure.microsoft.com/downloads/).</span></span>

5. <span data-ttu-id="fe279-134">Azure PowerShell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-134">Start Azure PowerShell.</span></span>  
    <span data-ttu-id="fe279-135">새 PowerShell 세션이 Azure 관리 모듈이 로드된 상태로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-135">A new PowerShell session opens, with the Azure administrative modules loaded.</span></span>

6. <span data-ttu-id="fe279-136">`Get-AzurePublishSettingsFile`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-136">Run `Get-AzurePublishSettingsFile`.</span></span> <span data-ttu-id="fe279-137">이 cmdlet은 게시 설정 파일을 로컬 디렉터리에 다운로드하도록 브라우저로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-137">This cmdlet directs you to a browser to download a publish settings file to a local directory.</span></span> <span data-ttu-id="fe279-138">Azure 구독에 대한 로그인 자격 증명을 묻는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-138">You might be prompted for your sign-in credentials for your Azure subscription.</span></span>

7. <span data-ttu-id="fe279-139">다운로드한 게시 설정 파일의 경로와 함께 다음 `Import-AzurePublishSettingsFile` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-139">Run the following `Import-AzurePublishSettingsFile` command with the path of the publish settings file that you downloaded:</span></span>

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    <span data-ttu-id="fe279-140">게시 설정 파일을 가져오면 PowerShell 세션에서 Azure 구독을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-140">After the publish settings file is imported, you can manage your Azure subscription in the PowerShell session.</span></span>

8. <span data-ttu-id="fe279-141">*ILB*에 대해 고정 IP 주소를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-141">For *ILB*, assign a static IP address.</span></span> <span data-ttu-id="fe279-142">다음 명령을 실행하여 현재 가상 네트워크 구성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-142">Examine the current virtual network configuration by running the following command:</span></span>

        (Get-AzureVNetConfig).XMLConfiguration
9. <span data-ttu-id="fe279-143">복제본을 호스트하는 VM이 포함된 서브넷의 *서브넷* 이름을 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-143">Note the *Subnet* name for the subnet that contains the VMs that host the replicas.</span></span> <span data-ttu-id="fe279-144">이 이름은 스크립트의 $SubnetName 매개 변수에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-144">This name is used in the $SubnetName parameter in the script.</span></span>

10. <span data-ttu-id="fe279-145">복제본을 호스트하는 VM이 포함된 서브넷의 *VirtualNetworkSite* 이름과 시작 *AddressPrefix*를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-145">Note the *VirtualNetworkSite* name and the starting *AddressPrefix* for the subnet that contains the VMs that host the replicas.</span></span> <span data-ttu-id="fe279-146">두 값을 `Test-AzureStaticVNetIP` 명령에 전달하고 *AvailableAddresses*를 검사하여 사용 가능한 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-146">Look for an available IP address by passing both values to the `Test-AzureStaticVNetIP` command and by examining the *AvailableAddresses*.</span></span> <span data-ttu-id="fe279-147">예를 들어 가상 네트워크 이름이 *MyVNet*이고 서브넷 주소 범위가 *172.16.0.128*에서 시작한다면 다음 명령을 통해 사용 가능한 주소를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-147">For example, if the virtual network is named *MyVNet* and has a subnet address range that starts at *172.16.0.128*, the following command would list available addresses:</span></span>

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. <span data-ttu-id="fe279-148">사용 가능한 주소 중 하나를 선택하고 다음 단계에 있는 스크립트의 $ILBStaticIP 매개 변수에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-148">Select one of the available addresses, and use it in the $ILBStaticIP parameter of the script in the next step.</span></span>

12. <span data-ttu-id="fe279-149">다음 PowerShell 스크립트를 텍스트 편집기에 복사하고 사용자 환경에 맞게 변수 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-149">Copy the following PowerShell script to a text editor, and set the variable values to suit your environment.</span></span> <span data-ttu-id="fe279-150">일부 매개 변수에 대해 기본값이 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-150">Defaults have been provided for some parameters.</span></span>  

    <span data-ttu-id="fe279-151">선호도 그룹을 사용하는 기존 배포는 ILB를 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-151">Existing deployments that use affinity groups cannot add an ILB.</span></span> <span data-ttu-id="fe279-152">ILB 요구 사항에 대한 자세한 내용은 [내부 부하 분산 장치 개요](../../../load-balancer/load-balancer-internal-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe279-152">For more information about ILB requirements, see [Internal load balancer overview](../../../load-balancer/load-balancer-internal-overview.md).</span></span>

    <span data-ttu-id="fe279-153">또한 가용성 그룹에 Azure 지역에 걸쳐 있는 경우, 데이터센터에 있는 클라우드 서비스 및 노드에 대해 각각의 데이터센터에서 한 번씩 스크립트를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-153">Also, if your availability group spans Azure regions, you must run the script once in each datacenter for the cloud service and nodes that reside in that datacenter.</span></span>

        # Define variables
        $ServiceName = "<MyCloudService>" # the name of the cloud service that contains the availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in the same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that the replicas use in the virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for the ILB in the subnet
        $ILBName = "AGListenerLB" # customize the ILB name or use this default value

        # Create the ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. <span data-ttu-id="fe279-154">변수를 설정한 후에는 텍스트 편집기에서 해당 스크립트를 PowerShell 세션에 복사하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-154">After you have set the variables, copy the script from the text editor to your PowerShell session to run it.</span></span> <span data-ttu-id="fe279-155">프롬프트에 **>>**가 계속 표시되면 Enter를 다시 입력하여 스크립트 실행이 시작되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-155">If the prompt still shows **>>**, press Enter again to make sure the script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="fe279-156">필요한 경우 KB2854082가 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-156">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-the-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="fe279-157">가용성 그룹 노드에서 방화벽 포트 열기</span><span class="sxs-lookup"><span data-stu-id="fe279-157">Open the firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-the-availability-group-listener"></a><span data-ttu-id="fe279-158">가용성 그룹 수신기 만들기</span><span class="sxs-lookup"><span data-stu-id="fe279-158">Create the availability group listener</span></span>

<span data-ttu-id="fe279-159">두 단계로 가용성 그룹 수신기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-159">Create the availability group listener in two steps.</span></span> <span data-ttu-id="fe279-160">먼저, 클라이언트 액세스 지점 클러스터 리소스를 만들고 종속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-160">First, create the client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="fe279-161">두 번째로, PowerShell에서 클러스터 리소스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-161">Second, configure the cluster resources in PowerShell.</span></span>

### <a name="create-the-client-access-point-and-configure-the-cluster-dependencies"></a><span data-ttu-id="fe279-162">클라이언트 액세스 지점을 만들고 클러스터 종속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-162">Create the client access point and configure the cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-the-cluster-resources-in-powershell"></a><span data-ttu-id="fe279-163">PowerShell로 클러스터 리소스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-163">Configure the cluster resources in PowerShell</span></span>
1. <span data-ttu-id="fe279-164">ILB의 경우 앞서 만든 ILB의 IP 주소를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-164">For ILB, you must use the IP address of the ILB that was created earlier.</span></span> <span data-ttu-id="fe279-165">PowerShell에서 이 IP 주소를 가져오려면 다음 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-165">To obtain this IP address in PowerShell, use the following script:</span></span>

        # Define variables
        $ServiceName="<MyServiceName>" # the name of the cloud service that contains the AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. <span data-ttu-id="fe279-166">VM 중 하나에서 사용 중인 운영 체제의 PowerShell 스크립트를 텍스트 편집기에 복사하고 앞에서 기록한 값으로 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-166">On one of the VMs, copy the PowerShell script for your operating system to a text editor, and then set the variables to the values you noted earlier.</span></span>

    <span data-ttu-id="fe279-167">Windows Server 2012 이상에서는 다음 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-167">For Windows Server 2012 or later, use the following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
        $IPResourceName = "<IPResourceName>" # the IP address resource name
        $ILBIP = “<X.X.X.X>” # the IP address of the ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    <span data-ttu-id="fe279-168">Windows Server 2008 R2에서는 다음 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-168">For Windows Server 2008 R2, use the following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
        $IPResourceName = "<IPResourceName>" # the IP address resource name
        $ILBIP = “<X.X.X.X>” # the IP address of the ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. <span data-ttu-id="fe279-169">변수를 설정한 후에는 앞으로 온 Windows PowerShell 창을 열고 텍스트 편집기의 스크립트를 복사하여 PowerShell 세션에 붙여넣어 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-169">After you have set the variables, open an elevated Windows PowerShell window, paste the script from the text editor into your PowerShell session to run it.</span></span> <span data-ttu-id="fe279-170">프롬프트에 **>>**가 계속 표시되면 Enter를 다시 입력하여 스크립트 실행이 시작되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-170">If the prompt still shows **>>**, Press Enter again to make sure that the script starts running.</span></span>

4. <span data-ttu-id="fe279-171">각 VM에 대해 이전 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-171">Repeat the preceding steps for each VM.</span></span>  
    <span data-ttu-id="fe279-172">이 스크립트는 클라우드 서비스의 IP 주소로 IP 주소 리소스를 구성하고 프로브 포트 등의 다른 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-172">This script configures the IP address resource with the IP address of the cloud service and sets other parameters, such as the probe port.</span></span> <span data-ttu-id="fe279-173">IP 주소 리소스를 온라인으로 불러올 때 앞 부분에서 부하가 분산된 끝점으로부터 프로브 포트에 대한 폴링에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe279-173">When the IP address resource is brought online, it can respond to the polling on the probe port from the load-balanced endpoint that you created earlier.</span></span>

## <a name="bring-the-listener-online"></a><span data-ttu-id="fe279-174">수신기를 온라인 상태로 만들기</span><span class="sxs-lookup"><span data-stu-id="fe279-174">Bring the listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="fe279-175">추가 작업 항목</span><span class="sxs-lookup"><span data-stu-id="fe279-175">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-the-availability-group-listener-within-the-same-virtual-network"></a><span data-ttu-id="fe279-176">(동일한 가상 네트워크 내)가용성 그룹 수신기 테스트</span><span class="sxs-lookup"><span data-stu-id="fe279-176">Test the availability group listener (within the same virtual network)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a><span data-ttu-id="fe279-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fe279-177">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
