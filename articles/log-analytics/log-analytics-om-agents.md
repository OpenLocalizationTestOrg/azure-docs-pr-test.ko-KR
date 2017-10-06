---
title: "Operations Manager tooLog aaaConnect 분석 | Microsoft Docs"
description: "toomaintain System Center Operations Manager 사용에 대 한 기존 투자를 확장 로그 분석을 사용 하는 기능, OMS 작업 영역으로 Operations Manager를 통합할 수 있습니다."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 245ef71e-15a2-4be8-81a1-60101ee2f6e6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: magoedte
ms.openlocfilehash: b2841c7aa209fec7357dc4c8b1ff4325fdaa37ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-operations-manager-toolog-analytics"></a>Operations Manager tooLog 분석 연결
toomaintain System Center Operations Manager 사용에 대 한 기존 투자를 확장 로그 분석을 사용 하는 기능, OMS 작업 영역으로 Operations Manager를 통합할 수 있습니다.  이렇게 하면 OMS의 hello 기회를 활용 하 여 toouse Operations Manager를 계속 하려면:

* Operations Manager와 함께 IT 서비스의 hello 상태 모니터링 계속
* 인시던트 및 문제 관리를 지원하는 ITSM 솔루션과 통합 유지 관리
* 배포 에이전트 tooon 온-프레미스 및 공용 클라우드 IaaS 가상 컴퓨터를 Operations Manager 모니터링 하는 hello 수명 주기 관리

System Center Operations Manager와 통합 OMS에서 수집, 저장 및 Operations Manager에서 데이터 분석의 hello 속도 효율성을 사용 하 여 값 tooyour 서비스 작업 전략을 추가 합니다.  OMS는 데 도움이 됩니다 상관관계를 설정한 후 및 hello 오류 문제를 식별 하 고 기존 문제 관리 프로세스를 지원 하기 위해 되풀이 표시가 방향으로 작업 합니다.   hello hello 검색 엔진 tooexamine 성능, 이벤트 및 경고 데이터를 풍부한 대시보드를 유연 하 고 기능 tooexpose 보고이 데이터를 의미 있는 방식으로 OMS는 Operations Manager complimenting에서 hello 강도 시연 합니다.

toohello Operations Manager 관리 그룹을 보고 하는 hello 에이전트 hello 로그 분석 데이터 원본 및 OMS 구독에서 설정한 솔루션에 따라 서버에서 데이터를 수집 합니다.  사용 하도록 설정한 hello 솔루션에 따라 이러한 솔루션의에서 데이터는 toohello OMS 웹 서비스에서 보내거나 hello 인해 hello 에이전트 관리 시스템에서 수집 된 데이터 볼륨 직접 Operations Manager 관리 서버에서 직접 전송 하는 중 hello 에이전트 tooOMS 웹 서비스입니다. 관리 서버 hello toohello OMS 웹 서비스로; 직접 hello OMS 데이터 전달 toohello OperationsManager 또는 OperationsManagerDW 데이터베이스는 작성 되지 않습니다.  OMS 웹 서비스로 hello와 연결이 끊기는 하는 관리 서버를 로컬로 통신은 OMS와 함께 다시 설정 될 때까지 hello 데이터를 캐시 합니다.  관리 서버 hello tooplanned 유지 관리 또는 계획 되지 않은 중단 인해 오프 라인 이면 hello 관리 그룹의 다른 관리 서버에 OMS와의 연결을 다시 시작 합니다.  

hello 다음 다이어그램은 hello 관리 서버 및 System Center Operations Manager 관리 그룹 및 hello 방향 및 포트를 포함 하 여 OMS에 에이전트 간의 hello 연결 합니다.   

![oms-operations-manager-integration-diagram](./media/log-analytics-om-agents/oms-operations-manager-connection.png)

관리 서버 구성된 tooconnect toohello OMS 게이트웨이 tooreceive 구성 정보 수 있고 hello 솔루션에 따라 수집 된 데이터를 보낼 경우 IT 보안 정책을 네트워크 tooconnect toohello 인터넷에서 컴퓨터를 허용 하지 않으므로, 사용 하도록 설정 합니다.  자세한 내용 및 tooconfigure OMS 게이트웨이 toohello OMS 서비스를 통해는 Operations Manager 관리 그룹 toocommunicate 확인 하려면 어떻게 해야 하는 단계에 대 한 [hello OMS 게이트웨이 사용 하 여 컴퓨터 tooOMS 연결](log-analytics-oms-gateway.md)합니다.  

## <a name="system-requirements"></a>시스템 요구 사항
을 시작 하기 전에 다음 선행 조건을 충족 하는 세부 정보 tooverify hello를 검토 합니다.

* OMS는 Operations Manager 2016, Operations Manager 2012 SP1 UR6 이상 및 Operations Manager 2012 R2 UR2 이상만을 지원합니다.  프록시 지원은 Operations Manager 2012 SP1 UR7 및 Operations Manager 2012 R2 UR3에 추가되었습니다.
* 모든 Operations Manager 에이전트는 최소 지원 요구 사항을 만족해야 합니다. 확인 에이전트 hello 최소 업데이트에는, 그렇지 않으면 Windows 에이전트 트래픽 실패할 수 있습니다 많은 오류가 hello Operations Manager 이벤트 로그를 가득 찰 수 있습니다.
* OMS 구독입니다.  자세한 내용은 [Log Analytics 시작](log-analytics-get-started.md)을 검토합니다.

### <a name="network"></a>네트워크
아래 목록 hello 프록시 및 방화벽에 필요한 구성 정보 hello Operations Manager 에이전트, 관리 서버와 OMS와 함께 Operations 콘솔 toocommunicate hello 정보입니다.  각 구성 요소에서 트래픽은 네트워크 toohello OMS 서비스에서 아웃 바운드입니다.     

|리소스 | 포트 번호| HTTP 검사 무시|  
|---------|------|-----------------------|  
|**에이전트**|||  
|\*.ods.opinsights.azure.com| 443 |예|  
|\*.oms.opinsights.azure.com| 443|예|  
|\*.blob.core.windows.net| 443|예|  
|\*.azure-automation.net| 443|예|  
|**관리 서버**|||  
|\*.service.opinsights.azure.com| 443||  
|\*.blob.core.windows.net| 443| 예|  
|\*.ods.opinsights.azure.com| 443| 예|  
|*.azure-automation.net | 443| 예|  
|**Operations Manager 콘솔 tooOMS**|||  
|service.systemcenteradvisor.com| 443||  
|\*.service.opinsights.azure.com| 443||  
|\*.live.com| 80 및 443||  
|\*.microsoft.com| 80 및 443||  
|\*.microsoftonline.com| 80 및 443||  
|\*.mms.microsoft.com| 80 및 443||  
|login.windows.net| 80 및 443||  


## <a name="connecting-operations-manager-toooms"></a>Operations Manager tooOMS 연결
OMS 작업 영역에 Operations Manager 관리 그룹 tooconnect tooone hello 일련의 단계 tooconfigure 다음을 수행 합니다.

1. Hello Operations Manager 콘솔에서 선택 hello **관리** 작업 영역입니다.
2. Hello Operations Management Suite 노드를 확장 하 고 클릭 **연결**합니다.
3. Hello 클릭 **tooOperations Management Suite 등록** 링크 합니다.
4. Hello에 **Operations Management Suite 등록 마법사: 인증** 페이지 hello 전자 메일 주소 또는 전화 번호와 OMS 구독에 연결 된 hello 관리자 계정의 암호를 입력 하 고 클릭 **로그인**합니다.
5. Hello에 성공적으로 인증 되 **Operations Management Suite 등록 마법사: 작업 영역 선택** 는 페이지에서 메시지가 tooselect OMS 작업 영역입니다.  선택 tooregister hello 드롭 다운 목록에서 hello Operations Manager 관리 그룹을 클릭 한 다음 작업 영역 hello 둘 이상의 작업 영역에 있으면 **다음**합니다.
   
   > [!NOTE]
   > Operations Manager는 한 번에 하나의 OMS 작업 영역을 지원합니다. hello 이전 작업 영역으로 등록 된 tooOMS 상태인 hello 컴퓨터 및 hello 연결은 OMS에서 제거 됩니다.
   > 
   > 
6. Hello에 **Operations Management Suite 등록 마법사: 요약** 페이지 설정을 확인 하 고 정확 하다 면 클릭 **만들기**합니다.
7. Hello에 **Operations Management Suite 등록 마법사: 마침** 페이지 **닫기**합니다.

### <a name="add-agent-managed-computers"></a>에이전트 관리 컴퓨터 추가
통합을 OMS 작업 영역을 구성 하면이 OMS와의 연결을 설정, 데이터 마트 tooyour 보고 hello 에이전트에서 데이터가 수집 되지 않습니다. 이는 Log Analytics에 대한 데이터를 수집할 특정 에이전트 관리 컴퓨터를 구성할 때까지 일어나지 않습니다. Hello 컴퓨터 개체를 개별적으로 선택 하거나 하거나 Windows 컴퓨터 개체를 포함 하는 그룹을 선택할 수 있습니다. 논리 디스크 또는 SQL 데이터베이스와 같은 다른 클래스의 인스턴스를 포함하는 그룹을 선택할 수 없습니다.

1. Operations Manager 콘솔 열기 hello 및 선택 hello **관리** 작업 영역입니다.
2. Hello Operations Management Suite 노드를 확장 하 고 클릭 **연결**합니다.
3. Hello 클릭 **컴퓨터/그룹 추가** hello 작업에서 링크 hello 창의 hello 오른쪽에 제목입니다.
4. Hello에 **컴퓨터 검색** 대화 상자, Operations Manager에서 모니터링 하는 그룹 또는 컴퓨터에 대 한 검색할 수 있습니다. 컴퓨터 또는 그룹 tooonboard tooOMS 선택를 클릭 **추가**, 클릭 하 고 **확인**합니다.

컴퓨터를 볼 수 있으며 hello에 그룹이 구성 Operations Management Suite 아래의 hello 관리 컴퓨터 노드에서 toocollect 데이터 **관리** hello 운영 콘솔의 작업 영역입니다.  여기에서 필요에 따라 컴퓨터 및 그룹을 추가하거나 제거할 수 있습니다.

### <a name="configure-oms-proxy-settings-in-hello-operations-console"></a>Hello, 운영 콘솔에서 OMS 프록시 설정 구성
Hello 된 내부 프록시 서버 hello 관리 그룹과 OMS 웹 서비스로 사이 있으면 다음 단계를 수행 합니다.  이러한 설정은 hello 관리 그룹과 OMS에 대 한 hello 범위 toocollect 데이터에 포함 된 분산된 tooagent 관리 시스템에서 중앙 집중식으로 관리 됩니다.  이 웹 서비스에 tooOMS 직접 특정 솔루션 hello 관리 서버 및 송신 데이터를 바이패스 하는 경우에 유용 합니다.

1. Operations Manager 콘솔 열기 hello 및 선택 hello **관리** 작업 영역입니다.
2. Operations Management Suite를 확장한 다음 **연결**을 클릭합니다.
3. OMS 연결 보기 hello 클릭 **프록시 서버 구성**합니다.
4. **Operations Management Suite 마법사: 프록시 서버** 페이지에서 **프록시 서버 tooaccess hello Operations Management Suite를 사용 하 여**, 예를 들어 http:// hello 포트 번호로 hello URL을 입력 하 고 클릭 하 고 corpproxy:80 **마침**합니다.

프록시 서버에 인증이 필요한 경우 수행 hello 다음 tooconfigure 자격 증명 및 설정은 toopropagate toomanaged 컴퓨터 tooOMS hello 관리 그룹에 보고 하는 단계입니다.

1. Operations Manager 콘솔 열기 hello 및 선택 hello **관리** 작업 영역입니다.
2. **RunAs 구성**에서 **프로필**을 선택합니다.
3. 열기 hello **System Center Advisor 실행 프로필 프록시** 프로필입니다.
4. Hello 실행 프로필 마법사에서에서 추가 toouse 실행 계정을 클릭 합니다. [실행 계정](https://technet.microsoft.com/library/hh321655.aspx)을 만들거나 기존 계정을 사용할 수 있습니다. 이 계정에는 hello 프록시 서버를 통해 충분 한 사용 권한을 toopass toohave 필요합니다.
5. tooset 계정 toomanage hello, 선택 **선택한 클래스, 그룹 또는 개체**, 클릭 **선택...** **그룹...**을 클릭하여 tooopen hello **그룹 검색** 상자입니다.
6. **Microsoft System Center Advisor 모니터링 서버 그룹**을 검색한 다음 선택합니다.  클릭 **확인** hello 그룹 tooclose hello를 선택한 후 **그룹 검색** 상자입니다.
7. 클릭 **확인** tooclose hello **실행 계정을 추가** 상자입니다.
8. 클릭 **저장** toocomplete 마법사 hello 하 고 변경 내용을 저장 합니다.

Hello 연결 생성 후 에이전트는 수집 하 고 데이터 tooOMS을 보고 구성할 hello 다음 구성이 적용 되 순서에 관계 없이 hello 관리 그룹:

* 실행 계정 hello **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** 만들어집니다.  hello 계정으로 실행 프로필과 연결 되어 **Microsoft System Center Advisor 실행으로 프로필 Blob** -두 개의 클래스를 대상으로 하 고 **컬렉션 서버** 및 **Operations Manager 관리 그룹** .
* 두 개의 커넥터가 생성됩니다.  hello 먼저 라는 **Microsoft.SystemCenter.Advisor.DataConnector** hello 관리 그룹 tooOMS 로그의에서 모든 클래스의 인스턴스로 생성 된 모든 경고를 전달 하는 구독에 자동으로 구성 되 고 분석 합니다. hello 두 번째 커넥터는 **Advisor 커넥터**를 담당 하는 OMS 웹 서비스와 통신 하 고 데이터 공유 합니다.
* 에이전트 및 hello 관리 그룹의 toocollect 데이터 선택한 그룹 toohello 추가 되며 **Microsoft System Center Advisor 모니터링 서버 그룹**합니다.

## <a name="management-pack-updates"></a>관리 팩 업데이트
구성이 완료 되 면 hello Operations Manager 관리 그룹 hello OMS 서비스와의 연결을 설정 합니다.  hello 관리 서버 hello 웹 서비스와 동기화 하 고 Operations Manager와 통합 하는 사용 하도록 설정한 hello 솔루션에 대 한 관리 팩의 hello 형태로 업데이트 된 구성 정보를 수신 합니다.   Operations Manager는 이러한 관리 팩의 업데이트를 확인하고 사용할 수 있을 때 자동으로 다운로드하고 가져옵니다.  특히 이 동작을 제어하는 두 개의 규칙이 있습니다.

* **Microsoft.SystemCenter.Advisor.MPUpdate** -hello 기본 OMS 관리 팩을 업데이트 합니다. 기본적으로 12시간마다 실행됩니다.
* **Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** - 작업 영역에서 활성화된 솔루션 관리 팩을 업데이트합니다. 기본적으로 5분마다 실행됩니다.

Tooeither, 비활성화 하 여 자동 다운로드를 금지 하는이 두 가지 규칙을 재정의 하거나 얼마나 자주 hello 관리 서버와 동기화 OMS toodetermine 새 관리 팩을 다운로드 해야 사용할 수 있고 경우에 대 한 hello 빈도 수정할 수 있습니다.  Hello 단계에 따라 [어떻게 tooOverride 규칙 또는 모니터](https://technet.microsoft.com/library/hh212869.aspx) toomodify hello **주파수** toochange 시간 (초)의에서 값이 매개 변수 동기화 일정을 hello 또는 hello 수정 **사용**  toodisable hello 규칙 매개 변수입니다.  대상 hello tooall 클래스 개체를 Operations Manager 관리 그룹을 재정의합니다.

Toocontinue 프로덕션 관리 그룹의 관리 팩 릴리스를 제어 하기 위한 기존 변경 제어 프로세스를 수행 하려는 경우에 hello 규칙을 사용 하지 않도록 설정할 수 있으며 업데이트 허용 되는 경우 특정 시간 동안 사용할 수 있도록 수 있습니다. 개발 또는 QA 관리 그룹 환경에 있는 연결 toohello 인터넷이이 시나리오는 OMS 작업 영역 toosupport와 해당 관리 그룹용 구성할 수 있습니다.  이 tooreview 있으며 프로덕션 관리 그룹에 배포 하 전에 hello 반복 릴리스의 hello OMS 관리 팩을 확인 합니다.

## <a name="switch-an-operations-manager-group-tooa-new-oms-workspace"></a>Operations Manager 그룹 tooa 전환 새로운 OMS 작업 영역
1. Tooyour OMS 구독에 로그인 하 고 작업 영역을 만들어야 [Microsoft Operations Management Suite](http://oms.microsoft.com/)합니다.
2. 선택 hello 및 hello Operations Manager 관리자 역할의 구성원 인 계정으로 Operations Manager 콘솔 열기 hello **관리** 작업 영역입니다.
3. Operations Management Suite를 확장하고 **연결**을 선택합니다.
4. 선택 hello **다시 구성 작업 관리 도구 모음** hello 창의 hello 중간-쪽에 링크 합니다.
5. Hello에 따라 **Operations Management Suite 등록 마법사** 고 hello 전자 메일 주소 또는 전화 번호와 연결 된 새 OMS 작업 영역 hello 관리자 계정의 암호를 입력 합니다.
   
   > [!NOTE]
   > hello **Operations Management Suite 등록 마법사: 작업 영역 선택** 페이지에서는 사용 중인 hello 기존 작업 영역입니다.
   > 
   > 

## <a name="validate-operations-manager-integration-with-oms"></a>OMS와 Operations Manager 통합 유효성 검사
OMS tooOperations Manager 통합 프로그램가 올바르게 되었는지 확인할 수는 몇 가지 방법이 있습니다.

### <a name="tooconfirm-integration-from-hello-oms-portal"></a>hello OMS 포털에서 tooconfirm 통합
1. Hello OMS 포털에서 클릭 hello **설정** 바둑판식으로 배열
2. **연결된 원본**을 선택합니다.
3. Hello System Center Operations Manager 섹션 아래의 hello 표에 데이터를 마지막으로 받은 경우 hello 수의 에이전트 및 상태를 나열 하는 hello 관리 그룹의 hello 이름이 표시 되어야 합니다.
   
   ![oms-settings-connectedsources](./media/log-analytics-om-agents/oms-settings-connectedsources.png)
4. 참고 hello **작업 영역 ID** hello 설정 페이지의 hello 왼쪽 아래에 값입니다.  아래 Operations Manager 관리 그룹을 기준으로 이 값의 유효성을 검사합니다.  

### <a name="tooconfirm-integration-from-hello-operations-console"></a>hello 운영 콘솔에서 tooconfirm 통합
1. Operations Manager 콘솔 열기 hello 및 선택 hello **관리** 작업 영역입니다.
2. 선택 **관리 팩** 및 hello **찾아보십시오:** 텍스트 상자 형식 **Advisor** 또는 **인텔리전스**합니다.
3. Hello 솔루션의 사용 하도록 설정한 경우에 따라 hello 검색 결과에 나열 된 해당 관리 팩을 볼 수 있습니다.  예를 들어 hello 경고 관리 솔루션을 사용 하는 경우 hello 관리 팩 Microsoft System Center Advisor 경고 관리는 hello 목록에.
4. Hello에서 **모니터링** 보기, toohello 탐색 **Operations Management Suite\Health State** 보기.  관리 서버 hello에 선택 **관리 서버 상태** 창 및 hello **세부 정보 보기** 속성에 대 한 hello 값을 확인 하는 창 **인증 서비스 URI** 일치 하는 hello OMS 작업 영역 id입니다.
   
   ![oms-opsmgr-mg-authsvcuri-property-ms](./media/log-analytics-om-agents/oms-opsmgr-mg-authsvcuri-property-ms.png)

## <a name="remove-integration-with-oms"></a>OMS와의 통합 제거
Operations Manager 관리 그룹과 OMS 작업 영역 간의 통합을 더이상 해야하는 경우 일부의 tooproperly hello 연결 필요한 단계와 hello 관리 그룹에서 구성 합니다. hello 다음 절차는 관리 그룹의 hello 참조를 삭제 하 여 OMS 작업 영역을 업데이트 하 고 hello OMS 커넥터를 삭제 한 다음 OMS를 지 원하는 관리 팩을 삭제 합니다.   

Operations Manager와 통합 하는 사용 하도록 설정한 hello 솔루션에 대 한 관리 팩 및 hello OMS 서비스와의 hello 관리 팩 필요한 toosupport 통합 hello 관리 그룹에서 쉽게 삭제할 수 없습니다.  다른 관련된 관리 팩에 대 한 일부 hello OMS 관리 팩 종속성 때문입니다.  hello 스크립트를 다운로드 하는 다른 관리 팩에 종속 toodelete 관리 팩 [종속성이 있는 관리 팩을 제거](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) TechNet 스크립트 센터에서.  

1. Hello Operations Manager 관리자 역할의 구성원 인 계정으로 Operations Manager 명령 셸 hello를 엽니다.
   
    > [!WARNING]
    > 계속 하기 전에 hello 이름에 모든 사용자 지정 관리 팩 hello 단어 관리자 또는 IntelligencePack을 없는, 그렇지 않으면 단계를 수행 하는 hello에서에서 삭제 hello 관리 그룹을 확인 합니다.
    > 

2. Hello 명령 셸 프롬프트에서 입력`Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
3. 그런 다음 `Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
4. tooremove 다른 System Center Advisor 관리에 대 한 종속 되어 있는 남은 관리 팩 팩 hello 스크립트를 사용 하 여, *RecursiveRemove.ps1* 이전 hello TechNet 스크립트 센터에서에서 다운로드 합니다.  
 
    > [!NOTE]
    > Hello Microsoft System Center Advisor 또는 Microsoft System Center Advisor 내부 관리 팩을 삭제 하지 마십시오.  
    >  

5. Hello Operations Manager 관리자 역할의 구성원 인 계정으로 hello Operations Manager 운영 콘솔을 엽니다.
6. **관리**선택, hello **관리 팩** 노드 및 hello **찾아보십시오:** 상자에 입력 합니다 **관리자** hello 확인 다음 관리 팩을 계속 관리 그룹에 가져옵니다.
   
   * Microsoft System Center Advisor
   * Microsoft System Center Advisor Internal
7. Hello OMS 포털에서 클릭 hello **설정** 바둑판식으로 배열입니다.
8. **연결된 원본**을 선택합니다.
9. System Center Operations Manager 섹션 hello 아래 hello 표에 hello 이름이 표시 되어야 tooremove hello 작업 영역에서 원하는 hello 관리 그룹의 합니다.  Hello 열 아래에서 **마지막 데이터**, 클릭 **제거**합니다.  
   
    > [!NOTE]
    > hello **제거** 링크가 제공 됩니다 때까지 14 일 후 hello 연결 된 관리 그룹에서 검색 작업이 없을 경우.  
    > 

10. Tooproceed hello 제거 되도록 tooconfirm 묻는 창이 표시 됩니다.  클릭 **예** tooproceed 합니다. 

toodelete Microsoft.SystemCenter.Advisor.DataConnector 및 Advisor 커넥터의 두 커넥터-hello, tooyour 컴퓨터 아래의 hello PowerShell 스크립트를 저장 및 예제 따르는 hello를 사용 하 여 실행 합니다.

```
    .\OM2012_DeleteConnector.ps1 “Advisor Connector” <ManagementServerName>
    .\OM2012_DeleteConnectors.ps1 “Microsoft.SytemCenter.Advisor.DataConnector” <ManagementServerName>
```

> [!NOTE]
> hello 컴퓨터에서이 스크립트를 실행 하지 않은 경우 관리 서버 hello Operations Manager 명령 셸을 관리 그룹의 hello 버전에 따라 설치 되어 있어야 합니다.
> 
> 

```
    `param(
    [String] $connectorName,
    [String] $msName="localhost"
    )
    $mg = new-object Microsoft.EnterpriseManagement.ManagementGroup $msName
    $admin = $mg.GetConnectorFrameworkAdministration()
    ##########################################################################################
    # Configures a connector with hello specified name.
    ##########################################################################################
    function New-Connector([String] $name)
    {
         $connectorForTest = $null;
         foreach($connector in $admin.GetMonitoringConnectors())
    {
    if($connectorName.Name -eq ${name})
    {
         $connectorForTest = Get-SCOMConnector -id $connector.id
    }
    }
    if ($connectorForTest -eq $null)
    {
         $testConnector = New-Object Microsoft.EnterpriseManagement.ConnectorFramework.ConnectorInfo
         $testConnector.Name = $name
         $testConnector.Description = "${name} Description"
         $testConnector.DiscoveryDataIsManaged = $false
         $connectorForTest = $admin.Setup($testConnector)
         $connectorForTest.Initialize();
    }
    return $connectorForTest
    }
    ##########################################################################################
    # Removes a connector with hello specified name.
    ##########################################################################################
    function Remove-Connector([String] $name)
    {
        $testConnector = $null
        foreach($connector in $admin.GetMonitoringConnectors())
       {
        if($connector.Name -eq ${name})
       {
         $testConnector = Get-SCOMConnector -id $connector.id
       }
      }
     if ($testConnector -ne $null)
     {
        if($testConnector.Initialized)
     {
     foreach($alert in $testConnector.GetMonitoringAlerts())
     {
       $alert.ConnectorId = $null;
       $alert.Update("Delete Connector");
     }
     $testConnector.Uninitialize()
     }
     $connectorIdForTest = $admin.Cleanup($testConnector)
     }
    }
    ##########################################################################################
    # Delete a connector's Subscription
    ##########################################################################################
    function Delete-Subscription([String] $name)
    {
      foreach($testconnector in $admin.GetMonitoringConnectors())
      {
      if($testconnector.Name -eq $name)
      {
        $connector = Get-SCOMConnector -id $testconnector.id
      }
    }
    $subs = $admin.GetConnectorSubscriptions()
    foreach($sub in $subs)
    {
      if($sub.MonitoringConnectorId -eq $connector.id)
      {
        $admin.DeleteConnectorSubscription($admin.GetConnectorSubscription($sub.Id))
      }
     }
    }
    #New-Connector $connectorName
    write-host "Delete-Subscription"
    Delete-Subscription $connectorName
    write-host "Remove-Connector"
    Remove-Connector $connectorName
```

Hello 향후에 관리 그룹 tooan OMS 작업 영역을 다시 연결 하려는 경우 필요한 toore 가져오기 hello `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` hello 최신 업데이트 롤업에서 관리 팩 파일 tooyour 관리 그룹을 적용 합니다.  Hello에서이 파일을 찾을 수 있습니다 `%ProgramFiles%\Microsoft System Center 2012` 또는 hello `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` 폴더입니다.

## <a name="next-steps"></a>다음 단계
tooadd 기능 및 데이터 수집 참조 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.


