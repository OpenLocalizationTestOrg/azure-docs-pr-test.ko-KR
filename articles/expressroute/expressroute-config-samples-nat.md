---
title: "ExpressRoute 고객 라우터 구성 샘플 | Microsoft 문서"
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
ms.openlocfilehash: 83a7da2db537a3c900e90432455d59e8ac56d917
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="router-configuration-samples-to-set-up-and-manage-nat"></a><span data-ttu-id="2e68e-103">NAT 설정 및 관리를 위한 라우터 구성 샘플</span><span class="sxs-lookup"><span data-stu-id="2e68e-103">Router configuration samples to set up and manage NAT</span></span>
<span data-ttu-id="2e68e-104">이 페이지는 Cisco ASA 및 Juniper SRX 시리즈 라우터에 NAT 구성 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2e68e-104">This page provides NAT configuration samples for Cisco ASA and Juniper SRX series routers.</span></span> <span data-ttu-id="2e68e-105">이러한 샘플은 참조용이므로 그대로 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e68e-105">These are intended to be samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="2e68e-106">사용 중인 네트워크에 적절하게 구성하려면 공급업체와 작업하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e68e-106">You can work with your vendor to come up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2e68e-107">이 페이지에 있는 샘플은 참조용입니다.</span><span class="sxs-lookup"><span data-stu-id="2e68e-107">Samples in this page are intended to be purely for guidance.</span></span> <span data-ttu-id="2e68e-108">공급업체의 영업/기술 팀 및 네트워킹 팀과 함께 작업하면서 필요에 맞게 적절히 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e68e-108">You must work with your vendor's sales / technical team and your networking team to come up with appropriate configurations to meet your needs.</span></span> <span data-ttu-id="2e68e-109">Microsoft는 이 페이지에 나열된 구성과 관련된 문제를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e68e-109">Microsoft will not support issues related to configurations listed in this page.</span></span> <span data-ttu-id="2e68e-110">지원 문제는 장치 공급업체에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e68e-110">You must contact your device vendor for support issues.</span></span>
> 
> 

* <span data-ttu-id="2e68e-111">아래의 라우터 구성 샘플은 Azure 공용 및 Microsoft 피어링에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e68e-111">Router configuration samples below apply to Azure Public and Microsoft peerings.</span></span> <span data-ttu-id="2e68e-112">Azure 개인 피어링의 경우 NAT를 구성하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e68e-112">You must not configure NAT for Azure private peering.</span></span> <span data-ttu-id="2e68e-113">자세한 내용은 [ExpressRoute 피어링](expressroute-circuit-peerings.md) 및 [ExpressRoute NAT 요구 사항](expressroute-nat.md)을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="2e68e-113">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute NAT requirements](expressroute-nat.md) for more details.</span></span>

* <span data-ttu-id="2e68e-114">인터넷 및 ExpressRoute에 대한 연결은 별도의 NAT IP 풀을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e68e-114">You MUST use separate NAT IP pools for connectivity to the internet and ExpressRoute.</span></span> <span data-ttu-id="2e68e-115">인터넷 및 Express 경로에서 동일한 NAT IP 풀을 사용하면 비대칭 라우팅 및 연결 손실이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2e68e-115">Using the same NAT IP pool across the internet and ExpressRoute will result in asymmetric routing and loss of connectivity.</span></span>


## <a name="cisco-asa-firewalls"></a><span data-ttu-id="2e68e-116">Cisco ASA 방화벽</span><span class="sxs-lookup"><span data-stu-id="2e68e-116">Cisco ASA firewalls</span></span>
### <a name="pat-configuration-for-traffic-from-customer-network-to-microsoft"></a><span data-ttu-id="2e68e-117">고객 네트워크에서 Microsoft로의 트래픽을 위한 PAT 구성</span><span class="sxs-lookup"><span data-stu-id="2e68e-117">PAT configuration for traffic from customer network to Microsoft</span></span>
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

### <a name="pat-configuration-for-traffic-from-microsoft-to-customer-network"></a><span data-ttu-id="2e68e-118">Microsoft에서 고객 네트워크로 트래픽 PAT 구성</span><span class="sxs-lookup"><span data-stu-id="2e68e-118">PAT configuration for traffic from Microsoft to customer network</span></span>

<span data-ttu-id="2e68e-119">**인터페이스 및 방향:**</span><span class="sxs-lookup"><span data-stu-id="2e68e-119">**Interfaces and Direction:**</span></span>

    Source Interface (where the traffic enters the ASA): inside
    Destination Interface (where the traffic exits the ASA): outside

<span data-ttu-id="2e68e-120">**구성:**</span><span class="sxs-lookup"><span data-stu-id="2e68e-120">**Configuration:**</span></span>

<span data-ttu-id="2e68e-121">NAT 풀:</span><span class="sxs-lookup"><span data-stu-id="2e68e-121">NAT Pool:</span></span>

    object network outbound-PAT
        host <NAT-IP>

<span data-ttu-id="2e68e-122">대상 서버:</span><span class="sxs-lookup"><span data-stu-id="2e68e-122">Target Server:</span></span>

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

<span data-ttu-id="2e68e-123">고객 IP 주소에 대한 개체 그룹</span><span class="sxs-lookup"><span data-stu-id="2e68e-123">Object Group for Customer IP Addresses</span></span>

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

<span data-ttu-id="2e68e-124">NAT 명령:</span><span class="sxs-lookup"><span data-stu-id="2e68e-124">NAT Commands:</span></span>

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a><span data-ttu-id="2e68e-125">Juniper SRX 시리즈 라우터</span><span class="sxs-lookup"><span data-stu-id="2e68e-125">Juniper SRX series routers</span></span>
### <a name="1-create-redundant-ethernet-interfaces-for-the-cluster"></a><span data-ttu-id="2e68e-126">1. 클러스터에 대한 중복 이더넷 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="2e68e-126">1. Create redundant Ethernet interfaces for the cluster</span></span>
    interfaces {
        reth0 {
            description "To Internal Network";
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
            description "To Microsoft via Edge Router";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 2;
            }
            unit 100 {
                description "To Microsoft via Edge Router";
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
    }


### <a name="2-create-two-security-zones"></a><span data-ttu-id="2e68e-127">2. 두 보안 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="2e68e-127">2. Create two security zones</span></span>
* <span data-ttu-id="2e68e-128">내부 네트워크에 대한 신뢰 영역 및 에지 라우터 방향의 외부 네트워크에 대한 신뢰할 수 없는 영역</span><span class="sxs-lookup"><span data-stu-id="2e68e-128">Trust Zone for internal network and Untrust Zone for external network facing Edge Routers</span></span>
* <span data-ttu-id="2e68e-129">영역에 적절한 인터페이스 할당</span><span class="sxs-lookup"><span data-stu-id="2e68e-129">Assign appropriate interfaces to the zones</span></span>
* <span data-ttu-id="2e68e-130">인터페이스에서 서비스 허용</span><span class="sxs-lookup"><span data-stu-id="2e68e-130">Allow services on the interfaces</span></span>

    <span data-ttu-id="2e68e-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span><span class="sxs-lookup"><span data-stu-id="2e68e-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span></span>


### <a name="3-create-security-policies-between-zones"></a><span data-ttu-id="2e68e-132">3. 영역 간에 보안 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="2e68e-132">3. Create security policies between zones</span></span>
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


### <a name="4-configure-nat-policies"></a><span data-ttu-id="2e68e-133">4. NAT 정책 구성</span><span class="sxs-lookup"><span data-stu-id="2e68e-133">4. Configure NAT policies</span></span>
* <span data-ttu-id="2e68e-134">두 NAT 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e68e-134">Create two NAT pools.</span></span> <span data-ttu-id="2e68e-135">하나는 Microsoft로의 NAT 트래픽 아웃바운드에 사용되며 다른 하나는 Microsoft에서 고객에게로의 NAT 트래픽 아웃바운드에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e68e-135">One will be used to NAT traffic outbound to Microsoft and other from Microsoft to the customer.</span></span>
* <span data-ttu-id="2e68e-136">각 트래픽에 대해 NAT를 수행하기 위한 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="2e68e-136">Create rules to NAT the respective traffic</span></span>
  
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
                       to routing-instance External-ExpressRoute;
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
                       to routing-instance Internal;
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

### <a name="5-configure-bgp-to-advertise-selective-prefixes-in-each-direction"></a><span data-ttu-id="2e68e-137">5. 각 방향으로 선택적 접두사를 보급하도록 BGP 구성</span><span class="sxs-lookup"><span data-stu-id="2e68e-137">5. Configure BGP to advertise selective prefixes in each direction</span></span>
<span data-ttu-id="2e68e-138">[라우팅 구성 예제 ](expressroute-config-samples-routing.md) 페이지에 있는 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e68e-138">Refer to samples in [Routing configuration samples ](expressroute-config-samples-routing.md) page.</span></span>

### <a name="6-create-policies"></a><span data-ttu-id="2e68e-139">6. 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="2e68e-139">6. Create policies</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="2e68e-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2e68e-140">Next steps</span></span>
<span data-ttu-id="2e68e-141">자세한 내용은 [Express 경로 FAQ](expressroute-faqs.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e68e-141">See the [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

