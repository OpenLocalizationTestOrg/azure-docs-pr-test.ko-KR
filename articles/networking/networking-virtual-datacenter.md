---
title: "Azure 가상 데이터 센터 aaaMicrosoft | Microsoft Docs"
description: "어떻게 toobuild 가상 데이터는 Azure에서을 가운데에 대해 알아봅니다"
services: networking
author: tracsman
manager: rossort
tags: azure-resource-manager
ms.service: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jonor
ms.openlocfilehash: 84f77b16edaece202a6a94b6107f1c9585ec7f38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-virtual-data-center"></a>Microsoft Azure 가상 데이터 센터
**Microsoft Azure**: 더 빠른 이동, 비용 절감, 온-프레미스 앱 및 데이터 통합

## <a name="overview"></a>개요
온-프레미스 응용 프로그램 tooAzure 마이그레이션, 중요 한 모든 변경 (접근 방식 "리프트 및 이동" 이라는) 없이 조직 hello 이점을 제공 하는 보안 및 비용 효율적인 인프라의 합니다. 그러나 toomake hello 가장 hello 민첩성 클라우드 컴퓨팅에 있을 수 있는의 기업에서는 Azure 기능의 아키텍처 tootake 이용 개선 되어야 합니다. Microsoft Azure는 대규모 서비스와 인프라, 엔터프라이즈급 기능과 안정성, 여러 하이브리드 연결 옵션을 제공합니다. 고객은 이러한 클라우드 서비스 중 하나를 통해 tooaccess hello 인터넷 또는 개인 네트워크 연결을 제공 하는 Azure ExpressRoute를 사용 선택할 수 있습니다. hello Microsoft Azure 플랫폼에는 고객을 tooseamlessly hello 클라우드로 인프라를 확장 하 고 다중 계층 아키텍처를 구축할 수 있습니다. 또한 보안 서비스를 제공 하 여 향상 된 기능을 제공 하는 Microsoft 파트너와는 가상 어플라이언스 Azure에서 toorun 최적화.

사용 되는 toosolve 일 수 있는 디자인 hello toohello 클라우드 일괄적 이동에 대 한를 고려할 때 많은 고객이 직면 아키텍처 확장성, 성능 및 보안 문제 및이 문서 패턴에 대 한 개요를 제공 합니다. 어떻게 toofit 다른 조직의 IT 역할 hello 관리 및 거 버 넌 스의 hello 시스템에도 설명 강조 toosecurity 요구 사항 및 비용 최적화의 개요.

## <a name="what-is-a-virtual-data-center"></a>가상 데이터 센터란 무엇일까요?
Hello에 초기 클라우드 솔루션 hello 공용 스펙트럼에서 설계 된 toohost 단일, 상대적으로 격리 된 응용 프로그램 되었습니다. 이 접근 방식은 몇 년 동안은 문제가 없었습니다. 그러나 클라우드 hello 혜택으로 솔루션 분명해 및 대규모 워크 로드를 여러 보안, 안정성, 성능, 주소 지정 hello 클라우드에 호스트 이었으며 하나에 배포의 문제를 비용 했거나 더 많은 영역이 hello 전체에서 중요 한 hello 클라우드 서비스의 수명 주기 합니다.

hello 다음 클라우드 배포 다이어그램에서는 보안 결함 (빨간색 상자) 및 최적화 네트워크 가상 어플라이언스를 위한 공간이의 몇 가지 예 (노란색 상자) 워크 로드 간에

[![0]][0]

hello 가상 데이터 센터 vDC ()이이 필요 toosupport 엔터프라이즈 작업 크기 조정에서 탄생 했으며 및 hello hello 공용 클라우드에서 대규모 응용 프로그램을 지 원하는 변환할 때 hello 문제가 있는 toodeal 필요 합니다.

VDC는 hello 클라우드 하지만 또한 hello 네트워크, 보안, 관리 및 인프라 (예: DNS 및 디렉터리 서비스)에서 응용 프로그램 작업 방금 hello 않습니다. 일반적으로 제공 개인 연결 백 tooan 온-프레미스 네트워크 또는 데이터 센터 합니다. 점점 더 많은 작업 tooAzure을 이동할 때 인프라 및 개체를 지 원하는 hello에 대 한 이러한 작업에 있는 중요 한 toothink 합니다. 리소스 구성 방법에 대해 신중 하 게 생각 수백 대의 독립적인 데이터 흐름, 보안 모델 및 규정 준수 문제를 사용 하 여 별도로 관리 해야 합니다 "워크 로드 아일랜드"의 hello 급증을 피할 수 있습니다.

가상 데이터 센터는 기본적으로 일반적인 지원 기능, 특성 및 인프라를 갖는 별개이면서도 연관된 엔터티의 모음입니다. 인해 비용 절감된을 실현할 수 통합된 vDC로 작업을 확인 하 여 구성 요소 및 데이터를 통해 최적화 된 보안 범위의 tooeconomies 흐름 쉽게 작업, 관리 및 규정 준수 감사 함께 중앙 집중화 합니다.

> [!NOTE]
> VDC hello toounderstand은 반드시 **하지** 별도 Azure 제품 하지만 다양 한 특징과 기능 hello 조합 너무 정확한 요구 사항을 충족 합니다. vDC는 리소스와 hello 클라우드의 작업 및 Azure 사용량 toomaximize에 대해 생각 하는 방법입니다. hello 가상 DC가 따라서 방법에 대 한 모듈 방식이 toobuild hello 조직 역할 및 책임을 유지 하는 Azure의에서 IT 서비스를 구성 합니다.

hello vDC 기업 hello 다음 시나리오에 대 한 작업 및 Azure에 응용 프로그램을 가져올 수 있습니다.

-   여러 관련 워크로드 호스트
-   온-프레미스 환경 tooAzure에서 마이그레이션 작업
-   워크로드에 대해 공유 또는 중앙 집중식 보안과 액세스 요구 사항 구현
-   대기업에 적합하게 DevOps 및 중앙 집중식 IT 혼합

vdc 키 toounlock hello 장점 hello, Azure 기능을 조합 하 여 중앙 집중식된 토폴로지 (허브 및 스포크)가: [Azure VNet][VNet], [Nsg] [ NSG], [VNet 피어 링][VNetPeering], [사용자 정의 경로 (UDR)][UDR], 및와 Azure Id [ 역할 기본 액세스 제어 (RBAC)][RBAC]합니다.

## <a name="who-needs-a-virtual-data-center"></a>가상 데이터 센터는 누구에게 필요할까요?
몇 가지 작업을 Azure에 둘 이상의 toomove 필요한 모든 Azure 고객은 공용 리소스를 사용 하 여 생각에서 유용할 수 있습니다. Hello 크기에 따라 hello 패턴을 사용 하 여에서 도움이 될 것도 단일 응용 프로그램 및 구성 요소는 vDC toobuild를 사용 합니다.

조직에 중앙 집중식된 IT, 네트워크, 보안, 규정 준수 팀/부서 정책 지점, 의무를 분리를 적용 하 고 많은 응용 프로그램 팀을 제공 하는 동안 공통 구성 요소를 기본 hello의 일관성을 유지 vDC 시킬 수 있습니다 및/또는 자유로움 / 컨트롤은 요구 사항에 적합 합니다.

TooDevOps를 모색 중인 조직이 hello 네트워크 하지만 tooprovide 다 수의 Azure 리소스에 권한이 있고 완전히 제어 (구독 또는 리소스 그룹에 공통 구독), 해당 그룹 내의 갖추어야 hello vDC 개념을 활용할 수 있습니다 및 보안 경계 규격 중앙 집중식된 정책 허브 VNet 및 리소스 그룹에 의해 정의 된 대로 유지 됩니다.

## <a name="considerations-on-implementing-a-virtual-data-center"></a>가상 데이터 센터 구현 시 고려 사항
VDC을 디자인할 때 중요 문제 tooconsider 여러 가지가 있습니다.

-   ID 및 디렉터리 서비스
-   보안 인프라
-   연결 toohello 클라우드
-   Hello 클라우드 내의 연결

##### <a name="identity-and-directory-service"></a>*ID 및 디렉터리 서비스*
Id 및 디렉터리 서비스는 모든 데이터의 중요 한 측면 센터, 온-프레미스 및 클라우드 hello 합니다. Id는 hello vDC 내에서 액세스 및 권한 부여 tooservices의 관련된 tooall 측면입니다. toohelp은 Azure 계정에 액세스 권한이 있는 사용자 및 프로세스가 고 리소스에 Azure 인증에 대 한 몇 가지 유형의 자격 증명을 사용 하는지 확인 합니다. 여기에 암호 (tooaccess는 Azure 계정 hello), 암호화 키, 디지털 서명 및 인증서 포함 됩니다. [*Azure MFA(Multi-factor Authentication)*][MFA]는 Azure 서비스 액세스에 대한 추가적인 보안 계층입니다. 쉽게 확인 옵션의 범위를 강력한 인증을 제공 하는 azure MFA-전화 통화, 문자 메시지 또는 모바일 앱 알림-원하는 toochoose hello 방법에서 고객 수 및 합니다.

모든 대기업 toodefine 개별 id의 hello 관리, 인증, 권한 부여, 역할 및 권한 또는 hello vDC 다른에서 설명 하는 식별 관리 프로세스가 필요 합니다. 이 프로세스의 hello 목표 비용, 가동 중지 시간 및 반복적인 수동 작업 택 tooincrease 보안 및 생산성 이어야 합니다.

엔터프라이즈/조직은 다양한 LOB(기간 업무)를 위한 까다로운 서비스 조합을 요구할 수 있으며, 직원들은 종종 프로젝트마다 다른 역할을 맡게 됩니다. 특정 역할 정의 좋은 거 버 넌 스를 실행 하는 tooget 시스템 각각 서로 다른 팀 간에 좋은 협력을 해야 하는 vDC 합니다. 책임, 액세스 및 권한을의 hello 매트릭스는 매우 복잡할 수 있습니다. vDC의 ID 관리는 [*AAD(Azure Active Directory)*][AAD] 및 RBAC(역할 기반 액세스 제어)를 통해 구현됩니다.

디렉터리 서비스는 매일의 항목 및 네트워크 리소스를 찾고, 관리하고, 운영하고, 구성하기 위한 공유 정보 인프라입니다. 이러한 리소스에는 볼륨, 폴더, 파일, 프린터, 사용자, 그룹, 장치 및 기타 개체가 포함될 수 있습니다. 각 네트워크 리소스에 hello hello 디렉터리 서버에서 개체로 간주 됩니다. 리소스에 대한 정보는 해당 리소스 또는 개체와 연결된 특성 모음으로 저장됩니다.

모든 Microsoft Online 비즈니스 서비스는 로그온 및 기타 ID가 필요로 할 때 AAD(Azure Active Directory)를 사용합니다. Azure Active Directory는 핵심 디렉터리 서비스, 고급 ID 관리 및 응용 프로그램 액세스 관리를 통합하는 포괄적이고 항상 사용가능한 ID 및 액세스 관리 클라우드 솔루션입니다. AAD는 tooenable single sign-on에 대 한 모든 클라우드 기반 및 호스트 (온-프레미스) 응용 프로그램을 로컬 온-프레미스 Active Directory와 통합할 수 있습니다. 온-프레미스 Active Directory의 사용자 특성 hello tooAAD 자동으로 동기화 될 수 있습니다.

한 명의 전역 관리자는 필요 하지 않음 tooassign vDC 모든 사용 권한입니다. 대신 각 특정 부서 (또는 hello 디렉터리 서비스에서에서 서비스 또는 사용자 그룹) hello 권한이 필요한 toomanage vDC 내에서 고유한 리소스가 있을 수 있습니다. 사용 권한을 구성할 때는 균형을 유지해야 합니다. 너무 많은 권한을 부여하면 성능 효율성이 저하될 수 있고, 권한이 너무 적거나 느슨하면 보안 위험이 높아질 수 있습니다. Azure 역할 기반 액세스 제어 (RBAC) vDC 리소스에 대 한 세분화 된 액세스 관리를 제공 하 여 tooaddress이이 문제를 수 있습니다.

##### <a name="security-infrastructure"></a>*보안 인프라*
보안 인프라는 vdc hello 컨텍스트에서 hello vDC 특정 가상 네트워크 세그먼트와 toocontrol ingress 및 egress hello vDC 전체에서 이동 하는 방법에 대 한 트래픽의 주로 관련된 toohello 분리입니다. Azure는 배포 간에 허가되지 않고 의도하지 않은 트래픽을 방지하는 다중 테넌트 아키텍처를 기반으로 하며, VNet(가상 네트워크) 격리, ACL(액세스 제어 목록), 부하 분산 장치 및 IP 필터와 트래픽 흐름 정책을 사용합니다. NAT(네트워크 주소 변환)는 외부 트래픽에서 내부 네트워크 트래픽을 분리합니다.

Azure 패브릭이 hello tootenant 작업 인프라 리소스를 할당 하 고 가상 컴퓨터 (Vm)에서 통신 tooand를 관리 합니다. hello Azure 하이퍼바이저 Vm와 안전 하 게 테 넌 트 네트워크 트래픽 tooguest OS 경로 간의 메모리와 프로세스 분리를 적용합니다.

##### <a name="connectivity-toohello-cloud"></a>*연결 toohello 클라우드*
hello vDC toooffer 서비스 toocustomers 외부 네트워크, 파트너 및/또는 내부 사용자와 연결 되어 있어야 합니다. 이 경우 대체로 연결 toohello 인터넷 뿐만 아니라 tooon 온-프레미스 네트워크 및 데이터 센터입니다.

고객의 보안 정책 toocontrol 무엇을 빌드하고 수 특정 vDC 호스팅된 서비스에서 액세스할 수 있는 방법 hello 필터링 및 트래픽 검사), (된 네트워크 가상 어플라이언스 및 사용자 지정 라우팅 정책을 필터링 (네트워크를 사용 하 여 인터넷 사용자 정의 라우팅 및 네트워크 보안 그룹).

기업에서는 tooconnect 개의 Vdc tooon 온-프레미스 데이터 센터 또는 기타 리소스를 필요한 경우가 많습니다. hello Azure와 온-프레미스 네트워크 간의 연결이 따라서 중요 한 요소 효과적인 아키텍처를 설계할 때 합니다. 기업에서는 두 가지 방법으로 toocreate vDC과 온-프레미스 간 연결는 Azure에 있는: hello 인터넷을 통해 및/또는 개인 직접 연결 하 여 전송 합니다.

[ **Azure 사이트 간 VPN** ] [ VPN] 온-프레미스 네트워크 간의 인터넷 hello를 통해 상호 연결 하는 서비스 되 고 보안을 통해 설정 하는 hello vDC 암호화 연결 (IPsec/IKE 터널)입니다. Azure 사이트 간 연결 유연 하 고 빠른 toocreate 되며 모든 추가 조달 필요 하지 않습니다, 그리고 모든 연결을 통해 연결 하는 대로 hello 인터넷 합니다.

[**ExpressRoute** ] [ ExR] vDC와 hello 간에 개인 연결 온-프레미스 네트워크를 만들 수 있는 Azure 연결 서비스입니다. ExpressRoute 연결은 공용 인터넷을 hello를 보다 높은 수준의 보안, 안정성 및 일관 된 대기 시간 함께 too10 g b p s) (위쪽 빠른 속도 제공 합니다. 계속 이동 하지 마십시오. ExpressRoute는 ExpressRoute 고객은 규정 준수 규칙에 개인 연결 연관의 hello 이점을 얻을 수로, 개의 Vdc에 매우 유용 합니다.

ExpressRoute 연결을 배포할 때는 ExpressRoute 서비스 공급자와 연계해야 합니다. Toostart를 신속 하 게 해야 하는 고객에 대 한 일반적으로 tooinitially 사용 hello vDC과 온-프레미스 리소스 간의 사이트 간 VPN tooestablish 연결 되며 다음 tooExpressRoute 연결을 마이그레이션합니다.

##### <a name="connectivity-within-hello-cloud"></a>*Hello 클라우드 내의 연결*
[Vnet] [ VNet] 및 [VNet 피어 링] [ VNetPeering] 는 hello 기본 네트워킹 vDC 내 연결 서비스입니다. VNet vDC 리소스에 대 한 격리의 자연 경계를 보장 하 고 hello 내에서 서로 다른 Vnet 간의 상호 통신을 허용 VNet 피어 링 동일한 Azure 지역에 있습니다. VNet 내 및 Vnet 간의 트래픽 제어 필요 toomatch 집합이 한 보안 액세스 제어 목록을 통해 지정 된 규칙 ([네트워크 보안 그룹][NSG]), [네트워크 가상 어플라이언스 ] [ NVA], 및 사용자 지정 라우팅 테이블 ([UDR][UDR]).

## <a name="virtual-data-center-overview"></a>가상 데이터 센터 개요

### <a name="topology"></a>토폴로지
허브 및 스포크 모델는 단일 Azure 지역 내에서 확장 된 hello 가상 데이터 센터

[![1]][1]

hello 허브는 제어 하 고 다른 영역은 ingress 및 egress 트래픽을 검사 하는 hello 중앙 영역: 인터넷, 온-프레미스, 바퀴 살 hello 및 합니다. hello 허브 및 스포크 토폴로지 잘못 된 구성 및 노출 하는 것에 대 한 hello 절감 하면서 hello IT 부서를 중앙 위치에 효과적으로 tooenforce 보안 정책을 제공 합니다.

hello 허브 hello 공통 서비스 구성 요소에서 hello 스포크 사용을 포함 합니다. 일반적인 중앙 서비스의 몇 가지 예는 다음과 같습니다.

-   hello Windows Active Directory 인프라 (hello로 ADFS 서비스 관련) 사용자 인증을 제 3 자에서 가져오는 액세스 toohello 작업 hello 스포크 전에에서 신뢰할 수 없는 네트워크에 액세스 하는 데 필요한
-   Hello 스포크 tooaccess 리소스 온-프레미스 및 인터넷 hello에 hello 작업에 대 한 DNS 서비스 tooresolve 명명
-   Tooimplement single sign on 워크 로드에는 PKI 인프라
-   Hello 스포크와 인터넷 간에 흐름 제어 (TCP/UDP)
-   Hello 스포크와 온-프레미스 간 흐름 제어
-   원할 경우 한 스포크와 다른 스포크 간의 흐름 제어

hello vDC 여러 하며 스포크 간에 hello 공유 허브 인프라를 사용 하 여 전반적인 비용을 줄입니다.

각 스포크의 hello role toohost 다른 유형의 작업을 사용할 수 있습니다. hello 스포크 제공할 수도 모듈식 방법을 반복 가능한 배포 (예를 들어, 개발 및 사용자 수용 테스트, 테스트, 사전 프로덕션 및 프로덕션) hello의 동일한 작업 합니다. hello 스포크 toosegregate 사용된 될 수 있고 조직 (예를 들어 DevOps 그룹) 내에서 서로 다른 그룹을 사용 하도록 설정 합니다. 스포크 내 것이 가능한 toodeploy hello 계층 간에 제어 하는 기본 작업이 나 트래픽이 복잡 한 다중 계층 작업 합니다.

##### <a name="subscription-limits-and-multiple-hubs"></a>구독 제한 및 다중 허브
Azure의 hello 형식에 관계 없이 모든 구성 요소는 Azure 구독에 배포 됩니다. 서로 다른 Azure 구독에 Azure 구성 요소의 hello 격리 차별화 된 수준의 액세스 및 권한 부여를 설정 하는 등의 다른 Lob의 hello 요구 사항을 충족할 수 있습니다.

모든 IT 시스템에서와 마찬가지로 플랫폼 제한 하지만 단일 vDC 스포크 toolarge 수를 확장할 수 있습니다. hello 허브 배포는 바인딩된 tooa 특정 있는 Azure 구독에 제한 사항 및 제한 (최대 수가 VNet 피어 링-참조 하는 예를 들어 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건] [ Limits] 세부 정보에 대 한). Hello 아키텍처 확장할 수 제한 문제가 될 수 있는 경우에서 최대 허브 및 스포크 단일 허브-스포크 tooa 클러스터에서 hello 모델을 확장 하 여 추가 합니다. 하나 이상의 Azure 지역에 있는 여러 허브를 Express Route 또는 사이트 간 VPN을 사용하여 상호 연결할 수 있습니다.

[![2]][2]

hello 여러 허브 hello 시스템의 hello 비용 및 관리 작업을 증가 하 고 확장성 맞춰집니다 것 (예: 시스템 한계 또는 중복) 및 지역 복제 (예: 최종 사용자 성능 또는 재해 복구). 여러 허브를 요구 하는 시나리오에서는 모든 hello 허브 손쉬운에 대 한 서비스 설정 동일 toooffer hello를 노력 해야 합니다.

##### <a name="interconnection-between-spokes"></a>스포크 간 상호 연결
단일 스포크 내부 것이 가능한 tooimplement 복잡 한 다중 계층 작업 합니다. 다중 계층 구성은 서브넷 (모든 계층에 대해 각각 하나씩)를 사용 하 여 동일한 VNet과 필터링 hello 흐름 Nsg를 사용 하 여 hello에 구현할 수 있습니다.

다른 손 hello, 설계자 여러 Vnet에서 toodeploy 다중 계층 작업 수 합니다. VNet 피어 링을 사용 하 여, 바퀴 살 연결할 수 tooother 스포크 hello에 동일한 허브 또는 다른 허브입니다. 이 시나리오의 일반적인 예 경우 hello 응용 프로그램 처리 서버에에서 있는 하나의 스포크 (VNet) hello 데이터베이스는 다른 스포크 (VNet)에 배포 되는 동안 합니다. 이 경우 쉽게 toointerconnect VNet 피어 링으로 hello 스포크 되며 hello 허브를 통해 전송 것을 방지할. 신중 하 게 아키텍처 및 보안 검토는 중요 한 보안 또는 감사 hello 허브에만 있을 수 있는 포인트를 무시 하지 않습니다 hello 허브 무시 수행된 tooensure 이어야 합니다.

[![3]][3]

스포크의 허브 역할을 하는 상호 연결 된 tooa 스포크 될 수도 있습니다. 이 방법을 사용 하면 2 단계 계층을 만듭니다: hello 될 hello 상위 수준의 멤버 (수준 0) 스포크 hello 허브 hello 계층의 더 낮은 스포크 (수준 1)입니다. vdc hello 스포크 toohello 온-프레미스 네트워크 또는 인터넷 아웃 tooforward hello 트래픽 toohello 중앙 허브 tooreach가 필요합니다. 두 가지 수준의 허브를 사용 하는 아키텍처 간단한 허브-스포크 관계의 hello 이점을 제거 하는 복잡 한 라우팅 소개 합니다.

Azure에서는 복잡 한 토폴로지에 수 있지만 반복 및 단순은 hello 핵심 원칙 hello vDC 개념 중 하나입니다. toominimize 관리 노력 hello 간단한 허브-스포크 디자인은 hello vDC 참조 아키텍처를 권장 합니다.

### <a name="components"></a>구성 요소
가상 데이터 센터는 4가지 기본 구성 요소 유형, 즉 **인프라**, **경계 네트워크**, **워크로드** 및 **모니터링**으로 구성됩니다.

각 구성 요소 유형은 다양한 Azure 기능 및 리소스로 구성됩니다. 프로그램 vDC 구성 된 여러 구성 요소 형식 및 여러 형태의 링크 만들기 hello 인스턴스 동일한 구성 요소 유형입니다. 예를 들어 다른 응용 프로그램을 나타내는 논리적으로 분리된 여러 다른 워크로드 인스턴스가 있을 수 있습니다. 이러한 다른 구성 요소 종류를 사용 하 고 인스턴스 tooultimately hello vDC를 빌드합니다.

[![4]][4]

hello vDC의 이전 상위 수준 아키텍처에서는 hello 허브-스포크 토폴로지의 여러 영역에 사용 되는 다양 한 구성 요소 형식 hello 다이어그램 hello 아키텍처의 다양 한 부분의 인프라 구성 요소를 보여 줍니다.

모범 사례로(온-프레미스 DC 또는 vDC) 액세스 권한 및 사용 권한을 그룹 기반으로 구성하는 것이 좋습니다. 개별 사용자가 아닌 그룹을 처리하면 여러 팀에서 액세스 정책을 일관되게 유지할 수 있으며 구성 오류를 최소화하는 데도 도움이 됩니다. 적절 한 그룹에서 사용자가 tooand 할당 또는 제거에 특정 사용자의 권한을 hello를 최신 상태로 유지 하는 데 도움이 됩니다.

각 역할 그룹에 있어서 쉽게 tooidentify는 워크 로드와 연결 된 그룹 이름에 고유한 접두사가 있어야 합니다. 예를 들어 인증 서비스를 호스트하는 워크로드에는 *AuthServiceNetOps, AuthServiceSecOps, AuthServiceDevOps, 및 AuthServiceInfraOps*라는 그룹이 있을 수 있습니다. 마찬가지로 대 한 중앙 집중식으로 역할 또는 역할 하지 tooa 특정 서비스와 관련 된, "Corp", 문자 앞 수 *CorpNetOps* 예입니다.

대부분의 조직에서는 다음 역할의 주요 분석 그룹 tooprovide hello의 변형을 사용 하 여:

-   hello *중앙 IT 그룹이 있어 (Corp)* hello 소유권 권한을 toocontrol 인프라 (예: 네트워킹 및 보안) 구성 요소가 및 따라서 hello 구독에서 참가자의 toohave hello 역할 (하며 제어 hello 허브) 및 네트워크 hello 스포크에서 참가자 권한. 대기업에서는 이러한 관리 책임을 네트워크 작업(CorpNetOps) 그룹(네트워킹 전용) 및 보안 작업(CorpSecOps) 그룹(방화벽 및 보안 정책 담당)과 같은 여러 팀 간에 분할하는 경우가 많습니다. 이 특정 한 경우에 서로 다른 두 그룹 이러한 사용자 지정 역할 할당을 위해 만든 toobe가 필요 합니다.
-   hello *개발 및 테스트 (AppDevOps) 그룹* hello 책임 toodeploy 작업 (응용 프로그램 또는 서비스). 이 그룹은 IaaS 배포 및/또는 하나에 대 한 가상 컴퓨터 참가자의 hello 역할 또는 더 많은 PaaS 참가자 역할 (참조 [신속히 알아봅니다 액세스 제어에 대 한 기본 제공 역할][Roles]). 필요에 따라 개발 hello 및 테스트 팀 보안 정책 (Nsg) 및 라우팅 정책 (UDR) hello 허브 내 또는 특정 스포크 toohave 가시성을 할 수 있습니다. 따라서 toohello 역할 작업에 대 한 참가자의 추가 사용자를이 그룹도 해야 네트워크 판독기의 hello 역할을 합니다.
-   hello *작업 및 유지 관리 그룹 (CorpInfraOps 또는 AppInfraOps)* hello 수행할 프로덕션 환경에서 작업을 관리 합니다. 이 그룹 toobe 구독 참가자 모든 프로덕션 구독에 대 한 작업에 필요합니다. 프로덕션 환경에서 및 hello 프로덕션에서 순서 toofix 잠재적 구성 문제에 hello 중앙 허브 구독에서 구독 참가자의 hello 역할에 추가 에스컬레이션 지원 팀 그룹 해야 하는 경우에 일부 조직에서는 평가할 수 있습니다. 환경입니다.

VDC는 hello 중앙 IT 그룹이 hello 허브 관리에 대해 만든 그룹 hello 작업 수준에서 해당 그룹을 가질 수 있도록 구성 됩니다. 또한 toomanaging 허브 리소스만 hello 중앙 IT 그룹이 수 toocontrol 외부 액세스 및 hello 구독에 대 한 최상위 권한을 것입니다. 그러나 작업 그룹 수 toocontrol 리소스 및 해당 VNet 중앙 IT에서 독립적으로의 사용 권한을 것입니다.

hello vDC 요구 toobe toosecurely 호스트 여러 프로젝트에서 서로 다른 줄-의-비즈니스 (Lob) 분할 합니다. 모든 프로젝트에는 격리된 다른 환경(개발, UAT, 프로덕션)이 필요합니다. 이러한 각 환경에 대해 별도의 Azure 구독을 유지하면 자연스럽게 격리가 이루어집니다.

[![5]][5]

hello 이전 다이어그램 관계를 보여 줍니다 hello 조직의 프로젝트, 사용자, 그룹 및 hello 환경 hello Azure 구성 요소 배포 되는 위치입니다.

일반적으로 IT 부서에서 환경(또는 계층)은 여러 응용 프로그램이 배포되고 실행되는 시스템입니다. 대기업은 개발 환경(처음에 변경이 수행되고 테스트됨) 및 프로덕션 환경(최종 사용자가 사용)을 사용합니다. 종종 이러한 환경은 여러 스테이징 환경 사이 더 이상 사용 tooallow 배포 (롤아웃), 테스트 및 문제가 있을 경우 롤백할으로 구분 됩니다. 배포 아키텍처 많이 다르지만 일반적으로 개발 (DEV)에서 시작 하 고 프로덕션 (PROD) 끝의 hello 기본 프로세스 계속 연결 합니다.

이러한 종류의 다중 계층 환경에 대한 일반적인 아키텍처는 DevOps(개발 및 테스트), UAT(스테이징) 및 프로덕션 환경으로 구성됩니다. 조직에서는 단일 활용할 수 있습니다 또는 여러 Azure AD는 toodefine 액세스 및 권한을 toothese 환경 테 넌 트가 있습니다. hello 이전 다이어그램 경우를 보여 줍니다 두 개의 서로 다른 Azure AD 테 넌 트 사용: DevOps 및 사용자 수용 테스트, 프로덕션에 대 한 단독으로 다른 hello에 대 한 합니다.

현재 상태를 hello 다른 Azure AD의 테 넌 트 환경 간에 hello 분리를 적용 합니다. 동일한 사용자 그룹을 예를 들어 중앙 IT) (으로 hello hello 역할 중 하나 hello DevOps의 사용 권한 또는 프로젝트의 프로덕션 환경 또는 tooauthenticate 다른 URI tooaccess 다른 AD 테 넌 트를 사용 하 여 수정 해야 합니다. 다른 사용자 인증 tooaccess 다른 환경의 hello 존재 가능한 작동 중단 및 휴먼 오류로 인해 발생 하는 다른 문제가 줄어듭니다.

#### <a name="component-type-infrastructure"></a>구성 요소 유형: 인프라
이 구성 요소 형식은 대부분 hello 지원 인프라의 상주 합니다. 또한 중앙 집중식 IT, 보안 및/또는 규정 준수 팀에는 대부분의 시간을 보내는 위치이기도 합니다.

[![6]][6]

인프라 구성 요소는 vdc hello 다른 구성 요소 간에 상호 연결을 제공 하며 hello 허브 및 스포크 hello 모두에 존재 합니다. hello 관리 및 유지 hello 인프라 구성 요소에 대 한 책임은 일반적으로 할당 toohello 중앙 IT 보안 팀 및/또는 합니다.

Hello hello IT 인프라 팀의 주요 작업 중 하나에 hello 엔터프라이즈 전체에서 IP 주소 스키마의 tooguarantee hello 일관성입니다. hello 개인 IP 주소 할당 된 공간 toohello vDC toobe 일관성 및 온-프레미스 네트워크에 할당 된 개인 IP 주소와 겹치지 필요 합니다.

Hello에 NAT 온-프레미스에 지 라우터 또는 azure에서 환경 IP 주소 충돌을 피할 수, 하는 동안 쿼리 복잡성 tooyour 인프라 구성 요소를 추가 합니다. 관리의 단순성은 hello vDC의 주요 목표 중 하나 이므로 NAT toohandle IP 문제를 사용 하 여 없습니다 권장된 솔루션입니다.

인프라 구성 요소 기능을 수행 하는 hello 포함 되어 있습니다.

-   [**ID 및 디렉터리 서비스**][AAD]. Azure의 액세스 tooevery 리소스 종류는 디렉터리 서비스에 저장 된 id에 의해 제어 됩니다. hello 디렉터리 서비스를 중지 사용자 목록이 hello 뿐 아니라 특정 Azure 구독에 대 한 액세스 권한을 tooresources도 hello 합니다. 이러한 서비스는 클라우드 전용으로 존재하거나 Active Directory에 저장된 온-프레미스 ID와 동기화될 수 있습니다.
-   [**가상 네트워크**][VPN]. 가상 네트워크는 vDC의 주요 구성 요소 중 하나 이며 toocreate hello Azure 플랫폼에서 트래픽 격리 경계를 사용 하도록 설정 합니다. 가상 네트워크는 각각이 특정 IP 네트워크 접두사(서브넷)를 갖는 단일 또는 여러 가상 네트워크 세그먼트로 구성됩니다. 가상 네트워크 hello IaaS 가상 컴퓨터 및 PaaS 서비스 개인 통신을 구성할 수 있는 내부 경계 영역을 정의 합니다. Vm (및 PaaS 서비스) tooVMs (및 PaaS 서비스) 다른 가상 네트워크에서 두 가상 네트워크가 하 여 만들어진 경우에 hello 동일한 고객의 직접 통신할 수 없습니다. 가상 네트워크 하나에 동일한 구독 hello 합니다. 격리는 고객 VM과 통신이 가상 네트워크 안에서 비공개 상태를 유지하는 데 있어 중요한 속성입니다.
-   [**UDR**][UDR]. 가상 네트워크에서 트래픽은 hello 시스템에 대 한 라우팅 테이블을 기반으로 하는 기본적으로 라우팅됩니다. 사용자 정의 경로 네트워크 관리자 tooone 또는 hello 시스템에 대 한 라우팅 테이블의 자세한 서브넷 toooverwrite hello 동작을 연결 하 고 가상 네트워크 내에서 통신 경로 정의할 수는 사용자 지정 라우팅 테이블. 특정 사용자 지정 Vm 및/또는 네트워크 가상 어플라이언스 및 hello 허브와 스포크 hello 동시 있는 부하 분산 장치를 통해 hello 스포크 전송에서 해당 송신 트래픽에 보장 하는 UDRs의 hello 존재 합니다.
-   [**NSG**][NSG]. 네트워크 보안 그룹은 IP 원본, IP 대상, 프로토콜, IP 원본 포트 및 IP 대상 포트에서 트래픽 필터링 역할을 하는 보안 규칙의 목록입니다. hello NSG에는 적용 된 tooa 서브넷에는 Azure VM 또는 둘 다와 연결 된 가상 NIC 카드 될 수 있습니다. hello Nsg 필수 tooimplement hello 허브 및 스포크 hello 올바른 흐름 제어 됩니다. hello 수준의 hello NSG에서 제공 하는 보안에는 포트를 열면 및 용도 대 한 함수입니다. 고객은 IPtables 같은 호스트 기반 방화벽을 사용 하 여 추가 VM 필터를 적용 하거나 Windows 방화벽 hello 해야 합니다.
-   **DNS** hello 이름 확인 hello는 vdc Vnet의 리소스에 DNS를 통해 제공 됩니다. hello 기본 DNS 이름 확인의 hello 범위 제한 toohello VNet을 됩니다. 일반적으로 사용자 지정 DNS 서비스 toobe hello 허브에서 공통 서비스의 일부분으로 배포 하지만 DNS 서비스의 기본 소비자 hello hello 스포크에 상주 합니다. 필요한 경우 고객 DNS 영역 toohello 스포크의 위임 계층 DNS 구조를 만들 수 있습니다.
-   [**구독][SubMgmt] 및 [리소스 그룹 관리][RGMgmt]**. 구독은은 Azure에서 자연 경계 toocreate 여러 리소스 그룹을 정의 합니다. 구독의 리소스는 리소스 그룹이라는 논리적 컨테이너에 함께 통합됩니다. 리소스 그룹 hello vDC의 논리 그룹 tooorganize hello 리소스를 나타냅니다.
-   [**RBAC**][RBAC]. RBAC를 통해 권한 tooaccess 특정 Azure 리소스와 함께 작업의 특정 하위 toorestrict 사용자 tooonly 허용 가능한 toomap 조직 역할 것 합니다. RBAC 사용 hello 적절 한 역할 toousers, 그룹 및 hello 관련 범위 내에서 응용 프로그램을 할당 하 여 액세스를 부여할 수 있습니다. 역할 할당의 hello 범위는 Azure 구독, 리소스 그룹 또는 단일 리소스 될 수 있습니다. RBAC는 권한 상속을 허용합니다. 부모 범위에서 지정 된 역할이 부여 액세스 toohello 자식에 포함 합니다. RBAC를 사용 하 여 의무를 분리 수 있으며 필요 하다는 tooperform 업무 hello 양의 데이터만 액세스 toousers에 권한을 부여할 수도 있습니다. SQL Db hello 내에서 관리할 수 있습니다 다른 동안 사용 하 여 RBAC toolet 직원이 한 명 구독에서 가상 컴퓨터를 관리 하는 예를 들어 동일한 구독 합니다.
-   [**VNet 피어링**][VNetPeering]. hello 사용 되는 기본 기능 toocreate hello 인프라는 vdc는 VNet 피어 링을 두 개의 가상 네트워크 (Vnet) hello에 연결 하는 메커니즘 hello hello Azure 데이터 센터 네트워크를 통해 동일한 지역입니다.

#### <a name="component-type-perimeter-networks"></a>구성 요소 유형: 경계 네트워크
[경계 네트워크] [ DMZ] (DMZ 네트워크) 구성 요소는 온-프레미스 또는 인터넷 hello에서 모든 연결 tooand 함께 물리적 데이터 센터 네트워크와 tooprovide 네트워크 연결을 허용 합니다. 이 네트워크는 네트워크 및 보안 팀이 대부분의 시간을 보내는 위치이기도 합니다.

들어오는 패킷을 hello 스포크의 hello 백 엔드 서버에 도달 하기 전에 hello 방화벽, ID 및 ip 주소로 같은 hello 허브의 보안 어플라이언스에서 hello 통과 해야 합니다. 또한 hello 워크 로드에서 인터넷에 바인딩된 패킷을 해야 정책 적용, 검사 및 감사할 목적으로 hello 네트워크에서 없어지기 전에 hello 경계 네트워크에 hello 보안 어플라이언스를 통해 전달 됩니다.

경계 네트워크 구성 요소는 hello 같은 기능을 제공 합니다.

-   [가상 네트워크][VNet], [UDR][UDR], [NSG][NSG]
-   [네트워크 가상 어플라이언스][NVA]
-   [부하 분산 장치][ALB]
-   [Application Gateway][AppGW] / [WAF][WAF]
-   [공용 IP][PIP]

일반적으로 hello 중앙 IT 보안 팀에 대 한 책임 hello 경계 네트워크의 작업과 요구 사항 정의 하 고 있습니다.

[![7]][7]

hello 앞의 다이어그램을 보여 줍니다 hello 적용 액세스 toohello와 두 개의 경계 인터넷 및 온-프레미스 네트워크의 둘 다 hello 허브에 상주 합니다. 단일 허브에 hello 경계 네트워크 toointernet toosupport 수가 많은 웹 응용 프로그램 방화벽 (WAFs) 및/또는 방화벽의 여러 팜을 사용 하 여 Lob 확장할 수 있습니다.

[**가상 네트워크** ] [ VNet] hello 허브는 일반적으로 여러 서브넷 toohost hello 다른 종류의 서비스와 VNet 기반 필터링 및 검사에서 트래픽을 tooor hello NVAs, WAFs 통해 인터넷 와 Azure 응용 프로그램 게이트웨이 합니다.

[**UDR**][UDR] UDR을 사용하여 고객은 보안 경계 정책 적용, 감사 및 검사를 위해 방화벽, IDS/IPS 및 기타 가상 어플라이언스를 배포하고 이러한 보안 어플라이언스를 통해 네트워크 트래픽을 라우팅할 수 있습니다. UDRs 두 hello 허브 및 hello 스포크 tooguarantee 특정 사용자 지정 Vm, 네트워크 가상 어플라이언스 및 hello vDC에서 사용 하는 부하 분산 장치를 통해 트래픽을 transits hello 하에서 만들 수 있습니다. hello 스포크 전송 toohello 올바른 가상 어플라이언스에 Vm에서 생성 된 트래픽 하는 tooguarantee는 UDR 필요한 toobe hello 다음 홉으로 hello hello 내부 부하 분산 장치 프런트 엔드 IP 주소를 설정 하 여 hello 스포크의 hello 서브넷에서 설정 합니다. hello 내부 부하 분산 장치는 hello 내부 트래픽이 toohello 가상 어플라이언스 (부하 분산 장치 백 엔드 풀)를 배포합니다.

[![8]][8]

[**네트워크 가상 어플라이언스** ] [ NVA] hello 허브에서 경계 네트워크와 인터넷 방화벽 및/또는 웹 응용 프로그램 방화벽 (WAFs) 팜을 통해 정상적으로 관리 되는 액세스 toohello hello 합니다.

다른 Lob 일반적으로 사용 하 여 여러 웹 응용 프로그램 하며 이러한 응용 프로그램 toosuffer 다양 한 취약점을 악용 가능성이 있습니다. 웹 응용 프로그램 방화벽은 특별 한 유형의 제품 제네릭 방화벽 보다 좀 더 깊이에 웹 응용 프로그램 (HTTP/HTTPS)에 대 한 toodetect 공격을 사용 합니다. 방화벽 기술 기능에 비해 WAFs에는 위협 요소 로부터 특정 기능 tooprotect 내부 웹 서버.

방화벽 팜은 hello hello 스포크 및 제어 액세스 tooon 온-프레미스 네트워크에서 호스트 보안 규칙 tooprotect hello 작업 집합과 같은 일반적인 관리 아래에서 함께 작업 하는 방화벽의 그룹입니다. 방화벽 팜 toofilter 범위가 지정 되 고 모든 유형의 송신 및 수신 트래픽 검사 광범위 한 응용 프로그램을 되었지만 덜 특수화 된 소프트웨어는 WAF와 비교 합니다. 방화벽 팜 hello Azure marketplace에서에서 사용할 수 있는 네트워크 가상 어플라이언스 (NVAs)를 통해 Azure에서 일반적으로 구현 됩니다.

Hello, 인터넷에서 발생 하는 트래픽에 대 한 하나 toouse 집합이 NVAs 것이 좋습니다 및 트래픽 발생에 대 한 다른 온-프레미스입니다. 네트워크 트래픽의 hello 두 집합 간의 없는 보안 경계를 제공 하므로 보안상 위험을은 NVAs 집합이 하나만 사용 하 여 모두에 대 한 합니다. 별도 NVAs를 사용 하 여 보안 규칙을 확인 하 여 hello 복잡성을 toowhich 들어오는 네트워크 요청을 해당 하는 규칙을 명확히 보여 줍니다.

대부분의 대기업은 여러 개의 도메인을 관리하고 있습니다. Azure DNS 특정 도메인에 대 한 사용된 toohost hello DNS 레코드를 수 있습니다. 예제로 hello Azure 외부 부하 분산 장치 (또는 hello WAFs)의 가상 IP 주소 (VIP) hello Azure DNS 레코드의 hello A 레코드에 등록할 수 있습니다.

[**Azure Load Balancer**][ALB] Azure Load Balancer는 고가용성 계층 4(TCP, UDP) 서비스를 제공하여 들어오는 트래픽을 부하 분산 집합에 정의된 서비스 인스턴스 간에 분산할 수 있도록 합니다. 트래픽이 전송 주소 변환 tooa 집합 (예제; 되 고 백 엔드 IP 주소 풀의 유무 toohello 부하 분산 장치 프런트 엔드 끝점 (공용 IP 끝점 또는 개인 IP 끝점)에서 재배포할 수 있으며 네트워크 가상 어플라이언스 또는 Vm)입니다.

Azure 부하 분산 장치 hello의 hello 상태 뿐만 아니라 다양 한 서버 인스턴스 검색 수 하 고는 프로브 toorespond hello 부하 분산 장치 중지 트래픽 toohello 비정상 인스턴스 전송에 실패 한 경우. 에 vDC는 외부 부하 분산의 hello 존재 hello 허브 (예를 들어, 균형 hello 트래픽 tooNVAs), 및 hello 스포크 (다중 계층 응용 프로그램의 다른 Vm 간의 트래픽을 분산 하는 것과 같은 tooperform 작업)에 있습니다.

[**Application Gateway**][AppGW] Microsoft Azure Application Gateway는 전용 가상 어플라이언스이며 ADC(응용 프로그램 배달 컨트롤러)를 서비스로 제공하여 다양한 계층 7 부하 분산 기능을 제공합니다. 있습니다 toooptimize 웹 팜 생산성을 CPU 집약적인 SSL 종료 toohello 응용 프로그램 게이트웨이 오프 로드 합니다. 들어오는 트래픽을, 쿠키 기반 세션 선호도, URL 경로 기반 라우팅 및 hello 기능 toohost 라운드 로빈 배포를 포함 하는 다른 계층 7 라우팅 기능 단일 응용 프로그램 게이트웨이 뒤에 있는 여러 웹 사이트도 제공 합니다. 웹 응용 프로그램 방화벽 (WAF) hello 응용 프로그램 게이트웨이 WAF SKU의 일부로 제공 됩니다. 이 SKU에서는 일반적인 웹 취약점을 악용 tooweb 응용 프로그램을 보호 합니다. Application Gateway는 인터넷 연결 게이트웨이, 내부 전용 게이트웨이 또는 둘의 조합으로 구성할 수 있습니다. 

[**공용 Ip** ] [ PIP] 에서 액세스 하면 tooassociate 서비스 끝점 tooa 공용 IP 주소 리소스 toobe tooyour 수 있는 일부 Azure 기능 사용 hello 인터넷 합니다. 이 끝점이 hello Azure 가상 네트워크에 네트워크 주소 변환 (NAT) tooroute 트래픽 toohello 내부 주소와 포트를 사용합니다. 이 경로 hello 외부 트래픽이 toopass hello 가상 네트워크로에 대 한 기본 방법입니다. hello 공용 IP 주소 구성된 toodetermine 트래픽을 전달 될 수 있습니다 및 위치와 방법을 toohello 가상 네트워크에 변환 됩니다.

#### <a name="component-type-monitoring"></a>구성 요소 유형: 모니터링
모니터링 구성 요소 표시 유형 및 모든 경고 hello 다른 구성 요소 종류를 제공 합니다. 모든 팀 hello 구성 요소에 대 한 액세스 toomonitoring 있어야 하 고 액세스할 수 있는 서비스 키를 누릅니다. 중앙 집중식된 도움말 기술 지원팀 또는 운영 팀을 사용 하는 경우 이러한 구성 요소에서 제공 하는 통합 toohave 액세스 toohello 데이터 필요할 것입니다.

Azure는 서로 다른 유형의 Azure의 서비스 tootrack hello 동작을 모니터링 및 로깅 리소스를 호스트 합니다. 거 버 넌 스 및 Azure에서 작업의 제어 기반된 하지 있는 것이 아니라 수집 된 로그 데이터 뿐만 아니라 특정 보고 된 이벤트에 따라 hello 기능 tootrigger 동작 됩니다.

Azure에는 다음과 같은 2가지 주요 로그 유형이 있습니다.

-   [**활동 로그** ] [ ActLog] ("작업 로그"로 함) hello Azure 구독에서에서 리소스에서 수행 된 hello 작업에 대 한 정보를 제공 합니다. 이러한 로그는 구독에 대 한 hello 제어 평면 이벤트를 보고합니다. 모든 Azure 리소스는 감사 로그를 생성합니다.

-   [**Azure 진단 로그** ] [ DiagLog] 해당 리소스의 hello 작업에 대 한 데이터를 다양 하 고 자주 제공 하는 리소스에서 생성 한 로그 됩니다. 이러한 로그의 hello 콘텐츠 리소스 유형에 따라 달라 집니다.

[![9]][9]

VDC에서 매우 중요 tootrack hello Nsg 로그, 특히이 정보입니다.

-   [**이벤트 로그**][NSGLog]: NSG 규칙은 적용 된 tooVMs 및 MAC 주소에 따라 인스턴스 역할에 대해 설명 합니다.
-   [**카운터 로그**][NSGLog]: 각 NSG가 실행 된 toodeny 규칙 또는 트래픽을 허용 횟수를 추적 합니다.

모든 로그는 감사, 정적 분석 또는 백업 목적으로 Azure Storage 계정에 저장될 수 있습니다. 고객이 다른 종류를 사용할 수 hello 로그를 Azure 저장소 계정에 저장 되어 있는 경우 프레임 워크 tooretrieve의 준비, 분석 및이 데이터 tooreport hello 상태 및 클라우드 리소스의 상태를 시각화 합니다.

대규모 엔터프라이즈 해야 이미 얻었습니다 표준 프레임 워크에 대 한 모니터링 온-프레미스 시스템을 확장할 수 클라우드 배포는 프레임 워크 toointegrate 로그가 생성 합니다. Hello 클라우드 로그인 hello 모든 tookeep 하려는 조직을 위해 [Microsoft Operations Management Suite (OMS)] [ OMS] 이 최선의 선택 합니다. OMS는 클라우드 기반 서비스로 구현되므로 인프라 서비스에 대한 최소한의 투자로 빠르게 실행할 수 있습니다. OMS 통합할 수도 System Center Operations Manager tooextend 같은 System Center 구성 요소와 되어 기존 관리 투자 hello 클라우드로.

OMS 로그 분석은 OMS 프레임 워크 toohelp hello의 구성 요소를 수집, 상관관계를 설정한 후, 검색 및 act 로그 및 성능 데이터에 의해 생성 된 운영 체제, 응용 프로그램, 클라우드 인프라 구성 요소입니다. 고객 실시간 작업 통찰력 vDC에서 모든 작업에서 통합 된 검색 및 사용자 지정 대시보드 tooanalyze 모든 hello 레코드를 사용 합니다.

#### <a name="component-type-workloads"></a>구성 요소 유형: 워크로드
워크로드 구성 요소는 실제 응용 프로그램 및 서비스가 있는 위치입니다. 응용 프로그램 개발 팀이 대부분의 시간을 보내는 위치이기도 합니다.

hello 작업 속성은 실제로 무한 있습니다. hello 다음은 몇 가지 hello 가능한 작업 형식입니다.

**내부 LOB 응용 프로그램**

기간 업무 응용 프로그램은 엔터프라이즈의 컴퓨터 응용 프로그램 중요 toohello 진행 중인 작업입니다. LOB 응용 프로그램은 다음과 같은 몇 가지 공통된 특성을 갖습니다.

-   **대화형**. LOB 응용 프로그램은 기본적으로 대화형입니다. 데이터가 입력되고 결과/보고서가 반환됩니다.
-   **데이터 기반**. LOB 응용 프로그램은 자주 액세스 toohello 데이터베이스 또는 기타 저장소를 많이 사용 되는 데이터입니다.
-   **통합형**. 내에서 또는 hello 조직 외부의 다른 시스템으로 응용 프로그램 제공 통합을 LOB입니다.

**고객 웹 사이트 (인터넷 또는 내부 연결) 관련** hello 인터넷 상호 작용 하는 대부분의 응용 프로그램은 웹 사이트입니다. Azure에서는 hello 기능 toorun IaaS VM에서 또는 웹 사이트는 [Azure 웹 앱] [ WebApps] 사이트 (PaaS). Azure 웹 앱 hello는 vdc hello 스포크에 hello 웹 응용 프로그램 배포를 허용 하는 Vnet와의 통합을 지원 합니다. VNET 통합 hello로 응용 프로그램에 대 한 인터넷 끝점 tooexpose 필요 하지는 않지만 개인 VNet에서 hello 리소스 개인-인터넷 라우팅 가능한 주소 대신 사용할 수 있습니다.

**빅 데이터/분석** 데이터 tooscale tooa 매우 큰 볼륨을 구성 하면 데이터베이스 수 비율이 제대로 조정 되지 합니다. Hadoop 기술은 시스템에서 많은 수의 노드가 병렬로 toorun 분산 쿼리를 제공합니다. 고객에 게 IaaS Vm 또는 PaaS hello 옵션 toorun 데이터 작업 ([HDInsight][HDI]). HDInsight 위치 기반 VNet에 배포를 지원, hello vdc 스포크에 배포 된 tooa 클러스터가 될 수 있습니다.

**이벤트 및 메시징**
[Azure Event Hubs][EventHubs]는 수백만 개의 이벤트를 수집, 변환 및 저장하는 하이퍼스케일(hyper-scale) 원격 분석 수집 서비스입니다. 분산된 스트리밍 플랫폼으로 서 낮은 대기 시간 및 Azure에 tooingest 엄청난 양의 원격 분석을 사용 하는 구성 가능한 시간 보존을 제공 하 고 여러 응용 프로그램에서 해당 데이터를 읽습니다. Event Hubs를 통해 단일 스트림은 실시간 및 일괄 처리 기반 파이프라인을 모두 지원할 수 있습니다.

응용 프로그램 및 서비스 사이의 매우 안정적인 클라우드 메시징 서비스는 구조화된 FIFO(선입 선출) 메시징 및 게시/구독 기능과 함께, 클라이언트와 서버 간에 조정된 비동기식 메시징을 제공하는 [Azure Service Bus][ServiceBus]를 통해 구현될 수 있습니다.

[![10]][10]

### <a name="multiple-vdc"></a>여러 vDC
지금까지이 문서는 hello 기본 구성 요소 및 tooa 탄력적인 vDC 영향을 주는 아키텍처를 설명 하는 단일 vDC에 데 사용 됩니다. Azure 부하 분산 장치를 NVAs, 가용성 집합을 다른 메커니즘과 함께 크기 집합 등의 azure 기능 tooa 시스템 할 수 있도록 toobuild 단색 SLA 수준을 프로덕션 서비스에 영향을 줍니다.

그러나 단일 vDC 단일 지역 내에서 호스트 되 고 해당 전체 지역에 영향을 줄 수 취약 toomajor 가동이 중지. 원하는 tooachieve 고객 높은 Sla hello 두 (이상) 개의 Vdc, 서로 다른 지역에 배치에서 동일한 프로젝트의 배포를 통해 tooprotect hello 서비스를 해야 합니다.

또한 tooSLA 우려 사항에서 몇 가지 일반적인 시나리오를 배포 하는 여러 개의 Vdc 의미가 있습니다.

-   지역/글로벌 서비스
-   재해 복구
-   DC 간 toodivert 트래픽이 메커니즘

#### <a name="regionalglobal-presence"></a>지역/글로벌 서비스
Azure 데이터 센터는 전 세계 여러 지역에 있습니다. 고객이 원하는 두 개의 관련된 요인 tooconsider 여러 Azure 데이터 센터를 선택할 때는: 지리적으로 떨어져 및 대기 시간입니다. 고객은 tooevaluate hello 지리적 hello 개의 Vdc와 거리 hello와 거리를 hello vDC toooffer hello 최상의 사용자 환경 hello 최종 사용자가 해야합니다.

hello 개의 Vdc 호스팅되는 Azure 지역 tooconform 조직 운영 중인 모든 행정이 설정한 규정 요구 사항이 있어야 합니다.

#### <a name="disaster-recovery"></a>재해 복구
재해 복구 계획의 hello 구현 관련 된 문제는 워크 로드의 관련성이 toohello 형식이 며 여러 개의 Vdc 간의 hello 기능 toosynchronize hello 작업 상태입니다. 이상적으로 대부분의 고객이 원하는 두 개의 서로 다른 Vdc tooimplement 빠른 장애 조치 메커니즘에서 실행 되는 배포 간에 toosynchronize 응용 프로그램 데이터입니다. 대부분의 응용 프로그램에서 중요 한 toolatency 되며 데이터 동기화에 잠재적 시간 제한 및 지연 될 수 있습니다.

여러 다른 vDC에 있는 응용 프로그램의 동기화 또는 하트비트 모니터링을 위해서는 이러한 vDC 간에 통신이 설정되어야 합니다. 다른 지역에 있는 두 vDC는 다음을 통해 연결될 수 있습니다.

-   ExpressRoute 개인 피어 링 hello vDC 허브는 연결 된 toohello 때 동일한 ExpressRoute 회로
-   연결 된 toohello ExpressRoute 회로 사용자 회사 backbone 및 vDC 메시를 통해 연결 된 여러 개의 ExpressRoute 회로
-   각 Azure 지역에 있는 vDC 허브 간의 사이트 간 VPN 연결

일반적으로 hello ExpressRoute 연결은 Microsoft backbone hello를 통해 전송 하는 경우 더 높은 대역폭 및 일관 된 대기 시간 때문 hello 기본 메커니즘입니다.

두 개 이상이 다른 개의 Vdc 다른 지역에 사이 분산 응용 프로그램은 매직 레시피 toovalidate 없습니다. 동기 또는 비동기 데이터 복제에 적합 한지 여부와 어떤 hello 최적의 복구 시간 목표 (RTO)에 사용할 수 있습니다 고객 네트워크 자격 테스트 tooverify hello 대기 시간 및 hello 연결 및 대상의 대역폭을 실행 해야 프로그램 워크 로드 합니다.

#### <a name="mechanism-toodivert-traffic-between-dc"></a>DC 간 toodivert 트래픽이 메커니즘
한 가지 효과적인 기법은 hello 트래픽 toodivert 템플릿 DC tooanother 하나에 들어오는 DNS를 기반으로 합니다. [Azure 트래픽 관리자] [ TM] 사용 하 여 DNS 도메인 이름 () 메커니즘 toodirect hello 최종 사용자 트래픽 toohello 가장 적합 한 공용 끝점에 특정 vDC hello 합니다. 프로브를 통해 여러 개의 Vdc에 공용 끝점의 hello 서비스 상태를 정기적으로 검사 하는 트래픽 관리자 및 해당 끝점의 오류를 발생 시 라우팅합니다 자동으로 보조 vDC toohello 합니다.

트래픽 관리자는 Azure 공용 끝점에서 작동 하 고 사용할 수 있습니다, 그리고 예를 들어 toocontrol/비가상 전환 트래픽 tooAzure Vm 및 웹 앱에 hello vDC 적절 합니다. 트래픽 관리자는 전체 Azure 지역 실패의 hello 면에도 복원 력이 하 고 기준에 따라 여러 개의 Vdc의 서비스 끝점에 대 한 사용자 트래픽의 hello 배포를 제어할 수 있습니다 (특정 vDC에 서비스의 예를 들어, 오류를 선택 하거나 hello vDC hello 가장 낮은 hello 클라이언트에 대 한 네트워크 대기 시간으로).

### <a name="conclusion"></a>결론
hello 가상 데이터 센터는 Azure에서 클라우드 리소스 사용을 최대화 하는 비용을 절감 하 고 시스템을 단순화 하는 확장 가능한 아키텍처 toocreate 기능 및 특성의 조합을 사용 하는 hello 클라우드로 접근 방식을 toodata 센터 마이그레이션 거 버 넌 스 합니다. hello vDC 개념 hello 허브에서 공통 공유 서비스를 제공 하 고 hello 스포크에서 특정 응용 프로그램/작업을 허용 하는 허브-스포크 토폴로지를 기반으로 합니다. VDC 회사 역할을 여기서 (중앙 IT, DevOps, 작업 및 유지 관리) 다른 부서 함께 작동 하는 역할 및 책임의 특정 목록을 사용 하 여 각각의 hello 구조와 일치 합니다. VDC "리프트 및 Shift" 마이그레이션에 대 한 hello 요구 사항을 충족 하지만 다양 한 이점을 toonative 클라우드 배포 제공 합니다.

## <a name="references"></a>참조
같은 기능 hello이이 문서에 설명 되어 있습니다. 더 많은 hello 링크 toolearn를 클릭 합니다.

| | | |
|-|-|-|
|네트워크 기능|부하 분산|연결|
|[Azure Virtual Networks][VNet]</br>[네트워크 보안 그룹][NSG]</br>[NSG 로그][NSGLog]</br>[사용자 정의 라우팅][UDR].</br>[네트워크 가상 어플라이언스][NVA]</br>[공용 IP 주소][PIP]|[Azure Load Balancer(L3)][ALB]</br>[Application Gateway(L7)][AppGW]</br>[웹 응용 프로그램 방화벽][WAF]</br>[Azure Traffic Manager][TM] |[VNet 피어링][VNetPeering]</br>[가상 사설망][VPN]</br>[ExpressRoute][ExR]
|ID</br>|모니터링</br>|모범 사례</br>|
|[Azure Active Directory][AAD]</br>[Multi-Factor Authentication][MFA]</br>[역할 기반 액세스 제어][RBAC]</br>[기본 AAD 역할][Roles] |[활동 로그][ActLog]</br>[진단 로그][DiagLog]</br>[Microsoft Operations Management Suite][OMS]</br> |[경계 네트워크 모범 사례][DMZ]</br>[구독 관리][SubMgmt]</br>[리소스 그룹 관리][RGMgmt]</br>[Azure 구독 제한][Limits] |
|기타 Azure 서비스|
|[Azure Web Apps][WebApps]</br>[HDInsights(Hadoop)][HDI]</br>[Event Hubs][EventHubs]</br>[Service Bus][ServiceBus]|



## <a name="next-steps"></a>다음 단계
 - 탐색 [VNet 피어 링][VNetPeering], vDC 허브에 대 한 기본 기술 hello 및 스포크 디자인
 - 구현 [AAD] [ AAD] tooget 시작 [RBAC] [ RBAC] 탐색
 - 구독 및 리소스 관리 모델을 개발 하 고 RBAC toomeet hello 구조, 요구 사항, 모델 및 해당 조직의 정책을 합니다. hello 가장 중요 한 작업은 계획 하 고 있습니다. 재구성, 합병, 신제품 라인 등에 대한 실제 계획도 중요합니다.

<!--Image References-->
[0]: ./media/networking-virtual-datacenter/redundant-equipment.png "구성 요소 중복 예제" 
[1]: ./media/networking-virtual-datacenter/vdc-high-level.png "고급 수준의 허브 및 스포크 vDC 예제"
[2]: ./media/networking-virtual-datacenter/hub-spokes-cluster.png "허브 및 스포크 클러스터"
[3]: ./media/networking-virtual-datacenter/spoke-to-spoke.png "스포크-스포크"
[4]: ./media/networking-virtual-datacenter/vdc-block-level-diagram.png "Hello vDC의 블록 수준 다이어그램"
[5]: ./media/networking-virtual-datacenter/users-groups-subsciptions.png "사용자, 그룹, 구독 및 프로젝트"
[6]: ./media/networking-virtual-datacenter/infrastructure-high-level.png "고급 수준의 인프라 다이어그램"
[7]: ./media/networking-virtual-datacenter/highlevel-perimeter-networks.png "고급 수준의 인프라 다이어그램"
[8]: ./media/networking-virtual-datacenter/vnet-peering-perimeter-neworks.png "VNet 피어링 및 경계 네트워크"
[9]: ./media/networking-virtual-datacenter/high-level-diagram-monitoring.png "모니터링에 대한 높은 수준의 다이어그램"
[10]: ./media/networking-virtual-datacenter/high-level-workloads.png "워크로드에 대한 높은 수준의 다이어그램"

<!--Link References-->
[Limits]: https://docs.microsoft.com/azure/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles
[VNet]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[NSG]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg 
[VNetPeering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview 
[UDR]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview 
[RBAC]: https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is
[MFA]: https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication
[AAD]: https://docs.microsoft.com/azure/active-directory/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways 
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction 
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[SubMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-subscription-governance 
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[DMZ]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/resource-groups-networking#public-ip-address
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[WAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
[ActLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs 
[DiagLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[NSGLog]: https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview
[WebApps]: https://docs.microsoft.com/azure/app-service-web/
[HDI]: https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs 
[ServiceBus]: https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview
[TM]: https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview
