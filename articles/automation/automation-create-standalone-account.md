---
title: "aaaCreate 독립 실행형 Azure 자동화 계정 | Microsoft Docs"
description: "자습서를 안내해 hello 작성, 테스트 및 예제를 사용 하 여 Azure 자동화의 보안 주체 인증 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 1500d25d9565d4082768933834303a17c5e84234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-azure-automation-account"></a>독립 실행형 Azure Automation 계정 만들기
이 항목에서는 방법을 toocreate hello tooevaluate 고 hello 추가 관리 솔루션 또는 OMS 로그 분석 tooprovide와의 통합을 포함 하지 않고 Azure 자동화를 알아보려면 Azure 포털에서에서 자동화 계정을 고급 모니터링 runbook 작업입니다.  이러한 관리 솔루션을 추가 하거나 hello 나중에 언제 든 지 로그 분석을 통합할 수 있습니다.  자동화 계정 hello 수 tooauthenticate runbook Azure 리소스 관리자 또는 Azure 클래식 배포의 리소스 관리 됩니다.

Hello Azure 포털에서에서 자동화 계정을 만들 때 자동으로 생성 됩니다.

* 다음 계정으로 실행 계정에서 인증서를 Azure Active Directory에서 새 서비스 사용자를 만드는 및 할당은 참가자 역할 기반 액세스 제어 (RBAC) hello toomanage 리소스 관리자 리소스 runbook을 사용 하는 데 사용 합니다.   
* 기본 실행 계정을 관리 인증서를 업로드 하 여 runbook을 사용 하 여 toomanage 클래식 리소스를 사용 합니다.  

이 사용자에 대 한 hello 프로세스가 간소화 되어 신속 하 게 작성을 시작 합니다 및 runbook toosupport 배포 자동화 요구 합니다.  

## <a name="permissions-required-toocreate-automation-account"></a>필요한 toocreate 자동화 계정 권한
이 항목 toocomplete 필요한 사용 권한 및 다음 특정 권한을 hello toocreate 또는 자동화 계정 업데이트 해야 합니다.   
 
* 순서 toocreate 자동화 계정에에서 AD 사용자 계정의 사용 권한 해당 toohello 소유자 역할을 가진 toobe 추가 tooa 역할 Microsoft.Automation 리소스에 대 한 설명 된 대로 문서의 [Azure 자동화에서 역할 기반 액세스 제어 ](automation-role-based-access-control.md).  
* Hello 응용 프로그램 등록 설정 너무 설정 되어 있으면**예**, Azure AD 테 넌 트의 관리자가 아닌 사용자 수 [AD 응용 프로그램 등록](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions)합니다.  Hello 응용 프로그램 등록 설정 너무 설정 되어 있으면**아니요**,이 작업을 수행 하는 hello 사용자는 Azure ad에서 전역 관리자 여야 합니다. 

가 아닌 hello 구독 Active Directory 인스턴스에서 소속 toohello 전역 관리자/공동 관리자의 역할 hello 구독을 추가 하기 전에 사용자 tooActive 디렉터리에 게스트로 추가 됩니다. 이 경우에는 "없는 사용 권한을 toocreate..." 표시 hello에 경고 **자동화 계정 추가** 블레이드입니다. 먼저 hello 구독 Active Directory 인스턴스에서 제거할 수도 있고 toomake 떼었다가 다시 추가 toohello 전역 관리자/공동 관리자 역할에 추가 된 사용자를 해당 Active Directory에서 전체 사용자입니다. tooverify hello에서 이러한 경우 **Azure Active Directory** hello Azure 포털의에서 창 **사용자 및 그룹**선택, **모든 사용자에 게** 및 hello를 선택한 후 특정 사용자 **프로필**합니다. 값의 hello hello **사용자 유형** hello 사용자 프로필 아래에 특성 같지 해야 **게스트**합니다.

## <a name="create-a-new-automation-account-from-hello-azure-portal"></a>Hello Azure 포털에서에서 새 자동화 계정 만들기
이 섹션에서는 다음 단계 toocreate hello Azure 포털에서에서 Azure 자동화 계정을 hello를 수행 합니다.    

1. Hello 구독 관리자 역할의 멤버 및 hello 구독의 공동 관리자 인 계정으로 Azure 포털 toohello에 로그인 합니다.
2. **새로 만들기**를 클릭합니다.<br><br> ![Azure Portal에서 새 옵션을 선택합니다.](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  
3. 검색할 **자동화** 다음 hello에 검색 결과 선택 하 고 **자동화 및 제어*** 합니다.<br><br> ![Marketplace에서 Automation을 검색하고 선택합니다.](media/automation-create-standalone-account/automation-marketplace-select-create-automationacct.png)<br> 
3. Hello 자동화 계정을 블레이드에서 클릭 **추가**합니다.<br><br>![Automation 계정 추가](media/automation-create-standalone-account/automation-create-automationacct-properties.png)
   
   > [!NOTE]
   > Hello hello에 경고 뒤에 표시 되 면 **자동화 계정 추가** 블레이드에서 것은 아니므로 계정 hello 구독 관리자 역할의 멤버 및 hello 구독의 공동 관리자입니다.<br><br>![자동화 계정 경고 추가](media/automation-create-standalone-account/create-account-without-perms.png)
   > 
   > 
4. Hello에 **자동화 계정 추가** 블레이드 hello **이름** 상자에 새 자동화 계정에 대 한 이름을 입력 합니다.
5. 둘 이상의 구독을 보유 하는 경우 지정 hello 새 계정에 대 한 새 또는 기존 **리소스 그룹** 과 Azure 데이터 센터 **위치**합니다.
6. Hello 값을 확인 **예** hello에 대 한 확인란이 **만들 Azure 실행 계정** 옵션을 클릭 하는 hello **만들기** 단추입니다.  
   
   > [!NOTE]
   > 선택 하면 toonot hello 실행 계정을 만들 hello 옵션을 선택 하 여 **아니요**, hello에 경고 메시지가 표시 됩니다 **자동화 계정 추가** 블레이드입니다.  Hello 계정이 hello Azure 포털에서에서 생성 되는 동안 구독에서 프로그램 클래식 또는 리소스 관리자 구독 디렉터리 서비스 및 따라서 없습니다 액세스 tooresources 내에서 해당 인증 id가 없는 합니다.  따라서을 tooauthenticate 수 없도록이 계정을 참조 하는 모든 runbook 수 없으며 이러한 배포 모델의 리소스에 대 한 작업을 수행 합니다.
   > 
   > ![자동화 계정 경고 추가](media/automation-create-standalone-account/create-account-decline-create-runas-msg.png)<br>
   > Hello 서비스 사용자 만들어지지 않은 경우에 hello 참가자 역할 할당 되지 않았습니다.
   > 

7. Azure 자동화 계정을 hello를 만드는 동안에 아래 hello 진행률을 추적할 수 **알림** hello 메뉴에서 합니다.

### <a name="resources-included"></a>포함된 리소스
Hello 자동화 계정을 성공적으로 만들어지면 여러 리소스를 자동으로 만들어집니다.  다음 표에 hello hello 실행 계정에 대 한 리소스를 요약 합니다.<br>

| 리소스 | 설명 |
| --- | --- |
| AzureAutomationTutorial Runbook |예제 그래픽 runbook입니다 tooauthenticate를 사용 하 여 실행 계정의 hello 하는 방법을 보여 주고 hello 리소스 관리자 리소스를 모두 가져옵니다. |
| AzureAutomationTutorialScript Runbook |예제 PowerShell runbook입니다 tooauthenticate를 사용 하 여 실행 계정의 hello 하는 방법을 보여 주고 hello 리소스 관리자 리소스를 모두 가져옵니다. |
| AzureRunAsCertificate |자동화 계정 만드는 동안 생성 또는 기존 계정에 대 한 아래의 hello PowerShell 스크립트를 사용 하 여 자동으로 인증서 자산  있습니다 tooauthenticate를 Azure 사용한 runbook에서 Azure 리소스 관리자 리소스를 관리할 수 있도록 합니다.  이 인증서는 수명이 1년입니다. |
| AzureRunAsConnection |자동화 계정 만드는 동안 생성 또는 기존 계정에 대 한 아래의 hello PowerShell 스크립트를 사용 하 여 자동으로 연결 자산 |

다음 표에 hello hello 클래식 실행 계정에 대 한 리소스를 요약 합니다.<br>

| 리소스 | 설명 |
| --- | --- |
| AzureClassicAutomationTutorial Runbook |예제 그래픽 runbook을 hello 클래식 실행 계정 (인증서)를 사용 하 여 구독에 있는 모든 hello 클래식 Vm을 가져와 hello VM 이름 및 상태를 출력 합니다. |
| AzureClassicAutomationTutorial Script Runbook |예제 PowerShell runbook을 hello 클래식 실행 계정 (인증서)를 사용 하 여 구독에 있는 모든 hello 클래식 Vm을 가져와 hello VM 이름 및 상태를 출력 합니다. |
| AzureClassicRunAsCertificate |Runbook에서 Azure 클래식 리소스를 관리할 수 있도록 azure tooauthenticate를 사용 하는 인증서 자산을 자동으로 만들어집니다.  이 인증서는 수명이 1년입니다. |
| AzureClassicRunAsConnection |Runbook에서 Azure 클래식 리소스를 관리할 수 있도록 azure tooauthenticate를 사용 하는 연결 자산을 자동으로 만들어집니다. |


## <a name="next-steps"></a>다음 단계
* 그래픽 작성에 대 한 더 toolearn 참조 [Azure 자동화의 그래픽 제작](automation-graphical-authoring-intro.md)합니다.
* PowerShell runbook 시작 tooget 참조 [내 첫 번째 PowerShell runbook](automation-first-runbook-textual-powershell.md)합니다.
* PowerShell 워크플로 runbook 시작 tooget 참조 [내 첫 번째 PowerShell 워크플로 runbook](automation-first-runbook-textual.md)합니다.
