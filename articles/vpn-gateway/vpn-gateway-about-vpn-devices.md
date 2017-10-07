---
title: "크로스-프레미스 Azure 연결의 VPN 장치 aaaAbout | Microsoft Docs"
description: "이 문서에서는 S2S VPN Gateway 크로스-프레미스 연결에 대한 VPN 장치 및 IPsec 매개 변수에 대해 설명합니다. 링크가는 tooconfiguration 지침 및 샘플 제공 됩니다."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: ba449333-2716-4b7f-9889-ecc521e4d616
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: yushwang;cherylmc
ms.openlocfilehash: 8b84afbf93d807342ecd56ab369d5909a13343e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-devices-and-ipsecike-parameters-for-site-to-site-vpn-gateway-connections"></a>사이트 간 VPN Gateway 연결에 대한 VPN 장치 및 IPsec/IKE 매개 변수 정보

VPN 장치가 크로스-프레미스 VPN 연결 사이트 및 사이트 간 (S2S) VPN 게이트웨이 사용 하 여 필요한 tooconfigure 합니다. 온-프레미스 네트워크와 가상 네트워크 간의 보안 연결이 필요할 때마다 또는 사이트 간 연결에는 하이브리드 솔루션을 사용 하는 toocreate 수 있습니다. 이 문서에서는 유효성이 검사된 VPN 장치 목록과 VPN 게이트웨이의 IPsec/IKE 매개 변수 목록을 제공합니다.

> [!IMPORTANT]
> 온-프레미스 VPN 장치 및 VPN 게이트웨이 간에 연결 문제가 발생 하는 경우 참조 너무[알려진 장치 호환성 문제](#known)합니다.
>
>

### <a name="items-toonote-when-viewing-hello-tables"></a>항목 toonote hello 테이블을 볼 때:

* Azure VPN 게이트웨이에 대한 용어가 변경되었습니다. Hello 이름만 변경 되었습니다. 기능이 변경되지 않았습니다.
  * 정적 라우팅 = 정책 기반
  * 동적 라우팅 = 경로 기반
* 다른 설명이 없는 한 고성능 VPN 게이트웨이와 RouteBased VPN 게이트웨이에 대 한 사양이 동일 하지만, hello 됩니다. 예를 들어 RouteBased VPN 게이트웨이 호환 되는 유효성을 검사 하는 hello VPN 장치 고성능 VPN 게이트웨이 hello와 호환 됩니다.

## <a name="devicetable"></a>확인된 VPN 장치 및 장치 구성 가이드

> [!NOTE]
> 사이트 간 연결을 구성할 때 VPN 장치에 공용 IPv4 IP 주소가 필요합니다.
>

장치 공급업체와 협력하여 표준 VPN 장치 집합의 유효성을 검사했습니다. 모든 hello 목록 다음에 hello 장치 제품군의 hello 장치의 VPN 게이트웨이 작동 해야 합니다. 참조 [VPN 게이트웨이 설정에 대 한](vpn-gateway-about-vpn-gateway-settings.md#vpntype) toounderstand hello VPN hello tooconfigure VPN 게이트웨이 솔루션에 대 한 use (PolicyBased 또는 RouteBased)를 입력 합니다.

toohelp은 VPN 장치를 구성 하려면이 tooappropriate 장치 제품군에 해당 하는 toohello 링크를 참조 하십시오. 최선의 노력을 기반으로 hello 링크 tooconfiguration 지침이 제공 됩니다. VPN 장치 지원은 장치 제조업체에 문의하세요.

|**공급업체**          |**장치 패밀리**     |**최소 OS 버전** |**정책 기반 구성 지침** |**경로 기반 구성 지침** |
| ---                | ---                  | ---                   | ---            | ---           |
| A10 Networks, Inc. |Thunder CFW           |ACOS 4.1.1             |호환되지 않음  |[구성 가이드](https://www.a10networks.com/resources/deployment-guides/a10-thunder-cfw-ipsec-vpn-interoperability-azure-vpn-gateways)|
| Allied Telesis     |AR 시리즈 VPN 라우터 |2.9.2                  |곧 출시됩니다     |호환되지 않음  |
| Barracuda Networks, Inc. |Barracuda NextGen 방화벽 F 시리즈 |정책 기반: 5.4.3<br>경로 기반: 6.2.0 |[구성 가이드](https://techlib.barracuda.com/NGF/AzurePolicyBasedVPNGW) |[구성 가이드](https://techlib.barracuda.com/NGF/AzureRouteBasedVPNGW) |
| Barracuda Networks, Inc. |Barracuda NextGen 방화벽 X 시리즈 |Barracuda Firewall 6.5 |[구성 가이드](https://techlib.barracuda.com/BFW/ConfigAzureVPNGateway) |호환되지 않음 |
| Brocade            |Vyatta 5400 vRouter   |Virtual Router 6.6R3 GA|[구성 가이드](http://www1.brocade.com/downloads/documents/html_product_manuals/vyatta/vyatta_5400_manual/wwhelp/wwhimpl/js/html/wwhelp.htm#href=VPN_Site-to-Site%20IPsec%20VPN/Preface.1.1.html) |호환되지 않음 |
| Check Point |Security Gateway |R77.30 |[구성 가이드](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |[구성 가이드](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |
| 시스코              |ASA       |8.3 |[구성 샘플](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASA) |호환되지 않음 |
| 시스코 |ASR |정책 기반: IOS 15.1<br>경로 기반: IOS 15.2 |[구성 샘플](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |[구성 샘플](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |
| 시스코 |ISR |정책 기반: IOS 15.0<br>경로 기반*: IOS 15.1 |[구성 샘플](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |[구성 샘플*](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |
| Citrix |NetScaler MPX, SDX, VPX |10.1 이상 |[구성 가이드](https://docs.citrix.com/en-us/netscaler/11-1/system/cloudbridge-connector-introduction/cloudbridge-connector-azure.html) |호환되지 않음 |
| F5 |BIG-IP 시리즈 |12.0 |[구성 가이드](https://devcentral.f5.com/articles/connecting-to-windows-azure-with-the-big-ip) |[구성 가이드](https://devcentral.f5.com/articles/big-ip-to-azure-dynamic-ipsec-tunneling) |
| Fortinet |FortiGate |FortiOS 5.4.2 |  |[구성 가이드](http://cookbook.fortinet.com/ipsec-vpn-microsoft-azure-54) |
| IIJ(Internet Initiative Japan) |SEIL 시리즈 |SEIL/X 4.60<br>SEIL/B1 4.60<br>SEIL/x86 3.20 |[구성 가이드](http://www.iij.ad.jp/biz/seil/ConfigAzureSEILVPN.pdf) |호환되지 않음 |
| Juniper |SRX |정책 기반: JunOS 10.2<br>경로 기반: JunOS 11.4 |[구성 샘플](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |[구성 샘플](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |
| Juniper |J 시리즈 |정책 기반: JunOS 10.4r9<br>경로 기반: JunOS 11.4 |[구성 샘플](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |[구성 샘플](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |
| Juniper |ISG |ScreenOS 6.3 |[구성 샘플](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |[구성 샘플](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |
| Juniper |SSG |ScreenOS 6.2 |[구성 샘플](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |[구성 샘플](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |
| Microsoft |라우팅 및 원격 액세스 서비스 |Windows Server 2012 |호환되지 않음 |[구성 샘플](http://go.microsoft.com/fwlink/p/?LinkId=717761) |
| 개방형 시스템 AG |핵심 업무 제어 보안 게이트웨이 |해당 없음 |[구성 가이드](https://www.open.ch/_pdf/Azure/AzureVPNSetup_Installation_Guide.pdf) |호환되지 않음 |
| Openswan |Openswan |2.6.32 |(출시 예정) |호환되지 않음 |
| Palo Alto Networks |PAN-OS를 실행하는 모든 장치 |PAN-OS<br>정책 기반: 6.1.5 이상<br>경로 기반: 7.1.4 |[구성 가이드](https://live.paloaltonetworks.com/t5/Configuration-Articles/How-to-Configure-VPN-Tunnel-Between-a-Palo-Alto-Networks/ta-p/59065) |[구성 가이드](https://live.paloaltonetworks.com/t5/Integration-Articles/Configuring-IKEv2-VPN-for-Microsoft-Azure-Environment/ta-p/60340) |
| SonicWall |TZ 시리즈, NSA 시리즈<br>SuperMassive 시리즈<br>E-클래스 NSA 시리즈 |SonicOS 5.8.x<br>SonicOS 5.9.x<br>SonicOS 6.x |[SonicOS 6.2에 대한 구성 가이드](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[SonicOS 5.9에 대한 구성 가이드](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |[SonicOS 6.2에 대한 구성 가이드](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[SonicOS 5.9에 대한 구성 가이드](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |
| WatchGuard |모두 |Fireware XTM<br> 정책 기반: v11.11.x<br>경로 기반: v11.12.x |[구성 가이드](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA2F00000000LI7KAM&lang=en_US) |[구성 가이드](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA22A000000XZogSAG&lang=en_US)|

(*) ISR 7200 시리즈 라우터는 정책 기반 VPN만을 지원합니다.

## <a name="additionaldevices"></a>확인되지 않은 VPN 장치

Hello 유효성을 검사 하는 VPN 장치 표에 나열 된 장치가 표시 되지 않으면, 장치 수 에서도 계속 작동 한 사이트 간 연결입니다. 추가 지원 및 구성 지침은 장치 제조업체에 문의하세요.

## <a name="editing"></a>장치 구성 샘플 편집

Tooreplace 해야 hello 제공 된 VPN 장치 구성 샘플을 다운로드 한 후 사용자 환경에 대 한 tooreflect hello 설정을 hello의 일부 값입니다.

### <a name="tooedit-a-sample"></a>tooedit 샘플:

1. 메모장을 사용 하 여 hello 샘플을 엽니다.
2. 찾기 및 바꾸기 모두 <*텍스트*> tooyour 환경 관련 된 hello 값이 포함 된 문자열입니다. 수 있는지 tooinclude < 및 >입니다. 이름이 지정 된 경우에 선택한 hello 이름은 고유 해야 합니다. 명령이 작동하지 않는 경우 해당 장치 제조업체 설명서를 참조하세요.

| **샘플 텍스트** | **변경** |
| --- | --- |
| &lt;RP_OnPremisesNetwork&gt; |이 개체에 대해 선택한 이름입니다. 예: myOnPremisesNetwork |
| &lt;RP_AzureNetwork&gt; |이 개체에 대해 선택한 이름입니다. 예: myAzureNetwork |
| &lt;RP_AccessList&gt; |이 개체에 대해 선택한 이름입니다. 예: myAzureAccessList |
| &lt;RP_IPSecTransformSet&gt; |이 개체에 대해 선택한 이름입니다. 예: myIPSecTransformSet |
| &lt;RP_IPSecCryptoMap&gt; |이 개체에 대해 선택한 이름입니다. 예: myIPSecCryptoMap |
| &lt;SP_AzureNetworkIpRange&gt; |범위를 지정합니다. 예: 192.168.0.0 |
| &lt;SP_AzureNetworkSubnetMask&gt; |서브넷 마스크를 지정합니다. 예: 255.255.0.0 |
| &lt;SP_OnPremisesNetworkIpRange&gt; |온-프레미스 범위를 지정합니다. 예: 10.2.1.0 |
| &lt;SP_OnPremisesNetworkSubnetMask&gt; |온-프레미스 서브넷 마스크를 지정합니다. 예: 255.255.255.0 |
| &lt;SP_AzureGatewayIpAddress&gt; |이 정보 특정 tooyour 가상 네트워크 hello 관리 포털에서에서 볼 수 있으며으로 **게이트웨이 IP 주소**합니다. |
| &lt;SP_PresharedKey&gt; |이 정보는 특정 tooyour 가상 네트워크 및 hello 관리 키로 관리 포털에에서 있는 합니다. |

## <a name="ipsec"></a>IPsec/IKE 매개 변수

> [!NOTE]
> 다음 표에 hello에 나열 된 hello 값 지원 되지만 hello VPN 게이트웨이에서 현재 없는 메커니즘은 없습니다 있습니다 toospecify 하거나 hello VPN 게이트웨이 매개 변수 이거나 이들 알고리즘의 특정 조합을 선택 합니다. Hello 온-프레미스 VPN 장치에서 모든 제약 조건을 지정 해야 합니다. 또한 **MSS**를 **1350**에 고정해야 합니다.
> 
>

다음 표에서 hello에서:

* SA = 보안 연결
* IKE 1단계는 "주 모드"라고도 합니다.
* IKE 2단계는 "빠른 모드"라고도 합니다.

### <a name="ike-phase-1-main-mode-parameters"></a>IKE 1단계(주 모드) 매개 변수

| **속성**          |**정책 기반**    | **경로 기반**    |
| ---                   | ---               | ---               |
| IKE 버전           |IKEv1              |IKEv2              |
| Diffie-Hellman 그룹  |그룹 2(1024비트) |그룹 2(1024비트) |
| 인증 방법 |미리 공유한 키     |미리 공유한 키     |
| 암호화 및 해싱 알고리즘 |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |1. AES256, SHA1<br>2. AES256, SHA256<br>3. AES128, SHA1<br>4. AES128, SHA256<br>5. 3DES, SHA1<br>6. 3DES, SHA256 |
| SA 수명           |28,800초     |28,800초     |

### <a name="ike-phase-2-quick-mode-parameters"></a>IKE 2단계(빠른 모드) 매개 변수

| **속성**                  |**정책 기반**| **경로 기반**                              |
| ---                           | ---           | ---                                         |
| IKE 버전                   |IKEv1          |IKEv2                                        |
| 암호화 및 해싱 알고리즘 |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |[RouteBased QM SA 제품](#RouteBasedOffers) |
| SA 수명(시간)            |3,600초  |27,000초                                |
| SA 수명(바이트)           |102,400,000 KB | -                                           |
| PFS(Perfect Forward Secrecy) |아니요             |[RouteBased QM SA 제품](#RouteBasedOffers) |
| 작동하지 않는 피어 검색(DPD)     |지원되지 않음  |지원됨                                    |


### <a name ="RouteBasedOffers"></a>RouteBased VPN IPsec 보안 연결(IKE 빠른 모드 SA) 제품

hello 다음 표에 나열 IPsec SA (IKE 빠른 모드) 제공 합니다. 제안 나열 된 hello 순서는 해당 hello 제품 기본 설정의 제시 되었거나 수락 합니다.

#### <a name="azure-gateway-as-initiator"></a>Azure 게이트웨이(초기자)

|-  |**암호화**|**인증**|**PFS 그룹**|
|---| ---          |---               |---          |
| 1 |GCM AES256    |GCM(AES256)      |없음         |
| 2 |AES256        |SHA1              |없음         |
| 3 |3DES          |SHA1              |없음         |
| 4 |AES256        |SHA256            |없음         |
| 5 |AES128        |SHA1              |없음         |
| 6 |3DES          |SHA256            |없음         |

#### <a name="azure-gateway-as-responder"></a>Azure 게이트웨이(응답자)

|-  |**암호화**|**인증**|**PFS 그룹**|
|---| ---          | ---              |---          |
| 1 |GCM AES256    |GCM(AES256)      |없음         |
| 2 |AES256        |SHA1              |없음         |
| 3 |3DES          |SHA1              |없음         |
| 4 |AES256        |SHA256            |없음         |
| 5 |AES128        |SHA1              |없음         |
| 6 |3DES          |SHA256            |없음         |
| 7 |DES           |SHA1              |없음         |
| 8 |AES256        |SHA1              |1            |
| 9 |AES256        |SHA1              |2            |
| 10|AES256        |SHA1              |14           |
| 11|AES128        |SHA1              |1            |
| 12|AES128        |SHA1              |2            |
| 13|AES128        |SHA1              |14           |
| 14|3DES          |SHA1              |1            |
| 15|3DES          |SHA1              |2            |
| 16|3DES          |SHA256            |2            |
| 17|AES256        |SHA256            |1            |
| 18|AES256        |SHA256            |2            |
| 19|AES256        |SHA256            |14           |
| 20|AES256        |SHA1              |24           |
| 21|AES256        |SHA256            |24           |
| 22|AES128        |SHA256            |없음         |
| 23|AES128        |SHA256            |1            |
| 24|AES128        |SHA256            |2            |
| 25|AES128        |SHA256            |14           |
| 26|3DES          |SHA1              |14           |

* 경로 기반 및 고성능 VPN 게이트웨이를 사용하여 IPsec ESP NULL 암호화를 지정할 수 있습니다. Null 기반된 암호화는 전송 중에 보호 toodata를 제공 하지 않으며 최대 때에 사용 해야 처리량 및 최소 대기 시간이 요구 됩니다. 클라이언트 또는 선택할 수 toouse이 VNet 대 VNet 통신 시나리오에서 암호화 hello 솔루션의 다른 곳에서 적용 되는 경우.
* Hello 인터넷을 통해 크로스-프레미스 연결을 위한 암호화 및 해시 알고리즘에 중요 한 통신의 보안을 tooensure 위에 hello 표에 나열 된 hello 기본 Azure VPN 게이트웨이 설정을 사용 합니다.

## <a name="known"></a>알려진 장치 호환성 문제

> [!IMPORTANT]
> 이러한 타사 VPN 장치 및 Azure VPN 게이트웨이 간에 알려진된 호환성 문제가 hello 됩니다. Azure 팀 hello tooaddress hello 여기에 나열 된 문제는 hello 공급 업체와 적극적으로 노력 합니다. Hello 문제가 해결 되 면이 페이지는 hello 가장 최신 정보로 업데이트 됩니다. 주기적으로 다시 확인하세요.
>
>

### <a name="feb-16-2017"></a>2017년 2월 16일

**이전 too7.1.4 버전을 사용 하 여 팔로 알토 네트워크 장치** Azure 경로 기반 VPN에 대 한: PAN-OS 버전 이전 too7.1.4를 팔로 알토 네트워크에서 VPN 장치를 사용 하 고 연결을 발생 하는 발급 tooAzure 경로 기반 VPN 게이트웨이 hello 다음 단계를 수행 합니다.

1. 팔로 알토 네트워크 장치의 hello 펌웨어 버전을 확인 합니다. PAN-OS 버전이 7.1.4 보다 오래 된 경우 too7.1.4를 업그레이드 합니다.
2. Hello 팔로 알토 네트워크 장치에서 변경 hello 단계 2 SA (또는 빠른 모드 SA) 수명 too28 800 초 (8 시간) 경우 toohello Azure VPN 게이트웨이 연결 합니다.
3. 연결 문제가 여전히 발생 하는 hello Azure 포털에서에서 지원 요청을 개시 합니다.
