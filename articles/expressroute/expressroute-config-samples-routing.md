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
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a>tooset 샘플링 하 고 라우팅을 관리 하는 라우터 구성
이 페이지는 Cisco IOS-XE 및 Juniper MX 시리즈 라우터에 대한 인터페이스 및 라우팅 구성 샘플을 제공합니다. 이들만 지침에 대 한 의도 한 toobe 샘플 되며 그대로 사용할 수 있어야 합니다. 수 작업할 공급 업체 toocome 적절 한 구성으로 네트워크에 대 한 합니다. 

> [!IMPORTANT]
> 이 페이지에 있는 샘플에는 지침을 위해 의도 한 toobe은 됩니다. 사용자의 요구와 적절 한 구성 toomeet 프로그램 네트워킹 팀 toocome 공급 업체의 영업 / 기술 팀과 작업 해야 합니다. Microsoft는 문제를 지원 하지 않으므로이 페이지에 나열 된 tooconfigurations 관련 합니다. 지원 문제는 장치 공급업체에 문의해야 합니다.
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a>라우터 인터페이스의 MTU 및 TCP MSS 설정
* hello ExpressRoute 인터페이스에 대 한 hello MTU 라우터의 이더넷 인터페이스에 대 한 hello 일반적인 기본 MTU은 1500, 됩니다. 라우터는 다른 MTU 기본적으로, 않으면 없습니다 필요 toospecify 값 hello 라우터 인터페이스에서.
* Azure VPN 게이트웨이 사용 하는 달리 ExpressRoute 회로 대 한 TCP MSS hello에 지정 된 toobe가 필요 하지 않습니다.

아래의 라우터 구성 샘플 tooall 피어 링을 적용합니다. 라우팅에 대한 자세한 내용은 [ExpressRoute 피어링](expressroute-circuit-peerings.md) 및 [ExpressRoute 라우팅 요구 사항](expressroute-routing.md)을 검토하세요.


## <a name="cisco-ios-xe-based-routers"></a>Cisco IOS-XE 기반 라우터
이 단원의 샘플 hello hello IOS XE OS 제품군을 실행 하 든 라우터에 적용 됩니다.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. 인터페이스 및 하위 인터페이스 구성
모든 라우터에서 피어 링 당 sub 인터페이스 tooMicrosoft 연결 해야 합니다. 하위 인터페이스는 VLAN ID 또는 누적된 한 쌍의 VLAN ID 및 IP 주소로 식별될 수 있습니다.

**Dot1Q 인터페이스 정의**

이 샘플에서는 단일 VLAN id 하위 인터페이스에 대 한 hello 하위 인터페이스 정의 hello VLAN ID는 피어 링 마다 고유 합니다. hello 마지막 8 진수 IPv4 주소는 항상 홀수 됩니다.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

**QinQ 인터페이스 정의**

이 예제는 두 개의 VLAN Id를 가진 하위 인터페이스에 대 한 hello 하위 인터페이스 정의 제공합니다. 외부 VLAN ID (s 태그)를 사용 하는 경우 상태를 유지 하는 hello에서 모든 hello 피어 링 동일 hello 합니다. hello 내부 VLAN ID (c 태그)가 피어 링 마다 고유 합니다. hello 마지막 8 진수 IPv4 주소는 항상 홀수 됩니다.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a>2. eBGP 세션 설정
모든 피어링에 대해 Microsoft와 BGP 세션을 설정해야 합니다. 아래 hello 샘플 microsoft BGP 세션 toosetup이 있습니다. Hello sub 인터페이스에 사용 되는 IPv4 주소를 비워둘 경우 hello BGP 인접 한 항목 (Microsoft)의 IP 주소 hello a.b.c.d+1 됩니다. hello 마지막 8 진수 hello BGP 인접 IPv4 주소는 항상 짝수 됩니다.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Hello BGP 세션을 통해 보급 접두사 toobe 설정
라우터 tooadvertise 선택 접두사 tooMicrosoft 프로그램을 구성할 수 있습니다. 아래 샘플 hello를 사용 하 여 하도록 할 수 있습니다.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a>4. 경로 맵
경로 맵을 사용할 수 있습니다 하 고 접두사는 네트워크로 전파 toofilter 접두사를 나열 합니다. Tooaccomplish hello 작업 아래 hello 샘플을 사용할 수 있습니다. 적절한 접두사 목록이 설정되어 있어야 합니다.

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


## <a name="juniper-mx-series-routers"></a>Juniper MX 시리즈 라우터
이 단원의 샘플 hello 있는 Juniper MX 시리즈 라우터가에 적용 됩니다.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. 인터페이스 및 하위 인터페이스 구성

**Dot1Q 인터페이스 정의**

이 샘플에서는 단일 VLAN id 하위 인터페이스에 대 한 hello 하위 인터페이스 정의 hello VLAN ID는 피어 링 마다 고유 합니다. hello 마지막 8 진수 IPv4 주소는 항상 홀수 됩니다.

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


**QinQ 인터페이스 정의**

이 예제는 두 개의 VLAN Id를 가진 하위 인터페이스에 대 한 hello 하위 인터페이스 정의 제공합니다. 외부 VLAN ID (s 태그)를 사용 하는 경우 상태를 유지 하는 hello에서 모든 hello 피어 링 동일 hello 합니다. hello 내부 VLAN ID (c 태그)가 피어 링 마다 고유 합니다. hello 마지막 8 진수 IPv4 주소는 항상 홀수 됩니다.

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

### <a name="2-setting-up-ebgp-sessions"></a>2. eBGP 세션 설정
모든 피어링에 대해 Microsoft와 BGP 세션을 설정해야 합니다. 아래 hello 샘플 microsoft BGP 세션 toosetup이 있습니다. Hello sub 인터페이스에 사용 되는 IPv4 주소를 비워둘 경우 hello BGP 인접 한 항목 (Microsoft)의 IP 주소 hello a.b.c.d+1 됩니다. hello 마지막 8 진수 hello BGP 인접 IPv4 주소는 항상 짝수 됩니다.

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

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Hello BGP 세션을 통해 보급 접두사 toobe 설정
라우터 tooadvertise 선택 접두사 tooMicrosoft 프로그램을 구성할 수 있습니다. 아래 샘플 hello를 사용 하 여 하도록 할 수 있습니다.

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


### <a name="4-route-maps"></a>4. 경로 맵
경로 맵을 사용할 수 있습니다 하 고 접두사는 네트워크로 전파 toofilter 접두사를 나열 합니다. Tooaccomplish hello 작업 아래 hello 샘플을 사용할 수 있습니다. 적절한 접두사 목록이 설정되어 있어야 합니다.

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

## <a name="next-steps"></a>다음 단계
Hello 참조 [express 경로 FAQ](expressroute-faqs.md) 자세한 세부 정보에 대 한 합니다.

