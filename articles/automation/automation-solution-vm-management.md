---
title: "업무 시간 이후 [미리 보기] 솔루션 중 Vm aaaStart/중지 | Microsoft Docs"
description: "hello VM 관리 솔루션 시작 및 일정에 따라 Azure 리소스 관리자 가상 컴퓨터를 중지 하 고 사전 예방적으로 로그 분석에서 모니터링 합니다."
services: automation
documentationCenter: 
authors: mgoedtel
manager: carmonm
editor: 
ms.assetid: 06c27f72-ac4c-4923-90a6-21f46db21883
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: magoedte
ms.openlocfilehash: 6cbe16dfb40bf13f29d9e58ca0bc8c5c7979879d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="startstop-vms-during-off-hours-preview-solution-in-automation"></a>Automation의 업무 시간 외 VM 시작/중지 [미리 보기] 솔루션

업무 시간 이후 [미리 보기] 솔루션 중 hello 시작/중지 Vm 시작 하 고 사용자 정의 일정에 따라 Azure 리소스 관리자 가상 컴퓨터를 중지 및 시작 하 고 OMS와 함께 가상 컴퓨터를 중지 하는 hello 자동화 작업의 성공 hello에 대 한 정보를 제공 합니다. 로그 분석 합니다.  

## <a name="prerequisites"></a>필수 조건

- hello runbook 작업을 한 [Azure 실행 계정](automation-offering-get-started.md#authentication-methods)합니다.  실행 계정을 hello hello 기본 설정 인증 방법 이므로 인증서 인증을 사용 하 여 암호 만료 되었거나 자주 변경 하는 대신입니다.  

- 이 솔루션에는 hello에 있는 Vm만 관리할 수 있습니다 hello 자동화 계정이 있는 위치와 같은 구독 합니다.  

- 이 솔루션에는 toohello 오스트레일리아 남동부, 미국 동부, 동남 아시아 및 서 부 유럽 Azure 지역에 따라 배포 됩니다.  hello VM 일정을 관리 하는 hello runbook 모든 지역에서 Vm을 지정할 수 있습니다.  

- toosend 전자 메일 알림을 hello 시작 및 완료 VM runbook을 중지 하는 경우 비즈니스용 Office 365 구독이 필요 합니다.  

## <a name="solution-components"></a>솔루션 구성 요소

이 솔루션의 다음 리소스를 가져오게 됩니다을 tooyour 자동화 계정을 추가 하는 hello 구성 됩니다.

### <a name="runbooks"></a>Runbook

Runbook | 설명|
--------|------------|
CleanSolution-MS-Mgmt-VM | 이 runbook은 구독에서 toodelete hello 솔루션으로 작업할 때 포함 된 모든 리소스 및 일정 제거 됩니다.|  
SendMailO365-MS-Mgmt | 이 Runbook은 Office 365 Exchange를 통해 전자 메일을 보냅니다.|
StartByResourceGroup-MS-Mgmt-VM | 이 runbook은 의도 한 toostart Vm (모두 클래식 및 ARM 기반 Vm) Azure 리소스 그룹의 지정 된 목록에 있는 합니다.
StopByResourceGroup-MS-Mgmt-VM | 이 runbook은 의도 한 toostop Vm (모두 클래식 및 ARM 기반 Vm) Azure 리소스 그룹의 지정 된 목록에 있는 합니다.|
<br>

### <a name="variables"></a>variables

변수 | 설명|
---------|------------|
**SendMailO365-MS-Mgmt** Runbook ||
SendMailO365-IsSendEmail-MS-Mgmt | StartByResourceGroup-MS-Mgmt-VM 및 StopByResourceGroup-MS-Mgmt-VM Runbook이 완료 시 전자 메일 알림을 보낼 수 있는지를 지정합니다.  선택 **True** tooenable 및 **False** toodisable 전자 메일 경고 합니다. 기본값은 **False**입니다.| 
**StartByResourceGroup-MS-Mgmt-VM** Runbook ||
StartByResourceGroup-ExcludeList-MS-Mgmt-VM | VM 이름 toobe 관리 작업에서 제외를 입력 합니다. 공백 없이 semi-colon(;)를 사용 하 여 이름을 구분 합니다. 값은 대/소문자가 구분되며 와일드카드(별표)가 지원됩니다.|
StartByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | 될 수 있는 텍스트가 hello 전자 메일 메시지 본문의 toohello 시작 부분을 추가 합니다.|
StartByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Hello hello hello 전자 메일 runbook이 포함 된 자동화 계정 이름을 지정 합니다.  **이 변수를 수정하지 마십시오.**|
StartByResourceGroup-SendMailO365-EmailRunbookName-MS-Mgmt | Hello 전자 메일 runbook의 hello 이름을 지정합니다.  이 hello StartByResourceGroup MS-Mgmt VM 및 StopByResourceGroup MS-Mgmt VM runbook toosend 전자 메일에서 사용 됩니다.  **이 변수를 수정하지 마십시오.**|
StartByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Hello hello 전자 메일 runbook이 포함 된 hello 리소스 그룹 이름을 지정 합니다.  **이 변수를 수정하지 마십시오.**|
StartByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Hello 전자 메일의 제목 줄 hello에 대 한 hello 텍스트를 지정합니다.|  
StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Hello 전자 메일의 받는 사람 hello를 지정합니다.  공백 없이 세미콜론(;)을 사용하여 구분한 이름을 입력합니다.|
StartByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | VM 이름 toobe 관리 작업에서 제외를 입력 합니다. 공백 없이 semi-colon(;)를 사용 하 여 이름을 구분 합니다. 값은 대/소문자가 구분되며 와일드카드(별표)가 지원됩니다.  기본값 (별표) hello 구독에서 모든 리소스 그룹을 포함 됩니다.|
StartByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | 이 솔루션에서 관리 하는 Vm toobe를 포함 하는 hello 구독을 지정 합니다.  이어야 합니다.이 솔루션의 자동화 계정 hello 상주 하는 동일한 구독 hello 합니다.|
**StopByResourceGroup-MS-Mgmt-VM** Runbook ||
StopByResourceGroup-ExcludeList-MS-Mgmt-VM | VM 이름 toobe 관리 작업에서 제외를 입력 합니다. 공백 없이 semi-colon(;)를 사용 하 여 이름을 구분 합니다. 값은 대/소문자가 구분되며 와일드카드(별표)가 지원됩니다.|
StopByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | 될 수 있는 텍스트가 hello 전자 메일 메시지 본문의 toohello 시작 부분을 추가 합니다.|
StopByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Hello hello hello 전자 메일 runbook이 포함 된 자동화 계정 이름을 지정 합니다.  **이 변수를 수정하지 마십시오.**|
StopByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Hello hello 전자 메일 runbook이 포함 된 hello 리소스 그룹 이름을 지정 합니다.  **이 변수를 수정하지 마십시오.**|
StopByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Hello 전자 메일의 제목 줄 hello에 대 한 hello 텍스트를 지정합니다.|  
StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Hello 전자 메일의 받는 사람 hello를 지정합니다.  공백 없이 세미콜론(;)을 사용하여 구분한 이름을 입력합니다.|
StopByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | VM 이름 toobe 관리 작업에서 제외를 입력 합니다. 공백 없이 semi-colon(;)를 사용 하 여 이름을 구분 합니다. 값은 대/소문자가 구분되며 와일드카드(별표)가 지원됩니다.  기본값 (별표) hello 구독에서 모든 리소스 그룹을 포함 됩니다.|
StopByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | 이 솔루션에서 관리 하는 Vm toobe를 포함 하는 hello 구독을 지정 합니다.  이어야 합니다.이 솔루션의 자동화 계정 hello 상주 하는 동일한 구독 hello 합니다.|  
<br>

### <a name="schedules"></a>일정

일정 | 설명|
---------|------------|
StartByResourceGroup-Schedule-MS-Mgmt | 이 솔루션에서 관리 하는 Vm의 hello 시작을 수행 하는 StartByResourceGroup runbook에 대 한 일정입니다. 를 만들 때 tooUTC 시간대 기본값으로 사용 합니다.|
StopByResourceGroup-Schedule-MS-Mgmt | 이 솔루션에서 관리 하는 Vm의 hello 종료를 수행 하는 StopByResourceGroup runbook에 대 한 일정입니다. 를 만들 때 tooUTC 시간대 기본값으로 사용 합니다.|

### <a name="credentials"></a>자격 증명

자격 증명 | 설명|
-----------|------------|
O365Credential | 유효한 Office 365 사용자 계정 toosend 전자 메일을 지정합니다.  변수 SendMailO365-IsSendEmail-MS-Mgmt 너무 설정 된 경우에 필요**True**합니다.

## <a name="configuration"></a>구성

Hello 단계 tooadd hello 시작/중지 Vm 업무 시간 이후 [미리 보기] 솔루션 tooyour 자동화 계정 하는 동안 다음을 수행 하 고 hello 변수 toocustomize hello 솔루션을 구성 합니다.

1. Hello 홈 화면에 hello Azure 포털에서 선택 hello **마켓플레이스** 바둑판식으로 배열입니다.  Hello 타일은 더 이상 고정 된 tooyour 홈 화면으로 hello 왼쪽된 탐색 창에서 선택 **새로**합니다.  
2. Hello 마켓플레이스 블레이드에서 입력 **VM 시작** hello 검색 상자를 닫은 다음 선택 hello 솔루션에서 **[미리 보기] 근무 시작/중지 Vm** hello 검색 결과에서 합니다.  
3. Hello에 **[미리 보기] 근무 시작/중지 Vm** 블레이드 hello에 대 한 솔루션 선택, hello 요약 정보를 검토 한 다음 클릭 **만들기**합니다.  
4. hello **솔루션 추가** 블레이드 자동화 구독으로 가져오기 전에 증명된 tooconfigure hello 솔루션의 현재 위치를 표시 합니다.<br><br> ![VM 관리 솔루션 추가 블레이드](media/automation-solution-vm-management/vm-management-solution-add-solution-blade.png)<br><br>
5.  Hello에 **솔루션 추가** 블레이드를 **작업 영역** 여기 hello 자동화 계정을 동일한 Azure 구독에는 연결 된 toohello 되었거나 새 OMS 작업 영역을 만들 OMS 작업 영역 선택 합니다.  OMS 작업 영역이 없는 경우 선택할 수 있습니다 **새 작업 영역 만들기** hello에 **OMS 작업 영역** 블레이드 hello 다음을 수행 합니다. 
   - 새 hello에 대 한 이름을 지정 **OMS 작업 영역**합니다.
   - 선택 된 **구독** toolink hello 기본 선택 된 적절 하지 않은 경우 tooby hello 드롭 다운 목록에서 선택 합니다.
   - **리소스 그룹**의 경우, 새 리소스 그룹을 만들거나 기존 리소스 그룹을 선택할 수 있습니다.  
   - **위치**를 선택합니다.  현재 선택 영역에 대해 제공 된 hello 유일한 위치는 **오스트레일리아 남동부**, **미국 동부**, **동남 아시아**, 및 **서 부 유럽**합니다.
   - **가격 책정 계층**을 선택합니다.  두 계층에 hello 솔루션 프린터가: 해제 하 고 OMS 유료 계층입니다.  hello 무료 계층에서는 hello 매일, 보존 기간 및 runbook 작업 런타임 분 수집 된 데이터 양을 제한 합니다.  매일 수집 되는 데이터의 hello 금액에 hello 유료 계층 OMS 제한을 않아도 됩니다.  

        > [!NOTE]
        > 독립 실행형 계층 유료 hello가 옵션으로 표시 하는 동안 적용 되지 않습니다.  선택 하 고 구독에서이 솔루션의 hello 작성을 진행할 경우 실패 합니다.  이 솔루션이 공식적으로 릴리스되면 해결될 것입니다.<br>이 솔루션을 사용하는 경우 Automation 작업 분 및 로그 수집을 사용합니다.  hello 솔루션 추가 OMS 노드 tooyour 환경을 추가 되지 않습니다.  

6. Hello에 hello 필요한 정보를 제공한 후 **OMS 작업 영역** 블레이드에서 클릭 **만들기**합니다.  Hello 정보를 확인 하 고 hello 작업 영역이 만들어진, 아래에서 진행률을 추적할 수 있습니다 **알림** hello 메뉴에서 합니다.  Toohello 돌아가면 **솔루션 추가** 블레이드입니다.  
7. Hello에 **솔루션 추가** 블레이드를 **자동화 계정**합니다.  새로운 OMS 작업 영역을 만들면 됩니다 필요 tooalso hello 새 OMS 작업 영역이 이전에 지정한 Azure 구독, 리소스 그룹 및 영역을 포함 하 여 연결 된 새 자동화 계정 만들기.  선택할 수 있습니다 **자동화 계정 만들기** hello에 **추가 자동화 계정** 블레이드를 hello 다음을 제공 합니다. 
  - Hello에 **이름** 필드의 자동화 계정 hello hello 이름을 입력 합니다.

    다른 모든 옵션 hello OMS 작업 영역이 선택에 따라 자동으로 채워진 및 이러한 옵션을 수정할 수 없습니다.  Azure 계정으로 실행 계정은이 솔루션에 포함 된 hello runbook에 대 한 hello 기본 인증 방법입니다.  클릭 한 후 **확인**hello 구성 옵션은 유효성을 검사 하 고 hello 자동화 계정이 생성 됩니다.  진행률을 추적할 수 있습니다 **알림** hello 메뉴에서 합니다. 

    그렇지 않으면, 기존 Automation 실행 계정을 선택할 수 있습니다.  선택한 hello 계정 이미 없습니다 될 연결 된 tooanother OMS 작업 영역, 그렇지 않으면 메시지에에서 제공 됩니다 hello 블레이드 tooinform 있습니다.  이미 연결 되어 경우 tooselect 다른 자동화 계정으로 실행 계정 또는 새로 만들는 있습니다.<br><br> ![자동화 계정을 연결 이미 된 tooOMS 작업 영역](media/automation-solution-vm-management/vm-management-solution-add-solution-blade-autoacct-warning.png)<br>

8. 마지막으로 hello에 **솔루션 추가** 블레이드를 **구성** 및 hello **매개 변수** 블레이드 나타납니다.  Hello에 **매개 변수** 것인지 묻는 블레이드를 만듭니다.  
   - Hello 지정 **대상 리소스 그룹 이름을**,이 Vm toobe이이 솔루션에서 관리 하는 포함 된 리소스 그룹 이름입니다.  이름은 두 개 이상 입력할 수 있으며 각 이름을 세미콜론(;)으로 구분해야 하고 대/소문자가 구분됩니다.  Hello 구독의 모든 리소스 그룹에 Vm tootarget를 원하는 경우 와일드 카드를 사용 하 여이 지원 됩니다.
   - 선택 된 **일정** 되 되풀이 날짜 및 시간을 시작 하 고 hello에 중지 hello VM의 대상 리소스 그룹입니다.  기본적으로 hello 일정은 구성 된 toohello UTC 표준 시간대와 사용할 수 없으면 다른 지역을 선택 합니다.  Hello 솔루션을 구성한 후 tooconfigure hello 일정 tooyour 특정 표준 시간대를 원하는 경우 참조 [수정 hello 시작 및 종료 일정](#modifying-the-startup-and-shutdown-schedule) 아래 합니다.    

10. Hello 솔루션에 필요한 구성 hello 초기 설정을 완료 되 면 선택 **만들기**합니다.  모든 설정의 유효성을 검사 합니다 하 고 toodeploy hello 솔루션 가입을 시도 합니다.  이 프로세스는 몇 가지 걸릴 수 초 toocomplete 하 고 아래에서 해당 진행률을 추적할 수 **알림** hello 메뉴에서 합니다. 

## <a name="collection-frequency"></a>수집 빈도

자동화 작업 로그 및 작업 스트림 데이터는 수집 된 hello OMS 리포지토리에 5 분 마다.  

## <a name="using-hello-solution"></a>Hello 솔루션을 사용 하 여

Hello VM 관리 솔루션을 OMS 작업 영역 hello에 추가 하면 **StartStopVM 보기** tooyour OMS 대시보드에 타일 추가 됩니다.  이 타일에는 개수 및 시작 되 고 성공적으로 완료 되었는지 여부를 지정 하는 hello 솔루션에 대 한 hello runbook 작업의 그래픽 표현을 표시 합니다.<br><br> ![VM 관리 StartStopVM 보기 타일](media/automation-solution-vm-management/vm-management-solution-startstopvm-view-tile.png)  

자동화 계정에서 액세스 고 hello를 선택 하 여 hello 솔루션을 관리할 수 있습니다 **솔루션** 타일 한 다음 hello **솔루션** hello 솔루션 선택 블레이드 **시작-STOP-VM [ 작업 영역]** hello 목록에서 합니다.<br><br> ![Automation 솔루션 목록](media/automation-solution-vm-management/vm-management-solution-autoaccount-solution-list.png)  

Hello 솔루션을 선택 하는 hello를 표시 합니다 **시작-STOP-VM [작업 영역]** hello와 같은 중요 한 세부 정보를 검토할 수 있는 솔루션 블레이드에서 **StartStopVM** 같은 OMS 작업 영역에서 타일입니다 count 및 시작 되 고 성공적으로 완료 되었는지 여부를 지정 하는 hello 솔루션에 대 한 hello runbook 작업의 그래픽 표현을 표시 합니다.<br><br> ![Automation VM 솔루션 블레이드](media/automation-solution-vm-management/vm-management-solution-solution-blade.png)  

여기에서 OMS 작업 영역을 열고 하 고 추가 hello 작업 레코드의 분석을 위해 수도 있습니다.  클릭 하기만 **모든 설정을**, 및 hello **설정** 블레이드를 **빠른 시작** 한 다음 hello **빠른 시작** 블레이드선택 **OMS 포털**합니다.   새 탭 또는 새 브라우저 세션이 열리고 Automation 계정 및 구독과 관련된 OMS 작업 영역을 제공합니다.  


### <a name="configuring-e-mail-notifications"></a>전자 메일 알림 구성

때 hello tooenable 전자 메일 알림을 시작 하 고 VM runbook 전체 중지를 toomodify hello **O365Credential** 자격 증명 및 여기에 최소한 다음 변수 hello:

 - SendMailO365-IsSendEmail-MS-Mgmt
 - StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt
 - StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt

tooconfigure hello **O365Credential** 자격 증명 hello 다음 단계를 수행 하십시오.

1. 자동화 계정에서 클릭 **모든 설정을** hello 창의 위쪽에 hello 합니다. 
2. Hello에 **설정** hello 섹션에서 블레이드 **자동화 리소스**선택, **자산**합니다. 
3. Hello에 **자산** 블레이드, 선택 hello **자격 증명** 타일 들어오고 hello **자격 증명** 블레이드, 선택 hello **O365Credential**합니다.  
4. 유효한 Office 365 사용자 이름과 암호를 입력 한 다음 클릭 **저장** toosave 변경 내용을 합니다.  

앞에서 강조 표시 tooconfigure hello 변수 hello 다음 단계를 수행 합니다.

1. 자동화 계정에서 클릭 **모든 설정을** hello 창의 위쪽에 hello 합니다. 
2. Hello에 **설정** hello 섹션에서 블레이드 **자동화 리소스**선택, **자산**합니다. 
3. Hello에 **자산** 블레이드, 선택 hello **변수** 타일 들어오고 hello **변수** 블레이드에서 위에 나열 된 hello 변수를 선택 하 고 다음 hello에 해당 값을 수정 hello에 지정 된 것에 대 한 [변수](##variables) 이전 섹션.  
4. 클릭 **저장** toosave hello 변경 toohello 변수입니다.   

### <a name="modifying-hello-startup-and-shutdown-schedule"></a>Hello 시작 및 종료 일정 수정

이 솔루션에서 관리 hello 시작 및 종료 일정 hello에 설명 된 대로 동일한 단계를 따르는 [Azure 자동화에서 runbook 예약](automation-schedules.md)합니다.  기억 hello 일정 구성을 수정할 수 없습니다.  Toodisable 해야 기존 일정을 hello 및 다음 새 만들고 다음 연결 toohello **StartByResourceGroup MS-Mgmt VM** 또는 **StopByResourceGroup MS-Mgmt VM** hello runbook tooapply를 예약 합니다.   

## <a name="log-analytics-records"></a>Log Analytics 레코드

자동화는 hello OMS 리포지토리에 두 종류의 레코드를 만듭니다.

### <a name="job-logs"></a>작업 로그

속성 | 설명|
----------|----------|
Caller |  Hello 작업을 시작한 사람입니다.  가능한 값은 전자 메일 주소 또는 예약된 작업의 시스템입니다.|
Category | Hello 종류의 데이터 분류 합니다.  자동화를 위해 hello 값은 JobLogs입니다.|
CorrelationId | hello hello runbook 작업의 상관 관계 Id는 GUID입니다.|
JobId | hello hello runbook 작업의 Id는 GUID입니다.|
operationName | Azure에서 수행한 작업의 hello 유형을 지정 합니다.  자동화를 위해 hello 값은 작업 됩니다.|
resourceId | Azure의 hello 리소스 종류를 지정합니다.  자동화를 위해 hello 값은 hello runbook과 연결 된 hello 자동화 계정.|
ResourceGroup | Hello runbook 작업의 hello 리소스 그룹 이름을 지정합니다.|
ResourceProvider | Hello hello 리소스 배포 및 관리할 수를 제공 하는 Azure 서비스를 지정 합니다.  자동화를 위해 hello 값은 Azure 자동화입니다.|
ResourceType | Azure의 hello 리소스 종류를 지정합니다.  자동화를 위해 hello 값은 hello runbook과 연결 된 hello 자동화 계정.|
resultType | hello runbook 작업의 hello 상태입니다.  가능한 값은 다음과 같습니다.<br>- 시작됨<br>- 중지됨<br>- 일시 중단됨<br>- 실패<br>- Succeeded입니다.|
resultDescription | Hello runbook 작업 결과 상태를 설명합니다.  가능한 값은 다음과 같습니다.<br>- 작업 시작<br>- 작업 실패<br>- Job Completed입니다.|
RunbookName | Hello runbook의 hello 이름을 지정합니다.|
SourceSystem | 제출 된 데이터를 hello에 대 한 hello 원본 시스템을 지정 합니다.  자동화를 위해 hello 값 됩니다: OpsManager|
StreamType | Hello 유형의 이벤트를 지정합니다. 가능한 값은 다음과 같습니다.<br>- Verbose입니다.<br>- 출력<br>- 오류<br>- 경고|
SubscriptionId | Hello 작업의 hello 구독 ID를 지정합니다.
Time | 날짜 및 hello runbook 작업 실행 시간입니다.|


### <a name="job-streams"></a>작업 스트림

속성 | 설명|
----------|----------|
Caller |  Hello 작업을 시작한 사람입니다.  가능한 값은 전자 메일 주소 또는 예약된 작업의 시스템입니다.|
Category | Hello 종류의 데이터 분류 합니다.  자동화를 위해 hello 값은 JobStreams입니다.|
JobId | hello hello runbook 작업의 Id는 GUID입니다.|
operationName | Azure에서 수행한 작업의 hello 유형을 지정 합니다.  자동화를 위해 hello 값은 작업 됩니다.|
ResourceGroup | Hello runbook 작업의 hello 리소스 그룹 이름을 지정합니다.|
resourceId | Azure의 hello 리소스 Id를 지정합니다.  자동화를 위해 hello 값은 hello runbook과 연결 된 hello 자동화 계정.|
ResourceProvider | Hello hello 리소스 배포 및 관리할 수를 제공 하는 Azure 서비스를 지정 합니다.  자동화를 위해 hello 값은 Azure 자동화입니다.|
ResourceType | Azure의 hello 리소스 종류를 지정합니다.  자동화를 위해 hello 값은 hello runbook과 연결 된 hello 자동화 계정.|
resultType | hello 시간 hello 이벤트에서 hello runbook 작업의 hello 결과 생성 되었습니다.  가능한 값은 다음과 같습니다.<br>- InProgress입니다.|
resultDescription | Hello runbook에서 출력 스트림에 hello 포함 되어 있습니다.|
RunbookName | hello runbook의 hello 이름입니다.|
SourceSystem | 제출 된 데이터를 hello에 대 한 hello 원본 시스템을 지정 합니다.  자동화를 위해 hello 값 OpsManager 됩니다.|
StreamType | 작업 스트림의 hello 형식입니다. 가능한 값은 다음과 같습니다.<br>- 진행<br>- 출력<br>- 경고<br>- 오류<br>- 디버그<br>- Verbose입니다.|
Time | 날짜 및 hello runbook 작업 실행 시간입니다.|

레코드의 범주를 반환 하는 모든 로그 검색을 수행 하는 경우 **JobLogs** 또는 **JobStreams**, hello를 선택할 수 있습니다 **JobLogs** 또는 **JobStreams** hello 검색에서 반환 된 hello 업데이트 요약 타일의 집합을 표시 하는 보기입니다.

## <a name="sample-log-searches"></a>샘플 로그 검색

hello 다음 표에서이 솔루션에 의해 수집 된 작업 레코드에 대 한 예제 로그 검색. 

쿼리 | 설명|
----------|----------|
성공적으로 완료된 StartVM Runbook에 대한 작업을 찾습니다. | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Succeeded &#124; measure count() by JobId_g|
성공적으로 완료된 StopVM Runbook에 대한 작업을 찾습니다. | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Failed &#124; measure count() by JobId_g
StartVM 및 StopVM Runbook의 시간에 따른 작업 상태를 보여줍니다. | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" OR "StopByResourceGroup-MS-Mgmt-VM" NOT(ResultType="started") | measure Count() by ResultType interval 1day|

## <a name="removing-hello-solution"></a>Hello 솔루션을 제거

더 이상 toouse hello 솔루션이 필요한 모든 추가 결정 한 경우에 hello 자동화 계정에서에서 삭제할 수 없습니다.  Hello 솔루션을 삭제 하면 hello runbook만 제거 됩니다, 그리고 hello 일정 또는 hello 솔루션 추가 될 때 생성 된 변수는 삭제 되지 않습니다.  이러한 자산 해야 toodelete 수동으로 다른 runbook에 사용 하지 않는 경우.  

toodelete 솔루션 hello hello 다음 단계를 수행 하십시오.

1.  자동화 계정에서 선택 hello **솔루션** 바둑판식으로 배열입니다.  
2.  Hello에 **솔루션** 블레이드, 선택 hello 솔루션 **시작-STOP-VM [작업 영역]**합니다.  Hello에 **VMManagementSolution [작업 영역]** 블레이드 hello 메뉴 클릭에서 **삭제**합니다.<br><br> ![VM Mgmt 솔루션 삭제](media/automation-solution-vm-management/vm-management-solution-delete.png)
3.  Hello에 **솔루션 삭제** 창 toodelete hello 솔루션을 확인 합니다.
4.  Hello 정보를 확인 하 고 hello 솔루션이 삭제, 아래에서 진행률을 추적할 수 있습니다 **알림** hello 메뉴에서 합니다.  Toohello 돌아가면 **VMManagementSolution [작업 영역]** 블레이드 hello 프로세스 tooremove 솔루션 시작 된 후입니다.  

이 프로세스의 일부로 hello 자동화 계정 및 OMS 작업 영역 삭제 되지 않습니다.  Tooretain hello OMS 작업 영역을 하지 않을 경우 해야 toomanually 삭제 합니다.  이 hello Azure 포털에서에서도 수행할 수 있습니다.   Hello 홈 화면에 hello Azure 포털에서 선택 **로그 분석** hello에서 **로그 분석** 블레이드, 작업 영역 선택 hello 및 클릭 **삭제** hello 메뉴에서 작업 영역 설정 블레이드에서 hello 합니다.  
      
## <a name="next-steps"></a>다음 단계

- toolearn 어떻게 tooconstruct 다른 검색 쿼리 및 검토 hello 자동화 작업 로그 분석을 사용 하 여 로그에 대 한 자세한 참조 [로그 분석 검색 로그인](../log-analytics/log-analytics-log-searches.md)
- toolearn toomonitor runbook 작업 및 기타 기술 정보가 참조 하는 방법 runbook 실행에 대 한 자세한 [runbook 작업을 추적 합니다.](automation-runbook-execution.md)
- OMS 로그 분석 및 데이터 컬렉션 원본에 대해 자세히 toolearn 참조 [로그 분석 개요에서 수집 하는 Azure 저장소 데이터](../log-analytics/log-analytics-azure-storage.md)






   

