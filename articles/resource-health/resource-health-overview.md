---
title: "Azure 리소스 상태 개요 | Microsoft Docs"
description: "Azure 리소스 상태 개요"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: d54979995ca97a70ba92c64915b919da09f548ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="42727-103">Azure Resource Health 개요</span><span class="sxs-lookup"><span data-stu-id="42727-103">Azure resource health overview</span></span>
 
<span data-ttu-id="42727-104">Resource Health는 Azure 문제가 리소스에 영향을 주는 경우 진단 및 지원을 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="42727-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="42727-105">리소스의 현재 및 이전 상태에 대해 알려주고 문제를 완화하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42727-105">It informs you about the current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="42727-106">Resource Health는 Azure 서비스 문제와 관련된 도움이 필요할 때 기술 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="42727-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="42727-107">[Azure 상태](https://status.azure.com)는 광범위한 고객 집합에 영향을 주는 서비스 문제를 알려주지만, 리소스 상태는 리소스의 상태에 대한 개인 설정된 대시보드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="42727-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of the health of your resources.</span></span> <span data-ttu-id="42727-108">리소스 상태는 Azure 서비스 문제로 인해 과거에 리소스를 사용할 수 없었던 모든 시간을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="42727-108">Resource health shows you all the times your resources were unavailable in the past due to Azure service issues.</span></span> <span data-ttu-id="42727-109">따라서 SLA를 위반하였는지 파악하기가 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="42727-109">This makes it simple for you to understand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="42727-110">무엇이 리소스로 간주되고 리소스 상태에서는 리소스가 정상인지를 어떻게 결정하나요?</span><span class="sxs-lookup"><span data-stu-id="42727-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="42727-111">리소스는 가상 컴퓨터, 웹앱 또는 SQL Database처럼 Azure Resource Manager를 통해 Azure 서비스에서 제공하는 리소스 유형의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="42727-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="42727-112">리소스 상태는 다양한 Azure 서비스에서 내보낸 신호에 의존하여 리소스가 정상인지를 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="42727-112">Resource health relies on signals emitted by the different Azure services to assess if a resource is healthy or not.</span></span> <span data-ttu-id="42727-113">리소스가 정상이 아니면 리소스 상태에서 추가 정보를 분석하여 문제 원인을 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="42727-113">If a resource is unhealthy, resource health analyzes additional information to determine the source of the problem.</span></span> <span data-ttu-id="42727-114">또한 Microsoft가 문제를 해결하기 위해 수행하는 작업 또는 문제의 원인을 해결하기 위해 수행할 수 있는 작업도 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="42727-114">It also identifies actions Microsoft is taking to fix the issue or what actions you can take to address the cause of the problem.</span></span> 

<span data-ttu-id="42727-115">상태를 평가하는 방법에 대한 자세한 내용은 [Azure Resource Health](resource-health-checks-resource-types.md)에서 리소스 유형 및 상태 검사에 대한 전체 목록을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="42727-115">Review the full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="42727-116">리소스 상태에서 제공하는 상태</span><span class="sxs-lookup"><span data-stu-id="42727-116">Health status provided by resource health</span></span>
<span data-ttu-id="42727-117">리소스 상태는 다음 상태 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="42727-117">The health of a resource is one of the following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="42727-118">사용 가능</span><span class="sxs-lookup"><span data-stu-id="42727-118">Available</span></span>
<span data-ttu-id="42727-119">서비스에서 리소스 상태에 영향을 주는 어떠한 이벤트도 감지하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="42727-119">The service has not detected any events impacting the health of the resource.</span></span> <span data-ttu-id="42727-120">리소스가 최근 24시간 동안 계획되지 않은 가동 중지 시간에서 복구된 경우 **최근 복구된** 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="42727-120">In cases where the resource has recovered from unplanned downtime during the last 24 hours you will see the **recently recovered** notification.</span></span>

![리소스 상태가 사용 가능한 가상 컴퓨터](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="42727-122">사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="42727-122">Unavailable</span></span>
<span data-ttu-id="42727-123">서비스에서 리소스 상태에 영향을 주는 진행 중인 플랫폼 또는 비-플랫폼 이벤트를 감지했습니다.</span><span class="sxs-lookup"><span data-stu-id="42727-123">The service has detected an ongoing platform or non-platform event impacting the health of the resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="42727-124">플랫폼 이벤트</span><span class="sxs-lookup"><span data-stu-id="42727-124">Platform events</span></span>
<span data-ttu-id="42727-125">이러한 이벤트는 Azure 인프라의 여러 구성 요소에 의해 트리거되며 계획된 유지 관리와 같은 예약된 작업과 계획되지 않은 호스트 재부팅과 같은 예기치 않은 인시던트를 모두 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="42727-125">These events are triggered by multiple components of the Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="42727-126">리소스 상태는 이벤트 및 복구 프로세스에 대한 추가 세부 정보를 제공하며 사용 중인 Microsoft 지원 계약이 없더라도 지원 담당자에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42727-126">Resource health provides additional details on the event, the recovery process and enables you to contact support even if you don't have an active Microsoft support agreement.</span></span>

![플랫폼 이벤트로 인해 리소스 상태가 사용 불가능한 가상 컴퓨터](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="42727-128">비-플랫폼 이벤트</span><span class="sxs-lookup"><span data-stu-id="42727-128">Non-Platform events</span></span>
<span data-ttu-id="42727-129">이러한 이벤트는 사용자가 수행한 작업(예: 가상 컴퓨터 중지 또는 Redis Cache에 대한 최대 연결 수 도달)에 의해 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="42727-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching the maximum number of connections to a Redis Cache.</span></span>

![비-플랫폼 이벤트로 인해 리소스 상태가 사용 불가능한 가상 컴퓨터](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="42727-131">알 수 없음</span><span class="sxs-lookup"><span data-stu-id="42727-131">Unknown</span></span>
<span data-ttu-id="42727-132">이 상태 정보는 리소스 상태에서 10분 이상 이 리소스에 대한 정보를 수신하지 못했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="42727-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="42727-133">이 상태는 리소스 상태에 대한 명확한 표시는 아니지만 문제 해결 프로세스의 중요한 데이터 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="42727-133">While this status is not a definitive indication of the state of the resource, it is an important data point in the troubleshooting process:</span></span>
* <span data-ttu-id="42727-134">리소스가 예상한 대로 실행되면 몇 분 후 리소스 상태가 사용 가능으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="42727-134">If the resource is running as expected the status of the resource will update to Available after a few minutes.</span></span>
* <span data-ttu-id="42727-135">리소스에 문제가 발생하는 경우 알 수 없음 상태로 플랫폼의 이벤트에 의해 리소스가 영향을 받음을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42727-135">If you are experiencing problems with the resource, the Unknown health status may suggest the resource is impacted by an event in the platform.</span></span>

![리소스 상태가 알 수 없음인 가상 컴퓨터](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="42727-137">잘못된 상태 보고</span><span class="sxs-lookup"><span data-stu-id="42727-137">Report an incorrect status</span></span>
<span data-ttu-id="42727-138">어느 시점에서 현재 상태가 잘못되었다고 생각되면 **Report incorrect health status(잘못된 상태 보고)**를 클릭하여 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="42727-138">If at any point you believe the current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="42727-139">Azure 문제의 영향을 받는 경우 리소스 상태 블레이드에서 지원 담당자에게 문의하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="42727-139">In cases where you are impacted by an Azure problem, we encourage you to contact support from the resource health blade.</span></span> 

![리소스 상태에서 잘못된 상태 보고](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="42727-141">기록 정보</span><span class="sxs-lookup"><span data-stu-id="42727-141">Historical Information</span></span>
<span data-ttu-id="42727-142">리소스 상태 블레이드에서 **기록 보기**를 클릭하여 최대 14일 동안의 기록 상태 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42727-142">You can access up to 14 days of historical health data by clicking **View History** in the Resource health blade.</span></span> 

![리소스 상태 보고 기록](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="42727-144">시작</span><span class="sxs-lookup"><span data-stu-id="42727-144">Getting started</span></span>
<span data-ttu-id="42727-145">하나의 리소스에 대한 리소스 상태를 열려면</span><span class="sxs-lookup"><span data-stu-id="42727-145">To open Resource health for one resource</span></span>
1.  <span data-ttu-id="42727-146">Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="42727-146">Sign in into the Azure portal.</span></span>
2.  <span data-ttu-id="42727-147">리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="42727-147">Navigate to your resource.</span></span>
3.  <span data-ttu-id="42727-148">왼쪽에 있는 리소스 메뉴에서 **리소스 상태**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42727-148">In the resource menu located in the left-hand side, click **Resource health**.</span></span>

![리소스 블레이드에서 리소스 상태 열기](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="42727-150">**추가 서비스**를 클릭하고 필터 텍스트 상자에서 **리소스 상태**를 입력하여 **도움말 + 지원** 블레이드를 열어 리소스 상태에 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42727-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box to open the **Help + Support** blade.</span></span> <span data-ttu-id="42727-151">마지막으로 [**리소스 상태**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42727-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![추가 서비스에서 리소스 상태 열기](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="42727-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="42727-153">Next steps</span></span>

<span data-ttu-id="42727-154">리소스 상태에 대한 자세한 내용은 다음 리소스를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="42727-154">Check out these resources to learn more about resource health:</span></span>
-  [<span data-ttu-id="42727-155">Azure Resource Health에서 리소스 유형 및 상태 검사</span><span class="sxs-lookup"><span data-stu-id="42727-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="42727-156">Azure Resource Health에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="42727-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




