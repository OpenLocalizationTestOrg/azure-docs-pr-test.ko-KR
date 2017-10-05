---
title: "Azure Network Watcher를 사용하여 네트워크 보안 그룹에 대한 흐름 로깅 소개 | Microsoft Docs"
description: "이 페이지에서는 Azure Network Watcher의 기능인 NSG 흐름 로그를 사용하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b7a9162d6c6219b6b1c51a49cd34b9616e9d3e8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-flow-logging-for-network-security-groups"></a><span data-ttu-id="433ba-103">네트워크 보안 그룹에 대한 흐름 로깅 소개</span><span class="sxs-lookup"><span data-stu-id="433ba-103">Introduction to flow logging for Network Security Groups</span></span>

<span data-ttu-id="433ba-104">네트워크 보안 그룹 흐름 로그는 네트워크 보안 그룹을 통해 수신 및 송신 IP 트래픽에 대한 정보를 볼 수 있는 Network Watcher의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-104">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="433ba-105">이러한 흐름 로그는 json 형식으로 작성되고 트래픽이 허용되거나 거부된 경우 각 규칙을 기준으로 아웃바운드 및 인바운드 흐름, 흐름이 적용되는 NIC, 흐름에 대한 5개의 튜플 정보(원본/대상 IP, 원본/대상 포트, 프로토콜)를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

![흐름 로그 개요][1]

<span data-ttu-id="433ba-107">흐름 로그는 네트워크 보안 그룹을 대상으로 하지만 다른 로그와 동일하게 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-107">While flow logs target Network Security Groups, they are not displayed the same as the other logs.</span></span> <span data-ttu-id="433ba-108">흐름 로그는 저장소 계정 내에만 저장되며 다음 예제와 같이 로깅 경로를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-108">Flow logs are stored only within a storage account and following the logging path as shown in the following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="433ba-109">다른 로그에서 보듯이 흐름 로그에 동일한 보존 정책을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-109">The same retention policies as seen on other logs apply to flow logs.</span></span> <span data-ttu-id="433ba-110">로그에는 1일에서 365일까지 설정할 수 있는 보존 정책이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-110">Logs have a retention policy that can be set from 1 day to 365 days.</span></span> <span data-ttu-id="433ba-111">보존 정책을 설정하지 않으면 로그는 계속 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-111">If a retention policy is not set, the logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="433ba-112">로그 파일</span><span class="sxs-lookup"><span data-stu-id="433ba-112">Log file</span></span>

<span data-ttu-id="433ba-113">흐름 로그에는 여러 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="433ba-114">다음 목록은 NSG 흐름 로그 내에서 반환되는 속성의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-114">The following list is a listing of the properties that are returned within the NSG flow log:</span></span>

* <span data-ttu-id="433ba-115">**시간** - 이벤트가 로그된 시간</span><span class="sxs-lookup"><span data-stu-id="433ba-115">**time** - Time when the event was logged</span></span>
* <span data-ttu-id="433ba-116">**systemId** - 네트워크 보안 그룹 리소스 ID</span><span class="sxs-lookup"><span data-stu-id="433ba-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="433ba-117">**범주** - 이벤트의 범주, 항상 NetworkSecurityGroupFlowEvent가 됨</span><span class="sxs-lookup"><span data-stu-id="433ba-117">**category** - The category of the event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="433ba-118">**resourceid** - NSG의 리소스 ID</span><span class="sxs-lookup"><span data-stu-id="433ba-118">**resourceid** - The resource Id of the NSG</span></span>
* <span data-ttu-id="433ba-119">**operationName** - 항상 NetworkSecurityGroupFlowEvents</span><span class="sxs-lookup"><span data-stu-id="433ba-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="433ba-120">**속성** - 흐름의 속성 컬렉션</span><span class="sxs-lookup"><span data-stu-id="433ba-120">**properties** - A collection of properties of the flow</span></span>
    * <span data-ttu-id="433ba-121">**버전** - 흐름 로그 이벤트 스키마의 버전 번호</span><span class="sxs-lookup"><span data-stu-id="433ba-121">**Version** - Version number of the Flow Log event schema</span></span>
    * <span data-ttu-id="433ba-122">**흐름** - 흐름의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="433ba-123">이 속성에는 서로 다른 규칙에 대한 여러 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="433ba-124">**규칙** - 흐름이 나열된 규칙</span><span class="sxs-lookup"><span data-stu-id="433ba-124">**rule** - Rule for which the flows are listed</span></span>
            * <span data-ttu-id="433ba-125">**흐름** - 흐름의 컬렉션</span><span class="sxs-lookup"><span data-stu-id="433ba-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="433ba-126">**mac** - 흐름이 수집된 VM에 대한 NIC의 MAC 주소</span><span class="sxs-lookup"><span data-stu-id="433ba-126">**mac** - The MAC address of the NIC for the VM where the flow was collected</span></span>
                * <span data-ttu-id="433ba-127">**flowTuples** - 쉼표로 구분된 형식에서 흐름 튜플에 대한 여러 속성을 포함하는 문자열</span><span class="sxs-lookup"><span data-stu-id="433ba-127">**flowTuples** - A string that contains multiple properties for the flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="433ba-128">**타임스탬프** - 이 값은 흐름이 UNIX EPOCH 형식에서 발생하는 경우의 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-128">**Time Stamp** - This value is the time stamp of when the flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="433ba-129">**원본 IP** - 원본 IP</span><span class="sxs-lookup"><span data-stu-id="433ba-129">**Source IP** - The source IP</span></span>
                    * <span data-ttu-id="433ba-130">**대상 IP** - 대상 IP</span><span class="sxs-lookup"><span data-stu-id="433ba-130">**Destination IP** - The destination IP</span></span>
                    * <span data-ttu-id="433ba-131">**원본 포트** - 원본 포트</span><span class="sxs-lookup"><span data-stu-id="433ba-131">**Source Port** - The source port</span></span>
                    * <span data-ttu-id="433ba-132">**대상 포트** - 대상 포트</span><span class="sxs-lookup"><span data-stu-id="433ba-132">**Destination Port** - The destination Port</span></span>
                    * <span data-ttu-id="433ba-133">**프로토콜** - 흐름의 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-133">**Protocol** - The protocol of the flow.</span></span> <span data-ttu-id="433ba-134">유효한 값은 TCP에 대해서 **T**이며 UDP에 대해서 **U**입니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="433ba-135">**트래픽 흐름** - 트래픽 흐름의 방향입니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-135">**Traffic Flow** - The direction of the traffic flow.</span></span> <span data-ttu-id="433ba-136">유효한 값은 인바운드에 대해서 **I**이며 아웃바운드에 대해서 **O**입니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="433ba-137">**트래픽** - 트래픽이 허용되었는지 거부되었는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="433ba-138">유효한 값은 허용에 대해 **A**이며 거부에 대해 **D**입니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="433ba-139">다음은 흐름 로그의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-139">The following is an example of a Flow log.</span></span> <span data-ttu-id="433ba-140">이전 섹션에 설명된 속성 목록을 따르는 여러 레코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-140">As you can see there are multiple records that follow the property list described in the preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="433ba-141">flowTuples 속성의 값은 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-141">Values in the flowTuples property are a comma-separated list.</span></span>
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a><span data-ttu-id="433ba-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="433ba-142">Next steps</span></span>

<span data-ttu-id="433ba-143">[흐름 로깅을 사용하도록 설정](network-watcher-nsg-flow-logging-portal.md)을 방문하여 흐름 로그를 사용하도록 설정하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-143">Learn how to enable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="433ba-144">[NSG(네트워크 보안 그룹)에 대한 로그 분석](../virtual-network/virtual-network-nsg-manage-log.md)을 방문하여 NSG 로깅에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="433ba-145">[IP 흐름 확인으로 트래픽 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 VM에서 트래픽이 허용되는지 또는 거부되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="433ba-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

