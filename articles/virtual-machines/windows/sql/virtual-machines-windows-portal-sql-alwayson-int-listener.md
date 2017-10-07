---
title: "Azure 가상 컴퓨터에서 SQL Server 가용성 그룹 수신기를 aaaCreate | Microsoft Docs"
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
ms.openlocfilehash: c6a44dc5c7c18b572c2bf5772b4651b7210aacbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-load-balancer-for-an-always-on-availability-group-in-azure"></a><span data-ttu-id="114c4-103">Azure에서 Always On 가용성 그룹에 대한 부하 분산 장치 구성</span><span class="sxs-lookup"><span data-stu-id="114c4-103">Configure a load balancer for an Always On availability group in Azure</span></span>
<span data-ttu-id="114c4-104">이 문서에 설명 방법을 toocreate 부하 분산 장치는 SQL Server Always On 가용성 그룹에에서 대 한 Azure 가상 컴퓨터를 Azure 리소스 관리자와 함께 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-104">This article explains how toocreate a load balancer for a SQL Server Always On availability group in Azure virtual machines that are running with Azure Resource Manager.</span></span> <span data-ttu-id="114c4-105">가용성 그룹 hello SQL Server 인스턴스를 Azure 가상 컴퓨터의 경우 부하 분산 장치가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-105">An availability group requires a load balancer when hello SQL Server instances are on Azure virtual machines.</span></span> <span data-ttu-id="114c4-106">hello 부하 분산 장치는 hello 가용성 그룹 수신기에 대 한 hello IP 주소를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-106">hello load balancer stores hello IP address for hello availability group listener.</span></span> <span data-ttu-id="114c4-107">가용성 그룹이 여러 지역에 분산된 경우 각 지역에 부하 분산 장치가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-107">If an availability group spans multiple regions, each region needs a load balancer.</span></span>

<span data-ttu-id="114c4-108">toocomplete toohave SQL Server 가용성 그룹 리소스 관리자를 사용 하 여 실행 하는 Azure 가상 컴퓨터에 배포 해야이 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-108">toocomplete this task, you need toohave a SQL Server availability group deployed on Azure virtual machines that are running with Resource Manager.</span></span> <span data-ttu-id="114c4-109">SQL Server 가상 컴퓨터 둘 다 toohello 속해야 합니다. 동일한 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-109">Both SQL Server virtual machines must belong toohello same availability set.</span></span> <span data-ttu-id="114c4-110">Hello를 사용할 수 있습니다 [Microsoft 템플릿](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically 리소스 관리자의 hello 가용성 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-110">You can use hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically create hello availability group in Resource Manager.</span></span> <span data-ttu-id="114c4-111">이 템플릿은 내부 부하 분산 장치를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-111">This template automatically creates an internal load balancer for you.</span></span> 

<span data-ttu-id="114c4-112">원하는 경우 [수동으로 가용성 그룹을 구성](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-112">If you prefer, you can [manually configure an availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="114c4-113">이 문서를 진행하려면 가용성 그룹이 이미 구성되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-113">This article requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="114c4-114">관련 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-114">Related topics include:</span></span>

* [<span data-ttu-id="114c4-115">Azure VM의 Always On 가용성 그룹 구성(GUI)</span><span class="sxs-lookup"><span data-stu-id="114c4-115">Configure Always On availability groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="114c4-116">Azure 리소스 관리자 및 PowerShell을 사용하여 VNet-VNet 연결 구성</span><span class="sxs-lookup"><span data-stu-id="114c4-116">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

<span data-ttu-id="114c4-117">이 문서 전체를 검색 하 여 만들고 hello Azure 포털에서에서 부하 분산 장치를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-117">By walking through this article, you create and configure a load balancer in hello Azure portal.</span></span> <span data-ttu-id="114c4-118">Hello 프로세스가 완료 되 면 hello 가용성 그룹 수신기에 대 한 hello 부하 분산 장치에서 hello 클러스터 toouse hello IP 주소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-118">After hello process is complete, you configure hello cluster toouse hello IP address from hello load balancer for hello availability group listener.</span></span>

## <a name="create-and-configure-hello-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="114c4-119">Hello Azure 포털에서에서 만들고 hello 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="114c4-119">Create and configure hello load balancer in hello Azure portal</span></span>
<span data-ttu-id="114c4-120">이 부분의 hello 작업 수행 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="114c4-120">In this portion of hello task, do hello following:</span></span>

1. <span data-ttu-id="114c4-121">Hello Azure 포털에서에서 부하 분산 장치 hello 만들고 hello IP 주소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-121">In hello Azure portal, create hello load balancer and configure hello IP address.</span></span>
2. <span data-ttu-id="114c4-122">Hello 백 엔드 풀을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-122">Configure hello back-end pool.</span></span>
3. <span data-ttu-id="114c4-123">Hello 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-123">Create hello probe.</span></span> 
4. <span data-ttu-id="114c4-124">Hello 부하 분산 규칙을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-124">Set hello load balancing rules.</span></span>

> [!NOTE]
> <span data-ttu-id="114c4-125">여러 리소스 그룹 및 지역 hello SQL Server 인스턴스의 경우 각 단계를 수행을 두 번 한 번만 각 리소스 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-125">If hello SQL Server instances are in multiple resource groups and regions, perform each step twice, once in each resource group.</span></span>
> 
> 

### <a name="step-1-create-hello-load-balancer-and-configure-hello-ip-address"></a><span data-ttu-id="114c4-126">1 단계: hello 부하 분산 장치 만들기 및 hello IP 주소 구성</span><span class="sxs-lookup"><span data-stu-id="114c4-126">Step 1: Create hello load balancer and configure hello IP address</span></span>
<span data-ttu-id="114c4-127">먼저 hello 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-127">First, create hello load balancer.</span></span> 

1. <span data-ttu-id="114c4-128">Hello Azure 포털에서에서 hello SQL Server 가상 컴퓨터를 포함 하는 hello 리소스 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-128">In hello Azure portal, open hello resource group that contains hello SQL Server virtual machines.</span></span> 

2. <span data-ttu-id="114c4-129">Hello 리소스 그룹에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-129">In hello resource group, click **Add**.</span></span>

3. <span data-ttu-id="114c4-130">검색할 **부하 분산 장치** 다음 hello 검색 결과 선택 하 고 **부하 분산 장치**에서 게시는 **Microsoft**합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-130">Search for **load balancer** and then, in hello search results, select **Load Balancer**, which is published by **Microsoft**.</span></span>

4. <span data-ttu-id="114c4-131">Hello에 **부하 분산 장치** 블레이드에서 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-131">On hello **Load Balancer** blade, click **Create**.</span></span>

5. <span data-ttu-id="114c4-132">Hello에 **부하 분산 장치 만들기** 대화 상자에서 다음과 같이 hello 부하 분산 장치를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-132">In hello **Create load balancer** dialog box, configure hello load balancer as follows:</span></span>

   | <span data-ttu-id="114c4-133">설정</span><span class="sxs-lookup"><span data-stu-id="114c4-133">Setting</span></span> | <span data-ttu-id="114c4-134">값</span><span class="sxs-lookup"><span data-stu-id="114c4-134">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="114c4-135">**Name**</span><span class="sxs-lookup"><span data-stu-id="114c4-135">**Name**</span></span> |<span data-ttu-id="114c4-136">Hello 부하 분산 장치를 나타내는 텍스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-136">A text name representing hello load balancer.</span></span> <span data-ttu-id="114c4-137">예를 들어 **sqlLB**입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-137">For example, **sqlLB**.</span></span> |
   | <span data-ttu-id="114c4-138">**형식**</span><span class="sxs-lookup"><span data-stu-id="114c4-138">**Type**</span></span> |<span data-ttu-id="114c4-139">**내부**: 대부분의 구현 hello 내에서 응용 프로그램에서 내부 부하 분산 장치를 사용 하 여 동일한 가상 네트워크 tooconnect toohello 가용성 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-139">**Internal**: Most implementations use an internal load balancer, which allows applications within hello same virtual network tooconnect toohello availability group.</span></span>  </br> <span data-ttu-id="114c4-140">**외부**: 공용 인터넷 연결을 통해 응용 프로그램 tooconnect toohello 가용성 그룹을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-140">**External**: Allows applications tooconnect toohello availability group through a public Internet connection.</span></span> |
   | <span data-ttu-id="114c4-141">**가상 네트워크**</span><span class="sxs-lookup"><span data-stu-id="114c4-141">**Virtual network**</span></span> |<span data-ttu-id="114c4-142">Hello에 hello SQL Server 인스턴스로만 구성 되어 있는 가상 네트워크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-142">Select hello virtual network that hello SQL Server intances are in.</span></span> |
   | <span data-ttu-id="114c4-143">**서브넷**</span><span class="sxs-lookup"><span data-stu-id="114c4-143">**Subnet**</span></span> |<span data-ttu-id="114c4-144">SQL Server 인스턴스가 hello hello 서브넷을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-144">Select hello subnet that hello SQL Server instances are in.</span></span> |
   | <span data-ttu-id="114c4-145">**IP 주소 할당**</span><span class="sxs-lookup"><span data-stu-id="114c4-145">**IP address assignment**</span></span> |<span data-ttu-id="114c4-146">**정적**</span><span class="sxs-lookup"><span data-stu-id="114c4-146">**Static**</span></span> |
   | <span data-ttu-id="114c4-147">**개인 IP 주소**</span><span class="sxs-lookup"><span data-stu-id="114c4-147">**Private IP address**</span></span> |<span data-ttu-id="114c4-148">Hello 서브넷에서 사용 가능한 IP 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-148">Specify an available IP address from hello subnet.</span></span> <span data-ttu-id="114c4-149">Hello 클러스터에서 수신기를 만들 때이 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-149">Use this IP address when you create a listener on hello cluster.</span></span> <span data-ttu-id="114c4-150">이 문서의 뒷부분에 나오는 PowerShell 스크립트에서 사용 하 여이 주소 hello에 대 한 `$ILBIP` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-150">In a PowerShell script, later in this article, use this address for hello `$ILBIP` variable.</span></span> |
   | <span data-ttu-id="114c4-151">**구독**</span><span class="sxs-lookup"><span data-stu-id="114c4-151">**Subscription**</span></span> |<span data-ttu-id="114c4-152">구독이 여러 개인 경우 이 필드가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-152">If you have multiple subscriptions, this field might appear.</span></span> <span data-ttu-id="114c4-153">이 리소스와 tooassociate hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-153">Select hello subscription that you want tooassociate with this resource.</span></span> <span data-ttu-id="114c4-154">일반적으로 동일한 구독 hello 가용성 그룹에 대 한 모든 hello 리소스 hello는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-154">It is normally hello same subscription as all hello resources for hello availability group.</span></span> |
   | <span data-ttu-id="114c4-155">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="114c4-155">**Resource group**</span></span> |<span data-ttu-id="114c4-156">SQL Server 인스턴스가 hello hello 리소스 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-156">Select hello resource group that hello SQL Server instances are in.</span></span> |
   | <span data-ttu-id="114c4-157">**위치**:</span><span class="sxs-lookup"><span data-stu-id="114c4-157">**Location**</span></span> |<span data-ttu-id="114c4-158">Hello hello SQL Server 인스턴스는 Azure 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-158">Select hello Azure location that hello SQL Server instances are in.</span></span> |

6. <span data-ttu-id="114c4-159">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-159">Click **Create**.</span></span> 

<span data-ttu-id="114c4-160">Azure는 hello 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-160">Azure creates hello load balancer.</span></span> <span data-ttu-id="114c4-161">부하 분산 장치 hello tooa 특정 네트워크, 서브넷, 리소스 그룹 및 위치에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-161">hello load balancer belongs tooa specific network, subnet, resource group, and location.</span></span> <span data-ttu-id="114c4-162">Azure hello 작업을 완료 한 후에 Azure의 hello 부하 분산 장치 설정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-162">After Azure completes hello task, verify hello load balancer settings in Azure.</span></span> 

### <a name="step-2-configure-hello-back-end-pool"></a><span data-ttu-id="114c4-163">2 단계: hello 백 엔드 풀 구성</span><span class="sxs-lookup"><span data-stu-id="114c4-163">Step 2: Configure hello back-end pool</span></span>
<span data-ttu-id="114c4-164">Azure 호출 hello 백 엔드 주소 풀 *백 엔드 풀*합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-164">Azure calls hello back-end address pool *backend pool*.</span></span> <span data-ttu-id="114c4-165">이 경우 hello 백 엔드 풀은 가용성 그룹의 hello 두 SQL Server 인스턴스의 hello 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-165">In this case, hello back-end pool is hello addresses of hello two SQL Server instances in your availability group.</span></span> 

1. <span data-ttu-id="114c4-166">리소스 그룹을 만든 hello 부하 분산 장치를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-166">In your resource group, click hello load balancer that you created.</span></span> 

2. <span data-ttu-id="114c4-167">**설정**에서 **백 엔드 풀**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-167">On **Settings**, click **Backend pools**.</span></span>

3. <span data-ttu-id="114c4-168">**백 엔드 풀**, 클릭 **추가** toocreate 백 엔드 주소 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-168">On **Backend pools**, click **Add** toocreate a back-end address pool.</span></span> 

4. <span data-ttu-id="114c4-169">**백 엔드 풀 추가**아래 **이름**를 hello 백 엔드 풀의 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-169">On **Add backend pool**, under **Name**, type a name for hello back-end pool.</span></span>

5. <span data-ttu-id="114c4-170">**가상 컴퓨터**에서 **가상 컴퓨터 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-170">Under **Virtual machines**, click **Add a virtual machine**.</span></span> 

6. <span data-ttu-id="114c4-171">아래 **가상 컴퓨터를 선택할**, 클릭 **가용성 집합 선택**, hello 가용성 집합 hello SQL Server 가상 컴퓨터에 속해 있는지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-171">Under **Choose virtual machines**, click **Choose an availability set**, and then specify hello availability set that hello SQL Server virtual machines belong to.</span></span>

7. <span data-ttu-id="114c4-172">Hello 가용성 집합을 선택한 후 클릭 **hello 가상 컴퓨터를 선택할**, 선택 hello hello 가용성 그룹의 hello SQL Server 인스턴스를 호스트 하 고 클릭 두 개의 가상 컴퓨터가 **선택**.</span><span class="sxs-lookup"><span data-stu-id="114c4-172">After you have chosen hello availability set, click **Choose hello virtual machines**, select hello two virtual machines that host hello SQL Server instances in hello availability group, and then click **Select**.</span></span> 

8. <span data-ttu-id="114c4-173">클릭 **확인** 용 tooclose hello 블레이드에 **가상 컴퓨터를 선택할**, 및 **백 엔드 풀 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-173">Click **OK** tooclose hello blades for **Choose virtual machines**, and **Add backend pool**.</span></span> 

<span data-ttu-id="114c4-174">Azure는 hello 백 엔드 주소 풀에 대 한 hello 설정을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-174">Azure updates hello settings for hello back-end address pool.</span></span> <span data-ttu-id="114c4-175">이제 가용성 집합에는 두 개의 SQL Server 인스턴스에 대한 풀이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-175">Now your availability set has a pool of two SQL Server instances.</span></span>

### <a name="step-3-create-a-probe"></a><span data-ttu-id="114c4-176">3단계: 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="114c4-176">Step 3: Create a probe</span></span>
<span data-ttu-id="114c4-177">hello 프로브 현재 소유 하 고 hello SQL Server 인스턴스는 가용성 그룹 수신기 hello Azure을 확인 하는 방법을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-177">hello probe defines how Azure verifies which of hello SQL Server instances currently owns hello availability group listener.</span></span> <span data-ttu-id="114c4-178">Azure는 hello 프로브를 만들 때 정의 하는 포트에 hello IP 주소를 기반으로 하는 hello 서비스를 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-178">Azure probes hello service based on hello IP address on a port that you define when you create hello probe.</span></span>

1. <span data-ttu-id="114c4-179">Hello에 부하 분산 장치 **설정** 블레이드에서 클릭 **상태 프로브**합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-179">On hello load balancer **Settings** blade, click **Health probes**.</span></span> 

2. <span data-ttu-id="114c4-180">Hello에 **상태 프로브** 블레이드에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-180">On hello **Health probes** blade, click **Add**.</span></span>

3. <span data-ttu-id="114c4-181">Hello에 hello 프로브를 구성 **추가 프로브** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-181">Configure hello probe on hello **Add probe** blade.</span></span> <span data-ttu-id="114c4-182">다음 사용 하 여 hello tooconfigure hello 프로브 값:</span><span class="sxs-lookup"><span data-stu-id="114c4-182">Use hello following values tooconfigure hello probe:</span></span>

   | <span data-ttu-id="114c4-183">설정</span><span class="sxs-lookup"><span data-stu-id="114c4-183">Setting</span></span> | <span data-ttu-id="114c4-184">값</span><span class="sxs-lookup"><span data-stu-id="114c4-184">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="114c4-185">**Name**</span><span class="sxs-lookup"><span data-stu-id="114c4-185">**Name**</span></span> |<span data-ttu-id="114c4-186">Hello 프로브를 나타내는 텍스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-186">A text name representing hello probe.</span></span> <span data-ttu-id="114c4-187">예를 들어 **SQLAlwaysOnEndPointProbe**입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-187">For example, **SQLAlwaysOnEndPointProbe**.</span></span> |
   | <span data-ttu-id="114c4-188">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="114c4-188">**Protocol**</span></span> |<span data-ttu-id="114c4-189">**TCP**</span><span class="sxs-lookup"><span data-stu-id="114c4-189">**TCP**</span></span> |
   | <span data-ttu-id="114c4-190">**포트**</span><span class="sxs-lookup"><span data-stu-id="114c4-190">**Port**</span></span> |<span data-ttu-id="114c4-191">사용 가능한 모든 포트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-191">You can use any available port.</span></span> <span data-ttu-id="114c4-192">예를 들어 *59999*입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-192">For example, *59999*.</span></span> |
   | <span data-ttu-id="114c4-193">**간격**</span><span class="sxs-lookup"><span data-stu-id="114c4-193">**Interval**</span></span> |<span data-ttu-id="114c4-194">*5*</span><span class="sxs-lookup"><span data-stu-id="114c4-194">*5*</span></span> |
   | <span data-ttu-id="114c4-195">**비정상 임계값**</span><span class="sxs-lookup"><span data-stu-id="114c4-195">**Unhealthy threshold**</span></span> |<span data-ttu-id="114c4-196">*2*</span><span class="sxs-lookup"><span data-stu-id="114c4-196">*2*</span></span> |

4.  <span data-ttu-id="114c4-197">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-197">Click **OK**.</span></span> 

> [!NOTE]
> <span data-ttu-id="114c4-198">지정한 hello 포트가 두 SQL Server 인스턴스의 hello 방화벽에서 열려 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-198">Make sure that hello port you specify is open on hello firewall of both SQL Server instances.</span></span> <span data-ttu-id="114c4-199">두 인스턴스의 hello 있습니다를 사용 하는 TCP 포트에 대 한 인바운드 규칙을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-199">Both instances require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="114c4-200">자세한 내용은 [방화벽 규칙 추가 또는 편집](http://technet.microsoft.com/library/cc753558.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="114c4-200">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span> 
> 
> 

<span data-ttu-id="114c4-201">Azure는 hello 프로브 만들고 tootest는 SQL Server 인스턴스에 hello hello 가용성 그룹 수신기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-201">Azure creates hello probe and then uses it tootest which SQL Server instance has hello listener for hello availability group.</span></span>

### <a name="step-4-set-hello-load-balancing-rules"></a><span data-ttu-id="114c4-202">4 단계: hello 부하 분산 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="114c4-202">Step 4: Set hello load balancing rules</span></span>
<span data-ttu-id="114c4-203">hello 부하 분산 규칙 hello 부하 분산 장치에서 트래픽을 toohello SQL Server 인스턴스를 라우팅하 하는 방법 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-203">hello load balancing rules configure how hello load balancer routes traffic toohello SQL Server instances.</span></span> <span data-ttu-id="114c4-204">이 부하 분산 장치에 대 한 hello 두 SQL Server 인스턴스 중 하나에만 hello 가용성 그룹 수신기 리소스를 소유 하 고 한 번에 직접 서버 반환 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-204">For this load balancer, you enable direct server return because only one of hello two SQL Server instances owns hello availability group listener resource at a time.</span></span>

1. <span data-ttu-id="114c4-205">Hello에 부하 분산 장치 **설정** 블레이드에서 클릭 **부하 분산 규칙**합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-205">On hello load balancer **Settings** blade, click **Load balancing rules**.</span></span> 

2. <span data-ttu-id="114c4-206">Hello에 **부하 분산 규칙** 블레이드에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-206">On hello **Load balancing rules** blade, click **Add**.</span></span>

3. <span data-ttu-id="114c4-207">Hello에 **추가 부하 분산 규칙** 블레이드에서 hello 부하 분산 규칙을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-207">On hello **Add load balancing rules** blade, configure hello load balancing rule.</span></span> <span data-ttu-id="114c4-208">다음 설정을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="114c4-208">Use hello following settings:</span></span> 

   | <span data-ttu-id="114c4-209">설정</span><span class="sxs-lookup"><span data-stu-id="114c4-209">Setting</span></span> | <span data-ttu-id="114c4-210">값</span><span class="sxs-lookup"><span data-stu-id="114c4-210">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="114c4-211">**Name**</span><span class="sxs-lookup"><span data-stu-id="114c4-211">**Name**</span></span> |<span data-ttu-id="114c4-212">Hello 부하 분산 규칙을 나타내는 텍스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-212">A text name representing hello load balancing rules.</span></span> <span data-ttu-id="114c4-213">예를 들어 **SQLAlwaysOnEndPointListener**입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-213">For example, **SQLAlwaysOnEndPointListener**.</span></span> |
   | <span data-ttu-id="114c4-214">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="114c4-214">**Protocol**</span></span> |<span data-ttu-id="114c4-215">**TCP**</span><span class="sxs-lookup"><span data-stu-id="114c4-215">**TCP**</span></span> |
   | <span data-ttu-id="114c4-216">**포트**</span><span class="sxs-lookup"><span data-stu-id="114c4-216">**Port**</span></span> |<span data-ttu-id="114c4-217">*1433*</span><span class="sxs-lookup"><span data-stu-id="114c4-217">*1433*</span></span> |
   | <span data-ttu-id="114c4-218">**백 엔드 포트**</span><span class="sxs-lookup"><span data-stu-id="114c4-218">**Backend Port**</span></span> |<span data-ttu-id="114c4-219">*1433*. 이 규칙은 **부동 IP(Direct Server Return)**를 사용하므로 이 값은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-219">*1433*. This value is ignored because this rule uses **Floating IP (direct server return)**.</span></span> |
   | <span data-ttu-id="114c4-220">**프로브**</span><span class="sxs-lookup"><span data-stu-id="114c4-220">**Probe**</span></span> |<span data-ttu-id="114c4-221">이 부하 분산 장치에 대해 만든 hello 검색의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-221">Use hello name of hello probe that you created for this load balancer.</span></span> |
   | <span data-ttu-id="114c4-222">**세션 지속성**</span><span class="sxs-lookup"><span data-stu-id="114c4-222">**Session persistence**</span></span> |<span data-ttu-id="114c4-223">**없음**</span><span class="sxs-lookup"><span data-stu-id="114c4-223">**None**</span></span> |
   | <span data-ttu-id="114c4-224">**유휴 제한 시간(분)**</span><span class="sxs-lookup"><span data-stu-id="114c4-224">**Idle timeout (minutes)**</span></span> |<span data-ttu-id="114c4-225">*4*</span><span class="sxs-lookup"><span data-stu-id="114c4-225">*4*</span></span> |
   | <span data-ttu-id="114c4-226">**부동 IP(Direct Server Return)**</span><span class="sxs-lookup"><span data-stu-id="114c4-226">**Floating IP (direct server return)**</span></span> |<span data-ttu-id="114c4-227">**사용**</span><span class="sxs-lookup"><span data-stu-id="114c4-227">**Enabled**</span></span> |

   > [!NOTE]
   > <span data-ttu-id="114c4-228">Hello 블레이드 tooview 아래로 tooscroll hello 설정을 모두 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-228">You might have tooscroll down hello blade tooview all hello settings.</span></span>
   > 

4. <span data-ttu-id="114c4-229">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-229">Click **OK**.</span></span> 
5. <span data-ttu-id="114c4-230">Azure는 hello 부하 분산 규칙을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-230">Azure configures hello load balancing rule.</span></span> <span data-ttu-id="114c4-231">이제 hello 부하 분산 장치는 hello hello 가용성 그룹 수신기를 호스팅하는 구성 된 tooroute 트래픽 toohello SQL Server 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-231">Now hello load balancer is configured tooroute traffic toohello SQL Server instance that hosts hello listener for hello availability group.</span></span> 

<span data-ttu-id="114c4-232">이 시점에서 hello 리소스 그룹 tooboth SQL Server 컴퓨터를 연결 하는 부하 분산 장치를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-232">At this point, hello resource group has a load balancer that connects tooboth SQL Server machines.</span></span> <span data-ttu-id="114c4-233">또한 hello 부하 분산 장치 컴퓨터와 hello 가용성 그룹에 대 한 toorequests 응답할 수 있도록 hello SQL Server Always On 가용성 그룹 수신기에 대 한 IP 주소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-233">hello load balancer also contains an IP address for hello SQL Server Always On availability group listener, so that either machine can respond toorequests for hello availability groups.</span></span>

> [!NOTE]
> <span data-ttu-id="114c4-234">SQL Server 인스턴스가 별도 두 지역에 있는 경우 hello의 hello 단계 다른 지역을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-234">If your SQL Server instances are in two separate regions, repeat hello steps in hello other region.</span></span> <span data-ttu-id="114c4-235">각 지역마다 하나의 부하 분산 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-235">Each region requires a load balancer.</span></span> 
> 
> 

## <a name="configure-hello-cluster-toouse-hello-load-balancer-ip-address"></a><span data-ttu-id="114c4-236">Hello 클러스터 toouse hello 부하 분산 장치 IP 주소 구성</span><span class="sxs-lookup"><span data-stu-id="114c4-236">Configure hello cluster toouse hello load balancer IP address</span></span>
<span data-ttu-id="114c4-237">hello 다음 단계는 hello 클러스터에서 tooconfigure hello 수신기 고 hello 수신기를 온라인 상태로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-237">hello next step is tooconfigure hello listener on hello cluster, and bring hello listener online.</span></span> <span data-ttu-id="114c4-238">다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-238">Do hello following:</span></span> 

1. <span data-ttu-id="114c4-239">Hello 장애 조치 클러스터에 hello 가용성 그룹 수신기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-239">Create hello availability group listener on hello failover cluster.</span></span> 

2. <span data-ttu-id="114c4-240">Hello 수신기를 온라인 상태로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-240">Bring hello listener online.</span></span>

### <a name="step-5-create-hello-availability-group-listener-on-hello-failover-cluster"></a><span data-ttu-id="114c4-241">5 단계: hello 장애 조치 클러스터에 hello 가용성 그룹 수신기 만들기</span><span class="sxs-lookup"><span data-stu-id="114c4-241">Step 5: Create hello availability group listener on hello failover cluster</span></span>
<span data-ttu-id="114c4-242">이 단계에서는 수동으로 장애 조치 클러스터 관리자 및 SQL Server Management Studio에서 hello 가용성 그룹 수신기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-242">In this step, you manually create hello availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

### <a name="verify-hello-configuration-of-hello-listener"></a><span data-ttu-id="114c4-243">Hello 수신기의 hello 구성 확인</span><span class="sxs-lookup"><span data-stu-id="114c4-243">Verify hello configuration of hello listener</span></span>

<span data-ttu-id="114c4-244">Hello 클러스터 리소스 및 종속성 제대로 구성 되어 SQL Server Management Studio에서 수 tooview hello 수신기 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-244">If hello cluster resources and dependencies are correctly configured, you should be able tooview hello listener in SQL Server Management Studio.</span></span> <span data-ttu-id="114c4-245">tooset 수신기 포트 hello, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-245">tooset hello listener port, do hello following:</span></span>

1. <span data-ttu-id="114c4-246">SQL Server Management Studio를 시작 하 고 toohello 주 복제본을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-246">Start SQL Server Management Studio, and then connect toohello primary replica.</span></span>

2. <span data-ttu-id="114c4-247">너무 이동**AlwaysOn 고가용성** > **가용성 그룹** > **가용성 그룹 수신기**합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-247">Go too**AlwaysOn High Availability** > **Availability Groups** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="114c4-248">이제 장애 조치 클러스터 관리자에서 만든 hello 수신기 이름이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-248">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> 

3. <span data-ttu-id="114c4-249">Hello 수신기 이름을 마우스 오른쪽 단추로 클릭 한 다음 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-249">Right-click hello listener name, and then click **Properties**.</span></span>

4. <span data-ttu-id="114c4-250">Hello에 **포트** 상자 이전 사용 $EndpointPort hello를 사용 하 여 hello 가용성 그룹 수신기에 대 한 hello 포트 번호를 지정 합니다 (1433 hello이 기본값 이었습니다)를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-250">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort you used earlier (1433 was hello default), and then click **OK**.</span></span>

<span data-ttu-id="114c4-251">이제 Resource Manager 모드에서 실행 중인 Azure 가상 컴퓨터에 가용성 그룹이 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-251">You now have an availability group in Azure virtual machines running in Resource Manager mode.</span></span> 

## <a name="test-hello-connection-toohello-listener"></a><span data-ttu-id="114c4-252">테스트 hello 연결 toohello 수신기</span><span class="sxs-lookup"><span data-stu-id="114c4-252">Test hello connection toohello listener</span></span>
<span data-ttu-id="114c4-253">Hello 다음을 수행 하 여 hello 연결을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-253">Test hello connection by doing hello following:</span></span>

1. <span data-ttu-id="114c4-254">RDP tooa SQL Server 인스턴스 hello에 있는 동일한 가상 네트워크 구성 요소, 않도록 지정 되었으나 자체 hello 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-254">RDP tooa SQL Server instance that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="114c4-255">이 서버는 hello 클러스터에서 다른 SQL Server 인스턴스에 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-255">This server can be hello other SQL Server instance in hello cluster.</span></span>

2. <span data-ttu-id="114c4-256">사용 하 여 **sqlcmd** 유틸리티 tootest hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-256">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="114c4-257">예를 들어 다음 스크립트는 hello 설정는 **sqlcmd** hello 수신기 Windows 인증을 통해 연결 toohello 주 복제본:</span><span class="sxs-lookup"><span data-stu-id="114c4-257">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>
   
        sqlcmd -S <listenerName> -E

<span data-ttu-id="114c4-258">hello SQLCMD 연결 hello 주 복제본을 호스팅하는 toohello SQL Server 인스턴스를 자동으로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-258">hello SQLCMD connection automatically connects toohello SQL Server instance that hosts hello primary replica.</span></span> 

## <a name="create-an-ip-address-for-an-additional-availability-group"></a><span data-ttu-id="114c4-259">추가 가용성 그룹의 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="114c4-259">Create an IP address for an additional availability group</span></span>

<span data-ttu-id="114c4-260">각 가용성 그룹은 별도의 수신기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-260">Each availability group uses a separate listener.</span></span> <span data-ttu-id="114c4-261">각 수신기는 자체 IP 주소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-261">Each listener has its own IP address.</span></span> <span data-ttu-id="114c4-262">사용 하 여 hello 동일 추가 수신기에 대 한 분산 toohold hello IP 주소를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-262">Use hello same load balancer toohold hello IP address for additional listeners.</span></span> <span data-ttu-id="114c4-263">가용성 그룹을 만든 후에 hello IP 주소 toohello 부하 분산 장치를 추가 하 고 hello 수신기를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-263">After you create an availability group, add hello IP address toohello load balancer, and then configure hello listener.</span></span>

<span data-ttu-id="114c4-264">hello Azure 포털에 대 한 IP 주소 tooa 부하 분산 tooadd 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-264">tooadd an IP address tooa load balancer with hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="114c4-265">Hello Azure 포털에서에서 hello 부하 분산 장치를 포함 하는 hello 리소스 그룹을 열고 hello 부하 분산 장치를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-265">In hello Azure portal, open hello resource group that contains hello load balancer, and then click hello load balancer.</span></span> 

2. <span data-ttu-id="114c4-266">**설정**에서 **프런트 엔드 IP 풀**을 클릭한 후 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-266">Under **SETTINGS**, click **Frontend IP pool**, and then click **Add**.</span></span> 

3. <span data-ttu-id="114c4-267">아래 **프런트 엔드 IP 주소 추가**, hello 프런트 엔드에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-267">Under **Add frontend IP address**, assign a name for hello front end.</span></span> 

4. <span data-ttu-id="114c4-268">해당 hello 확인 **가상 네트워크** 및 hello **서브넷** SQL Server 인스턴스 hello와 동일 하 게 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-268">Verify that hello **Virtual network** and hello **Subnet** are hello same as hello SQL Server instances.</span></span>

5. <span data-ttu-id="114c4-269">Hello 수신기에 대 한 hello IP 주소를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-269">Set hello IP address for hello listener.</span></span> 
   
   >[!TIP]
   ><span data-ttu-id="114c4-270">Hello IP 주소 toostatic 설정 하 고 hello 서브넷에 현재 사용 되지 않는 주소를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-270">You can set hello IP address toostatic and type an address that is not currently used in hello subnet.</span></span> <span data-ttu-id="114c4-271">또는 hello IP 주소 toodynamic 설정 하 고 hello 새 프런트 엔드 IP 풀을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-271">Alternatively, you can set hello IP address toodynamic and save hello new front-end IP pool.</span></span> <span data-ttu-id="114c4-272">이렇게 하면 hello Azure 포털 사용 가능한 IP 주소 toohello 풀을 자동으로 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-272">When you do so, hello Azure portal automatically assigns an available IP address toohello pool.</span></span> <span data-ttu-id="114c4-273">그런 다음 hello 프런트 엔드 IP 풀을 다시 열고 하 고 hello 할당 toostatic 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-273">You can then reopen hello front-end IP pool and change hello assignment toostatic.</span></span> 

6. <span data-ttu-id="114c4-274">Hello 수신기에 대 한 hello IP 주소를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-274">Save hello IP address for hello listener.</span></span> 

7. <span data-ttu-id="114c4-275">다음 설정을 hello를 사용 하 여 상태 검색을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-275">Add a health probe by using hello following settings:</span></span>

   |<span data-ttu-id="114c4-276">설정</span><span class="sxs-lookup"><span data-stu-id="114c4-276">Setting</span></span> |<span data-ttu-id="114c4-277">값</span><span class="sxs-lookup"><span data-stu-id="114c4-277">Value</span></span>
   |:-----|:----
   |<span data-ttu-id="114c4-278">**Name**</span><span class="sxs-lookup"><span data-stu-id="114c4-278">**Name**</span></span> |<span data-ttu-id="114c4-279">이름 tooidentify hello 프로브 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-279">A name tooidentify hello probe.</span></span>
   |<span data-ttu-id="114c4-280">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="114c4-280">**Protocol**</span></span> |<span data-ttu-id="114c4-281">TCP</span><span class="sxs-lookup"><span data-stu-id="114c4-281">TCP</span></span>
   |<span data-ttu-id="114c4-282">**포트**</span><span class="sxs-lookup"><span data-stu-id="114c4-282">**Port**</span></span> |<span data-ttu-id="114c4-283">사용하지 않는 TCP 포트를 모든 가상 컴퓨터에서 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-283">An unused TCP port, which must be available on all virtual machines.</span></span> <span data-ttu-id="114c4-284">다른 용도로는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-284">It cannot be used for any other purpose.</span></span> <span data-ttu-id="114c4-285">두 수신기 hello צ ְ ײ 프로브 포트로 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-285">No two listeners can use hello same probe port.</span></span> 
   |<span data-ttu-id="114c4-286">**간격**</span><span class="sxs-lookup"><span data-stu-id="114c4-286">**Interval**</span></span> |<span data-ttu-id="114c4-287">프로브 사이의 시간 크기 hello 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-287">hello amount of time between probe attempts.</span></span> <span data-ttu-id="114c4-288">Hello 기본 (5)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-288">Use hello default (5).</span></span>
   |<span data-ttu-id="114c4-289">**비정상 임계값**</span><span class="sxs-lookup"><span data-stu-id="114c4-289">**Unhealthy threshold**</span></span> |<span data-ttu-id="114c4-290">여러 가상 컴퓨터를 하기 전에 중지 해야 함을 연속 임계값 hello 비정상으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-290">hello number of consecutive thresholds that should fail before a virtual machine is considered unhealthy.</span></span>

8. <span data-ttu-id="114c4-291">클릭 **확인** toosave hello 프로브 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-291">Click **OK** toosave hello probe.</span></span> 

9. <span data-ttu-id="114c4-292">부하 분산 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-292">Create a load balancing rule.</span></span> <span data-ttu-id="114c4-293">**부하 분산 규칙**을 클릭한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-293">Click **Load balancing rules**, and then click **Add**.</span></span>

10. <span data-ttu-id="114c4-294">Hello 새 부하 분산 규칙 hello 다음 설정을 사용 하 여 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-294">Configure hello new load balancing rule by using hello following settings:</span></span>

   |<span data-ttu-id="114c4-295">설정</span><span class="sxs-lookup"><span data-stu-id="114c4-295">Setting</span></span> |<span data-ttu-id="114c4-296">값</span><span class="sxs-lookup"><span data-stu-id="114c4-296">Value</span></span>
   |:-----|:----
   |<span data-ttu-id="114c4-297">**Name**</span><span class="sxs-lookup"><span data-stu-id="114c4-297">**Name**</span></span> |<span data-ttu-id="114c4-298">이름 tooidentify hello 부하 분산 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-298">A name tooidentify hello load balancing rule.</span></span> 
   |<span data-ttu-id="114c4-299">**프런트 엔드 IP 주소**</span><span class="sxs-lookup"><span data-stu-id="114c4-299">**Frontend IP address**</span></span> |<span data-ttu-id="114c4-300">만든 hello IP 주소를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-300">Select hello IP address you created.</span></span> 
   |<span data-ttu-id="114c4-301">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="114c4-301">**Protocol**</span></span> |<span data-ttu-id="114c4-302">TCP</span><span class="sxs-lookup"><span data-stu-id="114c4-302">TCP</span></span>
   |<span data-ttu-id="114c4-303">**포트**</span><span class="sxs-lookup"><span data-stu-id="114c4-303">**Port**</span></span> |<span data-ttu-id="114c4-304">Hello SQL Server 인스턴스를 사용 하는 hello 포트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-304">Use hello port that hello SQL Server instances are using.</span></span> <span data-ttu-id="114c4-305">변경하지 않을 경우 기본 인스턴스는 포트 1433을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-305">A default instance uses port 1433, unless you changed it.</span></span> 
   |<span data-ttu-id="114c4-306">**백 엔드 포트**</span><span class="sxs-lookup"><span data-stu-id="114c4-306">**Backend port**</span></span> |<span data-ttu-id="114c4-307">같은 값으로 사용 하 여 hello **포트**합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-307">Use hello same value as **Port**.</span></span>
   |<span data-ttu-id="114c4-308">**백 엔드 풀**</span><span class="sxs-lookup"><span data-stu-id="114c4-308">**Backend pool**</span></span> |<span data-ttu-id="114c4-309">SQL Server 인스턴스에서 hello hello 가상 컴퓨터를 포함 하는 hello 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-309">hello pool that contains hello virtual machines with hello SQL Server instances.</span></span> 
   |<span data-ttu-id="114c4-310">**상태 프로브**</span><span class="sxs-lookup"><span data-stu-id="114c4-310">**Health probe**</span></span> |<span data-ttu-id="114c4-311">만든 hello 프로브를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-311">Choose hello probe you created.</span></span>
   |<span data-ttu-id="114c4-312">**세션 지속성**</span><span class="sxs-lookup"><span data-stu-id="114c4-312">**Session persistence**</span></span> |<span data-ttu-id="114c4-313">없음</span><span class="sxs-lookup"><span data-stu-id="114c4-313">None</span></span>
   |<span data-ttu-id="114c4-314">**유휴 제한 시간(분)**</span><span class="sxs-lookup"><span data-stu-id="114c4-314">**Idle timeout (minutes)**</span></span> |<span data-ttu-id="114c4-315">기본값(4)</span><span class="sxs-lookup"><span data-stu-id="114c4-315">Default (4)</span></span>
   |<span data-ttu-id="114c4-316">**부동 IP(Direct Server Return)**</span><span class="sxs-lookup"><span data-stu-id="114c4-316">**Floating IP (direct server return)**</span></span> | <span data-ttu-id="114c4-317">사용</span><span class="sxs-lookup"><span data-stu-id="114c4-317">Enabled</span></span>

### <a name="configure-hello-availability-group-toouse-hello-new-ip-address"></a><span data-ttu-id="114c4-318">Hello 가용성 그룹 toouse hello 새 IP 주소 구성</span><span class="sxs-lookup"><span data-stu-id="114c4-318">Configure hello availability group toouse hello new IP address</span></span>

<span data-ttu-id="114c4-319">toofinish hello 첫 번째 가용성 그룹을 만든 때 수행한 단계를 반복 hello hello 클러스터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-319">toofinish configuring hello cluster, repeat hello steps that you followed when you made hello first availability group.</span></span> <span data-ttu-id="114c4-320">즉, hello 구성 [toouse hello 새 IP 주소를 클러스터](#configure-the-cluster-to-use-the-load-balancer-ip-address)합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-320">That is, configure hello [cluster toouse hello new IP address](#configure-the-cluster-to-use-the-load-balancer-ip-address).</span></span> 

<span data-ttu-id="114c4-321">Hello 수신기에 대 한 IP 주소를 추가 하면 hello 다음을 수행 하 여 hello 추가 가용성 그룹을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-321">After you have added an IP address for hello listener, configure hello additional availability group by doing hello following:</span></span> 

1. <span data-ttu-id="114c4-322">Hello 새 IP 주소에 대 한 hello 프로브 포트를 두 SQL Server 가상 컴퓨터에서 열려 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-322">Verify that hello probe port for hello new IP address is open on both SQL Server virtual machines.</span></span> 

2. <span data-ttu-id="114c4-323">[클러스터 관리자에서 hello 클라이언트 액세스 지점 추가](#addcap)합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-323">[In Cluster Manager, add hello client access point](#addcap).</span></span>

3. <span data-ttu-id="114c4-324">[Hello 가용성 그룹에 대 한 hello IP 리소스 구성](#congroup)합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-324">[Configure hello IP resource for hello availability group](#congroup).</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="114c4-325">Hello IP 주소를 만들 때 toohello 부하 분산 장치를 추가한 hello IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-325">When you create hello IP address, use hello IP address that you added toohello load balancer.</span></span>  

4. <span data-ttu-id="114c4-326">[SQL Server 가용성 그룹 리소스가 hello hello 클라이언트 액세스 지점에 종속 되 게](#dependencyGroup)합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-326">[Make hello SQL Server availability group resource dependent on hello client access point](#dependencyGroup).</span></span>

5. <span data-ttu-id="114c4-327">[Hello 클라이언트 액세스 지점 hello IP 주소에 종속 리소스](#listname)합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-327">[Make hello client access point resource dependent on hello IP address](#listname).</span></span>
 
6. <span data-ttu-id="114c4-328">[PowerShell에서 hello 클러스터 매개 변수를 설정](#setparam)합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-328">[Set hello cluster parameters in PowerShell](#setparam).</span></span>

<span data-ttu-id="114c4-329">Hello 가용성 그룹 toouse hello 새 IP 주소를 구성한 후에 hello 연결 toohello 수신기를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="114c4-329">After you configure hello availability group toouse hello new IP address, configure hello connection toohello listener.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="114c4-330">다음 단계</span><span class="sxs-lookup"><span data-stu-id="114c4-330">Next steps</span></span>

- [<span data-ttu-id="114c4-331">다른 지역의 Azure Virtual Machines에서 SQL Server Always On 가용성 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="114c4-331">Configure a SQL Server Always On availability group on Azure virtual machines in different regions</span></span>](virtual-machines-windows-portal-sql-availability-group-dr.md)
