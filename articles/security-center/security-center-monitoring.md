---
title: "Azure 보안 센터에서 aaaSecurity 모니터링 | Microsoft Docs"
description: "이 문서에서는 tooget 모니터링 기능에 Azure 보안 센터를 시작 합니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3bd5b122-1695-495f-ad9a-7c2a4cd1c808
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: 43c2a8864d5fe27ba44b0d7bc979db970305ec17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-health-monitoring-in-azure-security-center"></a>Azure Security Center에서 보안 상태 모니터링
이 문서에서는 hello Azure 보안 센터 toomonitor 준수 정책 사용 하 여 모니터링 기능을 사용 하 여 합니다.

## <a name="what-is-security-health-monitoring"></a>보안 상태 모니터링이란?
우리는 종종를 감시 하 고 म toohello 상황 반응할 수 있도록 이벤트 toooccur에 대 한 대기로 모니터링 생각 합니다. 보안 모니터링 toohaving 조직의 표준 또는 모범 사례를 충족 하지 않는 리소스 tooidentify 시스템을 감사 하는 자동 관리 전략을 참조 합니다.

## <a name="monitoring-security-health"></a>보안 상태 모니터링
사용 하도록 설정한 후 [보안 정책](security-center-policies.md) 구독의 리소스에 대 한 보안 센터를 hello 보안 리소스 tooidentify 잠재적인 취약점을 분석 합니다. 네트워크 구성 정보는 즉시 이용할 수 있지만, 1 시간 걸릴 수 있습니다 또는 상태 및 운영 체제 구성, 사용 가능한 toobecome 보안 등의 가상 컴퓨터 구성에 대 한 정보에 대 한 추가 업데이트 합니다. Hello에서 모든 문제와 리소스의 hello 보안 상태를 볼 수 있습니다 **방지** 섹션. Hello에도 이러한 문제의 목록을 볼 수 있습니다 **권장 사항을** 바둑판식으로 배열입니다.

방법에 대 한 자세한 내용은 tooapply 권장 사항, 읽을 [Azure 보안 센터에서 보안 권장 사항 구현](security-center-recommendations.md)합니다.

Hello에서 **방지** 섹션 hello 보안 리소스 상태를 모니터링할 수 있습니다. 다음 예제는 hello에서 볼 수 있습니다 (계산, 네트워킹, 저장소 및 데이터 및 응용 프로그램)의 각 리소스의 타일에 있는 식별 된 문제의 hello 총 수입니다.

![리소스 보안 상태 타일](./media/security-center-monitoring/security-center-monitoring-fig1-newUI-2017.png)


### <a name="monitor-compute"></a>모니터 계산
클릭할 때 **계산** 타일을 hello **계산** 열리는 블레이드 세 개의 탭을 보여 줍니다.

- **개요**: 모니터링 및 가상 컴퓨터 권장 사항입니다.
- **Virtual Machines**: 모든 가상 컴퓨터와 현재 보안 상태를 나열합니다.
- **Cloud Services**: Security Center에서 모니터링하는 모든 웹 및 작업자 역할의 목록을 나열합니다.

![가상 컴퓨터에서 누락된 시스템 업데이트](./media/security-center-monitoring/security-center-monitoring-fig1-new002-2017.png)

각 탭에서 섹션이 여러 개 있을 수 있으며 각 섹션에서 개별 옵션 toosee를 선택할 수 있습니다 hello에 대 한 자세한 내용은 단계 tooaddress 특정 문제를 권장 합니다. 

#### <a name="monitoring-recommendations"></a>권장 사항 모니터링
이 섹션에서는 hello 데이터 수집 및 현재 상태에 대 한 초기화 된 가상 컴퓨터의 총 수를 보여 줍니다. 모든 가상 컴퓨터, 데이터 컬렉션을 초기화 한 다음 준비 tooreceive 보안 센터 보안 정책이 됩니다. 이 항목을 클릭할 때 hello **VM 에이전트가 없거나 응답 하지 않는** 블레이드를 엽니다. 

![가상 컴퓨터에서 누락된 시스템 업데이트](./media/security-center-monitoring/security-center-monitoring-fig1-new003-2017.png)


#### <a name="virtual-machine-recommendations"></a>가상 컴퓨터 권장 사항
이 섹션에는 Azure Security Center에서 모니터링하는 [각 VM에 대한 권장 사항](security-center-virtual-machine-recommendations.md)이 있습니다. hello 첫 번째 열에는 hello 권장 사항을 나열합니다. hello 두 번째 열 hello 해당 권장 구성의 영향을 받는 가상 컴퓨터의 총 수를 표시 합니다. hello 세 번째 열 hello 스크린 샷 다음에 설명 된 대로 hello 문제의 hello 심각도 표시 합니다.

![가상 컴퓨터 권장 사항](./media/security-center-monitoring/security-center-monitoring-fig1-new004-2017.png)

> [!NOTE]
> Hello에 공용 끝점을 하나 이상 가상 컴퓨터만 표시 되어 **네트워킹 상태** hello 블레이드 **네트워크 토폴로지** 목록입니다.
>
>

각 권장 사항에는 클릭하면 수행되는 작업 집합이 있습니다. 예를 들어, 클릭 하면 **누락 된 시스템 업데이트**, hello **누락 된 시스템 업데이트** 블레이드를 엽니다. Hello 고 가상 컴퓨터를 패치 누락 된 hello 다음과 같이 hello 누락 된 업데이트의 심각도 hello 나열 스크린 샷 합니다.

![가상 컴퓨터에서 누락된 시스템 업데이트](./media/security-center-monitoring/security-center-monitoring-fig5-ga.png)

hello **누락 된 시스템 업데이트** 블레이드 hello 다음 정보로 테이블을 보여 줍니다.

* **가상 컴퓨터**: 업데이트가 설치 되어 있지 hello 가상 컴퓨터의 hello 이름입니다.
* **시스템 업데이트**: hello 누락 된 시스템 업데이트 수입니다.
* **마지막 검사 시간**: hello 시간 보안 센터 마지막 업데이트에 대 한 hello 가상 컴퓨터를 검색 합니다.
* **상태**: hello hello 권장 구성의 현재 상태:
  * **열기**: hello 권장 사항 해결 하지 했습니다.
  * **진행 중인**: hello 권장 구성이 현재 적용 된 toothose 리소스를 생성할 수 있으며 사용자가 아무 작업도 필요 합니다.
  * **해결**: hello 권장 사항이 이미 만료 되었습니다. (Hello 문제를 해결 hello 항목이 흐리게 표시 됩니다).
* **심각도**: hello 심각도입니다. 해당 특정 권장 사항 설명 합니다.
  * **높음**: 중요한 리소스(응용 프로그램, VM 또는 네트워크 보안 그룹)에 취약점이 있으며 주의가 필요합니다.
  * **보통**: 단순한 또는 추가 단계는 필요한 toocomplete 프로세스 또는 문제를 제거 합니다.
  * **낮음**: 취약점을 해결해야 하지만 즉각적인 주의가 필요하지 않습니다. (기본적으로 낮은 권장 사항 표시 되지 않은, 하지만 tooview 하려는 경우 낮은 권장 사항에 필터링 할 수 있습니다 이러한.)

tooview hello 권장 사항 세부 정보에는 hello 가상 컴퓨터의 hello 이름을 클릭 합니다. Hello 스크린 샷 다음 그림과 같이 hello 업데이트 목록이 해당 가상 컴퓨터는 새 블레이드가 열립니다.

![특정 가상 컴퓨터에서 누락된 시스템 업데이트](./media/security-center-monitoring/security-center-monitoring-fig6-ga.png)

> [!NOTE]
> hello 보안 권장 사항 여기는 hello의 것과 동일한 hello **권장 사항을** 블레이드입니다. Hello 참조 [Azure 보안 센터에서 보안 권장 사항 구현](security-center-recommendations.md) 방법에 대 한 자세한 내용은 문서 tooresolve 권장 사항입니다. 뿐만 아니라 hello에서 사용할 수 있는 모든 리소스를 뿐만 아니라 가상 컴퓨터에 적용 됩니다 **리소스 상태** 바둑판식으로 배열입니다.
>
>

#### <a name="virtual-machines-section"></a>가상 컴퓨터 섹션
hello 가상 컴퓨터 섹션에서는 모든 가상 컴퓨터 및 권장 사항에 대 한 개요를 제공 합니다. 각 열 hello 스크린 샷 뒤에 표시 된 대로의 권장 구성 하나의 집합을 나타냅니다.

![모든 가상 컴퓨터 및 권장 사항 개요](./media/security-center-monitoring/security-center-monitoring-fig1-new005-2017.png)

각 권장 사항 사용 하면 아래에 표시 되는 hello 아이콘 tooquickly 하면 주의가 필요한 및 유형 권장 구성의 hello는 hello 가상 컴퓨터를 식별 합니다.

Hello 이전 예제에서는 하나의 가상 컴퓨터에는 끝점 보호와 관련 된 중요 한 권장 구성이 있습니다. tooget hello 가상 컴퓨터에 대 한 자세한 내용은 클릭 합니다. 열리는 새 블레이드의 스크린 샷 다음 hello와 같이이 가상 컴퓨터를 나타냅니다.

![가상 컴퓨터 보안 세부 정보](./media/security-center-monitoring/security-center-monitoring-fig8-ga.png)

이 블레이드는 hello 가상 컴퓨터에 대 한 hello 보안 세부 정보를 포함 합니다. 이 블레이드의 hello 아래쪽 hello 권장 작업 및 각 문제의 hello 심각도 볼 수 있습니다.

#### <a name="cloud-services-section"></a>클라우드 서비스 섹션
클라우드 서비스에 대 한 권장 사항은 hello 운영 체제 버전은 오래 된 hello 스크린 샷 뒤에 표시 된 대로 때 만들어집니다.

![클라우드 서비스 상태](./media/security-center-monitoring/security-center-monitoring-fig1-new006-2017.png)

권장 사항 (하지 hello에 대 한 경우 hello 앞의 예제) 권한이 시나리오에서는 hello 권장 tooupdate hello 운영 체제 버전의 hello 단계 toofollow 해야 합니다. 업데이트를 사용할 수 있는 경고 해야 합니다 (빨간색-주황색 했는지에 따라 또는 hello 문제의 hello 심각도). WebRole1 (Windows Server 웹 응용 프로그램을 자동으로 배포 tooIIS로 실행) 또는 (Windows Server 웹 응용 프로그램을 자동으로 배포 tooIIS로 실행) WorkerRole1 hello 행에서이 경고를 클릭 하면이 대 한 자세한 정보는 새 블레이드가 열립니다. hello 스크린 샷 뒤에 표시 된 대로 권장 사항:

![클라우드 서비스 세부 정보](./media/security-center-monitoring/security-center-monitoring-fig8-new3.png)

이 권장 구성에 대 한 규정 설명을 toosee 클릭 **업데이트 OS 버전** hello에서 **설명** 열입니다. hello **업데이트 OS 버전 (미리 보기)** 자세한 정보와 함께 블레이드를 엽니다.

![클라우드 서비스 권장 사항](./media/security-center-monitoring/security-center-monitoring-fig8-new4.png)  

### <a name="monitor-virtual-networks"></a>가상 네트워크 모니터링
클릭할 때 **네트워킹** 타일을 hello **네트워킹** hello 스크린 샷 뒤에 표시 된 대로 자세한 정보 블레이드에서 열립니다.

![네트워킹 블레이드](./media/security-center-monitoring/security-center-monitoring-fig9-new3.png)

#### <a name="networking-recommendations"></a>네트워킹 권장 사항
가상 컴퓨터의 리소스 상태 정보를 hello, 처럼이 블레이드 hello 아래쪽에 요약 된 hello 블레이드 맨 hello 및 모니터링 되는 네트워크의 목록이 문제 목록이 제공 합니다.

상태 분류 섹션 네트워킹 hello 잠재적인 보안 문제를 나열 하 고 제공 [권장 사항을](security-center-network-recommendations.md)합니다. 가능한 문제는 다음을 포함할 수 있습니다.

* 차세대 방화벽(NGFW)이 설치되지 않음
* 서브넷에서 NSG(네트워크 보안 그룹) 사용 안 함
* VM에서 NSG 사용 안 함
* 공용 외부 끝점을 통한 외부 액세스 제한
* 정상 인터넷 연결 끝점

권장 사항을 클릭 hello 다음 예제와 같이 hello 권장 사항에 대 한 자세한 정보는 새 블레이드가 열립니다.

![Hello 네트워킹 블레이드에서 권장 사항에 대 한 세부 정보](./media/security-center-monitoring/security-center-monitoring-fig9-ga.png)

이 예제에서는 hello **누락 된 네트워크 보안 그룹 구성 서브넷에 대 한** 블레이드는 서브넷 목록 및 누락 된 가상 컴퓨터를 네트워크 보안 그룹을 보호 합니다. Hello 서브넷 toowhich tooapply hello 네트워크 보안 그룹을 클릭 하면 다른 블레이드가 열립니다.

Hello에 **네트워크 보안 그룹 선택** 블레이드에서 hello 서브넷에 대 한 hello 가장 적합 한 네트워크 보안 그룹 선택 하거나 새 네트워크 보안 그룹을 만들 수 있습니다.

#### <a name="internet-facing-endpoints-section"></a>인터넷 연결 끝점 섹션
Hello에 **인터넷 연결 끝점** 섹션은 현재는 인터넷 끝점 및 서버 인스턴스의 현재 상태를 연결로 구성 된 hello 가상 컴퓨터를 볼 수 있습니다.

![인터넷 연결 끝점으로 구성된 가상 컴퓨터 및 상태](./media/security-center-monitoring/security-center-monitoring-fig10-ga.png)

이 테이블 hello 끝점을 나타내는 이름 hello 가상 컴퓨터를 hello 인터넷 연결 IP 주소 및 hello 네트워크 보안 그룹의 현재 심각도 상태 hello 않았으며 NGFW hello 됩니다. hello 테이블 심각도 별로 정렬 됩니다.

* 빨간색(최우선): 높은 우선 순위이며 즉시 해결해야 합니다.
* 주황색: 보통 우선 순위이며 가능한 한 빨리 해결해야 합니다.
* 녹색(마지막): 정상 상태

#### <a name="networking-topology-section"></a>네트워킹 토폴로지 섹션
hello **네트워킹 토폴로지** hello 스크린 샷 뒤에 표시 된 대로 섹션에 hello 리소스의 계층적 보기:

![네트워킹 토폴로지 섹션의 계층적 리소스 보기](./media/security-center-monitoring/security-center-monitoring-fig121-new4.png)

다음과 같이 심각도 별로 테이블이 정렬됩니다(VM 및 서브넷).

* 빨간색(최우선): 높은 우선 순위이며 즉시 해결해야 합니다.
* 주황색: 보통 우선 순위이며 가능한 한 빨리 해결해야 합니다.
* 녹색(마지막): 정상 상태

Hello 첫 번째 수준에는이 토폴로지 뷰에서 [가상 네트워크](../virtual-network/virtual-networks-overview.md), [가상 네트워크 게이트웨이](/vpn-gateway/vpn-gateway-site-to-site-create.md), 및 [가상 네트워크 (클래식)](/virtual-network/virtual-networks-create-vnet-classic-pportal.md)합니다. 두 번째 수준 hello 서브넷이 많고 hello 세 번째 수준 toothose 서브넷에 속하는 hello 가상 컴퓨터. hello 오른쪽 열에 다음 예제는 hello와 같이 hello 해당 리소스에 대 한 hello 네트워크 보안 그룹의 현재 상태:

![네트워킹 토폴로지 섹션에 hello 네트워크 보안 그룹의 상태](./media/security-center-monitoring/security-center-monitoring-fig12-ga.png)

hello이 블레이드의 아래 부분에 hello 권장 사항이 비슷한이 가상 컴퓨터에 대 한 toowhat 이전에 설명 되어 있습니다. 자세한 권장 사항을 toolearn를 클릭 하거나 필요한 hello 보안 제어 또는 구성을 적용할 수 있습니다.

### <a name="monitor-storage--data"></a>저장소 및 데이터 모니터링

클릭할 때 **데이터 및 저장소** hello에 **방지** 섹션 hello **데이터 리소스** SQL 및 저장소에 대 한 권장 사항과 블레이드를 엽니다. 또한 [권장 사항을](security-center-sql-service-recommendations.md) hello 데이터베이스의 hello 일반 성능 상태에 대 한 합니다. 저장소 암호화에 대한 자세한 내용은 [Azure Security Center에서 Azure Storage 계정에 대한 암호화 사용](security-center-enable-encryption-for-storage-account.md)을 참고하세요.

![데이터 리소스](./media/security-center-monitoring/security-center-monitoring-fig13-newUI-2017.png)

아래 **SQL 권장 사항**, 모든 권장 사항을 클릭 수 및 get 대 한 자세한 내용은 추가 작업 tooresolve 문제가 있습니다. hello 다음 예제에서는 hello의 hello 확장 **SQL 데이터베이스에서 데이터베이스 감사 및 위협 검색** 권장 합니다.

![SQL 권장 사항에 대한 세부 정보](./media/security-center-monitoring/security-center-monitoring-fig14-ga-new.png)

hello **SQL 데이터베이스에서 감사를 사용 하도록 설정 및 위협 검색** 블레이드는 hello 다음 정보:

* SQL 데이터베이스의 목록
* 있는 hello 서버
* 이 설정은 hello 서버에서 상속 된 여부 또는이 데이터베이스에 고유한 경우에 대 한 정보
* hello 현재 상태
* hello 문제의 hello 심각도

이 권장 사항은 hello 데이터베이스 tooaddress을 클릭할 때 hello **감사 및 위협 검색** hello 다음 화면에에서 표시 된 대로 블레이드를 엽니다.

![감사 및 위협 감지 블레이드](./media/security-center-monitoring/security-center-monitoring-fig15-ga.png)

tooenable 감사를 위해 선택 **ON** hello에서 **감사** 옵션입니다.

### <a name="monitor-applications"></a>응용 프로그램 모니터링

Azure 작업에 응용 프로그램에 있는 경우 [(Azure 리소스 관리자를 통해 만든) 가상 컴퓨터](../azure-resource-manager/resource-manager-deployment-model.md) 보안 센터 노출 된 웹 포트 (TCP 포트 80 및 443)를 함께 이러한 tooidentify 잠재적인 보안 문제를 모니터링할 수 있습니다 및 해결 단계는 것이 좋습니다. Hello를 클릭할 때 **응용 프로그램** 타일을 hello **응용 프로그램** 일련의 hello에 대 한 권장 사항 블레이드에서 열립니다 **응용 프로그램 권장 사항을** 섹션. 또한 hello 스크린 샷 뒤에 표시 된 대로 각 호스트/가상 IP hello 응용 프로그램 작업 분석을 보여줍니다.

![응용프로그램 보안 상태](./media/security-center-monitoring/security-center-monitoring-fig16-ga.png)

하면 않은와 hello 기타 권장 사항, 하는 것 처럼 클릭할 수 있는 권장 사항을 toosee hello 문제에 대 한 자세한 내용은 방법과 tooremediate 합니다. hello 다음 그림에에서 표시 된 hello 예는 응용 프로그램 보안 되지 않은 웹 응용 프로그램으로 확인 됨입니다. 보안 고려 되었지만 hello 응용 프로그램을 선택 하는 경우 hello 다음 옵션을 사용할 수 있는 다른 블레이드가 열립니다.

![안전하지 않은 응용 프로그램에 대한 세부 정보](./media/security-center-monitoring/security-center-monitoring-fig17-ga.png)

이 블레이드에는 해당 응용 프로그램에 대한 모든 권장 사항을 보여 주는 목록이 있습니다. Hello를 클릭할 때 **추가 웹 응용 프로그램 방화벽** 권장 사항, hello **추가 웹 응용 프로그램 방화벽** 블레이드 옵션이 열립니다 tooinstall 있습니다에 대 한 웹 응용 프로그램 방화벽 (WAF)으로 파트너에서 다음 스크린 샷 hello에 나와 있습니다.

![웹 응용 프로그램 방화벽 추가 대화 상자](./media/security-center-monitoring/security-center-monitoring-fig18-ga.png)

## <a name="see-also"></a>참고 항목
이 문서에서는 방법에 대해 배웠습니다 toouse Azure 보안 센터의 기능을 모니터링 합니다. Azure 보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md): 자세한 방법을 Azure 보안 센터의 tooconfigure 보안 설정 합니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md): 자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md): toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md): 찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.
