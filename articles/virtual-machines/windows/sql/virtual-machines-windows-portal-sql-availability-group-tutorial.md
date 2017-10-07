---
title: "서버 가용성 그룹-Azure 가상 컴퓨터-자습서 aaaSQL | Microsoft Docs"
description: "이 자습서에서는 어떻게 toocreate는 SQL Server Always On 가용성 그룹에 Azure 가상 컴퓨터."
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
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="6be00-103">수동으로 Azure VM에서 Always On 가용성 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="6be00-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="6be00-104">이 자습서에서는 어떻게 toocreate는 SQL Server Always On 가용성 그룹에 Azure 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="6be00-104">This tutorial shows how toocreate a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="6be00-105">hello 전체 자습서는 두 명의 SQL Server에서 데이터베이스 복제본으로 가용성 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-105">hello complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="6be00-106">**예상 시간**: hello 전제 조건이 충족 되 면 약 30 분 toocomplete를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-106">**Time estimate**: Takes about 30 minutes toocomplete once hello prerequisites are met.</span></span>

<span data-ttu-id="6be00-107">hello 다이어그램 hello 자습서에서 빌드할 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-107">hello diagram illustrates what you build in hello tutorial.</span></span>

![가용성 그룹](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="6be00-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6be00-109">Prerequisites</span></span>

<span data-ttu-id="6be00-110">hello 자습서에서는 SQL Server Always On 가용성 그룹에 대 한 기본적인 이해 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-110">hello tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="6be00-111">자세한 내용은 [Always On 가용성 그룹 개요(SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6be00-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="6be00-112">hello 다음 표에이 자습서를 시작 하기 전에 toocomplete 해야 하는 hello 필수 구성 요소.</span><span class="sxs-lookup"><span data-stu-id="6be00-112">hello following table lists hello prerequisites that you need toocomplete before starting this tutorial:</span></span>

|  |<span data-ttu-id="6be00-113">요구 사항</span><span class="sxs-lookup"><span data-stu-id="6be00-113">Requirement</span></span> |<span data-ttu-id="6be00-114">설명</span><span class="sxs-lookup"><span data-stu-id="6be00-114">Description</span></span> |
|----- |----- |----- |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="6be00-116">SQL Server 2개</span><span class="sxs-lookup"><span data-stu-id="6be00-116">Two SQL Servers</span></span> | <span data-ttu-id="6be00-117">- Azure 가용성 집합에</span><span class="sxs-lookup"><span data-stu-id="6be00-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="6be00-118">- 단일 도메인에</span><span class="sxs-lookup"><span data-stu-id="6be00-118">- In a single domain</span></span> <br/> <span data-ttu-id="6be00-119">- 장애 조치(Failover) 클러스터링 기능(설치됨)</span><span class="sxs-lookup"><span data-stu-id="6be00-119">- With Failover Clustering feature installed</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="6be00-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="6be00-121">Windows Server</span></span> | <span data-ttu-id="6be00-122">클러스터 감시를 위한 파일 공유</span><span class="sxs-lookup"><span data-stu-id="6be00-122">File share for cluster witness</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="6be00-124">SQL Server 서비스 계정</span><span class="sxs-lookup"><span data-stu-id="6be00-124">SQL Server service account</span></span> | <span data-ttu-id="6be00-125">도메인 계정</span><span class="sxs-lookup"><span data-stu-id="6be00-125">Domain account</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="6be00-127">SQL Server 에이전트 서비스 계정</span><span class="sxs-lookup"><span data-stu-id="6be00-127">SQL Server Agent service account</span></span> | <span data-ttu-id="6be00-128">도메인 계정</span><span class="sxs-lookup"><span data-stu-id="6be00-128">Domain account</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="6be00-130">방화벽 포트 열기</span><span class="sxs-lookup"><span data-stu-id="6be00-130">Firewall ports open</span></span> | <span data-ttu-id="6be00-131">- SQL Server: 기본 인스턴스에 대해 **1433**</span><span class="sxs-lookup"><span data-stu-id="6be00-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="6be00-132">- 데이터베이스 미러링 끝점: **5022** 또는 사용 가능한 포트</span><span class="sxs-lookup"><span data-stu-id="6be00-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="6be00-133">- Azure Load Balancer 프로브: **59999** 또는 사용 가능한 포트</span><span class="sxs-lookup"><span data-stu-id="6be00-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="6be00-135">장애 조치(Failover) 클러스터링 기능 추가</span><span class="sxs-lookup"><span data-stu-id="6be00-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="6be00-136">이 기능을 필요로 하는 SQL Server 2개</span><span class="sxs-lookup"><span data-stu-id="6be00-136">Both SQL Servers require this feature</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="6be00-138">설치 도메인 계정</span><span class="sxs-lookup"><span data-stu-id="6be00-138">Installation domain account</span></span> | <span data-ttu-id="6be00-139">- 각 SQL Server의 로컬 관리자</span><span class="sxs-lookup"><span data-stu-id="6be00-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="6be00-140">- SQL Server의 각 인스턴스에 대해 SQL Server sysadmin 고정 서버 역할의 멤버</span><span class="sxs-lookup"><span data-stu-id="6be00-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="6be00-141">너무 필요한 hello 자습서를 시작 하기 전에[Azure 가상 컴퓨터의 Always On 가용성 그룹을 만들기 위한 사전 요구 사항을 완료](virtual-machines-windows-portal-sql-availability-group-prereq.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-141">Before you begin hello tutorial, you need too[Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="6be00-142">이러한 필수 구성이 요소는 이미 완료 되 면 이동할 수 있습니다 너무[클러스터 만들기](#CreateCluster)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-142">If these prerequisites are completed already, you can jump too[Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="6be00-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Hello 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="6be00-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create hello cluster</span></span>

<span data-ttu-id="6be00-144">필수 구성 요소를 완료 하는 hello, 후 hello 첫 번째 단계는 toocreate 두 SQL Sever 포함 된 Windows Server 장애 조치 클러스터와 미러링 모니터 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-144">After hello prerequisites are completed, hello first step is toocreate a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="6be00-145">RDP toohello SQL 서버와 미러링 모니터 서버 hello에 관리자가 있는 도메인 계정을 사용 하 여 첫 번째 SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6be00-145">RDP toohello first SQL Server using a domain account that is an administrator on both SQL Servers and hello witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="6be00-146">Hello를 따른 경우 [필수 사항 문서](virtual-machines-windows-portal-sql-availability-group-prereq.md)를 호출 하는 계정을 만든 **CORP\Install**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-146">If you followed hello [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="6be00-147">이 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-147">Use this account.</span></span>

2. <span data-ttu-id="6be00-148">Hello에 **서버 관리자** 대시보드에서 **도구**, 클릭 하 고 **장애 조치 클러스터 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-148">In hello **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="6be00-149">Hello 왼쪽된 창에서 마우스 오른쪽 단추로 클릭 **장애 조치 클러스터 관리자**, 클릭 하 고 **클러스터 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-149">In hello left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="6be00-150">![클러스터 만들기](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="6be00-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="6be00-151">클러스터 만들기 마법사 hello 하 다음 표에 hello에 hello 설정을 사용 하 여 hello 페이지를 단계별로 실행 하 여 1 노드 클러스터 만들기:</span><span class="sxs-lookup"><span data-stu-id="6be00-151">In hello Create Cluster Wizard, create a one-node cluster by stepping through hello pages with hello settings in hello following table:</span></span>

   | <span data-ttu-id="6be00-152">Page</span><span class="sxs-lookup"><span data-stu-id="6be00-152">Page</span></span> | <span data-ttu-id="6be00-153">설정</span><span class="sxs-lookup"><span data-stu-id="6be00-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="6be00-154">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="6be00-154">Before You Begin</span></span> |<span data-ttu-id="6be00-155">기본값 사용</span><span class="sxs-lookup"><span data-stu-id="6be00-155">Use defaults</span></span> |
   | <span data-ttu-id="6be00-156">서버 선택</span><span class="sxs-lookup"><span data-stu-id="6be00-156">Select Servers</span></span> |<span data-ttu-id="6be00-157">첫 번째 SQL Server의 이름을 지정 하는 형식 hello **서버 이름을 입력** 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-157">Type hello first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="6be00-158">유효성 검사 경고</span><span class="sxs-lookup"><span data-stu-id="6be00-158">Validation Warning</span></span> |<span data-ttu-id="6be00-159">선택 **아니요.가이 클러스터에 대 한 Microsoft의 지원이 필요 하지 않으며 따라서 toorun hello 유효성 검사를 원하지 않는 I를 테스트 합니다. 다음을 클릭 하면 hello 클러스터 만들기를 계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want toorun hello validation tests. When I click Next, continue Creating hello cluster**.</span></span> |
   | <span data-ttu-id="6be00-160">클러스터 관리 hello에 대 한 액세스 지점</span><span class="sxs-lookup"><span data-stu-id="6be00-160">Access Point for Administering hello Cluster</span></span> |<span data-ttu-id="6be00-161">클러스터 이름(예: **SQLAGCluster1**)을 **클러스터 이름**에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="6be00-162">다음</span><span class="sxs-lookup"><span data-stu-id="6be00-162">Confirmation</span></span> |<span data-ttu-id="6be00-163">저장소 공간을 사용하지 않는 경우 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="6be00-164">이 표 아래 hello 참고를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6be00-164">See hello note following this table.</span></span> |

### <a name="set-hello-cluster-ip-address"></a><span data-ttu-id="6be00-165">Hello 클러스터 IP 주소 설정</span><span class="sxs-lookup"><span data-stu-id="6be00-165">Set hello cluster IP address</span></span>

1. <span data-ttu-id="6be00-166">**장애 조치 클러스터 관리자**, 너무 아래로 스크롤하여**클러스터 코어 리소스** hello 클러스터 세부 정보를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-166">In **Failover Cluster Manager**, scroll down too**Cluster Core Resources** and expand hello cluster details.</span></span> <span data-ttu-id="6be00-167">두 hello 표시 되어야 **이름** 및 hello **IP 주소** hello의 리소스 **실패** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-167">You should see both hello **Name** and hello **IP Address** resources in hello **Failed** state.</span></span> <span data-ttu-id="6be00-168">hello IP 주소 리소스 상태로 만들 수 없습니다 온라인 hello 클러스터 hello 지정 되기 때문에 자체 hello 컴퓨터와 동일한 IP 주소를 사용 하므로 중복 된 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-168">hello IP address resource cannot be brought online because hello cluster is assigned hello same IP address as hello machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="6be00-169">마우스 오른쪽 단추로 클릭 hello 실패 **IP 주소** 리소스 및 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-169">Right-click hello failed **IP Address** resource, and then click **Properties**.</span></span>

   ![클러스터 속성](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="6be00-171">선택 **고정 IP 주소** 하 고 SQL Server hello hello 주소 텍스트 상자에는 서브넷에서 사용 가능한 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-171">Select **Static IP Address** and specify an available address from subnet where hello SQL Server is in hello Address text box.</span></span> <span data-ttu-id="6be00-172">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="6be00-173">Hello에 **클러스터 코어 리소스** 섹션 클러스터 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **온라인 상태로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-173">In hello **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="6be00-174">그런 다음 두 리소스가 모두 온라인 상태로 전환될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="6be00-175">Hello 클러스터 이름 리소스가 온라인 상태가 되 면 새 AD 컴퓨터 계정으로 hello DC 서버를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-175">When hello cluster name resource comes online, it updates hello DC server with a new AD computer account.</span></span> <span data-ttu-id="6be00-176">이 AD 계정 toorun hello 나중에 가용성 그룹 클러스터형 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-176">Use this AD account toorun hello Availability Group clustered service later.</span></span>

### <span data-ttu-id="6be00-177"><a name="addNode"></a>추가 다른 SQL Server toocluster hello</span><span class="sxs-lookup"><span data-stu-id="6be00-177"><a name="addNode"></a>Add hello other SQL Server toocluster</span></span>

<span data-ttu-id="6be00-178">추가 다른 SQL Server toohello 클러스터 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-178">Add hello other SQL Server toohello cluster.</span></span>

1. <span data-ttu-id="6be00-179">Hello 브라우저 트리에서 hello 클러스터를 마우스 오른쪽 단추로 클릭 하 고 클릭 **노드 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-179">In hello browser tree, right-click hello cluster and click **Add Node**.</span></span>

    ![노드 toohello 클러스터를 추가 합니다.](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="6be00-181">Hello에 **노드 추가 마법사**, 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-181">In hello **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="6be00-182">Hello에 **서버 선택** 페이지에서 추가할 두 번째 SQL Server hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-182">In hello **Select Servers** page, add hello second SQL Server.</span></span> <span data-ttu-id="6be00-183">형식 hello 서버 이름은 **서버 이름을 입력** 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-183">Type hello server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="6be00-184">완료하면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="6be00-185">Hello에 **유효성 검사 경고** 페이지 **아니요** (프로덕션 시나리오에 테스트를 수행 해야 hello 유효성 검사).</span><span class="sxs-lookup"><span data-stu-id="6be00-185">In hello **Validation Warning** page, click **No** (in a production scenario you should perform hello validation tests).</span></span> <span data-ttu-id="6be00-186">그런 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="6be00-187">Hello에 **확인** 페이지에서 저장소 공간을 일반 hello 확인란을 사용 하는 경우 **모든 적합 한 저장소 toohello 클러스터를 추가 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6be00-187">In hello **Confirmation** page if you are using Storage Spaces, clear hello checkbox labeled **Add all eligible storage toohello cluster.**</span></span>

   ![노드 확인 추가](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="6be00-189">저장소 공간을 사용 하는 경우 및 선택을 취소 하지 않으면 **모든 적합 한 저장소 toohello 클러스터 추가**, Windows hello 프로세스를 클러스터링 하는 동안 hello 가상 디스크를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage toohello cluster**, Windows detaches hello virtual disks during hello clustering process.</span></span> <span data-ttu-id="6be00-190">결과적으로, 이러한 hello 저장소 공간을 hello 클러스터에서 제거 될 때까지 디스크 관리자 또는 탐색기에 표시 되지 않습니다 및 PowerShell을 사용 하 여 다시 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-190">As a result, they do not appear in Disk Manager or Explorer until hello storage spaces are removed from hello cluster and reattached using PowerShell.</span></span> <span data-ttu-id="6be00-191">저장소 공간 toostorage 풀의 여러 디스크를 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-191">Storage Spaces groups multiple disks in toostorage pools.</span></span> <span data-ttu-id="6be00-192">자세한 내용은 [저장소 공간](https://technet.microsoft.com/library/hh831739)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6be00-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="6be00-193">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-193">Click **Next**.</span></span>

1. <span data-ttu-id="6be00-194">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-194">Click **Finish**.</span></span>

   <span data-ttu-id="6be00-195">장애 조치 클러스터 관리자에서는 클러스터에 새 노드가 고 hello에 나열 **노드** 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-195">Failover Cluster Manager shows that your cluster has a new node and lists it in hello **Nodes** container.</span></span>

10. <span data-ttu-id="6be00-196">로그 아웃 hello 원격 데스크톱 세션.</span><span class="sxs-lookup"><span data-stu-id="6be00-196">Log out of hello remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="6be00-197">클러스터 쿼럼 파일 공유 추가</span><span class="sxs-lookup"><span data-stu-id="6be00-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="6be00-198">이 예제에서는 hello Windows 클러스터 파일 공유 toocreate 클러스터 쿼럼을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-198">In this example hello Windows cluster uses a file share toocreate a cluster quorum.</span></span> <span data-ttu-id="6be00-199">이 자습서에서는 노드 및 파일 공유 과반수 쿼럼을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="6be00-200">자세한 내용은 [장애 조치(Failover) 클러스터의 쿼럼 구성 이해](http://technet.microsoft.com/library/cc731739.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6be00-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="6be00-201">원격 데스크톱 세션 toohello 파일 공유 미러링 모니터 멤버 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-201">Connect toohello file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="6be00-202">**서버 관리자**에서 **도구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="6be00-203">**컴퓨터 관리**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="6be00-204">**공유 폴더**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="6be00-205">**공유**를 마우스 오른쪽 단추로 클릭하고 **새 공유...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![새 공유](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="6be00-207">사용 하 여 **공유 폴더 만들기 마법사** toocreate를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-207">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="6be00-208">**폴더 경로**, 클릭 **찾아보기** 를 찾거나 hello 공유 폴더에 대 한 경로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-208">On **Folder Path**, click **Browse** and locate or create a path for hello shared folder.</span></span> <span data-ttu-id="6be00-209">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-209">Click **Next**.</span></span>

1. <span data-ttu-id="6be00-210">**이름, 설명 및 설정을** hello 공유 이름 및 경로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-210">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="6be00-211">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-211">Click **Next**.</span></span>

1. <span data-ttu-id="6be00-212">**공유 폴더 사용 권한**에서 **사용 권한 사용자 지정**을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="6be00-213">**사용자 지정...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="6be00-214">**사용 권한 사용자 지정**에서 **추가...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="6be00-215">해당 hello 사용 되는 계정 toocreate hello 클러스터에 모든 권한이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-215">Make sure that hello account used toocreate hello cluster has full control.</span></span>

   ![새 공유](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="6be00-217">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-217">Click **OK**.</span></span>

1. <span data-ttu-id="6be00-218">**공유 폴더 사용 권한**에서 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="6be00-219">**마침**을 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="6be00-220">로그 아웃 hello 서버</span><span class="sxs-lookup"><span data-stu-id="6be00-220">Log out of hello server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="6be00-221">클러스터 쿼럼 구성</span><span class="sxs-lookup"><span data-stu-id="6be00-221">Configure cluster quorum</span></span>

<span data-ttu-id="6be00-222">다음으로 hello 클러스터 쿼럼을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-222">Next, set hello cluster quorum.</span></span>

1. <span data-ttu-id="6be00-223">원격 데스크톱 toohello 첫 번째 클러스터 노드를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-223">Connect toohello first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="6be00-224">**장애 조치 클러스터 관리자**hello 클러스터를 마우스 오른쪽 단추로 너무 가리킨**기타 작업**를 클릭 하 고 **클러스터 쿼럼 설정 구성 중... **.</span><span class="sxs-lookup"><span data-stu-id="6be00-224">In **Failover Cluster Manager**, right-click hello cluster, point too**More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![새 공유](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="6be00-226">**클러스터 쿼럼 구성 마법사**에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="6be00-227">**쿼럼 구성 옵션 선택**, 선택 **hello 쿼럼 감시 선택**를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-227">In **Select Quorum Configuration Option**, choose **Select hello quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="6be00-228">**쿼럼 감시 선택**에서 **파일 공유 감시 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="6be00-229">Windows Server 2016은 클라우드 감시를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="6be00-230">이 유형의 감시를 선택한 경우 파일 공유 감시가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="6be00-231">자세한 내용은 [장애 조치(Failover) 클러스터에 대한 클라우드 감시 배포](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6be00-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="6be00-232">이 자습서에서는 이전 운영 체제에서 지원되는 파일 공유 감시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="6be00-233">**파일 공유 감시 구성**, 사용자가 만든 hello 공유에 대 한 hello 패스를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-233">On **Configure File Share Witness**, type hello path for hello share you created.</span></span> <span data-ttu-id="6be00-234">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-234">Click **Next**.</span></span>

1. <span data-ttu-id="6be00-235">Hello 설정을 확인 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-235">Verify hello settings on **Confirmation**.</span></span> <span data-ttu-id="6be00-236">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-236">Click **Next**.</span></span>

1. <span data-ttu-id="6be00-237">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-237">Click **Finish**.</span></span>

<span data-ttu-id="6be00-238">hello 클러스터 코어 리소스 파일 공유 감시 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-238">hello cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="6be00-239">가용성 그룹 사용</span><span class="sxs-lookup"><span data-stu-id="6be00-239">Enable Availability Groups</span></span>

<span data-ttu-id="6be00-240">다음으로 hello를 사용 하도록 설정 **AlwaysOn 가용성 그룹** 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-240">Next, enable hello **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="6be00-241">두 SQL Server에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="6be00-242">Hello에서 **시작** 화면을 시작 하며, **SQL Server 구성 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-242">From hello **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="6be00-243">Hello 브라우저 트리에서 클릭 **SQL Server 서비스**, hello를 마우스 오른쪽 단추로 클릭 **SQL Server (MSSQLSERVER)** 서비스 마우스 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-243">In hello browser tree, click **SQL Server Services**, then right-click hello **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="6be00-244">Hello 클릭 **AlwaysOn 고가용성** 탭 한 다음 선택 **AlwaysOn 가용성 그룹 사용**다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-244">Click hello **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![AlwaysOn 가용성 그룹 사용](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="6be00-246">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-246">Click **Apply**.</span></span> <span data-ttu-id="6be00-247">클릭 **확인** hello 팝업 대화 상자에서.</span><span class="sxs-lookup"><span data-stu-id="6be00-247">Click **OK** in hello pop-up dialog.</span></span>

5. <span data-ttu-id="6be00-248">Hello SQL Server 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-248">Restart hello SQL Server service.</span></span>

<span data-ttu-id="6be00-249">다른 SQL Server hello에서 이러한 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-249">Repeat these steps on hello other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a><span data-ttu-id="6be00-250">Hello에 데이터베이스를 만드는 첫 번째 SQL Server</span><span class="sxs-lookup"><span data-stu-id="6be00-250">Create a database on hello first SQL Server</span></span>

1. <span data-ttu-id="6be00-251">시작 hello RDP 파일 toohello 도메인이 포함 된 첫 번째 SQL Server 계정 즉 sysadmin 소속 고정 서버 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-251">Launch hello RDP file toohello first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="6be00-252">SQL Server Management Studio를 열고 연결 toohello 첫 번째 SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6be00-252">Open SQL Server Management Studio and connect toohello first SQL Server.</span></span>
7. <span data-ttu-id="6be00-253">**개체 탐색기**에서 **데이터베이스**를 마우스 오른쪽 단추로 클릭하고 **새 데이터베이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="6be00-254">**데이터베이스 이름**에 **MyDB1**을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="6be00-255"><a name="backupshare"></a> 백업 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="6be00-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="6be00-256">첫 번째 SQL Server에 hello **서버 관리자**, 클릭 **도구**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-256">On hello first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="6be00-257">**컴퓨터 관리**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="6be00-258">**공유 폴더**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="6be00-259">**공유**를 마우스 오른쪽 단추로 클릭하고 **새 공유...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![새 공유](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="6be00-261">사용 하 여 **공유 폴더 만들기 마법사** toocreate를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-261">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="6be00-262">**폴더 경로**, 클릭 **찾아보기** 를 찾거나 hello 데이터베이스 백업 공유 폴더에 대 한 경로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-262">On **Folder Path**, click **Browse** and locate or create a path for hello database backup shared folder.</span></span> <span data-ttu-id="6be00-263">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-263">Click **Next**.</span></span>

1. <span data-ttu-id="6be00-264">**이름, 설명 및 설정을** hello 공유 이름 및 경로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-264">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="6be00-265">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-265">Click **Next**.</span></span>

1. <span data-ttu-id="6be00-266">**공유 폴더 사용 권한**에서 **사용 권한 사용자 지정**을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="6be00-267">**사용자 지정...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="6be00-268">**사용 권한 사용자 지정**에서 **추가...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="6be00-269">두 서버 모두에 대 한 hello SQL Server 및 SQL Server 에이전트 서비스 계정에 모든 권한이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-269">Make sure that hello SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![새 공유](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="6be00-271">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-271">Click **OK**.</span></span>

1. <span data-ttu-id="6be00-272">**공유 폴더 사용 권한**에서 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="6be00-273">**마침**을 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-hello-database"></a><span data-ttu-id="6be00-274">전체 hello 데이터베이스의 백업을 수행합니다</span><span class="sxs-lookup"><span data-stu-id="6be00-274">Take a full backup of hello database</span></span>

<span data-ttu-id="6be00-275">Hello 새 데이터베이스 tooinitialize hello 로그 체인을 tooback이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-275">You need tooback up hello new database tooinitialize hello log chain.</span></span> <span data-ttu-id="6be00-276">Hello 새 데이터베이스의 백업을 더 이상 수행 하지 않으면 가용성 그룹에 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-276">If you do not take a backup of hello new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="6be00-277">**개체 탐색기**hello 데이터베이스를 마우스 오른쪽 단추로 너무 가리킨**작업 중... **, 클릭 **백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-277">In **Object Explorer**, right-click hello database, point too**Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="6be00-278">클릭 **확인** tootake 전체 백업 toohello 기본 백업 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-278">Click **OK** tootake a full backup toohello default backup location.</span></span>

## <a name="create-hello-availability-group"></a><span data-ttu-id="6be00-279">Hello 가용성 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="6be00-279">Create hello Availability Group</span></span>
<span data-ttu-id="6be00-280">사용자는 이제 준비 tooconfigure 단계를 수행 하는 hello를 사용 하 여 가용성 그룹:</span><span class="sxs-lookup"><span data-stu-id="6be00-280">You are now ready tooconfigure an Availability Group using hello following steps:</span></span>

* <span data-ttu-id="6be00-281">Hello에 데이터베이스를 만드는 첫 번째 SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6be00-281">Create a database on hello first SQL Server.</span></span>
* <span data-ttu-id="6be00-282">전체 백업과 hello 데이터베이스의 트랜잭션 로그 백업을 모두</span><span class="sxs-lookup"><span data-stu-id="6be00-282">Take both a full backup and a transaction log backup of hello database</span></span>
* <span data-ttu-id="6be00-283">전체 복원 hello 및 hello로 SQL Server의 두 번째 로그 백업이 toohello **NORECOVERY** 옵션</span><span class="sxs-lookup"><span data-stu-id="6be00-283">Restore hello full and log backups toohello second SQL Server with hello **NORECOVERY** option</span></span>
* <span data-ttu-id="6be00-284">Hello 가용성 그룹 만들기 (**AG1**) 읽기 가능한 보조 복제본, 동기 커밋 및 자동 장애 조치와</span><span class="sxs-lookup"><span data-stu-id="6be00-284">Create hello Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-hello-availability-group"></a><span data-ttu-id="6be00-285">Hello 가용성 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-285">Create hello Availability Group:</span></span>

1. <span data-ttu-id="6be00-286">원격 데스크톱 세션 toohello에서 첫 번째 SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6be00-286">On remote desktop session toohello first SQL Server.</span></span> <span data-ttu-id="6be00-287">SSMS의 **개체 탐색기**에서 **AlwaysOn 고가용성**을 마우스 오른쪽 단추로 클릭하고 **새 가용성 그룹 마법사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![새 가용성 그룹 마법사 시작](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="6be00-289">Hello에 **소개** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-289">In hello **Introduction** page, click **Next**.</span></span> <span data-ttu-id="6be00-290">Hello에 **가용성 그룹 이름 지정** 페이지에서, 예를 들어 hello 가용성 그룹에 대 한 이름을 입력 **AG1**에 **가용성 그룹 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-290">In hello **Specify Availability Group Name** page, type a name for hello Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="6be00-291">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-291">Click **Next**.</span></span>

    ![새 AG 마법사, AG 이름 지정](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="6be00-293">Hello에 **데이터베이스 선택** 페이지 데이터베이스를 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-293">In hello **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="6be00-294">hello 의도 된 주 복제본에서 최소한 하나의 전체 백업을 수행 했으므로 hello 데이터베이스가 가용성 그룹에 대 한 hello 필수 구성 요소를 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-294">hello database meets hello prerequisites for an Availability Group because you have taken at least one full backup on hello intended primary replica.</span></span>

   ![새 AG 마법사, 데이터베이스 선택](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="6be00-296">Hello에 **복제본 지정** 페이지 **Add Replica**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-296">In hello **Specify Replicas** page, click **Add Replica**.</span></span>

   ![새 AG 마법사, 복제본 지정](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="6be00-298">hello **tooServer 연결** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-298">hello **Connect tooServer** dialog pops up.</span></span> <span data-ttu-id="6be00-299">두 번째 서버 hello 형식 hello 이름 **서버 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-299">Type hello name of hello second server in **Server name**.</span></span> <span data-ttu-id="6be00-300">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-300">Click **Connect**.</span></span>

   <span data-ttu-id="6be00-301">Hello에 다시 **복제본 지정** 페이지에서 이제 표시 hello 두 번째 서버에 나열 된 **가용성 복제본**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-301">Back in hello **Specify Replicas** page, you should now see hello second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="6be00-302">다음과 같이 hello 복제본을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-302">Configure hello replicas as follows.</span></span>

   ![새 AG 마법사, 복제본 지정(전체)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="6be00-304">클릭 **끝점** toosee hello 데이터베이스 미러링 끝점이이 가용성 그룹에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-304">Click **Endpoints** toosee hello database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="6be00-305">사용 하 여 hello hello을 설정할 때 사용 하는 동일한 포트 [데이터베이스 미러링 끝점에 대 한 방화벽 규칙](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-305">Use hello same port that you used when you set hello [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![새 AG 마법사, 초기 데이터 동기화 선택](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="6be00-307">Hello에 **초기 데이터 동기화 선택** 페이지 **전체** 공유 네트워크 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-307">In hello **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="6be00-308">Hello 위치에 대 한 hello를 사용 하 여 [만든 백업 공유](#backupshare)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-308">For hello location, use hello [backup share that you created](#backupshare).</span></span> <span data-ttu-id="6be00-309">에 있는 경우 hello 예에서 **\\\\\<첫 번째 SQL Server\>\Backup\**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-309">In hello example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="6be00-310">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="6be00-311">SQL Server의 첫 번째 인스턴스에 hello hello 데이터베이스의 전체 백업을 수행 하 고 toohello 두 번째 인스턴스를 복원 하는 전체 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-311">Full synchronization takes a full backup of hello database on hello first instance of SQL Server and restores it toohello second instance.</span></span> <span data-ttu-id="6be00-312">대형 데이터베이스의 경우 전체 동기화는 시간이 오래 걸릴 수 있으므로 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="6be00-313">수동으로 hello 데이터베이스의 백업을 수행 하 고 사용 하 여 복원 하 여이 시간을 줄일 수 `NO RECOVERY`합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-313">You can reduce this time by manually taking a backup of hello database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="6be00-314">Hello 데이터베이스를 복원 하는 경우 `NO RECOVERY` hello hello 가용성 그룹을 구성 하기 전에 SQL Server의 두 번째, 선택 **조인만**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-314">If hello database is already restored with `NO RECOVERY` on hello second SQL Server before configuring hello Availability Group, choose **Join only**.</span></span> <span data-ttu-id="6be00-315">Hello 가용성 그룹을 구성한 후 tootake hello 백업 하려는 경우 선택 **초기 데이터 동기화 건너뛰기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-315">If you want tootake hello backup after configuring hello Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![새 AG 마법사, 초기 데이터 동기화 선택](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="6be00-317">Hello에 **유효성 검사** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-317">In hello **Validation** page, click **Next**.</span></span> <span data-ttu-id="6be00-318">이 페이지에는 다음 이미지와 비슷한 toohello 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-318">This page should look similar toohello following image:</span></span>

    ![새 AG 마법사, 유효성 검사](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="6be00-320">가용성 그룹 수신기를 구성 하지 않았기 때문에는 hello 수신기 구성에 대 한 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-320">There is a warning for hello listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="6be00-321">Azure 가상 컴퓨터에 수신기를 만들면 hello hello Azure 부하 분산 장치를 만든 후 때문에이 경고를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-321">You can ignore this warning because on Azure virtual machines you create hello listener after creating hello Azure load balancer.</span></span>

10. <span data-ttu-id="6be00-322">Hello에 **요약** 페이지 **마침**, 다음 hello 마법사를 구성 하는 동안 잠시 기다려 hello 새 가용성 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-322">In hello **Summary** page, click **Finish**, then wait while hello wizard configures hello new Availability Group.</span></span> <span data-ttu-id="6be00-323">Hello에 **진행률** 페이지에서 클릭할 수 있는 **자세한 내용을 보려면** tooview hello 진행 상황을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-323">In hello **Progress** page, you can click **More details** tooview hello detailed progress.</span></span> <span data-ttu-id="6be00-324">Hello 마법사가 완료 되 면 hello 검사 **결과** 가용성 그룹을 hello 페이지 tooverify 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-324">Once hello wizard is finished, inspect hello **Results** page tooverify that hello Availability Group is successfully created.</span></span>

     ![새 AG 마법사, 결과](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="6be00-326">클릭 **닫기** tooexit hello 마법사.</span><span class="sxs-lookup"><span data-stu-id="6be00-326">Click **Close** tooexit hello wizard.</span></span>

### <a name="check-hello-availability-group"></a><span data-ttu-id="6be00-327">가용성 그룹 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-327">Check hello Availability Group</span></span>

1. <span data-ttu-id="6be00-328">**개체 탐색기**에서 **AlwaysOn 고가용성**을 확장하고 **가용성 그룹**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="6be00-329">이제이 컨테이너에 새 가용성 그룹을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-329">You should now see hello new Availability Group in this container.</span></span> <span data-ttu-id="6be00-330">Hello 가용성 그룹을 마우스 오른쪽 단추로 클릭 하 고 클릭 **대시보드 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-330">Right-click hello Availability Group and click **Show Dashboard**.</span></span>

   ![AG 대시보드 표시](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="6be00-332">프로그램 **AlwaysOn 대시보드** 비슷한 toothis 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-332">Your **AlwaysOn Dashboard** should look similar toothis.</span></span>

   ![AG 대시보드](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="6be00-334">Hello 복제본, 각 복제본과 hello 동기화 상태의 hello 장애 조치 모드를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-334">You can see hello replicas, hello failover mode of each replica and hello synchronization state.</span></span>

2. <span data-ttu-id="6be00-335">**장애 조치(Failover) 클러스터 관리자**에서 클러스터를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="6be00-336">**역할**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-336">Select **Roles**.</span></span> <span data-ttu-id="6be00-337">hello 가용성 그룹 이름을 사용 하는 hello 클러스터에서 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-337">hello Availability Group name you used is a role on hello cluster.</span></span> <span data-ttu-id="6be00-338">수신기를 구성하지 않았기 때문에 해당 가용성 그룹은 클라이언트 연결에 대한 IP 주소가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="6be00-339">Azure 부하 분산 장치를 만든 후에 hello 수신기를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-339">You will configure hello listener after you create an Azure load balancer.</span></span>

   ![장애 조치(Failover) 클러스터 관리자에서 AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="6be00-341">Hello 장애 조치 클러스터 관리자에서에서 hello 가용성 그룹을 통해 toofail를 시도 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-341">Do not try toofail over hello Availability Group from hello Failover Cluster Manager.</span></span> <span data-ttu-id="6be00-342">모든 장애 조치(Failover) 작업은 SSMS의 **AlwaysOn 대시보드** 에서 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="6be00-343">자세한 내용은 참조 [사용에 대 한 제한에는 가용성 그룹 장애 조치 클러스터 관리자 hello](https://msdn.microsoft.com/library/ff929171.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-343">For more information, see [Restrictions on Using hello Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="6be00-344">이 시점에서 SQL Server의 두 인스턴스에서 복제와 함께 가용성 그룹을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="6be00-345">인스턴스 간에 hello 가용성 그룹을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-345">You can move hello Availability Group between instances.</span></span> <span data-ttu-id="6be00-346">수신기 없기 때문에 아직 toohello 가용성 그룹을 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-346">You cannot connect toohello Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="6be00-347">Azure 가상 컴퓨터의 hello 수신기 부하 분산 장치에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-347">In Azure virtual machines, hello listener requires a load balancer.</span></span> <span data-ttu-id="6be00-348">hello 다음 단계는 Azure의 hello 부하 분산 장치 toocreate입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-348">hello next step is toocreate hello load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="6be00-349">Azure Load Balancer 만들기</span><span class="sxs-lookup"><span data-stu-id="6be00-349">Create an Azure load balancer</span></span>

<span data-ttu-id="6be00-350">Azure Virtual Machines에서 SQL Server 가용성 그룹에는 부하 분산 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="6be00-351">hello 부하 분산 장치는 hello 가용성 그룹 수신기에 대 한 hello IP 주소를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-351">hello load balancer holds hello IP address for hello Availability Group listener.</span></span> <span data-ttu-id="6be00-352">이 섹션에서는 toocreate hello 부하 분산 장치 hello Azure 포털에서에서 하는 방법을 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-352">This section summarizes how toocreate hello load balancer in hello Azure portal.</span></span>

1. <span data-ttu-id="6be00-353">Azure 포털 hello, 여기에서 SQL Server는 고 클릭 toohello 리소스 그룹 이동 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-353">In hello Azure portal, go toohello resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="6be00-354">**부하 분산 장치**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="6be00-355">Microsoft에서 게시 하는 hello 부하 분산 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-355">Choose hello load balancer published by Microsoft.</span></span>

   ![장애 조치(Failover) 클러스터 관리자에서 AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="6be00-357">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-357">Click **Create**.</span></span>
3. <span data-ttu-id="6be00-358">Hello 부하 분산 장치에 대 한 매개 변수 뒤 hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-358">Configure hello following parameters for hello load balancer.</span></span>

   | <span data-ttu-id="6be00-359">설정</span><span class="sxs-lookup"><span data-stu-id="6be00-359">Setting</span></span> | <span data-ttu-id="6be00-360">필드</span><span class="sxs-lookup"><span data-stu-id="6be00-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="6be00-361">**Name**</span><span class="sxs-lookup"><span data-stu-id="6be00-361">**Name**</span></span> |<span data-ttu-id="6be00-362">예를 들어 hello 부하 분산 장치에 대 한 텍스트 이름을 사용 하 여 **sqlLB**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-362">Use a text name for hello load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="6be00-363">**형식**</span><span class="sxs-lookup"><span data-stu-id="6be00-363">**Type**</span></span> |<span data-ttu-id="6be00-364">내부</span><span class="sxs-lookup"><span data-stu-id="6be00-364">Internal</span></span> |
   | <span data-ttu-id="6be00-365">**가상 네트워크**</span><span class="sxs-lookup"><span data-stu-id="6be00-365">**Virtual network**</span></span> |<span data-ttu-id="6be00-366">Hello hello Azure 가상 네트워크 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-366">Use hello name of hello Azure virtual network.</span></span> |
   | <span data-ttu-id="6be00-367">**서브넷**</span><span class="sxs-lookup"><span data-stu-id="6be00-367">**Subnet**</span></span> |<span data-ttu-id="6be00-368">가상 컴퓨터를 hello hello 서브넷의 사용 하 여 hello 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-368">Use hello name of hello subnet that hello virtual machine is in.</span></span>  |
   | <span data-ttu-id="6be00-369">**IP 주소 할당**</span><span class="sxs-lookup"><span data-stu-id="6be00-369">**IP address assignment**</span></span> |<span data-ttu-id="6be00-370">정적</span><span class="sxs-lookup"><span data-stu-id="6be00-370">Static</span></span> |
   | <span data-ttu-id="6be00-371">**IP 주소**</span><span class="sxs-lookup"><span data-stu-id="6be00-371">**IP address**</span></span> |<span data-ttu-id="6be00-372">서브넷에서 사용 가능한 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="6be00-373">**구독**</span><span class="sxs-lookup"><span data-stu-id="6be00-373">**Subscription**</span></span> |<span data-ttu-id="6be00-374">사용 하 여 hello 동일 hello 가상 컴퓨터로 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-374">Use hello same subscription as hello virtual machine.</span></span> |
   | <span data-ttu-id="6be00-375">**위치**:</span><span class="sxs-lookup"><span data-stu-id="6be00-375">**Location**</span></span> |<span data-ttu-id="6be00-376">사용 하 여 hello 동일 hello 가상 컴퓨터로 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-376">Use hello same location as hello virtual machine.</span></span> |

   <span data-ttu-id="6be00-377">Azure 포털 블레이드 hello 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-377">hello Azure portal blade should look like this:</span></span>

   ![부하 분산 장치 만들기](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="6be00-379">클릭 **만들기**, toocreate hello에 대 한 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-379">Click **Create**, toocreate hello load balancer.</span></span>

<span data-ttu-id="6be00-380">tooconfigure hello 부하 분산 장치 백 엔드 풀 toocreate, probe, 및 집합 hello 부하 분산 규칙 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-380">tooconfigure hello load balancer, you need toocreate a backend pool, a probe, and set hello load balancing rules.</span></span> <span data-ttu-id="6be00-381">Hello Azure 포털에서에서이 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-381">Do these in hello Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="6be00-382">백 엔드 풀 추가</span><span class="sxs-lookup"><span data-stu-id="6be00-382">Add backend pool</span></span>

1. <span data-ttu-id="6be00-383">Azure 포털 hello tooyour 가용성 그룹을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-383">In hello Azure portal, go tooyour availability group.</span></span> <span data-ttu-id="6be00-384">Toorefresh hello 보기 toosee hello 새로 만든 부하 분산 장치를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-384">You might need toorefresh hello view toosee hello newly created load balancer.</span></span>

   ![리소스 그룹의 부하 분산 장치 찾기](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="6be00-386">Hello 부하 분산 장치를 클릭 하 고 **백 엔드 풀**를 클릭 하 고 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-386">Click hello load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="6be00-387">Hello 백 엔드 풀을 다음과 같이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-387">Set hello backend pool as follows:</span></span>

   | <span data-ttu-id="6be00-388">설정</span><span class="sxs-lookup"><span data-stu-id="6be00-388">Setting</span></span> | <span data-ttu-id="6be00-389">설명</span><span class="sxs-lookup"><span data-stu-id="6be00-389">Description</span></span> | <span data-ttu-id="6be00-390">예제</span><span class="sxs-lookup"><span data-stu-id="6be00-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="6be00-391">**Name**</span><span class="sxs-lookup"><span data-stu-id="6be00-391">**Name**</span></span> | <span data-ttu-id="6be00-392">텍스트 이름 입력</span><span class="sxs-lookup"><span data-stu-id="6be00-392">Type a text name</span></span> | <span data-ttu-id="6be00-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="6be00-393">SQLLBBE</span></span>
   | <span data-ttu-id="6be00-394">**연결 대상**</span><span class="sxs-lookup"><span data-stu-id="6be00-394">**Associated to**</span></span> | <span data-ttu-id="6be00-395">목록에서 선택</span><span class="sxs-lookup"><span data-stu-id="6be00-395">Pick from list</span></span> | <span data-ttu-id="6be00-396">가용성 집합</span><span class="sxs-lookup"><span data-stu-id="6be00-396">Availability set</span></span>
   | <span data-ttu-id="6be00-397">**가용성 집합**</span><span class="sxs-lookup"><span data-stu-id="6be00-397">**Availability set**</span></span> | <span data-ttu-id="6be00-398">SQL Server Vm에 있는 hello 가용성 집합의 이름을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6be00-398">Use a name of hello availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="6be00-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="6be00-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="6be00-400">**가상 컴퓨터**</span><span class="sxs-lookup"><span data-stu-id="6be00-400">**Virtual machines**</span></span> |<span data-ttu-id="6be00-401">두 hello Azure SQL Server VM 이름</span><span class="sxs-lookup"><span data-stu-id="6be00-401">hello two Azure SQL Server VM names</span></span> | <span data-ttu-id="6be00-402">sqlserver-0, sqlserver-1</span><span class="sxs-lookup"><span data-stu-id="6be00-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="6be00-403">Hello 백 엔드 풀에 대 한 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-403">Type hello name for hello back end pool.</span></span>

1. <span data-ttu-id="6be00-404">**+가상 컴퓨터 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="6be00-405">Hello 가용성 집합에 대 한 hello 가용성 집합에 SQL Server의 해당 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-405">For hello availability set, choose hello availability set that hello SQL Servers are in.</span></span>

1. <span data-ttu-id="6be00-406">가상 컴퓨터에 대 한 hello SQL 서버를 둘 다를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-406">For virtual machines, include both of hello SQL Servers.</span></span> <span data-ttu-id="6be00-407">Hello 파일 공유 미러링 모니터 서버를 포함 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="6be00-407">Do not include hello file share witness server.</span></span>

1. <span data-ttu-id="6be00-408">클릭 **확인** toocreate hello 백 엔드 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-408">Click **OK** toocreate hello backend pool.</span></span>

### <a name="set-hello-probe"></a><span data-ttu-id="6be00-409">집합 hello 프로브</span><span class="sxs-lookup"><span data-stu-id="6be00-409">Set hello probe</span></span>

1. <span data-ttu-id="6be00-410">Hello 부하 분산 장치를 클릭 하 고 **상태 프로브**를 클릭 하 고 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-410">Click hello load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="6be00-411">다음과 같이 hello 상태 프로브를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-411">Set hello health probe as follows:</span></span>

   | <span data-ttu-id="6be00-412">설정</span><span class="sxs-lookup"><span data-stu-id="6be00-412">Setting</span></span> | <span data-ttu-id="6be00-413">설명</span><span class="sxs-lookup"><span data-stu-id="6be00-413">Description</span></span> | <span data-ttu-id="6be00-414">예제</span><span class="sxs-lookup"><span data-stu-id="6be00-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="6be00-415">**Name**</span><span class="sxs-lookup"><span data-stu-id="6be00-415">**Name**</span></span> | <span data-ttu-id="6be00-416">텍스트</span><span class="sxs-lookup"><span data-stu-id="6be00-416">Text</span></span> | <span data-ttu-id="6be00-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="6be00-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="6be00-418">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="6be00-418">**Protocol**</span></span> | <span data-ttu-id="6be00-419">TCP 선택</span><span class="sxs-lookup"><span data-stu-id="6be00-419">Choose TCP</span></span> | <span data-ttu-id="6be00-420">TCP</span><span class="sxs-lookup"><span data-stu-id="6be00-420">TCP</span></span> |
   | <span data-ttu-id="6be00-421">**포트**</span><span class="sxs-lookup"><span data-stu-id="6be00-421">**Port**</span></span> | <span data-ttu-id="6be00-422">사용하지 않는 모든 포트</span><span class="sxs-lookup"><span data-stu-id="6be00-422">Any unused port</span></span> | <span data-ttu-id="6be00-423">59999</span><span class="sxs-lookup"><span data-stu-id="6be00-423">59999</span></span> |
   | <span data-ttu-id="6be00-424">**간격**</span><span class="sxs-lookup"><span data-stu-id="6be00-424">**Interval**</span></span>  | <span data-ttu-id="6be00-425">hello 프로브 시간 간격 (초) 시도</span><span class="sxs-lookup"><span data-stu-id="6be00-425">hello amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="6be00-426">5</span><span class="sxs-lookup"><span data-stu-id="6be00-426">5</span></span> |
   | <span data-ttu-id="6be00-427">**비정상 임계값**</span><span class="sxs-lookup"><span data-stu-id="6be00-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="6be00-428">hello에 대 한 비정상으로 간주 하는 가상 컴퓨터 toobe 발생 해야 하는 연속 프로브 오류 수</span><span class="sxs-lookup"><span data-stu-id="6be00-428">hello number of consecutive probe failures that must occur for a virtual machine toobe considered unhealthy</span></span>  | <span data-ttu-id="6be00-429">2</span><span class="sxs-lookup"><span data-stu-id="6be00-429">2</span></span> |

1. <span data-ttu-id="6be00-430">클릭 **확인** tooset hello 상태 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-430">Click **OK** tooset hello health probe.</span></span>

### <a name="set-hello-load-balancing-rules"></a><span data-ttu-id="6be00-431">Hello 부하 분산 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="6be00-431">Set hello load balancing rules</span></span>

1. <span data-ttu-id="6be00-432">Hello 부하 분산 장치를 클릭 하 고 **부하 분산 규칙**를 클릭 하 고 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-432">Click hello load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="6be00-433">Hello 부하 분산 규칙을 다음과 같이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-433">Set hello load balancing rules as follows.</span></span>
   | <span data-ttu-id="6be00-434">설정</span><span class="sxs-lookup"><span data-stu-id="6be00-434">Setting</span></span> | <span data-ttu-id="6be00-435">설명</span><span class="sxs-lookup"><span data-stu-id="6be00-435">Description</span></span> | <span data-ttu-id="6be00-436">예제</span><span class="sxs-lookup"><span data-stu-id="6be00-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="6be00-437">**Name**</span><span class="sxs-lookup"><span data-stu-id="6be00-437">**Name**</span></span> | <span data-ttu-id="6be00-438">텍스트</span><span class="sxs-lookup"><span data-stu-id="6be00-438">Text</span></span> | <span data-ttu-id="6be00-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="6be00-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="6be00-440">**프런트 엔드 IP 주소**</span><span class="sxs-lookup"><span data-stu-id="6be00-440">**Frontend IP address**</span></span> | <span data-ttu-id="6be00-441">주소 선택</span><span class="sxs-lookup"><span data-stu-id="6be00-441">Choose an address</span></span> |<span data-ttu-id="6be00-442">Hello 부하 분산 장치를 만들 때 만들어지는 hello 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-442">Use hello address that you created when you created hello load balancer.</span></span> |
   | <span data-ttu-id="6be00-443">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="6be00-443">**Protocol**</span></span> | <span data-ttu-id="6be00-444">TCP 선택</span><span class="sxs-lookup"><span data-stu-id="6be00-444">Choose TCP</span></span> |<span data-ttu-id="6be00-445">TCP</span><span class="sxs-lookup"><span data-stu-id="6be00-445">TCP</span></span> |
   | <span data-ttu-id="6be00-446">**포트**</span><span class="sxs-lookup"><span data-stu-id="6be00-446">**Port**</span></span> | <span data-ttu-id="6be00-447">SQL Server 인스턴스에 hello hello 포트 사용</span><span class="sxs-lookup"><span data-stu-id="6be00-447">Use hello port for hello SQL Server instance</span></span> | <span data-ttu-id="6be00-448">1433</span><span class="sxs-lookup"><span data-stu-id="6be00-448">1433</span></span> |
   | <span data-ttu-id="6be00-449">**백 엔드 포트**</span><span class="sxs-lookup"><span data-stu-id="6be00-449">**Backend Port**</span></span> | <span data-ttu-id="6be00-450">이 필드는 부동 IP가 직접 서버 반환에 대해 설정된 경우 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="6be00-451">1433</span><span class="sxs-lookup"><span data-stu-id="6be00-451">1433</span></span> |
   | <span data-ttu-id="6be00-452">**프로브**</span><span class="sxs-lookup"><span data-stu-id="6be00-452">**Probe**</span></span> |<span data-ttu-id="6be00-453">hello 프로브에 대해 지정한 hello 이름</span><span class="sxs-lookup"><span data-stu-id="6be00-453">hello name you specified for hello probe</span></span> | <span data-ttu-id="6be00-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="6be00-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="6be00-455">**세션 지속성**</span><span class="sxs-lookup"><span data-stu-id="6be00-455">**Session Persistence**</span></span> | <span data-ttu-id="6be00-456">드롭다운 목록</span><span class="sxs-lookup"><span data-stu-id="6be00-456">Drop down list</span></span> | <span data-ttu-id="6be00-457">**없음**</span><span class="sxs-lookup"><span data-stu-id="6be00-457">**None**</span></span> |
   | <span data-ttu-id="6be00-458">**유휴 시간 제한**</span><span class="sxs-lookup"><span data-stu-id="6be00-458">**Idle Timeout**</span></span> | <span data-ttu-id="6be00-459">분 tookeep TCP 연결을 열 수</span><span class="sxs-lookup"><span data-stu-id="6be00-459">Minutes tookeep a TCP connection open</span></span> | <span data-ttu-id="6be00-460">4</span><span class="sxs-lookup"><span data-stu-id="6be00-460">4</span></span> |
   | <span data-ttu-id="6be00-461">**부동 IP(Direct Server Return)**</span><span class="sxs-lookup"><span data-stu-id="6be00-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="6be00-462">사용</span><span class="sxs-lookup"><span data-stu-id="6be00-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="6be00-463">직접 서버 반환은 만드는 동안 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-463">Direct server return is set during creation.</span></span> <span data-ttu-id="6be00-464">이는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-464">It cannot be changed.</span></span>

1. <span data-ttu-id="6be00-465">클릭 **확인** tooset hello 부하 분산 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-465">Click **OK** tooset hello load balancing rules.</span></span>

## <span data-ttu-id="6be00-466"><a name="configure-listener"></a>Hello 수신기 구성</span><span class="sxs-lookup"><span data-stu-id="6be00-466"><a name="configure-listener"></a> Configure hello listener</span></span>

<span data-ttu-id="6be00-467">다음 일 toodo hello tooconfigure hello 장애 조치 클러스터에 가용성 그룹 수신기입니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-467">hello next thing toodo is tooconfigure an Availability Group listener on hello failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="6be00-468">이 자습서에서는 하나의 ILB IP와 함께 단일 수신기-toocreate 해결 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-468">This tutorial shows how toocreate a single listener - with one ILB IP address.</span></span> <span data-ttu-id="6be00-469">하나 이상의 IP 주소를 사용 하 여 하나 이상의 수신기 참조 toocreate [Create Availability Group listener 및 부하 분산 장치 | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-469">toocreate one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="6be00-470">수신기 포트 설정</span><span class="sxs-lookup"><span data-stu-id="6be00-470">Set listener port</span></span>

<span data-ttu-id="6be00-471">SQL Server Management Studio에서 hello 수신기 포트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-471">In SQL Server Management Studio, set hello listener port.</span></span>

1. <span data-ttu-id="6be00-472">SQL Server Management Studio를 시작 하 고 toohello 주 복제본에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-472">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="6be00-473">너무 이동**AlwaysOn 고가용성** | **가용성 그룹** | **가용성 그룹 수신기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-473">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="6be00-474">이제 장애 조치 클러스터 관리자에서 만든 hello 수신기 이름이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-474">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="6be00-475">Hello 수신기 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-475">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="6be00-476">Hello에 **포트** 상자 이전 사용 $EndpointPort hello를 사용 하 여 hello 가용성 그룹 수신기에 대 한 hello 포트 번호를 지정 합니다 (1433 hello이 기본값 이었습니다)를 클릭 한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-476">In hello **Port** box, specify hello port number for hello Availability Group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

<span data-ttu-id="6be00-477">이제 Resource Manager 모드에서 실행 중인 Azure Virtual Machines의 SQL Server 가용성 그룹이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-toolistener"></a><span data-ttu-id="6be00-478">테스트 연결 toolistener</span><span class="sxs-lookup"><span data-stu-id="6be00-478">Test connection toolistener</span></span>

<span data-ttu-id="6be00-479">tootest hello 연결:</span><span class="sxs-lookup"><span data-stu-id="6be00-479">tootest hello connection:</span></span>

1. <span data-ttu-id="6be00-480">RDP tooa SQL 서버 hello에 있는 동일한 가상 네트워크 구성 요소, 않도록 지정 되었으나 자체 hello 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-480">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="6be00-481">사용할 수 있습니다 hello hello 클러스터의 다른 SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6be00-481">You can use hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="6be00-482">사용 하 여 **sqlcmd** 유틸리티 tootest hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-482">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="6be00-483">예를 들어 다음 스크립트는 hello 설정는 **sqlcmd** hello 수신기 Windows 인증을 통해 연결 toohello 주 복제본:</span><span class="sxs-lookup"><span data-stu-id="6be00-483">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="6be00-484">Hello 수신기 포트를 사용 하는 이외의 경우 hello 기본 포트 (1433)를 hello 연결 문자열에 hello 포트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-484">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="6be00-485">예를 들어 hello 다음 sqlcmd 명령을 연결 tooa 수신기 포트 1435에서:</span><span class="sxs-lookup"><span data-stu-id="6be00-485">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="6be00-486">hello SQLCMD 연결 toowhichever 인스턴스의 SQL Server 호스트 hello에 대 한 주 복제본을 자동으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-486">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="6be00-487">지정한 hello 포트가 두 SQL Server의 hello 방화벽에서 열려 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-487">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="6be00-488">두 서버 hello 있습니다를 사용 하는 TCP 포트에 대 한 인바운드 규칙을 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-488">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="6be00-489">자세한 내용은 [방화벽 규칙 추가 또는 편집](http://technet.microsoft.com/library/cc753558.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6be00-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a><span data-ttu-id="6be00-490">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6be00-490">Next steps</span></span>

- <span data-ttu-id="6be00-491">[두 번째 가용성 그룹에서 IP 주소 tooa 부하 분산 장치 추가](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be00-491">[Add an IP address tooa load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
