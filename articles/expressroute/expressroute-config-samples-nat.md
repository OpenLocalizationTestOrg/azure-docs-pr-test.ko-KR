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
# <a name="router-configuration-samples-tooset-up-and-manage-nat"></a><span data-ttu-id="07e0d-103">tooset 샘플링 하 고 NAT를 관리 하는 라우터 구성</span><span class="sxs-lookup"><span data-stu-id="07e0d-103">Router configuration samples tooset up and manage NAT</span></span>
<span data-ttu-id="07e0d-104">이 페이지는 Cisco ASA 및 Juniper SRX 시리즈 라우터에 NAT 구성 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="07e0d-104">This page provides NAT configuration samples for Cisco ASA and Juniper SRX series routers.</span></span> <span data-ttu-id="07e0d-105">이들만 지침에 대 한 의도 한 toobe 샘플 되며 그대로 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e0d-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="07e0d-106">수 작업할 공급 업체 toocome 적절 한 구성으로 네트워크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e0d-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="07e0d-107">이 페이지에 있는 샘플에는 지침을 위해 의도 한 toobe은 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e0d-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="07e0d-108">사용자의 요구와 적절 한 구성 toomeet 프로그램 네트워킹 팀 toocome 공급 업체의 영업 / 기술 팀과 작업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e0d-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="07e0d-109">Microsoft는 문제를 지원 하지 않으므로이 페이지에 나열 된 tooconfigurations 관련 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e0d-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="07e0d-110">지원 문제는 장치 공급업체에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e0d-110">You must contact your device vendor for support issues.</span></span>
> 
> 

* <span data-ttu-id="07e0d-111">아래의 라우터 구성 샘플 tooAzure 공개와 Microsoft 피어 링을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="07e0d-111">Router configuration samples below apply tooAzure Public and Microsoft peerings.</span></span> <span data-ttu-id="07e0d-112">Azure 개인 피어링의 경우 NAT를 구성하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e0d-112">You must not configure NAT for Azure private peering.</span></span> <span data-ttu-id="07e0d-113">자세한 내용은 [ExpressRoute 피어링](expressroute-circuit-peerings.md) 및 [ExpressRoute NAT 요구 사항](expressroute-nat.md)을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="07e0d-113">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute NAT requirements](expressroute-nat.md) for more details.</span></span>

* <span data-ttu-id="07e0d-114">연결 toohello에 대 한 별도 NAT IP 풀을 사용 해야 인터넷 및 express 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="07e0d-114">You MUST use separate NAT IP pools for connectivity toohello internet and ExpressRoute.</span></span> <span data-ttu-id="07e0d-115">Hello에서 동일한 NAT IP 풀을 사용 하 여 hello 인터넷 및 express 경로 비대칭 라우팅과 연결 손실이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e0d-115">Using hello same NAT IP pool across hello internet and ExpressRoute will result in asymmetric routing and loss of connectivity.</span></span>


## <a name="cisco-asa-firewalls"></a><span data-ttu-id="07e0d-116">Cisco ASA 방화벽</span><span class="sxs-lookup"><span data-stu-id="07e0d-116">Cisco ASA firewalls</span></span>
### <a name="pat-configuration-for-traffic-from-customer-network-toomicrosoft"></a><span data-ttu-id="07e0d-117">고객 네트워크 tooMicrosoft에서 트래픽을 PAT 구성</span><span class="sxs-lookup"><span data-stu-id="07e0d-117">PAT configuration for traffic from customer network tooMicrosoft</span></span>
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

### <a name="pat-configuration-for-traffic-from-microsoft-toocustomer-network"></a><span data-ttu-id="07e0d-118">Microsoft toocustomer 네트워크에서 트래픽을 PAT 구성</span><span class="sxs-lookup"><span data-stu-id="07e0d-118">PAT configuration for traffic from Microsoft toocustomer network</span></span>

<span data-ttu-id="07e0d-119">**인터페이스 및 방향:**</span><span class="sxs-lookup"><span data-stu-id="07e0d-119">**Interfaces and Direction:**</span></span>

    Source Interface (where hello traffic enters hello ASA): inside
    Destination Interface (where hello traffic exits hello ASA): outside

<span data-ttu-id="07e0d-120">**구성:**</span><span class="sxs-lookup"><span data-stu-id="07e0d-120">**Configuration:**</span></span>

<span data-ttu-id="07e0d-121">NAT 풀:</span><span class="sxs-lookup"><span data-stu-id="07e0d-121">NAT Pool:</span></span>

    object network outbound-PAT
        host <NAT-IP>

<span data-ttu-id="07e0d-122">대상 서버:</span><span class="sxs-lookup"><span data-stu-id="07e0d-122">Target Server:</span></span>

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

<span data-ttu-id="07e0d-123">고객 IP 주소에 대한 개체 그룹</span><span class="sxs-lookup"><span data-stu-id="07e0d-123">Object Group for Customer IP Addresses</span></span>

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

<span data-ttu-id="07e0d-124">NAT 명령:</span><span class="sxs-lookup"><span data-stu-id="07e0d-124">NAT Commands:</span></span>

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a><span data-ttu-id="07e0d-125">Juniper SRX 시리즈 라우터</span><span class="sxs-lookup"><span data-stu-id="07e0d-125">Juniper SRX series routers</span></span>
### <a name="1-create-redundant-ethernet-interfaces-for-hello-cluster"></a><span data-ttu-id="07e0d-126">1. Hello 클러스터에 대 한 중복 이더넷 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="07e0d-126">1. Create redundant Ethernet interfaces for hello cluster</span></span>
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


### <a name="2-create-two-security-zones"></a><span data-ttu-id="07e0d-127">2. 두 보안 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="07e0d-127">2. Create two security zones</span></span>
* <span data-ttu-id="07e0d-128">내부 네트워크에 대한 신뢰 영역 및 에지 라우터 방향의 외부 네트워크에 대한 신뢰할 수 없는 영역</span><span class="sxs-lookup"><span data-stu-id="07e0d-128">Trust Zone for internal network and Untrust Zone for external network facing Edge Routers</span></span>
* <span data-ttu-id="07e0d-129">적절 한 인터페이스 toohello 영역 할당</span><span class="sxs-lookup"><span data-stu-id="07e0d-129">Assign appropriate interfaces toohello zones</span></span>
* <span data-ttu-id="07e0d-130">Hello 인터페이스에는 서비스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e0d-130">Allow services on hello interfaces</span></span>

    <span data-ttu-id="07e0d-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span><span class="sxs-lookup"><span data-stu-id="07e0d-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span></span>


### <a name="3-create-security-policies-between-zones"></a><span data-ttu-id="07e0d-132">3. 영역 간에 보안 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="07e0d-132">3. Create security policies between zones</span></span>
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


### <a name="4-configure-nat-policies"></a><span data-ttu-id="07e0d-133">4. NAT 정책 구성</span><span class="sxs-lookup"><span data-stu-id="07e0d-133">4. Configure NAT policies</span></span>
* <span data-ttu-id="07e0d-134">두 NAT 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07e0d-134">Create two NAT pools.</span></span> <span data-ttu-id="07e0d-135">하나 사용된 tooNAT 트래픽 아웃 바운드 tooMicrosoft 오류 코드 및 기타 Microsoft toohello 고객 으로부터 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e0d-135">One will be used tooNAT traffic outbound tooMicrosoft and other from Microsoft toohello customer.</span></span>
* <span data-ttu-id="07e0d-136">TooNAT hello 각 트래픽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="07e0d-136">Create rules tooNAT hello respective traffic</span></span>
  
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

### <a name="5-configure-bgp-tooadvertise-selective-prefixes-in-each-direction"></a><span data-ttu-id="07e0d-137">5. 각 방향에서 BGP tooadvertise 선택적 접두사를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e0d-137">5. Configure BGP tooadvertise selective prefixes in each direction</span></span>
<span data-ttu-id="07e0d-138">참조에서 toosamples [라우팅 구성 예제 ](expressroute-config-samples-routing.md) 페이지.</span><span class="sxs-lookup"><span data-stu-id="07e0d-138">Refer toosamples in [Routing configuration samples ](expressroute-config-samples-routing.md) page.</span></span>

### <a name="6-create-policies"></a><span data-ttu-id="07e0d-139">6. 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="07e0d-139">6. Create policies</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="07e0d-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07e0d-140">Next steps</span></span>
<span data-ttu-id="07e0d-141">Hello 참조 [express 경로 FAQ](expressroute-faqs.md) 자세한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e0d-141">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

