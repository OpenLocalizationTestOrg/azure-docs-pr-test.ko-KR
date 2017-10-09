---
title: "사용 하 여 aaaConnect 컴퓨터 tooOMS hello OMS 게이트웨이 | Microsoft Docs"
description: "인터넷 액세스가 없는 경우 hello OMS 게이트웨이 toosend toohello OMS 서비스로 데이터를 OMS로 관리 되는 장치 및 Operations Manager 모니터링 되는 컴퓨터를 연결 합니다."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ae9a1623-d2ba-41d3-bd97-36e65d3ca119
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: magoedte
ms.openlocfilehash: 0cfa8f2fb66016e494f22c780e328be472b5fdee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-computers-without-internet-access-toooms-using-hello-oms-gateway"></a>Hello OMS 게이트웨이 사용 하 여 인터넷 액세스 tooOMS 하지 않고 컴퓨터 연결

이 문서에서는 OMS 관리 및 모니터링 하는 System Center Operations Manager 컴퓨터 보낼 수 있는 방법을 toohello OMS 서비스로 데이터 인터넷 액세스가 없는 경우에 대해 설명 합니다. hello OMS 게이트웨이 지 원하는 HTTP 터널링 정방향 HTTP 프록시는 데이터를 수집 하 고 대신 toohello OMS 서비스로 보낼 수 hello HTTP 연결 명령을 사용 하 여 합니다.  

hello OMS 게이트웨이 지원합니다.

* Azure 자동화 Hybrid Runbook Worker  
* Microsoft Monitoring Agent hello로 Windows 컴퓨터에 직접 tooan OMS 작업 영역 연결
* Linux 용 OMS 에이전트 hello로 Linux 컴퓨터에 직접 tooan OMS 작업 영역 연결  
* OMS와 통합되는 System Center Operations Manager 2012 SP1(UR7 포함), Operations Manager 2012 R2(UR3 포함) 또는 Operations Manager 2016 관리 그룹  

IT 보안 정책을 사용자 네트워크 tooconnect toohello 인터넷 판매 (POS) 장치 또는 IT 서비스를 지 원하는 서버 등의 컴퓨터를 허용 하지 않지만 tooconnect 해야 하는 경우 해당 tooOMS toomanage 모니터링 하 고, 구성할 수 있습니다 hello OMS 게이트웨이 tooreceive 구성 및 데이터를 대신해 전달와 직접 toocommunicate 합니다.  이러한 컴퓨터는 hello OMS 에이전트 toodirectly로 구성 된 경우는 tooan OMS 작업 영역을 연결 모든 컴퓨터 대신 hello 게이트웨이 OMS와 통신 합니다.  hello 게이트웨이 hello 에이전트 tooOMS에서 직접 데이터를 전송, 전송 중에 hello 데이터를 분석 하지 않습니다.

OMS와 함께 Operations Manager 관리 그룹에 통합 hello 관리 서버 구성된 tooconnect toohello OMS 게이트웨이 tooreceive 구성 정보 되며 사용 하도록 설정한 hello 솔루션에 따라 수집 된 데이터를 보낼 수 있습니다.  Operations Manager 에이전트는 Operations Manager 경고, 구성 평가, 인스턴스 공간 및 용량 데이터 toohello 관리 서버와 같은 일부 데이터를 보냅니다. IIS 로그, 성능 및 보안 이벤트와 같은 다른 대용량 데이터를 OMS 게이트웨이 toohello 직접 전송 됩니다.  하나 또는 신뢰할 수 없는 시스템 DMZ 또는 다른 격리 된 네트워크 toomonitor에 Operations Manager 게이트웨이 서버를 더 배포 하는 경우 OMS 게이트웨이와 통신할 수 없습니다.  Operations Manager 게이트웨이 서버를 보고서 tooa 관리 서버만 수 있습니다.  Hello 프록시 구성 정보 로그 분석을 위해 구성 된 toocollect 데이터를 자동으로 분산된 tooevery 에이전트 관리 컴퓨터를 Operations Manager 관리 그룹에는 OMS 게이트웨이 hello로 구성 된 toocommunicate 되 면 경우에 hello 설정은 비어 있습니다.    

direct에 대 한 고가용성 tooprovide 연결 하거나 운영 관리 그룹에서는 hello 게이트웨이 통해 OMS와 통신 하는 네트워크 부하 분산 tooredirect 및 여러 게이트웨이 서버 간에 hello 트래픽을 분산 합니다.  하나의 게이트웨이 서버가 다운 되 면 hello 트래픽은 리디렉션된 tooanother 사용할 수 있는 노드입니다.  

Hello OMS 게이트웨이 소프트웨어 toomonitor hello OMS 게이트웨이 실행 하는 hello 컴퓨터에서 hello OMS 에이전트를 설치 하 고 성능 또는 이벤트 데이터를 분석 하는 것이 좋습니다. 또한 hello 에이전트 수 hello OMS 게이트웨이 toocommunicate를 필요로 하는 hello 서비스 끝점을 식별 합니다.

각 에이전트는 에이전트 hello 게이트웨이에서 데이터 tooand를 자동으로 전송할 수 있도록 네트워크 연결 tooits 게이트웨이 있어야 합니다. 도메인 컨트롤러에 게이트웨이 설치할 hello 권장 되지 않습니다.

hello 다음 다이어그램에서 직접 에이전트 tooOMS hello 게이트웨이 서버를 사용 하 여 데이터 흐름을 보여 줍니다.  에이전트에는 동일한 hello 해당 프록시 구성 일치 있어야 합니다. 포트 hello OMS 게이트웨이 tooOMS와 구성 된 toocommunicate 됩니다.  

![OMS와 에이전트의 직접 통신 다이어그램](./media/log-analytics-oms-gateway/oms-omsgateway-agentdirectconnect.png)

hello 다음 다이어그램에서는 Operations Manager 관리 그룹 tooOMS에서 데이터 흐름   

![OMS와 Operations Manager의 통신 다이어그램](./media/log-analytics-oms-gateway/oms-omsgateway-opsmgrconnect.png)

## <a name="prerequisites"></a>필수 조건

컴퓨터 toorun hello OMS 게이트웨이 지정할 때이 컴퓨터에는 hello 다음을 항목이 있어야 합니다.

* Windows 10, Windows 8.1, Windows 7
* Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008
* .Net Framework 4.5
* 최소 4코어 프로세서 및 8GB 메모리

### <a name="language-availability"></a>사용 가능한 언어

hello OMS 게이트웨이 hello 다음 언어에서에서 제공 됩니다.

- 중국어 (간체)
- 중국어 (번체)
- 체코어
- 네덜란드어
- 영어
- 프랑스어
- 독일어
- 헝가리어
- 이탈리아어
- 일본어
- 한국어
- 폴란드어
- 포르투갈어(브라질)
- 포르투갈어(포르투갈)
- 러시아어
- 스페인어 (국제)

## <a name="download-hello-oms-gateway"></a>Hello OMS 게이트웨이 다운로드 합니다.

세 가지 방법으로 tooget hello 최신 버전의 hello OMS 게이트웨이 설치 파일 가지가 있습니다.

1. Hello에서 다운로드 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=54443)합니다.

2. Hello OMS 포털에서 다운로드 합니다.  OMS 작업 영역 tooyour 로그인 한 후 이동 너무**설정** > **연결 된 원본** > **Windows 서버** 클릭**OMS 게이트웨이 다운로드**합니다.

3. Hello에서 다운로드 [Azure 포털](https://portal.azure.com)합니다.  로그인한 후 다음 단계를 수행합니다.  

   1. 서비스의 hello 목록을 이동한 다음 선택 **로그 분석**합니다.  
   2. 작업 영역을 선택합니다.
   3. **일반**의 작업 영역 블레이드에서 **빠른 시작**을 클릭합니다.
   4. 아래 **데이터 소스 tooconnect toohello 작업 영역 선택**, 클릭 **컴퓨터**합니다.
   5. Hello에 **직접 에이전트** 블레이드에서 클릭 **OMS 게이트웨이 다운로드**합니다.<br><br> ![OMS Gateway 다운로드](./media/log-analytics-oms-gateway/download-gateway.png)


## <a name="install-hello-oms-gateway"></a>Hello OMS 게이트웨이 설치 합니다.

게이트웨이 tooinstall hello 다음 단계를 수행 합니다.  이전 버전을 설치한 경우 이전의 *로그 분석 전달자*, 됩니다 toothis 릴리스를 업그레이드 합니다.  

1. Hello 대상 폴더에서 두 번 클릭 **OMS Gateway.msi**합니다.
2. Hello에 **시작** 페이지 **다음**합니다.<br><br> ![게이트웨이 설치 마법사](./media/log-analytics-oms-gateway/gateway-wizard01.png)<br>
3. Hello에 **사용권 계약** 페이지에서 **hello 사용권 계약에에서 hello 조건에 동의** tooagree toohello EULA 클릭 하 고 **다음**합니다.
4. Hello에 **포트 및 프록시 주소** 페이지:
   1. 형식 hello TCP 포트 번호 toobe hello 게이트웨이에 사용 합니다. 설치 프로그램에서 Windows 방화벽의 인바운드 규칙을 이 포트 번호로 구성합니다.  hello 기본값은 8080입니다.
      hello hello 포트 번호의 유효한 범위는 1-65535 까지입니다. Hello 입력이이 범위에 해당 하지 않으면, 오류 메시지가 나타납니다.
   2. 필요에 따라 hello 여기서는 hello 게이트웨이 서버 설치 경우 프록시를 통해 요구 toocommunicate hello 게이트웨이에서 tooconnect 여기서 hello 프록시 주소를 입력 합니다. 예: `http://myorgname.corp.contoso.com:80`.  이 옵션이 공백인 경우 hello 게이트웨이 tooconnect toohello 인터넷 직접 시도 합니다.  프록시 서버에 인증이 필요한 경우 사용자 이름과 암호를 입력합니다.<br><br> ![게이트웨이 마법사 프록시 구성](./media/log-analytics-oms-gateway/gateway-wizard02.png)<br>   
   3. **다음**을 누릅니다.
5. Microsoft 업데이트 사용 경우 hello Microsoft Update 페이지 나타납니다 tooenable를 선택할 수 있는 것입니다. 선택한 후에 **다음**을 클릭합니다. 그렇지 않으면 toohello 다음 단계를 계속 합니다.
6. Hello에 **대상 폴더** hello 기본 폴더 Files\OMS 게이트웨이나 유형 C:\Program hello 위치 tooinstall 게이트웨이 선택 하 고 클릭 그대로 페이지 **다음**합니다.
7. Hello에 **준비 tooinstall** 페이지 **설치**합니다. 사용자 계정 컨트롤 요청 권한 tooinstall 나타날 수 있습니다. 그런 경우에는 **예**를 클릭합니다.
8. 설치가 완료된 후에 **마침**을 클릭합니다. Hello 서비스 hello services.msc 스냅인을 열고 실행 하 고 있는지 확인 하는지 확인할 수 있습니다 **OMS 게이트웨이** 상태 서비스의 hello 목록에 있는 표시 되는 **실행**합니다.<br><br> ![서비스 – OMS 게이트웨이](./media/log-analytics-oms-gateway/gateway-service.png)  

## <a name="configure-network-load-balancing"></a>네트워크 부하 분산 구성
네트워크 부하 분산 (NLB) Microsoft 네트워크 부하 분산 (NLB) 또는 하드웨어 기반의 부하 분산 장치 중 하나를 사용 하 여 사용 하 여 고가용성에 대 한 hello 게이트웨이 구성할 수 있습니다.  hello 부하 분산 장치를 관리 트래픽을 리디렉션하여 hello 해당 노드에서 hello OMS 에이전트의에서 연결 또는 Operations Manager 관리 서버를 요청 합니다. 한 게이트웨이 서버가 되 면 hello 트래픽 리디렉션된 tooother 노드를 가져옵니다.

toolearn 어떻게 toodesign Windows Server 2016 네트워크 부하 분산 클러스터를 배포 하 고, 참조 [네트워크 로드 균형 조정](https://technet.microsoft.com/windows-server-docs/networking/technologies/network-load-balancing)합니다.  hello 다음 단계에서는 어떻게 tooconfigure Microsoft 네트워크 부하 분산 클러스터.  

1.  관리자 계정으로 hello NLB 클러스터의 구성원 인 hello Windows 서버에 로그인 합니다.  
2.  [서버 관리자]에서 [네트워크 부하 분산 관리자]를 열고, **도구**를 클릭한 다음 **네트워크 부하 분산 관리자**를 클릭합니다.
3. tooconnect hello Microsoft Monitoring Agent 설치를 사용 하 여 OMS 게이트웨이 서버 hello 클러스터 IP 주소를 마우스 오른쪽 단추로 클릭 **호스트 추가 tooCluster**합니다.<br><br> ![네트워크 부하 분산 관리자-호스트 tooCluster 추가](./media/log-analytics-oms-gateway/nlb02.png)<br>
4. 원하는 tooconnect hello 게이트웨이 서버의 hello IP 주소를 입력 합니다.<br><br> ![네트워크 부하 분산 관리자-호스트 tooCluster 추가: 연결](./media/log-analytics-oms-gateway/nlb03.png)

## <a name="configure-oms-agent-and-operations-manager-management-group"></a>OMS 에이전트 및 Operations Manager 관리 그룹 구성
hello 다음 섹션에서는 어떻게 tooconfigure 직접 연결 된 OMS 에이전트, Operations Manager 관리 그룹 또는 Azure 자동화 Hybrid Runbook Worker OMS와 함께 OMS 게이트웨이 toocommunicate hello와에서 단계 합니다.  

toounderstand 요구 사항 및 단계 어떻게 tooinstall hello tooOMS에 직접 연결 하는 Windows 컴퓨터에 OMS 에이전트에 참조 [연결 Windows 컴퓨터 tooOMS](log-analytics-windows-agents.md) 또는 Linux 컴퓨터 참조에 대 한 [Linux 컴퓨터 연결 tooOMS](log-analytics-linux-agents.md)합니다.

### <a name="configuring-hello-oms-agent-and-operations-manager-toouse-hello-oms-gateway-as-a-proxy-server"></a>프록시 서버로 hello OMS 에이전트 및 Operations Manager toouse hello OMS 게이트웨이 구성

### <a name="configure-standalone-oms-agent"></a>독립 실행형 OMS 에이전트 구성
참조 [hello Microsoft Monitoring Agent로 프록시 및 방화벽 설정 구성](log-analytics-proxy-firewall.md) 에이전트 toouse hello 게이트웨이이 경우에 프록시 서버를 구성 하는 방법에 대 한 정보에 대 한 합니다.  Hello OMS 에이전트 프록시 구성은 네트워크 부하 분산 장치 뒤에 여러 게이트웨이 서버를 배포한 경우 hello NLB의 가상 IP 주소를 hello?<br><br> ![Microsoft Monitoring Agent 속성 – 프록시 설정](./media/log-analytics-oms-gateway/nlb04.png)

### <a name="configure-operations-manager---all-agents-use-hello-same-proxy-server"></a>Operations Manager 구성-hello를 사용 하는 모든 에이전트 같은 프록시 서버
Operations Manager tooadd hello 게이트웨이 서버를 구성 합니다.  hello 설정은 비어 있는 경우에 관리자 tooOperations 보고 tooall 에이전트를 적용 하는 hello 프록시 구성은 자동으로 Operations Manager.

toouse hello 게이트웨이 toosupport Operations Manager이 필요 합니다.

* Microsoft Monitoring Agent (에이전트 버전 – **8.0.10900.0** 이상) hello 게이트웨이 서버에 설치 하 고 toocommunicate 하려는 hello OMS 작업 영역에 대 한 구성 합니다.
* hello 게이트웨이 인터넷에 연결 하거나 수행 하는 연결 된 tooa 프록시 서버로 해야 합니다.

> [!NOTE]
> Hello 게이트웨이에 대 한 값을 지정 하지 않는 경우 빈 값 tooall 에이전트가 푸시됩니다.


1. Operations Manager 콘솔 열기 hello 고 **Operations Management Suite**, 클릭 **연결** 클릭 하 고 **프록시 서버 구성**합니다.<br><br> ![Operations Manager – 프록시 서버 구성](./media/log-analytics-oms-gateway/scom01.png)<br>
2. 선택 **프록시 서버 tooaccess hello Operations Management Suite를 사용 하 여** hello OMS 게이트웨이 서버 hello IP 주소 또는 hello NLB의 가상 IP 주소를 입력 합니다. Hello로 시작 되도록 `http://` 접두사입니다.<br><br> ![Operations Manager – 프록시 서버 주소](./media/log-analytics-oms-gateway/scom02.png)<br>
3. **마침**을 클릭합니다. Operations Manager 서버에는 연결 된 tooyour OMS 작업 영역입니다.

### <a name="configure-operations-manager---specific-agents-use-proxy-server"></a>Operations Manager 구성 - 특정 에이전트에서 프록시 서버 사용
크거나 복잡 한 환경에 대 한 특정 서버 (또는 그룹) toouse hello OMS 게이트웨이 서버를 하기만 할 수도 있습니다.  이러한 서버에 대 한 hello Operations Manager 에이전트 직접이 값으로 덮어쓰기 hello hello 관리 그룹에 대 한 전역 값을 업데이트할 수 없습니다.  대신 toooverride hello 사용 되는 규칙 toopush이 값이 필요 합니다.

> [!NOTE]
> 이 동일한 구성 기술을 수 사용자 환경에서 여러 명의 OMS 게이트웨이 서버의 tooallow hello 사용을 사용 합니다.  예를 들어 각 지역 마다 별로 지정 하는 특정 OMS 게이트웨이 서버 toobe가 필요할 수 있습니다.

1. Operations Manager 콘솔 열기 hello 및 선택 hello **제작** 작업 영역입니다.  
2. Hello 제작 작업 영역에서 선택 **규칙** hello 클릭 **범위** hello Operations Manager 도구 모음에서 단추입니다. 이 단추를 사용할 수 없는 경우에 toomake 개체 폴더가 아니라 hello 모니터링 창에서 선택 했는지 확인 합니다. hello **관리 팩 개체 범위** 대화 상자에는 공통 대상된 클래스, 그룹 또는 개체의 목록이 표시 됩니다.
3. 형식 **상태 관리 서비스** hello에 **찾아보십시오** 필드 고 hello 목록에서 선택 합니다.  **확인**을 클릭합니다.  
4. Hello 규칙에 대 한 검색 **관리자 프록시 설정을 규칙** hello 운영 콘솔 도구 모음에서 클릭 **재정의** 가리킨 다음 너무**재정의 hello Rule\For 클래스의 특정 개체: 상태 서비스** hello 목록에서 특정 개체를 선택 합니다.  Hello 상태 서비스 개체를 포함 하는 사용자 지정 그룹을 만들 수는 필요에 따라 hello 서버 tooapply이 재정의 tooand 원하는 하면 다음이 hello 재정의 toothat 그룹을 적용 합니다.
5. Hello에 **재정의 속성** 대화 상자에서 tooplace hello에 확인 표시를 클릭 **재정의** 열 다음 toohello **WebProxyAddress** 매개 변수입니다.  Hello에 **재정의 값** 필드에, hello로 시작 하는 hello OMS 게이트웨이 서버 확인의 hello URL 입력 `http://` 접두사입니다.
   >[!NOTE]
   > 재정의 hello Microsoft System Center Advisor 보안 참조 재정의 관리 팩에 포함 hello Microsoft System Center Advisor 모니터링 서버 그룹을 대상으로 지정 하면 자동으로 관리 이미 않는 대로 tooenable hello 규칙을 않아도 됩니다.
   >
6. Hello에서 관리 팩을 선택 하거나 **대상 관리 팩 선택** 나열 하거나 클릭 하 여 새로운 봉인 되지 않은 관리 팩을 만들 **새로**합니다.
7. 변경을 완료하면 **확인**을 클릭합니다.

### <a name="configure-for-automation-hybrid-workers"></a>Automation Hybrid Worker에 대한 구성
단계를 수행 하는 hello 수동, 임시 해결 방법 tooconfigure hello 게이트웨이 toosupport 제공 자동화 Hybrid Runbook Worker 사용자 환경에 있으면 해당 합니다.

다음 단계는 hello, tooknow hello hello 자동화 계정이 있는 Azure 지역 해야 합니다. toolocate hello 위치:

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello Azure 자동화 서비스를 선택 합니다.
3. Hello 적절 한 Azure 자동화 계정을 선택 합니다.
4. **위치** 아래에서 해당 지역을 확인합니다.<br><br> ![Azure Portal – Automation 계정 위치](./media/log-analytics-oms-gateway/location.png)  

각 위치에 대 한 테이블 tooidentify hello url hello를 사용 합니다.

**작업 런타임 데이터 서비스 URL**

| **위치** | **URL** |
| --- | --- |
| 미국 중북부 |ncus-jobruntimedata-prod-su1.azure-automation.net |
| 서유럽 |we-jobruntimedata-prod-su1.azure-automation.net |
| 미국 중남부 |scus-jobruntimedata-prod-su1.azure-automation.net |
| 미국 동부 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| 캐나다 중부 |cc-jobruntimedata-prod-su1.azure-automation.net |
| 북유럽 |ne-jobruntimedata-prod-su1.azure-automation.net |
| 동남아시아 |sea-jobruntimedata-prod-su1.azure-automation.net |
| 인도 중부 |cid-jobruntimedata-prod-su1.azure-automation.net |
| 일본 |jpe-jobruntimedata-prod-su1.azure-automation.net |
| 오스트레일리아 |ase-jobruntimedata-prod-su1.azure-automation.net |

**에이전트 서비스 URL**

| **위치** | **URL** |
| --- | --- |
| 미국 중북부 |ncus-agentservice-prod-1.azure-automation.net |
| 서유럽 |we-agentservice-prod-1.azure-automation.net |
| 미국 중남부 |scus-agentservice-prod-1.azure-automation.net |
| 미국 동부 2 |eus2-agentservice-prod-1.azure-automation.net |
| 캐나다 중부 |cc-agentservice-prod-1.azure-automation.net |
| 북유럽 |ne-agentservice-prod-1.azure-automation.net |
| 동남아시아 |sea-agentservice-prod-1.azure-automation.net |
| 인도 중부 |cid-agentservice-prod-1.azure-automation.net |
| 일본 |jpe-agentservice-prod-1.azure-automation.net |
| 오스트레일리아 |ase-agentservice-prod-1.azure-automation.net |

컴퓨터 등록 되어 있으면 하이브리드 Runbook 작업자로 자동으로 hello 업데이트 관리 솔루션을 사용 하 여 패치 기능에 다음이 단계를 수행 합니다.

1. OMS 게이트웨이 hello에 hello 작업 런타임 데이터 서비스 Url toohello 호스트 허용 목록을 추가 합니다. 예: `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
2. Hello 다음 PowerShell cmdlet을 사용 하 여 hello OMS 게이트웨이 서비스를 다시 시작 합니다.`Restart-Service OMSGatewayService`

컴퓨터가 hello 하이브리드 Runbook 작업자 등록 cmdlet를 사용 하 여 등록 된 tooAzure 자동화 있으면 다음이 단계를 따르십시오.

1. OMS 게이트웨이 hello에 hello 에이전트 서비스 등록 URL toohello 호스트 허용 목록을 추가 합니다. 예: `Add-OMSGatewayAllowedHost ncus-agentservice-prod-1.azure-automation.net`
2. OMS 게이트웨이 hello에 hello 작업 런타임 데이터 서비스 Url toohello 호스트 허용 목록을 추가 합니다. 예: `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
3. Hello OMS 게이트웨이 서비스를 다시 시작 합니다.
    `Restart-Service OMSGatewayService`

## <a name="useful-powershell-cmdlets"></a>유용한 PowerShell cmdlet
Cmdlet은 필요한 tooupdate hello OMS 게이트웨이 구성 설정 작업을 수행할 수 있습니다. 사용하기 전에 다음을 수행해야 합니다.

1. Hello OMS 게이트웨이 (MSI) 설치 합니다.
2. PowerShell 콘솔 창을 엽니다.
3. tooimport hello 모듈이이 명령을 입력 합니다.`Import-Module OMSGateway`
4. 오류가 발생 하지 않으면 hello 이전 단계에서 hello 모듈 성공적으로 가져왔는지와 hello cmdlet을 사용할 수 있습니다. `Get-Module OMSGateway`를 입력합니다.
5. Hello cmdlet을 사용 하 여 변경한 후 hello 게이트웨이 서비스를 다시 시작할 수 있는지 확인 합니다.

3 단계에서 오류가 발생 하면 hello 모듈을 가져올 되지 않았습니다. PowerShell은 없습니다 toofind hello 모듈 hello 오류가 발생할 수 있습니다. Hello 게이트웨이 설치 경로에서 찾을 수 있습니다: *C:\Program Files\Microsoft OMS Gateway\PowerShell*합니다.

| **Cmdlet** | **매개 변수** | **설명** | **예제** |
| --- | --- | --- | --- |  
| `Get-OMSGatewayConfig` |키 |Hello 서비스의 hello 구성을 가져옵니다. |`Get-OMSGatewayConfig` |  
| `Set-OMSGatewayConfig` |키(필수) <br> 값 |변경 내용을 hello hello 서비스의 구성 |`Set-OMSGatewayConfig -Name ListenPort -Value 8080` |  
| `Get-OMSGatewayRelayProxy` | |릴레이 (업스트림) 프록시의 hello 주소를 가져옵니다. |`Get-OMSGatewayRelayProxy` |  
| `Set-OMSGatewayRelayProxy` |주소<br> 사용자 이름<br> 암호 |릴레이 (업스트림) 프록시의 hello 주소 (및 자격 증명)를 설정합니다. |1. 릴레이 프록시 및 자격 증명 설정:<br> `Set-OMSGatewayRelayProxy`<br>`-Address http://www.myproxy.com:8080`<br>`-Username user1 -Password 123` <br><br> 2. 인증이 필요 없는 릴레이 프록시 설정: `Set-OMSGatewayRelayProxy`<br> `-Address http://www.myproxy.com:8080` <br><br> 3. 지우기 hello 릴레이 프록시 설정:<br> `Set-OMSGatewayRelayProxy` <br> `-Address ""` |  
| `Get-OMSGatewayAllowedHost` | |가져옵니다 hello 현재 허용 되는 호스트 (hello 로컬로 구성 된 허용 된 호스트는 자동으로 다운로드 한 허용 된 호스트)만 |`Get-OMSGatewayAllowedHost` |
| `Add-OMSGatewayAllowedHost` |호스트(필수) |Hello 호스트 toohello 허용 목록에 추가 |`Add-OMSGatewayAllowedHost -Host www.test.com` |  
| `Remove-OMSGatewayAllowedHost` |호스트(필수) |Hello 호스트 hello 허용 목록에서 제거 |`Remove-OMSGatewayAllowedHost`<br> `-Host www.test.com` |  
| `Add-OMSGatewayAllowedClientCertificate` |주체(필수) |Hello 클라이언트 인증서 주체 toohello 허용 목록에 추가 |`Add-OMSGatewayAllowed`<br>`ClientCertificate` <br> `-Subject mycert` |  
| `Remove-OMSGatewayAllowedClientCertificate` |주체(필수) |Hello 허용 목록에서에서 hello 클라이언트 인증서 주체를 제거 합니다. |`Remove-OMSGatewayAllowed` <br> `ClientCertificate` <br> `-Subject mycert` |  
| `Get-OMSGatewayAllowedClientCertificate` | |가져옵니다 hello 현재 허용 된 클라이언트 인증서 주체 (hello 로컬로 구성 허용 된 주제를 포함 하지는 자동으로 다운로드 한 허용 된 주제) |`Get-`<br>`OMSGatewayAllowed`<br>`ClientCertificate` |  

## <a name="troubleshooting"></a>문제 해결
hello 게이트웨이에서 기록 되는 toocollect 이벤트가 해야 tooalso hello OMS 에이전트가 설치 되어 있어야 합니다.<br><br> ![이벤트 뷰어 – OMS 게이트웨이 로그](./media/log-analytics-oms-gateway/event-viewer.png)

**OMS 게이트웨이 이벤트 ID 및 설명**

hello 다음 표에 나와 hello 이벤트 Id와 OMS 게이트웨이 로그 이벤트에 대 한 설명입니다.

| **ID** | **설명** |
| --- | --- |
| 400 |특정 ID가 없는 모든 응용 프로그램 오류 |
| 401 |잘못된 구성. 예: listenPort = 정수가 아닌 “텍스트" |
| 402 |TLS 핸드셰이크 메시지 구문 분석 중 예외 |
| 403 |네트워킹 오류. 예를 들어: tootarget 서버를 연결할 수 없음 |
| 100 |일반 정보 |
| 101 |서비스가 시작됨 |
| 102 |서비스가 중지됨 |
| 103 |클라이언트로부터 HTTP CONNECT 명령을 수신함 |
| 104 |HTTP CONNECT 명령이 아님 |
| 105 |대상 서버에 허용 된 목록 없거나 hello 대상 포트가 보안 포트 (443) 않습니다. <br> <br> 게이트웨이 서버에서 해당 hello MMA 에이전트를 확인 하 고 게이트웨이 hello와 통신 하는 hello 에이전트 연결된 toohello는 동일한 로그 분석 작업 영역입니다. |
| 105 |ERROR TcpConnection – 클라이언트 인증서가 잘못됨: CN=Gateway <br><br> 다음 사항을 확인합니다. <br>    <br> &#149; 버전 번호가 1.0.395.0 이상인 게이트웨이를 사용 중입니다. <br> &#149; hello MMA 에이전트에서 게이트웨이 서버 및 게이트웨이 hello와 통신 하는 hello 에이전트는 연결 된 toohello 동일한 로그 분석 작업 영역입니다. |
| 106 |의심 스러운와 거부 된 hello TLS 세션은 어떤 이유로 |
| 107 |확인 된 hello TLS 세션 |

**성능 카운터 toocollect**

hello 다음 표에 hello ÷ ´ ֹ OMS 게이트웨이 hello에 사용할 수 있습니다. 성능 모니터를 사용 하 여 hello 카운터를 추가할 수 있습니다.

| **Name** | **설명** |
| --- | --- |
| OMS 게이트웨이/활성 클라이언트 연결 |활성 클라이언트 네트워크(TCP) 연결의 수 |
| OMS 게이트웨이/오류 수 |오류 수 |
| OMS 게이트웨이/연결된 클라이언트 |연결된 클라이언트 수 |
| OMS 게이트웨이/거부 횟수 |사용 권한 거부 때문 tooany TLS 유효성 검사 오류 수 |

![OMS 게이트웨이 성능 카운터](./media/log-analytics-oms-gateway/counters.png)

## <a name="get-assistance"></a>지원 받기
로그인 toohello Azure 포털을 하는 경우 OMS 게이트웨이 hello 또는 다른 Azure 서비스 또는 서비스의 기능 지원에 대 한 요청을 만들 수 있습니다.
toorequest 지원을 hello hello 포털의 맨 위 오른쪽 모서리에 hello 물음표 기호를 클릭 한 다음 클릭 **새로운 지원 요청**합니다. 그런 다음 새 지원 요청 양식 hello를 완료 합니다.

![새 지원 요청](./media/log-analytics-oms-gateway/support.png)

Hello에 OMS 또는 로그 분석에 대 한 의견을 둘 수도 있으며 [Microsoft Azure 피드백 포럼](https://feedback.azure.com/forums/267889)합니다.

## <a name="next-steps"></a>다음 단계
* [데이터 원본을 추가](log-analytics-data-sources.md) toocollect 데이터를 OMS 작업 영역에 연결 된 원본 hello 및 hello OMS 리포지토리에 저장 합니다.
