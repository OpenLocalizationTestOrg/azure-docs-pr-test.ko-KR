---
title: "aaaExpressRoute 고객 라우터 구성 샘플 | Microsoft Docs"
description: "이 페이지는 Cisco 및 Juniper 라우터에 대한 라우터 구성 샘플을 제공합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: d6ea716f-d5ee-4a61-92b0-640d6e7d6974
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: b5faca0666bda6173e54abb0b6560d5f8bf8bfc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-nat"></a>tooset 샘플링 하 고 NAT를 관리 하는 라우터 구성
이 페이지는 Cisco ASA 및 Juniper SRX 시리즈 라우터에 NAT 구성 샘플을 제공합니다. 이들만 지침에 대 한 의도 한 toobe 샘플 되며 그대로 사용할 수 있어야 합니다. 수 작업할 공급 업체 toocome 적절 한 구성으로 네트워크에 대 한 합니다. 

> [!IMPORTANT]
> 이 페이지에 있는 샘플에는 지침을 위해 의도 한 toobe은 됩니다. 사용자의 요구와 적절 한 구성 toomeet 프로그램 네트워킹 팀 toocome 공급 업체의 영업 / 기술 팀과 작업 해야 합니다. Microsoft는 문제를 지원 하지 않으므로이 페이지에 나열 된 tooconfigurations 관련 합니다. 지원 문제는 장치 공급업체에 문의해야 합니다.
> 
> 

* 아래의 라우터 구성 샘플 tooAzure 공개와 Microsoft 피어 링을 적용합니다. Azure 개인 피어링의 경우 NAT를 구성하면 안 됩니다. 자세한 내용은 [ExpressRoute 피어링](expressroute-circuit-peerings.md) 및 [ExpressRoute NAT 요구 사항](expressroute-nat.md)을 검토하세요.

* 연결 toohello에 대 한 별도 NAT IP 풀을 사용 해야 인터넷 및 express 경로입니다. Hello에서 동일한 NAT IP 풀을 사용 하 여 hello 인터넷 및 express 경로 비대칭 라우팅과 연결 손실이 발생 합니다.


## <a name="cisco-asa-firewalls"></a>Cisco ASA 방화벽
### <a name="pat-configuration-for-traffic-from-customer-network-toomicrosoft"></a>고객 네트워크 tooMicrosoft에서 트래픽을 PAT 구성
    object network MSFT-PAT
      range <SNAT-START-IP> <SNAT-END-IP>


    object-group network MSFT-Range
      network-object <IP> <Subnet_Mask>

    object-group network on-prem-range-1
      network-object <IP> <Subnet-Mask>

    object-group network on-prem-range-2
      network-object <IP> <Subnet-Mask>

    object-group network on-prem
      network-object object on-prem-range-1
      network-object object on-prem-range-2

    nat (outside,inside) source dynamic on-prem pat-pool MSFT-PAT destination static MSFT-Range MSFT-Range

### <a name="pat-configuration-for-traffic-from-microsoft-toocustomer-network"></a>Microsoft toocustomer 네트워크에서 트래픽을 PAT 구성

**인터페이스 및 방향:**

    Source Interface (where hello traffic enters hello ASA): inside
    Destination Interface (where hello traffic exits hello ASA): outside

**구성:**

NAT 풀:

    object network outbound-PAT
        host <NAT-IP>

대상 서버:

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

고객 IP 주소에 대한 개체 그룹

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

NAT 명령:

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a>Juniper SRX 시리즈 라우터
### <a name="1-create-redundant-ethernet-interfaces-for-hello-cluster"></a>1. Hello 클러스터에 대 한 중복 이더넷 인터페이스 만들기
    interfaces {
        reth0 {
            description "tooInternal Network";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 1;
            }
            unit 100 {
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
        reth1 {
            description "tooMicrosoft via Edge Router";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 2;
            }
            unit 100 {
                description "tooMicrosoft via Edge Router";
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
    }


### <a name="2-create-two-security-zones"></a>2. 두 보안 영역 만들기
* 내부 네트워크에 대한 신뢰 영역 및 에지 라우터 방향의 외부 네트워크에 대한 신뢰할 수 없는 영역
* 적절 한 인터페이스 toohello 영역 할당
* Hello 인터페이스에는 서비스를 허용 합니다.

    security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }


### <a name="3-create-security-policies-between-zones"></a>3. 영역 간에 보안 정책 만들기
    security {
        policies {
            from-zone Trust to-zone Untrust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
            from-zone Untrust to-zone Trust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
        }
    }


### <a name="4-configure-nat-policies"></a>4. NAT 정책 구성
* 두 NAT 풀을 만듭니다. 하나 사용된 tooNAT 트래픽 아웃 바운드 tooMicrosoft 오류 코드 및 기타 Microsoft toohello 고객 으로부터 이어야 합니다.
* TooNAT hello 각 트래픽 규칙 만들기
  
       security {
           nat {
               source {
                   pool SNAT-To-ExpressRoute {
                       routing-instance {
                           External-ExpressRoute;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   pool SNAT-From-ExpressRoute {
                       routing-instance {
                           Internal;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   rule-set Outbound_NAT {
                       from routing-instance Internal;
                       toorouting-instance External-ExpressRoute;
                       rule SNAT-Out {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-To-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
                   rule-set Inbound-NAT {
                       from routing-instance External-ExpressRoute;
                       toorouting-instance Internal;
                       rule SNAT-In {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-From-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
               }
           }
       }

### <a name="5-configure-bgp-tooadvertise-selective-prefixes-in-each-direction"></a>5. 각 방향에서 BGP tooadvertise 선택적 접두사를 구성 합니다.
참조에서 toosamples [라우팅 구성 예제 ](expressroute-config-samples-routing.md) 페이지.

### <a name="6-create-policies"></a>6. 정책 만들기
    routing-options {
                  autonomous-system <Customer-ASN>;
    }
    policy-options {
        prefix-list Microsoft-Prefixes {
            <IP-Address/Subnet-Mask;
            <IP-Address/Subnet-Mask;
        }
        prefix-list private-ranges {
            10.0.0.0/8;
            172.16.0.0/12;
            192.168.0.0/16;
            100.64.0.0/10;
        }
        policy-statement Advertise-NAT-Pools {
            from {
                protocol static;
                route-filter <NAT-Pool-Address/Subnet-mask> prefix-length-range /32-/32;
            }
            then accept;
        }
        policy-statement Accept-from-Microsoft {
            term 1 {
                from {
                    instance External-ExpressRoute;
                    prefix-list-filter Microsoft-Prefixes orlonger;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
        policy-statement Accept-from-Internal {
            term no-private {
                from {
                    instance Internal;
                    prefix-list-filter private-ranges orlonger;
                }
                then reject;
            }
            term bgp {
                from {
                    instance Internal;
                    protocol bgp;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
    }
    routing-instances {
        Internal {
            instance-type virtual-router;
            interface reth0.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Microsoft;
            }
            protocols {
                bgp {
                    group customer {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-ASN-1>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
        External-ExpressRoute {
            instance-type virtual-router;
            interface reth1.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Internal;
            }
            protocols {
                bgp {
                    group edge-router {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-Public-ASN>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
    }

## <a name="next-steps"></a>다음 단계
Hello 참조 [express 경로 FAQ](expressroute-faqs.md) 자세한 세부 정보에 대 한 합니다.

