---
title: "Azure에서 서비스 aaaUsing 부하 분산 | Microsoft Docs"
description: "이 자습서에서는 방법을 사용 하 여 시나리오 toocreate hello Azure 부하 분산 포트폴리오: 트래픽 관리자, 응용 프로그램 게이트웨이 및 부하 분산 장치입니다."
services: traffic-manager
documentationcenter: 
author: liumichelle
manager: vitinnan
editor: 
ms.assetid: f89be3be-a16f-4d47-bcae-db2ab72ade17
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/27/2016
ms.author: limichel
ms.openlocfilehash: d217047102d8c4828250dc0733e8ec9ee1e84b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-load-balancing-services-in-azure"></a>Azure에서 부하 분산 서비스 사용

## <a name="introduction"></a>소개

Microsoft Azure는 네트워크 트래픽을 분산하고 부하를 분산하는 방법을 관리하는 여러 서비스를 제공합니다. 이러한 서비스를 개별적으로 사용 하거나 toobuild hello 최적의 솔루션 요구 사항에 따라 자신의 방법을 결합할 수 있습니다.

이 자습서에서는 먼저 고객이 사용 사례를 정의 하 고 다음 Azure 부하 분산 포트폴리오 hello를 사용 하 여 방법으로 설정할 수 있는 보다 강력한 및 고성능을 참조 하십시오: 트래픽 관리자, 응용 프로그램 게이트웨이 및 부하 분산 장치입니다. 그런 다음 각기 다른 유형의 요청을 관리 하는 지리적으로 중복, 트래픽 tooVMs 배포 및는 사용 하면 배포를 만들기 위한 단계별 지침 제공 합니다.

개념 수준에서 이러한 각 서비스에서에서 역할을 고유 hello 계층 부하 분산 합니다.

* **Traffic Manager**는 전역 DNS 부하 분산을 제공 합니다. 들어오는 DNS 요청 확인 하 고 정상 상태의 끝점을 사용 하 여 응답으로 hello에 따라 라우팅 정책 hello 고객이 선택 됩니다. 라우팅 메서드의 옵션은 다음과 같습니다.
  * 성능 라우팅 toosend hello 요청자 toohello 가장 가까운 끝점 지연 시간의 측면에서입니다.
  * 우선 순위 라우팅 toodirect 백업으로 다른 끝점과 모든 트래픽 tooan 끝점입니다.
  * 가중치가 적용 된 라운드 로빈 라우팅, tooeach 끝점 할당 된 hello 가중치에 따라 트래픽을 분산입니다.

  클라이언트 hello toothat 끝점 직접 연결 합니다. Azure 트래픽 관리자 끝점 손상 되었습니다. 하 고 다음 리디렉션을 hello 클라이언트 tooanother 정상 인스턴스를 검색 합니다. 너무 참조[Azure 트래픽 관리자 설명서](traffic-manager-overview.md) toolearn hello 서비스에 대 한 자세한 합니다.
* **Application Gateway**는 ADC(응용 프로그램 전달 컨트롤러)를 서비스로 제공하여 응용 프로그램에 대한 다양한 Layer 7 부하 분산 기능을 제공합니다. 이 통해 고객 toooptimize 웹 팜 생산성 CPU를 많이 사용 SSL 종료 toohello 응용 프로그램 게이트웨이 오프 로드 합니다. 다른 계층 7 라우팅 기능 들어오는 트래픽을, 쿠키 기반 세션 선호도, URL 경로 기반 라우팅 및 hello 기능 toohost 라운드 로빈 배포는 단일 응용 프로그램 게이트웨이 뒤에 있는 여러 웹 사이트를 포함 합니다. Application Gateway는 인터넷 연결 게이트웨이, 내부 전용 게이트웨이 또는 둘의 조합으로 구성될 수 있습니다. Application Gateway는 전적으로 Azure에 의해 관리되고, 확장성 및 고가용성을 제공합니다. 관리 효율성을 향상시키기 위한 풍부한 진단 및 로깅 기능을 제공합니다.
* **부하 분산 장치** 고성능의 대기 시간이 짧은 계층 4 부하 분산 서비스 제공 모든 UDP 및 TCP 프로토콜에 대 한 hello Azure SDN 스택의 필수적인 부분입니다. 인바운드 및 아웃 바운드 연결을 관리합니다. Public 및 내부 부하 분산 된 끝점을 구성 하 고 규칙 toomap 정의할 수 있습니다 연결 tooback 엔드 풀 대상 TCP 및 HTTP 상태 검색 옵션 toomanage 서비스 가용성을 사용 하 여 인바운드 합니다.

## <a name="scenario"></a>시나리오

이 예제 시나리오에서는 두 가지 유형의 콘텐츠와 동적으로 렌더링 되는 웹 페이지를 제공하는 간단한 웹 사이트를 사용합니다. hello 웹 사이트는 지리적으로 중복 이어야 하며 사용자 들이 hello 가장 가까운 (가장 낮은 대기 시간)을 제공 해야 위치 toothem 합니다. hello 응용 프로그램 개발자가 결정는 일치 하는 모든 Url hello 패턴/이미지 / * hello hello 웹 팜의 나머지와에서 다른 Vm의 전용된 풀에서 제공 됩니다.

또한 hello 동적 콘텐츠를 서비스 하는 hello 기본 VM 풀이 tootalk tooa 백 엔드 데이터베이스는 고가용성 클러스터에서 호스트 되는 필요 합니다. hello 전체 배포 Azure 리소스 관리자를 통해 설정 됩니다.

트래픽 관리자, 응용 프로그램 게이트웨이 및 부하 분산 장치를 사용 하 여 사용 하면이 웹 사이트 tooachieve 이러한 목표를 디자인 합니다.

* **다중 지리적 중복성**: 하나의 영역 다운 되 면 트래픽 관리자 경로 트래픽 hello 응용 프로그램 소유자의 도움 없이 toohello 가장 가까운 지역 원활 하 게 합니다.
* **지연 시간이 단축**: hello 웹 페이지 콘텐츠를 요청할 때 hello 사용자 환경과 더 낮은 대기 시간, 때문에 트래픽 관리자는 자동으로 hello 고객 toohello 가장 가까운 지역을 지정 합니다.
* **독립 확장성**: hello 웹 응용 프로그램 작업 부하로 콘텐츠 유형의 구분 때문에 hello 응용 프로그램 소유자 hello 요청 작업을 서로 독립적으로 확장할 수 있습니다. 응용 프로그램 게이트웨이 사용 하면 hello 트래픽을 지정 된 hello를 바탕으로 라우트된 toohello 오른쪽 풀 규칙 및 hello 응용 프로그램의 hello 상태입니다.
* **내부 부하 분산**: 때문에 부하 분산 장치 hello 고가용성 클러스터 앞에 사용할 수 있는 데이터베이스에 대 한 hello 활성 상태이 고 정상 상태의 끝점을 노출 된 toohello 응용 프로그램입니다. 또한 데이터베이스 관리자는 활성 노드와 수동 복제본 hello 클러스터 독립적 hello 프런트 엔드 응용 프로그램으로 배포 하 여 hello 작업을 최적화할 수 있습니다. 부하 분산 장치 연결 toohello 고가용성 클러스터를 제공 하 고 정상 상태의 데이터베이스에만 연결 요청을 받이 되도록 합니다.

hello 다음 그림에이 시나리오의 hello 아키텍처:

![부하 분산 아키텍처의 다이어그램](./media/traffic-manager-load-balancing-azure/scenario-diagram.png)

> [!NOTE]
> 이 예제에서는 Azure에서 제공 하는 hello 부하 분산 서비스의 구성이 다양 중 하나일 뿐입니다. 트래픽 관리자, 응용 프로그램 게이트웨이 및 부하 분산 장치를 혼합 될 수와 일치 하는 toobest 부하 분산 요구에 맞게 합니다. 예를 들어, SSL 오프 로드 또는 Layer 7 처리가 필요 없는 경우 부하 분산 장치 Application Gateway 대신에 Load Balancer를 사용할 수 있습니다.

## <a name="setting-up-hello-load-balancing-stack"></a>부하 분산 스택 hello 설정

### <a name="step-1-create-a-traffic-manager-profile"></a>1단계: Traffic Manager 프로필 만들기

1. Hello Azure 포털에서에서 클릭 **새로**, 및 "트래픽 관리자 프로필."에 대 한 hello marketplace 다음 검색
2. Hello에 **만들 트래픽 관리자 프로필** 블레이드에서 hello 다음 기본 정보를 입력 합니다.

  * **이름**: Traffic Manager 프로필에 DNS 접두사 이름을 지정합니다.
  * **라우팅 방법**: 선택 hello 트래픽 라우팅 방법 정책입니다. Hello 방법에 대 한 자세한 내용은 참조 [트래픽 관리자에 대 한 트래픽 라우팅 방법](traffic-manager-routing-methods.md)합니다.
  * **구독**: hello 프로필을 포함 하는 hello 구독을 선택 합니다.
  * **리소스 그룹**: hello 프로필이 포함 된 Select hello 리소스 그룹입니다. 새 리소스 그룹이나 기존 리소스 그룹을 선택할 수 있습니다.
  * **리소스 그룹 위치**: 트래픽 관리자 서비스가 전역 이며 바인딩되지 않았습니다 tooa 위치가 있습니다. 그러나 hello 트래픽 관리자 프로필에 연결 된 hello 메타 데이터가 있는 hello 그룹에 대 한 영역을 지정 해야 합니다. 이 위치는 hello 프로필의 hello 런타임 가용성에 영향을 주어에 있습니다.

3. 클릭 **만들기** toogenerate hello 트래픽 관리자 프로필.

  !["Traffic Manager 만들기" 블레이드](./media/traffic-manager-load-balancing-azure/s1-create-tm-blade.png)

### <a name="step-2-create-hello-application-gateways"></a>2 단계: hello 응용 프로그램 게이트웨이 만들기

1. Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 **새로** > **네트워킹** > **응용 프로그램 게이트웨이**합니다.
2. Hello 다음 응용 프로그램 게이트웨이 hello에 대 한 기본 정보를 입력 합니다.

  * **이름**: hello hello 응용 프로그램 게이트웨이의 이름입니다.
  * **SKU 크기**: hello 크기의 hello 응용 프로그램 게이트웨이 소형, 중형 또는 대형으로 사용할 수 있습니다.
  * **인스턴스 수를**: hello 인스턴스 수, 2에서 10 사이의 값입니다.
  * **리소스 그룹**: hello 응용 프로그램 게이트웨이 포함 하는 hello 리소스 그룹입니다. 기존 리소스 그룹이나 새 리소스 그룹을 선택할 수 있습니다.
  * **위치**: 동일 hello는 응용 프로그램 게이트웨이 hello에 대 한 hello 영역 hello 리소스 그룹 위치입니다. hello 위치는 hello 가상 네트워크와 공용 IP hello에 있어야 하기 때문에, 중요 한 hello 게이트웨이와 동일한 위치입니다.
3. **확인**을 클릭합니다.
4. Hello 가상 네트워크, 서브넷, 프런트 엔드 IP 및 응용 프로그램 게이트웨이 hello에 대 한 수신기 구성을 정의 합니다. 이 시나리오에서는 hello 프런트 엔드 IP 주소는 **공용**, toobe 끝점 toohello 트래픽 관리자 프로필으로 나중에 추가할 수 있는 합니다.
5. Hello 다음 옵션 중 하나가 지정 된 hello 수신기를 구성 합니다.
    * 없는 경우 HTTP를 사용 하면 tooconfigure 합니다. **확인**을 클릭합니다.
    * HTTPS를 사용하는 경우 추가 구성이 필요합니다. 너무 참조[응용 프로그램 게이트웨이 만들](../application-gateway/application-gateway-create-gateway-portal.md)9 단계에서 시작 합니다. Hello 구성을 완료 한 클릭 **확인**합니다.

#### <a name="configure-url-routing-for-application-gateways"></a>Application Gateway에 대한 URL 라우팅 구성

백 엔드 풀을 선택 하면 경로 기반 규칙으로 구성 된 응용 프로그램 게이트웨이 더하기 tooround 로빈 배포에서 hello 요청 URL의 경로 패턴을 가져옵니다. 이 시나리오에서는 추가 하 고 경로 기반 규칙 toodirect와 모든 URL "/images/\*" toohello 이미지 서버 풀입니다. URL을 구성 하는 방법에 대 한 자세한 내용은 응용 프로그램 게이트웨이 대 한 라우팅 경로 기반 참조 너무[응용 프로그램 게이트웨이 대 한 기준으로 경로 규칙을 만들](../application-gateway/application-gateway-create-url-route-portal.md)합니다.

![Application Gateway 웹 계층 다이어그램](./media/traffic-manager-load-balancing-azure/web-tier-diagram.png)

1. 리소스 그룹에서 toohello 인스턴스의 hello 섹션 앞에서 만든 hello 응용 프로그램 게이트웨이 이동 합니다.
2. 아래 **설정**선택, **백 엔드 풀**, 선택한 후 **추가** tooadd hello tooassociate hello 웹 계층 백 엔드 풀과 원하는 Vm입니다.
3. Hello에 **백 엔드 풀 추가** 블레이드에서 hello 백 엔드 풀의 hello 이름과 hello 풀에 있는 hello 컴퓨터의 모든 hello IP 주소를 입력 합니다. 이 시나리오에서는 가상 컴퓨터에 있는 두 개의 백 엔드 서버 풀을 연결합니다.

  ![Application Gateway "백 엔드 풀 추가" 블레이드](./media/traffic-manager-load-balancing-azure/s2-appgw-add-bepool.png)

4. 아래 **설정** hello 응용 프로그램 게이트웨이 선택 **규칙**, hello를 클릭 한 다음 **경로 기반** 단추 tooadd 규칙입니다.

  ![Application Gateway 규칙 "경로 기반" 단추](./media/traffic-manager-load-balancing-azure/s2-appgw-add-pathrule.png)

5. Hello에 **경로 기반 규칙 추가** 블레이드에서 hello 다음 정보를 제공 하 여 hello 규칙을 구성 합니다.

   기본 설정:

   + **이름**: hello hello 포털에 액세스할 수 있는 hello 규칙의 이름입니다.
   + **수신기**: hello 규칙에 사용 되는 hello 수신기입니다.
   + **백 엔드 풀 기본**: hello 백 엔드 풀 toobe hello 기본 규칙을 함께 사용 합니다.
   + **기본 HTTP 설정**: hello HTTP 설정 toobe hello 기본 규칙을 함께 사용 합니다.

   패스 기반 규칙:

   + **이름**: hello hello 경로 기반 규칙의 이름입니다.
   + **경로**: 트래픽을 전달에 사용 되는 hello 경로 규칙입니다.
   + **백 엔드 풀**:이 규칙으로 사용 되는 백 엔드 풀 toobe hello 합니다.
   + **HTTP 설정**: hello HTTP 설정 toobe이이 규칙과 함께 사용 합니다.

   > [!IMPORTANT]
   > 패스: 유효한 패스는 "/"로 시작해야 합니다. 와일드 카드 hello "\*" hello 끝에만 허용 됩니다. 사용 가능한 예는 /xyz, /xyz\* 또는 /xyz/\*입니다.

   ![Application Gateway "경로 기반 규칙 추가" 블레이드](./media/traffic-manager-load-balancing-azure/s2-appgw-pathrule-blade.png)

### <a name="step-3-add-application-gateways-toohello-traffic-manager-endpoints"></a>3 단계: 응용 프로그램 게이트웨이 toohello 트래픽 관리자 끝점 추가

이 시나리오에서는 트래픽 관리자는 서로 다른 지역에 있는 연결 된 tooapplication 게이트웨이 (대로 hello 이전 단계에서에서 구성)는입니다. Hello 다음 단계는 tooconnect hello 응용 프로그램 게이트웨이 구성 했으므로 해당 tooyour 트래픽 관리자 프로필.

1. Traffic Manager 프로필을 엽니다. toodo 리소스 그룹이 나에서 hello 트래픽 관리자 프로필의 hello 이름에 대 한 검색, 찾는 **모든 리소스**합니다.
2. Hello 왼쪽된 창에서 선택 **끝점**, 클릭 하 고 **추가** tooadd 끝점입니다.

  ![Traffic Manager 끝점 "추가" 단추](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint.png)

3. Hello에 **끝점 추가** 블레이드에서 hello 다음 정보를 입력 하 여 끝점을 만듭니다.

  * **형식**: hello 유형의 끝점 tooload 균형을 선택 합니다. 이 시나리오에서는 선택 **Azure 끝점** toohello 이전에 구성 된 응용 프로그램 게이트웨이 인스턴스가 연결 하려는 것 때문에 있습니다.
  * **이름**: hello 끝점의 hello 이름을 입력 합니다.
  * **대상 리소스 종류**: 선택 **공용 IP 주소** 차례로 선택한 다음 **대상 리소스**, 이전에 구성한 hello 응용 프로그램 게이트웨이의 hello 공용 IP를 선택 합니다.

   ![Traffic Manager "끝점 추가" 블레이드](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint-blade.png)

4. 이제 hello 트래픽 관리자 프로필의 DNS에 액세스 하 여 설치 프로그램을 테스트할 수 있습니다 (이 예제의: TrafficManagerScenario.trafficmanager.net). 요청을 다시 보냅니다, 그리고 (를) 실행 또는 Vm과 다른 지역에 생성 된 웹 서버를 종료 하 고 변경할 수 hello 트래픽 관리자 프로필 설정을 tootest 설치 합니다.

### <a name="step-4-create-a-load-balancer"></a>4단계: 부하 분산 장치 만들기

이 시나리오에서 부하 분산 장치 hello 웹 계층 toohello 데이터베이스 고가용성 클러스터 내에서에서 연결을 배포합니다.

가용성이 높은 데이터베이스 클러스터 SQL Server AlwaysOn을 사용 하는 경우 참조 너무[하나 이상의 항상에 가용성 그룹 수신기 구성](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) 단계별 지침.

내부 부하 분산 장치 구성에 대 한 자세한 내용은 참조 [hello Azure 포털에에서는 내부 부하 분산 장치를 만들](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)합니다.

1. Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 **새로** > **네트워킹** > **부하 분산 장치**합니다.
2. Hello에 **부하 분산 장치 만들기** 블레이드, 부하 분산 장치에 대 한 이름을 선택 합니다.
3. 집합 hello **형식** 너무**내부**, hello 적절 한 가상 네트워크와 서브넷에 부하 분산 장치 tooreside hello에 대 한를 선택 합니다.
4. **IP 주소 할당**에서 **동적** 또는 **정적** 중 하나를 선택합니다.
5. 아래 **리소스 그룹**, hello 부하 분산 장치에 대 한 hello 리소스 그룹을 선택 합니다.
6. 아래 **위치**, hello hello 부하 분산 장치에 대 한 적절 한 지역을 선택 합니다.
7. 클릭 **만들기** toogenerate hello에 대 한 부하 분산 장치입니다.

#### <a name="connect-a-back-end-database-tier-toohello-load-balancer"></a>백 엔드 데이터베이스 계층 toohello 부하 분산 장치 연결

1. 리소스 그룹에서 hello 이전 단계에서 만든 hello 부하 분산 장치를 찾습니다.
2. 아래 **설정**, 클릭 **백 엔드 풀**, 클릭 하 고 **추가** tooadd 백 엔드 풀입니다.

  ![부하 분산 장치 "백 엔드 풀 추가" 블레이드](./media/traffic-manager-load-balancing-azure/s4-ilb-add-bepool.png)

3. Hello에 **백 엔드 풀 추가** 블레이드에서 hello 백 엔드 풀의 hello 이름을 입력 합니다.
4. 개별 컴퓨터 또는 프로그램 가용성 집합 toohello 백 엔드 풀을 추가 합니다.

#### <a name="configure-a-probe"></a>프로브를 구성합니다.

1. 부하 분산 장치에서 아래 **설정**을 선택 **프로브**, 클릭 하 고 **추가** tooadd에 검색 합니다.

 ![부하 분산 장치 "프로브 추가" 블레이드](./media/traffic-manager-load-balancing-azure/s4-ilb-add-probe.png)

2. Hello에 **추가 프로브** 블레이드에서 hello 프로브에 대 한 hello 이름을 입력 합니다.
3. 선택 hello **프로토콜** hello 검색 합니다. 데이터베이스의 경우 HTTP 프로브가 아닌 TCP 프로브를 사용하려고 할 수 있습니다. 부하 분산 장치 프로브에 대해 자세히 toolearn 너무 참조[이해 부하 분산 장치 프로브](../load-balancer/load-balancer-custom-probe-overview.md)합니다.
4. Hello 입력 **포트** hello 프로브를 액세스 하기 위해 사용 하 여 데이터베이스 toobe의 합니다.
5. 아래 **간격**를 얼마나 자주 tooprobe hello 응용 프로그램을 지정 합니다.
6. 아래 **비정상 임계값**, hello 비정상으로 간주 하는 hello 백 엔드 VM toobe 발생 해야 하는 연속 프로브 오류 수를 지정 합니다.
7. 클릭 **확인** toocreate hello 프로브 합니다.

#### <a name="configure-hello-load-balancing-rules"></a>Hello 부하 분산 규칙 구성

1. 아래 **설정** 부하 분산 장치를 선택 **부하 분산 규칙**, 클릭 하 고 **추가** toocreate 규칙입니다.
2. Hello에 **추가 부하 분산 규칙** 블레이드에서 hello 입력 **이름** hello 부하 분산 규칙에 대 한 합니다.
3. Hello 선택 **프런트 엔드 IP 주소** hello의 부하 분산 장치, **프로토콜**, 및 **포트**합니다.
4. 아래 **백 엔드 포트가**, hello 백 엔드 풀에서 사용 하는 hello 포트 toobe를 지정 합니다.
5. 선택 hello **백 엔드 풀** hello 및 **프로브** hello 이전 단계 tooapply hello 규칙이 생성 된입니다.
6. 아래 **세션 지 속성**, hello 세션 toopersist 원하는 형식을 선택 합니다.
7. 아래 **유휴 시간 제한을**, hello는 유휴 시간 제한 (분) 수를 지정 합니다.
8. **부동 IP**에서 **사용 안 함**이나 **사용**을 선택합니다.
9. 클릭 **확인** toocreate hello 규칙입니다.

### <a name="step-5-connect-web-tier-vms-toohello-load-balancer"></a>5 단계: 웹 계층 Vm toohello 부하 분산 장치 연결

이제 모든 데이터베이스 연결에 대해 웹 계층 Vm에서 실행 되는 hello 응용 프로그램에서 hello IP 주소 및 부하 분산 장치 프런트 엔드 포트를 구성 합니다. 이 구성은 이러한 Vm에서 실행 되는 특정 toohello 응용 프로그램에 설명 합니다. tooconfigure hello 대상 IP 주소 및 포트를 toohello 응용 프로그램 설명서를 참조 하세요. hello Azure 포털에서에서 hello 프런트 엔드의 toofind hello IP 주소 hello toohello 프런트 엔드 IP 풀 이동 **부하 분산 장치 설정** 블레이드입니다.

![부하 분산 장치 "프런트 엔드 IP 풀" 탐색 창](./media/traffic-manager-load-balancing-azure/s5-ilb-frontend-ippool.png)

## <a name="next-steps"></a>다음 단계

* [Traffic Manager 개요](traffic-manager-overview.md)
* [Application Gateway 개요](../application-gateway/application-gateway-introduction.md)
* [Azure Load Balancer개요](../load-balancer/load-balancer-overview.md)
