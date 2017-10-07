---
title: "Azure 실행 계정 aaaConfigure | Microsoft Docs"
description: "이 자습서에서는 Azure 자동화의 보안 주체 인증 hello 작성, 테스트 및 예제 사용을 안내합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: "서비스 주체 이름, setspn, azure 인증"
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a>Azure 실행 계정으로 Runbook 인증
이 문서에서는 hello Azure 포털에에서 tooconfigure Azure 자동화 계정 하는 방법을 설명 합니다. toodo 때문 hello 계정으로 실행 계정 기능은 tooauthenticate runbook에서 Azure 리소스 관리자 또는 Azure 서비스 관리 리소스 관리를 사용 합니다.

Hello Azure 포털에서에서 자동화 계정을 만들면 두 개의 계정을 자동으로 만듭니다.

* 실행 계정 이 계정은 Azure AD(Azure Active Directory)의 서비스 주체 및 인증서를 만듭니다. 또한 hello 참가자 역할 기반 액세스 제어 (RBAC) runbook을 사용 하 여 리소스 관리자 리소스를 관리 하는 할당 합니다.
* 클래식 실행 계정 이 계정에는 관리 인증서를 업로드 runbook을 사용 하 여 서비스 관리 toomanage 또는 클래식 리소스를 사용 합니다.

자동화 계정 및 빌드 및 배포 runbook toosupport 빠르게 시작할 수에 대 한 hello 프로세스를 간소화 하는 자동화를 작성 해야 합니다.

실행 계정 및 클래식 실행 계정을 사용하여 다음 작업을 수행할 수 있습니다.

* Hello Azure 포털에서에서 runbook에서 리소스 관리자 또는 서비스 관리 리소스를 관리 하는 경우 Azure에 표준화 된 방식으로 tooauthenticate를 제공 합니다.
* Hello를 사용 하 여 Azure Alerts에서 구성할 수 있는 글로벌 runbook을 자동화 합니다.

> [!NOTE]
> hello [Azure 경고 통합 기능](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) 자동화 with 글로벌 runbook이 실행 계정 및 기존 실행 계정을 사용 하 여 구성 된 자동화 계정이 있어야 합니다. 가 다음 계정으로 실행 및 클래식 계정으로 실행 계정, 이미 정의 되어 있는 자동화 계정을 선택 하거나 새 자동화 계정 toocreate를 선택할 수 있습니다.
>  

이 문서는 toocreate hello Azure 포털에서에서 자동화 계정을 Azure PowerShell을 사용 하 여 자동화 계정을 업데이트할 hello 계정 구성을 관리 하 고 한 runbook에서 인증 방법을 보여줍니다.

자동화 계정 만들기를 시작 하기 전에 좋습니다 toounderstand 되며 hello 다음을 고려 하세요.

* 자동화 계정을 만드는 자동화 계정을 클래식 hello 또는 리소스 관리자 배포 모델에서 이미 만든 영향을 주지 않습니다.
* hello hello Azure 포털에서에서 만든 자동화 계정에 대해서만 작동 합니다. Toocreate hello Azure 클래식 포털에서에서이 계정이 시도 hello 계정으로 실행 계정 구성을 복제 하지 않습니다.
* Runbook과 자산 (예: 일정 또는 변수)에 이미 내부 toomanage 클래식 리소스는 경우 hello 새 클래식 실행 계정에 runbook tooauthenticate hello 다음 중 하나를 수행 합니다.

  * toocreate 클래식 계정으로 실행 계정 "실행 계정 관리" 섹션 hello에에서 hello 지침을 따르십시오. 
  * tooupdate hello "PowerShell을 사용 하 여 자동화 계정을 업데이트" 섹션에서 기존 계정에 사용 하 여 hello PowerShell 스크립트입니다.
* 기존 runbook으로 hello hello 섹션에 제공 된 예제 코드 toomodify 해야 hello 새 실행 계정 및 클래식 실행으로 자동화 계정을 사용 하 여 tooauthenticate, [인증 코드 예제](#authentication-code-examples)합니다.

    >[!NOTE]
    >실행 계정을 hello hello 인증서 기반 서비스 사용자를 사용 하 여 리소스 관리자 리소스에 대 한 인증입니다. hello 클래식 실행 계정 관리 인증서를 사용 하 여 서비스 관리 리소스에 대해 인증을 수행 하기 위해 사용 되며

## <a name="create-an-automation-account-from-hello-azure-portal"></a>Hello Azure 포털에서에서 자동화 계정 만들기
이 섹션에서는 hello 실행 계정을 클래식 실행 계정을 만들 Azure 포털에서에서 Azure 자동화 계정을 만듭니다.

>[!NOTE]
>자동화 계정을 toocreate hello 서비스 관리자가 관리자 역할의 멤버 또는 toohello 구독 액세스 권한을 부여 하는 hello 구독의 공동 관리자 여야 합니다. 사용자 toothat 구독 기본 Active Directory 인스턴스로 추가 해야 합니다. hello 계정 권한 있는 역할 할당 toobe가 필요는 없습니다.
>
>Toohello hello 구독 공동 관리자 역할을 추가 하기 전에 hello 구독 Active Directory 인스턴스에서 소속 없는, 경우 추가 tooActive 디렉터리에 게스트로 합니다. 이 인스턴스에서 받게 됩니다는 "없는 사용 권한을 toocreate..." hello에 경고 **자동화 계정 추가** 블레이드입니다.
>
>먼저 hello 구독 Active Directory 인스턴스에서 제거할 수도 있고 toomake 다시 추가 toohello 공동 관리자 역할에 추가 된 사용자를 해당 Active Directory에서 전체 사용자입니다. tooverify hello이이 상황이 **Azure Active Directory** hello 선택 하 여 Azure 포털의에서 창 **사용자 및 그룹**선택한 **모든 사용자에 게** 및 선택한 후 hello 특정 사용자를 선택 하면 **프로필**합니다. 값의 hello hello **사용자 유형** hello 사용자 프로필 아래에 특성 같지 해야 **게스트**합니다.
>

1. Toohello hello 구독 관리자 역할의 구성원 및 hello 구독의 공동 관리자 인 계정으로 Azure 포털에에서 로그인 합니다.

2. **Automation 계정**을 선택합니다.

3. Hello에 **자동화 계정을** 블레이드에서 클릭 **추가**합니다.
hello **자동화 계정 추가** 블레이드를 엽니다.

 ![hello "자동화 계정 추가" 블레이드](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > 다음 경고 hello hello에 표시 되 사용자 계정이 아닌 경우 hello 구독 관리자 역할의 구성원 및 hello 구독의 공동 관리자를 **자동화 계정 추가** 블레이드:
   >
   >![Automation 계정 경고 추가](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. Hello에 **자동화 계정 추가** 블레이드 hello **이름** 상자 새 자동화 계정에 대 한 이름을 입력 합니다.

5. 둘 이상의 구독을 보유 하는 경우 다음 hello지 않습니다.

    a. 아래 **구독**, hello 새 계정에 대해 하나를 지정 합니다.

    b. **리소스 그룹** 아래에서 **새로 만들기** 또는 **기존 항목 사용**을 클릭합니다.

    c. **위치** 아래에서 Azure 데이터 센터를 지정합니다.

6. **Azure 실행 계정 만들기** 아래에서 **예**를 선택하고 **만들기**를 클릭합니다.

   > [!NOTE]
   > 하지 toocreate hello 실행 계정을 선택 하 여 선택 하면 **아니요**, 경고 메시지가 표시 됩니다 hello **자동화 계정 추가** 블레이드입니다. Hello 계정 hello Azure 포털에서에서 만들어지지만 프로그램 클래식 또는 리소스 관리자 구독 디렉터리 서비스 내에서 해당 인증 id가 없는 합니다. 따라서 hello 계정을 구독에 없는 액세스 tooresources에 있습니다. 이 시나리오는 이 계정을 참조하는 Runbook이 그러한 배포 모델의 리소스에 대해 작업을 인증하고 수행하지 않도록 방지합니다.
   >
   > ![Hello "자동화 계정 추가" 블레이드에서 경고 메시지](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > 또한 hello 서비스 사용자를 만들지 않은 때문에 hello 참가자 역할 할당 되지 않았습니다.
   >

7. Azure 자동화 계정을 hello를 만드는 동안에 아래 hello 진행률을 추적할 수 **알림** hello 메뉴에서 합니다.

### <a name="resources"></a>리소스
Hello 자동화 계정을 성공적으로 만들어지면 여러 리소스를 자동으로 만들어집니다. hello 리소스는 다음 두 표 hello에 요약 되어 있습니다.

#### <a name="run-as-account-resources"></a>실행 계정 리소스

| 리소스 | 설명 |
| --- | --- |
| AzureAutomationTutorial Runbook | 예제 그래픽 runbook을 사용 하 여 tooauthenticate 실행 계정을 hello 하는 방법을 보여 줍니다. 모든 hello 리소스 관리자 리소스를 가져옵니다. |
| AzureAutomationTutorialScript Runbook | 예제 PowerShell runbook을 사용 하 여 tooauthenticate 실행 계정을 hello 하는 방법을 보여 줍니다. 모든 hello 리소스 관리자 리소스를 가져옵니다. |
| AzureRunAsCertificate | 자동화 계정을 만들거나 기존 계정에 대 한 PowerShell 스크립트 뒤 hello를 사용 하는 경우 자동으로 만들어지는 hello 인증서 자산 hello 인증서 하면 Azure와 tooauthenticate runbook에서 Azure 리소스 관리자 리소스를 관리할 수 있도록 합니다. hello 인증서에는 1 년 수명이 있습니다. |
| AzureRunAsConnection | 자동화 계정을 만들거나 기존 계정에 대 한 hello PowerShell 스크립트를 사용 하 여 때 자동으로 만들어지는 hello 연결 자산 |

#### <a name="classic-run-as-account-resources"></a>클래식 실행 계정 리소스

| 리소스 | 설명 |
| --- | --- |
| AzureClassicAutomationTutorial Runbook | 구독에 hello 클래식 배포 모델을 사용 하 여 hello 클래식 실행 계정 (인증서)를 사용 하 여 만들어지고 다음 hello VM 이름 및 상태를 기록 하는 모든 hello Vm을 가져오는 예제 그래픽 runbook입니다. |
| AzureClassicAutomationTutorial Script Runbook | 모두 가져오는 하는 예제 PowerShell runbook hello 클래식 실행 계정 (인증서)를 사용 하 여 구독에 클래식 Vm hello 및 VM 이름 및 상태 쓰기의 hello 다음 합니다. |
| AzureClassicRunAsCertificate | runbook에서 Azure 클래식 리소스를 관리할 수 있도록 tooauthenticate Azure와 함께 사용 하는 인증서 자산을 hello 자동으로 생성 됩니다. hello 인증서에는 1 년 수명이 있습니다. |
| AzureClassicRunAsConnection | runbook에서 Azure 클래식 리소스를 관리할 수 있도록 tooauthenticate Azure와 함께 사용 하는 자동으로 만들어진된 연결 자산을 hello 합니다. |

## <a name="verify-run-as-authentication"></a>실행 인증 확인
Hello 새 실행 계정을 사용 하 여 성공적으로 인증할 수 있는 작은 테스트 tooconfirm를 수행 합니다.

1. Hello Azure 포털에서에서 앞에서 만든 hello 자동화 계정을 엽니다.

2. Hello 클릭 **Runbook** runbook의 타일 tooopen hello 목록입니다.

3. 선택 hello **AzureAutomationTutorialScript** runbook을 클릭 하 고 **시작** toostart hello runbook입니다. hello 다음 이벤트가 발생 합니다.
 * A [runbook 작업](automation-runbook-execution.md) 만들어지면 hello **작업** 블레이드에 표시 되 고 hello에 hello 작업 상태가 표시 되 **작업 요약** 바둑판식으로 배열입니다.
 * 작업 상태 hello로 시작 **큐 대기**를 사용할 수 있는 hello 클라우드 toobecome에 runbook worker를 대기 하 고 있음을 나타내는입니다.
 * hello 상태가 **시작** 작업자 hello 작업을 주장 하는 경우.
 * hello 상태가 **실행** hello runbook 실행을 시작할 때입니다.
 * 상태를 확인할 해야 hello runbook 작업 실행이 완료 되었을 때 **Completed**합니다.

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. toosee hello runbook의 자세한 결과 hello, hello 클릭 **출력** 바둑판식으로 배열입니다.  
hello **출력** 블레이드가 표시 되며, 해당 hello runbook에 성공적으로 인증 하 고 hello 리소스 그룹에서 사용할 수 있는 모든 리소스의 목록을 반환 했습니다.

5. 닫기 hello **출력** 블레이드 tooreturn toohello **작업 요약** 블레이드입니다.

6. 닫기 hello **작업 요약** 블레이드와 해당 하는 hello **AzureAutomationTutorialScript** runbook 블레이드에서 합니다.

## <a name="verify-classic-run-as-authentication"></a>클래식 실행 인증 확인
비슷한 작은 수행 tooconfirm hello 클래식으로 새 실행 계정을 사용 하 여 성공적으로 인증할 수 있는 테스트 합니다.

1. Hello Azure 포털에서에서 앞에서 만든 hello 자동화 계정을 엽니다.

2. Hello 클릭 **Runbook** runbook의 타일 tooopen hello 목록입니다.

3. 선택 hello **AzureClassicAutomationTutorialScript** runbook을 클릭 하 고 **시작** 너무 hello runbook을 시작 합니다. hello 다음 이벤트가 발생 합니다.

 * A [runbook 작업](automation-runbook-execution.md) 만들어지면 hello **작업** 블레이드에 표시 되 고 hello에 hello 작업 상태가 표시 되 **작업 요약** 바둑판식으로 배열입니다.
 * 작업 상태 hello로 시작 **큐 대기**를 사용할 수 있는 hello 클라우드 toobecome에 runbook worker를 대기 하 고 있음을 나타내는입니다.
 * hello 상태가 **시작** 작업자 hello 작업을 주장 하는 경우.
 * hello 상태가 **실행** hello runbook 실행을 시작할 때입니다.
 * 상태를 확인할 해야 hello runbook 작업 실행이 완료 되었을 때 **Completed**합니다.

    ![보안 주체 Runbook 테스트](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. toosee hello runbook의 자세한 결과 hello, hello 클릭 **출력** 바둑판식으로 배열입니다.  
hello **출력** 블레이드가 표시 되며, 해당 hello runbook에 성공적으로 인증 하 고 hello 구독에서 모든 클래식 Vm의 목록을 반환 했습니다.

5. 닫기 hello **출력** 블레이드 tooreturn toohello **작업 요약** 블레이드입니다.

6. 닫기 hello **작업 요약** 블레이드와 해당 하는 hello **AzureAutomationTutorialScript** runbook 블레이드에서 합니다.

## <a name="managing-your-run-as-account"></a>Azure 실행 계정 관리
어느 시점 자동화 계정 만료 되기 전에 인증서가 필요 toorenew hello 합니다. 실행 계정이 해당 hello가 손상 된 경우 삭제 한 다시 만들 수 있습니다. 이 섹션에서는 어떻게 tooperform 이러한 작업 합니다.

### <a name="self-signed-certificate-renewal"></a>자체 서명된 인증서 갱신
hello 실행 계정에 대해 만든 자체 서명 된 인증서를 hello hello 생성 날짜 로부터 1 년에 만료 됩니다. 만료되기 전에 언제든지 갱신할 수 있습니다. Hello 현재 유효한 인증서를 갱신 하기 경우 보존된 tooensure 하는 최대 또는 적극적으로 실행 되 고 실행 계정 hello로 인증 하는 모든 runbook 부정적인 영향을 받지 않습니다. hello 인증서 만료 날짜까지 유효합니다.

> [!NOTE]
> 프로그램 엔터프라이즈 인증 기관에서 발급 한 인증서의 자동화 계정으로 실행 계정 toouse 구성한 경우이 옵션을 사용 하는 경우에 hello 엔터프라이즈 인증서 자체 서명 된 인증서로 바뀝니다.

toorenew hello 인증서, 다음 hello지 않습니다.

1. Hello Azure 포털에서에서 자동화 계정을 hello를 엽니다.

2. Hello에 **자동화 계정** hello에 블레이드 **속성 계정** 창 아래에서 **계정 설정**선택, **실행 계정**합니다.

    ![Automation 계정 속성 창](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. Hello에 **실행 계정** 속성 블레이드를 선택 하거나 hello 계정 또는 계정으로 실행 hello 클래식 계정으로 실행에 대 한 toorenew hello 인증서 원하는 합니다.

4. Hello에 **속성** 블레이드 hello에 대 한 계정 선택, 클릭 **갱신 인증서**합니다.

    ![실행 계정용 인증서 갱신](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. Hello 인증서를 갱신 하는 동안에 아래 hello 진행률을 추적할 수 **알림** hello 메뉴에서 합니다.

### <a name="delete-a-run-as-or-classic-run-as-account"></a>실행 또는 클래식 실행 계정 삭제
이 섹션에서는 설명 방법을 toodelete 다시 실행 또는 클래식 실행 계정을 만듭니다. 이 작업을 수행 하는 경우 자동화 계정을 hello 유지 됩니다. 다음 계정으로 실행 또는 클래식 계정으로 실행 계정을 삭제 한 후 hello Azure 포털에에서 다시 만들 수 있습니다.

1. Hello Azure 포털에서에서 자동화 계정을 hello를 엽니다.

2. Hello에 **자동화 계정** hello 계정 속성 창에서 선택 블레이드 **실행 계정**합니다.

3. Hello에 **실행 계정** toodelete 원하는 계정 속성 블레이드를 선택 하거나 hello 실행 계정 또는 클래식 계정으로 실행 합니다. 그런 다음 hello **속성** 블레이드 hello에 대 한 계정 선택, 클릭 **삭제**합니다.

 ![실행 계정 삭제](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. Hello 계정을 삭제 하는 동안에 아래 hello 진행률을 추적할 수 **알림** hello 메뉴에서 합니다.

5. Hello 계정을 삭제 한 후 다시 만들 수 있습니다이 hello에 **실행 계정** hello를 선택 하 여 속성 블레이드 생성 옵션 **Azure 실행 계정**합니다.

 ![Hello 자동화 계정으로 실행 계정을 다시 만드는](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a>잘못된 구성
Hello 계정으로 실행 또는 클래식 실행 계정 toofunction에 필요한 일부 구성 항목 제대로 수 삭제 되거나 부적절 하 게 초기 설치 중에 생성 합니다. hello 항목은 다음과 같습니다.

* 인증서 자산
* 연결 자산
* 실행 계정은 hello 참가자 역할에서 제거 되었습니다.
* Azure AD의 서비스 주체 또는 응용 프로그램

위의 hello 및 잘못 된 구성의 다른 인스턴스 hello 자동화 계정을 검색 hello 변경의 상태를 표시 하 고 *완료 안 됨* hello에 **실행 계정** hello에 대 한 속성 블레이드 계정입니다.

![불완전 실행 계정 구성 상태](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

Hello 실행 계정을 선택 하면 계정 hello **속성** 창 hello 다음과 같은 오류 메시지가 표시 됩니다.

![불완전 실행 계정 구성 경고 메시지](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)에서도 확인할 수 있습니다.

삭제 및 다시 hello 계정을 작성 하 여 이러한 계정으로 실행 계정 문제를 신속 하 게 해결할 수 있습니다.

## <a name="update-your-automation-account-by-using-powershell"></a>PowerShell을 사용하여 Automation 계정 업데이트
경우 기존 자동화 계정을 PowerShell tooupdate을 사용할 수 있습니다.

* 자동화 계정을 만들지만 toocreate hello 계정으로 실행을 거부 합니다.
* 자동화 계정 toomanage 리소스 관리자 리소스를 이미 사용 중이 고 tooupdate hello 계정 tooinclude hello 실행 계정을 runbook 인증에 대 한 합니다.
* 자동화 계정 toomanage 클래식 리소스를 이미 사용 중이 고 tooupdate 것 toouse hello 클래식 실행 계정 대신 새 계정을 만들고 runbook과 자산 tooit 마이그레이션.   
* Toocreate 실행 하 고 기본 실행 계정을 사용 하 여 원하는 엔터프라이즈 인증 기관 (CA)에서 발급 한 인증서입니다.

hello 스크립트에 다음 필수 구성 요소는 hello:

* Azure 리소스 관리자 모듈 2.01 이상 hello 스크립트를 Windows 10 및 Windows Server 2016에 대해서만 실행할 수 있습니다. 이전 버전의 Windows에서는 지원되지 않습니다.
* Azure PowerShell 1.0 이상 PowerShell 1.0 hello 릴리스에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.
* Hello에 대 한 hello 값으로 참조 하는 자동화 계정을 *– AutomationAccountName* 및 *-ApplicationDisplayName* hello PowerShell 스크립트 뒤에 매개 변수입니다.

tooget hello에 대 한 값 *SubscriptionID*, *ResourceGroup*, 및 *AutomationAccountName*, hello 스크립트에 대 한 필수 매개 변수는, 다음 hello지 않습니다.
1. Hello Azure 포털에서 hello에서 자동화 계정을 선택 **자동화 계정** 블레이드에서 다음을 선택 하 고 **모든 설정을**합니다. 
2. Hello에 **모든 설정을** 블레이드 아래 **계정 설정**선택, **속성**합니다. 
3. Hello에 hello 값을 기록 **속성** 블레이드입니다.

![hello 자동화 계정 "속성" 블레이드](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a>실행 계정 PowerShell 스크립트 만들기
이 PowerShell 스크립트는 구성을 따르고 hello에 대 한 지원이 포함 됩니다.

* 자체 서명된 인증서를 사용하여 실행 계정을 만듭니다.
* 자체 서명된 인증서를 사용하여 실행 계정 및 클래식 실행 계정을 만듭니다.
* 엔터프라이즈 인증서를 사용하여 실행 계정 및 클래식 실행 계정을 만듭니다.
* Hello Azure Government 클라우드에서에서 자체 서명 된 인증서를 사용 하 여 실행 계정 및 기존 실행 계정을 만듭니다.

선택한 hello 구성 옵션에 따라 hello 스크립트 hello 다음 항목을 만듭니다.

**실행 계정의 경우:**

* 만듭니다는 Azure AD 응용 프로그램 toobe 자체 서명 하거나 hello를 사용 하 여 내보낸 또는 엔터프라이즈 인증서 공개 키를 hello 응용 프로그램에 대 한 서비스 사용자 계정에 Azure AD를 만들고 할당 hello 후 현재에서 hello 계정에 대 한 참가자 역할 구독입니다. 이 설정은 tooOwner 또는 다른 역할을 변경할 수 있습니다. 자세한 내용은 [Azure Automation의 역할 기반 액세스 제어](automation-role-based-access-control.md)를 참조하세요.
* 명명 된 자동화 인증서 자산을 만듭니다 *AzureRunAsCertificate* hello 자동화 계정을 지정 합니다. hello 인증서 자산 hello Azure AD 응용 프로그램에서 사용 되는 hello 인증서 개인 키를 보유 합니다.
* 명명 된 자동화 연결 자산을 만듭니다 *AzureRunAsConnection* hello 자동화 계정을 지정 합니다. hello applicationId, tenantId, subscriptionId, 및 인증서 지문을 hello 연결 자산을 보유합니다.

**클래식 실행 계정의 경우:**

* 명명 된 자동화 인증서 자산을 만듭니다 *AzureClassicRunAsCertificate* hello 자동화 계정을 지정 합니다. hello 인증서 자산 hello 관리 인증서에 의해 사용 된 hello 인증서 개인 키를 보유 합니다.
* 명명 된 자동화 연결 자산을 만듭니다 *AzureClassicRunAsConnection* hello 자동화 계정을 지정 합니다. hello 연결 자산 hello 구독 이름, subscriptionId, 이름과 인증서 자산을 보유합니다.

>[!NOTE]
> Hello 스크립트를 실행 한 후 기본 계정으로 실행 계정 만들기에 대 한 옵션 중 하나를 선택 하면 업로드 hello 공용 인증서 (.cer 파일 이름 확장명) toohello 관리 저장 hello 구독에 대 한 해당 hello 자동화 계정에 만들어졌습니다.
> 

tooexecute 스크립트 hello 및 hello 인증서를 업로드, 다음 hello지 않습니다.

1. 컴퓨터에서 스크립트를 다음 hello를 저장 합니다. 이 예제에서는 hello 파일 이름으로 저장 *새로 RunAsAccount.ps1*합니다.

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. 사용자 컴퓨터에서 **시작**을 클릭한 다음 관리자 권한으로**Windows PowerShell**을 시작합니다.

3. Hello에서 높은 1 단계에서 만든 hello 스크립트가 포함 된 폴더를 이동 toohello PowerShell 명령줄 셸입니다.

4. 필요한 hello 구성에 대 한 hello 매개 변수 값을 사용 하 여 hello 스크립트를 실행 합니다.

    **자체 서명된 인증서를 사용하여 실행 계정 만들기**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **자체 서명된 인증서를 사용하여 실행 계정 및 클래식 실행 계정 만들기**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **엔터프라이즈 인증서를 사용하여 실행 계정 및 클래식 실행 계정 만들기**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Hello Azure Government 클라우드에서에서 자체 서명 된 인증서를 사용 하 여 실행 계정 및 클래식 계정으로 실행 계정 만들기**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Hello 스크립트 실행 된 후 Azure 사용한 메시지 표시 tooauthenticate 됩니다. Hello 구독 관리자 역할의 구성원 및 hello 구독의 공동 관리자 인 계정으로 로그인 합니다.
    >
    >

Hello 스크립트 성공적으로 실행 된 후에 hello 다음 note:
* Hello 스크립트 만들고 hello 사용자 프로필 아래에 임시 파일 폴더 toohello 저장 자체 서명 된 공용 인증서 (.cer 파일)를 사용 하 여 기존 실행 계정을 만든 경우 *%USERPROFILE%\AppData\Local\Temp*, tooexecute hello PowerShell 세션을 사용 합니다.
* 엔터프라이즈 공용 인증서(.cer 파일)를 사용하여 클래식 실행 계정을 만든 경우 이 인증서를 사용합니다. 에 대 한 hello 지침 [관리 API 인증서 toohello Azure 클래식 포털을 업로드](../azure-api-management-certs.md), hello를 사용 하 여 서비스 관리 리소스와 hello 자격 증명 구성의 유효성을 검사 하 [샘플 코드 서비스 관리 리소스를 tooauthenticate](#sample-code-to-authenticate-with-service-management-resources)합니다. 
* 작업을 수행한 경우 *하지* 클래식 실행 계정을 만들고 리소스 관리자 리소스를 사용 하 여 인증 hello를 사용 하 여 hello 자격 증명 구성 유효성 검사 [서비스 관리를 사용 하 여 인증에 대 한 코드 샘플 리소스](#sample-code-to-authenticate-with-resource-manager-resources)합니다.

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a>리소스 관리자 리소스와 코드 tooauthenticate 샘플
Hello 다음 업데이트를 사용할 수 있습니다 예제 코드, hello에서 가져온 *AzureAutomationTutorialScript* 예제 runbook, runbook 함께 hello 계정으로 실행 계정 toomanage 리소스 관리자 리소스를 사용 하 여 tooauthenticate 합니다.

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

여러 구독 간에 작동 하면 tooeasily toohelp, hello 스크립트를 지 원하는 구독 컨텍스트 참조 코드의 두 추가 줄이 포함 합니다. 명명 된 변수 자산 *SubscriptionId* hello hello 구독의 ID를 포함 합니다. Hello 후 `Add-AzureRmAccount` cmdlet 문을 hello [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) hello 매개 변수 집합으로 cmdlet은 지정한 *-SubscriptionId*합니다. Hello 변수 이름이 너무 제네릭인 경우에 tooinclude 접두사를 수정 하거나 다른 명명 규칙 toomake를 사용할 수 있습니다 것 보다 쉽게 tooidentify 합니다. 또는 hello 매개 변수 집합을 사용할 수 *-s u b* 대신 *-SubscriptionId* 해당 변수 자산을 사용 합니다.

hello runbook에서 인증 하기 위해 사용 하는 cmdlet hello `Add-AzureRmAccount`를 사용 하 여 hello *ServicePrincipalCertificate* 매개 변수 집합입니다. Hello 서비스 보안 주체 인증서 하지 hello 사용자 자격 증명을 사용 하 여 인증 합니다.

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a>샘플 코드 tooauthenticate 서비스 관리 리소스
Hello hello에서 사용 되는 업데이트 된 예제 코드를 다음을 사용할 수 있습니다 *AzureClassicAutomationTutorialScript* 예제 runbook, tooauthenticate hello 클래식 실행 계정 toomanage 클래식 리소스를 사용 하 여 프로그램 runbook입니다.

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a>다음 단계
* [Azure AD의 응용 프로그램 및 서비스 주체 개체](../active-directory/active-directory-application-objects.md)
* [Azure Automation의 역할 기반 액세스 제어](automation-role-based-access-control.md)
* [Azure Cloud Services의 인증서 개요](../cloud-services/cloud-services-certs-create.md)
