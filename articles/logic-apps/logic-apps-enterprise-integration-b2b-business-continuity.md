---
title: "B2B 통합 계정-Azure 논리 앱에 대 한 복구 aaaDisaster | Microsoft Docs"
description: "Logic Apps B2B 재해 복구"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a><span data-ttu-id="e5361-103">Logic Apps B2B 지역 간 재해 복구</span><span class="sxs-lookup"><span data-stu-id="e5361-103">Logic Apps B2B cross-region disaster recovery</span></span>

<span data-ttu-id="e5361-104">B2B 워크로드에는 주문 및 청구서와 같은 금전 거래가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-104">B2B workloads involve money transactions like orders and invoices.</span></span> <span data-ttu-id="e5361-105">이 재해 이벤트 동안 해당 파트너와 비즈니스 수준의 Sla 합의 한 비즈니스 tooquickly 복구 toomeet hello에 대 한 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-105">During a disaster event, it's critical for a business tooquickly recover toomeet hello business-level SLAs agreed upon with their partners.</span></span> <span data-ttu-id="e5361-106">이 문서에서는 비즈니스 연속성 toobuild B2B 작업에 대 한 계획 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-106">This article demonstrates how toobuild a business continuity plan for B2B workloads.</span></span> 

* <span data-ttu-id="e5361-107">재해 복구 준비</span><span class="sxs-lookup"><span data-stu-id="e5361-107">Disaster Recovery readiness</span></span> 
* <span data-ttu-id="e5361-108">재해 이벤트 중에 장애 조치 toosecondary 영역</span><span class="sxs-lookup"><span data-stu-id="e5361-108">Fail over toosecondary region during a disaster event</span></span> 
* <span data-ttu-id="e5361-109">재해 이벤트 후 tooprimary 지역 대체</span><span class="sxs-lookup"><span data-stu-id="e5361-109">Fall back tooprimary region after a disaster event</span></span>

## <a name="disaster-recovery-readiness"></a><span data-ttu-id="e5361-110">재해 복구 준비</span><span class="sxs-lookup"><span data-stu-id="e5361-110">Disaster Recovery readiness</span></span>  

1. <span data-ttu-id="e5361-111">보조 영역을 확인 및 만들기는 [통합 계정](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) hello 보조 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in hello secondary region.</span></span>

2. <span data-ttu-id="e5361-112">파트너, 스키마 및 필요한 hello 메시지 흐름에서 상태를 실행 하는 hello 해야 복제 toobe toosecondary 영역 통합 계정에 대 한 계약을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-112">Add partners, schemas, and agreements for hello required message flows where hello run status needs toobe replicated toosecondary region integration account.</span></span>

   > [!TIP]
   > <span data-ttu-id="e5361-113">지역에 걸쳐 hello 통합 계정 아티팩트 명명 규칙에 일관성 없는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-113">Make sure there's consistency in hello integration account artifact's naming convention across regions.</span></span> 

3. <span data-ttu-id="e5361-114">hello 기본 지역에서 실행 되는 상태 toopull hello는 hello 보조 지역에서 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-114">toopull hello run status from hello primary region, create a logic app in hello secondary region.</span></span> 

   <span data-ttu-id="e5361-115">논리 앱에 *트리거* 및 *작업*이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-115">This logic app should have a *trigger* and an *action*.</span></span> 
   <span data-ttu-id="e5361-116">hello 트리거 tooprimary 영역 통합 계정을 연결 해야 하 고 hello 동작 toosecondary 영역 통합 계정을 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-116">hello trigger should connect tooprimary region integration account, and hello action should connect toosecondary region integration account.</span></span> 
   <span data-ttu-id="e5361-117">Hello 시간 간격에 따라, hello 트리거 hello를 실행 하는 기본 지역 상태 테이블을 폴링하여 하 고 있는 경우 hello 새 레코드를 가져오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-117">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> <span data-ttu-id="e5361-118">hello 업데이트 동작을 toosecondary 지역 통합 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-118">hello action updates them toosecondary region integration account.</span></span> 
   <span data-ttu-id="e5361-119">이렇게 하면 기본 지역의 toosecondary 영역에서 tooget 증분 런타임 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-119">This helps tooget incremental runtime status from primary region toosecondary region.</span></span>

4. <span data-ttu-id="e5361-120">논리 앱 통합 계정이의 비즈니스 연속성 toosupport B2B 프로토콜-X12, AS2 및 EDIFACT에 따라 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-120">Business continuity in Logic Apps integration account is designed toosupport based on B2B protocols - X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="e5361-121">자세한 단계는 toofind, 선택 hello 각 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-121">toofind detailed steps, select hello respective links.</span></span>

5. <span data-ttu-id="e5361-122">권장 hello toodeploy 보조 지역에 있는 모든 기본 지역 리소스를 너무 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-122">hello recommendation is toodeploy all primary region resources in a secondary region too.</span></span> 

   <span data-ttu-id="e5361-123">기본 지역 리소스는 Azure SQL 데이터베이스 또는 Azure Cosmos DB, Azure 서비스 버스 및 메시징, Azure API 관리 및 Azure 앱 서비스의 hello Azure 논리 앱 기능에 사용 되는 Azure 이벤트 허브에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and hello Azure Logic Apps feature in Azure App Service.</span></span>   

6. <span data-ttu-id="e5361-124">기본 지역 tooa 보조 지역에서 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-124">Establish a connection from a primary region tooa secondary region.</span></span> <span data-ttu-id="e5361-125">기본 지역에서 실행 되는 상태 toopull hello 보조 지역에서 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-125">toopull hello run status from a primary region, create a logic app in a secondary region.</span></span> 

   <span data-ttu-id="e5361-126">hello 논리 앱 트리거와 작업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-126">hello logic app should have a trigger and an action.</span></span> 
   <span data-ttu-id="e5361-127">hello 트리거 tooa 기본 지역 통합 계정을 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-127">hello trigger should connect tooa primary region integration account.</span></span> 
   <span data-ttu-id="e5361-128">hello 동작 tooa 보조 지역 통합 계정을 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-128">hello action should connect tooa secondary region integration account.</span></span> 
   <span data-ttu-id="e5361-129">Hello 시간 간격에 따라, hello 트리거 hello를 실행 하는 기본 지역 상태 테이블을 폴링하여 하 고 있는 경우 hello 새 레코드를 가져오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-129">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> 
   <span data-ttu-id="e5361-130">hello 업데이트 동작을 tooa 보조 지역 통합 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-130">hello action updates them tooa secondary region integration account.</span></span> 
   <span data-ttu-id="e5361-131">이 프로세스는 hello 기본 지역 toohello 보조 지역에서 tooget 증분 런타임 상태를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-131">This process helps tooget incremental runtime status from hello primary region toohello secondary region.</span></span>

<span data-ttu-id="e5361-132">논리 앱 통합 계정에서의 비즈니스 연속성은 hello B2B 프로토콜 X12, AS2 및 EDIFACT에 따라 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-132">Business continuity in a Logic Apps integration account provides support based on hello B2B protocols X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="e5361-133">X12 및 AS2 사용에 대한 자세한 단계는 이 문서의 [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) 및 [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5361-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span></span>

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a><span data-ttu-id="e5361-134">재해 이벤트 중에 장애 조치 tooa 보조 지역</span><span class="sxs-lookup"><span data-stu-id="e5361-134">Fail over tooa secondary region during a disaster event</span></span>

<span data-ttu-id="e5361-135">재해 이벤트에서 hello 기본 지역 비즈니스 연속성, 트래픽 직접 toohello 보조 지역에 사용할 수 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="e5361-135">During a disaster event, when hello primary region is not available for business continuity, direct traffic toohello secondary region.</span></span> <span data-ttu-id="e5361-136">비즈니스 toorecover 함수 RPO/RTO 합의 toomeet hello를 해당 파트너에 의해 신속 하 게 보조 지역은 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-136">A secondary region helps a business toorecover functions quickly toomeet hello RPO/RTO agreed upon by their partners.</span></span> <span data-ttu-id="e5361-137">통해 노력 toofail 한 지역의 tooanother 영역에서 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-137">It also minimizes efforts toofail over from one region tooanother region.</span></span> 

<span data-ttu-id="e5361-138">기본 지역 tooa 보조 지역에서 제어 번호를 복사 하는 동안 예상 되는 대기 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-138">There is an expected latency while copying control numbers from a primary region tooa secondary region.</span></span> <span data-ttu-id="e5361-139">생성 된 중복 컨트롤 보내는 tooavoid 재해 이벤트 동안 toopartners를 숫자, hello 좋습니다 tooincrement hello 제어 번호 hello 보조 지역 계약에 사용 하 여 [PowerShell cmdlet](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-139">tooavoid sending duplicate generated control numbers toopartners during a disaster event, hello recommendation is tooincrement hello control numbers in hello secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a><span data-ttu-id="e5361-140">대체 tooa 기본 지역 재해 발생 후 이벤트</span><span class="sxs-lookup"><span data-stu-id="e5361-140">Fall back tooa primary region post-disaster event</span></span>

<span data-ttu-id="e5361-141">toofall 백 tooa 기본 지역, 사용 가능한 경우 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="e5361-141">toofall back tooa primary region when it is available, follow these steps:</span></span>

1. <span data-ttu-id="e5361-142">Hello 보조 지역에서 파트너 로부터 메시지를 수락을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-142">Stop accepting messages from partners in hello secondary region.</span></span>  

2. <span data-ttu-id="e5361-143">사용 하 여 모든 hello 기본 지역 계약에 대해 생성 된 hello 제어 번호를 하나씩 늘립니다. [PowerShell cmdlet](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-143">Increment hello generated control numbers for all hello primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>  

3. <span data-ttu-id="e5361-144">Hello 보조 지역 toohello 기본 지역에서 직접 트래픽입니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-144">Direct traffic from hello secondary region toohello primary region.</span></span>

4. <span data-ttu-id="e5361-145">Hello 기본 지역에서의 실행 상태를 추출 하는 데 hello 보조 지역에서 만든 hello 논리 앱 사용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-145">Check that hello logic app created in hello secondary region for pulling run status from hello primary region is enabled.</span></span>

## <a name="x12"></a><span data-ttu-id="e5361-146">X12</span><span class="sxs-lookup"><span data-stu-id="e5361-146">X12</span></span> 

<span data-ttu-id="e5361-147">EDI X12 문서의 비즈니스 연속성은 컨트롤 번호를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-147">Business continuity for EDI X12 documents is based on control numbers:</span></span>

> [!TIP]
> <span data-ttu-id="e5361-148">Hello를 사용할 수도 있습니다 [X12 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="e5361-148">You can also use hello [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps.</span></span> <span data-ttu-id="e5361-149">만드는 기본 및 보조 통합 계정에 필수 구성 요소 toouse hello 템플릿이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-149">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="e5361-150">hello 서식 파일에는 두 논리 앱 toocreate, 받은 제어 번호에 대 한 및 생성 된 제어 번호에 대 한 다른 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-150">hello template helps toocreate two logic apps, one for received control numbers and another for generated control numbers.</span></span> <span data-ttu-id="e5361-151">각 트리거 및 작업 hello 트리거 toohello 기본 통합 계정 및 hello 작업 toohello 보조 통합 계정 연결 되는 hello 논리 앱에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-151">Respective triggers and actions are created in hello logic apps, connecting hello trigger toohello primary integration account and hello action toohello secondary integration account.</span></span>

<span data-ttu-id="e5361-152">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="e5361-152">**Prerequisites**</span></span>

<span data-ttu-id="e5361-153">인바운드 메시지에 대 한 재해 복구 tooenable hello X12 규약의 수신 설정에 hello 중복 검사 설정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-153">tooenable disaster recovery for inbound messages, select hello duplicate check settings in hello X12 agreement's Receive Settings.</span></span>

![중복된 검사 설정 선택](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. <span data-ttu-id="e5361-155">보조 지역에 [논리 앱](../logic-apps/logic-apps-create-a-logic-app.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-155">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="e5361-156">**X12**를 검색하고 **X12 - 컨트롤 번호가 수정되었을 때**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-156">Search on **X12**, and select **X12 - When a control number is modified**.</span></span>   

   ![X12 검색](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   <span data-ttu-id="e5361-158">hello 트리거 tooestablish 연결 tooan 통합 계정 라는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-158">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="e5361-159">hello 트리거는 반드시 tooa 기본 지역 통합 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-159">hello trigger should be connected tooa primary region integration account.</span></span>

3. <span data-ttu-id="e5361-160">연결 이름을 입력을 선택 하면 *기본 지역 통합 계정* hello에서 목록을 연 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-160">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>   

   ![주 지역 통합 계정 이름](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. <span data-ttu-id="e5361-162">hello **DateTime toostart 제어 번호 동기화** 설정은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-162">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="e5361-163">hello **주파수** 너무 설정할 수 있습니다**일**, **시간**, **분**, 또는 **두 번째** 간격을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-163">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![날짜/시간 및 빈도](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. <span data-ttu-id="e5361-165">**새 단계** > **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-165">Select **New step** > **Add an action**.</span></span>

   ![새 단계 후 작업 추가](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. <span data-ttu-id="e5361-167">**X12**를 검색하고 **X12 - 컨트롤 번호 추가 또는 업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span></span>   

   ![제어 번호를 추가 또는 업데이트](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. <span data-ttu-id="e5361-169">tooconnect 작업 tooa 보조 지역 통합 계정 선택 **연결 변경** > **새 연결 추가** hello 사용할 수 있는 통합 계정 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-169">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="e5361-170">연결 이름을 입력을 선택 하면 *통합 계정 보조 지역* hello에서 목록을 연 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-170">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span> 

   ![보조 지역 통합 계정 이름](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. <span data-ttu-id="e5361-172">오른쪽 위 모서리에서 hello 아이콘을 클릭 하 여 tooraw 입력을 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-172">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Tooraw 입력을 전환](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. <span data-ttu-id="e5361-174">Hello 동적 콘텐츠 선택기에서 본문을 선택 하 고 hello 논리 앱을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-174">Select Body from hello dynamic content picker, and save hello logic app.</span></span>

   ![동적 콘텐츠 필드](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   <span data-ttu-id="e5361-176">Hello 시간 간격에 따라, hello hello 수신 하는 기본 지역 제어 번호 테이블을 폴링합니다 트리거와 hello 새 레코드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-176">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span> 
   <span data-ttu-id="e5361-177">hello 보조 지역 통합 계정에 hello 레코드를 업데이트 하는 hello 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-177">hello action updates hello records in hello secondary region integration account.</span></span> 
   <span data-ttu-id="e5361-178">업데이트가 없습니다 hello 트리거 상태 표시 **건너뜀**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-178">If there are no updates, hello trigger status appears as **Skipped**.</span></span>   

   ![컨트롤 번호 테이블](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="e5361-180">Hello 증분 런타임 상태 hello 시간 간격에 따라, 기본 지역 tooa 보조 지역에서 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-180">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="e5361-181">재해 이벤트에서 hello 기본 지역 비즈니스 연속성을 위한 toohello 보조 지역 트래픽을 직접 사용할 수 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="e5361-181">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="edifact"></a><span data-ttu-id="e5361-182">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="e5361-182">EDIFACT</span></span> 

<span data-ttu-id="e5361-183">EDI EDIFACT 문서의 비즈니스 연속성은 컨트롤 번호를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span></span>

<span data-ttu-id="e5361-184">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="e5361-184">**Prerequisites**</span></span>

<span data-ttu-id="e5361-185">인바운드 메시지에 대 한 재해 복구 tooenable EDIFACT 규약의 수신 설정에 hello 중복 검사 설정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-185">tooenable disaster recovery for inbound messages, select hello duplicate check settings in your EDIFACT agreement's Receive Settings.</span></span>

![중복된 검사 설정 선택](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. <span data-ttu-id="e5361-187">보조 지역에 [논리 앱](../logic-apps/logic-apps-create-a-logic-app.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-187">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="e5361-188">**EDIFACT**를 검색하고 **EDIFACT - 컨트롤 번호가 수정되는 경우**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span></span>

   ![EDIFACT 검색](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   <span data-ttu-id="e5361-190">hello 트리거 tooestablish 연결 tooan 통합 계정 라는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-190">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="e5361-191">hello 트리거는 반드시 tooa 기본 지역 통합 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-191">hello trigger should be connected tooa primary region integration account.</span></span> 

3. <span data-ttu-id="e5361-192">연결 이름을 입력을 선택 하면 *기본 지역 통합 계정* hello에서 목록을 연 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-192">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>    

   ![주 지역 통합 계정 이름](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. <span data-ttu-id="e5361-194">hello **DateTime toostart 제어 번호 동기화** 설정은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-194">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="e5361-195">hello **주파수** 너무 설정할 수 있습니다**일**, **시간**, **분**, 또는 **두 번째** 간격을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-195">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    

   ![날짜/시간 및 빈도](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. <span data-ttu-id="e5361-197">**새 단계** > **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-197">Select **New step** > **Add an action**.</span></span>    

   ![새 단계 후 작업 추가](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. <span data-ttu-id="e5361-199">**EDIFACT**를 검색하고 **EDIFACT - 컨트롤 번호 추가 또는 업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span></span>   

   ![제어 번호를 추가 또는 업데이트](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. <span data-ttu-id="e5361-201">tooconnect 작업 tooa 보조 지역 통합 계정 선택 **연결 변경** > **새 연결 추가** hello 사용할 수 있는 통합 계정 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-201">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="e5361-202">연결 이름을 입력을 선택 하면 *통합 계정 보조 지역* hello에서 목록을 연 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-202">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![보조 지역 통합 계정 이름](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. <span data-ttu-id="e5361-204">오른쪽 위 모서리에서 hello 아이콘을 클릭 하 여 tooraw 입력을 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-204">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Tooraw 입력을 전환](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. <span data-ttu-id="e5361-206">Hello 동적 콘텐츠 선택기에서 본문을 선택 하 고 hello 논리 앱을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-206">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![동적 콘텐츠 필드](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   <span data-ttu-id="e5361-208">Hello 시간 간격에 따라, hello hello 수신 하는 기본 지역 제어 번호 테이블을 폴링합니다 트리거와 hello 새 레코드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-208">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span>
   <span data-ttu-id="e5361-209">hello 레코드 toohello 보조 지역 통합 계정을 업데이트 하는 hello 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-209">hello action updates hello records toohello secondary region integration account.</span></span> 
   <span data-ttu-id="e5361-210">업데이트가 없습니다 hello 트리거 상태 표시 **건너뜀**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-210">If there are no updates, hello trigger status appears as **Skipped**.</span></span>

   ![컨트롤 번호 테이블](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="e5361-212">Hello 증분 런타임 상태 hello 시간 간격에 따라, 기본 지역 tooa 보조 지역에서 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-212">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="e5361-213">재해 이벤트에서 hello 기본 지역 비즈니스 연속성을 위한 toohello 보조 지역 트래픽을 직접 사용할 수 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="e5361-213">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="e5361-214">AS2</span><span class="sxs-lookup"><span data-stu-id="e5361-214">AS2</span></span> 

<span data-ttu-id="e5361-215">Hello AS2 프로토콜을 사용 하는 문서에 대 한 비즈니스 연속성은 hello 메시지 ID와 hello MIC 값을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-215">Business continuity for documents that use hello AS2 protocol is based on hello message ID and hello MIC value.</span></span>

> [!TIP]
> <span data-ttu-id="e5361-216">Hello를 사용할 수도 있습니다 [AS2 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="e5361-216">You can also use hello [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps.</span></span> <span data-ttu-id="e5361-217">만드는 기본 및 보조 통합 계정에 필수 구성 요소 toouse hello 템플릿이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-217">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="e5361-218">hello 서식 파일을 트리거와 작업을 갖춘 논리 앱을 만들기를 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-218">hello template helps create a logic app that has a trigger and an action.</span></span> <span data-ttu-id="e5361-219">hello 논리 앱 트리거 tooa 기본 통합 계정 및 작업 tooa 보조 통합 계정에서 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-219">hello logic app creates a connection from a trigger tooa primary integration account and an action tooa secondary integration account.</span></span>

1. <span data-ttu-id="e5361-220">만들기는 [논리 앱](../logic-apps/logic-apps-create-a-logic-app.md) hello 보조 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-220">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in hello secondary region.</span></span>  

2. <span data-ttu-id="e5361-221">**AS2**를 검색하고 **AS2 - MIC 값이 만들어질 때**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span></span>   

   ![AS2 검색](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   <span data-ttu-id="e5361-223">트리거 메시지 tooestablish 연결 tooan 통합 계정을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-223">A trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="e5361-224">hello 트리거는 반드시 tooa 기본 지역 통합 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-224">hello trigger should be connected tooa primary region integration account.</span></span> 
   
3. <span data-ttu-id="e5361-225">연결 이름을 입력을 선택 하면 *기본 지역 통합 계정* hello에서 목록을 연 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-225">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>

   ![주 지역 통합 계정 이름](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. <span data-ttu-id="e5361-227">hello **DateTime toostart MIC 값 동기화** 설정은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-227">hello **DateTime toostart MIC value sync** setting is optional.</span></span> <span data-ttu-id="e5361-228">hello **주파수** 너무 설정할 수 있습니다**일**, **시간**, **분**, 또는 **두 번째** 간격을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-228">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![날짜/시간 및 빈도](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. <span data-ttu-id="e5361-230">**새 단계** > **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-230">Select **New step** > **Add an action**.</span></span>  

   ![새 단계 후 작업 추가](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. <span data-ttu-id="e5361-232">**AS2**를 검색하고 **AS2 - MIC 콘텐츠 추가 또는 업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span></span>  

   ![MIC 추가 또는 업데이트](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. <span data-ttu-id="e5361-234">tooconnect 작업 tooa 보조 통합 계정 선택 **연결 변경** > **새 연결 추가** hello 사용할 수 있는 통합 계정 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-234">tooconnect an action tooa secondary integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="e5361-235">연결 이름을 입력을 선택 하면 *통합 계정 보조 지역* hello에서 목록을 연 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-235">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![보조 지역 통합 계정 이름](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. <span data-ttu-id="e5361-237">오른쪽 위 모서리에서 hello 아이콘을 클릭 하 여 tooraw 입력을 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-237">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Tooraw 입력을 전환](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. <span data-ttu-id="e5361-239">Hello 동적 콘텐츠 선택기에서 본문을 선택 하 고 hello 논리 앱을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-239">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![동적 콘텐츠](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   <span data-ttu-id="e5361-241">Hello 시간 간격에 따라, hello 트리거 hello 기본 지역 테이블 폴링한 hello 새 레코드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-241">Based on hello time interval, hello trigger polls hello primary region table and pulls hello new records.</span></span> <span data-ttu-id="e5361-242">hello 업데이트 동작을 toohello 보조 지역 통합 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-242">hello action updates them toohello secondary region integration account.</span></span> 
   <span data-ttu-id="e5361-243">업데이트가 없습니다 hello 트리거 상태 표시 **건너뜀**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-243">If there are no updates, hello trigger status appears as **Skipped**.</span></span>  

   ![주 지역 테이블](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

<span data-ttu-id="e5361-245">Hello 증분 런타임 상태 hello 시간 간격에 따라, hello 기본 지역 toohello 보조 지역에서 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5361-245">Based on hello time interval, hello incremental runtime status replicates from hello primary region toohello secondary region.</span></span> <span data-ttu-id="e5361-246">재해 이벤트에서 hello 기본 지역 비즈니스 연속성을 위한 toohello 보조 지역 트래픽을 직접 사용할 수 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="e5361-246">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e5361-247">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e5361-247">Next steps</span></span>

[<span data-ttu-id="e5361-248">B2B 메시지 모니터링</span><span class="sxs-lookup"><span data-stu-id="e5361-248">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md)

