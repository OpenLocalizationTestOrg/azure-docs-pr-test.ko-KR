---
title: "aaaAzure IoT 허브 IP 연결 필터 | Microsoft Docs"
description: "특정 IP에서 tooblock 연결 필터링 toouse IP 해결 하는 방법을 tooyour Azure IoT 허브에 대 한 합니다. 개별 또는 IP 주소 범위에서 연결을 차단할 수 있습니다."
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="fc579-104">IP 필터 사용</span><span class="sxs-lookup"><span data-stu-id="fc579-104">Use IP filters</span></span>

<span data-ttu-id="fc579-105">보안은 Azure IoT Hub를 기반으로 하는 모든 IoT 솔루션의 중요한 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="fc579-106">Tooexplicitly 필요한 경우에 따라 보안 구성의 일부로 장치 연결할 수는 hello IP 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-106">Sometimes you need tooexplicitly specify hello IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="fc579-107">hello _IP 필터_ 거부 하거나 특정 IPv4 주소에서 트래픽을 받아들이고에 대 한 tooconfigure 규칙 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-107">hello _IP filter_ feature enables you tooconfigure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-toouse"></a><span data-ttu-id="fc579-108">때 toouse</span><span class="sxs-lookup"><span data-stu-id="fc579-108">When toouse</span></span>

<span data-ttu-id="fc579-109">특정 IP 주소에 대 한 유용한 tooblock hello IoT Hub 끝점을 되었을 때에 두 개의 특정 사용 사례:</span><span class="sxs-lookup"><span data-stu-id="fc579-109">There are two specific use-cases when it is useful tooblock hello IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="fc579-110">IoT Hub가 지정된 범위의 IP 주소에서 오는 트래픽만 수신하고 그 밖의 트래픽은 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="fc579-111">IoT 허브를 사용 하는 예를 들어 [Azure Express 경로] toocreate IoT hub와 온-프레미스 인프라 간에 개인 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-111">For example, you are using your IoT hub with [Azure Express Route] toocreate private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="fc579-112">IoT 허브 관리자에 게 의심 스러운 것으로 확인 된 IP 주소에서 tooreject 트래픽이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-112">You need tooreject traffic from IP addresses that have been identified as suspicious by hello IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="fc579-113">필터 규칙이 적용되는 방식</span><span class="sxs-lookup"><span data-stu-id="fc579-113">How filter rules are applied</span></span>

<span data-ttu-id="fc579-114">hello IP 필터 규칙 hello IoT 허브 서비스 수준에서 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-114">hello IP filter rules are applied at hello IoT Hub service level.</span></span> <span data-ttu-id="fc579-115">따라서 hello IP 필터 규칙 tooall 연결 장치 및 모든 지원 되는 프로토콜을 사용 하 여 백 엔드 응용 프로그램에서 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-115">Therefore hello IP filter rules apply tooall connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="fc579-116">IoT Hub의 거부 IP 규칙에 일치하는 IP 주소에서 오는 모든 연결 시도는 권한 없음 401 상태 코드 및 설명을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="fc579-117">hello 응답 메시지는 hello IP 규칙을 언급 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-117">hello response message does not mention hello IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="fc579-118">기본 설정</span><span class="sxs-lookup"><span data-stu-id="fc579-118">Default setting</span></span>

<span data-ttu-id="fc579-119">기본적으로 hello **IP 필터** IoT 허브에 대 한 hello 포털에서 표는 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-119">By default, hello **IP Filter** grid in hello portal for an IoT hub is empty.</span></span> <span data-ttu-id="fc579-120">이러한 기본 설정은 허브가 모든 IP 주소의 연결을 수락한다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="fc579-121">이 기본 설정은 hello 0.0.0.0/0 IP 주소 범위를 허용 하는 해당 tooa 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-121">This default setting is equivalent tooa rule that accepts hello 0.0.0.0/0 IP address range.</span></span>

![IoT Hub 기본 IP 필터 설정][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="fc579-123">IP 필터 규칙 추가 또는 편집</span><span class="sxs-lookup"><span data-stu-id="fc579-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="fc579-124">IP 필터 규칙을 추가 하는 경우에 다음 값에는 hello에 대 한 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-124">When you add an IP filter rule, you are prompted for hello following values:</span></span>

- <span data-ttu-id="fc579-125">**IP 필터 규칙 이름** 하 too128 자를 고유한, 대/소문자 구분, 영숫자 문자열 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up too128 characters long.</span></span> <span data-ttu-id="fc579-126">Hello ASCII 7 비트 영숫자 문자만 더하기 `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-126">Only hello ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="fc579-127">선택 된 **거부** 또는 **수락** hello로 **동작** hello IP 필터 규칙에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-127">Select a **reject** or **accept** as hello **action** for hello IP filter rule.</span></span>
- <span data-ttu-id="fc579-128">단일 IPv4 주소 또는 CIDR 표기법으로 IP 주소 블록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="fc579-129">예를 들어 CIDR 표기법 192.168.100.0/22 나타냅니다 hello 1024 IPv4 주소에서 192.168.100.0이 고 too192.168.103.255 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-129">For example, in CIDR notation 192.168.100.0/22 represents hello 1024 IPv4 addresses from 192.168.100.0 too192.168.103.255.</span></span>

![IP 필터 규칙 tooan IoT hub 추가][img-ip-filter-add-rule]

<span data-ttu-id="fc579-131">Hello 규칙을 저장 하면 해당 hello 업데이트 진행에서 됨을 알리는 경고가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-131">After you save hello rule, you see an alert notifying you that hello update is in progress.</span></span>

![IP 필터 규칙 저장에 대한 알림][img-ip-filter-save-new-rule]

<span data-ttu-id="fc579-133">hello **추가** hello 최대 10 개의 IP 필터 규칙에 도달 하면 옵션은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-133">hello **Add** option is disabled when you reach hello maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="fc579-134">Hello 규칙을 포함 하는 hello 행을 두 번 클릭 하 여 기존 규칙을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-134">You can edit an existing rule by double-clicking hello row that contains hello rule.</span></span>

> [!NOTE]
> <span data-ttu-id="fc579-135">거부 된 IP 주소는 다른 Azure 서비스 (예: Azure Stream Analytics, Azure 가상 컴퓨터 또는 hello 포털에서 장치 탐색기 hello) hello IoT 허브와 상호 작용에서 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or hello Device Explorer in hello portal) from interacting with hello IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="fc579-136">IoT hub에서 Azure 스트림 분석 (ASA) tooread 메시지를 사용 하 여 IP 필터링이 활성화 된 경우 hello ASA 연결 문자열에에서 hello 이벤트 허브 호환 이름과 IoT Hub 끝점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-136">If you use Azure Stream Analytics (ASA) tooread messages from an IoT hub with IP filtering enabled, use hello Event Hub-compatible name and endpoint of your IoT Hub in hello ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="fc579-137">IP 필터 규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="fc579-137">Delete an IP filter rule</span></span>

<span data-ttu-id="fc579-138">toodelete IP 필터 규칙에 hello 그리드에서 하나 이상의 규칙 선택 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-138">toodelete an IP filter rule, select one or more rules in hello grid and click **Delete**.</span></span>

![IoT Hub IP 필터 규칙 삭제][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="fc579-140">IP 필터 규칙 평가</span><span class="sxs-lookup"><span data-stu-id="fc579-140">IP filter rule evaluation</span></span>

<span data-ttu-id="fc579-141">IP 필터 규칙 순서에 적용 되 고 hello hello hello IP 주소를 일치 하는 항목을 결정 하는 첫 번째 규칙 적용 하거나 작업을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-141">IP filter rules are applied in order and hello first rule that matches hello IP address determines hello accept or reject action.</span></span>

<span data-ttu-id="fc579-142">예를 들어 hello 범위 192.168.100.0/22에서 tooaccept 주소가 다른 모든 항목을 거부 하는 경우 hello 그리드에서 첫 번째 규칙 hello 주소 범위 192.168.100.0/22 hello를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-142">For example, if you want tooaccept addresses in hello range 192.168.100.0/22 and reject everything else, hello first rule in hello grid should accept hello address range 192.168.100.0/22.</span></span> <span data-ttu-id="fc579-143">다음 규칙 hello hello 범위 0.0.0.0/0을 사용 하 여 모든 주소를 거부 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-143">hello next rule should reject all addresses by using hello range 0.0.0.0/0.</span></span>

<span data-ttu-id="fc579-144">Hello 점 세 개 세로 hello 시작 되는 행을 클릭 하 고 끌어서를 사용 하 여 hello 표에에서는 IP 필터 규칙의 hello 순서를 변경 하 고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-144">You can change hello order of your IP filter rules in hello grid by clicking hello three vertical dots at hello start of a row and using drag and drop.</span></span>

<span data-ttu-id="fc579-145">toosave 새 IP 필터링 규칙 순서를 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="fc579-145">toosave your new IP filter rule order, click **Save**.</span></span>

![IoT 허브 IP 필터 규칙의 hello 순서 변경][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="fc579-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fc579-147">Next steps</span></span>

<span data-ttu-id="fc579-148">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fc579-148">toofurther explore hello capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="fc579-149">[작업 모니터링][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="fc579-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="fc579-150">[IoT Hub 메트릭][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="fc579-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Express 경로]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md