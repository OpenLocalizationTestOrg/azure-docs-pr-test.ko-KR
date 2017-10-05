---
title: "Azure Virtual Machines에서 SQL Server 가용성 그룹 수신기 만들기 | Microsoft Docs"
description: "Azure Virtual Machines에서 SQL Server에 대한 Always On 가용성 그룹용 수신기를 만드는 단계별 지침"
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: d1f291e9-9af2-41ba-9d29-9541e3adcfcf
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/01/2017
ms.author: mikeray
ms.openlocfilehash: 09fed7e785708d4afe64905de973becc188181d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-load-balancer-for-an-always-on-availability-group-in-azure"></a><span data-ttu-id="0f566-103">Azure에서 Always On 가용성 그룹에 대한 부하 분산 장치 구성</span><span class="sxs-lookup"><span data-stu-id="0f566-103">Configure a load balancer for an Always On availability group in Azure</span></span>
<span data-ttu-id="0f566-104">이 문서에서는 Azure Resource Manager로 실행 중인 Azure Virtual Machines에서 SQL Server Always On 가용성 그룹에 대한 부하 분산 장치를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-104">This article explains how to create a load balancer for a SQL Server Always On availability group in Azure virtual machines that are running with Azure Resource Manager.</span></span> <span data-ttu-id="0f566-105">SQL Server 인스턴스가 Azure 가상 컴퓨터에 있는 경우 가용성 그룹을 사용하려면 부하 분산 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-105">An availability group requires a load balancer when the SQL Server instances are on Azure virtual machines.</span></span> <span data-ttu-id="0f566-106">부하 분산 장치는 가용성 그룹 수신기의 IP 주소를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-106">The load balancer stores the IP address for the availability group listener.</span></span> <span data-ttu-id="0f566-107">가용성 그룹이 여러 지역에 분산된 경우 각 지역에 부하 분산 장치가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-107">If an availability group spans multiple regions, each region needs a load balancer.</span></span>

<span data-ttu-id="0f566-108">이 작업을 완료하려면 Resource Manager로 실행 중인 Azure Virtual Machines에 SQL Server 가용성 그룹이 배포되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-108">To complete this task, you need to have a SQL Server availability group deployed on Azure virtual machines that are running with Resource Manager.</span></span> <span data-ttu-id="0f566-109">두 SQL Server 가상 컴퓨터는 동일한 가용성 집합에 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-109">Both SQL Server virtual machines must belong to the same availability set.</span></span> <span data-ttu-id="0f566-110">[Microsoft 템플릿](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)을 사용하여 Resource Manager에서 가용성 그룹을 자동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-110">You can use the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) to automatically create the availability group in Resource Manager.</span></span> <span data-ttu-id="0f566-111">이 템플릿은 내부 부하 분산 장치를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-111">This template automatically creates an internal load balancer for you.</span></span> 

<span data-ttu-id="0f566-112">원하는 경우 [수동으로 가용성 그룹을 구성](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-112">If you prefer, you can [manually configure an availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="0f566-113">이 문서를 진행하려면 가용성 그룹이 이미 구성되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-113">This article requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="0f566-114">관련 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-114">Related topics include:</span></span>

* [<span data-ttu-id="0f566-115">Azure VM의 Always On 가용성 그룹 구성(GUI)</span><span class="sxs-lookup"><span data-stu-id="0f566-115">Configure Always On availability groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="0f566-116">Azure 리소스 관리자 및 PowerShell을 사용하여 VNet-VNet 연결 구성</span><span class="sxs-lookup"><span data-stu-id="0f566-116">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

<span data-ttu-id="0f566-117">이 문서를 통해 Azure Portal에서 부하 분산 장치를 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-117">By walking through this article, you create and configure a load balancer in the Azure portal.</span></span> <span data-ttu-id="0f566-118">프로세스 완료 후에는 가용성 그룹 수신기에 대한 부하 분산 장치에서 IP 주소를 사용하도록 클러스터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-118">After the process is complete, you configure the cluster to use the IP address from the load balancer for the availability group listener.</span></span>

## <a name="create-and-configure-the-load-balancer-in-the-azure-portal"></a><span data-ttu-id="0f566-119">Azure 포털에서 부하 분산 장치 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="0f566-119">Create and configure the load balancer in the Azure portal</span></span>
<span data-ttu-id="0f566-120">작업의 이 부분에서는 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-120">In this portion of the task, do the following:</span></span>

1. <span data-ttu-id="0f566-121">Azure Portal에서 부하 분산 장치를 만들고 IP 주소를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-121">In the Azure portal, create the load balancer and configure the IP address.</span></span>
2. <span data-ttu-id="0f566-122">백 엔드 풀을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-122">Configure the back-end pool.</span></span>
3. <span data-ttu-id="0f566-123">프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-123">Create the probe.</span></span> 
4. <span data-ttu-id="0f566-124">부하 분산 규칙을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-124">Set the load balancing rules.</span></span>

> [!NOTE]
> <span data-ttu-id="0f566-125">여러 리소스 그룹 및 지역에 SQL Server 인스턴스가 있는 경우 리소스 그룹당 한 번씩 각 단계를 두 번 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-125">If the SQL Server instances are in multiple resource groups and regions, perform each step twice, once in each resource group.</span></span>
> 
> 

### <a name="step-1-create-the-load-balancer-and-configure-the-ip-address"></a><span data-ttu-id="0f566-126">1단계: 부하 분산 장치 만들기 및 IP 주소 구성</span><span class="sxs-lookup"><span data-stu-id="0f566-126">Step 1: Create the load balancer and configure the IP address</span></span>
<span data-ttu-id="0f566-127">먼저, 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-127">First, create the load balancer.</span></span> 

1. <span data-ttu-id="0f566-128">Azure 포털에서 SQL Server 가상 컴퓨터를 포함하는 리소스 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-128">In the Azure portal, open the resource group that contains the SQL Server virtual machines.</span></span> 

2. <span data-ttu-id="0f566-129">리소스 그룹에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-129">In the resource group, click **Add**.</span></span>

3. <span data-ttu-id="0f566-130">**부하 분산 장치**를 검색한 후 검색 결과에서 **Microsoft**에서 게시하는 **부하 분산 장치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-130">Search for **load balancer** and then, in the search results, select **Load Balancer**, which is published by **Microsoft**.</span></span>

4. <span data-ttu-id="0f566-131">**부하 분산 장치** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-131">On the **Load Balancer** blade, click **Create**.</span></span>

5. <span data-ttu-id="0f566-132">**부하 분산 장치 만들기** 대화 상자에서 다음과 같이 부하 분산 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-132">In the **Create load balancer** dialog box, configure the load balancer as follows:</span></span>

   | <span data-ttu-id="0f566-133">설정</span><span class="sxs-lookup"><span data-stu-id="0f566-133">Setting</span></span> | <span data-ttu-id="0f566-134">값</span><span class="sxs-lookup"><span data-stu-id="0f566-134">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="0f566-135">**Name**</span><span class="sxs-lookup"><span data-stu-id="0f566-135">**Name**</span></span> |<span data-ttu-id="0f566-136">부하 분산 장치를 나타내는 텍스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-136">A text name representing the load balancer.</span></span> <span data-ttu-id="0f566-137">예를 들어 **sqlLB**입니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-137">For example, **sqlLB**.</span></span> |
   | <span data-ttu-id="0f566-138">**형식**</span><span class="sxs-lookup"><span data-stu-id="0f566-138">**Type**</span></span> |<span data-ttu-id="0f566-139">**내부**: 대부분의 구현에서는 내부 부하 분산 장치를 사용하며, 동일한 가상 네트워크 내에 있는 응용 프로그램은 가용성 그룹에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-139">**Internal**: Most implementations use an internal load balancer, which allows applications within the same virtual network to connect to the availability group.</span></span>  </br> <span data-ttu-id="0f566-140">**외부**: 응용 프로그램이 공용 인터넷 연결을 통해 가용성 그룹에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-140">**External**: Allows applications to connect to the availability group through a public Internet connection.</span></span> |
   | <span data-ttu-id="0f566-141">**가상 네트워크**</span><span class="sxs-lookup"><span data-stu-id="0f566-141">**Virtual network**</span></span> |<span data-ttu-id="0f566-142">SQL Server 인스턴스가 있는 가상 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-142">Select the virtual network that the SQL Server intances are in.</span></span> |
   | <span data-ttu-id="0f566-143">**서브넷**</span><span class="sxs-lookup"><span data-stu-id="0f566-143">**Subnet**</span></span> |<span data-ttu-id="0f566-144">SQL Server 인스턴스가 있는 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-144">Select the subnet that the SQL Server instances are in.</span></span> |
   | <span data-ttu-id="0f566-145">**IP 주소 할당**</span><span class="sxs-lookup"><span data-stu-id="0f566-145">**IP address assignment**</span></span> |<span data-ttu-id="0f566-146">**정적**</span><span class="sxs-lookup"><span data-stu-id="0f566-146">**Static**</span></span> |
   | <span data-ttu-id="0f566-147">**개인 IP 주소**</span><span class="sxs-lookup"><span data-stu-id="0f566-147">**Private IP address**</span></span> |<span data-ttu-id="0f566-148">서브넷에서 사용 가능한 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-148">Specify an available IP address from the subnet.</span></span> <span data-ttu-id="0f566-149">클러스터에서 수신기를 만들 때 이 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-149">Use this IP address when you create a listener on the cluster.</span></span> <span data-ttu-id="0f566-150">이 주소는 이 문서 뒷부분의 PowerShell 스크립트에서 `$ILBIP` 변수에 대해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-150">In a PowerShell script, later in this article, use this address for the `$ILBIP` variable.</span></span> |
   | <span data-ttu-id="0f566-151">**구독**</span><span class="sxs-lookup"><span data-stu-id="0f566-151">**Subscription**</span></span> |<span data-ttu-id="0f566-152">구독이 여러 개인 경우 이 필드가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-152">If you have multiple subscriptions, this field might appear.</span></span> <span data-ttu-id="0f566-153">이 리소스와 연결할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-153">Select the subscription that you want to associate with this resource.</span></span> <span data-ttu-id="0f566-154">일반적으로 가용성 그룹에 대한 모든 리소스와 동일한 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-154">It is normally the same subscription as all the resources for the availability group.</span></span> |
   | <span data-ttu-id="0f566-155">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="0f566-155">**Resource group**</span></span> |<span data-ttu-id="0f566-156">SQL Server 인스턴스가 있는 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-156">Select the resource group that the SQL Server instances are in.</span></span> |
   | <span data-ttu-id="0f566-157">**위치**:</span><span class="sxs-lookup"><span data-stu-id="0f566-157">**Location**</span></span> |<span data-ttu-id="0f566-158">SQL Server 인스턴스가 있는 Azure 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-158">Select the Azure location that the SQL Server instances are in.</span></span> |

6. <span data-ttu-id="0f566-159">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-159">Click **Create**.</span></span> 

<span data-ttu-id="0f566-160">Azure에서 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-160">Azure creates the load balancer.</span></span> <span data-ttu-id="0f566-161">부하 분산 장치는 특정 네트워크, 서브넷, 리소스 그룹 및 위치에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-161">The load balancer belongs to a specific network, subnet, resource group, and location.</span></span> <span data-ttu-id="0f566-162">Azure에서 작업이 완료되면 Azure에서 부하 분산 장치 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-162">After Azure completes the task, verify the load balancer settings in Azure.</span></span> 

### <a name="step-2-configure-the-back-end-pool"></a><span data-ttu-id="0f566-163">2단계: 백 엔드 풀 구성</span><span class="sxs-lookup"><span data-stu-id="0f566-163">Step 2: Configure the back-end pool</span></span>
<span data-ttu-id="0f566-164">Azure에서 백 엔드 주소 풀 *백 엔드 풀*이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-164">Azure calls the back-end address pool *backend pool*.</span></span> <span data-ttu-id="0f566-165">이 경우 백 엔드 풀은 가용성 그룹에 있는 두 SQL Server 인스턴스의 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-165">In this case, the back-end pool is the addresses of the two SQL Server instances in your availability group.</span></span> 

1. <span data-ttu-id="0f566-166">리소스 그룹에서, 만든 부하 분산 장치를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-166">In your resource group, click the load balancer that you created.</span></span> 

2. <span data-ttu-id="0f566-167">**설정**에서 **백 엔드 풀**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-167">On **Settings**, click **Backend pools**.</span></span>

3. <span data-ttu-id="0f566-168">**백 엔드 풀**에서 **추가**를 클릭하여 백 엔드 주소 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-168">On **Backend pools**, click **Add** to create a back-end address pool.</span></span> 

4. <span data-ttu-id="0f566-169">**백 엔드 풀 추가**에서 **이름**에 백 엔드 풀의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-169">On **Add backend pool**, under **Name**, type a name for the back-end pool.</span></span>

5. <span data-ttu-id="0f566-170">**가상 컴퓨터**에서 **가상 컴퓨터 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-170">Under **Virtual machines**, click **Add a virtual machine**.</span></span> 

6. <span data-ttu-id="0f566-171">**가상 컴퓨터 선택**에서 **가용성 집합 선택**을 클릭하고 SQL Server 가상 컴퓨터가 속한 가용성 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-171">Under **Choose virtual machines**, click **Choose an availability set**, and then specify the availability set that the SQL Server virtual machines belong to.</span></span>

7. <span data-ttu-id="0f566-172">가용성 집합을 선택한 후 **가상 컴퓨터 선택**을 클릭하고, 가용성 그룹에서 SQL Server 인스턴스를 호스트하는 가상 컴퓨터를 두 개 선택한 후 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-172">After you have chosen the availability set, click **Choose the virtual machines**, select the two virtual machines that host the SQL Server instances in the availability group, and then click **Select**.</span></span> 

8. <span data-ttu-id="0f566-173">**확인**을 클릭하여 **가상 컴퓨터 선택** 및 **백 엔드 풀 추가**에 대한 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-173">Click **OK** to close the blades for **Choose virtual machines**, and **Add backend pool**.</span></span> 

<span data-ttu-id="0f566-174">Azure에서 백 엔드 주소 풀에 대한 설정이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-174">Azure updates the settings for the back-end address pool.</span></span> <span data-ttu-id="0f566-175">이제 가용성 집합에는 두 개의 SQL Server 인스턴스에 대한 풀이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-175">Now your availability set has a pool of two SQL Server instances.</span></span>

### <a name="step-3-create-a-probe"></a><span data-ttu-id="0f566-176">3단계: 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="0f566-176">Step 3: Create a probe</span></span>
<span data-ttu-id="0f566-177">프로브는 Azure에서 현재 가용성 그룹 수신기를 소유하는 SQL Server 인스턴스를 확인하는 방법을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-177">The probe defines how Azure verifies which of the SQL Server instances currently owns the availability group listener.</span></span> <span data-ttu-id="0f566-178">Azure는 프로브를 만들 때 정의한 포트의 IP 주소를 기반으로 서비스를 프로브합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-178">Azure probes the service based on the IP address on a port that you define when you create the probe.</span></span>

1. <span data-ttu-id="0f566-179">부하 분산 장치 **설정** 블레이드에서 **상태 프로브**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-179">On the load balancer **Settings** blade, click **Health probes**.</span></span> 

2. <span data-ttu-id="0f566-180">**상태 프로브** 블레이드에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-180">On the **Health probes** blade, click **Add**.</span></span>

3. <span data-ttu-id="0f566-181">**프로브 추가** 블레이드에서 프로브를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-181">Configure the probe on the **Add probe** blade.</span></span> <span data-ttu-id="0f566-182">다음 값을 사용하여 프로브를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-182">Use the following values to configure the probe:</span></span>

   | <span data-ttu-id="0f566-183">설정</span><span class="sxs-lookup"><span data-stu-id="0f566-183">Setting</span></span> | <span data-ttu-id="0f566-184">값</span><span class="sxs-lookup"><span data-stu-id="0f566-184">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="0f566-185">**Name**</span><span class="sxs-lookup"><span data-stu-id="0f566-185">**Name**</span></span> |<span data-ttu-id="0f566-186">프로브를 나타내는 텍스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-186">A text name representing the probe.</span></span> <span data-ttu-id="0f566-187">예를 들어 **SQLAlwaysOnEndPointProbe**입니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-187">For example, **SQLAlwaysOnEndPointProbe**.</span></span> |
   | <span data-ttu-id="0f566-188">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="0f566-188">**Protocol**</span></span> |<span data-ttu-id="0f566-189">**TCP**</span><span class="sxs-lookup"><span data-stu-id="0f566-189">**TCP**</span></span> |
   | <span data-ttu-id="0f566-190">**포트**</span><span class="sxs-lookup"><span data-stu-id="0f566-190">**Port**</span></span> |<span data-ttu-id="0f566-191">사용 가능한 모든 포트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-191">You can use any available port.</span></span> <span data-ttu-id="0f566-192">예를 들어 *59999*입니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-192">For example, *59999*.</span></span> |
   | <span data-ttu-id="0f566-193">**간격**</span><span class="sxs-lookup"><span data-stu-id="0f566-193">**Interval**</span></span> |<span data-ttu-id="0f566-194">*5*</span><span class="sxs-lookup"><span data-stu-id="0f566-194">*5*</span></span> |
   | <span data-ttu-id="0f566-195">**비정상 임계값**</span><span class="sxs-lookup"><span data-stu-id="0f566-195">**Unhealthy threshold**</span></span> |<span data-ttu-id="0f566-196">*2*</span><span class="sxs-lookup"><span data-stu-id="0f566-196">*2*</span></span> |

4.  <span data-ttu-id="0f566-197">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-197">Click **OK**.</span></span> 

> [!NOTE]
> <span data-ttu-id="0f566-198">지정한 포트가 두 SQL Server 인스턴스의 방화벽에서 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-198">Make sure that the port you specify is open on the firewall of both SQL Server instances.</span></span> <span data-ttu-id="0f566-199">두 인스턴스 모두 사용하는 TCP 포트에 대한 인바운드 규칙이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-199">Both instances require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="0f566-200">자세한 내용은 [방화벽 규칙 추가 또는 편집](http://technet.microsoft.com/library/cc753558.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f566-200">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span> 
> 
> 

<span data-ttu-id="0f566-201">Azure는 프로브를 만든 후 가용성 그룹에 대한 수신기가 있는 SQL Server 인스턴스를 테스트하는 데 프로브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-201">Azure creates the probe and then uses it to test which SQL Server instance has the listener for the availability group.</span></span>

### <a name="step-4-set-the-load-balancing-rules"></a><span data-ttu-id="0f566-202">4단계: 부하 분산 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="0f566-202">Step 4: Set the load balancing rules</span></span>
<span data-ttu-id="0f566-203">부하 분산 규칙은 부하 분산 장치가 트래픽을 SQL Server 인스턴스로 라우트하는 방법을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-203">The load balancing rules configure how the load balancer routes traffic to the SQL Server instances.</span></span> <span data-ttu-id="0f566-204">이 부하 분산 장치의 경우 한 번에 두 SQL Server 인스턴스 중 하나만 가용성 그룹 수신기 리소스를 소유하므로 Direct Server Return(DSR)이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-204">For this load balancer, you enable direct server return because only one of the two SQL Server instances owns the availability group listener resource at a time.</span></span>

1. <span data-ttu-id="0f566-205">부하 분산 장치 **설정** 블레이드에서 **부하 분산 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-205">On the load balancer **Settings** blade, click **Load balancing rules**.</span></span> 

2. <span data-ttu-id="0f566-206">**부하 분산 규칙** 블레이드에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-206">On the **Load balancing rules** blade, click **Add**.</span></span>

3. <span data-ttu-id="0f566-207">**부하 분산 규칙 추가** 블레이드에서 부하 분산 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-207">On the **Add load balancing rules** blade, configure the load balancing rule.</span></span> <span data-ttu-id="0f566-208">다음 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-208">Use the following settings:</span></span> 

   | <span data-ttu-id="0f566-209">설정</span><span class="sxs-lookup"><span data-stu-id="0f566-209">Setting</span></span> | <span data-ttu-id="0f566-210">값</span><span class="sxs-lookup"><span data-stu-id="0f566-210">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="0f566-211">**Name**</span><span class="sxs-lookup"><span data-stu-id="0f566-211">**Name**</span></span> |<span data-ttu-id="0f566-212">부하 분산 규칙을 나타내는 텍스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-212">A text name representing the load balancing rules.</span></span> <span data-ttu-id="0f566-213">예를 들어 **SQLAlwaysOnEndPointListener**입니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-213">For example, **SQLAlwaysOnEndPointListener**.</span></span> |
   | <span data-ttu-id="0f566-214">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="0f566-214">**Protocol**</span></span> |<span data-ttu-id="0f566-215">**TCP**</span><span class="sxs-lookup"><span data-stu-id="0f566-215">**TCP**</span></span> |
   | <span data-ttu-id="0f566-216">**포트**</span><span class="sxs-lookup"><span data-stu-id="0f566-216">**Port**</span></span> |<span data-ttu-id="0f566-217">*1433*</span><span class="sxs-lookup"><span data-stu-id="0f566-217">*1433*</span></span> |
   | <span data-ttu-id="0f566-218">**백 엔드 포트**</span><span class="sxs-lookup"><span data-stu-id="0f566-218">**Backend Port**</span></span> |<span data-ttu-id="0f566-219">*1433*. 이 규칙은 **부동 IP(Direct Server Return)**를 사용하므로 이 값은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-219">*1433*. This value is ignored because this rule uses **Floating IP (direct server return)**.</span></span> |
   | <span data-ttu-id="0f566-220">**프로브**</span><span class="sxs-lookup"><span data-stu-id="0f566-220">**Probe**</span></span> |<span data-ttu-id="0f566-221">이 부하 분산 장치에 대해 만든 프로브의 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-221">Use the name of the probe that you created for this load balancer.</span></span> |
   | <span data-ttu-id="0f566-222">**세션 지속성**</span><span class="sxs-lookup"><span data-stu-id="0f566-222">**Session persistence**</span></span> |<span data-ttu-id="0f566-223">**없음**</span><span class="sxs-lookup"><span data-stu-id="0f566-223">**None**</span></span> |
   | <span data-ttu-id="0f566-224">**유휴 제한 시간(분)**</span><span class="sxs-lookup"><span data-stu-id="0f566-224">**Idle timeout (minutes)**</span></span> |<span data-ttu-id="0f566-225">*4*</span><span class="sxs-lookup"><span data-stu-id="0f566-225">*4*</span></span> |
   | <span data-ttu-id="0f566-226">**부동 IP(Direct Server Return)**</span><span class="sxs-lookup"><span data-stu-id="0f566-226">**Floating IP (direct server return)**</span></span> |<span data-ttu-id="0f566-227">**사용**</span><span class="sxs-lookup"><span data-stu-id="0f566-227">**Enabled**</span></span> |

   > [!NOTE]
   > <span data-ttu-id="0f566-228">블레이드에서 모든 설정을 보려면 아래로 스크롤해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-228">You might have to scroll down the blade to view all the settings.</span></span>
   > 

4. <span data-ttu-id="0f566-229">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-229">Click **OK**.</span></span> 
5. <span data-ttu-id="0f566-230">부하 분산 규칙이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-230">Azure configures the load balancing rule.</span></span> <span data-ttu-id="0f566-231">이제 가용성 그룹에 대한 수신기를 호스트하는 SQL Server 인스턴스로 트래픽을 라우트하도록 부하 분산 장치가 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-231">Now the load balancer is configured to route traffic to the SQL Server instance that hosts the listener for the availability group.</span></span> 

<span data-ttu-id="0f566-232">현재 리소스 그룹에는 두 SQL Server 컴퓨터에 모두 연결하는 하나의 부하 분산 장치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-232">At this point, the resource group has a load balancer that connects to both SQL Server machines.</span></span> <span data-ttu-id="0f566-233">부하 분산 장치에는 SQL Server Always On 가용성 그룹 수신기에 대한 IP 주소도 있으므로 두 컴퓨터 중 하나가 가용성 그룹에 대한 요청에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-233">The load balancer also contains an IP address for the SQL Server Always On availability group listener, so that either machine can respond to requests for the availability groups.</span></span>

> [!NOTE]
> <span data-ttu-id="0f566-234">SQL Server 인스턴스가 두 개의 별도 지역에 있는 경우 다른 지역에서 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-234">If your SQL Server instances are in two separate regions, repeat the steps in the other region.</span></span> <span data-ttu-id="0f566-235">각 지역마다 하나의 부하 분산 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-235">Each region requires a load balancer.</span></span> 
> 
> 

## <a name="configure-the-cluster-to-use-the-load-balancer-ip-address"></a><span data-ttu-id="0f566-236">부하 분산 장치 IP 주소를 사용하도록 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="0f566-236">Configure the cluster to use the load balancer IP address</span></span>
<span data-ttu-id="0f566-237">다음 단계는 클러스터에서 수신기를 구성하고 수신기를 온라인 상태로 전환하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-237">The next step is to configure the listener on the cluster, and bring the listener online.</span></span> <span data-ttu-id="0f566-238">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-238">Do the following:</span></span> 

1. <span data-ttu-id="0f566-239">장애 조치(failover) 클러스터에서 가용성 그룹 수신기 만들기</span><span class="sxs-lookup"><span data-stu-id="0f566-239">Create the availability group listener on the failover cluster.</span></span> 

2. <span data-ttu-id="0f566-240">수신기를 온라인 상태로 만들기</span><span class="sxs-lookup"><span data-stu-id="0f566-240">Bring the listener online.</span></span>

### <a name="step-5-create-the-availability-group-listener-on-the-failover-cluster"></a><span data-ttu-id="0f566-241">5단계: 장애 조치(failover) 클러스터에서 가용성 그룹 수신기 만들기</span><span class="sxs-lookup"><span data-stu-id="0f566-241">Step 5: Create the availability group listener on the failover cluster</span></span>
<span data-ttu-id="0f566-242">이 단계에서는 장애 조치(Failover) 클러스터 관리자와 SQL Server Management Studio에서 가용성 그룹 수신기를 수동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-242">In this step, you manually create the availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

### <a name="verify-the-configuration-of-the-listener"></a><span data-ttu-id="0f566-243">수신기의 구성 확인</span><span class="sxs-lookup"><span data-stu-id="0f566-243">Verify the configuration of the listener</span></span>

<span data-ttu-id="0f566-244">클러스터 리소스 및 종속성이 제대로 구성된 경우 SQL Server Management Studio에서 수신기를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-244">If the cluster resources and dependencies are correctly configured, you should be able to view the listener in SQL Server Management Studio.</span></span> <span data-ttu-id="0f566-245">수신기 포트를 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-245">To set the listener port, do the following:</span></span>

1. <span data-ttu-id="0f566-246">SQL Server Management Studio를 시작한 다음 주 복제본에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-246">Start SQL Server Management Studio, and then connect to the primary replica.</span></span>

2. <span data-ttu-id="0f566-247">**AlwaysOn 고가용성** > **가용성 그룹** > **가용성 그룹 수신기**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-247">Go to **AlwaysOn High Availability** > **Availability Groups** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="0f566-248">이제 장애 조치(Failover) 클러스터 관리자에서 만든 수신기 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-248">You should now see the listener name that you created in Failover Cluster Manager.</span></span> 

3. <span data-ttu-id="0f566-249">수신기 이름을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-249">Right-click the listener name, and then click **Properties**.</span></span>

4. <span data-ttu-id="0f566-250">**포트** 상자에서 이전에 사용한 $EndpointPort(1433이 기본값임)를 사용하여 가용성 그룹 수신기에 대한 포트 번호를 지정한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-250">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort you used earlier (1433 was the default), and then click **OK**.</span></span>

<span data-ttu-id="0f566-251">이제 Resource Manager 모드에서 실행 중인 Azure 가상 컴퓨터에 가용성 그룹이 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-251">You now have an availability group in Azure virtual machines running in Resource Manager mode.</span></span> 

## <a name="test-the-connection-to-the-listener"></a><span data-ttu-id="0f566-252">수신기에 대한 연결 테스트</span><span class="sxs-lookup"><span data-stu-id="0f566-252">Test the connection to the listener</span></span>
<span data-ttu-id="0f566-253">다음을 수행하여 연결을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-253">Test the connection by doing the following:</span></span>

1. <span data-ttu-id="0f566-254">동일한 가상 네트워크에 있지만 복제본을 소유하지 않는 SQL Server 인스턴스로 RDP합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-254">RDP to a SQL Server instance that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="0f566-255">이 서버는 클러스터의 다른 SQL Server 인스턴스가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-255">This server can be the other SQL Server instance in the cluster.</span></span>

2. <span data-ttu-id="0f566-256">**sqlcmd** 유틸리티를 사용하여 연결을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-256">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="0f566-257">예를 들어 다음 스크립트는 Windows 인증을 사용하는 수신기를 통해 주 복제본에 대한 **sqlcmd** 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-257">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>
   
        sqlcmd -S <listenerName> -E

<span data-ttu-id="0f566-258">SQLCMD 연결은 주 복제본을 호스트하는 SQL Server 인스턴스에 자동으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-258">The SQLCMD connection automatically connects to the SQL Server instance that hosts the primary replica.</span></span> 

## <a name="create-an-ip-address-for-an-additional-availability-group"></a><span data-ttu-id="0f566-259">추가 가용성 그룹의 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="0f566-259">Create an IP address for an additional availability group</span></span>

<span data-ttu-id="0f566-260">각 가용성 그룹은 별도의 수신기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-260">Each availability group uses a separate listener.</span></span> <span data-ttu-id="0f566-261">각 수신기는 자체 IP 주소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-261">Each listener has its own IP address.</span></span> <span data-ttu-id="0f566-262">동일한 부하 분산 장치를 사용하여 추가 수신기의 IP 주소를 저장하세요.</span><span class="sxs-lookup"><span data-stu-id="0f566-262">Use the same load balancer to hold the IP address for additional listeners.</span></span> <span data-ttu-id="0f566-263">가용성 그룹을 만든 후에는 부하 분산 장치에 IP 주소를 추가한 다음 수신기를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-263">After you create an availability group, add the IP address to the load balancer, and then configure the listener.</span></span>

<span data-ttu-id="0f566-264">Azure Portal을 사용하여 부하 분산 장치에 IP 주소를 추가하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-264">To add an IP address to a load balancer with the Azure portal, do the following:</span></span>

1. <span data-ttu-id="0f566-265">Azure Portal에서 부하 분산 장치가 포함된 리소스 그룹을 열고 부하 분산 장치를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-265">In the Azure portal, open the resource group that contains the load balancer, and then click the load balancer.</span></span> 

2. <span data-ttu-id="0f566-266">**설정**에서 **프런트 엔드 IP 풀**을 클릭한 후 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-266">Under **SETTINGS**, click **Frontend IP pool**, and then click **Add**.</span></span> 

3. <span data-ttu-id="0f566-267">**프런트 엔드 IP 주소 추가**에서 프런트 엔드의 이름을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-267">Under **Add frontend IP address**, assign a name for the front end.</span></span> 

4. <span data-ttu-id="0f566-268">**가상 네트워크** 및 **서브넷**이 SQL Server 인스턴스와 동일한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-268">Verify that the **Virtual network** and the **Subnet** are the same as the SQL Server instances.</span></span>

5. <span data-ttu-id="0f566-269">수신기의 IP 주소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-269">Set the IP address for the listener.</span></span> 
   
   >[!TIP]
   ><span data-ttu-id="0f566-270">IP 주소를 고정으로 설정하고 현재 서브넷에서 사용되지 않는 주소를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-270">You can set the IP address to static and type an address that is not currently used in the subnet.</span></span> <span data-ttu-id="0f566-271">또는 IP 주소를 동적으로 설정하고 새 프런트 엔드 IP 풀을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-271">Alternatively, you can set the IP address to dynamic and save the new front-end IP pool.</span></span> <span data-ttu-id="0f566-272">이렇게 하면 Azure Portal이 풀에 사용 가능한 IP 주소를 자동으로 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-272">When you do so, the Azure portal automatically assigns an available IP address to the pool.</span></span> <span data-ttu-id="0f566-273">그런 다음 프런트 엔드 IP 풀을 다시 열고 주소 할당을 고정으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-273">You can then reopen the front-end IP pool and change the assignment to static.</span></span> 

6. <span data-ttu-id="0f566-274">수신기의 IP 주소를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-274">Save the IP address for the listener.</span></span> 

7. <span data-ttu-id="0f566-275">다음 설정을 사용하여 상태 검색을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-275">Add a health probe by using the following settings:</span></span>

   |<span data-ttu-id="0f566-276">설정</span><span class="sxs-lookup"><span data-stu-id="0f566-276">Setting</span></span> |<span data-ttu-id="0f566-277">값</span><span class="sxs-lookup"><span data-stu-id="0f566-277">Value</span></span>
   |:-----|:----
   |<span data-ttu-id="0f566-278">**Name**</span><span class="sxs-lookup"><span data-stu-id="0f566-278">**Name**</span></span> |<span data-ttu-id="0f566-279">프로브를 식별하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-279">A name to identify the probe.</span></span>
   |<span data-ttu-id="0f566-280">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="0f566-280">**Protocol**</span></span> |<span data-ttu-id="0f566-281">TCP</span><span class="sxs-lookup"><span data-stu-id="0f566-281">TCP</span></span>
   |<span data-ttu-id="0f566-282">**포트**</span><span class="sxs-lookup"><span data-stu-id="0f566-282">**Port**</span></span> |<span data-ttu-id="0f566-283">사용하지 않는 TCP 포트를 모든 가상 컴퓨터에서 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-283">An unused TCP port, which must be available on all virtual machines.</span></span> <span data-ttu-id="0f566-284">다른 용도로는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-284">It cannot be used for any other purpose.</span></span> <span data-ttu-id="0f566-285">두 수신기가 동일한 프로브 포트를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-285">No two listeners can use the same probe port.</span></span> 
   |<span data-ttu-id="0f566-286">**간격**</span><span class="sxs-lookup"><span data-stu-id="0f566-286">**Interval**</span></span> |<span data-ttu-id="0f566-287">프로브 시도 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-287">The amount of time between probe attempts.</span></span> <span data-ttu-id="0f566-288">기본값(5)을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="0f566-288">Use the default (5).</span></span>
   |<span data-ttu-id="0f566-289">**비정상 임계값**</span><span class="sxs-lookup"><span data-stu-id="0f566-289">**Unhealthy threshold**</span></span> |<span data-ttu-id="0f566-290">이 연속 임계값을 실패하면 가상 컴퓨터를 비정상으로 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-290">The number of consecutive thresholds that should fail before a virtual machine is considered unhealthy.</span></span>

8. <span data-ttu-id="0f566-291">**확인**을 클릭하여 프로브를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-291">Click **OK** to save the probe.</span></span> 

9. <span data-ttu-id="0f566-292">부하 분산 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-292">Create a load balancing rule.</span></span> <span data-ttu-id="0f566-293">**부하 분산 규칙**을 클릭한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-293">Click **Load balancing rules**, and then click **Add**.</span></span>

10. <span data-ttu-id="0f566-294">다음 설정을 사용하여 새 부하 분산 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-294">Configure the new load balancing rule by using the following settings:</span></span>

   |<span data-ttu-id="0f566-295">설정</span><span class="sxs-lookup"><span data-stu-id="0f566-295">Setting</span></span> |<span data-ttu-id="0f566-296">값</span><span class="sxs-lookup"><span data-stu-id="0f566-296">Value</span></span>
   |:-----|:----
   |<span data-ttu-id="0f566-297">**Name**</span><span class="sxs-lookup"><span data-stu-id="0f566-297">**Name**</span></span> |<span data-ttu-id="0f566-298">부하 분산 규칙을 식별하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-298">A name to identify the load balancing rule.</span></span> 
   |<span data-ttu-id="0f566-299">**프런트 엔드 IP 주소**</span><span class="sxs-lookup"><span data-stu-id="0f566-299">**Frontend IP address**</span></span> |<span data-ttu-id="0f566-300">만든 IP 주소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-300">Select the IP address you created.</span></span> 
   |<span data-ttu-id="0f566-301">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="0f566-301">**Protocol**</span></span> |<span data-ttu-id="0f566-302">TCP</span><span class="sxs-lookup"><span data-stu-id="0f566-302">TCP</span></span>
   |<span data-ttu-id="0f566-303">**포트**</span><span class="sxs-lookup"><span data-stu-id="0f566-303">**Port**</span></span> |<span data-ttu-id="0f566-304">SQL Server 인스턴스에서 사용하는 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-304">Use the port that the SQL Server instances are using.</span></span> <span data-ttu-id="0f566-305">변경하지 않을 경우 기본 인스턴스는 포트 1433을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-305">A default instance uses port 1433, unless you changed it.</span></span> 
   |<span data-ttu-id="0f566-306">**백 엔드 포트**</span><span class="sxs-lookup"><span data-stu-id="0f566-306">**Backend port**</span></span> |<span data-ttu-id="0f566-307">**포트**와 동일한 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-307">Use the same value as **Port**.</span></span>
   |<span data-ttu-id="0f566-308">**백 엔드 풀**</span><span class="sxs-lookup"><span data-stu-id="0f566-308">**Backend pool**</span></span> |<span data-ttu-id="0f566-309">SQL Server 인스턴스가 포함된 가상 컴퓨터를 포함하는 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-309">The pool that contains the virtual machines with the SQL Server instances.</span></span> 
   |<span data-ttu-id="0f566-310">**상태 프로브**</span><span class="sxs-lookup"><span data-stu-id="0f566-310">**Health probe**</span></span> |<span data-ttu-id="0f566-311">만든 프로브를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-311">Choose the probe you created.</span></span>
   |<span data-ttu-id="0f566-312">**세션 지속성**</span><span class="sxs-lookup"><span data-stu-id="0f566-312">**Session persistence**</span></span> |<span data-ttu-id="0f566-313">없음</span><span class="sxs-lookup"><span data-stu-id="0f566-313">None</span></span>
   |<span data-ttu-id="0f566-314">**유휴 제한 시간(분)**</span><span class="sxs-lookup"><span data-stu-id="0f566-314">**Idle timeout (minutes)**</span></span> |<span data-ttu-id="0f566-315">기본값(4)</span><span class="sxs-lookup"><span data-stu-id="0f566-315">Default (4)</span></span>
   |<span data-ttu-id="0f566-316">**부동 IP(Direct Server Return)**</span><span class="sxs-lookup"><span data-stu-id="0f566-316">**Floating IP (direct server return)**</span></span> | <span data-ttu-id="0f566-317">사용</span><span class="sxs-lookup"><span data-stu-id="0f566-317">Enabled</span></span>

### <a name="configure-the-availability-group-to-use-the-new-ip-address"></a><span data-ttu-id="0f566-318">새 IP 주소를 사용하도록 가용성 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="0f566-318">Configure the availability group to use the new IP address</span></span>

<span data-ttu-id="0f566-319">클러스터 구성을 완료하려면 첫 번째 가용성 그룹을 만들 때 수행한 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-319">To finish configuring the cluster, repeat the steps that you followed when you made the first availability group.</span></span> <span data-ttu-id="0f566-320">즉, [새 IP 주소를 사용하도록 클러스터를 구성](#configure-the-cluster-to-use-the-load-balancer-ip-address)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-320">That is, configure the [cluster to use the new IP address](#configure-the-cluster-to-use-the-load-balancer-ip-address).</span></span> 

<span data-ttu-id="0f566-321">수신기의 IP 주소를 추가한 후에는 다음을 수행하여 추가 가용성 그룹을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-321">After you have added an IP address for the listener, configure the additional availability group by doing the following:</span></span> 

1. <span data-ttu-id="0f566-322">새 IP 주소의 프로브 포트가 두 SQL Server 가상 컴퓨터에서 모두 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-322">Verify that the probe port for the new IP address is open on both SQL Server virtual machines.</span></span> 

2. <span data-ttu-id="0f566-323">[클러스터 관리자에서 클라이언트 액세스 지점을 추가합니다](#addcap).</span><span class="sxs-lookup"><span data-stu-id="0f566-323">[In Cluster Manager, add the client access point](#addcap).</span></span>

3. <span data-ttu-id="0f566-324">[가용성 그룹에 대한 IP 리소스를 구성합니다](#congroup).</span><span class="sxs-lookup"><span data-stu-id="0f566-324">[Configure the IP resource for the availability group](#congroup).</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="0f566-325">IP 주소를 만들 때 부하 분산 장치에 추가한 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-325">When you create the IP address, use the IP address that you added to the load balancer.</span></span>  

4. <span data-ttu-id="0f566-326">[SQL Server 가용성 그룹 리소스가 클라이언트 액세스 지점에 종속되게 합니다.](#dependencyGroup)</span><span class="sxs-lookup"><span data-stu-id="0f566-326">[Make the SQL Server availability group resource dependent on the client access point](#dependencyGroup).</span></span>

5. <span data-ttu-id="0f566-327">[클라이언트 액세스 지점 리소스가 IP 주소에 종속되게 합니다](#listname).</span><span class="sxs-lookup"><span data-stu-id="0f566-327">[Make the client access point resource dependent on the IP address](#listname).</span></span>
 
6. <span data-ttu-id="0f566-328">[PowerShell에서 클러스터 매개 변수를 설정합니다](#setparam).</span><span class="sxs-lookup"><span data-stu-id="0f566-328">[Set the cluster parameters in PowerShell](#setparam).</span></span>

<span data-ttu-id="0f566-329">새 IP 주소를 사용하도록 가용성 그룹을 구성한 후에는 수신기에 대한 연결을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0f566-329">After you configure the availability group to use the new IP address, configure the connection to the listener.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0f566-330">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f566-330">Next steps</span></span>

- [<span data-ttu-id="0f566-331">다른 지역의 Azure Virtual Machines에서 SQL Server Always On 가용성 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="0f566-331">Configure a SQL Server Always On availability group on Azure virtual machines in different regions</span></span>](virtual-machines-windows-portal-sql-availability-group-dr.md)
