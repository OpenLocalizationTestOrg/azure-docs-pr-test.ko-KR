---
title: "Azure 로그 분석에서 성능 모니터 솔루션 aaaNetwork | Microsoft Docs"
description: "Azure 로그 분석에서 네트워크 성능 모니터를 사용 하면 네트워크 기능에 실시간 일회용 toodetect 근처의 hello 성능을 모니터링 하 고 네트워크 성능 병목 상태를 찾을 수 있습니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 5b9c9c83-3435-488c-b4f6-7653003ae18a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: e074948221fdd003c640861d759c4ce69ced1cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="network-performance-monitor-solution-in-log-analytics"></a>Log Analytics의 네트워크 성능 모니터 솔루션

![네트워크 성능 모니터 기호](./media/log-analytics-network-performance-monitor/npm-symbol.png)

이 문서에서는 tooset 및 사용 하 여 네트워크 기능에 실시간 일회용 toodetect 근처의 hello 성능을 모니터링 및 네트워크 성능 병목 상태를 찾을 수 있도록 로그 분석에서 네트워크 성능 모니터 솔루션 hello 방법을 설명 합니다. 네트워크 성능 모니터 솔루션 hello로 hello 손실 되 고 두 네트워크, 서브넷 또는 서버 간의 대기 시간을 모니터링할 수 있습니다. 네트워크 성능 모니터 트래픽 blackholing, 라우팅 오류 및 규칙에 따른 네트워크 모니터링 방법을 수 toodetect 없는 문제의 경우와 같은 네트워크 문제를 검색 합니다. 네트워크 성능 모니터는 네트워크 링크의 임계값이 위반될 때 경고와 알림을 표시합니다. 이러한 임계값 hello 시스템에 의해 자동으로 얻을 수 있습니다 또는 이러한 사용자 지정 경고 규칙 toouse를 구성할 수 있습니다. 네트워크 성능 모니터 네트워크 성능 문제를 시기 적절 한 통해 및 보여지는 hello 소스 hello 문제 tooa 특정 네트워크 세그먼트 또는 장치입니다.

최근 네트워크 상태 이벤트, 비정상 네트워크 링크 및 높은 패킷 손실 및 대기 시간에 직면 하는 서브 네트워크 링크를 비롯 하 여 네트워크에 대 한 요약된 정보를 표시 하는 hello 솔루션 대시보드 네트워크 문제를 검색할 수 있습니다. 있습니다 수로 드릴 다운 된 네트워크 링크 tooview hello 현재 상태도 서브 네트워크 링크 노드와 노드 링크. 연결 끊김 및 지연과 hello 네트워크, 서브 네트워크 및 노드와 노드 수준에서의 hello 기록 추세를 볼 수 있습니다. 패킷 손실 및 대기 시간에 대한 기존 추세 차트를 확인해서 일시적인 네트워크 문제를 감지하고 토폴로지 맵에서 네트워크 병목을 확인할 수 있습니다. hello 대화형 토폴로지 그래프 toovisualize hello 홉으로 네트워크 경로 허용 하 고 hello 문제의 hello 출처를 결정 합니다. 다른 솔루션에 같은 다양 한 분석에 대 한 로그 검색을 사용할 수 있습니다 요구 사항 toocreate 사용자 지정 보고서 네트워크 성능 모니터에 의해 수집 된 hello 데이터 기반으로 합니다.

hello 솔루션에는 기본 메커니즘 toodetect 네트워크 오류로 가상 트랜잭션을 사용합니다. 따라서 특정 네트워크 장치의 공급업체 또는 모델과 상관없이 사용할 수 있으며 온-프레미스, 클라우드(IaaS), 하이브리드 환경에서 작동합니다. hello 솔루션 hello 네트워크 토폴로지 및 네트워크의 다양 한 경로 자동으로 검색 합니다.

Hello 모니터링에서 모니터링 제품 포커스 일반적인 네트워크 장치 (예: 라우터, 스위치 등) 상태 네트워크 하지만 작업을 수행 하는 네트워크 성능 모니터 두 점 사이의 네트워크 연결의 실제 품질 hello에 대 한 정보를 제공 하지 않습니다.

### <a name="using-hello-solution-standalone"></a>Hello 솔루션 독립 실행형을 사용 하 여
Toomonitor hello 품질의 중요 한 워크 로드 간에 네트워크 연결을 원하는 경우 네트워크, 데이터 센터 또는 사이트를 사용할 수 있습니다 hello 네트워크 성능 모니터 솔루션 단독으로 사이의 toomonitor 연결 상태:

* 공용 또는 사설 네트워크를 사용하여 연결된 여러 데이터 센터 또는 지점 사이트 사이
* 기간 업무 애플리케이션을 실행하는 중요 워크로드 사이
* Microsoft Azure 또는 IaaS (VM) 사용할 수 있는 경우 게이트웨이 있으면 서비스 AWS (Amazon Web) 및 온-프레미스 네트워크와 같은 공용 클라우드 서비스는 온-프레미스 네트워크 및 클라우드 네트워크 간의 tooallow 통신 구성
* Express Route를 사용하는 경우 Azure 및 온-프레미스 네트워크

### <a name="using-hello-solution-with-other-networking-tools"></a>Hello 솔루션을 사용 하 여 다른 네트워킹 도구로
Toomonitor 비즈니스 응용 프로그램을 사용 하도록 하려는 경우에 도우미 솔루션 tooother 네트워크 도구와 hello 네트워크 성능 모니터 솔루션을 사용할 수 있습니다. 느린 네트워크 tooslow 응용 프로그램 및 네트워크 성능 모니터 수는 기본 네트워킹 문제로 인해 발생 하는 응용 프로그램 성능 문제를 조사할 수 있습니다. Hello 솔루션 액세스 toonetwork 장치에 필요 하지 않으면 때문에 응용 프로그램 관리자에 게 toorely hello 네트워크 응용 프로그램에 영향을 주지는 방법에 대 한 네트워킹 팀 tooprovide 정보에 필요 하지 않습니다.

또한 이미 다른 네트워크 모니터링 도구에에서 투자를 하는 경우 다음 hello 솔루션 보충할 수 있습니다 이러한 도구 대부분의 일반적인 네트워크 모니터링 솔루션 연결 끊김 및 지연과 같은 성능 메트릭이 종단 간 네트워크에 대 한 정보를 제공 하지 않기 때문입니다.  네트워크 성능 모니터 솔루션 hello 이러한 간격을 채울 수 있습니다.

## <a name="installing-and-configuring-agents-for-hello-solution"></a>Hello 솔루션에 대 한 에이전트 설치 및 구성
기본 프로세스 tooinstall 에이전트 hello를 사용 하 여 [연결 Windows 컴퓨터 tooLog 분석](log-analytics-windows-agents.md) 및 [Operations Manager 연결 tooLog 분석](log-analytics-om-agents.md)합니다.

> [!NOTE]
> 충분 한 데이터 toodiscover 순서 toohave의 2 개 이상 tooinstall 에이전트가 필요 하 고 네트워크 리소스를 모니터링 합니다. 그렇지 않은 경우 설치 하 고 추가 에이전트를 구성할 때까지 hello 솔루션 구성 상태로 유지 됩니다.
>
>

### <a name="where-tooinstall-hello-agents"></a>여기서 tooinstall hello 에이전트
에이전트를 설치 하기 전에 hello 네트워크의 토폴로지와 hello 부분 네트워크를 원하는 toomonitor 고려 합니다. 원하는 toomonitor 각 서브넷에 대해 둘 이상의 에이전트를 설치 하는 것이 좋습니다. 즉, toomonitor 지정 하는 모든 서브넷에 대해 두 개 이상의 서버 또는 Vm을 선택 하 고 hello 에이전트에 설치 합니다.

네트워크의 토폴로지 hello에 대 한 확실 하지 않은, toomonitor hello 네트워크 성능을 원하는 중요 한 워크 로드와 서버의 hello 에이전트를 설치 합니다. 예를 들어 웹 서버와 SQL Server를 실행 하는 서버 간의 네트워크 연결의 tookeep 트랙을 좋습니다. 이 예에서는 두 서버에 에이전트를 설치합니다.

에이전트는 hello 호스트 자체 하지 호스트 간의 네트워크 연결 (링크)를 모니터링합니다. 따라서 toomonitor 네트워크 링크를 해당 링크의 양 끝점 모두에 에이전트를 설치 해야 합니다.

### <a name="configure-agents"></a>에이전트 구성

가상 트랜잭션을 위해 toouse hello ICMP 프로토콜을 가져오려는 경우 tooenable hello 방화벽 규칙에 안정적으로 ICMP를 활용 하는 데 필요 합니다.

```
netsh advfirewall firewall add rule name="NPMDICMPV4Echo" protocol="icmpv4:8,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6Echo" protocol="icmpv6:128,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4DestinationUnreachable" protocol="icmpv4:3,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6DestinationUnreachable" protocol="icmpv6:1,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4TimeExceeded" protocol="icmpv4:11,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6TimeExceeded" protocol="icmpv6:3,any" dir=in action=allow
```


Toouse hello TCP 프로토콜을 가져오려는 경우 에이전트 통신할 수 있는 해당 컴퓨터 tooensure tooopen 방화벽 포트가 필요 합니다. 그러고 나 서 hello 및 toodownload 해야 [EnableRules.ps1 PowerShell 스크립트](https://gallery.technet.microsoft.com/OMS-Network-Performance-04a66634) 관리자 권한으로 PowerShell 창에서 매개 변수 없이 합니다.

hello 스크립트 hello 네트워크 성능 모니터에 필요한 레지스트리 키를 만듭니다 하 고 서로 상호 Windows 방화벽 규칙 tooallow 에이전트 toocreate TCP 연결을 만듭니다. hello 스크립트로 만든 hello 레지스트리 키 toolog hello 디버그 로그 및 hello 로그 파일에 대 한 hello 경로 여부를 지정할 수도 있습니다. 또한 통신에 사용 되는 hello 에이전트 TCP 포트를 정의 합니다. 이러한 키를 수동으로 변경 하지 않아야 하므로 이러한 키에 대 한 hello 값 hello 스크립트에 의해 자동으로 설정 됩니다.

기본적으로 연 hello 포트 8084입니다. 사용자 지정 포트를 사용 하 여 hello 매개 변수를 제공 하 여 `portNumber` toohello 스크립트입니다. 그러나 hello 동일한 포트 해야 컴퓨터에 사용할 모든 hello hello 스크립트가 실행 됩니다.

> [!NOTE]
> hello EnableRules.ps1 스크립트 hello 스크립트가 실행 되는 hello 컴퓨터 에서만 Windows 방화벽 규칙을 구성 합니다. 네트워크 방화벽을 사용 하는 경우 네트워크 성능 모니터에서 사용 하 고 hello TCP 포트에 대 한 전송 트래픽을 허용 하는지 확인 해야 합니다.
>
>

## <a name="configuring-hello-solution"></a>Hello 솔루션 구성
다음 정보 tooinstall hello를 사용 하 고 hello 솔루션을 구성 합니다.

1. Windows 7 SP1 또는 Windows Server 2008 SP 1 이상을 실행 하는 컴퓨터에서 데이터를 획득 하는 네트워크 성능 모니터 솔루션 hello 또는 이상 버전에서는 동일 환영 되는 Microsoft Monitoring Agent (MMA) hello 요구 사항이 있습니다. NPM 에이전트 또한 Windows 데스크톱/클라이언트 운영 체제(Windows 10, Windows 8.1, Windows 8 및 Windows 7)에서 실행할 수 있습니다.
    >[!NOTE]
    >Windows server 운영 체제에 대 한 hello 에이전트 가상 트랜잭션 hello 프로토콜로 TCP 및 ICMP를 모두를 지원합니다. 그러나 Windows 클라이언트 운영 체제에 대 한 hello 에이전트는 가상 트랜잭션 hello 프로토콜로 ICMP만 지원 했습니다.

2. Hello 네트워크 성능 모니터 솔루션 tooyour 작업 영역에서 추가 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.NetworkMonitoringOMS?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.  
   ![네트워크 성능 모니터 기호](./media/log-analytics-network-performance-monitor/npm-symbol.png)
3. Hello OMS 포털에서 이라는 새 타일이 표시 됩니다 **네트워크 성능 모니터** hello 메시지와 함께 *솔루션에 추가 구성이 필요*합니다. Tooconfigure hello 솔루션 tooadd 네트워크 에이전트에서 검색 되는 노드 및 하위 네트워크에 따라 필요 합니다. 클릭 **네트워크 성능 모니터** toostart hello 기본 네트워크를 구성 합니다.  
   ![solution requires additional configuration](./media/log-analytics-network-performance-monitor/npm-config.png)

### <a name="configure-hello-solution-with-a-default-network"></a>기본 네트워크와 hello 솔루션을 구성 합니다.
Hello 구성 페이지에서 명명 된 단일 네트워크를 확인할 수 있습니다 **기본**합니다. 모든 네트워크를 정의 하지 않은 모든 hello 자동으로 검색 서브넷 hello 기본 네트워크에 배치 됩니다.

네트워크를 만들 때마다 hello 기본 네트워크에서 서브넷 tooit 및 해당 서브넷은 제거 추가할 수 있습니다. 네트워크를 삭제 하면 모든 서브넷 toohello 기본 네트워크를 자동으로 반환 됩니다.

즉, hello 기본 네트워크는 모든 사용자 지정 네트워크에 포함 되지 않은 모든 hello 서브넷에 대 한 hello 컨테이너입니다. 편집 하거나 hello 기본 네트워크를 삭제할 수 없습니다. Hello 시스템에 항상 유지 됩니다. 하지만 네트워크는 필요한 만큼 만들 수 있습니다.

대부분의 경우에서 hello 서브넷 조직에서 하나 이상의 네트워크에 정렬 됩니다 하 하나 만들어야 또는 더 많은 네트워크 toologically 서브넷을 그룹화 합니다.

### <a name="create-new-networks"></a>새 네트워크 만들기
네트워크 성능 모니터의 네트워크는 서브넷의 컨테이너입니다. 원하는 toohello 네트워크 서브넷을 추가 하는 이름으로 네트워크를 만들 수 있습니다. 예를 들어 명명 된 네트워크를 만들 수 있습니다 *Building1* 다음 서브넷을 추가 하거나 명명 된 네트워크를 만들 수 *DMZ* toodemilitarized 영역 toothis 네트워크에 속한 모든 서브넷을 추가 합니다.

#### <a name="toocreate-a-new-network"></a>새 네트워크 toocreate
1. 클릭 **추가 네트워크** hello 네트워크 이름 및 설명을 입력 합니다.
2. 하나 이상의 서브넷을 선택한 다음 **Add**를 클릭합니다.
3. 클릭 **저장** toosave hello 구성 합니다.  
   ![네트워크 추가](./media/log-analytics-network-performance-monitor/npm-add-network.png)

### <a name="wait-for-data-aggregation"></a>데이터 집계 대기
처음으로 hello 구성, 저장 한 후 hello 솔루션 에이전트가 설치 된 hello 노드 간 네트워크 패킷 손실 및 대기 시간 정보를 수집을 시작 합니다. 이 프로세스는 많은 시간이 소요되며 30분 이상이 소요되는 경우도 있습니다. Hello 네트워크 성능 모니터 타일 hello 개요 페이지에서이 상태 라는 메시지를 표시 *프로세스에서 데이터 집계*합니다.

![데이터 집계 진행 중](./media/log-analytics-network-performance-monitor/npm-aggregation.png)

Hello 데이터 업로드 한 데이터를 네트워크 성능 모니터 타일을 업데이트할 보여 주는 하는 hello 표시 됩니다.

![네트워크 성능 모니터 타일](./media/log-analytics-network-performance-monitor/npm-tile.png)

Hello 타일 tooview hello 네트워크 성능 모니터 대시보드를 클릭 합니다.

![네트워크 성능 모니터 대시보드](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="edit-monitoring-settings-for-subnets"></a>서브넷의 모니터링 설정 편집
하나 이상의 에이전트가 설치 된 모든 서브넷 hello에 나열 된 **하위 네트워크** hello 구성 페이지에서 탭 합니다.

#### <a name="tooenable-or-disable-monitoring-for-particular-subnetworks"></a>tooenable 또는 특정 하위 네트워크에 대 한 모니터링 사용 안 함
1. 선택 또는 취소 hello 상자 다음 toohello **ID 서브 네트워크** 되어 있는지를 확인 하 고 **모니터링에 대 한 사용** 선택 또는 선택 취소 됨, 적절 하 게 됩니다. 여러 서브넷을 선택 또는 선택 취소할 수 있습니다. 해제 된 경우 하위 네트워크 hello 에이전트가 다른 에이전트 ping을 실행 하는 업데이트 된 toostop 있을 모니터링 되지 않습니다.
2. Hello 노드 되도록 toomonitor 특정 하위 네트워크에 대 한 hello 목록과 이동에서 hello 하위 네트워크를 선택 하 여 hello 방식으로 모니터링 하 고 모니터링 대상 노드를 포함 하는 hello 목록 간의 필요한 노드를 선택 합니다.
   사용자 지정을 추가할 수 있습니다 **설명** 서브, 원하는 경우 toohello 네트워크입니다.
3. 클릭 **저장** toosave hello 구성 합니다.  
   ![서브넷 편집](./media/log-analytics-network-performance-monitor/npm-edit-subnet.png)

### <a name="choose-nodes-toomonitor"></a>노드 toomonitor 선택
에이전트에 설치 되어 있는 모든 hello 노드 hello에 나열 됩니다 **노드** 탭 합니다.

#### <a name="tooenable-or-disable-monitoring-for-nodes"></a>tooenable 또는 노드에 대 한 모니터링을 비활성화
1. 선택 하거나 원하는 toomonitor 하거나 모니터링을 중지 하는 hello 노드 선택을 취소 합니다.
2. **Use for Monitoring**을 적절히 클릭하거나 선택 취소합니다.
3. **Save**를 클릭합니다.  
   ![노드 모니터링 사용](./media/log-analytics-network-performance-monitor/npm-enable-node-monitor.png)

### <a name="set-monitoring-rules"></a>모니터링 규칙 설정
네트워크 성능 모니터 노드 또는 하위 네트워크 또는 네트워크 링크는 임계값을 초과할 때 쌍 간의 hello 연결에 대 한 상태 이벤트를 생성 합니다. 이러한 임계값 hello 시스템에 의해 자동으로 얻을 수 있습니다 또는 이러한 사용자 지정 경고 규칙을 구성할 수 있습니다.

hello *기본 규칙* hello 시스템에서 만든 오류나 네트워크 또는 서브 네트워크 쌍 간의 대기 시간 위반 hello 시스템 학습 임계값 링크 때마다 상태 이벤트를 만듭니다. Toodisable hello 기본 규칙을 선택 하 고 사용자 지정 모니터링 규칙을 만들 수 있습니다.

#### <a name="toocreate-custom-monitoring-rules"></a>toocreate 모니터링 규칙 사용자 지정
1. 클릭 **규칙 추가** hello에 **모니터** 탭 하 고 hello 규칙 이름 및 설명을 입력 합니다.
2. Hello 목록에서 네트워크 또는 서브 네트워크 링크 toomonitor hello 쌍을 선택 합니다.
3. Hello 네트워크 드롭다운에서 관심 있는 첫 번째 하위 네트워크/s는 hello에 포함 되어 hello 네트워크를 선택한 다음 hello 해당 하위 네트워크 드롭다운에서 hello 서브 네트워크/s를 선택 합니다.
   선택 **모든 하위 네트워크** 서브 네트워크 링크의 hello 모든 toomonitor 하려는 경우. 마찬가지로 select hello 관심 있는 다른 하위 네트워크/s입니다. 클릭 수 및 **예외 추가** tooexclude hello 선택 영역에서 특정 서브 네트워크 링크에 대 한 모니터링 했습니다.
4. ICMP 및 TCP 프로토콜 중 가상 트랜잭션 실행에 사용할 프로토콜을 선택합니다.
5. 선택한 hello 항목에 대 한 상태 이벤트 toocreate 않으려는 경우 선택을 취소 합니다 **이 규칙에 의해 적용 하는 hello 링크에 대 한 상태 모니터링을 사용 하도록 설정**합니다.
6. 모니터링 조건을 선택합니다.
   임계값을 입력하여 상태 이벤트 생성에 대한 사용자 지정 임계값을 설정할 수 있습니다. Hello 조건의 hello 값 hello 선택한 네트워크/서브 네트워크 쌍에 대 한 선택 된 임계값을 넘으면 때마다 상태 이벤트 생성 됩니다.
7. 클릭 **저장** toosave hello 구성 합니다.  
   ![사용자 지정 모니터링 규칙 만들기](./media/log-analytics-network-performance-monitor/npm-monitor-rule.png)

모니터링 규칙을 저장한 후에는 **경고 만들기**를 클릭하여 규칙을 경고 관리와 통합할 수 있습니다. 경고 규칙 hello 검색 쿼리 및 기타 필수 만들어집니다 자동으로 매개 변수에서 자동으로 채워집니다. 경고 규칙을 사용 하 여 전자 메일 기반 경고를 받을 구성할 수 또한 NPM 내 경고 toohello 기존 수 있습니다. 경고를 통해 Runbook으로 수정 작업을 트리거하거나 웹후크를 사용하여 기존 서비스 관리 솔루션과 통합할 수 있습니다. 클릭할 수 있는 **관리 경고** tooedit hello에 대 한 경고 설정 합니다.

### <a name="choose-hello-right-protocol-icmp-or-tcp"></a>Hello 오른쪽 프로토콜 ICMP 또는 TCP를 선택 합니다.

네트워크 성능 모니터 (NPM) 패킷 손실 되 고 링크 대기 시간과 마찬가지로 가상 트랜잭션을 toocalculate 네트워크 성능 메트릭을 사용합니다. toounderstand이을 더 잘 고려 네트워크 링크의 NPM 에이전트 연결 된 tooone 종료 합니다. 이 NPM 에이전트 보냅니다 프로브 패킷 tooa 두 번째 NPM 에이전트 연결된 tooanother의 끝 hello 네트워크입니다. hello 두 번째 에이전트 회신 응답 패킷의 합니다. 이 프로세스는 몇 번 반복됩니다. 각 회신 hello 수가 회신 및 tooreceive에 걸린 시간을 측정 하 여 첫 번째 NPM 에이전트 hello 링크 대기 시간을 평가 하 고 패킷 삭제 합니다.

hello 형식, 크기 및 이러한 패킷 순서 따라 사용자가 모니터링 규칙을 만들 때 선택 하는 hello 프로토콜입니다. 중간 네트워크 장치 (예: 라우터, 스위치 등) hello hello 패킷에의 프로토콜에 따라,이 패킷을 다르게 처리할 수 있습니다. 따라서 프로토콜 선택 hello 결과의 hello 정확도를 영향을 줍니다. 및 프로토콜 선택 hello NPM 솔루션을 배포한 후 모든 수동 단계를 수행 해야 하는지 여부를 결정 합니다.

NPM 가상 트랜잭션을 실행 하기 위한 ICMP 및 TCP 프로토콜 중 하나를 선택 hello를 제공 합니다.
가상 트랜잭션 규칙을 만들 때 ICMP를 선택 하면 ICMP 에코 메시지 toocalculate hello 네트워크 대기 시간 및 패킷 손실이 hello NPM 에이전트 사용 합니다. Hello 규칙에 따른 Ping 유틸리티에서 ICMP 에코 사용 하 여 hello 동일한 메시지를 전송 합니다. Hello 프로토콜로 TCP를 사용할 때 NPM 에이전트 TCP SYN 패킷을 hello 네트워크를 통해 보냅니다. 그런 다음 TCP 핸드셰이크 완료 한 다음 RST 패킷을 사용 하 여 hello 연결을 제거 합니다.

#### <a name="points-tooconsider-before-choosing-hello-protocol"></a>포인트 tooconsider hello 프로토콜을 선택 하기 전에
Hello 프로토콜 toouse 선택 하기 전에 다음 정보를 고려 합니다.

##### <a name="discovering-multiple-network-routes"></a>여러 네트워크 경로 검색
TCP는 여러 경로 검색 시 보다 정확하며 각 서브넷에 필요한 에이전트 수가 더 적습니다. 예를 들어 TCP를 사용하는 하나 또는 두 개의 에이전트는 서브넷 간의 모든 중복 경로를 검색할 수 있습니다. 그러나 ICMP tooachieve 비슷한 결과 사용 하 여 여러 에이전트 해야 합니다. ICMP 사용 시 두 서브넷 간에 경로가 *N*개이면 원본 또는 대상 서브넷에 에이전트가 5*N*개 넘게 필요합니다.

##### <a name="accuracy-of-results"></a>결과의 정확성
라우터 및 스위치 tooassign 낮은 우선 순위 tooICMP 에코 패킷을 비교 tooTCP 패킷을 경향이 있습니다. 특정 상황에서 네트워크 장치 과도 하 게 로드 되는 경우 보다 긴밀 하 게 TCP 하 여 가져온 hello 데이터가 반영 hello 손실과 응용 프로그램의 대기 시간. 대부분의 응용 프로그램 트래픽이 hello TCP를 통해 이동 하므로 발생 합니다. 이러한 경우 ICMP 정확도 낮아집니다 비교 결과 tooTCP를 제공합니다.

##### <a name="firewall-configuration"></a>방화벽 구성
TCP 프로토콜 tooa 대상 포트 TCP 패킷 전송 되도록 요구 합니다. NPM 에이전트에서 사용 하는 hello 기본 포트는 8084, 에이전트를 구성 하는 경우이 변경할 수 있습니다. 따라서 해야 tooensure 네트워크 방화벽 또는 (Azure)에서 NSG 규칙 hello 포트에서 트래픽을 허용 됩니다. 또한 toomake 해야 해당 hello 로컬 컴퓨터 방화벽에 hello 에이전트가 설치 되어 구성 되어 있어야이 포트에서 트래픽을 tooallow 합니다.

사용할 수 있습니다 PowerShell 스크립트 tooconfigure 방화벽 규칙 Windows를 실행 하는 컴퓨터 tooconfigure 필요한 네트워크 방화벽 수동으로 합니다.

반면에 ICMP는 포트를 사용하여 운영되지 않습니다. 대부분의 엔터프라이즈 시나리오에서 hello 방화벽 tooallow toouse 네트워크 진단 도구 하 시겠습니까? hello Ping 유틸리티를 통해 ICMP 트래픽이 허용 됩니다. 따라서 다른 한 컴퓨터에서를 ping 할 수 없으면 사용할 수 있습니다 hello ICMP 프로토콜 tooconfigure 방화벽을 수동으로 필요 없이 합니다.

> [!NOTE]
> 어떤 프로토콜 toouse 해야 할지 잘 모를 경우 ICMP toostart를 선택 합니다. Hello 결과 만족 하지 않는 경우 나중에 tooTCP를 전환할 항상 있습니다.


#### <a name="how-tooswitch-hello-protocol"></a>Tooswitch 프로토콜 hello 하는 방법

배포 하는 동안 toouse ICMP를 선택한 경우에 hello 기본 모니터링 규칙을 편집 하 여 언제 든 지 tooTCP를 전환할 수 있습니다.

##### <a name="tooedit-hello-default-monitoring-rule"></a>tooedit hello 기본 모니터링 규칙
1.  너무 이동**네트워크 성능을** > **모니터** > **구성** > **모니터** 클릭 하 고 **기본 규칙**합니다.
2.  Toohello 스크롤하여 **프로토콜** 섹션 및 toouse hello 프로토콜을 선택 합니다.
3.  클릭 **저장** tooapply hello 설정 합니다.

Hello 기본 규칙이 특정 프로토콜을 사용 하는 경우에 서로 다른 프로토콜을 사용한 새 규칙을 만들 수 있습니다. ICMP를 사용 하 여 hello 규칙 중 일부 다른 TCP를 사용 하는 규칙을 혼합 하 여 만들 수 있습니다.




## <a name="data-collection-details"></a>데이터 수집 세부 정보
Hello 프로토콜 toocollect 손실 및 대기 시간 정보로 ICMP를 선택 하면 선택한 및 ICMP 에코 ICMP 에코 응답 TCP는 경우 TCP SYN SYNACK ACK 핸드셰이크 패킷을 사용 하는 네트워크 성능 모니터입니다. Traceroute는 토폴로지 정보를 사용 하는 tooget 이기도합니다.

hello 다음 표에서 데이터 수집 방법과 및 네트워크 성능 모니터에 대 한 데이터 수집 방법에 대 한 기타 세부 정보.

| 플랫폼 | 직접 에이전트 | SCOM 에이전트 | Azure 저장소 | SCOM 필요? | 관리 그룹을 통해 전송되는 SCOM 에이전트 데이터 | 수집 빈도 |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  |  |TCP는 5초마다 핸드셰이크/ICMP ECHO 메시지를 전송하며 3분마다 데이터가 전송됩니다. |

hello 솔루션 hello 네트워크의 가상 트랜잭션을 tooassess hello 상태를 사용합니다. 서로 (프로토콜에 따라 hello 모니터링 용으로 선택) hello 네트워크 exchange TCP 패킷 또는 ICMP 에코의 다양 한 지점에서 설치 된 OMS 에이전트입니다. Hello 프로세스 에이전트 있는 경우 hello 왕복 시간 및 패킷 손실에 설명 합니다. 정기적으로 각 에이전트를 테스트 해야 하는 hello 네트워크에서 다양 한 경로 hello 모든 추적 경로 tooother 에이전트 toofind를 수행 합니다. 이 데이터를 사용 하 여 hello 에이전트 hello 네트워크 대기 시간, 패킷 손실 숫자를 추론할 수 있습니다. 5 초 마다 및 데이터 3 분 기간에 대 한 하 여 집계 됩니다 hello 에이전트 toohello 로그 분석 서비스를 업로드 하기 전에 hello 테스트 반복 됩니다.

> [!NOTE]
> 통신할 수 있지만 에이전트 서로 자주를 생성 하지 않기 많은 네트워크 트래픽 hello 테스트를 수행 하는 중입니다. 에이전트는 TCP SYN SYNACK ACK 핸드셰이크 패킷 toodetermine hello 손실 및 대기 시간-패킷 교환 되는 데이터가 없는 경우에 의존 합니다. 이 과정에서 에이전트와 필요한 경우에 서로 통신 하 고 hello 에이전트 통신 토폴로지에 최적화 되어 tooreduce 네트워크 트래픽이 있습니다.
>
>

## <a name="using-hello-solution"></a>Hello 솔루션을 사용 하 여
이 섹션에서는 모든 hello 대시보드 기능을 설명 및 방법을 toouse 해당 합니다.

### <a name="solution-overview-tile"></a>솔루션 개요 타일
Hello 네트워크 성능 모니터 솔루션을 설정한 후 hello 솔루션 타일 hello OMS 개요 페이지에서 hello 네트워크 상태가의 간략 한 개요를 제공 합니다. Hello 수가 정상 및 비정상 서브 네트워크 링크를 표시 하는 도넛형 차트를 표시 합니다. Hello 타일을 클릭할 때 hello 솔루션 대시보드가 열립니다.

![네트워크 성능 모니터 타일](./media/log-analytics-network-performance-monitor/npm-tile.png)

### <a name="network-performance-monitor-solution-dashboard"></a>네트워크 성능 모니터 솔루션 대시보드
hello **네트워크 요약** 블레이드 hello 네트워크의 상대 크기의 요약 정보를 표시 합니다. Hello 시스템 (경로 hello IP 주소로 이루어진 에이전트와 함께 두 명의 호스트 및 모든 hello 홉 사이)의 경로 서브넷 링크를 사용 하는, 네트워크 링크의 총 수를 보여 주는 타일 나옵니다.

hello **상위 네트워크 상태 이벤트가** 블레이드 hello 이벤트 활성화 된 이후 hello 시스템과 hello 시간에 가장 최근 상태 이벤트 및 경고의 목록을 제공 합니다. 상태 이벤트 나 경고는 hello 패킷 손실이 나 네트워크 또는 서브 네트워크 링크의 대기 시간 임계값을 초과할 때마다 생성 됩니다.

hello **Top 비정상 네트워크 링크** 블레이드 비정상 네트워크 링크의 목록을 표시 합니다. 이들은 하나 이상의 부정적인 상태 이벤트에 대 한 해당 hello 순간에 hello 네트워크 링크입니다.

hello **손실 가장 위쪽 서브 네트워크 링크** 및 **가장 대기 시간으로 서브 네트워크 링크** 블레이드 패킷 손실 hello 상위 서브 네트워크 링크를 표시 하 고 각각의 대기 시간으로 서브 네트워크 링크를 위에서 합니다. 특정 네트워크 링크는 대기 시간 또는 패킷 손실량이 높은 상태가 정상일 수 있습니다. 이러한 링크 hello 상위 10 개 목록에 나타나지만 비정상으로 표시 되지 않습니다.

hello **일반적인 쿼리** 블레이드를 원시 네트워크 직접 모니터링 데이터를 페치하는 검색 쿼리 집합을 포함 합니다. 이러한 쿼리를 시작점으로 사용하여 사용자 지정 보고를 위한 쿼리를 만들 수 있습니다.

![네트워크 성능 모니터 대시보드](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="drill-down-for-depth"></a>상세하게 드릴다운
관심 있는 영역으로 hello 솔루션 대시보드 toodrill 다운 하위 수준에 대 한 다양 한 링크를 클릭할 수 있습니다. 예를 들어, 경고 또는 hello 대시보드에 표시 되는 비정상 네트워크 링크를 보면 클릭할 수 있는 것 tooinvestigate 추가 합니다. Hello 특정 네트워크 링크에 대 한 모든 hello 서브 네트워크 링크를 나열 된 tooa 페이지를 이동 하 고 합니다. 각 서브 네트워크 링크의 수 toosee hello 손실, 대기 시간 및 상태 상태 고 서브 네트워크 링크에 대해 알아봅니다 hello 문제를 유발 하는 신속 하 게 있습니다. 클릭 수 **노드 링크를 보려면** toosee hello 비정상 서브넷에 대 한 모든 hello 노드 링크 연결 합니다. 그런 다음 개별 노드 링크를 보고 hello 비정상 노드 링크를 찾을 수 있습니다.

클릭할 수 있는 **보기 토폴로지** tooview hello 홉으로 토폴로지 hello 소스 노드와 대상 노드 간의 hello 경로입니다. 비정상 경로 hello 또는 hello 문제 tooa hello 네트워크의 특정 부분을 신속 하 게 식별할 수 있도록 홉 빨간색으로 표시 됩니다.

![드릴다운 데이터](./media/log-analytics-network-performance-monitor/npm-drill.png)

### <a name="network-state-recorder"></a>네트워크 상태 레코더

각 보기에는 특정 시점에서 네트워크 상태에 대한 스냅숏이 표시됩니다. 기본적으로 hello 가장 최근 상태 표시 됩니다. hello hello 페이지 위쪽에 hello 막대 hello 상태 표시 되는 시간에 hello 지점을 표시 합니다. Hello 막대에서 클릭 하 여 네트워크 상태가의 hello 스냅샷 시간과 보기에 다시 toogo를 선택할 수 있습니다 **동작**합니다. 또한 hello 최신 상태를 보는 동안 모든 페이지에 대 한 자동 새로 고침을 사용 하지 않도록 설정 하거나 tooenable 선택할 수 있습니다.

![네트워크 상태](./media/log-analytics-network-performance-monitor/network-state.png)

#### <a name="trend-charts"></a>추세 차트
각 수준을 드릴 다운 손실 및 대기 시간 네트워크 링크의 hello 추세를 볼 수 있습니다. 추세 차트는 서브네트워크 또는 노드 링크에도 사용할 수 있습니다. Hello 차트의 hello 위쪽 hello 타임 컨트롤을 사용 하 여 그래프 tooplot hello에 대 한 hello 시간 간격을 변경할 수 있습니다.

추세 차트는 기록 네트워크 링크의 hello 성능 측면을 보여 줍니다. 일부 네트워크 문제는 일시적인와 유사 하드 toocatch hello hello 네트워크의 현재 상태를 확인 합니다. 문제에서 신속 하 게 노출 하 고 사실이 발견 되기만 tooreappear 나중 시점에, 전에 사라질 수 때문입니다. 응용 프로그램 응답 시간, 모든 응용 프로그램 구성 요소 toorun를 원활 하 게 표시 하는 경우에 설명할 수 없는 증가 함에 따라 종종 화면을 발급 하는 것 때문에도 이러한 일시적인 문제가 응용 프로그램 관리자에 대 한 어려울 수 있습니다.

네트워크 대기 시간 또는 패킷 손실이 급증으로 hello 문제가 표시 되는 위치 추세 차트를 보면 이러한 종류의 문제를 쉽게 검색할 수 있습니다.

![추세 차트](./media/log-analytics-network-performance-monitor/npm-trend.png)

#### <a name="hop-by-hop-topology-map"></a>홉 단위 토폴로지 맵
네트워크 대화형 토폴로지 맵의에서 두 노드 간의 경로 홉으로 토폴로지 hello 성능 모니터 보여 줍니다. 노드 링크를 선택 하 고 다음을 클릭 하 여 hello 토폴로지 맵의 볼 수 있습니다 **보기 토폴로지**합니다. 클릭 하 여 hello 토폴로지 맵의 볼 수는 또한 **경로** hello 대시보드에서 타일을 합니다. 클릭할 때 **경로** hello 대시보드에서 tooselect hello 왼쪽 패널에서 원본 및 대상 노드 hello 및 클릭 해야 합니다. **그릴** hello 두 노드 간 tooplot hello 경로입니다.

hello 토폴로지 맵의 개수는 경로 hello 간에 두 개 노드가 및 어떤 경로 hello 패킷을 사용 하는 데이터를 표시 합니다. 네트워크 성능 병목 현상은 hello 토폴로지 지도에 빨간색으로 표시 됩니다. Hello 토폴로지 맵의에서 빨간 색이 지정 된 요소를 확인 하 여 잘못 된 네트워크 연결 또는 잘못 된 네트워크 장치를 찾을 수 있습니다.

클릭할 때 노드 또는 가리키기 올려 hello 토폴로지 맵의 FQDN 및 IP 주소 처럼 hello 노드의 hello 속성이 표시 됩니다. IP 주소가 홉 toosee를 클릭 합니다. Hello 축소할 수 있는 작업 창에서 hello 필터를 사용 하 여 toofilter 특정 경로 선택할 수 있습니다. 및 hello 중간 홉 hello 슬라이더를 사용 하 여 hello 작업 창에서 숨기는 방식으로 hello 네트워크 토폴로지를 단순화할 수도 있습니다. 있습니다 수 확대/축소 또는 hello 토폴로지 맵의 마우스 휠을 사용 하 여 합니다.

Note hello 지도에 표시 된 해당 hello 토폴로지는 3 계층 토폴로지 및 계층 2 장치 및 연결을 포함 하지 않습니다.

![홉 단위 토폴로지 맵](./media/log-analytics-network-performance-monitor/npm-topology.png)

#### <a name="fault-localization"></a>오류 있는 지역화
네트워크 성능 모니터는 toohello 네트워크 장치를 연결 하지 않고도 수 toofind hello 네트워크 병목 상태입니다. 네트워크 성능 모니터는 hello 네트워크와 네트워크 그래프 hello에 고급 알고리즘을 적용 하 여 수집한 hello 데이터에 따라 hello 부분 네트워크에 hello 문제의 가장 가능성이 높은 hello 출처를 확률적 예측할을 만듭니다.

이 방법은 유용 toodetermine hello 네트워크 병목 현상을 액세스 toohops 라우터 또는 스위치 같은 hello 네트워크 장치에서 수집 된 모든 데이터 toobe 필요 하지 않으므로 사용할 수 없는 경우. 이 경우도 유용 hello 홉 두 노드 사이 관리 제어에 있지 않습니다. 예를 들어 hello 홉 ISP 라우터를 수 있습니다.

### <a name="log-analytics-search"></a>Log Analytics 검색
그래픽으로 hello 네트워크 성능 모니터 대시보드 및 드릴 다운 페이지를 통해 노출 되는 모든 데이터도 기본적으로 로그 분석 검색에 제공 됩니다. Hello 검색 쿼리 언어를 사용 하 여 hello 데이터를 쿼리하고 데이터 tooExcel hello 또는 PowerBI를 내보내 사용자 지정 보고서를 만들 수 있습니다. hello **일반적인 쿼리** hello 대시보드에 블레이드는 쿼리와 보고서를 만들기 위한 시작점 hello로 사용할 수 있는 몇 가지 유용한 쿼리 합니다.

![검색 쿼리](./media/log-analytics-network-performance-monitor/npm-queries.png)

## <a name="investigate-hello-root-cause-of-a-health-alert"></a>상태 경고의 hello 근본 원인을 조사합니다
네트워크 성능 모니터에 대 한 참고 했으므로 상태 이벤트에 대 한 hello 근본 원인에 대 한 간단한 조사에서 살펴보겠습니다.

1. Hello 개요 페이지에서 얻게 됩니다 네트워크의 hello 상태의 빠른 스냅숏을 hello 관찰 하 여 **네트워크 성능 모니터** 바둑판식으로 배열입니다. Hello 6 개에서 모니터링 되 고 연결 된 공지, 2 정상 상태가 아닌 합니다. 이 경우 조사가 필요합니다. Hello 타일 tooview hello 솔루션 대시보드를 클릭 합니다.  
   ![네트워크 성능 모니터 타일](./media/log-analytics-network-performance-monitor/npm-investigation01.png)
2. Hello 예제 이미지 아래에 있다는 것 상태 이벤트 비정상 네트워크 링크를 확인할 수 있습니다. Tooinvestigate hello 문제를 결정 하 고 hello 클릭 **DMZ2 DMZ1** 네트워크 링크 toofind hello 문제의 hello 루트 아웃 합니다.  
   ![비정상 네트워크 링크 예](./media/log-analytics-network-performance-monitor/npm-investigation02.png)
3. hello 드릴 다운 페이지에 있는 모든 hello 서브 네트워크 링크 표시 **DMZ2 DMZ1** 네트워크 링크 합니다. 두 hello 서브 네트워크 링크에 대 한 hello 대기 시간 초과 했음을 hello 네트워크 링크를 비정상적으로 만드는 hello 임계값을 확인할 수 있습니다. 두 hello 서브 네트워크 링크의 hello 대기 시간 추세를 볼 수 있습니다. Hello 시간 선택 컨트롤 hello 그래프 toofocus에서 hello에 필요한 시간 범위를 사용할 수 있습니다. Hello 시간 피크 대기 시간에 도달한 경우 hello 볼 수 있습니다. 나중에이 시간 기간 tooinvestigate hello 문제에 대 한 hello 로그를 검색할 수 있습니다. 클릭 **노드 링크를 보려면** toodrill 다운 추가 합니다.  
   ![비정상 서브넷 링크 예](./media/log-analytics-network-performance-monitor/npm-investigation03.png)
4. 비슷한 toohello 이전 페이지 hello 특정 서브 네트워크 링크에 대 한 hello 드릴 다운 페이지의 구성 요소 노드 링크 다운 나열 됩니다. 비슷한 작업을 수행할 수 hello 이전 단계에서 수행한 것 처럼 여기 합니다. 클릭 **보기 토폴로지** hello 2 노드 간에 tooview hello 토폴로지입니다.  
   ![비정상 노드 링크 예](./media/log-analytics-network-performance-monitor/npm-investigation04.png)
5. 선택한 hello 2 노드 간의 모든 hello 경로 토폴로지 맵의 hello 표시 됩니다. Hello 토폴로지 맵의에서 두 노드 간의 경로 hello 홉 여 토폴로지를 시각화할 수 있습니다. 어떤 경로 hello 데이터 패킷의 수행 하는 간격과 hello 두 노드 간에 몇 개입니까 경로가 명확 하 게 파악할 생깁니다. 네트워크 성능 병목은 빨간색으로 표시되어 있습니다. Hello 토폴로지 맵의에서 빨간 색이 지정 된 요소를 확인 하 여 잘못 된 네트워크 연결 또는 잘못 된 네트워크 장치를 찾을 수 있습니다.  
   ![비정상 토폴로지 보기 예](./media/log-analytics-network-performance-monitor/npm-investigation05.png)
6. hello 손실, 대기 시간 및 각 경로에 홉 수가 hello hello에서 검토할 수 있습니다 **동작** 창. 이러한 비정상적인 경로의 hello scrollbar tooview hello 정보를 사용 하 여 합니다.  사용 하 여 hello 필터 tooselect hello 경로 hello 비정상 홉만 hello에 대 한 hello 토폴로지 경로 선택 되도록 표시 됩니다. 마우스 휠 toozoom 또는 hello 토폴로지 맵의 축소를 사용할 수 있습니다.

   Hello 이미지 아래에 명확 하 게 보일 hello 경로 및 빨간색에서 홉 확인 하 여 hello 문제 영역 toohello의 특정 섹션 hello 네트워크의 근본 원인을 hello 합니다. Hello 토폴로지 맵에서 노드를 클릭 하면 hello, FQDN 및 IP 주소를 포함 하 여 hello 노드의 hello 속성 표시 합니다. 홉을 클릭 하면 hello 홉의 IP 주소 hello를 표시 합니다.  
   ![비정상 토폴로지 - 패스 세부 정보 예](./media/log-analytics-network-performance-monitor/npm-investigation06.png)

## <a name="provide-feedback"></a>피드백 제공

- **UserVoice** -네트워크 성능 모니터는 us toowork에서 원하는 기능에 대 한 아이디어를 게시할 수 있습니다. [UserVoice 페이지](https://feedback.azure.com/forums/267889-log-analytics/category/188146-network-monitoring)를 방문하세요.
- **코호트 조인** - 코호트에 조인하는 새 고객을 항상 환영합니다. 일부로, 초기에 이용해 toonew 기능 하 고 네트워크 성능 모니터를 개선할 수 있도록 합니다. 조인에 관심이 있을 경우 이 [빠른 설문 조사](https://aka.ms/npmcohort)에 참여하세요.

## <a name="next-steps"></a>다음 단계
* [로그 검색](log-analytics-log-searches.md) tooview 네트워크 성능 데이터 레코드를 자세히 설명 합니다.
