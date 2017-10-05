---
title: "SQL Server 가용성 그룹 - Azure Virtual Machines - 자습서 | Microsoft Docs"
description: "이 자습서에서는 Azure Virtual Machines에 SQL Server Always On 가용성 그룹을 만드는 방법을 보여 줍니다."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 228ca9ca5fddc493d27bfd6a40df5ee7306d6aa9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="80143-103">수동으로 Azure VM에서 Always On 가용성 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="80143-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="80143-104">이 자습서에서는 Azure Virtual Machines에 SQL Server Always On 가용성 그룹을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="80143-104">This tutorial shows how to create a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="80143-105">전체 자습서는 두 개의 SQL Server의 데이터베이스 복제본으로 가용성 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80143-105">The complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="80143-106">**예상 시간**: 필수 조건이 충족된 경우 완료하는 데 30분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="80143-106">**Time estimate**: Takes about 30 minutes to complete once the prerequisites are met.</span></span>

<span data-ttu-id="80143-107">다이어그램은 자습서에서 빌드할 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="80143-107">The diagram illustrates what you build in the tutorial.</span></span>

![가용성 그룹](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="80143-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="80143-109">Prerequisites</span></span>

<span data-ttu-id="80143-110">이 자습서는 사용자가 SQL Server Always On 가용성 그룹을 기본적으로 이해하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-110">The tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="80143-111">자세한 내용은 [Always On 가용성 그룹 개요(SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80143-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="80143-112">다음 표에 이 자습서를 시작하기 전에 완료해야 하는 필수 구성 요소가 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-112">The following table lists the prerequisites that you need to complete before starting this tutorial:</span></span>

|  |<span data-ttu-id="80143-113">요구 사항</span><span class="sxs-lookup"><span data-stu-id="80143-113">Requirement</span></span> |<span data-ttu-id="80143-114">설명</span><span class="sxs-lookup"><span data-stu-id="80143-114">Description</span></span> |
|----- |----- |----- |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="80143-116">SQL Server 2개</span><span class="sxs-lookup"><span data-stu-id="80143-116">Two SQL Servers</span></span> | <span data-ttu-id="80143-117">- Azure 가용성 집합에</span><span class="sxs-lookup"><span data-stu-id="80143-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="80143-118">- 단일 도메인에</span><span class="sxs-lookup"><span data-stu-id="80143-118">- In a single domain</span></span> <br/> <span data-ttu-id="80143-119">- 장애 조치(Failover) 클러스터링 기능(설치됨)</span><span class="sxs-lookup"><span data-stu-id="80143-119">- With Failover Clustering feature installed</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="80143-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="80143-121">Windows Server</span></span> | <span data-ttu-id="80143-122">클러스터 감시를 위한 파일 공유</span><span class="sxs-lookup"><span data-stu-id="80143-122">File share for cluster witness</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="80143-124">SQL Server 서비스 계정</span><span class="sxs-lookup"><span data-stu-id="80143-124">SQL Server service account</span></span> | <span data-ttu-id="80143-125">도메인 계정</span><span class="sxs-lookup"><span data-stu-id="80143-125">Domain account</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="80143-127">SQL Server 에이전트 서비스 계정</span><span class="sxs-lookup"><span data-stu-id="80143-127">SQL Server Agent service account</span></span> | <span data-ttu-id="80143-128">도메인 계정</span><span class="sxs-lookup"><span data-stu-id="80143-128">Domain account</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="80143-130">방화벽 포트 열기</span><span class="sxs-lookup"><span data-stu-id="80143-130">Firewall ports open</span></span> | <span data-ttu-id="80143-131">- SQL Server: 기본 인스턴스에 대해 **1433**</span><span class="sxs-lookup"><span data-stu-id="80143-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="80143-132">- 데이터베이스 미러링 끝점: **5022** 또는 사용 가능한 포트</span><span class="sxs-lookup"><span data-stu-id="80143-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="80143-133">- Azure Load Balancer 프로브: **59999** 또는 사용 가능한 포트</span><span class="sxs-lookup"><span data-stu-id="80143-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="80143-135">장애 조치(Failover) 클러스터링 기능 추가</span><span class="sxs-lookup"><span data-stu-id="80143-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="80143-136">이 기능을 필요로 하는 SQL Server 2개</span><span class="sxs-lookup"><span data-stu-id="80143-136">Both SQL Servers require this feature</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="80143-138">설치 도메인 계정</span><span class="sxs-lookup"><span data-stu-id="80143-138">Installation domain account</span></span> | <span data-ttu-id="80143-139">- 각 SQL Server의 로컬 관리자</span><span class="sxs-lookup"><span data-stu-id="80143-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="80143-140">- SQL Server의 각 인스턴스에 대해 SQL Server sysadmin 고정 서버 역할의 멤버</span><span class="sxs-lookup"><span data-stu-id="80143-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="80143-141">자습서를 시작하기 전에 [Azure Virtual Machines에 Always On 가용성 그룹을 만들기 위한 필수 조건을 완료](virtual-machines-windows-portal-sql-availability-group-prereq.md)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-141">Before you begin the tutorial, you need to [Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="80143-142">이러한 필수 구성 요소를 이미 완료한 경우 [클러스터 만들기](#CreateCluster)로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-142">If these prerequisites are completed already, you can jump to [Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="80143-143"><!--**Procedure**: *This is the first “step”. Make titles H2’s and short and clear – H2’s appear in the right pane on the web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="80143-143"><!--**Procedure**: *This is the first “step”. Make titles H2’s and short and clear – H2’s appear in the right pane on the web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create the cluster</span></span>

<span data-ttu-id="80143-144">필수 구성 요소를 완료한 후 첫 번째 단계는 두 개의 SQL Sever와 미러링 모니터 서버를 포함하는 Windows Server 장애 조치(Failover) 클러스터를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="80143-144">After the prerequisites are completed, the first step is to create a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="80143-145">SQL Server 및 미러링 모니터 서버에서 모두 관리자인 도메인 계정을 사용하여 첫 번째 SQL Server로 RDP합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-145">RDP to the first SQL Server using a domain account that is an administrator on both SQL Servers and the witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="80143-146">[필수 구성 요소 문서](virtual-machines-windows-portal-sql-availability-group-prereq.md)에 따라 **CORP\Install**이라고 하는 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-146">If you followed the [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="80143-147">이 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-147">Use this account.</span></span>

2. <span data-ttu-id="80143-148">**서버 관리자** 대시보드에서 **도구**를 선택한 후 **장애 조치(Failover) 클러스터 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-148">In the **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="80143-149">왼쪽 창에서 **장애 조치(Failover) 클러스터 관리자**를 마우스 오른쪽 단추로 클릭하고 **클러스터 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-149">In the left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="80143-150">![클러스터 만들기](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="80143-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="80143-151">클러스터 만들기 마법사에서 아래 표에 나온 설정으로 페이지를 단계별로 진행하여 1노드 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80143-151">In the Create Cluster Wizard, create a one-node cluster by stepping through the pages with the settings in the following table:</span></span>

   | <span data-ttu-id="80143-152">페이지</span><span class="sxs-lookup"><span data-stu-id="80143-152">Page</span></span> | <span data-ttu-id="80143-153">설정</span><span class="sxs-lookup"><span data-stu-id="80143-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="80143-154">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="80143-154">Before You Begin</span></span> |<span data-ttu-id="80143-155">기본값 사용</span><span class="sxs-lookup"><span data-stu-id="80143-155">Use defaults</span></span> |
   | <span data-ttu-id="80143-156">서버 선택</span><span class="sxs-lookup"><span data-stu-id="80143-156">Select Servers</span></span> |<span data-ttu-id="80143-157">첫 번째 SQL Server 이름을 **서버 이름 입력**에 입력하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-157">Type the first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="80143-158">유효성 검사 경고</span><span class="sxs-lookup"><span data-stu-id="80143-158">Validation Warning</span></span> |<span data-ttu-id="80143-159">**아니요. 이 클러스터에 대한 Microsoft의 지원이 필요 없으므로 유효성 검사 테스트를 실행하지 않습니다. [다음]을 클릭하면 클러스터 만들기를 계속합니다.**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want to run the validation tests. When I click Next, continue Creating the cluster**.</span></span> |
   | <span data-ttu-id="80143-160">클러스터 관리를 위한 액세스 지점</span><span class="sxs-lookup"><span data-stu-id="80143-160">Access Point for Administering the Cluster</span></span> |<span data-ttu-id="80143-161">클러스터 이름(예: **SQLAGCluster1**)을 **클러스터 이름**에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="80143-162">다음</span><span class="sxs-lookup"><span data-stu-id="80143-162">Confirmation</span></span> |<span data-ttu-id="80143-163">저장소 공간을 사용하지 않는 경우 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="80143-164">이 표 다음의 참고 사항을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80143-164">See the note following this table.</span></span> |

### <a name="set-the-cluster-ip-address"></a><span data-ttu-id="80143-165">클러스터 IP 주소 설정</span><span class="sxs-lookup"><span data-stu-id="80143-165">Set the cluster IP address</span></span>

1. <span data-ttu-id="80143-166">**장애 조치(Failover) 클러스터 관리자**에서 **클러스터 코어 리소스**로 아래로 스크롤하여 클러스터 세부 정보를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-166">In **Failover Cluster Manager**, scroll down to **Cluster Core Resources** and expand the cluster details.</span></span> <span data-ttu-id="80143-167">**이름** 및 **IP 주소** 리소스가 **실패** 상태에 모두 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="80143-167">You should see both the **Name** and the **IP Address** resources in the **Failed** state.</span></span> <span data-ttu-id="80143-168">클러스터에 컴퓨터 자체와 동일한 IP 주소가 할당되어 주소가 중복되므로 IP 주소 리소스는 온라인 상태로 전환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-168">The IP address resource cannot be brought online because the cluster is assigned the same IP address as the machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="80143-169">오류가 발생한 **IP 주소** 리소스를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-169">Right-click the failed **IP Address** resource, and then click **Properties**.</span></span>

   ![클러스터 속성](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="80143-171">**고정 IP 주소**를 선택하고 주소 텍스트 상자에서 SQL Server가 있는 서브넷에서 사용 가능한 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-171">Select **Static IP Address** and specify an available address from subnet where the SQL Server is in the Address text box.</span></span> <span data-ttu-id="80143-172">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="80143-173">**클러스터 코어 리소스** 섹션에서 클러스터 이름을 마우스 오른쪽 단추로 클릭하고 **온라인 상태로 전환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-173">In the **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="80143-174">그런 다음 두 리소스가 모두 온라인 상태로 전환될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="80143-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="80143-175">클러스터 이름 리소스가 온라인 상태가 되면 새 AD 컴퓨터 계정으로 DC 서버를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-175">When the cluster name resource comes online, it updates the DC server with a new AD computer account.</span></span> <span data-ttu-id="80143-176">이 AD 계정을 사용하여 나중에 가용성 그룹 클러스터형 서비스를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-176">Use this AD account to run the Availability Group clustered service later.</span></span>

### <span data-ttu-id="80143-177"><a name="addNode"></a>다른 SQL Server를 클러스터에 추가</span><span class="sxs-lookup"><span data-stu-id="80143-177"><a name="addNode"></a>Add the other SQL Server to cluster</span></span>

<span data-ttu-id="80143-178">다른 SQL Server를 클러스터에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-178">Add the other SQL Server to the cluster.</span></span>

1. <span data-ttu-id="80143-179">브라우저 트리에서 클러스터를 마우스 오른쪽 단추로 클릭하고 **노드 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-179">In the browser tree, right-click the cluster and click **Add Node**.</span></span>

    ![클러스터에 노드 추가](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="80143-181">**노드 추가 마법사**에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-181">In the **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="80143-182">**서버 선택** 페이지에서 두 번째 SQL Server를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-182">In the **Select Servers** page, add the second SQL Server.</span></span> <span data-ttu-id="80143-183">서버 이름을 **서버 이름 입력**에 입력하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-183">Type the server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="80143-184">완료하면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="80143-185">**유효성 검사 경고** 페이지에서 **아니요**(유효성 검사 테스트를 수행할 프로덕션 시나리오에서)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-185">In the **Validation Warning** page, click **No** (in a production scenario you should perform the validation tests).</span></span> <span data-ttu-id="80143-186">그런 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="80143-187">저장소 공간을 사용 중인 경우 **확인** 페이지에서 **클러스터에 사용할 수 있는 모든 저장소를 추가하세요.** 확인란을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-187">In the **Confirmation** page if you are using Storage Spaces, clear the checkbox labeled **Add all eligible storage to the cluster.**</span></span>

   ![노드 확인 추가](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="80143-189">만약 저장소 공간을 사용하면서 **클러스터에 사용할 수 있는 모든 저장소를 추가하세요.** 확인란을 선택 취소하지 않으면 Windows에서 클러스터링 프로세스 도중 가상 디스크를 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage to the cluster**, Windows detaches the virtual disks during the clustering process.</span></span> <span data-ttu-id="80143-190">그 결과, 저장소 공간이 클러스터에서 제거되고 PowerShell을 사용하여 다시 연결할 때까지 디스크 관리자 또는 탐색기에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-190">As a result, they do not appear in Disk Manager or Explorer until the storage spaces are removed from the cluster and reattached using PowerShell.</span></span> <span data-ttu-id="80143-191">저장소 공간은 여러 디스크를 저장소 풀로 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-191">Storage Spaces groups multiple disks in to storage pools.</span></span> <span data-ttu-id="80143-192">자세한 내용은 [저장소 공간](https://technet.microsoft.com/library/hh831739)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80143-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="80143-193">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-193">Click **Next**.</span></span>

1. <span data-ttu-id="80143-194">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-194">Click **Finish**.</span></span>

   <span data-ttu-id="80143-195">이제 장애 조치(Failover) 클러스터 관리자에 새 노드가 포함된 클러스터가 표시되고 **노드** 컨테이너에 목록으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="80143-195">Failover Cluster Manager shows that your cluster has a new node and lists it in the **Nodes** container.</span></span>

10. <span data-ttu-id="80143-196">원격 데스크톱 세션에서 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-196">Log out of the remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="80143-197">클러스터 쿼럼 파일 공유 추가</span><span class="sxs-lookup"><span data-stu-id="80143-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="80143-198">이 예제에서 Windows 클러스터는 파일 공유를 사용하여 클러스터 쿼럼을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80143-198">In this example the Windows cluster uses a file share to create a cluster quorum.</span></span> <span data-ttu-id="80143-199">이 자습서에서는 노드 및 파일 공유 과반수 쿼럼을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="80143-200">자세한 내용은 [장애 조치(Failover) 클러스터의 쿼럼 구성 이해](http://technet.microsoft.com/library/cc731739.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80143-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="80143-201">원격 데스크톱 세션으로 파일 공유 미러링 모니터 구성원 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-201">Connect to the file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="80143-202">**서버 관리자**에서 **도구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="80143-203">**컴퓨터 관리**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="80143-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="80143-204">**공유 폴더**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="80143-205">**공유**를 마우스 오른쪽 단추로 클릭하고 **새 공유...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![새 공유](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="80143-207">**공유 폴더 만들기 마법사**를 사용하여 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80143-207">Use **Create a Shared Folder Wizard** to create a share.</span></span>

1. <span data-ttu-id="80143-208">**폴더 경로**에서 **찾아보기**를 클릭한 후 공유 폴더에 대한 경로를 찾거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80143-208">On **Folder Path**, click **Browse** and locate or create a path for the shared folder.</span></span> <span data-ttu-id="80143-209">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-209">Click **Next**.</span></span>

1. <span data-ttu-id="80143-210">**이름, 설명 및 설정**에서 공유 이름 및 경로를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-210">In **Name, Description, and Settings** verify the share name and path.</span></span> <span data-ttu-id="80143-211">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-211">Click **Next**.</span></span>

1. <span data-ttu-id="80143-212">**공유 폴더 사용 권한**에서 **사용 권한 사용자 지정**을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="80143-213">**사용자 지정...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="80143-214">**사용 권한 사용자 지정**에서 **추가...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="80143-215">클러스터를 만드는 데 사용되는 계정에 모든 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-215">Make sure that the account used to create the cluster has full control.</span></span>

   ![새 공유](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="80143-217">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-217">Click **OK**.</span></span>

1. <span data-ttu-id="80143-218">**공유 폴더 사용 권한**에서 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="80143-219">**마침**을 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="80143-220">서버에서 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-220">Log out of the server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="80143-221">클러스터 쿼럼 구성</span><span class="sxs-lookup"><span data-stu-id="80143-221">Configure cluster quorum</span></span>

<span data-ttu-id="80143-222">다음으로 클러스터 쿼럼을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-222">Next, set the cluster quorum.</span></span>

1. <span data-ttu-id="80143-223">원격 데스크톱을 사용하여 첫 번째 클러스터 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-223">Connect to the first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="80143-224">**장애 조치(Failover) 클러스터 관리자**에서 클러스터를 마우스 오른쪽 단추로 클릭하고, **기타 작업**을 가리킨 다음 **클러스터 쿼럼 설정 구성...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-224">In **Failover Cluster Manager**, right-click the cluster, point to **More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![새 공유](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="80143-226">**클러스터 쿼럼 구성 마법사**에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="80143-227">**쿼럼 구성 옵션 선택**에서 **쿼럼 감시 선택**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-227">In **Select Quorum Configuration Option**, choose **Select the quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="80143-228">**쿼럼 감시 선택**에서 **파일 공유 감시 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="80143-229">Windows Server 2016은 클라우드 감시를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="80143-230">이 유형의 감시를 선택한 경우 파일 공유 감시가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="80143-231">자세한 내용은 [장애 조치(Failover) 클러스터에 대한 클라우드 감시 배포](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80143-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="80143-232">이 자습서에서는 이전 운영 체제에서 지원되는 파일 공유 감시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="80143-233">**파일 공유 감시 구성**에서 사용자가 만든 공유에 대한 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-233">On **Configure File Share Witness**, type the path for the share you created.</span></span> <span data-ttu-id="80143-234">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-234">Click **Next**.</span></span>

1. <span data-ttu-id="80143-235">**확인**에서 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-235">Verify the settings on **Confirmation**.</span></span> <span data-ttu-id="80143-236">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-236">Click **Next**.</span></span>

1. <span data-ttu-id="80143-237">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-237">Click **Finish**.</span></span>

<span data-ttu-id="80143-238">클러스터 코어 리소스는 파일 공유 감시로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="80143-238">The cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="80143-239">가용성 그룹 사용</span><span class="sxs-lookup"><span data-stu-id="80143-239">Enable Availability Groups</span></span>

<span data-ttu-id="80143-240">다음으로 **AlwaysOn 가용성 그룹** 기능을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-240">Next, enable the **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="80143-241">두 SQL Server에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="80143-242">**시작** 화면에서 **SQL Server 구성 관리자**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-242">From the **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="80143-243">브라우저 트리에서 **SQL Server 서비스**를 클릭하고 **SQL Server (MSSQLSERVER)** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-243">In the browser tree, click **SQL Server Services**, then right-click the **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="80143-244">**AlwaysOn 고가용성** 탭을 클릭한 후 다음과 같이 **AlwaysOn 가용성 그룹 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-244">Click the **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![AlwaysOn 가용성 그룹 사용](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="80143-246">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-246">Click **Apply**.</span></span> <span data-ttu-id="80143-247">팝업 대화 상자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-247">Click **OK** in the pop-up dialog.</span></span>

5. <span data-ttu-id="80143-248">SQL Server 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-248">Restart the SQL Server service.</span></span>

<span data-ttu-id="80143-249">다른 SQL Server에서도 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-249">Repeat these steps on the other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for the database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for the instance of SQL Server that is used to synchronize the database replicas in the Availability Groups on that instance.

On both SQL Servers, open the firewall for the TCP port for the database mirroring endpoint.

1. On the first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In the left pane, select **Inbound Rules**. On the right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For the port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In the **Action** page, keep **Allow the connection** selected and click **Next**.
6. In the **Profile** page, accept the default settings and click **Next**.
7. In the **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in the **Name** text box, then click **Finish**.

Repeat these steps on the second SQL Server.
-------------------------->

## <a name="create-a-database-on-the-first-sql-server"></a><span data-ttu-id="80143-250">첫 번째 SQL Server에서 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="80143-250">Create a database on the first SQL Server</span></span>

1. <span data-ttu-id="80143-251">Sysadmin 고정 서버 역할의 구성원인 도메인 계정을 사용하여 첫 번째 SQL Server에 RDP 파일을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-251">Launch the RDP file to the first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="80143-252">SQL Server Management Studio를 열고 첫 번째 SQL Server에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-252">Open SQL Server Management Studio and connect to the first SQL Server.</span></span>
7. <span data-ttu-id="80143-253">**개체 탐색기**에서 **데이터베이스**를 마우스 오른쪽 단추로 클릭하고 **새 데이터베이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="80143-254">**데이터베이스 이름**에 **MyDB1**을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="80143-255"><a name="backupshare"></a> 백업 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="80143-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="80143-256">첫 번째 SQL Server의 **서버 관리자**에서 **도구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-256">On the first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="80143-257">**컴퓨터 관리**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="80143-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="80143-258">**공유 폴더**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="80143-259">**공유**를 마우스 오른쪽 단추로 클릭하고 **새 공유...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![새 공유](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="80143-261">**공유 폴더 만들기 마법사**를 사용하여 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80143-261">Use **Create a Shared Folder Wizard** to create a share.</span></span>

1. <span data-ttu-id="80143-262">**폴더 경로**에서 **찾아보기**를 클릭한 후 데이터베이스 백업 공유 폴더에 대한 경로를 찾거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80143-262">On **Folder Path**, click **Browse** and locate or create a path for the database backup shared folder.</span></span> <span data-ttu-id="80143-263">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-263">Click **Next**.</span></span>

1. <span data-ttu-id="80143-264">**이름, 설명 및 설정**에서 공유 이름 및 경로를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-264">In **Name, Description, and Settings** verify the share name and path.</span></span> <span data-ttu-id="80143-265">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-265">Click **Next**.</span></span>

1. <span data-ttu-id="80143-266">**공유 폴더 사용 권한**에서 **사용 권한 사용자 지정**을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="80143-267">**사용자 지정...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="80143-268">**사용 권한 사용자 지정**에서 **추가...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="80143-269">두 서버 모두에 대한 SQL Server 및 SQL Server 에이전트 서비스 계정에 모든 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-269">Make sure that the SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![새 공유](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="80143-271">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-271">Click **OK**.</span></span>

1. <span data-ttu-id="80143-272">**공유 폴더 사용 권한**에서 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="80143-273">**마침**을 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-the-database"></a><span data-ttu-id="80143-274">데이터베이스의 전체 백업 수행</span><span class="sxs-lookup"><span data-stu-id="80143-274">Take a full backup of the database</span></span>

<span data-ttu-id="80143-275">새 데이터베이스를 백업하여 로그 체인을 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-275">You need to back up the new database to initialize the log chain.</span></span> <span data-ttu-id="80143-276">새 데이터베이스의 백업을 수행하지 않으면 가용성 그룹에 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-276">If you do not take a backup of the new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="80143-277">**개체 탐색기**에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **작업...**을 가리킨 다음 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-277">In **Object Explorer**, right-click the database, point to **Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="80143-278">**확인**을 클릭하여 기본 백업 위치로 전체 백업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-278">Click **OK** to take a full backup to the default backup location.</span></span>

## <a name="create-the-availability-group"></a><span data-ttu-id="80143-279">가용성 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="80143-279">Create the Availability Group</span></span>
<span data-ttu-id="80143-280">이제 다음과 같은 단계를 통해 가용성 그룹을 구성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-280">You are now ready to configure an Availability Group using the following steps:</span></span>

* <span data-ttu-id="80143-281">첫 번째 SQL Server에서 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80143-281">Create a database on the first SQL Server.</span></span>
* <span data-ttu-id="80143-282">데이터베이스의 전체 백업 및 트랜잭션 로그 백업 수행</span><span class="sxs-lookup"><span data-stu-id="80143-282">Take both a full backup and a transaction log backup of the database</span></span>
* <span data-ttu-id="80143-283">**NORECOVERY** 옵션으로 전체 및 로그 백업을 두 번째 SQL Server로 복원</span><span class="sxs-lookup"><span data-stu-id="80143-283">Restore the full and log backups to the second SQL Server with the **NORECOVERY** option</span></span>
* <span data-ttu-id="80143-284">동기 커밋, 자동 장애 조치(failover) 및 읽을 수 있는 보조 복제본으로 가용성 그룹 만들기(**AG1**)</span><span class="sxs-lookup"><span data-stu-id="80143-284">Create the Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-the-availability-group"></a><span data-ttu-id="80143-285">가용성 그룹 만들기:</span><span class="sxs-lookup"><span data-stu-id="80143-285">Create the Availability Group:</span></span>

1. <span data-ttu-id="80143-286">첫 번째 SQL Server에 원격 데스크톱 세션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="80143-286">On remote desktop session to the first SQL Server.</span></span> <span data-ttu-id="80143-287">SSMS의 **개체 탐색기**에서 **AlwaysOn 고가용성**을 마우스 오른쪽 단추로 클릭하고 **새 가용성 그룹 마법사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![새 가용성 그룹 마법사 시작](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="80143-289">**소개** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-289">In the **Introduction** page, click **Next**.</span></span> <span data-ttu-id="80143-290">**가용성 그룹 이름 지정** 페이지의 **가용성 그룹 이름**에 가용성 그룹에 사용할 이름(예: **AG1**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-290">In the **Specify Availability Group Name** page, type a name for the Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="80143-291">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-291">Click **Next**.</span></span>

    ![새 AG 마법사, AG 이름 지정](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="80143-293">**데이터베이스 선택** 페이지에서 데이터베이스를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-293">In the **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="80143-294">원하는 주 복제본에서 전체 백업을 하나 이상 생성했으므로, 이러한 데이터베이스는 가용성 그룹의 필수 구성 요소를 충족합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-294">The database meets the prerequisites for an Availability Group because you have taken at least one full backup on the intended primary replica.</span></span>

   ![새 AG 마법사, 데이터베이스 선택](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="80143-296">**복제본 지정** 페이지에서 **복제본 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-296">In the **Specify Replicas** page, click **Add Replica**.</span></span>

   ![새 AG 마법사, 복제본 지정](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="80143-298">**서버에 연결** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="80143-298">The **Connect to Server** dialog pops up.</span></span> <span data-ttu-id="80143-299">두 번째 서버 이름을 **서버 이름**에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-299">Type the name of the second server in **Server name**.</span></span> <span data-ttu-id="80143-300">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-300">Click **Connect**.</span></span>

   <span data-ttu-id="80143-301">**복제본 지정** 페이지로 돌아가면 이제 **가용성 복제본**에 두 번째 서버가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="80143-301">Back in the **Specify Replicas** page, you should now see the second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="80143-302">아래와 같이 복제본을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-302">Configure the replicas as follows.</span></span>

   ![새 AG 마법사, 복제본 지정(전체)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="80143-304">**끝점**을 클릭하여 이 가용성 그룹에 사용될 데이터베이스 미러링 끝점을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-304">Click **Endpoints** to see the database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="80143-305">[데이터베이스 미러링 끝점에 대한 방화벽 규칙](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall)을 설정할 때 사용한 것과 동일한 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-305">Use the same port that you used when you set the [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![새 AG 마법사, 초기 데이터 동기화 선택](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="80143-307">**초기 데이터 동기화 선택** 페이지에서 **전체**를 선택하고 공유 네트워크 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-307">In the **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="80143-308">위치의 경우 [만든 백업 공유](#backupshare)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-308">For the location, use the [backup share that you created](#backupshare).</span></span> <span data-ttu-id="80143-309">예제에서는 **\\\\\<First SQL Server\>\Backup\**입니다.</span><span class="sxs-lookup"><span data-stu-id="80143-309">In the example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="80143-310">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="80143-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="80143-311">전체 동기화는 SQL Server의 첫 번째 인스턴스에서 데이터베이스의 전체 백업을 수행하고 두 번째 인스턴스로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-311">Full synchronization takes a full backup of the database on the first instance of SQL Server and restores it to the second instance.</span></span> <span data-ttu-id="80143-312">대형 데이터베이스의 경우 전체 동기화는 시간이 오래 걸릴 수 있으므로 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="80143-313">수동으로 데이터베이스의 백업을 수행하고 `NO RECOVERY`를 통해 복원하여 이 시간을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-313">You can reduce this time by manually taking a backup of the database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="80143-314">가용성 그룹을 구성하기 전에 두 번째 SQL Server에서 이미 `NO RECOVERY`로 데이터베이스를 복원한 경우 **조인만**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-314">If the database is already restored with `NO RECOVERY` on the second SQL Server before configuring the Availability Group, choose **Join only**.</span></span> <span data-ttu-id="80143-315">가용성 그룹을 구성한 후 백업을 수행하려는 경우 **초기 데이터 동기화 건너뛰기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-315">If you want to take the backup after configuring the Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![새 AG 마법사, 초기 데이터 동기화 선택](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="80143-317">**유효성 검사** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-317">In the **Validation** page, click **Next**.</span></span> <span data-ttu-id="80143-318">이 페이지는 다음 이미지와 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="80143-318">This page should look similar to the following image:</span></span>

    ![새 AG 마법사, 유효성 검사](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="80143-320">가용성 그룹 수신기가 구성되어 있지 않으므로 수신기 구성에 대한 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="80143-320">There is a warning for the listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="80143-321">Azure Virtual Machines에서 Azure Load Balancer를 만든 후 수신기를 만들기 때문에 이 경고는 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-321">You can ignore this warning because on Azure virtual machines you create the listener after creating the Azure load balancer.</span></span>

10. <span data-ttu-id="80143-322">**요약** 페이지에서 **마침**을 클릭한 후 마법사에서 새 가용성 그룹을 구성하는 동안 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="80143-322">In the **Summary** page, click **Finish**, then wait while the wizard configures the new Availability Group.</span></span> <span data-ttu-id="80143-323">**진행률** 페이지에서 **자세한 내용**을 클릭하여 자세한 진행 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-323">In the **Progress** page, you can click **More details** to view the detailed progress.</span></span> <span data-ttu-id="80143-324">마법사가 완료되면 **결과** 페이지를 검토하여 가용성 그룹이 올바르게 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-324">Once the wizard is finished, inspect the **Results** page to verify that the Availability Group is successfully created.</span></span>

     ![새 AG 마법사, 결과](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="80143-326">**닫기**를 클릭하여 마법사를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-326">Click **Close** to exit the wizard.</span></span>

### <a name="check-the-availability-group"></a><span data-ttu-id="80143-327">가용성 그룹 확인</span><span class="sxs-lookup"><span data-stu-id="80143-327">Check the Availability Group</span></span>

1. <span data-ttu-id="80143-328">**개체 탐색기**에서 **AlwaysOn 고가용성**을 확장하고 **가용성 그룹**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="80143-329">이 컨테이너에 새 가용성 그룹이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="80143-329">You should now see the new Availability Group in this container.</span></span> <span data-ttu-id="80143-330">가용성 그룹을 마우스 오른쪽 단추로 클릭하고 **대시보드 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-330">Right-click the Availability Group and click **Show Dashboard**.</span></span>

   ![AG 대시보드 표시](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="80143-332">**AlwaysOn 대시보드**는 다음과 유사하게 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-332">Your **AlwaysOn Dashboard** should look similar to this.</span></span>

   ![AG 대시보드](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="80143-334">복제본, 각 복제본의 장애 조치(failover) 모드 및 동기화 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-334">You can see the replicas, the failover mode of each replica and the synchronization state.</span></span>

2. <span data-ttu-id="80143-335">**장애 조치(Failover) 클러스터 관리자**에서 클러스터를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="80143-336">**역할**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-336">Select **Roles**.</span></span> <span data-ttu-id="80143-337">사용하는 가용성 그룹 이름은 클러스터에서 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="80143-337">The Availability Group name you used is a role on the cluster.</span></span> <span data-ttu-id="80143-338">수신기를 구성하지 않았기 때문에 해당 가용성 그룹은 클라이언트 연결에 대한 IP 주소가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="80143-339">Azure Load Balancer를 만든 후에 수신기를 구성하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80143-339">You will configure the listener after you create an Azure load balancer.</span></span>

   ![장애 조치(Failover) 클러스터 관리자에서 AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="80143-341">장애 조치(Failover) 클러스터 관리자에서 가용성 그룹으로 장애 조치를 시도하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="80143-341">Do not try to fail over the Availability Group from the Failover Cluster Manager.</span></span> <span data-ttu-id="80143-342">모든 장애 조치(Failover) 작업은 SSMS의 **AlwaysOn 대시보드** 에서 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="80143-343">자세한 내용은 [가용성 그룹에서 장애 조치(Failover) 클러스터 관리자 사용에 대한 제한 사항](https://msdn.microsoft.com/library/ff929171.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80143-343">For more information, see [Restrictions on Using The Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="80143-344">이 시점에서 SQL Server의 두 인스턴스에서 복제와 함께 가용성 그룹을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80143-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="80143-345">가용성 그룹을 인스턴스 간에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-345">You can move the Availability Group between instances.</span></span> <span data-ttu-id="80143-346">아직 수신기가 없으므로 가용성 그룹에 연결할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-346">You cannot connect to the Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="80143-347">Azure Virtual Machines에서 수신기에는 분산 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-347">In Azure virtual machines, the listener requires a load balancer.</span></span> <span data-ttu-id="80143-348">다음 단계는 Azure에서 부하 분산 장치를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="80143-348">The next step is to create the load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="80143-349">Azure Load Balancer 만들기</span><span class="sxs-lookup"><span data-stu-id="80143-349">Create an Azure load balancer</span></span>

<span data-ttu-id="80143-350">Azure Virtual Machines에서 SQL Server 가용성 그룹에는 부하 분산 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="80143-351">부하 분산 장치는 가용성 그룹 수신기의 IP 주소를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-351">The load balancer holds the IP address for the Availability Group listener.</span></span> <span data-ttu-id="80143-352">이 섹션에서는 Azure Portal에서 부하 분산 장치를 만드는 방법을 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-352">This section summarizes how to create the load balancer in the Azure portal.</span></span>

1. <span data-ttu-id="80143-353">Azure Portal에서 SQL Server가 있는 리소스 그룹으로 이동하여 **+추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-353">In the Azure portal, go to the resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="80143-354">**부하 분산 장치**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="80143-355">Microsoft에서 게시한 부하 분산 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-355">Choose the load balancer published by Microsoft.</span></span>

   ![장애 조치(Failover) 클러스터 관리자에서 AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="80143-357">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-357">Click **Create**.</span></span>
3. <span data-ttu-id="80143-358">부하 분산 장치에 대한 다음 매개 변수를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-358">Configure the following parameters for the load balancer.</span></span>

   | <span data-ttu-id="80143-359">설정</span><span class="sxs-lookup"><span data-stu-id="80143-359">Setting</span></span> | <span data-ttu-id="80143-360">필드</span><span class="sxs-lookup"><span data-stu-id="80143-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="80143-361">**Name**</span><span class="sxs-lookup"><span data-stu-id="80143-361">**Name**</span></span> |<span data-ttu-id="80143-362">예를 들어 **sqlLB**와 같은 부하 분산 장치에 대한 텍스트 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-362">Use a text name for the load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="80143-363">**형식**</span><span class="sxs-lookup"><span data-stu-id="80143-363">**Type**</span></span> |<span data-ttu-id="80143-364">내부</span><span class="sxs-lookup"><span data-stu-id="80143-364">Internal</span></span> |
   | <span data-ttu-id="80143-365">**가상 네트워크**</span><span class="sxs-lookup"><span data-stu-id="80143-365">**Virtual network**</span></span> |<span data-ttu-id="80143-366">Azure Virtual Network의 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-366">Use the name of the Azure virtual network.</span></span> |
   | <span data-ttu-id="80143-367">**서브넷**</span><span class="sxs-lookup"><span data-stu-id="80143-367">**Subnet**</span></span> |<span data-ttu-id="80143-368">가상 컴퓨터가 있는 서브넷 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-368">Use the name of the subnet that the virtual machine is in.</span></span>  |
   | <span data-ttu-id="80143-369">**IP 주소 할당**</span><span class="sxs-lookup"><span data-stu-id="80143-369">**IP address assignment**</span></span> |<span data-ttu-id="80143-370">정적</span><span class="sxs-lookup"><span data-stu-id="80143-370">Static</span></span> |
   | <span data-ttu-id="80143-371">**IP 주소**</span><span class="sxs-lookup"><span data-stu-id="80143-371">**IP address**</span></span> |<span data-ttu-id="80143-372">서브넷에서 사용 가능한 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="80143-373">**구독**</span><span class="sxs-lookup"><span data-stu-id="80143-373">**Subscription**</span></span> |<span data-ttu-id="80143-374">가상 컴퓨터와 동일한 구독을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-374">Use the same subscription as the virtual machine.</span></span> |
   | <span data-ttu-id="80143-375">**위치**:</span><span class="sxs-lookup"><span data-stu-id="80143-375">**Location**</span></span> |<span data-ttu-id="80143-376">가상 컴퓨터와 동일한 위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-376">Use the same location as the virtual machine.</span></span> |

   <span data-ttu-id="80143-377">Azure Portal 블레이드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-377">The Azure portal blade should look like this:</span></span>

   ![부하 분산 장치 만들기](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="80143-379">**만들기**를 클릭하여 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80143-379">Click **Create**, to create the load balancer.</span></span>

<span data-ttu-id="80143-380">부하 분산 장치를 구성하려면 백 엔드 풀, 프로브를 만들고 부하 분산 규칙을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-380">To configure the load balancer, you need to create a backend pool, a probe, and set the load balancing rules.</span></span> <span data-ttu-id="80143-381">Azure Portal에서 이러한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-381">Do these in the Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="80143-382">백 엔드 풀 추가</span><span class="sxs-lookup"><span data-stu-id="80143-382">Add backend pool</span></span>

1. <span data-ttu-id="80143-383">Azure Portal에서 가용성 그룹으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-383">In the Azure portal, go to your availability group.</span></span> <span data-ttu-id="80143-384">새로 만든 부하 분산 장치를 보려면 보기를 새로 고쳐야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-384">You might need to refresh the view to see the newly created load balancer.</span></span>

   ![리소스 그룹의 부하 분산 장치 찾기](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="80143-386">부하 분산 장치를 클릭하고 **백엔드 풀**, **+추가**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-386">Click the load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="80143-387">백엔드 풀을 다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-387">Set the backend pool as follows:</span></span>

   | <span data-ttu-id="80143-388">설정</span><span class="sxs-lookup"><span data-stu-id="80143-388">Setting</span></span> | <span data-ttu-id="80143-389">설명</span><span class="sxs-lookup"><span data-stu-id="80143-389">Description</span></span> | <span data-ttu-id="80143-390">예제</span><span class="sxs-lookup"><span data-stu-id="80143-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="80143-391">**Name**</span><span class="sxs-lookup"><span data-stu-id="80143-391">**Name**</span></span> | <span data-ttu-id="80143-392">텍스트 이름 입력</span><span class="sxs-lookup"><span data-stu-id="80143-392">Type a text name</span></span> | <span data-ttu-id="80143-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="80143-393">SQLLBBE</span></span>
   | <span data-ttu-id="80143-394">**연결 대상**</span><span class="sxs-lookup"><span data-stu-id="80143-394">**Associated to**</span></span> | <span data-ttu-id="80143-395">목록에서 선택</span><span class="sxs-lookup"><span data-stu-id="80143-395">Pick from list</span></span> | <span data-ttu-id="80143-396">가용성 집합</span><span class="sxs-lookup"><span data-stu-id="80143-396">Availability set</span></span>
   | <span data-ttu-id="80143-397">**가용성 집합**</span><span class="sxs-lookup"><span data-stu-id="80143-397">**Availability set**</span></span> | <span data-ttu-id="80143-398">SQL Server VM이 있는 가용성 집합의 이름 사용</span><span class="sxs-lookup"><span data-stu-id="80143-398">Use a name of the availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="80143-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="80143-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="80143-400">**가상 컴퓨터**</span><span class="sxs-lookup"><span data-stu-id="80143-400">**Virtual machines**</span></span> |<span data-ttu-id="80143-401">두 개의 Azure SQL Server VM 이름</span><span class="sxs-lookup"><span data-stu-id="80143-401">The two Azure SQL Server VM names</span></span> | <span data-ttu-id="80143-402">sqlserver-0, sqlserver-1</span><span class="sxs-lookup"><span data-stu-id="80143-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="80143-403">백 엔드 풀에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-403">Type the name for the back end pool.</span></span>

1. <span data-ttu-id="80143-404">**+가상 컴퓨터 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="80143-405">가용성 집합의 경우 SQL Server가 있는 가용성 집합을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-405">For the availability set, choose the availability set that the SQL Servers are in.</span></span>

1. <span data-ttu-id="80143-406">가상 컴퓨터의 경우 두 SQL Server를 모두 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-406">For virtual machines, include both of the SQL Servers.</span></span> <span data-ttu-id="80143-407">파일 공유 미러링 모니터 서버는 포함하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="80143-407">Do not include the file share witness server.</span></span>

1. <span data-ttu-id="80143-408">**확인**을 클릭하여 백엔드 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80143-408">Click **OK** to create the backend pool.</span></span>

### <a name="set-the-probe"></a><span data-ttu-id="80143-409">프로브 설정</span><span class="sxs-lookup"><span data-stu-id="80143-409">Set the probe</span></span>

1. <span data-ttu-id="80143-410">부하 분산 장치를 클릭하고 **상태 프로브**, **+추가**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-410">Click the load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="80143-411">다음과 같이 상태 프로브를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-411">Set the health probe as follows:</span></span>

   | <span data-ttu-id="80143-412">설정</span><span class="sxs-lookup"><span data-stu-id="80143-412">Setting</span></span> | <span data-ttu-id="80143-413">설명</span><span class="sxs-lookup"><span data-stu-id="80143-413">Description</span></span> | <span data-ttu-id="80143-414">예제</span><span class="sxs-lookup"><span data-stu-id="80143-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="80143-415">**Name**</span><span class="sxs-lookup"><span data-stu-id="80143-415">**Name**</span></span> | <span data-ttu-id="80143-416">텍스트</span><span class="sxs-lookup"><span data-stu-id="80143-416">Text</span></span> | <span data-ttu-id="80143-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="80143-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="80143-418">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="80143-418">**Protocol**</span></span> | <span data-ttu-id="80143-419">TCP 선택</span><span class="sxs-lookup"><span data-stu-id="80143-419">Choose TCP</span></span> | <span data-ttu-id="80143-420">TCP</span><span class="sxs-lookup"><span data-stu-id="80143-420">TCP</span></span> |
   | <span data-ttu-id="80143-421">**포트**</span><span class="sxs-lookup"><span data-stu-id="80143-421">**Port**</span></span> | <span data-ttu-id="80143-422">사용하지 않는 모든 포트</span><span class="sxs-lookup"><span data-stu-id="80143-422">Any unused port</span></span> | <span data-ttu-id="80143-423">59999</span><span class="sxs-lookup"><span data-stu-id="80143-423">59999</span></span> |
   | <span data-ttu-id="80143-424">**간격**</span><span class="sxs-lookup"><span data-stu-id="80143-424">**Interval**</span></span>  | <span data-ttu-id="80143-425">프로브 시도 간격(초)</span><span class="sxs-lookup"><span data-stu-id="80143-425">The amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="80143-426">5</span><span class="sxs-lookup"><span data-stu-id="80143-426">5</span></span> |
   | <span data-ttu-id="80143-427">**비정상 임계값**</span><span class="sxs-lookup"><span data-stu-id="80143-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="80143-428">가상 컴퓨터가 비정상 상태로 간주되기 위한 연속된 프로브 실패 횟수</span><span class="sxs-lookup"><span data-stu-id="80143-428">The number of consecutive probe failures that must occur for a virtual machine to be considered unhealthy</span></span>  | <span data-ttu-id="80143-429">2</span><span class="sxs-lookup"><span data-stu-id="80143-429">2</span></span> |

1. <span data-ttu-id="80143-430">**확인**을 클릭하여 상태 프로브를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-430">Click **OK** to set the health probe.</span></span>

### <a name="set-the-load-balancing-rules"></a><span data-ttu-id="80143-431">부하 분산 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="80143-431">Set the load balancing rules</span></span>

1. <span data-ttu-id="80143-432">부하 분산 장치를 클릭하고 **부하 분산 규칙**, **+추가**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-432">Click the load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="80143-433">부하 분산 규칙을 다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-433">Set the load balancing rules as follows.</span></span>
   | <span data-ttu-id="80143-434">설정</span><span class="sxs-lookup"><span data-stu-id="80143-434">Setting</span></span> | <span data-ttu-id="80143-435">설명</span><span class="sxs-lookup"><span data-stu-id="80143-435">Description</span></span> | <span data-ttu-id="80143-436">예제</span><span class="sxs-lookup"><span data-stu-id="80143-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="80143-437">**Name**</span><span class="sxs-lookup"><span data-stu-id="80143-437">**Name**</span></span> | <span data-ttu-id="80143-438">텍스트</span><span class="sxs-lookup"><span data-stu-id="80143-438">Text</span></span> | <span data-ttu-id="80143-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="80143-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="80143-440">**프런트 엔드 IP 주소**</span><span class="sxs-lookup"><span data-stu-id="80143-440">**Frontend IP address**</span></span> | <span data-ttu-id="80143-441">주소 선택</span><span class="sxs-lookup"><span data-stu-id="80143-441">Choose an address</span></span> |<span data-ttu-id="80143-442">부하 분산 장치를 만들 때 생성된 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-442">Use the address that you created when you created the load balancer.</span></span> |
   | <span data-ttu-id="80143-443">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="80143-443">**Protocol**</span></span> | <span data-ttu-id="80143-444">TCP 선택</span><span class="sxs-lookup"><span data-stu-id="80143-444">Choose TCP</span></span> |<span data-ttu-id="80143-445">TCP</span><span class="sxs-lookup"><span data-stu-id="80143-445">TCP</span></span> |
   | <span data-ttu-id="80143-446">**포트**</span><span class="sxs-lookup"><span data-stu-id="80143-446">**Port**</span></span> | <span data-ttu-id="80143-447">SQL Server 인스턴스에 대한 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-447">Use the port for the SQL Server instance</span></span> | <span data-ttu-id="80143-448">1433</span><span class="sxs-lookup"><span data-stu-id="80143-448">1433</span></span> |
   | <span data-ttu-id="80143-449">**백 엔드 포트**</span><span class="sxs-lookup"><span data-stu-id="80143-449">**Backend Port**</span></span> | <span data-ttu-id="80143-450">이 필드는 부동 IP가 직접 서버 반환에 대해 설정된 경우 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="80143-451">1433</span><span class="sxs-lookup"><span data-stu-id="80143-451">1433</span></span> |
   | <span data-ttu-id="80143-452">**프로브**</span><span class="sxs-lookup"><span data-stu-id="80143-452">**Probe**</span></span> |<span data-ttu-id="80143-453">프로브에 대해 지정한 이름</span><span class="sxs-lookup"><span data-stu-id="80143-453">The name you specified for the probe</span></span> | <span data-ttu-id="80143-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="80143-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="80143-455">**세션 지속성**</span><span class="sxs-lookup"><span data-stu-id="80143-455">**Session Persistence**</span></span> | <span data-ttu-id="80143-456">드롭다운 목록</span><span class="sxs-lookup"><span data-stu-id="80143-456">Drop down list</span></span> | <span data-ttu-id="80143-457">**없음**</span><span class="sxs-lookup"><span data-stu-id="80143-457">**None**</span></span> |
   | <span data-ttu-id="80143-458">**유휴 시간 제한**</span><span class="sxs-lookup"><span data-stu-id="80143-458">**Idle Timeout**</span></span> | <span data-ttu-id="80143-459">TCP 연결을 열린 상태로 유지하는 시간(분)</span><span class="sxs-lookup"><span data-stu-id="80143-459">Minutes to keep a TCP connection open</span></span> | <span data-ttu-id="80143-460">4</span><span class="sxs-lookup"><span data-stu-id="80143-460">4</span></span> |
   | <span data-ttu-id="80143-461">**부동 IP(Direct Server Return)**</span><span class="sxs-lookup"><span data-stu-id="80143-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="80143-462">사용</span><span class="sxs-lookup"><span data-stu-id="80143-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="80143-463">직접 서버 반환은 만드는 동안 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="80143-463">Direct server return is set during creation.</span></span> <span data-ttu-id="80143-464">이는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-464">It cannot be changed.</span></span>

1. <span data-ttu-id="80143-465">**확인**을 클릭하여 부하 분산 규칙을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-465">Click **OK** to set the load balancing rules.</span></span>

## <span data-ttu-id="80143-466"><a name="configure-listener"></a> 수신기 구성</span><span class="sxs-lookup"><span data-stu-id="80143-466"><a name="configure-listener"></a> Configure the listener</span></span>

<span data-ttu-id="80143-467">다음에 수행할 작업은 장애 조치(failover) 클러스터에서 가용성 그룹 수신기를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="80143-467">The next thing to do is to configure an Availability Group listener on the failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="80143-468">이 자습서에서는 ILB IP 주소 하나로 단일 수신기를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="80143-468">This tutorial shows how to create a single listener - with one ILB IP address.</span></span> <span data-ttu-id="80143-469">하나 이상의 IP 주소를 사용하여 하나 이상의 수신기를 만들려면 [가용성 그룹 수신기 및 부하 분산 장치 만들기 | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80143-469">To create one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="80143-470">수신기 포트 설정</span><span class="sxs-lookup"><span data-stu-id="80143-470">Set listener port</span></span>

<span data-ttu-id="80143-471">SQL Server Management Studio에서 수신기 포트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-471">In SQL Server Management Studio, set the listener port.</span></span>

1. <span data-ttu-id="80143-472">SQL Server Management Studio를 시작하고 주 복제본에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-472">Launch SQL Server Management Studio and connect to the primary replica.</span></span>

1. <span data-ttu-id="80143-473">**AlwaysOn 고가용성** | **가용성 그룹** | **가용성 그룹 수신기**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-473">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="80143-474">이제 장애 조치(Failover) 클러스터 관리자에서 만든 수신기 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="80143-474">You should now see the listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="80143-475">수신기 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-475">Right-click the listener name and click **Properties**.</span></span>

1. <span data-ttu-id="80143-476">**포트** 상자에서 이전에 사용한 $EndpointPort(1433이 기본값임)를 사용하여 가용성 그룹 수신기에 대한 포트 번호를 지정한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-476">In the **Port** box, specify the port number for the Availability Group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span></span>

<span data-ttu-id="80143-477">이제 Resource Manager 모드에서 실행 중인 Azure Virtual Machines의 SQL Server 가용성 그룹이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-to-listener"></a><span data-ttu-id="80143-478">수신기에 대한 연결 테스트</span><span class="sxs-lookup"><span data-stu-id="80143-478">Test connection to listener</span></span>

<span data-ttu-id="80143-479">연결을 테스트하려면</span><span class="sxs-lookup"><span data-stu-id="80143-479">To test the connection:</span></span>

1. <span data-ttu-id="80143-480">동일한 가상 네트워크에 있지만 복제본을 소유하지 않는 SQL Server로 RDP합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-480">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="80143-481">클러스터의 다른 SQL Server를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80143-481">You can use the other SQL Server in the cluster.</span></span>

1. <span data-ttu-id="80143-482">**sqlcmd** 유틸리티를 사용하여 연결을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-482">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="80143-483">예를 들어 다음 스크립트는 Windows 인증을 사용하는 수신기를 통해 주 복제본에 대한 **sqlcmd** 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-483">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="80143-484">수신기가 기본 포트(1433) 이외의 포트를 사용하는 경우 연결 문자열에서 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-484">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span></span> <span data-ttu-id="80143-485">예를 들어 다음 sqlcmd 명령은 포트 1435에서 수신기에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-485">For example, the following sqlcmd command connects to a listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="80143-486">SQLCMD 연결은 주 복제본을 호스트하는 SQL Server 인스턴스에 자동으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-486">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="80143-487">지정한 포트가 두 SQL Server의 방화벽에서 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-487">Make sure that the port you specify is open on the firewall of both SQL Servers.</span></span> <span data-ttu-id="80143-488">두 서버 모두 사용하는 TCP 포트에 대한 인바운드 규칙이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-488">Both servers require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="80143-489">자세한 내용은 [방화벽 규칙 추가 또는 편집](http://technet.microsoft.com/library/cc753558.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80143-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by the way” info, an Important is info users need to complete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is the second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note the format for documenting the UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult to maintain. Highlight areas you are referring to in red.*-->

<!--**No. of steps**: *Make sure the number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want to go on.*-->

## <a name="next-steps"></a><span data-ttu-id="80143-490">다음 단계</span><span class="sxs-lookup"><span data-stu-id="80143-490">Next steps</span></span>

- <span data-ttu-id="80143-491">[두 번째 가용성 그룹에 대한 부하 분산 장치에 IP 주소를 추가](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP)합니다.</span><span class="sxs-lookup"><span data-stu-id="80143-491">[Add an IP address to a load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
