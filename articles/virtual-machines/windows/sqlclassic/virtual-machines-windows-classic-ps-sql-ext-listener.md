---
title: "Always On 가용성 그룹에 대한 외부 수신기 구성 | Microsoft Docs"
description: "이 자습서에서는 연결된 클라우드 서비스의 공용 가상 IP 주소를 사용하여 외부에서 액세스 가능한 Azure의 Always On 가용성 그룹 수신기를 만드는 과정을 안내합니다."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a2453032-94ab-4775-b976-c74d24716728
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: 8e506be42aea4fb3c48c29b771a78dcf694f4518
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-an-external-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="1f975-103">Azure에서 Always On 가용성 그룹에 대한 외부 수신기 구성</span><span class="sxs-lookup"><span data-stu-id="1f975-103">Configure an external listener for Always On Availability Groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f975-104">내부 수신기</span><span class="sxs-lookup"><span data-stu-id="1f975-104">Internal Listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="1f975-105">외부 수신기</span><span class="sxs-lookup"><span data-stu-id="1f975-105">External Listener</span></span>](../classic/ps-sql-ext-listener.md)
> 
> 

<span data-ttu-id="1f975-106">이 항목에서는 외부에서 인터넷에 액세스할 수 있는 Always On 가용성 그룹에 대해 수신기를 구성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-106">This topic shows you how to configure a listener for an Always On Availability Group that is externally accessible on the internet.</span></span> <span data-ttu-id="1f975-107">수신기를 구성하려면 클라우드 서비스의 **공용 VIP(가상 IP)** 주소를 수신기와 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-107">This is made possible by associating the cloud service's **public Virtual IP (VIP)** address with the listener.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="1f975-108">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1f975-109">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-109">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="1f975-110">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="1f975-111">가용성 그룹은 온-프레미스 전용, Azure 전용 또는 하이브리드 구성에 대한 온-프레미스와 Azure 모두에 걸쳐 있는 복제본을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-111">Your Availability Group can contain replicas that are on-premises only, Azure only, or span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="1f975-112">Azure 복제본은 동일한 지역 내 또는 여러 Vnet(가상 네트워크)을 사용하 여 여러 지역에 걸쳐 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-112">Azure replicas can reside within the same region or across multiple regions using multiple virtual networks (VNets).</span></span> <span data-ttu-id="1f975-113">다음 단계에서는 [가용성 그룹을 구성](../classic/portal-sql-alwayson-availability-groups.md)했지만 수신기는 구성하지 않았다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-113">The steps below assume you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-external-listeners"></a><span data-ttu-id="1f975-114">외부 수신기에 대한 지침 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="1f975-114">Guidelines and limitations for external listeners</span></span>
<span data-ttu-id="1f975-115">클라우드 서비스 공용 VIP 주소를 사용하여 배포할 경우 Azure의 가용성 그룹 수신기에 다음과 같은 지침이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-115">Note the following guidelines about the availability group listener in Azure when you are deploying using the cloud service pubic VIP address:</span></span>

* <span data-ttu-id="1f975-116">가용성 그룹 수신기는 Windows Server 2008 R2, Windows Server 2012 및 Windows Server 2012 R2에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-116">The availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="1f975-117">클라이언트 응용 프로그램은 가용성 그룹 VM이 포함된 것과는 다른 클라우드 서비스에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-117">The client application must reside on a different cloud service than the one that contains your availability group VMs.</span></span> <span data-ttu-id="1f975-118">Azure는 동일한 클라우드 서비스에 있는 클라이언트 및 서버에서의 직접 서버 반환을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-118">Azure does not support direct server return with client and server in the same cloud service.</span></span>
* <span data-ttu-id="1f975-119">이 문서의 단계는 기본적으로 클라우드 서비스 VIP(가상 IP) 주소를 사용하도록 하나의 수신기를 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-119">By default, the steps in this article show how to configure one listener to use the cloud service Virtual IP (VIP) address.</span></span> <span data-ttu-id="1f975-120">그러나 클라우드 서비스에 대한 여러 VIP 주소를 예약하고 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-120">However, it is possible to reserve and create multiple VIP addresses for your cloud service.</span></span> <span data-ttu-id="1f975-121">이렇게 하면 이 문서의 단계를 사용하여 각각 다른 VIP와 연결된 여러 수신기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-121">This enables you to use the steps in this article to create multiple listeners that are each associated with a different VIP.</span></span> <span data-ttu-id="1f975-122">여러 VIP 주소를 만드는 방법에 대한 자세한 내용은 [클라우드 서비스당 여러 VIP](../../../load-balancer/load-balancer-multivip.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f975-122">For information on how to create multiple VIP addresses, see [Multiple VIPs per cloud service](../../../load-balancer/load-balancer-multivip.md).</span></span>
* <span data-ttu-id="1f975-123">하이브리드 환경에 대한 수신기를 만드는 경우 온-프레미스 네트워크에 Azure 가상 네트워크와 사이트-사이트 VPN뿐 아니라 공용 인터넷에 대한 연결이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-123">If you are creating a listener for a hybrid environment, the on-premises network must have connectivity to the public Internet in addition to the site-to-site VPN with the Azure virtual network.</span></span> <span data-ttu-id="1f975-124">Azure 서브넷에 있을 때 가용성 그룹 수신기는 해당 클라우드 서비스의 공용 IP 주소를 통해서만 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-124">When in the Azure subnet, the availability group listener is reachable only by the public IP address of the respective cloud service.</span></span>
* <span data-ttu-id="1f975-125">ILB(내부 부하 분산 장치)를 사용하여 내부 수신기도 있는 동일한 클라우드 서비스에서 외부 수신기를 만들 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-125">It is not supported to create an external listener in the same cloud service where you also have an internal listener using the Internal Load Balancer (ILB).</span></span>

## <a name="determine-the-accessibility-of-the-listener"></a><span data-ttu-id="1f975-126">수신기의 액세스 가능 여부 확인</span><span class="sxs-lookup"><span data-stu-id="1f975-126">Determine the accessibility of the listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="1f975-127">이 문서에서는 **외부 부하 분산**을 사용하는 수신기를 만드는 데 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-127">This article focuses on creating a listener that uses **external load balancing**.</span></span> <span data-ttu-id="1f975-128">가상 네트워크에 대한 개인 수신기를 만들려면 [ILB를 사용하여 수신기](../classic/ps-sql-int-listener.md)를 설정하는 단계를 설명하는 이 문서의 다른 버전을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f975-128">If you want a listener that is private to your virtual network, see the version of this article that provides steps for setting up an [listener with ILB](../classic/ps-sql-int-listener.md)</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="1f975-129">직접 서버 반환이 있는 부하 분산 VM 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="1f975-129">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="1f975-130">외부 부하 분산에서는 VM을 호스팅하는 클라우드 서비스의 공용 가상 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-130">External load balancing uses the virtual the public Virtual IP address of the cloud service that hosts your VMs.</span></span> <span data-ttu-id="1f975-131">따라서 이 경우에는 부하 분산 장치를 만들거나 구성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-131">So you do not need to create or configure the load balancer in this case.</span></span>

<span data-ttu-id="1f975-132">Azure 복제본을 호스트하는 각 VM에 대해 부하가 분산된 끝점을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-132">You must create a load-balanced endpoint for each VM hosting an Azure replica.</span></span> <span data-ttu-id="1f975-133">여러 지역에 복제본이 있는 경우 해당 지역에 대한 각 복제본은 동일한 VNet의 동일한 클라우드 서비스에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-133">If you have replicas in multiple regions, each replica for that region must be in the same cloud service in the same VNet.</span></span> <span data-ttu-id="1f975-134">여러 Azure 지역에 걸쳐 있는 가용성 그룹 복제본을 만들려면 여러 VNet을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-134">Creating Availability Group replicas that span multiple Azure regions requires configuring multiple VNets.</span></span> <span data-ttu-id="1f975-135">VNet 간 연결 구성에 대한 자세한 내용은 [VNet 간 연결 구성](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f975-135">For more information on configuring cross VNet connectivity, see  [Configure VNet to VNet Connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="1f975-136">Azure 포털에서 복제본을 호스트하는 각 VM으로 이동하고 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-136">In the Azure portal, navigate to each VM hosting a replica and view the details.</span></span>
2. <span data-ttu-id="1f975-137">각 VM에 대한 **끝점** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-137">Click the **Endpoints** tab for each of the VMs.</span></span>
3. <span data-ttu-id="1f975-138">사용할 수신기 끝점의 **이름** 및 **공용 포트**가 사용 중이지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-138">Verify that the **Name** and **Public Port** of the listener endpoint you want to use is not already in use.</span></span> <span data-ttu-id="1f975-139">아래 예제에서는 이름이 "MyEndpoint"이고 포트는 "1433"입니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-139">In the example below, the name is “MyEndpoint” and the port is “1433”.</span></span>
4. <span data-ttu-id="1f975-140">로컬 클라이언트에서 [최신 PowerShell 모듈](https://azure.microsoft.com/downloads/)을 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-140">On your local client, download and install [the latest PowerShell module](https://azure.microsoft.com/downloads/).</span></span>
5. <span data-ttu-id="1f975-141">**Azure PowerShell**을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-141">Launch **Azure PowerShell**.</span></span> <span data-ttu-id="1f975-142">새 PowerShell 세션이 Azure 관리 모듈이 로드된 상태로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-142">A new PowerShell session is opened with the Azure administrative modules loaded.</span></span>
6. <span data-ttu-id="1f975-143">**Get-AzurePublishSettingsFile**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-143">Run **Get-AzurePublishSettingsFile**.</span></span> <span data-ttu-id="1f975-144">이 cmdlet은 게시 설정 파일을 로컬 디렉터리에 다운로드하도록 브라우저로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-144">This cmdlet directs you to a browser to download a publish settings file to a local directory.</span></span> <span data-ttu-id="1f975-145">Azure 구독에 대한 로그인 자격 증명을 묻는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-145">You may be prompted for your log-in credentials for your Azure subscription.</span></span>
7. <span data-ttu-id="1f975-146">다운로드한 게시 설정 파일의 경로와 함께 **Import-AzurePublishSettingsFile** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-146">Run the **Import-AzurePublishSettingsFile** command with the path of the publish settings file that you downloaded:</span></span>
   
        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>
   
    <span data-ttu-id="1f975-147">게시 설정 파일을 가져오면 PowerShell 세션에서 Azure 구독을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-147">Once the publish settings file is imported, you can manage your Azure subscription in the PowerShell session.</span></span>
    
1. <span data-ttu-id="1f975-148">아래의 PowerShell 스크립트를 텍스트 편집기에 복사하고 사용자 환경에 맞게 변수 값을 설정합니다(일부 매개 변수에 대한 기본값 제공).</span><span class="sxs-lookup"><span data-stu-id="1f975-148">Copy the PowerShell script below into a text editor and set the variable values to suit your environment (defaults have been provided for some parameters).</span></span> <span data-ttu-id="1f975-149">가용성 그룹에 Azure 지역에 걸쳐 있는 경우, 데이터센터에 있는 클라우드 서비스 및 노드에 대해 각각의 데이터센터에서 한 번씩 스크립트를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-149">Note that if your availability group spans Azure regions, you must run the script once in each datacenter for the cloud service and nodes that reside in that datacenter.</span></span>
   
        # Define variables
        $ServiceName = "<MyCloudService>" # the name of the cloud service that contains the availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in the same cloud service, separated by commas
   
        # Configure a load balanced endpoint for each node in $AGNodes, with direct server return enabled
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -Protocol "TCP" -PublicPort 1433 -LocalPort 1433 -LBSetName "ListenerEndpointLB" -ProbePort 59999 -ProbeProtocol "TCP" -DirectServerReturn $true | Update-AzureVM
        }

2. <span data-ttu-id="1f975-150">변수를 설정한 후에는 텍스트 편집기에서 해당 스크립트를 Azure PowerShell 세션에 복사하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-150">Once you have set the variables, copy the script from the text editor into your Azure PowerShell session to run it.</span></span> <span data-ttu-id="1f975-151">프롬프트에 >>가 계속 표시되면 Enter를 다시 입력하여 스크립트 실행이 시작되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-151">If the prompt still shows >>, type ENTER again to make sure the script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="1f975-152">필요한 경우 KB2854082가 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-152">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-the-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="1f975-153">가용성 그룹 노드에서 방화벽 포트 열기</span><span class="sxs-lookup"><span data-stu-id="1f975-153">Open the firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-the-availability-group-listener"></a><span data-ttu-id="1f975-154">가용성 그룹 수신기 만들기</span><span class="sxs-lookup"><span data-stu-id="1f975-154">Create the availability group listener</span></span>

<span data-ttu-id="1f975-155">두 단계로 가용성 그룹 수신기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-155">Create the availability group listener in two steps.</span></span> <span data-ttu-id="1f975-156">먼저, 클라이언트 액세스 지점 클러스터 리소스를 만들고 종속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-156">First, create the client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="1f975-157">두번째로, PowerShell로 클러스터 리소스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-157">Second, configure the cluster resources with PowerShell.</span></span>

### <a name="create-the-client-access-point-and-configure-the-cluster-dependencies"></a><span data-ttu-id="1f975-158">클라이언트 액세스 지점을 만들고 클러스터 종속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-158">Create the client access point and configure the cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-the-cluster-resources-in-powershell"></a><span data-ttu-id="1f975-159">PowerShell로 클러스터 리소스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-159">Configure the cluster resources in PowerShell</span></span>
1. <span data-ttu-id="1f975-160">외부 부하 분산에서는 복제본을 포함하는 클라우드 서비스의 공용 가상 IP 주소를 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-160">For external load balancing, you must obtain the public virtual IP address of the cloud service that contains your replicas.</span></span> <span data-ttu-id="1f975-161">Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-161">Log into the Azure portal.</span></span> <span data-ttu-id="1f975-162">가용성 그룹 VM이 포함된 클라우드 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-162">Navigate to the cloud service that contains your availability group VM.</span></span> <span data-ttu-id="1f975-163">**대시보드** 보기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-163">Open the **Dashboard** view.</span></span>
2. <span data-ttu-id="1f975-164">**공용 VIP(가상 IP) 주소**아래에 표시된 주소를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-164">Note the address shown under **Public Virtual IP (VIP) Address**.</span></span> <span data-ttu-id="1f975-165">솔루션이 Vnet에 걸쳐 있으면 복제본을 호스팅하는 VM이 포함된 각 클라우드 서비스에 대해 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-165">If your solution spans VNets, repeat this step for each cloud service that contains a VM that hosts a replica.</span></span>
3. <span data-ttu-id="1f975-166">VM 중 하나에서 아래의 PowerShell 스크립트를 텍스트 편집기에 복사하 고 앞에서 기록한 값으로 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-166">On one of the VMs, copy the PowerShell script below into a text editor and set the variables to the values you noted earlier.</span></span>
   
        # Define variables
        $ClusterNetworkName = "<ClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
        $IPResourceName = "<IPResourceName>" # the IP Address resource name
        $CloudServiceIP = "<X.X.X.X>" # Public Virtual IP (VIP) address of your cloud service
   
        Import-Module FailoverClusters
   
        # If you are using Windows Server 2012 or higher, use the Get-Cluster Resource command. If you are using Windows Server 2008 R2, use the cluster res command. Both commands are commented out. Choose the one applicable to your environment and remove the # at the beginning of the line to convert the comment to an executable line of code.
   
        # Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$CloudServiceIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"OverrideAddressMatch"=1;"EnableDhcp"=0}
        # cluster res $IPResourceName /priv enabledhcp=0 overrideaddressmatch=1 address=$CloudServiceIP probeport=59999  subnetmask=255.255.255.255
4. <span data-ttu-id="1f975-167">변수를 설정한 후에는 앞으로 온 Windows PowerShell 창을 열고 텍스트 편집기의 스크립트를 복사하여 Azure PowerShell 세션에 붙여넣어 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-167">Once you have set the variables, open an elevated Windows PowerShell window, then copy the script from the text editor and paste into your Azure PowerShell session to run it.</span></span> <span data-ttu-id="1f975-168">프롬프트에 >>가 계속 표시되면 Enter를 다시 입력하여 스크립트 실행이 시작되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-168">If the prompt still shows >>, type ENTER again to make sure the script starts running.</span></span>
5. <span data-ttu-id="1f975-169">각 VM에서 이 작업을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-169">Repeat this on each VM.</span></span> <span data-ttu-id="1f975-170">이 스크립트는 클라우드 서비스의 IP 주소로 IP 주소 리소스를 구성하고 프로프 포트 등의 다른 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-170">This script configures the IP Address resource with the IP address of the cloud service and sets other parameters like the probe port.</span></span> <span data-ttu-id="1f975-171">IP 주소 리소스를 온라인으로 불러올 때 이 자습서의 앞 부분에서 부하 분산된 끝점으로부터 프로브 포트에 대한 폴링에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-171">When the IP Address resource is brought online, it can then respond to the polling on the probe port from the load-balanced endpoint created earlier in this tutorial.</span></span>

## <a name="bring-the-listener-online"></a><span data-ttu-id="1f975-172">수신기를 온라인 상태로 만들기</span><span class="sxs-lookup"><span data-stu-id="1f975-172">Bring the listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="1f975-173">추가 작업 항목</span><span class="sxs-lookup"><span data-stu-id="1f975-173">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-the-availability-group-listener-within-the-same-vnet"></a><span data-ttu-id="1f975-174">(동일한 VNet 내)가용성 그룹 수신기 테스트</span><span class="sxs-lookup"><span data-stu-id="1f975-174">Test the availability group listener (within the same VNet)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="test-the-availability-group-listener-over-the-internet"></a><span data-ttu-id="1f975-175">(인터넷을 통해)가용성 그룹 수신기 테스트</span><span class="sxs-lookup"><span data-stu-id="1f975-175">Test the availability group listener (over the internet)</span></span>
<span data-ttu-id="1f975-176">가상 네트워크 외부에서 수신기에 액세스하려면 동일한 VNet 안에서만 액세스 가능한 ILB보다는 외부/공용 부하 분산(이 항목에서 설명)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-176">In order to access the listener from outside the virtual network, you must be using external/public load balancing (described in this topic) rather than ILB, which is only accesible within the same VNet.</span></span> <span data-ttu-id="1f975-177">연결 문자열에서 클라우드 서비스 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-177">In the connection string, you specify the cloud service name.</span></span> <span data-ttu-id="1f975-178">예를 들어 이름이 *mycloudservice*인 클라우드 서비스가 있는 경우 sqlcmd 문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-178">For example, if you had a cloud service with the name *mycloudservice*, the sqlcmd statement would be as follows:</span></span>

    sqlcmd -S "mycloudservice.cloudapp.net,<EndpointPort>" -d "<DatabaseName>" -U "<LoginId>" -P "<Password>"  -Q "select @@servername, db_name()" -l 15

<span data-ttu-id="1f975-179">앞의 예와 달리 호출자가 인터넷을 통해 windows 인증을 사용할 수 없으므로 SQL 인증을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-179">Unlike the previous example, SQL authentication must be used, because the caller cannot use windows authentication over the internet.</span></span> <span data-ttu-id="1f975-180">자세한 내용은 [Azure VM의 Always On 가용성 그룹: 클라이언트 연결 시나리오](http://blogs.msdn.com/b/sqlcat/archive/2014/02/03/alwayson-availability-group-in-windows-azure-vm-client-connectivity-scenarios.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f975-180">For more information, see [Always On Availability Group in Azure VM: Client Connectivity Scenarios](http://blogs.msdn.com/b/sqlcat/archive/2014/02/03/alwayson-availability-group-in-windows-azure-vm-client-connectivity-scenarios.aspx).</span></span> <span data-ttu-id="1f975-181">SQL 인증을 사용할 때는 두 복제본에서 동일한 로그인을 만들 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-181">When using SQL authentication, make sure that you create the same login on both replicas.</span></span> <span data-ttu-id="1f975-182">가용성 그룹 로그인 문제 해결에 대한 자세한 내용은 [로그인 매핑 또는 포함된 SQL 데이터베이스 사용자를 통해 다른 복제본에 연결하고 가용성 데이터베이스에 매핑하는 방법](http://blogs.msdn.com/b/alwaysonpro/archive/2014/02/19/how-to-map-logins-or-use-contained-sql-database-user-to-connect-to-other-replicas-and-map-to-availability-databases.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f975-182">For more information about troubleshooting logins with Availability Groups, see [How to map logins or use contained SQL database user to connect to other replicas and map to availability databases](http://blogs.msdn.com/b/alwaysonpro/archive/2014/02/19/how-to-map-logins-or-use-contained-sql-database-user-to-connect-to-other-replicas-and-map-to-availability-databases.aspx).</span></span>

<span data-ttu-id="1f975-183">Always On 복제본이 다른 서브넷에 있는 경우 클라이언트는 연결 문자열에 **MultisubnetFailover=True** 를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-183">If the Always On replicas are in different subnets, clients must specify **MultisubnetFailover=True** in the connection string.</span></span> <span data-ttu-id="1f975-184">그러면 다른 서브넷에 있는 복제본에 대한 병렬 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-184">This results in parallel connection attempts to replicas in the different subnets.</span></span> <span data-ttu-id="1f975-185">이 시나리오에는 영역 간 Always On 가용성 그룹 배포가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f975-185">Note that this scenario includes a cross-region Always On Availability Group deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f975-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f975-186">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]

