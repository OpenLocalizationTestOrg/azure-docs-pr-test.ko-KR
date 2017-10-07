---
title: "Azure AD Connect 동기화: hello Azure AD 연결 동기화 서비스 계정 변경 | Microsoft Docs"
description: "항목 설명 hello 암호화 키 및 tooabandon hello 암호 후 방법은 변경 합니다."
services: active-directory
keywords: "Azure AD 동기화 서비스 계정, 암호"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a>Hello Azure AD Connect 동기화 서비스 계정 암호 변경
Hello Azure AD Connect 동기화 서비스 계정 암호를 변경 하면 hello 동기화 서비스 됩니다 수 시작 올바르게 hello 암호화 키를 중단 하 고 hello Azure AD Connect 동기화 서비스 계정 암호를 다시 초기화 될 때까지 합니다. 

Azure AD Connect hello 동기화 서비스의 일부로 hello AD DS와 Azure AD 서비스 계정을 암호화 키 toostore hello 암호를 사용 합니다.  이러한 계정은 hello 데이터베이스에 저장 되기 전에 암호화 됩니다. 

hello 사용 되는 암호화 키로 보호 될 [Windows DPAPI (데이터 보호)](https://msdn.microsoft.com/library/ms995355.aspx)합니다. Hello를 사용 하 여 hello 암호화 키를 보호 하는 DPAPI **hello Azure AD Connect 동기화 서비스 계정 암호**합니다. 

hello 절차를 사용할 수 toochange hello 서비스 계정 암호가 필요한 경우 [Abandoning hello Azure AD Sync 연결 암호화 키](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish이 있습니다.  또한 어떤 이유로 든 tooabandon hello 암호화 키가 필요한 경우 이러한 절차를 사용 해야 합니다.

##<a name="issues-that-arise-from-changing-hello-password"></a>Hello 암호 변경에서 발생 하는 문제
Toobe hello 서비스 계정 암호를 변경 하는 경우 수행 해야 하는 두 가지입니다.

먼저 hello Windows 서비스 제어 관리자에서 toochange hello 암호입니다.  이 문제가 해결될 때까지 다음 오류가 표시됩니다.


- Hello 오류가 나타나면 toostart hello 동기화 서비스 Windows 서비스 제어 관리자에서 시도 하면 "**로컬 컴퓨터에서 Windows hello Microsoft Azure AD Sync 서비스를 시작 하지 못했습니다**"입니다. **오류 1069: hello 서비스 tooa 로그온 실패로 인해 시작 되지 않았습니다.** "
- Hello 시스템 이벤트 로그에서 Windows 이벤트 뷰어 오류가 포함 되어 **이벤트 ID 7038** 및 메시지 "**hello ADSync 서비스에 없습니다 toolog toohello 다음 인해 hello 현재 구성 된 암호와 마찬가지로 된 오류: hello 사용자 이름 또는 암호가 올바르지 않습니다.** "

둘째, 특정 조건에서 hello 암호 업데이트 되 면 hello 동기화 서비스가 더 이상 검색할 수 DPAPI 통해 hello 암호화 키. Hello 암호화 키가 없으면 동기화 서비스 hello 필요한 toosynchronize로 /에서 암호를 해독할 수 없음 hello 온-프레미스 AD와 Azure AD.
다음과 같은 오류가 표시됩니다.

- Windows 서비스 제어 관리자에서 toostart hello 동기화 서비스는 hello 암호화 키를 검색할 수 없는 경우 요청이 실패 오류 "* * 로컬 컴퓨터에서 Windows hello Microsoft Azure AD Sync를 시작 하지 못했습니다. 자세한 내용은 hello 시스템 이벤트 로그를 검토 합니다. 이 타사 서비스 hello 서비스 공급 업체에 문의 한 tooservice 요소별 오류 코드를 참조 하십시오. * *-21451857952 * * *. "
- Hello 응용 프로그램 이벤트 로그에서 Windows 이벤트 뷰어 오류가 포함 되어 **이벤트 ID 6028** 및 오류 메시지 *"**hello 서버 암호화 키에 액세스할 수 없습니다.* *"*

이러한 오류를 수신 하지 않는 tooensure에 hello 절차에 따라 [Abandoning hello Azure AD Sync 연결 암호화 키](#abandoning-the-azure-ad-connect-sync-encryption-key) hello 암호를 변경 하는 경우.
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a>암호화 키를 Azure AD 연결 동기화 하는 hello를 중단합니다.
>[!IMPORTANT]
>hello 다음 절차만 적용 tooAzure AD Connect 빌드 1.1.443.0 또는 이전 버전입니다.

다음 프로시저 tooabandon hello 암호화 키 hello를 사용 합니다.

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a>어떤 toodo tooabandon hello 암호화 키가 필요한 경우

필요한 경우 tooabandon hello 암호화 키를 사용 프로시저 tooaccomplish 다음 hello이 합니다.

1. [Hello 기존 암호화 키를 중단 합니다.](#abandon-the-existing-encryption-key)

2. [AD DS 계정 hello hello 암호 제공](#provide-the-password-of-the-ad-ds-account)

3. [Azure AD 동기화 계정 hello의 hello 암호를 다시 초기화](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [Hello 동기화 서비스를 시작 합니다.](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a>Hello 기존 암호화 키를 중단 합니다.
Hello 기존 암호화 키를 중단 하는 새로운 암호화 키를 만들 수 있습니다.

1. 관리자 권한으로 Azure AD 연결 서버 tooyour에 로그인 합니다.

2. 새 PowerShell 세션을 시작합니다.

3. Toofolder를 이동 합니다.`$env:Program Files\Microsoft Azure AD Sync\bin\`

4. Hello 명령을 실행 합니다.`./miiskmu.exe /a`

![Azure AD Connect 동기화 암호화 키 유틸리티](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a>AD DS 계정 hello hello 암호 제공
Hello 데이터베이스 내에 저장 하는 hello 기존 암호를 해독할 수 없습니다, AD DS hello 계정의 hello 암호로 tooprovide hello 동기화 서비스 필요. hello 새 암호화 키를 사용 하 여 hello 암호를 암호화 하는 hello 동기화 서비스:

1. Hello 동기화 서비스 관리자 (→ 시작 동기화 서비스)를 시작 합니다.
</br>![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  
2. Toohello 이동 **커넥터** 탭 합니다.
3. 선택 hello **AD 커넥터** tooyour 해당 하는 온-프레미스 AD 합니다. 둘 이상의 AD 커넥터를 설정한 경우 hello 각각의 다음 단계를 반복 합니다.
4. **작업** 아래에서 **속성**을 선택합니다.
5. Hello 팝업 대화 상자에서 선택 **tooActive Directory 포리스트에 연결**:
6. Hello에 AD DS hello 계정의 hello 암호를 입력 **암호** 텍스트 상자에 붙여넣습니다. 암호를 모르는 경우이 단계를 수행 하기 전에 값을 알려진 tooa를 설정 해야 합니다.
7. 클릭 **확인** toosave hello 새 암호와 닫기 hello 팝업 대화 상자.
![Azure AD Connect 동기화 암호화 키 유틸리티](media/active-directory-aadconnectsync-encryption-key/key6.png)

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a>Azure AD 동기화 계정 hello의 hello 암호를 다시 초기화
직접 hello Azure AD 서비스 계정 toohello 동기화 서비스의 hello 암호를 제공할 수 없습니다. 대신, toouse hello cmdlet 필요 **추가 ADSyncAADServiceAccount** tooreinitialize hello Azure AD 서비스 계정입니다. hello cmdlet hello 계정 암호를 재설정 하 고 사용할 수 있는 toohello 동기화 서비스를 사용 하면:

1. Hello Azure AD Connect 서버에서 새 PowerShell 세션을 시작 합니다.
2. cmdlet `Add-ADSyncAADServiceAccount`를 실행합니다.
3. Hello 팝업 대화 상자에서 Azure AD 테 넌 트에 대 한 hello Azure AD 전역 관리자 자격 증명을 제공 합니다.
![Azure AD Connect 동기화 암호화 키 유틸리티](media/active-directory-aadconnectsync-encryption-key/key7.png)
4. 성공한 경우에 hello PowerShell 명령 프롬프트를 표시 됩니다.

#### <a name="start-hello-synchronization-service"></a>Hello 동기화 서비스를 시작 합니다.
Hello 동기화 서비스에 대 한 액세스 toohello 암호화 키 및 암호를 hello 모든 했으므로, hello Windows 서비스 제어 관리자에서에서 hello 서비스를 다시 시작할 수 있습니다.


1. TooWindows 서비스 제어 관리자 (시작 → 서비스)를 이동 합니다.
2. **Microsoft Azure AD 동기화**를 선택하고 다시 시작을 클릭합니다.

## <a name="next-steps"></a>다음 단계
**개요 항목**

* [Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정](active-directory-aadconnectsync-whatis.md)

* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
