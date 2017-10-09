---
title: "aaaExpressRoute 고객 라우터 구성 샘플 | Microsoft Docs"
description: "이 페이지는 Cisco 및 Juniper 라우터에 대한 라우터 구성 샘플을 제공합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 564826bc-017a-4683-a385-37c9fa814948
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 5c91f24e6082e01c3e8df91b4fcfda46a6c29fa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a><span data-ttu-id="29187-103">tooset 샘플링 하 고 라우팅을 관리 하는 라우터 구성</span><span class="sxs-lookup"><span data-stu-id="29187-103">Router configuration samples tooset up and manage routing</span></span>
<span data-ttu-id="29187-104">이 페이지는 Cisco IOS-XE 및 Juniper MX 시리즈 라우터에 대한 인터페이스 및 라우팅 구성 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="29187-105">이들만 지침에 대 한 의도 한 toobe 샘플 되며 그대로 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="29187-106">수 작업할 공급 업체 toocome 적절 한 구성으로 네트워크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="29187-107">이 페이지에 있는 샘플에는 지침을 위해 의도 한 toobe은 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29187-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="29187-108">사용자의 요구와 적절 한 구성 toomeet 프로그램 네트워킹 팀 toocome 공급 업체의 영업 / 기술 팀과 작업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="29187-109">Microsoft는 문제를 지원 하지 않으므로이 페이지에 나열 된 tooconfigurations 관련 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="29187-110">지원 문제는 장치 공급업체에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="29187-111">라우터 인터페이스의 MTU 및 TCP MSS 설정</span><span class="sxs-lookup"><span data-stu-id="29187-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="29187-112">hello ExpressRoute 인터페이스에 대 한 hello MTU 라우터의 이더넷 인터페이스에 대 한 hello 일반적인 기본 MTU은 1500, 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29187-112">hello MTU for hello ExpressRoute interface is 1500, which is hello typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="29187-113">라우터는 다른 MTU 기본적으로, 않으면 없습니다 필요 toospecify 값 hello 라우터 인터페이스에서.</span><span class="sxs-lookup"><span data-stu-id="29187-113">Unless your router has a different MTU by default, there is no need toospecify a value on hello router interface.</span></span>
* <span data-ttu-id="29187-114">Azure VPN 게이트웨이 사용 하는 달리 ExpressRoute 회로 대 한 TCP MSS hello에 지정 된 toobe가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29187-114">Unlike an Azure VPN Gateway, hello TCP MSS for an ExpressRoute circuit does not need toobe specified.</span></span>

<span data-ttu-id="29187-115">아래의 라우터 구성 샘플 tooall 피어 링을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-115">Router configuration samples below apply tooall peerings.</span></span> <span data-ttu-id="29187-116">라우팅에 대한 자세한 내용은 [ExpressRoute 피어링](expressroute-circuit-peerings.md) 및 [ExpressRoute 라우팅 요구 사항](expressroute-routing.md)을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="29187-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="29187-117">Cisco IOS-XE 기반 라우터</span><span class="sxs-lookup"><span data-stu-id="29187-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="29187-118">이 단원의 샘플 hello hello IOS XE OS 제품군을 실행 하 든 라우터에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29187-118">hello samples in this section apply for any router running hello IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="29187-119">1. 인터페이스 및 하위 인터페이스 구성</span><span class="sxs-lookup"><span data-stu-id="29187-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="29187-120">모든 라우터에서 피어 링 당 sub 인터페이스 tooMicrosoft 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-120">You will require a sub interface per peering in every router you connect tooMicrosoft.</span></span> <span data-ttu-id="29187-121">하위 인터페이스는 VLAN ID 또는 누적된 한 쌍의 VLAN ID 및 IP 주소로 식별될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29187-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="29187-122">**Dot1Q 인터페이스 정의**</span><span class="sxs-lookup"><span data-stu-id="29187-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="29187-123">이 샘플에서는 단일 VLAN id 하위 인터페이스에 대 한 hello 하위 인터페이스 정의</span><span class="sxs-lookup"><span data-stu-id="29187-123">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="29187-124">hello VLAN ID는 피어 링 마다 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-124">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="29187-125">hello 마지막 8 진수 IPv4 주소는 항상 홀수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29187-125">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="29187-126">**QinQ 인터페이스 정의**</span><span class="sxs-lookup"><span data-stu-id="29187-126">**QinQ interface definition**</span></span>

<span data-ttu-id="29187-127">이 예제는 두 개의 VLAN Id를 가진 하위 인터페이스에 대 한 hello 하위 인터페이스 정의 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-127">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="29187-128">외부 VLAN ID (s 태그)를 사용 하는 경우 상태를 유지 하는 hello에서 모든 hello 피어 링 동일 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-128">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="29187-129">hello 내부 VLAN ID (c 태그)가 피어 링 마다 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-129">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="29187-130">hello 마지막 8 진수 IPv4 주소는 항상 홀수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29187-130">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="29187-131">2. eBGP 세션 설정</span><span class="sxs-lookup"><span data-stu-id="29187-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="29187-132">모든 피어링에 대해 Microsoft와 BGP 세션을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="29187-133">아래 hello 샘플 microsoft BGP 세션 toosetup이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29187-133">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="29187-134">Hello sub 인터페이스에 사용 되는 IPv4 주소를 비워둘 경우 hello BGP 인접 한 항목 (Microsoft)의 IP 주소 hello a.b.c.d+1 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29187-134">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="29187-135">hello 마지막 8 진수 hello BGP 인접 IPv4 주소는 항상 짝수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29187-135">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="29187-136">3. Hello BGP 세션을 통해 보급 접두사 toobe 설정</span><span class="sxs-lookup"><span data-stu-id="29187-136">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="29187-137">라우터 tooadvertise 선택 접두사 tooMicrosoft 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29187-137">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="29187-138">아래 샘플 hello를 사용 하 여 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29187-138">You can do so using hello sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="29187-139">4. 경로 맵</span><span class="sxs-lookup"><span data-stu-id="29187-139">4. Route maps</span></span>
<span data-ttu-id="29187-140">경로 맵을 사용할 수 있습니다 하 고 접두사는 네트워크로 전파 toofilter 접두사를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-140">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="29187-141">Tooaccomplish hello 작업 아래 hello 샘플을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29187-141">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="29187-142">적절한 접두사 목록이 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-142">Ensure that you have appropriate prefix lists setup.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
      neighbor <IP#2_used_by_Azure> route-map <MS_Prefixes_Inbound> in
     exit-address-family
    !
    route-map <MS_Prefixes_Inbound> permit 10
     match ip address prefix-list <MS_Prefixes>
    !


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="29187-143">Juniper MX 시리즈 라우터</span><span class="sxs-lookup"><span data-stu-id="29187-143">Juniper MX series routers</span></span>
<span data-ttu-id="29187-144">이 단원의 샘플 hello 있는 Juniper MX 시리즈 라우터가에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29187-144">hello samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="29187-145">1. 인터페이스 및 하위 인터페이스 구성</span><span class="sxs-lookup"><span data-stu-id="29187-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="29187-146">**Dot1Q 인터페이스 정의**</span><span class="sxs-lookup"><span data-stu-id="29187-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="29187-147">이 샘플에서는 단일 VLAN id 하위 인터페이스에 대 한 hello 하위 인터페이스 정의</span><span class="sxs-lookup"><span data-stu-id="29187-147">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="29187-148">hello VLAN ID는 피어 링 마다 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-148">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="29187-149">hello 마지막 8 진수 IPv4 주소는 항상 홀수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29187-149">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interfaces {
        vlan-tagging;
        <Interface_Number> {
            unit <Number> {
                vlan-id <VLAN_ID>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }
            }
        }
    }


<span data-ttu-id="29187-150">**QinQ 인터페이스 정의**</span><span class="sxs-lookup"><span data-stu-id="29187-150">**QinQ interface definition**</span></span>

<span data-ttu-id="29187-151">이 예제는 두 개의 VLAN Id를 가진 하위 인터페이스에 대 한 hello 하위 인터페이스 정의 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-151">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="29187-152">외부 VLAN ID (s 태그)를 사용 하는 경우 상태를 유지 하는 hello에서 모든 hello 피어 링 동일 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-152">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="29187-153">hello 내부 VLAN ID (c 태그)가 피어 링 마다 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-153">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="29187-154">hello 마지막 8 진수 IPv4 주소는 항상 홀수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29187-154">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interfaces {
        <Interface_Number> {
            flexible-vlan-tagging;
            unit <Number> {
                vlan-tags outer <S-tag> inner <C-tag>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }                           
            }                               
        }                                   
    }                           

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="29187-155">2. eBGP 세션 설정</span><span class="sxs-lookup"><span data-stu-id="29187-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="29187-156">모든 피어링에 대해 Microsoft와 BGP 세션을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="29187-157">아래 hello 샘플 microsoft BGP 세션 toosetup이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29187-157">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="29187-158">Hello sub 인터페이스에 사용 되는 IPv4 주소를 비워둘 경우 hello BGP 인접 한 항목 (Microsoft)의 IP 주소 hello a.b.c.d+1 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29187-158">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="29187-159">hello 마지막 8 진수 hello BGP 인접 IPv4 주소는 항상 짝수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29187-159">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

    routing-options {
        autonomous-system <Customer_ASN>;
    }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="29187-160">3. Hello BGP 세션을 통해 보급 접두사 toobe 설정</span><span class="sxs-lookup"><span data-stu-id="29187-160">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="29187-161">라우터 tooadvertise 선택 접두사 tooMicrosoft 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29187-161">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="29187-162">아래 샘플 hello를 사용 하 여 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29187-162">You can do so using hello sample below.</span></span>

    policy-options {
        policy-statement <Policy_Name> {
            term 1 {
                from protocol OSPF;
        route-filter <Prefix_to_be_advertised/Subnet_Mask> exact;
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }


### <a name="4-route-maps"></a><span data-ttu-id="29187-163">4. 경로 맵</span><span class="sxs-lookup"><span data-stu-id="29187-163">4. Route maps</span></span>
<span data-ttu-id="29187-164">경로 맵을 사용할 수 있습니다 하 고 접두사는 네트워크로 전파 toofilter 접두사를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-164">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="29187-165">Tooaccomplish hello 작업 아래 hello 샘플을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29187-165">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="29187-166">적절한 접두사 목록이 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-166">Ensure that you have appropriate prefix lists setup.</span></span>

    policy-options {
        prefix-list MS_Prefixes {
            <IP_Prefix_1/Subnet_Mask>;
            <IP_Prefix_2/Subnet_Mask>;
        }
        policy-statement <MS_Prefixes_Inbound> {
            term 1 {
                from {
        prefix-list MS_Prefixes;
                }
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                import <MS_Prefixes_Inbound>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

## <a name="next-steps"></a><span data-ttu-id="29187-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="29187-167">Next Steps</span></span>
<span data-ttu-id="29187-168">Hello 참조 [express 경로 FAQ](expressroute-faqs.md) 자세한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="29187-168">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

