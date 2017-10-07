---
title: "Azure AD Connect 동기화로 암호 동기화 aaaTroubleshoot | Microsoft Docs"
description: "이 문서는 방법에 대 한 정보를 제공 tootroubleshoot 암호 동기화 문제."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a>Azure AD Connect 동기화를 사용하여 암호 동기화 문제 해결
이 항목에서는 암호 동기화와 함께 tootroubleshoot 발급 하는 방법에 대 한 단계를 제공 합니다. 암호가 예상대로 동기화되지 않으면 사용자의 하위 집합 또는 모든 사용자의 암호일 수 있습니다. Azure Active Directory (Azure AD)에 대 한 배포 1.1.524.0 버전과 연결 또는 이상 버전에서는 이제 진단 cmdlet이 tootroubleshoot 암호 동기화 문제를 사용할 수 있습니다.

* 암호가 동기화는 문제가 있는, 하는 경우 참조 toohello [암호가 동기화: hello 진단 cmdlet을 사용 하 여 문제를 해결](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) 섹션.

* 개별 개체에 문제가 있는 경우 참조 toohello [하나의 개체만 암호 동기화 되지 않는: hello 진단 cmdlet을 사용 하 여 문제를 해결](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) 섹션.

이전 버전의 Azure AD Connect 배포:

* 암호가 동기화는 문제가 있는, 하는 경우 참조 toohello [암호가 동기화: 문제 해결 단계는 수동](#no-passwords-are-synchronized-manual-troubleshooting-steps) 섹션.

* 개별 개체에 문제가 있는 경우 참조 toohello [하나의 개체만 암호 동기화 되지 않는: 문제 해결 단계는 수동](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) 섹션.

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>암호가 동기화: hello 진단 cmdlet을 사용 하 여 문제 해결
Hello를 사용할 수 있습니다 `Invoke-ADSyncDiagnostics` cmdlet toofigure 아웃 이유 암호가 동기화 됩니다.

> [!NOTE]
> hello `Invoke-ADSyncDiagnostics` cmdlet은 이상 1.1.524.0 Azure AD Connect 버전에 대해서만 사용할 수 있습니다.

### <a name="run-hello-diagnostics-cmdlet"></a>Hello 진단 cmdlet 실행
tootroubleshoot 문제 암호가 동기화 됩니다.

1. Hello로 Azure AD Connect 서버에서 새 Windows PowerShell 세션을 열고 **관리자 권한으로 실행** 옵션입니다.

2. `Set-ExecutionPolicy RemoteSigned` 또는 `Set-ExecutionPolicy Unrestricted`를 실행합니다.

3. `Import-Module ADSyncDiagnostics`을 실행합니다.

4. `Invoke-ADSyncDiagnostics -PasswordSync`을 실행합니다.

### <a name="understand-hello-results-of-hello-cmdlet"></a>Hello cmdlet의 hello 결과 이해
hello 진단 cmdlet는 검사를 수행 하는 hello를 수행 합니다.

* 해당 hello의 유효성을 검사 Azure AD 테 넌 트에 대 한 암호 동기화 기능을 사용할 수 있습니다.

* 해당 hello 서버를 준비 모드에 있지 않습니다. Azure AD Connect의 유효성을 검사 합니다.

* 각각의 기존 온-프레미스 Active Directory connector (를 기존 Active Directory 포리스트에 tooan 해당):

   * 해당 hello의 유효성을 검사 암호 동기화 기능을 사용할 수 있습니다.
   
   * Windows 응용 프로그램 이벤트 로그를 hello에서 암호 동기화 하트 비트 이벤트를 검색 합니다.

   * Hello 온-프레미스 Active Directory connector에서 각 Active Directory 도메인:

      * 해당 hello의 유효성을 검사 도메인은 hello Azure AD Connect 서버에서 연결할 수 있습니다.

      * Hello 올바른 사용자 이름, 암호 및 암호 동기화에 필요한 사용 권한에 hello 온-프레미스 Active Directory connector에서 사용 하는 hello Active Directory 도메인 서비스 (AD DS) 계정에 있는지 확인 합니다.

hello 다음 다이어그램에서는 단일 도메인, 온-프레미스 Active Directory 토폴로지를 hello cmdlet의 hello 결과를 보여 줍니다.

![암호 동기화에 대한 진단 출력](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

이 섹션의 나머지 부분 hello hello cmdlet에서 반환 되는 특정 결과 설명 및 해당 문제입니다.

#### <a name="password-synchronization-feature-isnt-enabled"></a>암호 동기화 기능이 사용되지 않음
Hello Azure AD Connect 마법사를 사용 하 여 암호 동기화를 활성화 하지 않은, hello 다음 오류가 반환 됩니다.

![암호 동기화가 사용되지 않음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a>Azure AD Connect 서버가 준비 모드에 있음
Hello Azure AD Connect 서버가 준비 모드에 있으면 암호 동기화가 일시적으로 해제 하 고 hello 다음 오류가 반환 됩니다.

![Azure AD Connect 서버가 준비 모드에 있음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a>암호 동기화 하트비트 이벤트 없음
각각의 온-프레미스 Active Directory 커넥터에 자체 암호 동기화 채널이 있습니다. Hello 암호 동기화 채널이 설정 될 때 동기화는 암호 변경 내용을 toobe 없는 하트 비트 이벤트 (이벤트 Id 654) 분 마다 한 번씩 30 hello Windows 응용 프로그램 이벤트 로그에서 생성 됩니다. 각 온-프레미스 Active Directory 커넥터에 대 한 hello cmdlet 검색 hello에서 해당 하트 비트 이벤트에 대 한 지난 3 시간입니다. 하트 비트 이벤트가 발견 되 면 hello 다음과 같은 오류가 반환 됩니다.

![암호 동기화 하트비트 이벤트 없음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a>AD DS 계정에 올바른 사용 권한이 없음
Hello AD DS 계정 hello에서 사용 되는 온-프레미스 Active Directory connector toosynchronize 암호 해시 hello 적절 한 권한이 없을 경우 hello 다음과 같은 오류가 반환 됩니다.

![잘못된 자격 증명](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a>잘못된 AD DS 계정 사용자 이름 또는 암호
Hello AD DS 계정에서 사용 하는 경우 hello 온-프레미스 Active Directory connector toosynchronize 암호 해시는 잘못 된 사용자 이름 또는 암호를 hello 다음 오류가 반환 됩니다.

![잘못된 자격 증명](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>하나의 개체에 암호 동기화 되지 않는: hello 진단 cmdlet을 사용 하 여 문제 해결
Hello를 사용할 수 있습니다 `Invoke-ADSyncDiagnostics` cmdlet toodetermine 하나의 개체만 암호 동기화 되지 않는 이유입니다.

> [!NOTE]
> hello `Invoke-ADSyncDiagnostics` cmdlet은 이상 1.1.524.0 Azure AD Connect 버전에 대해서만 사용할 수 있습니다.

### <a name="run-hello-diagnostics-cmdlet"></a>Hello 진단 cmdlet 실행
tootroubleshoot 문제 암호가 동기화 됩니다.

1. Hello로 Azure AD Connect 서버에서 새 Windows PowerShell 세션을 열고 **관리자 권한으로 실행** 옵션입니다.

2. `Set-ExecutionPolicy RemoteSigned` 또는 `Set-ExecutionPolicy Unrestricted`를 실행합니다.

3. `Import-Module ADSyncDiagnostics`을 실행합니다.

4. Hello 다음 cmdlet을 실행 합니다.
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   예:
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a>Hello cmdlet의 hello 결과 이해
hello 진단 cmdlet는 검사를 수행 하는 hello를 수행 합니다.

* Hello Active Directory 개체에 hello Active Directory 커넥터 공간, 메타 버스 및 Azure의 hello 상태를 검사 하 여 AD 커넥터 공간입니다.

* 동기화 규칙 암호 동기화와 함께 사용 하 고 toohello Active Directory 개체를 적용 합니다. 확인 합니다.

* Hello 마지막 시도 toosynchronize hello에 대 한 암호 hello 개체 hello 결과 tooretrieve 및 표시를 시도합니다.

hello 다음 다이어그램에서는 단일 개체에 대 한 암호 동기화 문제를 해결할 때 hello cmdlet의 hello 결과를 보여 줍니다.

![암호 동기화에 대한 진단 출력 - 단일 개체](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

이 섹션의 나머지 부분 hello hello cmdlet에서 반환 하는 특정 결과 설명 및 해당 문제입니다.

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a>hello는 Active Directory 개체가 하지 않은 내보낸된 tooAzure AD
이 온-프레미스 Active Directory 계정에 대 한 암호 동기화 hello Azure AD 테 넌 트에 해당 개체가 있기 때문에 실패 합니다. hello 다음 오류가 반환 됩니다.

![Azure AD 개체가 없음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a>사용자에게 임시 암호가 있음
현재, Azure AD Connect는 임시 암호를 Azure AD와 동기화하는 기능을 지원하지 않습니다. 암호를 사용 하도록 toobe 임시 경우 hello **다음 로그온 할 때 암호 변경** hello 온-프레미스 Active Directory 사용자에 옵션을 설정 합니다. hello 다음 오류가 반환 됩니다.

![임시 암호는 내보내지지 않음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a>마지막 시도 toosynchronize 암호의 결과 사용할 수 없습니다.
기본적으로 Azure AD Connect를 7 일 동안 암호 동기화 시도 hello 결과 저장합니다. Hello 선택한 Active Directory 개체에 사용할 수 없는 결과가 없는 경우 경고를 수행 하는 hello 반환 됩니다.

![단일 개체에 대한 진단 출력 - 암호 동기화 기록 없음](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a>암호가 동기화되지 않음: 수동 문제 해결 단계
이러한 단계 toodetermine 없는 암호가 동기화 되는 이유를 수행 합니다.

1. hello 연결 서버인 [준비 모드](active-directory-aadconnectsync-operations.md#staging-mode)? 스테이징 모드의 서버는 암호를 동기화하지 않습니다.

2. Hello에서 hello 스크립트를 실행 [암호 동기화 설정의 hello 상태 가져오기](#get-the-status-of-password-sync-settings) 섹션. Hello 암호 동기화 구성에 대해 간략하게를 제공 합니다.  

    ![암호 동기화 설정의 PowerShell 스크립트 출력](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. Azure AD에서 hello 기능이 설정 되지 않은 또는 hello 동기화 채널 상태를 사용 하지 않는 경우 hello Connect 설치 마법사를 실행 합니다. **동기화 옵션 사용자 지정**을 선택하고 암호 동기화의 선택을 취소합니다. 이 변경은 hello 기능을 일시적으로 해제 합니다. 그런 다음 hello 마법사를 다시 실행 하 고 암호 동기화를 다시 사용 하도록 설정 합니다. Hello 스크립트 실행 구성 hello tooverify 올바른지 다시 합니다.

4. 오류에 대 한 hello 이벤트 로그를 확인 합니다. Hello 다음 문제를 나타내는 이벤트를 찾습니다.
    * 원본: "디렉터리 동기화" ID: 0, 611, 652, 655 이러한 이벤트가 표시되면 연결 문제가 있는 것입니다. hello 이벤트 로그 메시지는 문제가 있는 경우 포리스트 정보를 포함 합니다. 자세한 내용은 [연결 문제](#connectivity problem)를 참조하세요.

5. 하트비트가 표시되지 않거나 아무 작동도 진행되지 않으면 [모든 암호의 전체 동기화 트리거](#trigger-a-full-sync-of-all-passwords)를 실행합니다. Hello 스크립트를 한 번만 실행 합니다.

6. Hello 참조 [암호 동기화 되지 않은 한 개체의 문제를 해결](#one-object-is-not-synchronizing-passwords) 섹션.

### <a name="connectivity-problems"></a>연결 문제

Azure AD와 연결되어 있나요?

Hello 계정이 모든 도메인에서 권한을 tooread hello 암호 해시를 필요한가지고? 기본 설정을 사용 하 여 연결을 설치한 경우 hello 사용 권한을 이미 수정 됩니다. 

사용자 지정 설치를 사용 하는 경우 hello 사용 권한을 수동으로 설정 hello 다음을 수행 하 여:
    
1. hello Active Directory 커넥터 시작에 의해 사용 되는 toofind hello 계정 **동기화 서비스 관리자**합니다. 
 
2. 너무 이동**커넥터**, 한 다음 문제를 해결 하는 hello 온-프레미스 Active Directory 포리스트 검색 합니다. 
 
3. Hello 커넥터를 선택 하 고 클릭 한 다음 **속성**합니다. 
 
4. 너무 이동**tooActive Directory 포리스트에 연결**합니다.  
    
    ![Active Directory 커넥터에서 사용되는 계정](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    Hello 사용자 이름 및 hello 계정 위치한 hello 도메인 note 합니다.
    
5. 시작 **Active Directory 사용자 및 컴퓨터**, 다음 이전에 발견 된 hello 계정에 포리스트의 모든 도메인의 hello 루트에 설정 된 hello 수행 권한은 있는지를 확인 합니다.
    * 디렉터리 변경 내용 복제
    * 모든 디렉터리 변경 내용 복제

6. Hello Azure AD Connect에서 연결할 수 있는 도메인 컨트롤러는? Hello 연결 서버 tooall 도메인 컨트롤러에 연결할 수 없는 경우 구성 **만 선호 도메인 컨트롤러를 사용 하 여**합니다.  
    
    ![Active Directory 커넥터에서 사용되는 도메인 컨트롤러](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. 너무 돌아가서**동기화 서비스 관리자** 및 **구성 디렉터리 파티션의**합니다. 
 
8. 도메인을 선택 **디렉터리 파티션 선택**선택, hello **만 선호 도메인 컨트롤러를 사용 하 여** 확인란을 선택한 다음 클릭 **구성**합니다. 

9. Hello 목록에서 연결 암호 동기화에 사용 해야 하는 hello 도메인 컨트롤러를 입력 합니다. hello 동일한 목록은 가져오기 및 내보내기에도 사용 됩니다. 모든 도메인에 대해 이 단계를 수행합니다.

10. Hello 스크립트 하트 비트가 임을 표시 되 면 hello 스크립트에서 실행 [모든 암호의 전체 동기화를 트리거할](#trigger-a-full-sync-of-all-passwords)합니다.

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a>한 개체가 암호를 동기화하지 않음: 수동 문제 해결 단계
개체의 hello 상태를 검토 하 여 암호 동기화 문제를 쉽게 해결할 수 있습니다.

1. **Active Directory 사용자 및 컴퓨터**hello 사용자를 검색 한 다음 해당 hello를 확인, **사용자 다음 로그온 할 때 암호를 변경 해야** 확인란의 선택을 취소 합니다.  

    ![Active Directory 생산성 높은 암호](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    Hello 확인란을 선택 하면 hello 사용자 toosign에 게 문의 하 고 hello 암호를 변경 합니다. 임시 암호는 Azure AD와 동기화되지 않습니다.

2. Hello 암호와 Active Directory에서 올바른 나타나는 경우 hello 사용자를 hello 동기화 엔진에 따릅니다. 온-프레미스 Active Directory tooAzure AD에서에서 다음 hello 사용자에 의해 hello 개체에서 설명 하는 오류 인지를 볼 수 있습니다.

    a. Hello 시작 [동기화 서비스 관리자](active-directory-aadconnectsync-service-manager-ui.md)합니다.

    b. **커넥터**를 클릭합니다.

    c. 선택 hello **Active Directory Connector** hello 사용자가 있는 합니다.

    d. **커넥터 공간 검색**을 선택합니다.

    e. Hello에 **범위** 상자 **DN 또는 앵커**, 해결 하는 hello 사용자의 전체 DN hello를 입력 합니다.

    ![DN을 사용하여 커넥터 공간에서 사용자 검색](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    f. 검색 중인 하 고 클릭 hello 사용자를 찾고 **속성** toosee 모든 hello 특성입니다. Hello 사용자 hello 검색 결과에 없으면 확인 프로그램 [필터링 규칙](active-directory-aadconnectsync-configure-filtering.md) 를 실행 하 고 [적용 및 변경 확인](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) 연결에서 사용자 tooappear hello에 대 한 합니다.

    g. toosee hello 암호 동기화 개체의 세부 정보 hello hello에 대 한 지난 주 클릭 **로그**합니다.  

    ![개체 로그 정보](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    Hello 개체 로그 비어 있으면 Azure AD Connect Active Directory에서 없습니다 tooread hello 암호 해시 되었습니다. [연결 오류](#connectivity-errors) 문제를 계속 해결합니다. 이외의 다른 값을 표시 되 면 **성공**, toohello 표에 참조 [암호 동기화 로그](#password-sync-log)합니다.

    h. 선택 hello **계보** 탭을 만들고 해당 적어도 하나의 동기화 규칙 hello에 **PasswordSync** 열이 **True**합니다. Hello 기본 구성으로 hello hello 동기화 규칙 이름이 **에서 from AD-User AccountEnabled**합니다.  

    ![사용자에 대한 계보 정보](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    i. 클릭 **메타 버스 개체 속성** toodisplay 사용자 특성 목록입니다.  

    ![메타버스 정보](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    **cloudFiltered** 특성이 없는지 확인합니다. Hello 도메인 특성 (domainFQDN 및 domainNetBios) hello 예상 값에 있는지 확인 합니다.

    j. Hello 클릭 **커넥터** 탭 합니다. 커넥터 tooboth 온-프레미스 Active Directory를 볼 수 있어야 하 고 Azure AD.

    ![메타버스 정보](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    k. Azure AD를 나타내는 선택 hello 행 클릭 **속성**, hello를 클릭 한 다음 **계보** 탭 hello 커넥터 공간 개체는 아웃 바운드 규칙 hello를가지고 있어야 **PasswordSync** 열이 너무 설정**True**합니다. Hello 기본 구성으로 hello hello 동기화 규칙 이름이 **tooAAD-User Join 아웃**합니다.  

    ![커넥터 공간 개체 속성 대화 상자](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a>암호 동기화 로그
hello 상태 열에는 다음 값에는 hello를 가질 수 있습니다.

| 가동 상태 | 설명 |
| --- | --- |
| 성공 |암호가 성공적으로 동기화되었습니다. |
| FilteredByTarget |암호가 너무 설정**사용자 다음 로그온 할 때 암호를 변경 해야**합니다. 암호가 동기화되지 않았습니다. |
| NoTargetConnection |Hello 메타 버스의 또는 hello Azure AD 커넥터 공간에 없는 개체입니다. |
| SourceConnectorNotPresent |개체가 hello 온-프레미스 Active Directory 커넥터 공간에서 찾을 수 없습니다. |
| TargetNotExportedToDirectory |Azure AD 커넥터 공간 hello에 hello 개체 아직 내보내지 않았습니다. |
| MigratedCheckDetailsForMoreInfo |로그 항목 1.0.9125.0 빌드 전에 만들어졌으며 레거시 상태로 표시됩니다. |
| 오류 |서비스에 알 수 없는 오류가 반환되었습니다. |
| 알 수 없음 |Tooprocess 암호 해시의 일괄 처리 하는 동안 오류가 발생 했습니다.  |
| MissingAttribute |Azure AD Domain Services에 필요한 특정 특성(예: Kerberos 해시)을 사용할 수 없습니다. |
| RetryRequestedByTarget |Azure AD Domain Services에 필요한 특정 특성(예: Kerberos 해시)을 이전에 사용할 수 없었습니다. 가 시도 tooresynchronize hello 사용자의 암호 해시가 이루어집니다. |

## <a name="scripts-toohelp-troubleshooting"></a>스크립트 toohelp 문제 해결

### <a name="get-hello-status-of-password-sync-settings"></a>암호 동기화 설정의 hello 상태를 가져옵니다.
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a>모든 암호의 전체 동기화 트리거
> [!NOTE]
> 이 스크립트는 한 번만 실행합니다. 이 두 번 이상 toorun 해야 할 경우 다른 작업은 hello 문제입니다. tootroubleshoot hello 문제를 Microsoft 지원에 문의 합니다.

다음 스크립트는 hello를 사용 하 여 모든 암호의 전체 동기화를 트리거할 수 있습니다.

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a>다음 단계
* [Azure AD Connect 동기화로 암호 동기화 구현](active-directory-aadconnectsync-implement-password-synchronization.md)
* [Azure AD Connect 동기화: 동기화 옵션 사용자 지정](active-directory-aadconnectsync-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
