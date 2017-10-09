---
title: "aaaInfrastructure 및 연결 tooSAP Azure (대형 인스턴스)에서 HANA | Microsoft Docs"
description: "Azure (대형 인스턴스)에서 연결이 필요한 인프라 toouse SAP HANA를 구성 합니다."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0af34fbd82413bf63981036a76eaa264d8299ec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-infrastructure-and-connectivity-on-azure"></a>Azure(큰 인스턴스)의 SAP HANA 인프라 및 연결 

이 가이드를 읽기에 앞서 일부 사전 정의. [SAP HANA (큰 인스턴스) 개요 및 Azure 상의 아키텍처](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)에서 HANA 큰 인스턴스 단위의 두 다른 클래스를 도입했습니다.

- S72, S72m, S144, S144m, S192, 및 S192m tooas hello '클래스 I t y'는 Sku입니다.
- S384, S384m, S384xm, S576, S768, 및은 기관 S960 tooas hello Sku의 ' Type II 클래스'.

hello 클래스 지정자는 진행 중인 toobe hello toodifferent 기능 및 HANA 큰 인스턴스 Sku를 기준으로 요구 사항 설명서 tooeventually 참조 HANA 큰 인스턴스 전체에서 사용 됩니다.

우리가 자주 사용하는 다른 정의는 다음과 같습니다.
- **대형 인스턴스 스탬프:** SAP HANA TDI 하드웨어 인프라 스택이 인증 하며 Azure 내에서 SAP HANA 인스턴스 toorun 전용입니다.
- **(대형 인스턴스) Azure에서 SAP HANA:** 에 인증 된 하드웨어에 큰 인스턴스 스탬프 서로 다른 Azure 지역에 배포 된 SAP HANA TDI의 Azure toorun HANA 인스턴스에 hello 제안에 대 한 공식 이름입니다. hello 관련 용어 **HANA 큰 인스턴스** (대형 인스턴스) Azure에서 SAP HANA 짧은 이며 널리이 기술 배포 가이드를 사용 합니다.
 

(대형 인스턴스) Azure에서 SAP HANA의 hello 구매, 사용자와 Microsoft 엔터프라이즈 계정 팀 hello 간에 종료한 후 hello 다음 정보에 필요한 Microsoft toodeploy HANA 큰 인스턴스 단위:

- 고객 이름
- 비즈니스 연락처 정보(전자 메일 주소 및 전화 번호 포함)
- 기술 담당자 정보(전자 메일 주소 및 전화 번호 포함)
- 기술 네트워킹 담당자 정보(전자 메일 주소 및 전화 번호 포함)
- Azure 배포 지역 (7월 현재 미국 서부, 미국 동부, 오스트레일리아 동부, 오스트레일리아 남동부, 유럽 서부 및 북유럽 
- 2017)
- Azure(큰 인스턴스) SKU(구성)에서 SAP HANA 확인
- 이미에 자세히 설명 hello 개요 및 아키텍처 문서 HANA 큰 인스턴스에 대 한 모든 Azure 지역에 배포 되 고:
    - / 29 Azure Vnet tooHANA 큰 인스턴스를 연결 하는 ER P2P 연결에 대 한 IP 주소 범위
    - Hello HANA 큰 인스턴스 서버 IP 풀에 사용 되 는/24 CIDR 블록
- toohello HANA 큰 인스턴스를 연결 하는 모든 Azure VNet의 hello VNet 주소 공간 특성에 사용 하는 hello IP 주소 범위 값
- HANA 큰 인스턴스 시스템 각각에 대한 데이터:
  - 원하는 호스트 이름 - 정규화된 도메인 이름이 이상적.
  - 서버 IP 풀 주소 범위-hello 부족 hello HANA 큰 인스턴스 단위에 대 한 원하는 IP 주소 염두에서에 둬야 해당 hello hello 서버 IP 풀 주소 범위는 HANA 큰 인스턴스 내에서 내부 사용을 위해 예약 되어 있는 처음 30 IP 주소
  - Hello SAP HANA 인스턴스 (필수 toocreate hello 필요한 SAP HANA 관련 디스크 볼륨)에 대 한 SAP HANA SID 이름입니다. hello HANA SID는에 대 한 hello 권한을 만드는 데 필요한 <sidadm> hello NFS 볼륨에 연결 된 toohello HANA 큰 인스턴스 단위 가져오는지입니다. 또한로 사용 hello 디스크 볼륨을 탑재 가져오기 hello 이름 구성 요소 중 하나입니다. Hello 단위에 둘 이상의 HANA 인스턴스가 toorun을 원하는 경우 toolist 여러 HANA Sid 필요. 각각에 별도의 볼륨 집합이 할당됩니다.
  - hello groupid hello hana sidadm 사용자에 게 hello Linux OS에에서는 필요한 toocreate hello 필요한 SAP HANA 관련 디스크 볼륨입니다. hello SAP HANA 설치는 일반적으로 그룹 id가 1001 인 hello sapsys 그룹을 만듭니다. hello hana sidadm 사용자는 해당 그룹의 구성원이
  - hello userid hello hana sidadm 사용자에 게 hello Linux OS에에서는 필요한 toocreate hello 필요한 SAP HANA 관련 디스크 볼륨입니다. 모든 hello toolist hello 단위에서 여러 HANA 인스턴스를 실행 하는 경우 해야 <sid>adm 사용자 
- Hello Azure 구독 toowhich HANA 큰 인스턴스 Azure에서 SAP HANA에 대 한 azure 구독 ID toobe 직접 연결 하려고 합니다. 이 구독 ID는 hello toobe HANA 큰 인스턴스 장치 hello로 청구 될 수 있는 Azure 구독을 참조 합니다.

사용자가 제공한 정보를 Microsoft 프로 비전 (대형 인스턴스) Azure에서 SAP HANA hello 및 hello 정보 필요한 toolink 프로그램 Azure Vnet tooHANA 큰 인스턴스 및 tooaccess hello HANA 인스턴스가 큰 단위를 반환 합니다.

## <a name="connecting-azure-vms-toohana-large-instances"></a>Azure Vm tooHANA 큰 인스턴스 연결

이미 설명한 것 처럼에서 [개요 SAP HANA (대형 인스턴스) 및 Azure에서 아키텍처](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) Azure 검색의 hello SAP 응용 프로그램 계층 HANA 큰 인스턴스 hello 최소한의 배포와 같은:

![Azure VNet tooSAP HANA (대형 인스턴스)를 Azure와 온-프레미스에 연결](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

Azure VNet 쪽 hello에 더 가깝기 때문에 찾는 이라는 사실을 인식 hello 필요:

- 진행 중인 사용 toobe toodeploy hello SAP 응용 프로그램 계층으로의 hello Vm이 Azure VNet의 hello 정의입니다.
- 자동으로 즉 실제로 hello 하나 사용 하는 toodeploy hello Vm에는 Azure Vnet에서 정의 된 hello에서 기본 서브넷 됩니다.
- 만든 Azure VNet hello toohave 필요한 하나 이상의 VM 서브넷 및 한 express 경로 게이트웨이 서브넷입니다. 이러한 서브넷은 hello IP 주소 범위 지정 및 hello 다음 섹션에에서 설명 된 것으로 지정 되어야 합니다.

따라서 살펴보겠습니다 약간 더 가깝기 때문 hello HANA 큰 인스턴스를 만들 Azure VNet에

### <a name="creating-hello-azure-vnet-for-hana-large-instances"></a>Azure VNet hello HANA 큰 인스턴스 만들기

>[!Note]
>hello Azure 리소스 관리자 배포 모델을 사용 하 여 hello HANA 큰 인스턴스에 대 한 Azure VNet을 만들어야 합니다. hello 이전 Azure 배포 모델을 일반적으로 클래식 배포 모델 이라고 HANA 큰 인스턴스 솔루션 hello로 지원 되지 않습니다.

hello VNet 만들어질 hello Azure 포털, PowerShell, Azure 서식 파일 또는 Azure CLI를 사용 하 여 (참조 [hello Azure 포털을 사용 하 여 가상 네트워크 만들기](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). 다음 예제는 hello에서 hello Azure 포털을 통해 만들지는 VNet 안으로 찾습니다.

Hello Azure 포털을 통해 Azure VNet의 hello 정의로 보면 살펴보겠습니다 hello 정의 및 toowhat 해당 관계의 일부에에서는 서로 다른 IP 주소 범위 목록입니다. Hello에 대 한 논의 하 고 대로 **주소 공간**, 의미는 hello Azure VNet 주소 공간을 hello toouse ï ´ ù. 이 주소 공간 BGP 경로 전파에 대 한 사용 하 여 VNet hello hello 주소 범위 이기도 합니다. 이 **주소 공간**은 여기에서 볼 수 있습니다.

![Azure 포털 hello에 표시 된 Azure VNet의 주소 공간](./media/hana-overview-connectivity/image1-azure-vnet-address-space.png)

앞, 10.16.0.0/16, hello 경우에서 hello Azure VNet을 보다 크고 넓은 IP 주소 범위 toouse를 제공 되었습니다. 이 VNet 내의 후속 서브넷의 모든 IP 주소 범위 hello ' 주소 공간이 ' 내에서 해당 범위를 가질 수 있다는 합니다. 일반적으로는 Azure에서 단일 VNet에 대해서는 이러한 큰 주소 범위를 권장하지 않습니다. 하지만 한 단계 더 나아가, 가져올 hello Azure VNet에에서 정의 된 hello 서브넷에 살펴보겠습니다.

![Azure VNet 서브넷 및 해당 IP 주소 범위](./media/hana-overview-connectivity/image2b-vnet-subnets.png)

알다시피 VNet은 첫 번째 VM 서브넷(여기서는 'default'라고 함)과 'GatewaySubnet'이라는 서브넷을 포함합니다.
'Default' hello 그래픽으로 호출 된 hello 서브넷의 IP 주소 범위 toohello 언급할 hello 섹션 뒤, **Azure VM 서브넷 IP 주소 범위**합니다. 다음 섹션 hello, hello 게이트웨이 서브넷의 IP 주소 범위 toohello 참조로 **VNet 게이트웨이 서브넷 IP 주소 범위**합니다. 

위의 두 hello 그래픽에서 보여 주는 hello 경우 해당 hello 표시 **VNet 주소 공간** 에서는 둘 다 hello **Azure VM 서브넷 IP 주소 범위** 및 hello **VNet 게이트웨이 서브넷 IP 주소 범위**합니다. 

Tooconserve 필요 하거나 IP 주소 범위와 특정 수 있는 경우에 따라 hello를 제한할 수 있습니다 **VNet 주소 공간** 각 서브넷에서 사용 하 고 VNet toohello 특정 범위입니다. 이 경우 hello를 정의할 수 있습니다 **VNet 주소 공간** VNet의 여러 특정 범위는 다음과 같이 합니다.

![두 공간이 있는 Azure VNet 주소 공간](./media/hana-overview-connectivity/image3-azure-vnet-address-space_alternate.png)

이 경우 hello **VNet 주소 공간** 정의 하는 두 개의 공백을 포함 합니다. 이러한 두 가지 공간 동일한 toohello IP 주소 범위에 대해 정의 **Azure VM 서브넷 IP 주소 범위** 및 hello **VNet 게이트웨이 서브넷 IP 주소 범위입니다.**

이러한 테넌트 서브넷(VM 서브넷)에 원하는 모든 명명 표준을 사용할 수 있습니다. 그러나 **항상 지정 되어 있어야 각 VNet에 대 한 게이트웨이 서브넷만 하나의** toohello SAP HANA (대형 인스턴스) Azure express 경로 회로에 연결 하 합니다. 및 **이 게이트웨이 서브넷 "GatewaySubnet" 이름은 항상** hello express 경로 게이트웨이 tooensure 제대로 배치 합니다.

> [!WARNING] 
> Hello 게이트웨이 서브넷은 이름은 항상 "GatewaySubnet"는

연속되지 않은 주소 범위를 활용하더라도 여러 VM 서브넷을 사용할 수 있습니다. 이러한 주소 범위 hello 적용 해야 듯이 **VNet 주소 공간** hello VNet의 hello 목록이 나 집계 된 형식에 hello VM 서브넷 범위의 및 게이트웨이 서브넷 hello 합니다.

Hello 명심할 사실은 tooHANA 큰 인스턴스를 연결 하는 Azure VNet에 대 한 요약:

- Toosubmit tooMicrosoft hello 필요한 **VNet 주소 공간** HANA 큰 인스턴스의 초기 배포를 수행 하는 경우. 
- hello **VNet 주소 공간** Azure VM 서브넷 IP 주소 범위도 및 hello VNet 게이트웨이 서브넷 IP 주소 범위에 대 한 hello 범위를 포함 하는 하나의 큰 범위의 될 수 있습니다.
- 으로 전송 하는 경우 또는 **VNet 주소 공간** 여러 범위를 다루는 hello 다른 IP 주소 범위 VM 서브넷 IP 주소 범위도 및 hello VNet 게이트웨이 서브넷 IP 주소 범위입니다.
- 정의 된 hello **VNet 주소 공간** 사용 되는 BGP 라우팅 전파 됩니다.
- hello 게이트웨이 서브넷의 hello 이름 이어야 합니다: **"GatewaySubnet."**
- hello **VNet 주소 공간** HANA 큰 인스턴스 쪽 tooallow hello에 대 한 필터로 사용 하거나 Azure에서 트래픽이 toohello HANA 인스턴스가 큰 단위를 허용 하지 않습니다. Hello hello Azure VNet의 BGP 라우팅 정보 및 HANA 큰 인스턴스 쪽 hello에 대 한 필터링을 구성 하는 hello IP 주소 범위 일치 하지 않는 경우 연결에 문제가 발생할 수 있습니다.
- hello 게이트웨이 서브넷에 대 한 일부 세부 설명 아래 'VNet tooHANA 큰 인스턴스 ExpressRoute 연결' 섹션에는



### <a name="different-ip-address-ranges-toobe-defined"></a>다른 IP 주소 범위를 정의 하는 toobe 

이미 일부 hello IP 주소 범위 필요한 toodeploy HANA 큰 인스턴스 이전 섹션에서 도입 되었습니다. 하지만 중요한 IP 주소 범위가 몇 가지 더 있습니다. 이 내용에 대해 자세히 알아보겠습니다. hello toobe 필요한 일부는 다음과 같은 IP 주소 전송 tooMicrosoft toobe 초기 배포에 대 한 요청을 보내기 전에 정의 해야 합니다.

- **VNet 주소 공간:** 이미 이전 버전에 도입 된, 또는는 hello IP 주소 범위 할당 (또는 tooassign 계획) tooyour 주소 공간 매개 변수 hello Azure 가상 네트워크 (VNet)에 SAP HANA 큰 인스턴스 toohello 연결 환경입니다. Azure VM 서브넷 범위도 hello 및 hello Azure 게이트웨이 서브넷 범위 이전 hello 그래픽에 표시 된 대로 구성 된 다중 선 값이 주소 공간 매개 변수는 것이 좋습니다. 이 범위는 온-프레미스, 서버 IP 풀 또는 ER-P2P 주소 범위와 겹치면 안 됩니다. 어떻게 tooget이 또는 이러한 IP 주소 범위도? 회사 네트워크 팀 또는 서비스 공급자는 네트워크 내에서 사용되지 않는 하나 이상의 IP 주소 범위를 제공해야 합니다. 예: Azure VM 서브넷 (이전 참조), 10.0.1.0/24 이며 Azure 게이트웨이 서브넷 (다음 참조) 10.0.2.0/28, 다음 Azure VNet 주소 공간 좋습니다 toobe 두 줄; 10.0.1.0/24 및 10.0.2.0/28 합니다. 있지만 hello 주소 공간 값을 집계할 수, 좋습니다 toohello 서브넷 범위를 일치 tooavoid 실수로 인 한 다시 사용할 수 있도록 사용 되지 않는 ip 주소 범위 hello 향후에 더 큰 주소 공간 내에서 다른 위치에서 네트워크의 합니다. **VNET 주소 공간 hello는 초기 배포를 요청 하는 경우 어떤 요구 toobe tooMicrosoft를 전송 하는 IP 주소 범위**

- **Azure VM 서브넷 IP 주소 범위:** 이미 앞서 설명 했 듯이 IP 주소 범위는 hello 하나 할당 된 사용자 (또는 tooassign 계획) toohello SAP HANA 큰 인스턴스 환경 연결 Azure VNET에서 Azure VNet 서브넷 매개 변수가 toohello . 이 IP 주소 범위는 tooassign 사용 되는 IP 주소 tooyour Azure Vm입니다. 이 범위를 벗어났습니다. hello IP 주소는 SAP HANA 큰 인스턴스 서버 tooconnect tooyour는 허용 합니다. 필요한 경우 여러 Azure VM 서브넷을 사용할 수 있습니다. 각 Azure VM 서브넷에 대해 /24 CIDR 블록을 사용하는 것이 좋습니다. 이 주소 범위에는 hello Azure VNet 주소 공간에에서 사용 된 hello 값의 일부 여야 합니다. 어떻게 tooget이 IP 주소 범위? 회사 네트워크 팀 또는 서비스 공급자는 네트워크 내에서 현재 사용되지 않는 IP 주소 범위를 제공해야 합니다.

- **VNet 게이트웨이 서브넷 IP 주소 범위:** 계획 기능 toouse, hello hello에 따라 크기는 것을 권장 합니다.
   - Ultra-performance ExpressRoute 게이트웨이: /26 주소 블록 - SKU의 Type II 클래스에 필요함
   - High-performance ExpressRoute 게이트웨이(이하)를 사용하고 VPN 및 ExpressRoute의 동시 존재: /27 주소 블록
   - 기타 모든 상황: /28 주소 블록. 이 주소 범위에는 hello "VNet 주소 공간" 값에 사용 된 hello 값의 일부 여야 합니다. 이 주소 범위에는 toosubmit tooMicrosoft 해야 하는 hello Azure VNet 주소 공간 값에 사용 된 hello 값의 일부 여야 합니다. 어떻게 tooget이 IP 주소 범위? 회사 네트워크 팀 또는 서비스 공급자는 네트워크 내에서 현재 사용되지 않는 IP 주소 범위를 제공해야 합니다. 

- **주소 ER P2P 연결에 대 한 범위:** 이 범위는 SAP HANA 큰 인스턴스 express 경로 (ER) P2P 연결에 대 한 hello IP 범위. 이 IP 주소 범위는 /29 CIDR IP 주소 범위여야 합니다. 이 범위는 온-프레미스 또는 기타 Azure IP 주소 범위와 겹치면 안 됩니다. 이 IP 주소 범위는 Azure VNet express 경로 게이트웨이 toohello SAP HANA 큰 인스턴스 서버 로부터 hello ER 연결을 사용 하는 tooset 합니다. 어떻게 tooget이 IP 주소 범위? 회사 네트워크 팀 또는 서비스 공급자는 네트워크 내에서 현재 사용되지 않는 IP 주소 범위를 제공해야 합니다. **이 범위는 초기 배포를 요청 하는 경우 어떤 요구 toobe tooMicrosoft를 전송 하는 IP 주소 범위**
  
- **서버 IP 풀 주소 범위:** 이 IP 주소 범위는 사용 되는 tooassign hello 개별 IP 주소 tooHANA 큰 인스턴스 서버입니다. hello 권장 서브넷 크기는 / 24 CIDR 블록-이지만 필요한는 것이 더 작은 tooa 최소 64 IP 주소를 제공 하는 중입니다. 이 범위에서 hello 처음 30 IP 주소는 예약 되어 사용 하기 위해 Microsoft에서 합니다. 이 팩트 차지 하기 위해 hello hello 범위 크기를 선택할 때 확인 합니다. 이 범위는 온-프레미스 또는 기타 Azure IP 주소와 겹치면 안 됩니다. 어떻게 tooget이 IP 주소 범위? 회사 네트워크 팀 또는 서비스 공급자는 네트워크 내에서 현재 사용되지 않는 IP 주소 범위를 제공해야 합니다. / 24 (대형 인스턴스) Azure에서 SAP HANA에 대해 필요한 hello 특정 IP 주소를 할당 하는 데 사용 되는 toobe 차단 고유 CIDR (권장). **이 범위는 초기 배포를 요청 하는 경우 어떤 요구 toobe tooMicrosoft를 전송 하는 IP 주소 범위**
 
Toodefine 필요 하 고 위의 hello IP 주소 범위 계획에 일부 전송 toobe tooMicrosoft 필요 합니다. toosummarize hello 위의 필수 tooname tooMicrosoft는 hello IP 주소 범위는.

- Azure VNet 주소 공간
- ER-P2P 연결에 대한 주소 범위
- 서버 IP 풀 주소 범위

Tooconnect tooHANA 큰 인스턴스를 필요로 하는 추가 Vnet을 추가 하려면 해야 toosubmit hello tooMicrosoft를 추가 하는 새 Azure VNet 주소 공간입니다. 

다음은 서로 다른 범위 hello 및 몇 가지 예제 범위 예 tooconfigure 필요 하 고 결국 tooMicrosoft를 제공 합니다. 볼 수 있듯이 hello Azure VNet 주소 공간에 대 한 hello 값 hello 첫 번째 예제에서는 집계 되지 않습니다 되지만 hello 범위 hello 첫 번째 Azure VM 서브넷 IP 주소 범위와 hello VNet 게이트웨이 서브넷 IP 주소 범위에서에서 정의 됩니다. 주소 범위 hello Azure VNet 주소 공간의 일부로 추가 VM 서브넷을 hello는 작업에 따라 구성 하 고 제출 하 여 hello IP hello Azure VNet 내에서 여러 VM 서브넷을 사용 하 합니다.

![Azure(큰 인스턴스)에서 SAP HANA 최소 배포에 필요한 IP 주소 범위](./media/hana-overview-connectivity/image4b-ip-addres-ranges-necessary.png)

또한 tooMicrosoft 제출 hello 데이터 집계의 hello 가능성이 있습니다. 이 경우 hello hello Azure VNet의 주소 공간만 포함 하나의 공백이 있습니다. 이전 버전의 hello 예에 사용 된 hello IP 주소 범위를 사용 합니다. 이 집계된 VNet 주소 공간은 다음과 같습니다.

![Azure(큰 인스턴스)에서 SAP HANA 최소 배포에 필요한 IP 주소 범위의 두 번째 가능성](./media/hana-overview-connectivity/image5b-ip-addres-ranges-necessary-one-value.png)

Hello Azure VNet의 hello 주소 공간을 정의 하는 두 개의 더 작은 범위 대신 위에서 볼 수 있듯이 우리는 4096 IP 주소를 검사 하는 하나의 큰 범위입니다. 이러한 큰 정의의 주소 공간 hello 사용 되지 않는 일부 큰 범위를 유지합니다. BGP 경로 전파에 대 한 hello VNet 주소 공간 값을 사용 하므로의 사용 hello 사용 하지 않는 범위 온-프레미스 또는 다른 위치에서 네트워크의 라우팅 하면 문제가 발생할 수 있습니다. 따라서 것이 권장된 tookeep hello 밀접 하 게 hello 실제 서브넷 주소 공간 사용 되는 주소 공간에 맞춰집니다. Hello VNet에 가동 중지 시간 없이 필요한 경우 나중에 새 주소 공간 값을 추가할 항상 있습니다.
 
> [!IMPORTANT] 
> 각 IP 주소 범위의 ER-P2P, 서버 IP 풀에서 Azure VNet 주소 공간 해야 **하지** 서로 겹치는 또는 다른 범위를 사용 하 여 네트워크의 다른 위치; 각 불연속 열 이어야 및 hello 두 그래픽으로 이전 표시 되지 않을 수 있습니다는 다른 범위의 서브넷입니다. 범위 사이 겹치면 toohello ExpressRoute 회로 hello Azure VNet에 연결 하지 않을 수 있습니다.

### <a name="next-steps-after-address-ranges-have-been-defined"></a>주소 범위를 정의한 후 다음 단계
Hello IP 주소 범위를 정의한 후 hello 다음과 같은 작업 필요 toohappen 합니다.

1. Hello hello 문서 맨 앞에 나열 된 다른 데이터와 함께 Azure VNet 주소 공간, hello ER P2P 연결 및 서버 IP 풀 주소 범위에 대 한 hello IP 주소 범위를 제출 합니다. 이 시점에서,도 시작할 수 있습니다 toocreate hello VNet 및 hello VM 서브넷. 
2. Express 경로 회로 Azure 구독 및 hello HANA 큰 인스턴스 스탬프 간에 Microsoft에서 생성 됩니다.
3. Microsoft에서 테 넌 트 네트워크 hello 큰 인스턴스 스탬프에 만들어집니다.
4. Microsoft은 Azure VNet 주소 공간에서 통신 하는 HANA 큰 인스턴스 IP 주소 인프라 tooaccept (대형 인스턴스) Azure에서 SAP HANA hello에서 네트워킹을 구성 합니다.
5. Hello Azure (대형 인스턴스) SKU에서 특정 SAP HANA 구입에 따라 Microsoft에서 테 넌 트 네트워크 계산 단위 할당, 할당 및 저장소를 탑재 및 hello 운영 체제 (SUSE 또는 Red Hat Linux)를 설치 합니다. 이러한 장치에 대 한 IP 주소는 hello 서버 IP 풀 주소 범위 tooMicrosoft 전송에서 수행 됩니다.

Microsoft는 hello 배포 프로세스의 hello 끝 hello 데이터 tooyou 다음을 제공 합니다.
- Tooconnect Azure Vnet tooHANA 큰 인스턴스를 연결 하 여 Azure VNet(s) toohello ExpressRoute 회로 필요한 정보:
     - 권한 부여 키
     - ExpressRoute PeerID
- 한 후 데이터 tooaccess HANA 큰 인스턴스 ExpressRoute 회로 Azure VNet를 설정 합니다.

HANA 큰 인스턴스 hello 문서에 연결 하는 hello 시퀀스를 찾을 수도 있습니다 [tooEnd SAP HANA 큰 인스턴스에 대 한 설치 프로그램을 종료](https://azure.microsoft.com/resources/sap-hana-on-azure-large-instances-setup/)합니다. 다양 한 단계를 수행 하는 hello 해당 문서에 배포 하는 예에에서 표시 됩니다. 


## <a name="connecting-a-vnet-toohana-large-instance-expressroute"></a>VNet tooHANA 큰 인스턴스 ExpressRoute 연결

모든 hello IP 주소 범위를 정의 하 고 이제 Microsoft에서 hello 데이터를 다시 가져온 hello tooHANA 큰 인스턴스 전에 만든 VNet 연결을 시작할 수 있습니다. 한 번 hello Azure VNet 만들어질, express 경로 게이트웨이 만들어야 hello VNet toolink hello VNet toohello hello 큰 인스턴스 스탬프에서 toohello 고객 테 넌 트를 연결 하는 ExpressRoute 회로에 합니다.

> [!NOTE] 
> 이 단계에 Azure 구독을 지정 하는 hello hello 새 게이트웨이 만들어지고 연결 된 toohello Azure VNet을 지정 하는 다음으로 too30 분 toocomplete 차지할 수 있습니다.

게이트웨이가 이미 있는 경우 ExpressRoute 게이트웨이인지 여부를 확인합니다. 그렇지 않으면 hello 게이트웨이 삭제 하 고 express 경로 게이트웨이로 다시 해야 합니다. Express 경로 게이트웨이가 이미 설정 hello Azure VNet이 이미 연결 온-프레미스 연결에 대 한 toohello ExpressRoute 회로 경우 toohello 아래의 Vnet 연결 섹션을 진행 합니다.

- (New) 중 하나가 hello를 사용 하 여 [Azure 포털](https://portal.azure.com/), 또는 PowerShell toocreate ExpressRoute VPN 게이트웨이 tooyour VNet를 연결 합니다.
  - 새 Azure 포털 hello를 사용 하는 경우 추가 **가상 네트워크 게이트웨이** 선택한 후 **ExpressRoute** hello 게이트웨이 유형으로 합니다.
  - PowerShell을 대신 선택 하는 경우 먼저 다운로드 하 여 최신 버전의 hello를 사용 하 여 [Azure PowerShell SDK](https://azure.microsoft.com/downloads/) tooensure 최적의 경험 합니다. 다음 명령을 hello express 경로 게이트웨이 만듭니다. hello 텍스트 앞에  _$_  해당 필요 toobe 특정 사용자 정보로 업데이트 하는 사용자 정의 변수입니다.

```PowerShell
# These Values should already exist, update toomatch your environment
$myAzureRegion = "eastus"
$myGroupName = "SAP-East-Coast"
$myVNetName = "VNet01"

# These values are used toocreate hello gateway, update for how you wish hello GW components toobe named
$myGWName = "VNet01GW"
$myGWConfig = "VNet01GWConfig"
$myGWPIPName = "VNet01GWPIP"
$myGWSku = "HighPerformance" # Supported values for HANA Large Instances are: HighPerformance or UltraPerformance

# These Commands create hello Public IP and ExpressRoute Gateway
$vnet = Get-AzureRmVirtualNetwork -Name $myVNetName -ResourceGroupName $myGroupName
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
New-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName `
-Location $myAzureRegion -AllocationMethod Dynamic
$gwpip = Get-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $myGWConfig -SubnetId $subnet.Id `
-PublicIpAddressId $gwpip.Id

New-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName -Location $myAzureRegion `
-IpConfigurations $gwipconfig -GatewayType ExpressRoute `
-GatewaySku $myGWSku -VpnType PolicyBased -EnableBgp $true
```

이 예제에서는 고성능 게이트웨이 SKU hello 사용 되었습니다. 옵션 (대형 인스턴스) Azure에서 SAP HANA에 지원 되는 게이트웨이 Sku만 hello 대로 HighPerformance 또는 UltraPerformance 집니다.

> [!IMPORTANT]
> 에 대 한 hello SKU의 큰 인스턴스 HANA S384, S384m, S384xm, S576, S768, 및 유형의 S960 (II 클래스 Sku 형식), hello hello UltraPerformance 게이트웨이 SKU의 사용은 필수입니다.

### <a name="linking-vnets"></a>VNet 연결

이제 hello Azure VNet에 express 경로 게이트웨이 사용 하는 hello 인증 정보가이 연결에 대해 만든 (대형 인스턴스) Azure express 경로 회로에 Microsoft tooconnect hello express 경로 게이트웨이 toohello SAP HANA에서 제공 합니다. Hello Azure 포털 또는 PowerShell을 사용 하 여이 단계를 수행할 수 있습니다. 그러나 다음과 같은 PowerShell 지침은 hello 포털이 좋습니다. 

- 각 연결에 대해 다른 AuthGUID를 사용 하 여 각 VNet 게이트웨이 대 한 명령을 수행 하는 hello를 실행 합니다. hello 스크립트 다음에 표시 된 hello 처음 두 항목은 Microsoft에서 제공 하는 hello 정보에서 가져옵니다. 또한 hello AuthGUID 모든 VNet 및 해당 게이트웨이를 해당 됩니다. 다른 Azure VNet tooadd 하려는 경우 필요한 tooget 다른 AuthID HANA 큰 인스턴스를 Azure에 연결 하 여 ExpressRoute 회로 대 한를 의미 합니다. 

```PowerShell
# Populate with information provided by Microsoft Onboarding team
$PeerID = "/subscriptions/9cb43037-9195-4420-a798-f87681a0e380/resourceGroups/Customer-USE-Circuits/providers/Microsoft.Network/expressRouteCircuits/Customer-USE01"
$AuthGUID = "76d40466-c458-4d14-adcf-3d1b56d1cd61"

# Your ExpressRoute Gateway Information
$myGroupName = "SAP-East-Coast"
$myGWName = "VNet01GW"
$myGWLocation = "East US"

# Define hello name for your connection
$myConnectionName = "VNet01GWConnection"

# Create a new connection between hello ER Circuit and your Gateway using hello Authorization
$gw = Get-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName
    
New-AzureRmVirtualNetworkGatewayConnection -Name $myConnectionName `
-ResourceGroupName $myGroupName -Location $myGWLocation -VirtualNetworkGateway1 $gw `
-PeerId $PeerID -ConnectionType ExpressRoute -AuthorizationKey $AuthGUID
```

Tooconnect hello 게이트웨이 toomultiple ExpressRoute 회로 구독과 연결 하려면 할 수 있습니다 tooexecute이이 단계 두 번 이상. 예를 들어 가능성이 하려는 tooconnect hello hello VNet tooyour 온-프레미스 네트워크에 연결 하는 동일한 VNet 게이트웨이 toohello ExpressRoute 회로 합니다.

## <a name="adding-more-ip-addresses-or-subnets"></a>더 많은 IP 주소 또는 서브넷 추가

더 많은 IP 주소 또는 서브넷을 추가 하는 경우 어느 hello Azure 포털, PowerShell 또는 CLI를 사용 합니다.

이 경우 hello 좋습니다 tooadd hello 새 IP 주소 범위 새 범위 toohello VNet 주소 공간으로 집계 된 새 범위를 생성 하는 대신. 두 경우 모두 toosubmit이 변경 tooMicrosoft tooallow 연결을 하면 해당 새 IP 주소 범위 toohello HANA 큰 인스턴스 단위 아웃 클라이언트에서 됩니다. Azure 지원 요청 tooget hello 새 VNet 주소 공간 추가 열 수 있습니다. 확인 메시지가 나타나면 hello 다음 단계를 수행 합니다.

hello Azure 포털에서에서는 추가로 서브넷 toocreate hello 문서를 참조 하십시오. [hello Azure 포털을 사용 하 여 가상 네트워크를 만들고](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), powershell에서 toocreate 참조 및 [PowerShell을사용하여가상네트워크만들기](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="adding-vnets"></a>VNet 추가

하나 이상의 Azure Vnet에 처음 연결 하면 tooadd (대형 인스턴스) Azure에서 SAP HANA에 액세스 하는 것을 추가로 할 수 있습니다. 첫째, Azure 지원 요청을 제출, 요청에 hello 특정 정보 식별 hello Azure는 배포와의 Azure VNet 주소 공간 hello hello IP 주소 공간 범위도 모두를 포함 합니다. SAP HANA Azure 서비스 관리에서 다음 정보를 제공 hello 필요한 tooconnect hello Vnet 및 express 경로 추가 합니다. 모든 VNet에 대 한 고유한 인증 키 tooconnect toohello ExpressRoute 회로 tooHANA 큰 인스턴스 해야합니다.

새 Azure VNet tooadd 단계:

1. Hello hello 온 보 딩 프로세스의 첫 번째 단계를 완료 한 자세한 내용은 hello _Azure VNet 만들기_ 섹션.
2. Hello hello 온 보 딩 프로세스의 두 번째 단계를 완료 한 자세한 내용은 hello _게이트웨이 서브넷을 만드는_ 섹션.
3. tooconnect 프로그램 추가 Vnet toohello HANA 큰 인스턴스 ExpressRoute 회로에 정보와 함께 Azure 지원 요청을 열고 새 VNet을 hello 및 새 인증 키를 요청 합니다.
4. Hello 인증이 toocomplete hello hello 온 보 딩 프로세스의 세 번째 단계는 hello Microsoft에서 제공한 인증 정보를 사용 하 여, 완료 됨을 알림을 받은 후 참조 hello _Vnet 연결_ 섹션.

## <a name="increasing-expressroute-circuit-bandwidth"></a>ExpressRoute 회로 대역폭 증가

Azure의 SAP HANA Service Management에 문의하세요. 이 권장된 tooincrease hello 대역폭 (대형 인스턴스) Azure express 경로 회로에 hello SAP HANA의 경우 Azure 지원 요청을 만듭니다. (10gbps tooa 최대를 단일 회로 대역폭에 대 한 증가 요청할 수 있습니다.) Hello 작업이 완료 된 후 다음 알림을 받을합니다 추가 작업이 필요 하지 tooenable Azure에서이 높은 속도입니다.

## <a name="adding-an-additional-expressroute-circuit"></a>추가 ExpressRoute 회로 추가

새 ExpressRoute 회로 (및 tooget 권한 부여 정보 tooconnect tooit)는 Azure 지원 요청 toocreate 확인 추가 ExpressRoute 회로 필요한의 좋습니다 하는 경우 Azure 서비스 관리에서 SAP HANA 문의 하십시오. hello 주소 공간을 사용할 hello Vnet Azure 서비스 관리 tooprovide 권한 부여에서 SAP HANA에 대해 순서로 hello 요청을 수행 하기 전에 정의 해야 합니다.

Hello 새 회로가 만들어진 Azure 서비스 관리 구성에 SAP HANA hello 완료 되 면 tooproceed 필요한 hello 정보에 tooreceive 알림을 하려고 합니다. 만들기 및 hello 새 VNet toothis 추가 회로 연결에 대 한 위에 제공 된 hello 단계를 수행 합니다. 없는 수 tooconnect Azure Vnet toothis 추가 회로 tooanother SAP HANA hello에서 Azure (대형 인스턴스) ExpressRoute 회로에 이미 연결 된 동일한 Azure 지역입니다.

## <a name="deleting-a-subnet"></a>서브넷 삭제

tooremove VNet 서브넷 중 하나가 hello Azure 포털, PowerShell 또는 CLI를 사용할 수 있습니다. Azure VNet IP 주소 범위/Azure VNet 주소 공간이 집계 범위인 경우 Microsoft의 후속 조치가 없습니다. 해당 hello를 제외 하 고 VNet 전파 되 고 여전히 BGP 경로 주소 공간을 삭제 하는 hello 서브넷을 포함 합니다. 여러 IP 주소 범위도 hello Azure VNet IP 주소 범위/Azure VNet 주소 공간을 정의 하는 경우 어떤 것의 삭제 된 할당 된 tooyour 서브넷을 VNet 주소 공간 부족를 삭제 하 고 이후에 Azure 서비스 관리에서 SAP HANA를 알릴 Azure (대형 인스턴스)에서 해당 SAP HANA 범위 hello에서 tooremove와 toocommunicate를 허용 됩니다.

서브넷을 제거에 특정 한 전용 Azure.com 지침, 서브넷을 제거 하기 위한 hello 프로세스는 아직 없는 hello를 반대로 hello에 대 한 프로세스에 추가 합니다. Hello 문서 참조 [hello Azure 포털을 사용 하 여 가상 네트워크 만들기](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 서브넷을 만드는 방법에 대 한 자세한 내용은 합니다.

## <a name="deleting-a-vnet"></a>VNet 삭제

VNet을 삭제할 때 어느 hello Azure 포털, PowerShell 또는 CLI를 사용 합니다. Azure 서비스 관리에서 SAP HANA hello Azure (대형 인스턴스) ExpressRoute 회로에 SAP HANA hello에 대 한 기존 권한 제거 하 고 hello Azure VNet IP 주소 범위/Azure VNet에서 주소 공간을 hello 통신용 HANA 큰 인스턴스를 제거 합니다.

VNet hello 제거 되 면 Azure 지원 요청 tooprovide hello IP 주소 공간 범위 toobe 제거를 엽니다.

Vnet를 제거 하는 방법에 특정 한 전용 Azure.com 지침, Vnet을 제거 하기 위한 hello 프로세스는 아직 없는 hello에 대 한 프로세스, 위에서 설명한 추가 hello를 반대로 합니다. Hello 문서를 참조 [hello Azure 포털을 사용 하 여 가상 네트워크를 만들고](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 및 [PowerShell을 사용 하 여 가상 네트워크를 만들고](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Vnet을 만드는 방법에 대 한 자세한 내용은 합니다.

모든 항목이 제거 되 면 tooensure hello 다음 항목을 삭제 합니다.

- express 경로 연결을 VNet 게이트웨이 hello VNet 게이트웨이 공용 IP 및 VNet

## <a name="deleting-an-expressroute-circuit"></a>ExpressRoute 회로 삭제

Azure 서비스 관리에서 SAP HANA로 Azure 지원 요청을 열고 hello 회로 삭제할지 요청 tooremove (대형 인스턴스) Azure express 경로 회로에 추가 SAP HANA 합니다. Hello Azure 구독 내에서 삭제 하거나 필요에 따라 VNet hello 유지 될 수 있습니다. 그러나 hello 연결이 hello HANA 큰 인스턴스 ExpressRoute 회로 삭제 해야 하 고 hello VNet 게이트웨이 연결.

또한 tooremove VNet을 하려는 경우 위의 hello 섹션에는 VNet 삭제에 hello 지침을 따릅니다.


