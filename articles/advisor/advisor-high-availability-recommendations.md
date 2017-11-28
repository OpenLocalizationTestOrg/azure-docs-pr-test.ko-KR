---
title: "aaaAzure 고가용성 Advisor 권장 사항을 | Microsoft Docs"
description: "Azure 배포의 Azure 관리자 tooimprove 높은 가용성을 사용 합니다."
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
ms.openlocfilehash: 3ac75ce401271f0212d198d7a7dc75ab702b6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-high-availability-recommendations"></a><span data-ttu-id="76f4e-103">Advisor 고가용성 권장 사항</span><span class="sxs-lookup"><span data-stu-id="76f4e-103">Advisor High Availability recommendations</span></span>

<span data-ttu-id="76f4e-104">Azure 관리자를 사용 하면 확인 하 고 비즈니스에 중요 한 응용 프로그램의 hello 연속성 개선.</span><span class="sxs-lookup"><span data-stu-id="76f4e-104">Azure Advisor helps you ensure and improve hello continuity of your business-critical applications.</span></span> <span data-ttu-id="76f4e-105">Hello에서 관리자가 권장 사항을 고가용성을 얻을 수 있습니다 **고가용성** hello 관리자 대시보드 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-105">You can get high availability recommendations by Advisor from hello **High Availability** tab of hello Advisor dashboard.</span></span>

![Hello 관리자 대시보드에서 높은 가용성 단추](./media/advisor-high-availability-recommendations/advisor-high-availability-tab.png)


## <a name="ensure-virtual-machine-fault-tolerance"></a><span data-ttu-id="76f4e-107">가상 컴퓨터 내결함성 보장</span><span class="sxs-lookup"><span data-stu-id="76f4e-107">Ensure virtual machine fault tolerance</span></span>

<span data-ttu-id="76f4e-108">Advisor는 가용성 집합에 속하지 않는 가상 컴퓨터를 식별하고 이러한 가상 컴퓨터를 가용성 집합으로 이동할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-108">Advisor identifies virtual machines that are not part of an availability set and recommends moving them into an availability set.</span></span> <span data-ttu-id="76f4e-109">중복 tooyour 응용 프로그램을 제공 하려면 가용성 집합에 두 개 이상의 가상 컴퓨터를 그룹화 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-109">To provide redundancy tooyour application, we recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="76f4e-110">이 구성을 사용 하면 계획 되거나 계획 되지 않은 유지 관리 이벤트 중 하나에서 하나 이상의 가상 컴퓨터를 사용할 수 충족 hello Azure 가상 컴퓨터 SLA 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-110">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets hello Azure virtual machine SLA.</span></span> <span data-ttu-id="76f4e-111">가용성 집합에 대 한 hello 가상 컴퓨터 또는 tooadd hello 가상 컴퓨터 tooan 기존 가용성 집합 toocreate 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-111">You can choose either toocreate an availability set for hello virtual machine or tooadd hello virtual machine tooan existing availability set.</span></span>

> [!NOTE]
> <span data-ttu-id="76f4e-112">Toocreate를 선택 하면 가용성 집합을 추가 해야 적어도 하나 이상의 가상 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-112">If you choose toocreate an availability set, you must add at least one more virtual machine into it.</span></span> <span data-ttu-id="76f4e-113">두 그룹 또는 가용성에서 더 많은 가상 컴퓨터 설정 tooensure 하는 것이 좋습니다 중단이 발생 하는 동안 하나 이상의 컴퓨터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-113">We recommend that you group two or more virtual machines in an availability set tooensure that at least one machine is available during an outage.</span></span>

![Advisor 권장 사항: 가상 컴퓨터 중복성을 위해 가용성 집합 사용](./media/advisor-high-availability-recommendations/advisor-high-availability-create-availability-set.png)

## <a name="ensure-availability-set-fault-tolerance"></a><span data-ttu-id="76f4e-115">가용성 집합 내결함성 보장</span><span class="sxs-lookup"><span data-stu-id="76f4e-115">Ensure availability set fault tolerance</span></span> 

<span data-ttu-id="76f4e-116">관리자는 단일 가상 컴퓨터를 포함 하는 가용성 집합을 식별 하 고 하나 이상의 가상 컴퓨터 tooit를 추가 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-116">Advisor identifies availability sets that contain a single virtual machine and recommends adding one or more virtual machines tooit.</span></span> <span data-ttu-id="76f4e-117">중복 tooyour 응용 프로그램을 제공 하려면 가용성 집합에 두 개 이상의 가상 컴퓨터를 그룹화 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-117">To provide redundancy tooyour application, we recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="76f4e-118">이 구성을 사용 하면 계획 되거나 계획 되지 않은 유지 관리 이벤트 중 하나에서 하나 이상의 가상 컴퓨터를 사용할 수 충족 hello Azure 가상 컴퓨터 SLA 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-118">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets hello Azure virtual machine SLA.</span></span> <span data-ttu-id="76f4e-119">가상 컴퓨터 또는 기존 가상 컴퓨터를 toouse 및 tooadd toocreate 중 하나를 선택할 수 있습니다이 toohello 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-119">You can choose either toocreate a virtual machine or toouse an existing virtual machine, and tooadd it toohello availability set.</span></span>  

![관리자의 권장 구성: 하나 이상의 Vm toothis 가용성 집합 추가](./media/advisor-high-availability-recommendations/advisor-high-availability-add-vm-to-availability-set.png)


## <a name="ensure-application-gateway-fault-tolerance"></a><span data-ttu-id="76f4e-121">응용 프로그램 게이트웨이 내결함성 보장</span><span class="sxs-lookup"><span data-stu-id="76f4e-121">Ensure application gateway fault tolerance</span></span>
<span data-ttu-id="76f4e-122">응용 프로그램 게이트웨이에서 구동 되는 중요 한 응용 프로그램의 tooensure hello 비즈니스 연속성, Advisor 결함 허용을 위해 구성 되지 않은 응용 프로그램 게이트웨이 인스턴스를 식별 하 고 사용할 수 있는 수정 작업과 하도록 제안 .</span><span class="sxs-lookup"><span data-stu-id="76f4e-122">tooensure hello business continuity of mission-critical applications that are powered by application gateways, Advisor identifies application gateway instances that are not configured for fault tolerance, and it suggests remediation actions that you can take.</span></span> <span data-ttu-id="76f4e-123">Advisor는 중간 규모 또는 대규모 단일 인스턴스 응용 프로그램 게이트웨이를 식별하고 하나 이상의 인스턴스 추가를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-123">Advisor identifies medium or large single-instance application gateways, and it recommends adding at least one more instance.</span></span> <span data-ttu-id="76f4e-124">또한 단일 또는 다중 instance 작은 응용 프로그램 게이트웨이 식별 하 고 마이그레이션 toomedium 또는 큰 Sku 것을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-124">It also identifies single- or multi-instance small application gateways and recommends migrating toomedium or large SKUs.</span></span> <span data-ttu-id="76f4e-125">관리자가 응용 프로그램 게이트웨이 인스턴스는 구성 된 toosatisfy hello 현재 SLA 요구 사항입니다 이러한 리소스에 대 한 이러한 작업 tooensure 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-125">Advisor recommends these actions tooensure that your application gateway instances are configured toosatisfy hello current SLA requirements for these resources.</span></span>

![Advisor 권장 사항: 두 개 이상의 중간 규모 또는 대규모 응용 프로그램 게이트웨이 인스턴스 배포](./media/advisor-high-availability-recommendations/advisor-high-availability-application-gateway.png)

## <a name="improve-hello-performance-and-reliability-of-virtual-machine-disks"></a><span data-ttu-id="76f4e-127">가상 컴퓨터 디스크의 hello 성능 및 안정성 개선</span><span class="sxs-lookup"><span data-stu-id="76f4e-127">Improve hello performance and reliability of virtual machine disks</span></span>

<span data-ttu-id="76f4e-128">관리자는 표준 디스크를 사용 하 여 가상 컴퓨터를 식별 하 고 toopremium 디스크 업그레이드할 것을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-128">Advisor identifies virtual machines with standard disks and recommends upgrading toopremium disks.</span></span>
 
<span data-ttu-id="76f4e-129">Azure Premium Storage는 I/O 사용량이 많은 작업을 실행하는 가상 컴퓨터에서 대기 시간이 짧은 고성능 디스크 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-129">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines that run I/O-intensive workloads.</span></span> <span data-ttu-id="76f4e-130">프리미엄 저장소 계정을 사용하는 가상 컴퓨터 디스크는 SSD(솔리드 스테이트 드라이브)에 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-130">Virtual machine disks that use premium storage accounts store data on solid-state drives (SSDs).</span></span> <span data-ttu-id="76f4e-131">응용 프로그램에 대 한 최상의 성능을 위해서는 hello 높은 IOPS toopremium 저장소를 필요로 하는 모든 가상 컴퓨터 디스크를 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-131">For hello best performance for your application, we recommend that you migrate any virtual machine disks requiring high IOPS toopremium storage.</span></span> 

<span data-ttu-id="76f4e-132">디스크에 높은 IOPS가 필요하지 않으면 표준 저장소에 유지 관리하여 비용을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-132">If your disks do not require high IOPS, you can limit costs by maintaining them in standard storage.</span></span> <span data-ttu-id="76f4e-133">표준 저장소는 SSD 대신 HDD(하드 디스크 드라이브)에 가상 컴퓨터 디스크 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-133">Standard storage stores virtual machine disk data on hard disk drives (HDDs) instead of SSDs.</span></span> <span data-ttu-id="76f4e-134">가상 컴퓨터 디스크 toopremium 디스크 toomigrate를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-134">You can choose toomigrate your virtual machine disks toopremium disks.</span></span> <span data-ttu-id="76f4e-135">프리미엄 디스크는 대부분의 가상 컴퓨터 SKU에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-135">Premium disks are supported on most virtual machine SKUs.</span></span> <span data-ttu-id="76f4e-136">그러나 경우에 따라 toouse 프리미엄 디스크를 원하는 경우 할 수 있습니다 tooupgrade 가상 컴퓨터가 Sku도.</span><span class="sxs-lookup"><span data-stu-id="76f4e-136">However, in some cases, if you want toouse premium disks, you might need tooupgrade your virtual machine SKUs as well.</span></span>

![관리자의 권장 구성: toopremium 디스크를 업그레이드 하 여 가상 컴퓨터 디스크의 hello 안정성이 개선](./media/advisor-high-availability-recommendations/advisor-high-availability-upgrade-to-premium-disks.png)

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a><span data-ttu-id="76f4e-138">가상 컴퓨터 데이터를 실수로 삭제되지 않도록 보호</span><span class="sxs-lookup"><span data-stu-id="76f4e-138">Protect your virtual machine data from accidental deletion</span></span>
<span data-ttu-id="76f4e-139">Advisor는 백업이 활성화되지 않은 가상 컴퓨터를 식별하고 백업을 활성화할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-139">Advisor identifies virtual machines where backup is not enabled, and it recommends enabling backup.</span></span> <span data-ttu-id="76f4e-140">가상 컴퓨터 백업 설정 업무에 중요 한 데이터의 hello 가용성을 보장 하 고 실수로 인 한 삭제 또는 손상에 대 한 보호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-140">Setting up virtual machine backup ensures hello availability of your business-critical data and offers protection against accidental deletion or corruption.</span></span>

![관리자의 권장 구성: 가상 컴퓨터 백업 tooprotect 업무상 중요 한 데이터 구성](./media/advisor-high-availability-recommendations/advisor-high-availability-virtual-machine-backup.png)

## <a name="access-high-availability-recommendations-in-advisor"></a><span data-ttu-id="76f4e-142">Advisor의 고가용성 권장 사항에 액세스</span><span class="sxs-lookup"><span data-stu-id="76f4e-142">Access high availability recommendations in Advisor</span></span>

1. <span data-ttu-id="76f4e-143">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-143">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="76f4e-144">Hello 왼쪽된 창에서 클릭 **더 많은 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-144">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="76f4e-145">Hello 메뉴 창을 아래에서 서비스 **모니터링 및 관리**, 클릭 **Azure 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-145">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="76f4e-146">hello 관리자 대시보드 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-146">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="76f4e-147">Hello 관리자 대시보드에서 hello 클릭 **고가용성** 탭을 선택한 다음 tooreceive 권장 사항을 보려는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-147">On hello Advisor dashboard, click hello **High Availability** tab, and then select hello subscription for which you want tooreceive recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="76f4e-148">관리자의 권장 구성이 tooaccess 먼저 *구독 등록* 관리자와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-148">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="76f4e-149">구독을 등록 때는 *구독 소유자* 실행 하는 경우 관리자 대시보드 및 클릭 hello hello **위한 권장 사항 보기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-149">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="76f4e-150">이 작업은 *한 번만* 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-150">This is a *one-time operation*.</span></span> <span data-ttu-id="76f4e-151">Hello 구독을 등록 하 고, Advisor 권장 사항을 사용할 수 있습니다 *소유자*, *참가자*, 또는 *판독기* 구독에 리소스 그룹 또는 특정 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="76f4e-151">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76f4e-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="76f4e-152">Next steps</span></span>

<span data-ttu-id="76f4e-153">Advisor 권장 사항에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76f4e-153">For more information about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="76f4e-154">소개 tooAzure 관리자</span><span class="sxs-lookup"><span data-stu-id="76f4e-154">Introduction tooAzure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="76f4e-155">Advisor 시작</span><span class="sxs-lookup"><span data-stu-id="76f4e-155">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="76f4e-156">Advisor 비용 권장 사항</span><span class="sxs-lookup"><span data-stu-id="76f4e-156">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="76f4e-157">Advisor 성능 권장 사항</span><span class="sxs-lookup"><span data-stu-id="76f4e-157">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="76f4e-158">Advisor 보안 권장 사항</span><span class="sxs-lookup"><span data-stu-id="76f4e-158">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

