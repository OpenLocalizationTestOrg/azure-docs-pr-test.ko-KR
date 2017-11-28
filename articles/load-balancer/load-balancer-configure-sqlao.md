---
title: "sql에 항상 aaaConfigure 부하 분산 장치 | Microsoft Docs"
description: "부하 분산 장치 toowork에 항상 SQL 및 tooleverage powershell toocreate hello SQL 구현에 대 한 분산 장치를 로드 하는 방법 구성"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="ae39d-103">SQL Always On에 대해 부하 분산 장치 구성</span><span class="sxs-lookup"><span data-stu-id="ae39d-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="ae39d-104">이제 ILB에서 SQL Server AlwaysOn 가용성 그룹을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae39d-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="ae39d-105">가용성 그룹은 고가용성 및 재해 복구를 위한 SQL Server의 주력 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="ae39d-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="ae39d-106">가용성 그룹 수신기 hello 하면 클라이언트 응용 프로그램 tooseamlessly toohello hello hello 구성의 hello 복제본 수에 관계 없이 주 복제본을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae39d-106">hello Availability Group Listener allows client applications tooseamlessly connect toohello primary replica, irrespective of hello number of hello replicas in hello configuration.</span></span>

<span data-ttu-id="ae39d-107">hello 수신기 (DNS) 이름은 매핑된 tooa 부하 분산 된 IP 주소 이며 Azure의 부하 분산 장치 hello 들어오는 트래픽을 tooonly hello 주 서버에 지시 hello 복제 세트에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae39d-107">hello listener (DNS) name is mapped tooa load-balanced IP address and Azure's load balancer directs hello incoming traffic tooonly hello primary server in hello replica set.</span></span>

<span data-ttu-id="ae39d-108">SQL Server AlwaysOn(수신기) 끝점에 대해 ILB 지원을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae39d-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="ae39d-109">이제 hello 수신기의 hello 액세스 가능성을 제어할 하 고 가상 네트워크 (VNet)에 특정 서브넷에서 hello 부하 분산 된 IP 주소를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae39d-109">You now have control over hello accessibility of hello listener and can choose hello load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="ae39d-110">ILB를 hello 수신기에서 사용 하 여 SQL server 끝점 hello (예: Server tcp:ListenerName, 1433 = 데이터베이스 DatabaseName =)만 액세스할 수 있는:</span><span class="sxs-lookup"><span data-stu-id="ae39d-110">By using ILB on hello listener, hello SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="ae39d-111">서비스 및 Vm에서 hello 동일한 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="ae39d-111">Services and VMs in hello same Virtual network</span></span>
* <span data-ttu-id="ae39d-112">연결된 온-프레미스 네트워크의 서비스 및 VM</span><span class="sxs-lookup"><span data-stu-id="ae39d-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="ae39d-113">상호 연결된 VNet의 서비스 및 VM</span><span class="sxs-lookup"><span data-stu-id="ae39d-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="ae39d-115">그림 1 - 인터넷 연결 부하 분산 장치로 구성된 SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="ae39d-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-toohello-service"></a><span data-ttu-id="ae39d-116">내부 부하 분산 장치 toohello 서비스 추가</span><span class="sxs-lookup"><span data-stu-id="ae39d-116">Add Internal Load Balancer toohello service</span></span>

1. <span data-ttu-id="ae39d-117">다음 예제는 hello, 우리 ' 서브넷-1' 이라는 서브넷을 포함 하는 가상 네트워크 구성:</span><span class="sxs-lookup"><span data-stu-id="ae39d-117">In hello following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="ae39d-118">각 VM에서 ILB에 대한 부하 분산 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="ae39d-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="ae39d-119">2 VM의 호출된 "sqlsvc1" 및 "sqlsvc2" 실행 되 고 있는 위의 hello 예제에서 서비스 "Sqlsvc" hello 클라우드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae39d-119">In hello example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in hello cloud service "Sqlsvc".</span></span> <span data-ttu-id="ae39d-120">Hello ILB를 만든 후 `DirectServerReturn` 스위치를 추가 하면 분산 된 끝점 toohello ILB tooallow SQL tooconfigure hello에 대 한 수신기 hello 가용성 그룹을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae39d-120">After creating hello ILB with `DirectServerReturn` switch, you add load balanced endpoints toohello ILB tooallow SQL tooconfigure hello listeners for hello availability groups.</span></span>

<span data-ttu-id="ae39d-121">SQL AlwaysOn에 대한 자세한 내용은 [Azure에서 AlwaysOn 가용성 그룹에 대한 내부 부하 분산 장치 구성](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae39d-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="ae39d-122">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ae39d-122">See Also</span></span>
[<span data-ttu-id="ae39d-123">인터넷 연결 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="ae39d-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="ae39d-124">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="ae39d-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="ae39d-125">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="ae39d-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="ae39d-126">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="ae39d-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
