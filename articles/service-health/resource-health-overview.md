---
title: "aaaAzure 리소스 상태 개요 | Microsoft Docs"
description: "Azure 리소스 상태 개요"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/01/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: f06153864090487829f717dc3e8972c78a4a58af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="9c013-103">Azure Resource Health 개요</span><span class="sxs-lookup"><span data-stu-id="9c013-103">Azure resource health overview</span></span>
 
<span data-ttu-id="9c013-104">Resource Health는 Azure 문제가 리소스에 영향을 주는 경우 진단 및 지원을 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="9c013-105">리소스의 hello 최신 및 이전 상태에 대해 알려 하 고 문제를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-105">It informs you about hello current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="9c013-106">Resource Health는 Azure 서비스 문제와 관련된 도움이 필요할 때 기술 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="9c013-107">반면 [Azure 상태](https://status.azure.com) 다양 한 Azure 고객 집합에 영향을 주는 서비스 문제에 대해 알려, 리소스 상태 리소스 hello 상태의 개인 설정 된 대시보드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of hello health of your resources.</span></span> <span data-ttu-id="9c013-108">리소스 상태를 보면 리소스 hello에 사용할 수 없었습니다. hello 항상 기한이 지 남 tooAzure 서비스 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-108">Resource health shows you all hello times your resources were unavailable in hello past due tooAzure service issues.</span></span> <span data-ttu-id="9c013-109">이렇게 하면 toounderstand 있습니다에 대 한 간단한 SLA 위반 된 경우.</span><span class="sxs-lookup"><span data-stu-id="9c013-109">This makes it simple for you toounderstand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="9c013-110">무엇이 리소스로 간주되고 리소스 상태에서는 리소스가 정상인지를 어떻게 결정하나요?</span><span class="sxs-lookup"><span data-stu-id="9c013-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="9c013-111">리소스는 가상 컴퓨터, 웹앱 또는 SQL Database처럼 Azure Resource Manager를 통해 Azure 서비스에서 제공하는 리소스 유형의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="9c013-112">리소스 상태는 리소스의 정상 상태 경우 hello 서로 다른 Azure 서비스 tooassess에서 내보낸 신호에 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-112">Resource health relies on signals emitted by hello different Azure services tooassess if a resource is healthy or not.</span></span> <span data-ttu-id="9c013-113">리소스 상태가 정상이 아닌 경우 리소스 상태 hello 문제의 toodetermine hello 소스 추가 정보를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-113">If a resource is unhealthy, resource health analyzes additional information toodetermine hello source of hello problem.</span></span> <span data-ttu-id="9c013-114">또한 Microsoft toofix hello 문제 또는 hello 문제의 원인을 tooaddress hello를 수행할 수 있는 작업에 소요 되는 동작을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-114">It also identifies actions Microsoft is taking toofix hello issue or what actions you can take tooaddress hello cause of hello problem.</span></span> 

<span data-ttu-id="9c013-115">리소스 종류와 상태의 검토 hello 전체 목록은 체크 인할 [Azure 리소스 상태](resource-health-checks-resource-types.md) 상태 평가 하는 방법을 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-115">Review hello full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="9c013-116">리소스 상태에서 제공하는 상태</span><span class="sxs-lookup"><span data-stu-id="9c013-116">Health status provided by resource health</span></span>
<span data-ttu-id="9c013-117">리소스의 hello 상태 hello 다음 상태 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-117">hello health of a resource is one of hello following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="9c013-118">사용 가능</span><span class="sxs-lookup"><span data-stu-id="9c013-118">Available</span></span>
<span data-ttu-id="9c013-119">hello 서비스가 hello 리소스의 hello 상태에 영향을 주지는 이벤트가 검색 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-119">hello service has not detected any events impacting hello health of hello resource.</span></span> <span data-ttu-id="9c013-120">여기서 hello 리소스에서에서 복구 계획 되지 않은 가동 중지 시간 동안 hello 마지막 하는 경우에 표시 됩니다는 24 시간 동안 hello **최근 복구** 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-120">In cases where hello resource has recovered from unplanned downtime during hello last 24 hours you will see hello **recently recovered** notification.</span></span>

![리소스 상태가 사용 가능한 가상 컴퓨터](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="9c013-122">사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="9c013-122">Unavailable</span></span>
<span data-ttu-id="9c013-123">진행 중인 플랫폼 또는 플랫폼 비 이벤트 hello 리소스의 hello 상태에 영향을 주지 hello 검색 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-123">hello service has detected an ongoing platform or non-platform event impacting hello health of hello resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="9c013-124">플랫폼 이벤트</span><span class="sxs-lookup"><span data-stu-id="9c013-124">Platform events</span></span>
<span data-ttu-id="9c013-125">이러한 이벤트는 hello Azure 인프라의 여러 구성 요소에 의해 트리거되는 및 계획 된 유지 관리와 같은 예약 된 작업 및 계획 되지 않은 호스트 재부팅와 같은 예기치 않은 문제를 모두 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-125">These events are triggered by multiple components of hello Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="9c013-126">리소스 상태 이벤트 hello hello 복구 프로세스에 추가 세부 정보를 제공 하며 지원할 수 있도록 하면 toocontact는 활성 Microsoft 계약을 지원 해야 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-126">Resource health provides additional details on hello event, hello recovery process and enables you toocontact support even if you don't have an active Microsoft support agreement.</span></span>

![Tooplatform 이벤트 인해 리소스 상태 사용할 수 없는 가상 컴퓨터](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="9c013-128">비-플랫폼 이벤트</span><span class="sxs-lookup"><span data-stu-id="9c013-128">Non-Platform events</span></span>
<span data-ttu-id="9c013-129">이러한 이벤트는 사용자가 예를 들어 가상 컴퓨터를 중지 하거나 hello 연결 tooa Redis 캐시의 최대 수에 도달 하 여 수행 된 작업에 의해 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching hello maximum number of connections tooa Redis Cache.</span></span>

![Toonon 플랫폼 이벤트 인해 리소스 상태 사용할 수 없는 가상 컴퓨터](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="9c013-131">알 수 없음</span><span class="sxs-lookup"><span data-stu-id="9c013-131">Unknown</span></span>
<span data-ttu-id="9c013-132">이 상태 정보는 리소스 상태에서 10분 이상 이 리소스에 대한 정보를 수신하지 못했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="9c013-133">이 상태 hello 상태의 hello 리소스의 명확한 표시 동안 hello 문제 해결 과정에에서는 중요 한 데이터 요소는:</span><span class="sxs-lookup"><span data-stu-id="9c013-133">While this status is not a definitive indication of hello state of hello resource, it is an important data point in hello troubleshooting process:</span></span>
* <span data-ttu-id="9c013-134">Hello 리소스 hello 리소스의 예상된 hello 상태와 실행 중인 경우 tooAvailable 몇 분 후 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-134">If hello resource is running as expected hello status of hello resource will update tooAvailable after a few minutes.</span></span>
* <span data-ttu-id="9c013-135">Hello 리소스에 문제가 발생 하는 경우 hello 알 수 없는 상태를 제안할 수 있습니다 hello 리소스 hello 플랫폼에서 이벤트에 의해 영향을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-135">If you are experiencing problems with hello resource, hello Unknown health status may suggest hello resource is impacted by an event in hello platform.</span></span>

![리소스 상태가 알 수 없음인 가상 컴퓨터](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="9c013-137">잘못된 상태 보고</span><span class="sxs-lookup"><span data-stu-id="9c013-137">Report an incorrect status</span></span>
<span data-ttu-id="9c013-138">클릭 하 여 알려 주십시오 수는 경우 언제 든 지 hello 현재 상태가 잘못 되었습니다., **잘못 된 상태를 보고**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-138">If at any point you believe hello current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="9c013-139">여기서 Azure 문제로 인해 영향을 받는 경우 좋습니다 hello 리소스 상태 블레이드에서 toocontact 지원을.</span><span class="sxs-lookup"><span data-stu-id="9c013-139">In cases where you are impacted by an Azure problem, we encourage you toocontact support from hello resource health blade.</span></span> 

![리소스 상태에서 잘못된 상태 보고](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="9c013-141">기록 정보</span><span class="sxs-lookup"><span data-stu-id="9c013-141">Historical Information</span></span>
<span data-ttu-id="9c013-142">클릭 하 여 too14 일 분량의 기록 상태 데이터를 액세스할 수 있습니다 **기록 보기** hello 리소스 상태 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-142">You can access up too14 days of historical health data by clicking **View History** in hello Resource health blade.</span></span> 

![리소스 상태 보고 기록](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="9c013-144">시작</span><span class="sxs-lookup"><span data-stu-id="9c013-144">Getting started</span></span>
<span data-ttu-id="9c013-145">tooopen 한 리소스에 대 한 리소스 상태</span><span class="sxs-lookup"><span data-stu-id="9c013-145">tooopen Resource health for one resource</span></span>
1.  <span data-ttu-id="9c013-146">Azure 포털 hello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-146">Sign in into hello Azure portal.</span></span>
2.  <span data-ttu-id="9c013-147">Tooyour 리소스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-147">Navigate tooyour resource.</span></span>
3.  <span data-ttu-id="9c013-148">Hello 왼쪽에 있는 hello 리소스 메뉴를 클릭 **리소스 상태**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-148">In hello resource menu located in hello left-hand side, click **Resource health**.</span></span>

![리소스 블레이드에서 리소스 상태 열기](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="9c013-150">리소스 상태를 클릭 하 여 액세스할 수도 있습니다 **더 많은 서비스**를 입력 하 고 **리소스 상태** 필터 텍스트 상자 tooopen hello에 **도움말 + 지원** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box tooopen hello **Help + Support** blade.</span></span> <span data-ttu-id="9c013-151">마지막으로 [**리소스 상태**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c013-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![추가 서비스에서 리소스 상태 열기](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="9c013-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c013-153">Next steps</span></span>

<span data-ttu-id="9c013-154">이러한 리소스 toolearn 리소스 상태에 대해 자세히 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="9c013-154">Check out these resources toolearn more about resource health:</span></span>
-  [<span data-ttu-id="9c013-155">Azure Resource Health에서 리소스 유형 및 상태 검사</span><span class="sxs-lookup"><span data-stu-id="9c013-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="9c013-156">Azure Resource Health에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="9c013-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




