---
title: "ExpressRoute 고객 라우터 구성 샘플 | Microsoft 문서"
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
ms.openlocfilehash: 032e584dc5abf59e9e3e8d80673b402f1fbf721b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="router-configuration-samples-to-set-up-and-manage-routing"></a><span data-ttu-id="56c1f-103">라우팅 설정 및 관리를 위한 라우터 구성 샘플</span><span class="sxs-lookup"><span data-stu-id="56c1f-103">Router configuration samples to set up and manage routing</span></span>
<span data-ttu-id="56c1f-104">이 페이지는 Cisco IOS-XE 및 Juniper MX 시리즈 라우터에 대한 인터페이스 및 라우팅 구성 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="56c1f-105">이러한 샘플은 참조용이므로 그대로 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-105">These are intended to be samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="56c1f-106">사용 중인 네트워크에 적절하게 구성하려면 공급업체와 작업하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-106">You can work with your vendor to come up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="56c1f-107">이 페이지에 있는 샘플은 참조용입니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-107">Samples in this page are intended to be purely for guidance.</span></span> <span data-ttu-id="56c1f-108">공급업체의 영업/기술 팀 및 네트워킹 팀과 함께 작업하면서 필요에 맞게 적절히 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-108">You must work with your vendor's sales / technical team and your networking team to come up with appropriate configurations to meet your needs.</span></span> <span data-ttu-id="56c1f-109">Microsoft는 이 페이지에 나열된 구성과 관련된 문제를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-109">Microsoft will not support issues related to configurations listed in this page.</span></span> <span data-ttu-id="56c1f-110">지원 문제는 장치 공급업체에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="56c1f-111">라우터 인터페이스의 MTU 및 TCP MSS 설정</span><span class="sxs-lookup"><span data-stu-id="56c1f-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="56c1f-112">ExpressRoute 인터페이스에 대한 MTU는 라우터의 이더넷 인터페이스에 대한 일반적인 기본 MTU인 1500입니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-112">The MTU for the ExpressRoute interface is 1500, which is the typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="56c1f-113">라우터에 기본적으로 다른 MTU가 있지 않는 한, 라우터 인터페이스에서 값을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-113">Unless your router has a different MTU by default, there is no need to specify a value on the router interface.</span></span>
* <span data-ttu-id="56c1f-114">Azure VPN Gateway와는 달리, ExpressRoute 회로용 TCP MSS를 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-114">Unlike an Azure VPN Gateway, the TCP MSS for an ExpressRoute circuit does not need to be specified.</span></span>

<span data-ttu-id="56c1f-115">아래의 라우터 구성 샘플은 모든 피어링에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-115">Router configuration samples below apply to all peerings.</span></span> <span data-ttu-id="56c1f-116">라우팅에 대한 자세한 내용은 [ExpressRoute 피어링](expressroute-circuit-peerings.md) 및 [ExpressRoute 라우팅 요구 사항](expressroute-routing.md)을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="56c1f-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="56c1f-117">Cisco IOS-XE 기반 라우터</span><span class="sxs-lookup"><span data-stu-id="56c1f-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="56c1f-118">이 섹션의 샘플은 IOS-XE OS 제품군을 실행하는 모든 라우터에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-118">The samples in this section apply for any router running the IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="56c1f-119">1. 인터페이스 및 하위 인터페이스 구성</span><span class="sxs-lookup"><span data-stu-id="56c1f-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="56c1f-120">Microsoft에 연결하는 모든 라우터에서 피어링별로 하위 인터페이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-120">You will require a sub interface per peering in every router you connect to Microsoft.</span></span> <span data-ttu-id="56c1f-121">하위 인터페이스는 VLAN ID 또는 누적된 한 쌍의 VLAN ID 및 IP 주소로 식별될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="56c1f-122">**Dot1Q 인터페이스 정의**</span><span class="sxs-lookup"><span data-stu-id="56c1f-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="56c1f-123">이 샘플에서는 VLAN ID가 하나인 하위 인터페이스에 대한 하위 인터페이스 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-123">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="56c1f-124">VLAN ID는 피어링별로 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-124">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="56c1f-125">IPv4 주소의 마지막 옥텟은 항상 홀수입니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-125">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="56c1f-126">**QinQ 인터페이스 정의**</span><span class="sxs-lookup"><span data-stu-id="56c1f-126">**QinQ interface definition**</span></span>

<span data-ttu-id="56c1f-127">이 샘플에서는 VLAN ID가 두 개인 하위 인터페이스에 대한 하위 인터페이스 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-127">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="56c1f-128">바깥쪽의 VLAN ID(s-tag)는 사용되는 경우 모든 피어링에서 동일하게 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-128">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="56c1f-129">안쪽의 VLAN ID(c-tag)는 피어링별로 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-129">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="56c1f-130">IPv4 주소의 마지막 옥텟은 항상 홀수입니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-130">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="56c1f-131">2. eBGP 세션 설정</span><span class="sxs-lookup"><span data-stu-id="56c1f-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="56c1f-132">모든 피어링에 대해 Microsoft와 BGP 세션을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="56c1f-133">아래의 샘플에서 Microsoft와 BGP 세션을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-133">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="56c1f-134">하위 인터페이스에 사용한 IPv4 주소가 a.b.c.d인 경우 BGP 인접 라우터(Microsoft)의 IP 주소는 a.b.c.d+1입니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-134">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="56c1f-135">BGP 인접 라우터에 대한 IPv4 주소의 마지막 옥텟은 항상 짝수입니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-135">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="56c1f-136">3. BGP 세션을 통해 알릴 접두사 설정</span><span class="sxs-lookup"><span data-stu-id="56c1f-136">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="56c1f-137">선택된 접두사를 Microsoft에 알리도록 라우터를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-137">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="56c1f-138">아래의 샘플을 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-138">You can do so using the sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="56c1f-139">4. 경로 맵</span><span class="sxs-lookup"><span data-stu-id="56c1f-139">4. Route maps</span></span>
<span data-ttu-id="56c1f-140">경로 맵과 접두사 목록을 사용하여 네트워크에 전파되는 접두사를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-140">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="56c1f-141">아래의 샘플을 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-141">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="56c1f-142">적절한 접두사 목록이 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-142">Ensure that you have appropriate prefix lists setup.</span></span>

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


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="56c1f-143">Juniper MX 시리즈 라우터</span><span class="sxs-lookup"><span data-stu-id="56c1f-143">Juniper MX series routers</span></span>
<span data-ttu-id="56c1f-144">이 섹션의 샘플은 모든 Juniper MX 시리즈 라우터에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-144">The samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="56c1f-145">1. 인터페이스 및 하위 인터페이스 구성</span><span class="sxs-lookup"><span data-stu-id="56c1f-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="56c1f-146">**Dot1Q 인터페이스 정의**</span><span class="sxs-lookup"><span data-stu-id="56c1f-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="56c1f-147">이 샘플에서는 VLAN ID가 하나인 하위 인터페이스에 대한 하위 인터페이스 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-147">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="56c1f-148">VLAN ID는 피어링별로 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-148">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="56c1f-149">IPv4 주소의 마지막 옥텟은 항상 홀수입니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-149">The last octet of your IPv4 address will always be an odd number.</span></span>

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


<span data-ttu-id="56c1f-150">**QinQ 인터페이스 정의**</span><span class="sxs-lookup"><span data-stu-id="56c1f-150">**QinQ interface definition**</span></span>

<span data-ttu-id="56c1f-151">이 샘플에서는 VLAN ID가 두 개인 하위 인터페이스에 대한 하위 인터페이스 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-151">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="56c1f-152">바깥쪽의 VLAN ID(s-tag)는 사용되는 경우 모든 피어링에서 동일하게 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-152">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="56c1f-153">안쪽의 VLAN ID(c-tag)는 피어링별로 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-153">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="56c1f-154">IPv4 주소의 마지막 옥텟은 항상 홀수입니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-154">The last octet of your IPv4 address will always be an odd number.</span></span>

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

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="56c1f-155">2. eBGP 세션 설정</span><span class="sxs-lookup"><span data-stu-id="56c1f-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="56c1f-156">모든 피어링에 대해 Microsoft와 BGP 세션을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="56c1f-157">아래의 샘플에서 Microsoft와 BGP 세션을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-157">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="56c1f-158">하위 인터페이스에 사용한 IPv4 주소가 a.b.c.d인 경우 BGP 인접 라우터(Microsoft)의 IP 주소는 a.b.c.d+1입니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-158">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="56c1f-159">BGP 인접 라우터에 대한 IPv4 주소의 마지막 옥텟은 항상 짝수입니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-159">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

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

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="56c1f-160">3. BGP 세션을 통해 알릴 접두사 설정</span><span class="sxs-lookup"><span data-stu-id="56c1f-160">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="56c1f-161">선택된 접두사를 Microsoft에 알리도록 라우터를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-161">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="56c1f-162">아래의 샘플을 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-162">You can do so using the sample below.</span></span>

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


### <a name="4-route-maps"></a><span data-ttu-id="56c1f-163">4. 경로 맵</span><span class="sxs-lookup"><span data-stu-id="56c1f-163">4. Route maps</span></span>
<span data-ttu-id="56c1f-164">경로 맵과 접두사 목록을 사용하여 네트워크에 전파되는 접두사를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-164">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="56c1f-165">아래의 샘플을 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-165">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="56c1f-166">적절한 접두사 목록이 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56c1f-166">Ensure that you have appropriate prefix lists setup.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="56c1f-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="56c1f-167">Next Steps</span></span>
<span data-ttu-id="56c1f-168">자세한 내용은 [Express 경로 FAQ](expressroute-faqs.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56c1f-168">See the [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

