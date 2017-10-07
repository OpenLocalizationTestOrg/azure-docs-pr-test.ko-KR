---
title: "Azure AD 사용자 계정 aaaCreate | Microsoft Docs"
description: "이 문서에서는 toocreate Azure AD 사용자 계정을 Azure 및 Azure 클래식에서 tooauthenticate Azure 자동화에서에서 runbook에 대 한 자격 증명 하는 방법을 설명 합니다."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: "azure active directory 사용자, azure 서비스 관리, azure ad 사용자 계정"
ms.assetid: fcfe266d-b22e-4dfb-8272-adcab09fc0cf
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 7c6ed4182dbab074d0bc5da7057f74ad321d8884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-azure-classic-deployment-and-resource-manager"></a>Azure 클래식 배포 및 Resource Manager를 사용하여 Runbook 인증
이 문서에서는 Azure 리소스 관리자 리소스 또는 Azure 클래식 배포 모델에 대해 실행 되는 Azure 자동화 runbook에 대 한 Azure AD 사용자 계정을 tooconfigure를 수행 해야 하는 hello 단계를 설명 합니다.  이 계속 toobe 되는 동안 Azure 리소스 관리자에 대 한 지원 되는 인증 id를 따라 runbook, hello 메서드는 Azure 계정으로 실행 계정을 사용 하는 것이 좋습니다.       

## <a name="create-a-new-azure-active-directory-user"></a>새 Azure Active Directory 사용자 만들기
1. Hello toomanage를 원하는 Azure 구독에 대 한 서비스 관리자는 toohello Azure 클래식 포털에 로그인 합니다.
2. 선택 **Active Directory**, 조직 디렉터리의 hello 이름을 선택 합니다.
3. 선택 hello **사용자** 탭을 선택한 다음 hello 명령 영역에서 선택 **사용자 추가**합니다.
4. Hello에 **이 사용자에 대해 알리기** 페이지의 **유형의 사용자**선택, **조직 내에서 새 사용자**합니다.
5. 사용자 이름을 입력합니다.  
6. Hello Active Directory 페이지에서 Azure 구독과 연결 된 hello 디렉터리 이름을 선택 합니다.
7. Hello에 **사용자 프로필** 페이지를 hello에서 첫 번째 및 마지막 이름, 사용자에 게 친숙 한 이름 및 사용자 제공 **역할** 목록입니다.  **Multi-Factor Authentication 활성화**를 하지 마세요.
8. Hello 사용자의 전체 이름 및 임시 암호를 note 합니다.
9. **설정 > 관리자 > 추가**를 선택합니다.
10. 만든 hello 사용자의 hello 전체 사용자 이름을 입력 합니다.
11. 삭제할 사용자 toomanage hello hello 구독을 선택 합니다.
12. Azure 최대 활용 로그 하 한 다음 방금 만든 hello 계정으로 다시 로그인 합니다. 입력 정보 요청된 toochange hello 사용자의 암호가 됩니다.

## <a name="create-an-automation-account-in-azure-classic-portal"></a>Azure 클래식 포털에서 Automation 계정 만들기
이 섹션에서는 hello 단계 toocreate hello 사용 하기 위해 Azure 포털에서에서 Azure 자동화 계정을 Azure 클래식 배포의 리소스를 관리 하 여 runbook과 다음을 수행 합니다.  

> [!NOTE]
> Azure 클래식 hello 및 Azure 포털 및 하거나 hello Azure 클래식 포털을 사용 하 여 만든 자동화 계정을 관리할 수 있습니다는 cmdlet 집합. Hello 계정이 만들어지면 차이가 없습니다. 만들고 hello 계정 내에서 리소스를 관리 합니다. 대신 사용 해야 합니다 toocontinue toouse hello Azure 클래식 포털에 계획 이라면 모든 자동화 계정을 Azure 포털 toocreate hello 합니다.
> 
> 

1. Hello toomanage를 원하는 Azure 구독에 대 한 서비스 관리자는 toohello Azure 클래식 포털에 로그인 합니다.
2. **Automation**을 선택합니다.
3. Hello에 **자동화** 페이지에서 **자동화 계정 만들기**합니다.
4. Hello에 **자동화 계정 만들기** 상자 새 자동화 계정에 대 한 이름을 입력 하 고 선택 된 **지역** hello 드롭 다운 목록에서 합니다.  
5. 클릭 **확인** tooaccept 설정을 hello 계정을 만듭니다.
6. Hello에 나타날 것을 만든 후 **자동화** 페이지.
7. Hello 계정을 클릭 하 고 toohello 대시보드 페이지 나타납니다.  
8. Hello 자동화 대시보드 페이지에서 선택 **자산**합니다.
9. Hello에 **자산** 페이지에서 **설정 추가** hello hello 페이지 맨 아래에 배치 합니다.
10. Hello에 **설정 추가** 페이지에서 **자격 증명 추가**합니다.
11. Hello에 **자격 증명을 정의** 페이지에서 **Windows PowerShell 자격 증명** hello에서 **자격 증명 형식을** 드롭 다운 목록 고 hello 자격 증명에 대 한 이름을 제공 합니다.
12. Hello 다음에 **자격 증명 정의** hello 앞부분에서 만든 hello AD 사용자 계정의 hello 사용자 이름 입력 페이지 **사용자 이름** hello에 필드 및 hello 암호 **암호**및 **암호 확인** 필드입니다. 클릭 **확인** toosave 변경 내용을 합니다.

## <a name="create-an-automation-account-in-hello-azure-portal"></a>Hello Azure 포털의에서 자동화 계정 만들기
이 섹션에서는 hello 단계 toocreate hello 사용 하기 위해 Azure 포털에서에서 Azure 자동화 계정을 Azure 리소스 관리자 모드에서 리소스를 관리 하 여 runbook과 다음을 수행 합니다.  

1. Hello toomanage를 원하는 Azure 구독에 대 한 서비스 관리자는 Azure 포털 toohello에 로그인 합니다.
2. **Automation 계정**을 선택합니다.
3. Hello 자동화 계정을 블레이드에서 클릭 **추가**합니다.<br><br>![Automation 계정 추가](media/automation-create-aduser-account/add-automation-acct-properties.png)
4. Hello에 **자동화 계정 추가** 블레이드 hello **이름** 상자에 새 자동화 계정에 대 한 이름을 입력 합니다.
5. 둘 이상의 구독을 보유 하는 경우 새 계정을 hello와 같은 새 hello 하나 또는 기존 지정 **리소스 그룹** 과 Azure 데이터 센터 **위치**합니다.
6. Hello 값 선택 **예** hello에 대 한 **만들 Azure 실행 계정** 옵션을 클릭 하는 hello **만들기** 단추입니다.  
   
    > [!NOTE]
    > 선택 하면 toonot hello 실행 계정을 만들 hello 옵션을 선택 하 여 **아니요**, hello에 경고 메시지가 나타납니다 **자동화 계정 추가** 블레이드입니다.  Hello 계정을 만들고 toohello 할당 하는 동안 **참가자** 역할 구독 디렉터리 서비스에 액세스할 수 없는 및 따라서 내에서 해당 인증 id를 갖지 것입니다 hello 구독에서 구독에 리소스를 제공 합니다.  이 수 tooauthenticate에서이 계정을 참조 하는 모든 runbook 작업이 방지 되 고 Azure 리소스 관리자 리소스에 대 한 작업을 수행 합니다.
    > 
    >

    <br>![Automation 계정 경고 추가](media/automation-create-aduser-account/add-automation-acct-properties-error.png)<br>  
7. Azure 자동화 계정을 hello를 만드는 동안에 아래 hello 진행률을 추적할 수 **알림** hello 메뉴에서 합니다.

Hello hello 자격 증명 만들기가 완료 되 면 hello AD 사용자 계정이 있는 자격 증명 자산 tooassociate hello 자동화 계정을 앞에서 만든 toocreate가 필요 합니다.  Hello 자동화 계정을 만든만 하 고 인증 id와 연결 되지 않은 기억 합니다.  Hello에 설명 된 hello 단계를 수행 [자산 문서 Azure 자동화 자격 증명](automation-credentials.md#creating-a-new-credential-asset) hello 값을 입력 하 고 **username** hello 형태로 표시 **도메인 \ 사용자**합니다.

## <a name="use-hello-credential-in-a-runbook"></a>Hello 자격 증명을 사용 하 여 runbook에서
Hello를 사용 하 여 runbook에서 hello 자격 증명을 검색할 수 있습니다 [Get-automationpscredential](http://msdn.microsoft.com/library/dn940015.aspx) 활동으로 사용 하 여 [Add-azureaccount](http://msdn.microsoft.com/library/azure/dn722528.aspx) tooconnect tooyour Azure 구독. Hello 자격 증명이 여러 Azure 구독 관리자 경우에 사용 해야 [Select-azuresubscription](http://msdn.microsoft.com/library/dn495203.aspx) toospecify hello 올바르다는 것입니다. 이 일반적으로 대부분의 Azure 자동화 runbook의 hello 위쪽에 표시 되는 hello 샘플 아래 Windows PowerShell에에서 표시 됩니다.

    $cred = Get-AutomationPSCredential –Name "myuseraccount.onmicrosoft.com"
    Add-AzureAccount –Credential $cred
    Select-AzureSubscription –SubscriptionName "My Subscription"

Runbook의 모든 [검사점](http://technet.microsoft.com/library/dn469257.aspx#bk_Checkpoints) 뒤에 이러한 줄을 반복해야 합니다. Hello runbook이 일시 중단 후 다른 작업자에서 다시 시작을 tooperform hello를 다시 인증을 해야 합니다.

## <a name="next-steps"></a>다음 단계
* 다음 문서에서 runbook을 직접 만드는 하기 위한 단계 및 검토 hello 다른 runbook 종류 hello [Azure 자동화 runbook 형식](automation-runbook-types.md)

