---
title: "aaaTroubleshooting 및 모니터링의 SAP HANA Azure (대형 인스턴스)에서 | Microsoft Docs"
description: "Azure(큰 인스턴스)에서 SAP HANA 문제 해결 및 모니터링"
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
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a>Tootroubleshoot 및 모니터의 SAP HANA (대형 인스턴스) Azure에서


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a>Azure(큰 인스턴스)의 SAP HANA 모니터링

(대형 인스턴스) Azure에서 SAP HANA는 것과 다른 IaaS 배포는-OS hello 어떤 toomonitor 필요 하 고 hello 응용 프로그램은 수행 하 고 이러한 리소스를 다음 hello을 소비 하는 방법:

- CPU
- 메모리
- 네트워크 대역폭
- 디스크 공간

Azure 가상 컴퓨터와 함께 원하는 toofigure 이러한 고갈 가져올 여부 또는 위에 명시 된 hello 리소스 클래스가으로 충분 합니다. Hello 서로 다른 클래스의 각 자세히 다음과 같습니다.

**CPU 리소스 소비량:** hello SAP HANA에 대 한 특정 작업에 대해 정의 된 비율이 적용된 toomake 있는지 통해 hello 저장 된 데이터를 메모리에 충분 한 CPU 리소스가 사용 가능한 toowork 없어야 합니다. 그럼에도 불구 하 고 HANA 많은 CPU toomissing 인덱스 또는 이와 비슷한 문제가 인해 쿼리 실행을 사용 하는 경우 있을 수 있습니다. 즉, hello 특정 HANA 서비스가 사용 되는 CPU 리소스와 함께 hello HANA 인스턴스가 큰 단위의 CPU 리소스 사용 모니터링 해야 합니다.

**메모리 사용량:** 은 중요 한 toomonitor에서 HANA를 다른 곳과 HANA 외부 hello 단위에 있습니다. HANA, 내 hello 데이터 HANA 할당 된 크기 조정 지침 sap 필요한 hello 내에서 순서 toostay에 메모리를 소비 하는 방법을 모니터링 합니다. Hello 큰 인스턴스 수준 toomake 추가 설치 된 비-HANA 소프트웨어 메모리가 너무 많이 사용 고 따라서 메모리에 대 한 HANA와 경합 되지 않는 있는지에서 toomonitor 메모리 소비를 사용할 수 있습니다.

**네트워크 대역폭:** hello Azure VNet 게이트웨이 hello Azure VNet으로 이동 하는 데이터의 대역폭 제한 되어 있고, 모든 받은 toomonitor hello 데이터에 대해서 hello Azure의 toohello 한계는 얼마나 비슷한지를 VNet toofigure 내에서 Azure Vm hello 하면 도움이 됩니다 게이트웨이 SKU 선택한 합니다. Hello HANA 큰 인스턴스 단위에 게 의미 toomonitor 들어오고 나가는 네트워크 트래픽을 하 고 처리 하는 시간이 지남에 따라 hello 볼륨의 tookeep 추적 합니다.

**디스크 공간:** 디스크 공간 사용량은 일반적으로 시간이 지남에 따라 증가합니다. 여러 가지 원인이 있지만 대부분 데이터 볼륨 증가, 트랜잭션 로그 백업 실행, 추적 파일 저장 및 저장소 스냅숏 수행으로 인해 발생합니다. 따라서 중요 한 toomonitor 디스크 공간 사용 되며 hello HANA 큰 인스턴스 단위와 연결 된 hello 디스크 공간을 관리 합니다.

## <a name="monitoring-and-troubleshooting-from-hana-side"></a>HANA 쪽에서 모니터링 및 문제 해결

순서 tooeffectively 문제 관련된 tooSAP Azure (대형 인스턴스)에서 HANA을 분석 하에 문제의 근본 원인 hello 아래로 유용 toonarrow 합니다. SAP가 많은 양의 문서 toohelp 게시 있습니다.

적용 가능한 Faq 관련된 tooSAP HANA 성능 hello SAP Note를 다음에서 확인할 수 있습니다.

- [SAP 참고 사항 #2222200 – FAQ: SAP HANA 네트워크](https://launchpad.support.sap.com/#/notes/2222200)
- [SAP 참고 사항 #2100040 – FAQ: SAP HANA CPU](https://launchpad.support.sap.com/#/notes/0002100040)
- [SAP 참고 사항 #199997 – FAQ: SAP HANA 메모리](https://launchpad.support.sap.com/#/notes/2177064)
- [SAP 참고 사항 #200000 – FAQ: SAP HANA 성능 최적화](https://launchpad.support.sap.com/#/notes/2000000)
- [SAP 참고 사항 #199930 – FAQ: SAP HANA I/O 분석](https://launchpad.support.sap.com/#/notes/1999930)
- [SAP 참고 사항 #2177064 – FAQ: SAP HANA 서비스 다시 시작 및 충돌](https://launchpad.support.sap.com/#/notes/2177064)

**SAP HANA 경고**

첫 번째 단계로 hello 현재 SAP HANA 경고 로그를 확인 합니다. SAP HANA Studio에서 이동 너무**관리 콘솔: 경고: 표시: 모든 경고**합니다. 이 탭에는 hello 설정 최소 및 최대 임계값 범위에 속하지 않는 특정 값 (사용 가능한 실제 메모리, CPU 사용률 등)에 대 한 모든 SAP HANA 경고가 표시 됩니다. 기본적으로 검사는 15분마다 자동으로 새로 고쳐집니다.

![SAP HANA Studio 이동 tooAdministration 콘솔: 경고: 표시: 모든 경고](./media/troubleshooting-monitoring/image1-show-alerts.png)

**CPU**

Tooimproper 임계값 설정 인해 트리거되는 경고에 대 한는 해결 방법이 tooreset toohello 기본값 또는 보다 적절 한 크기 임계값을 지정 합니다.

![Toohello 기본값 또는 더 적절 하 게 임계값 값을 다시 설정](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

hello 경고 다음 CPU 리소스 문제를 나타낼 수 있습니다.

- 호스트 CPU 사용량(경고 5)
- 가장 최근 저장 지점 작업(경고 28)
- 저장 지점 기간(경고 54)

CPU 사용률이 높을 hello 다음 중 하나에서 SAP HANA 데이터베이스에서 발생할 수 있습니다.

- 경고 5(호스트 CPU 사용량)는 현재 또는 과거 CPU 사용량에 발생합니다.
- hello는 hello 개요 화면에 CPU 사용량 표시

![CPU 사용량 hello 개요 화면에 표시](./media/troubleshooting-monitoring/image3-cpu-usage.png)

hello 부하 그래프는 지난 hello에 CPU 사용률이 높을 또는 사용률이 높을 표시할 수 있습니다.

![hello 부하 그래프 지난 hello에서 CPU 사용률이 높을 또는 높은 소비를 표시할 수 있습니다.](./media/troubleshooting-monitoring/image4-load-graph.png)

Toohigh CPU 사용률 인해 트리거된 경고에 제한 되지 않음 등 여러 원인으로 인해 발생할 수 있습니다: 특정 트랜잭션, 데이터 로드, SQL 문 및 잘못 된 쿼리 성능을 (예를 들어 BW HANA에 장기 실행 작업의 첫 줄의 실행 큐브)입니다.

Toohello 참조 [SAP HANA 문제 해결: CPU 관련 시키고 유효성 검사 솔루션](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) 자세한 문제 해결 단계에 대 한 사이트입니다.

**운영 체제**

Linux에서 SAP HANA는 toomake 투명 하 게 거 대 한 페이지를 사용할 수 없다는 있는지 확인 하는 가장 중요 한 hello 중 하나를 참조 하십시오 [SAP 참고 #2131662 투명 하 게 거 대 한 페이지 (THP) SAP HANA 서버에](https://launchpad.support.sap.com/#/notes/2131662)합니다.

- Hello 다음 Linux 명령을 통해 투명 하 게 거 대 한 페이지 활성화 여부를 확인할 수 있습니다: **/sys/kernel/mm/transparent 분류기\_hugepage/설정**
- 경우 _항상_ 둘러싸입니다 아래와 같이 대괄호로 hello 투명 하 게 거 대 한 페이지는 사용할 수 있음을 의미: [항상] madvise 되지 경우 _되지_ 둘러싸입니다 해당 hello 투명 아래와 같이 대괄호로 의미 큰 페이지를 사용할 수 없습니다: 항상 madvise [하지]

다음 Linux 명령을 hello nothing을 반환 해야: **rpm qa | grep ulimit 합니다.** _ulimit_가 표시되는 경우 즉시 설치를 제거합니다.

**메모리**

Hello 크기가 것을 확인할 수 hello SAP HANA에 의해 할당 된 메모리의 데이터베이스 예상 보다 높습니다. 다음 경고 hello 높은 메모리 사용 문제를 나타냅니다.

- 호스트 실제 메모리 사용량(경고 1)
- 이름 서버의 메모리 사용량(경고 12)
- 열 저장소 테이블의 총 메모리 사용량(경고 40)
- 서비스의 메모리 사용량(경고 43)
- 열 저장소 테이블 중 기본 저장소의 메모리 사용량(경고 45)
- 런타임 덤프 파일(경고 46)

Toohello 참조 [SAP HANA 문제 해결: 메모리 문제](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) 자세한 문제 해결 단계에 대 한 사이트입니다.

**네트워크**

너무 참조[SAP 참고 #2081065 SAP HANA 네트워크 문제 해결](https://launchpad.support.sap.com/#/notes/2081065) hello 네트워크 문제 해결이 SAP note 단계를 수행 합니다.

1. 서버와 클라이언트 간의 왕복 시간을 분석합니다.
  A. Hello SQL 스크립트 실행 [ _HANA\_네트워크\_클라이언트_](https://launchpad.support.sap.com/#/notes/1969700)_합니다._
  
2. 노드 간 통신을 분석합니다.
  A. SQL 스크립트 [_HANA\_네트워크\_서비스_](https://launchpad.support.sap.com/#/notes/1969700)_를 실행합니다._

3. Linux 명령을 실행 **ifconfig** (hello 출력 패킷 손실을 발생 하는 경우 표시 하는 데 사용).
4. Linux 명령 **tcpdump**를 실행합니다.

또한 hello 오픈 소스를 사용 하 여 [IPERF](https://iperf.fr/) 도구 (또는 유사한 곳) toomeasure 실제 응용 프로그램 네트워크 성능입니다.

Toohello 참조 [SAP HANA 문제 해결: 성능 네트워킹 및 연결 문제](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) 자세한 문제 해결 단계에 대 한 사이트입니다.

**저장소**

최종 사용자 측면에서 볼 때 응용 프로그램 (또는 hello 시스템 전체의) 느리게 실행, 응답 하지 않는 또는 I/O 성능 문제가 있는 경우에 toohang를 보일 수도 있습니다. Hello에 **볼륨** 탭에서 SAP HANA Studio 볼 수 있습니다 hello 연결 된 볼륨 및 볼륨 각 서비스에 의해 사용 됩니다.

![SAP HANA Studio hello 볼륨 탭에서 볼 수 있습니다 hello 연결 된 볼륨 및 볼륨 각 서비스에 의해 사용 됩니다.](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

Hello 아래쪽의 세부 정보를 볼 수는 hello 화면에 연결 된 볼륨이 볼륨, 파일 및 I/O 통계와 같은 hello 합니다.

![Hello 아래쪽의 세부 정보를 볼 수는 hello 화면에 연결 된 볼륨이 hello 볼륨, 파일 등의 I/O 통계](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

Toohello 참조 [SAP HANA 문제 해결: I/O 관련 근본 원인 및 해결](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) 및 [SAP HANA 문제 해결: 디스크 관련 근본 원인 및 해결](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) 자세한 문제 해결 단계에 대 한 사이트입니다.

**진단 도구**

HANA\_Configuration\_Minichecks를 통해 SAP HANA 상태 검사를 수행합니다. 이 도구는 SAP HANA Studio에서 이미 경고로 발생했어야 하는 잠재적으로 중요한 기술 문제를 반환합니다.

너무 참조[SAP 참고 #1969700 SAP HANA에 대 한 SQL 문 컬렉션](https://launchpad.support.sap.com/#/notes/1969700) hello SQL Statements.zip 파일 첨부 toothat 참고를 다운로드 합니다. Hello 로컬 하드 드라이브에이.zip 파일을 저장 합니다.

Hello에 SAP HANA Studio에서 **시스템 정보** 탭에서 hello 마우스 오른쪽 단추로 클릭 **이름** 선택 **가져오기 SQL 문을**합니다.

![Hello 시스템 정보 탭에서 SAP HANA Studio에서 hello 이름 열을 마우스 오른쪽 단추로 클릭 하 고 SQL 문 가져오기 선택](./media/troubleshooting-monitoring/image7-import-statements-a.png)

선택 hello SQL Statements.zip 파일을 로컬에 저장 하 고 hello 해당 SQL 문으로 폴더를 가져옵니다. 이러한 SQL 문으로 여러 다른 진단 검사를 실행할 수 hello이 시점에서

예를 들어 tootest SAP HANA 시스템 복제 대역폭 요구 사항이 단추로 클릭 하 고 hello **대역폭** 문에 **복제: 대역폭** 선택 **열려** SQL 콘솔.

hello 완전 한 SQL 문이 변경 되 고 그런 다음 실행 가능 입력된 매개 변수 (수정 섹션) toobe를 열립니다.

![hello 완전 한 SQL 문이 변경 되 고 그런 다음 실행 가능 입력된 매개 변수 (수정 섹션) toobe를 열립니다.](./media/troubleshooting-monitoring/image8-import-statements-b.png)

또 다른 예로 hello 문 아래에 단추로 클릭 한 다음 **복제: 개요**합니다. 선택 **Execute** hello 상황에 맞는 메뉴에서:

![또 다른 예로 복제 hello 문에서 단추로 클릭 한 다음: 개요입니다. Hello 상황에 맞는 메뉴에서 실행을 선택 합니다.](./media/troubleshooting-monitoring/image9-import-statements-c.png)

그러면 문제 해결에 도움이 되는 정보가 표시됩니다.

![그러면 문제 해결에 도움이 되는 정보가 표시됩니다.](./media/troubleshooting-monitoring/image10-import-statements-d.png)

HANA에 대해 동일 hello 마십시오\_구성\_Minichecks 및 검사에 대 한 _X_ hello에서 부호 _C_ (Critical) 열입니다.

샘플 출력:

일반 SAP HANA 검사는 **HANA\_Configuration\_MiniChecks\_Rev102.01+1**.

![일반 SAP HANA 검사는 [HANA\_Configuration\_MiniChecks\_Rev102.01+1].](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

현재 실행 중인 SAP HANA 서비스의 개요는 **HANA\_Services\_Overview**.

![현재 실행 중인 SAP HANA 서비스의 개요는 [HANA\_Services\_Overview].](./media/troubleshooting-monitoring/image12-services-overview.png)

SAP HANA 서비스 정보(CPU, 메모리 등)는 **HANA\_Services\_Statistics**.

![SAP HANA 서비스 정보는 [HANA\_Services\_Statistics]. ](./media/troubleshooting-monitoring/image13-services-statistics.png)

**HANA\_구성\_개요\_Rev110 +** hello SAP HANA 인스턴스에 대 한 일반적인 정보입니다.

![HANA\_구성\_개요\_Rev110 + hello SAP HANA 인스턴스에 대 한 일반적인 정보](./media/troubleshooting-monitoring/image14-configuration-overview.png)

**HANA\_구성\_매개 변수\_Rev70 +** toocheck SAP HANA 매개 변수입니다.

![HANA\_구성\_매개 변수\_Rev70 + toocheck SAP HANA 매개 변수](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

