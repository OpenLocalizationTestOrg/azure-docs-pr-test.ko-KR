---
title: "Cisco ASA 장치 tooAzure VPN 게이트웨이 연결-aaaSample 구성 | Microsoft Docs"
description: "이 문서에서는 Cisco ASA 장치 tooAzure VPN 게이트웨이 연결에 대 한 샘플 구성 합니다."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: dad13e02afe8dad2379db750eb09602e08e8ea99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a>샘플 구성: Cisco ASA 장치(IKEv2/BGP 아님)
이 문서에서는 Cisco ASA 장치 tooAzure VPN 게이트웨이 연결에 대 한 샘플 구성 합니다.

## <a name="device-at-a-glance"></a>장치 개요

|                        |                                   |
| ---                    | ---                               |
| 장치 공급 업체          | 시스코                             |
| 장치 모델           | ASA(적응 보안 어플라이언스) |
| 대상 버전         | 8.4+                              |
| 테스트 모델           | ASA 5505                          |
| 테스트 버전         | 9.2                               |
| IKE 버전            | **IKEv2**                         |
| BGP                    | **아니요**                            |
| Azure VPN 게이트웨이 유형 | **경로 기반** VPN 게이트웨이       |
|                        |                                   |

> [!NOTE]
> 1. Cisco ASA 장치 tooan Azure 연결 하는 hello 구성 아래 **경로 기반** 에 설명 된 대로 "UserPolicyBasedTrafficSelectors" 옵션을 사용자 지정 IPsec/IKE 정책을 사용 하 여 VPN 게이트웨이 [이 여기서](vpn-gateway-connect-multiple-policybased-rm-ps.md).
> 2. ASA 장치 toouse 필요 **IKEv2** 액세스 목록 기반 구성을 사용 하 여 VTI 기반 합니다.
> 3. VPN 장치 공급 업체 사양을 tooensure hello 정책은 온-프레미스 VPN 장치 지원에 문의 하십시오.

## <a name="vpn-device-requirements"></a>VPN 장치 요구 사항
Azure VPN 게이트웨이 도구 모음 tooestablish S2S VPN 터널에 대 한 표준의 IPsec/IKE 프로토콜을 사용 합니다. 너무 참조[에 대 한 VPN 장치](vpn-gateway-about-vpn-devices.md) hello에 대 한 자세한 IPsec/IKE 프로토콜 매개 변수 및 Azure VPN 게이트웨이에 대 한 기본 암호화 알고리즘입니다. 에 설명 된 대로 암호화 알고리즘 및 키 길이 특정 연결에 대 한 정확한 조합 hello를 선택적으로 지정할 수 [암호화 요구 사항에 대 한](vpn-gateway-about-compliance-crypto.md)합니다. 암호화 알고리즘 및 키 길이의 특정 조합을 선택 하는 경우 해당 사양을 hello를 사용 하 여 VPN 장치에 있는지 확인 하십시오.

## <a name="single-vpn-tunnel"></a>단일 VPN 터널
이 토폴로지는 Azure VPN 게이트웨이와 온-프레미스 VPN 장치 간에 단일 S2S VPN 터널로 구성됩니다. 필요에 따라 hello VPN 터널에서 BGP를 구성할 수 있습니다.

![단일 터널](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

너무 참조[단일 터널 설치](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) 단계별 지침 toobuild hello Azure 구성 하세요.

### <a name="network-and-vpn-gateway-information"></a>네트워크 및 VPN 게이트웨이 정보
이 여기서는이 샘플 hello에 대 한 hello 매개 변수를 나열 합니다.

| **매개 변수**                | **값**                    |
| ---                          | ---                          |
| VNet 주소 접두사        | 10.11.0.0/16<br>10.12.0.0/16 |
| Azure VPN 게이트웨이 IP         | Azure_Gateway_Public_IP      |
| 온-프레미스 주소 접두사 | 10.51.0.0/16<br>10.52.0.0/16 |
| 온-프레미스 VPN 장치 IP    | OnPrem_Device_Public_IP     |
| *VNet BGP ASN                | 65010                        |
| *Azure BGP 피어 IP           | 10.12.255.30                 |
| *온-프레미스 BGP ASN         | 65050                        |
| *온-프레미스 BGP 피어 IP     | 10.52.255.254                |
|                              |                              |

* (*) BGP에 대한 선택적 매개 변수만 해당

### <a name="ipsecike-policy--parameters"></a>IPsec/IKE 정책 및 매개 변수

hello 아래 표에 hello IPsec/IKE 알고리즘 및 hello 샘플에 사용 된 매개 변수입니다. 프로그램 VPN 장치 사양 toomake 위에 나열 된 모든 알고리즘 VPN 장치 모델와 펌웨어 버전에서 사용할 수 있는지를 참조 하십시오.

| **IPsec/IKEv2**  | **값**                            |
| ---              | ---                                  |
| IKEv2 암호화 | AES256                               |
| IKEv2 무결성  | SHA384                               |
| DH 그룹         | DHGroup24                            |
| IPsec 암호화 | AES256                               |
| IPsec 무결성  | SHA1                                 |
| PFS 그룹        | PFS24                                |
| QM SA 수명   | 7200초                         |
| 트래픽 선택기 | UsePolicyBasedTrafficSelectors $True |
| 미리 공유한 키   | PreSharedKey                         |
|                  |                                      |

- (*) 일부 장치에서 IPsec 무결성은 GCM-AES가 IPsec 암호화 알고리즘으로 사용되는 경우 "null"이어야 합니다.

### <a name="device-notes"></a>장치 정보

>[!NOTE]
>
> 1. IKEv2 지원에는 ASA 버전 8.4 이상이 필요합니다.
> 2. 더 높은 DH 및 PFS 그룹 지원(그룹 5 이외)에는 ASA 버전 9.x가 필요합니다.
> 3. SHA-256, SHA-384, SHA-512로 AES GCM 및 IPsec 무결성을 사용하는 IPsec 암호화 지원에는 최신 ASA 하드웨어에서 ASA 버전 9.x가 필요합니다. ASA 5505, 5510, 5520, 5540, 5550, 5580은 지원되지 **않습니다**. (Hello 공급 업체 사양 tooconfirm 확인 하십시오.)
>


### <a name="sample-device-configurations"></a>샘플 장치 구성
아래의 hello 스크립트 hello 토폴로지를 기반으로 하는 샘플 구성 및 위에 나열 된 매개 변수를 제공 합니다. hello S2S VPN 터널 구성의 hello 부분을 다음으로 구성 됩니다.

1. 인터페이스 및 경로
2. 액세스 목록
3. IKE 정책 및 매개 변수(1단계 또는 기본 모드)
4. IPsec 정책 및 매개 변수(2단계 또는 빠른 모드)
5. 기타 매개 변수(TCP MSS 고정 등)

>[!IMPORTANT] 
>아래에 나열 된 hello 추가 구성을 완료 하 고 hello 자리 표시자 hello 실제 값으로 대체 했는지 확인 하세요.
> 
> - 인터페이스 내부와 외부에 대해 인터페이스 구성
> - 내부/개인 및 외부/공용 네트워크에 대한 경로
> - 모든 이름 및 정책 번호는 고유 hello 장치에서 확인 하십시오.
> - 장치에서 hello 암호화 알고리즘이 지원 되는지 확인
> - Hello 다음 자리 표시자 hello 실제 값으로 바꾸기
>   - 외부 인터페이스 이름: "outside"
>   - Azure_Gateway_Public_IP
>   - OnPrem_Device_Public_IP
>   - IKE Pre_Shared_Key
>   - VNet 및 로컬 네트워크 게이트웨이 이름(VNetName, LNGName)
>   - VNet 및 온-프레미스 네트워크 주소 접두사
>   - 적절한 네트워크 마스크

#### <a name="sample-configuration"></a>샘플 구성

```
! Sample ASA configuration for connecting tooAzure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace hello following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - hello Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with hello actual nexthop IP address
!
! (*) Must be unique names in hello device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on hello outside interface or vlan
!     > <PrivateIPAddress> on hello inside interface or vlan; e.g., 10.51.0.1/24
!     > Route tooconnect too<Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between hello ASA and hello Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding toohello <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines hello on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify hello access-list between hello Azure VNet and your on-premises network.
!       This access list defines hello IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between hello on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure hello policy number is not used
!       - integrity and prf must be hello same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as hello crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned tooyour outside interface, you must use
!         hello same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses hello access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses hello proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS too1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a>간단한 디버깅 명령

디버깅 목적을 위한 일부 ASA 명령은 다음과 같습니다.

1. 표시 IPsec과 IKE SA hello
    - "show crypto ipsec sa"
    - "show crypto ikev2 sa"
2. 시작 중 디버그 모드-이의 가져올 수 매우 불안정 hello 콘솔
    - "debug crypto ikev2 platform <level>"
    - "debug crypto ikev2 protocol <level>"
3. 현재 구성 나열
    - "실행 표시"-표시 hello hello 장치;에서 현재 구성 사용할 수 있습니다 hello hello 구성의 다양 한 하위 명령을 toolist 특정 부분입니다. 예: "show run crypto", "show run access-list", "show run tunnel-group" 등


## <a name="next-steps"></a>다음 단계
참조 [크로스-프레미스 및 VNet 대 VNet 연결에 대해 액티브-액티브 VPN 게이트웨이 구성](vpn-gateway-activeactive-rm-powershell.md) 단계 tooconfigure 액티브-액티브 크로스-프레미스 및 VNet 대 VNet 연결 합니다.

