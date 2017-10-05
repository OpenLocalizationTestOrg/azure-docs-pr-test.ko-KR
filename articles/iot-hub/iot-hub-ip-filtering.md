---
title: "Azure IoT Hub IP 연결 필터 | Microsoft Docs"
description: "특정 IP 주소에서 Azure IoT hub로 연결을 차단하도록 IP 필터링을 사용하는 방법입니다. 개별 또는 IP 주소 범위에서 연결을 차단할 수 있습니다."
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
ms.openlocfilehash: 85f5f044faddd5180f0c19d3f2c235b20f6373d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="56740-104">IP 필터 사용</span><span class="sxs-lookup"><span data-stu-id="56740-104">Use IP filters</span></span>

<span data-ttu-id="56740-105">보안은 Azure IoT Hub를 기반으로 하는 모든 IoT 솔루션의 중요한 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="56740-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="56740-106">경우에 따라 장치가 보안 구성의 일부로 연결할 수 있는 IP 주소를 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56740-106">Sometimes you need to explicitly specify the IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="56740-107">_IP 필터_ 기능을 사용하면 특정 IPv4 주소에서 들어오는 트래픽을 거부하거나 수락하는 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56740-107">The _IP filter_ feature enables you to configure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-to-use"></a><span data-ttu-id="56740-108">사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="56740-108">When to use</span></span>

<span data-ttu-id="56740-109">특정 IP 주소에 대해 IoT Hub 끝점을 차단하는 것이 유용한 두 가지 사용 사례가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56740-109">There are two specific use-cases when it is useful to block the IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="56740-110">IoT Hub가 지정된 범위의 IP 주소에서 오는 트래픽만 수신하고 그 밖의 트래픽은 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="56740-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="56740-111">예를 들어 IoT Hub를 [Azure ExpressRoute]와 사용하여 IoT Hub와 온-프레미스 인프라 간의 개인 연결을 만드는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="56740-111">For example, you are using your IoT hub with [Azure Express Route] to create private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="56740-112">IoT Hub 관리자에 의해 의심스러운 것으로 식별된 IP 주소에서 오는 트래픽을 거부해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56740-112">You need to reject traffic from IP addresses that have been identified as suspicious by the IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="56740-113">필터 규칙이 적용되는 방식</span><span class="sxs-lookup"><span data-stu-id="56740-113">How filter rules are applied</span></span>

<span data-ttu-id="56740-114">IP 필터 규칙은 IoT Hub 서비스 수준에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56740-114">The IP filter rules are applied at the IoT Hub service level.</span></span> <span data-ttu-id="56740-115">따라서 IP 필터 규칙은 지원되는 모든 프로토콜을 사용하는 장치 및 백 엔드 앱의 모든 연결에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56740-115">Therefore the IP filter rules apply to all connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="56740-116">IoT Hub의 거부 IP 규칙에 일치하는 IP 주소에서 오는 모든 연결 시도는 권한 없음 401 상태 코드 및 설명을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="56740-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="56740-117">응답 메시지는 IP 규칙을 언급하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56740-117">The response message does not mention the IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="56740-118">기본 설정</span><span class="sxs-lookup"><span data-stu-id="56740-118">Default setting</span></span>

<span data-ttu-id="56740-119">기본적으로 IoT Hub에 대한 포털의 **IP 필터** 그리드는 비어있습니다.</span><span class="sxs-lookup"><span data-stu-id="56740-119">By default, the **IP Filter** grid in the portal for an IoT hub is empty.</span></span> <span data-ttu-id="56740-120">이러한 기본 설정은 허브가 모든 IP 주소의 연결을 수락한다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="56740-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="56740-121">이러한 기본 설정은 0.0.0.0/0 IP 주소 범위를 수락하는 규칙과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56740-121">This default setting is equivalent to a rule that accepts the 0.0.0.0/0 IP address range.</span></span>

![IoT Hub 기본 IP 필터 설정][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="56740-123">IP 필터 규칙 추가 또는 편집</span><span class="sxs-lookup"><span data-stu-id="56740-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="56740-124">IP 필터 규칙을 추가하는 경우 다음 값을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="56740-124">When you add an IP filter rule, you are prompted for the following values:</span></span>

- <span data-ttu-id="56740-125">**IP 필터 규칙 이름**은 최대 128자의 대/소문자를 구분하지 않는 영숫자 문자열로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56740-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up to 128 characters long.</span></span> <span data-ttu-id="56740-126">ASCII 7 비트 영숫자 및 `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}`만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56740-126">Only the ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="56740-127">IP 필터 규칙에 대한 **작업**으로 **거부** 또는 **수락**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56740-127">Select a **reject** or **accept** as the **action** for the IP filter rule.</span></span>
- <span data-ttu-id="56740-128">단일 IPv4 주소 또는 CIDR 표기법으로 IP 주소 블록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56740-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="56740-129">예를 들어 CIDR 표기법 192.168.100.0/22는 192.168.100.0에서 192.168.103.255까지 IPv4 주소 1024개를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="56740-129">For example, in CIDR notation 192.168.100.0/22 represents the 1024 IPv4 addresses from 192.168.100.0 to 192.168.103.255.</span></span>

![IP 필터 규칙을 IoT Hub에 추가][img-ip-filter-add-rule]

<span data-ttu-id="56740-131">규칙을 저장한 후 업데이트를 진행 중이라고 알려주는 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="56740-131">After you save the rule, you see an alert notifying you that the update is in progress.</span></span>

![IP 필터 규칙 저장에 대한 알림][img-ip-filter-save-new-rule]

<span data-ttu-id="56740-133">최대 10개의 IP 필터 규칙에 도달하면 **추가** 옵션이 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="56740-133">The **Add** option is disabled when you reach the maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="56740-134">규칙을 포함하는 행을 두 번 클릭하면 기존 규칙을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56740-134">You can edit an existing rule by double-clicking the row that contains the rule.</span></span>

> [!NOTE]
> <span data-ttu-id="56740-135">IP 주소를 거부하면 다른 Azure 서비스(예: Azure Stream Analytics, Azure Virtual Machines 또는 포털의 장치 탐색기)가 IoT Hub와 상호 작용하는 것을 막을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56740-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or the Device Explorer in the portal) from interacting with the IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="56740-136">ASA(Azure Stream Analytics)를 사용하여 IP 필터링이 활성화된 IoT Hub에서 메시지를 읽는 경우 ASA 연결 문자열에 이벤트 허브와 호환되는 IoT Hub 이름 및 끝점을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56740-136">If you use Azure Stream Analytics (ASA) to read messages from an IoT hub with IP filtering enabled, use the Event Hub-compatible name and endpoint of your IoT Hub in the ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="56740-137">IP 필터 규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="56740-137">Delete an IP filter rule</span></span>

<span data-ttu-id="56740-138">IP 필터 규칙을 삭제하려면 그리드에서 규칙을 하나 이상 선택하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56740-138">To delete an IP filter rule, select one or more rules in the grid and click **Delete**.</span></span>

![IoT Hub IP 필터 규칙 삭제][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="56740-140">IP 필터 규칙 평가</span><span class="sxs-lookup"><span data-stu-id="56740-140">IP filter rule evaluation</span></span>

<span data-ttu-id="56740-141">IP 필터 규칙은 순서대로 적용되며 IP 주소와 일치하는 첫 번째 규칙이 수락 또는 거부 작업을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="56740-141">IP filter rules are applied in order and the first rule that matches the IP address determines the accept or reject action.</span></span>

<span data-ttu-id="56740-142">예를 들어 192.168.100.0/22 범위의 주소를 수락하고 그 외의 주소는 거부하려는 경우 그리드에 있는 첫 번째 규칙이 주소 범위 192.168.100.0/22를 수락해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56740-142">For example, if you want to accept addresses in the range 192.168.100.0/22 and reject everything else, the first rule in the grid should accept the address range 192.168.100.0/22.</span></span> <span data-ttu-id="56740-143">다음 규칙은 0.0.0.0/0 범위를 사용하여 모든 주소를 거부해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56740-143">The next rule should reject all addresses by using the range 0.0.0.0/0.</span></span>

<span data-ttu-id="56740-144">행의 시작 부분에 있는 세 개의 세로 점을 클릭하고 끌어서 놓기를 사용하여 그리드에서 IP 필터 규칙의 순서를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56740-144">You can change the order of your IP filter rules in the grid by clicking the three vertical dots at the start of a row and using drag and drop.</span></span>

<span data-ttu-id="56740-145">새 IP 필터 규칙 순서를 저장하려면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56740-145">To save your new IP filter rule order, click **Save**.</span></span>

![IoT Hub IP 필터 규칙의 순서 변경][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="56740-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="56740-147">Next steps</span></span>

<span data-ttu-id="56740-148">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56740-148">To further explore the capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="56740-149">[작업 모니터링][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="56740-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="56740-150">[IoT Hub 메트릭][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="56740-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
<span data-ttu-id="56740-151">[Azure ExpressRoute]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services</span><span class="sxs-lookup"><span data-stu-id="56740-151">[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services</span></span>

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md