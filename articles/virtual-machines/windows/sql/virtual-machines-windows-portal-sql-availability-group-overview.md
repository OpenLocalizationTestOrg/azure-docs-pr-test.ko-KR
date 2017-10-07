---
title: "서버 가용성 그룹-Azure 가상 컴퓨터-개요 aaaSQL | Microsoft Docs"
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
ms.openlocfilehash: ecac8b8c5073021af2aa22a05490bb8c4c20ed17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="ed811-103">Azure Virtual Machines의 SQL Server Always On 가용성 그룹 소개</span><span class="sxs-lookup"><span data-stu-id="ed811-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="ed811-104">이 문서에서는 Azure Virtual Machines의 SQL Server 가용성 그룹을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="ed811-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="ed811-105">Always On 가용성 그룹에 Azure 가상 컴퓨터는 온-프레미스 가용성 그룹에 비슷한 tooAlways 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed811-105">Always On availability groups on Azure Virtual Machines are similar tooAlways On availability groups on premises.</span></span> <span data-ttu-id="ed811-106">자세한 내용은 [Always On 가용성 그룹(SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed811-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="ed811-107">hello 다이어그램 hello 부분의 전체 SQL Server 가용성 그룹에서 Azure 가상 컴퓨터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed811-107">hello diagram illustrates hello parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![가용성 그룹](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="ed811-109">hello 주요 차이점 Azure 가상 컴퓨터의 가용성 그룹은 Azure 가상 컴퓨터는 hello에 대 한 요구는 [부하 분산 장치](../../../load-balancer/load-balancer-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed811-109">hello key difference for an Availability Group in Azure Virtual Machines is that hello Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="ed811-110">hello 부하 분산 장치는 hello 가용성 그룹 수신기에 대 한 hello IP 주소를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="ed811-110">hello load balancer holds hello IP addresses for hello availability group listener.</span></span> <span data-ttu-id="ed811-111">가용성 그룹을 여러 개 있는 경우 그룹마다 수신기가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ed811-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="ed811-112">하나의 부하 분산 장치가 여러 수신기를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed811-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="ed811-113">Azure 가상 컴퓨터에는 SQL Server 가용성 aroup 준비 toobuild 러 우면 toothese 자습서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ed811-113">When you are ready toobuild a SQL Server availability aroup on Azure Virtual Machines, refer toothese tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="ed811-114">템플릿에서 자동으로 가용성 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ed811-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="ed811-115">자동으로 Azure VM의 Always On 가용성 그룹 구성 - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ed811-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="ed811-116">Azure Portal에서 수동으로 가용성 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ed811-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="ed811-117">또한 직접 만들 수 있습니다 hello 가상 컴퓨터 hello 서식 파일 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed811-117">You can also create hello virtual machines yourself without hello template.</span></span> <span data-ttu-id="ed811-118">먼저 hello 필수 다음 hello 가용성 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed811-118">First, complete hello prerequisites, then create hello availability group.</span></span> <span data-ttu-id="ed811-119">Hello 다음 항목을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ed811-119">See hello following topics:</span></span> 

- [<span data-ttu-id="ed811-120">Azure Virtual Machines의 SQL Server Always On 가용성 그룹에 대한 필수 구성 요소 구성</span><span class="sxs-lookup"><span data-stu-id="ed811-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="ed811-121">만들 Always On 가용성 그룹 tooimprove 고가용성 및 재해 복구</span><span class="sxs-lookup"><span data-stu-id="ed811-121">Create Always On Availability Group tooimprove availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="ed811-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ed811-122">Next steps</span></span>

<span data-ttu-id="ed811-123">[다른 지역의 Azure Virtual Machines에서 SQL Server Always On 가용성 그룹 구성](virtual-machines-windows-portal-sql-availability-group-dr.md).</span><span class="sxs-lookup"><span data-stu-id="ed811-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
