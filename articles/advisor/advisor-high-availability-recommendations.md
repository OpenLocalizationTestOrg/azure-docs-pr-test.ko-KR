---
title: "Azure Advisor 고가용성 권장 사항 | Microsoft Docs"
description: "Azure Advisor를 사용하여 Azure 배포의 가용성을 향상시킵니다."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 23c159471a6e5a7ad9cb545840e8afd3ac72ecba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-high-availability-recommendations"></a><span data-ttu-id="f1be1-103">Advisor 고가용성 권장 사항</span><span class="sxs-lookup"><span data-stu-id="f1be1-103">Advisor High Availability recommendations</span></span>

<span data-ttu-id="f1be1-104">Azure Advisor는 업무상 중요한 응용 프로그램의 연속성을 보장하고 향상시키는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-104">Azure Advisor helps you ensure and improve the continuity of your business-critical applications.</span></span> <span data-ttu-id="f1be1-105">Advisor 대시보드의 **고가용성** 탭에서 Advisor의 고가용성 권장 사항을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-105">You can get high availability recommendations by Advisor from the **High Availability** tab of the Advisor dashboard.</span></span>

![Advisor 대시보드의 고가용성 단추](./media/advisor-high-availability-recommendations/advisor-high-availability-tab.png)


## <a name="ensure-virtual-machine-fault-tolerance"></a><span data-ttu-id="f1be1-107">가상 컴퓨터 내결함성 보장</span><span class="sxs-lookup"><span data-stu-id="f1be1-107">Ensure virtual machine fault tolerance</span></span>

<span data-ttu-id="f1be1-108">Advisor는 가용성 집합에 속하지 않는 가상 컴퓨터를 식별하고 이러한 가상 컴퓨터를 가용성 집합으로 이동할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-108">Advisor identifies virtual machines that are not part of an availability set and recommends moving them into an availability set.</span></span> <span data-ttu-id="f1be1-109">응용 프로그램에 중복성을 제공하기 위해 여러 개의 가상 컴퓨터를 가용성 집합으로 그룹화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-109">To provide redundancy to your application, we recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="f1be1-110">이 구성은 계획된 유지 관리 또는 계획되지 않은 유지 관리 이벤트 중에 적어도 하나의 가상 컴퓨터를 사용할 수 있고 Azure 가상 컴퓨터 SLA가 충족되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-110">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets the Azure virtual machine SLA.</span></span> <span data-ttu-id="f1be1-111">가상 컴퓨터에 대한 가용성 집합을 만들거나, 기존 가용성 집합에 가상 컴퓨터를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-111">You can choose either to create an availability set for the virtual machine or to add the virtual machine to an existing availability set.</span></span>

> [!NOTE]
> <span data-ttu-id="f1be1-112">가용성 집합을 만들도록 선택한 경우 해당 가용성 집합에 적어도 하나 이상의 가상 컴퓨터를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-112">If you choose to create an availability set, you must add at least one more virtual machine into it.</span></span> <span data-ttu-id="f1be1-113">중단 시간 동안 하나 이상의 컴퓨터를 사용할 수 있도록 하기 위해 가용성 집합에 둘 이상의 가상 컴퓨터를 그룹화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-113">We recommend that you group two or more virtual machines in an availability set to ensure that at least one machine is available during an outage.</span></span>

![Advisor 권장 사항: 가상 컴퓨터 중복성을 위해 가용성 집합 사용](./media/advisor-high-availability-recommendations/advisor-high-availability-create-availability-set.png)

## <a name="ensure-availability-set-fault-tolerance"></a><span data-ttu-id="f1be1-115">가용성 집합 내결함성 보장</span><span class="sxs-lookup"><span data-stu-id="f1be1-115">Ensure availability set fault tolerance</span></span> 

<span data-ttu-id="f1be1-116">Advisor는 단일 가상 컴퓨터를 포함하는 가용성 집합을 식별하고 여기에 하나 이상의 가상 컴퓨터를 추가할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-116">Advisor identifies availability sets that contain a single virtual machine and recommends adding one or more virtual machines to it.</span></span> <span data-ttu-id="f1be1-117">응용 프로그램에 중복성을 제공하기 위해 여러 개의 가상 컴퓨터를 가용성 집합으로 그룹화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-117">To provide redundancy to your application, we recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="f1be1-118">이 구성은 계획된 유지 관리 또는 계획되지 않은 유지 관리 이벤트 중에 적어도 하나의 가상 컴퓨터를 사용할 수 있고 Azure 가상 컴퓨터 SLA가 충족되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-118">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets the Azure virtual machine SLA.</span></span> <span data-ttu-id="f1be1-119">가상 컴퓨터를 만들거나 기존 가상 컴퓨터를 사용하도록 선택하고 해당 컴퓨터를 가용성 집합에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-119">You can choose either to create a virtual machine or to use an existing virtual machine, and to add it to the availability set.</span></span>  

![Advisor 권장 사항: 이 가용성 집합에 하나 이상의 VM 추가](./media/advisor-high-availability-recommendations/advisor-high-availability-add-vm-to-availability-set.png)


## <a name="ensure-application-gateway-fault-tolerance"></a><span data-ttu-id="f1be1-121">응용 프로그램 게이트웨이 내결함성 보장</span><span class="sxs-lookup"><span data-stu-id="f1be1-121">Ensure application gateway fault tolerance</span></span>
<span data-ttu-id="f1be1-122">응용 프로그램 게이트웨이에서 구동되는 중요 업무용 응용 프로그램의 비즈니스 연속성을 위해 Advisor는 내결함성에 대해 구성되지 않은 응용 프로그램 게이트웨이 인스턴스를 식별하고 수행할 수 있는 수정 작업을 제안합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-122">To ensure the business continuity of mission-critical applications that are powered by application gateways, Advisor identifies application gateway instances that are not configured for fault tolerance, and it suggests remediation actions that you can take.</span></span> <span data-ttu-id="f1be1-123">Advisor는 중간 규모 또는 대규모 단일 인스턴스 응용 프로그램 게이트웨이를 식별하고 하나 이상의 인스턴스 추가를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-123">Advisor identifies medium or large single-instance application gateways, and it recommends adding at least one more instance.</span></span> <span data-ttu-id="f1be1-124">또한 단일 또는 다중 인스턴스 소규모 응용 프로그램 게이트웨이를 식별하고 중간 규모 또는 대규모 SKU로 마이그레이션을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-124">It also identifies single- or multi-instance small application gateways and recommends migrating to medium or large SKUs.</span></span> <span data-ttu-id="f1be1-125">Advisor는 응용 프로그램 게이트웨이 인스턴스가 이러한 리소스에 대한 현재 SLA 요구 사항을 만족하도록 구성되어 있는지 확인하는 데 이러한 작업을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-125">Advisor recommends these actions to ensure that your application gateway instances are configured to satisfy the current SLA requirements for these resources.</span></span>

![Advisor 권장 사항: 두 개 이상의 중간 규모 또는 대규모 응용 프로그램 게이트웨이 인스턴스 배포](./media/advisor-high-availability-recommendations/advisor-high-availability-application-gateway.png)

## <a name="improve-the-performance-and-reliability-of-virtual-machine-disks"></a><span data-ttu-id="f1be1-127">가상 컴퓨터 디스크의 성능 및 안정성 향상</span><span class="sxs-lookup"><span data-stu-id="f1be1-127">Improve the performance and reliability of virtual machine disks</span></span>

<span data-ttu-id="f1be1-128">Advisor는 표준 디스크를 포함하는 가상 컴퓨터를 식별하고 프리미엄 디스크로 업그레이드할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-128">Advisor identifies virtual machines with standard disks and recommends upgrading to premium disks.</span></span>
 
<span data-ttu-id="f1be1-129">Azure Premium Storage는 I/O 사용량이 많은 작업을 실행하는 가상 컴퓨터에서 대기 시간이 짧은 고성능 디스크 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-129">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines that run I/O-intensive workloads.</span></span> <span data-ttu-id="f1be1-130">프리미엄 저장소 계정을 사용하는 가상 컴퓨터 디스크는 SSD(솔리드 스테이트 드라이브)에 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-130">Virtual machine disks that use premium storage accounts store data on solid-state drives (SSDs).</span></span> <span data-ttu-id="f1be1-131">응용 프로그램이 최고 성능을 낼 수 있도록 높은 IOPS가 필요한 모든 가상 컴퓨터 디스크를 프리미엄 저장소로 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-131">For the best performance for your application, we recommend that you migrate any virtual machine disks requiring high IOPS to premium storage.</span></span> 

<span data-ttu-id="f1be1-132">디스크에 높은 IOPS가 필요하지 않으면 표준 저장소에 유지 관리하여 비용을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-132">If your disks do not require high IOPS, you can limit costs by maintaining them in standard storage.</span></span> <span data-ttu-id="f1be1-133">표준 저장소는 SSD 대신 HDD(하드 디스크 드라이브)에 가상 컴퓨터 디스크 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-133">Standard storage stores virtual machine disk data on hard disk drives (HDDs) instead of SSDs.</span></span> <span data-ttu-id="f1be1-134">가상 컴퓨터 디스크를 프리미엄 디스크로 마이그레이션하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-134">You can choose to migrate your virtual machine disks to premium disks.</span></span> <span data-ttu-id="f1be1-135">프리미엄 디스크는 대부분의 가상 컴퓨터 SKU에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-135">Premium disks are supported on most virtual machine SKUs.</span></span> <span data-ttu-id="f1be1-136">그러나 일부 경우에 프리미엄 디스크를 사용하려는 경우 가상 컴퓨터 SKU도 업그레이드해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-136">However, in some cases, if you want to use premium disks, you might need to upgrade your virtual machine SKUs as well.</span></span>

![Advisor 권장 사항: 프리미엄 디스크로 업그레이드하여 가상 컴퓨터 디스크의 안정성 향상](./media/advisor-high-availability-recommendations/advisor-high-availability-upgrade-to-premium-disks.png)

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a><span data-ttu-id="f1be1-138">가상 컴퓨터 데이터를 실수로 삭제되지 않도록 보호</span><span class="sxs-lookup"><span data-stu-id="f1be1-138">Protect your virtual machine data from accidental deletion</span></span>
<span data-ttu-id="f1be1-139">Advisor는 백업이 활성화되지 않은 가상 컴퓨터를 식별하고 백업을 활성화할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-139">Advisor identifies virtual machines where backup is not enabled, and it recommends enabling backup.</span></span> <span data-ttu-id="f1be1-140">가상 컴퓨터 백업 설정은 비즈니스에 중요한 데이터의 가용성을 보장하고 실수로 인한 삭제 또는 손상에 대한 보호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-140">Setting up virtual machine backup ensures the availability of your business-critical data and offers protection against accidental deletion or corruption.</span></span>

![Advisor 권장 사항: 중요 업무용 데이터를 보호하도록 가상 컴퓨터 백업 구성](./media/advisor-high-availability-recommendations/advisor-high-availability-virtual-machine-backup.png)

## <a name="access-high-availability-recommendations-in-advisor"></a><span data-ttu-id="f1be1-142">Advisor의 고가용성 권장 사항에 액세스</span><span class="sxs-lookup"><span data-stu-id="f1be1-142">Access high availability recommendations in Advisor</span></span>

1. <span data-ttu-id="f1be1-143">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-143">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="f1be1-144">왼쪽 창에서 **더 많은 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-144">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="f1be1-145">서비스 메뉴 창의 **모니터링 및 관리** 아래에서 **Azure Advisor**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-145">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="f1be1-146">Advisor 대시보드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-146">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="f1be1-147">Advisor 대시보드에서 **고가용성** 탭을 클릭한 다음 권장 사항을 받아보려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-147">On the Advisor dashboard, click the **High Availability** tab, and then select the subscription for which you want to receive recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="f1be1-148">Advisor 권장 사항에 액세스하려면 먼저 Advisor에 *구독을 등록*해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-148">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="f1be1-149">구독은 *구독 소유자*가 Advisor 대시보드를 시작하고 **권장 사항 가져오기** 단추를 클릭할 때 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-149">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="f1be1-150">이 작업은 *한 번만* 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-150">This is a *one-time operation*.</span></span> <span data-ttu-id="f1be1-151">구독이 등록된 후 구독, 리소스 그룹 또는 특정 리소스에 대한 *소유자*, *참여자* 또는 *리더*로 Advisor 권장 사항에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1be1-151">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1be1-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f1be1-152">Next steps</span></span>

<span data-ttu-id="f1be1-153">Advisor 권장 사항에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1be1-153">For more information about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="f1be1-154">Azure Advisor 소개</span><span class="sxs-lookup"><span data-stu-id="f1be1-154">Introduction to Azure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="f1be1-155">Advisor 시작</span><span class="sxs-lookup"><span data-stu-id="f1be1-155">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="f1be1-156">Advisor 비용 권장 사항</span><span class="sxs-lookup"><span data-stu-id="f1be1-156">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="f1be1-157">Advisor 성능 권장 사항</span><span class="sxs-lookup"><span data-stu-id="f1be1-157">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="f1be1-158">Advisor 보안 권장 사항</span><span class="sxs-lookup"><span data-stu-id="f1be1-158">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

