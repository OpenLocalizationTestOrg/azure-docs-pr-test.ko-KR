---
title: "Azure 네트워크 감시자를 네트워크 보안 그룹에 대 한 aaaIntroduction tooflow 로깅을 | Microsoft Docs"
description: "이 페이지에서는 toouse NSG 흐름 Azure 네트워크 감시자의 기능을 기록 하는 방법을 설명 합니다."
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
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a><span data-ttu-id="6317f-103">네트워크 보안 그룹에 대 한 소개 tooflow 로깅</span><span class="sxs-lookup"><span data-stu-id="6317f-103">Introduction tooflow logging for Network Security Groups</span></span>

<span data-ttu-id="6317f-104">네트워크 보안 그룹 흐름 로그는 네트워크 보안 그룹을 통해 IP 트래픽 ingress 및 egress에 대 한 tooview 정보 수 있는 네트워크 감시자의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-104">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="6317f-105">이러한 흐름 로그 json 형식으로 작성 되 고 아웃 바운드 표시 및 hello 흐름 (소스/대상 IP, 소스/대상 포트, 프로토콜)에 대 한 5-튜플 정보에 각 규칙 별로 인바운드 흐름 hello NIC hello 흐름 적용 하 고 트래픽이 허용 된 경우 hello 또는 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

![흐름 로그 개요][1]

<span data-ttu-id="6317f-107">표시 되지 흐름 대상 네트워크 보안 그룹 로그, 동안 hello 동일 hello로 다른 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-107">While flow logs target Network Security Groups, they are not displayed hello same as hello other logs.</span></span> <span data-ttu-id="6317f-108">다음 예제는 hello와 같이 저장소 계정 및 다음 hello 로깅 경로 내 에서만 흐름 로그 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-108">Flow logs are stored only within a storage account and following hello logging path as shown in hello following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="6317f-109">동일한 hello 다른 로그에 표시 된 대로 보존 정책을 tooflow 로그를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-109">hello same retention policies as seen on other logs apply tooflow logs.</span></span> <span data-ttu-id="6317f-110">로그에는 1 한 일에서 설정할 수 있는 보존 정책을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-110">Logs have a retention policy that can be set from 1 day too365 days.</span></span> <span data-ttu-id="6317f-111">보존 정책이 설정 되어 있지 않으면 hello 로그 영원히 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-111">If a retention policy is not set, hello logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="6317f-112">로그 파일</span><span class="sxs-lookup"><span data-stu-id="6317f-112">Log file</span></span>

<span data-ttu-id="6317f-113">흐름 로그에는 여러 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="6317f-114">hello 다음 목록에는의 목록을 hello NSG 흐름 로그 내에서 반환 되는 hello 속성:</span><span class="sxs-lookup"><span data-stu-id="6317f-114">hello following list is a listing of hello properties that are returned within hello NSG flow log:</span></span>

* <span data-ttu-id="6317f-115">**시간** -hello 이벤트가 기록 된 시간</span><span class="sxs-lookup"><span data-stu-id="6317f-115">**time** - Time when hello event was logged</span></span>
* <span data-ttu-id="6317f-116">**systemId** - 네트워크 보안 그룹 리소스 ID</span><span class="sxs-lookup"><span data-stu-id="6317f-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="6317f-117">**범주** -hello 범주 hello 이벤트의이 항상 수 NetworkSecurityGroupFlowEvent</span><span class="sxs-lookup"><span data-stu-id="6317f-117">**category** - hello category of hello event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="6317f-118">**resourceid** -hello 리소스 hello NSG의 Id</span><span class="sxs-lookup"><span data-stu-id="6317f-118">**resourceid** - hello resource Id of hello NSG</span></span>
* <span data-ttu-id="6317f-119">**operationName** - 항상 NetworkSecurityGroupFlowEvents</span><span class="sxs-lookup"><span data-stu-id="6317f-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="6317f-120">**속성** -hello 흐름의 속성 컬렉션</span><span class="sxs-lookup"><span data-stu-id="6317f-120">**properties** - A collection of properties of hello flow</span></span>
    * <span data-ttu-id="6317f-121">**버전** -hello 흐름 로그 이벤트 스키마의 버전 번호</span><span class="sxs-lookup"><span data-stu-id="6317f-121">**Version** - Version number of hello Flow Log event schema</span></span>
    * <span data-ttu-id="6317f-122">**흐름** - 흐름의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="6317f-123">이 속성에는 서로 다른 규칙에 대한 여러 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="6317f-124">**규칙** -흐름 나열 된는 hello에 대 한 규칙</span><span class="sxs-lookup"><span data-stu-id="6317f-124">**rule** - Rule for which hello flows are listed</span></span>
            * <span data-ttu-id="6317f-125">**흐름** - 흐름의 컬렉션</span><span class="sxs-lookup"><span data-stu-id="6317f-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="6317f-126">**mac** -hello hello hello 흐름 수집 된 VM에 대 한 hello NIC의 MAC 주소</span><span class="sxs-lookup"><span data-stu-id="6317f-126">**mac** - hello MAC address of hello NIC for hello VM where hello flow was collected</span></span>
                * <span data-ttu-id="6317f-127">**flowTuples** -hello 흐름 튜플 쉼표로 구분 된 형식에서에 대 한 여러 속성을 포함 하는 문자열</span><span class="sxs-lookup"><span data-stu-id="6317f-127">**flowTuples** - A string that contains multiple properties for hello flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="6317f-128">**타임 스탬프** -hello 흐름 UNIX EPOCH 형식에서 발생 했을 때이 값은의 hello 타임 스탬프</span><span class="sxs-lookup"><span data-stu-id="6317f-128">**Time Stamp** - This value is hello time stamp of when hello flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="6317f-129">**원본 IP** -hello 원본 IP</span><span class="sxs-lookup"><span data-stu-id="6317f-129">**Source IP** - hello source IP</span></span>
                    * <span data-ttu-id="6317f-130">**대상 IP** -hello 대상 IP</span><span class="sxs-lookup"><span data-stu-id="6317f-130">**Destination IP** - hello destination IP</span></span>
                    * <span data-ttu-id="6317f-131">**원본 포트** -hello 원본 포트</span><span class="sxs-lookup"><span data-stu-id="6317f-131">**Source Port** - hello source port</span></span>
                    * <span data-ttu-id="6317f-132">**대상 포트** -hello 대상 포트</span><span class="sxs-lookup"><span data-stu-id="6317f-132">**Destination Port** - hello destination Port</span></span>
                    * <span data-ttu-id="6317f-133">**프로토콜** -hello hello 흐름의 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-133">**Protocol** - hello protocol of hello flow.</span></span> <span data-ttu-id="6317f-134">유효한 값은 TCP에 대해서 **T**이며 UDP에 대해서 **U**입니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="6317f-135">**트래픽 흐름** -hello hello 트래픽 흐름 방향입니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-135">**Traffic Flow** - hello direction of hello traffic flow.</span></span> <span data-ttu-id="6317f-136">유효한 값은 인바운드에 대해서 **I**이며 아웃바운드에 대해서 **O**입니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="6317f-137">**트래픽** - 트래픽이 허용되었는지 거부되었는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="6317f-138">유효한 값은 허용에 대해 **A**이며 거부에 대해 **D**입니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="6317f-139">hello 다음은 흐름 로그의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-139">hello following is an example of a Flow log.</span></span> <span data-ttu-id="6317f-140">Hello 앞 섹션에서에서 설명 하는 hello 속성 목록에 나오는 레코드가 여러 개 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-140">As you can see there are multiple records that follow hello property list described in hello preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="6317f-141">Hello flowTuples 속성의 값은 쉼표로 구분 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-141">Values in hello flowTuples property are a comma-separated list.</span></span>
 
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

## <a name="next-steps"></a><span data-ttu-id="6317f-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6317f-142">Next steps</span></span>

<span data-ttu-id="6317f-143">방문 하 여 tooenable 흐름을 기록 하는 방법에 대해 알아봅니다 [흐름을 사용 하도록 설정 하는 로깅](network-watcher-nsg-flow-logging-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-143">Learn how tooenable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="6317f-144">[NSG(네트워크 보안 그룹)에 대한 로그 분석](../virtual-network/virtual-network-nsg-manage-log.md)을 방문하여 NSG 로깅에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="6317f-145">[IP 흐름 확인으로 트래픽 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 VM에서 트래픽이 허용되는지 또는 거부되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6317f-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

