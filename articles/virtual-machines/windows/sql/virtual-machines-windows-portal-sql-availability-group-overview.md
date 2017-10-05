---
title: "SQL Server 가용성 그룹 - Azure Virtual Machines - 개요 | Microsoft Docs"
description: "이 문서에서는 Azure Virtual Machines의 SQL Server 가용성 그룹을 소개합니다."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: 2cbb9ff3b2d13996b1b8dc64aa833807c264c877
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="862ce-103">Azure Virtual Machines의 SQL Server Always On 가용성 그룹 소개</span><span class="sxs-lookup"><span data-stu-id="862ce-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="862ce-104">이 문서에서는 Azure Virtual Machines의 SQL Server 가용성 그룹을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="862ce-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="862ce-105">Azure Virtual Machines의 Always On 가용성 그룹은 온-프레미스의 Always On 가용성 그룹과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="862ce-105">Always On availability groups on Azure Virtual Machines are similar to Always On availability groups on premises.</span></span> <span data-ttu-id="862ce-106">자세한 내용은 [Always On 가용성 그룹(SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="862ce-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="862ce-107">이 다이어그램에서는 Azure Virtual Machines의 전체 SQL Server 가용성 그룹 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="862ce-107">The diagram illustrates the parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![가용성 그룹](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="862ce-109">Azure Virtual Machines의 가용성 그룹에 대한 주요 차이점은 Azure Virtual Machines에 [부하 분산 장치](../../../load-balancer/load-balancer-overview.md)가 필요하다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="862ce-109">The key difference for an Availability Group in Azure Virtual Machines is that the Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="862ce-110">부하 분산 장치는 가용성 그룹 수신기의 IP 주소를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="862ce-110">The load balancer holds the IP addresses for the availability group listener.</span></span> <span data-ttu-id="862ce-111">가용성 그룹을 여러 개 있는 경우 그룹마다 수신기가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="862ce-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="862ce-112">하나의 부하 분산 장치가 여러 수신기를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="862ce-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="862ce-113">Azure Virtual Machines에서 SQL Server 가용성을 빌드할 준비가 되면 다음 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="862ce-113">When you are ready to build a SQL Server availability aroup on Azure Virtual Machines, refer to these tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="862ce-114">템플릿에서 자동으로 가용성 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="862ce-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="862ce-115">자동으로 Azure VM의 Always On 가용성 그룹 구성 - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="862ce-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="862ce-116">Azure Portal에서 수동으로 가용성 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="862ce-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="862ce-117">또한 템플릿을 사용하지 않고 가상 컴퓨터를 직접 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="862ce-117">You can also create the virtual machines yourself without the template.</span></span> <span data-ttu-id="862ce-118">먼저 필수 구성 요소를 완료한 다음 가용성 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="862ce-118">First, complete the prerequisites, then create the availability group.</span></span> <span data-ttu-id="862ce-119">또한 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="862ce-119">See the following topics:</span></span> 

- [<span data-ttu-id="862ce-120">Azure Virtual Machines의 SQL Server Always On 가용성 그룹에 대한 필수 구성 요소 구성</span><span class="sxs-lookup"><span data-stu-id="862ce-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="862ce-121">Always On 가용성 그룹을 만들어 가용성 및 재해 복구 개선</span><span class="sxs-lookup"><span data-stu-id="862ce-121">Create Always On Availability Group to improve availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="862ce-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="862ce-122">Next steps</span></span>

<span data-ttu-id="862ce-123">[다른 지역의 Azure Virtual Machines에서 SQL Server Always On 가용성 그룹 구성](virtual-machines-windows-portal-sql-availability-group-dr.md).</span><span class="sxs-lookup"><span data-stu-id="862ce-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
