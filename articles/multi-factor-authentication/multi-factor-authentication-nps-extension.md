---
title: "aaaUse 기존 NPS 서버 tooprovide Azure MFA 기능 | Microsoft Docs"
description: "Azure Multi-factor Authentication에 대 한 네트워크 정책 서버 확장 hello 간단한 솔루션 tooadd 클라우드 기반 2 단계 vericiation 기능 tooyour 기존 인증 인프라입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: e9fc495b06873d45f06233f1aa618db9d94f8bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-existing-nps-infrastructure-with-azure-multi-factor-authentication"></a>기존 NPS 인프라를 Azure Multi-Factor Authentication과 통합

클라우드 기반 MFA 기능 tooyour 인증 인프라 기존 서버를 사용 하 여 hello Azure MFA에 대 한 정책 서버 NPS (네트워크) 확장을 추가 합니다. NPS 확장 hello로 tooinstall를 구성 하 고 새 서버를 관리할 필요 없이 전화 통화, 문자 메시지 또는 전화 앱 확인 tooyour 기존 인증 흐름을 추가할 수 있습니다. 

Hello Azure MFA 서버를 배포 하지 않고 tooprotect VPN 연결 하려는 조직에이 확장 프로그램을 만들었습니다. hello NPS 확장 페더레이션 방식 또는 동기화 된 사용자에 대 한 인증의 두 번째 요소를 RADIUS와 클라우드 기반 Azure MFA tooprovide 사이의 어댑터로 사용 됩니다.

Azure MFA에 대 한 hello NPS 확장을 사용 하는 경우 다음과 같은 구성 요소가 hello hello 인증 흐름에 포함 됩니다. 

1. **NAS/VPN 서버** VPN 클라이언트에서 요청을 받아 RADIUS 요청 tooNPS 서버로 변환 합니다. 
2. **NPS 서버** tooActive 디렉터리 tooperform hello 기본 인증 hello RADIUS 요청 하 고, 요청이 성공 하면 전달 hello 요청 tooany 설치 된 확장에 대 한 연결 합니다.  
3. **NPS 확장** hello 보조 인증에 대 한 요청 tooAzure MFA를 트리거합니다. Hello 확장 hello 응답을 받은 후 및 hello MFA 시도 성공 하면 Azure STS에서 발급 하는 MFA 클레임을 포함 하는 보안 토큰에 hello NPS 서버를 제공 하 여 hello 인증 요청이 완료 합니다.  
4. **Azure MFA** Azure Active Directory tooretrieve hello 사용자 세부 정보와 통신 하 고 확인 방법을 구성 toohello 사용자를 사용 하 여 hello 보조 인증을 수행 합니다.

다이어그램을 다음 hello이 높은 수준의 인증 요청 흐름을 보여 줍니다. 

![인증 흐름 다이어그램](./media/multi-factor-authentication-nps-extension/auth-flow.png)

## <a name="plan-your-deployment"></a>배포 계획

특별 한 구성이 필요 하지 hello NPS 확장은 자동 중복성을 처리 합니다.

Azure MFA가 사용되는 NPS 서버를 필요한 만큼 많이 만들 수 있습니다. 여러 서버를 설치한 경우 중 각각에 대해 다른 클라이언트 인증서를 사용해야 합니다. 각 서버에 대한 인증서를 만드는 것은 각 인증서를 개별적으로 업데이트할 수 있고 모든 서버 간의 가동 중지 시간을 걱정하지 않아도 된다는 의미입니다.

VPN 서버 67gb toobe hello 새 Azure MFA 사용이 가능한 NPS 서버를 인식 하므로 인증 요청을 라우팅합니다.

## <a name="prerequisites"></a>필수 조건

hello NPS 확장은 기존 인프라와 toowork는 의미 합니다. 시작 하기 전에 필수 구성 요소를 다음 hello 있는지 확인 합니다.

### <a name="licenses"></a>라이선스

hello Azure MFA에 대 한 NPS 확장으로 사용할 수 있는 toocustomers는 [Azure Multi-factor Authentication에 대 한 라이선스](multi-factor-authentication.md) (Azure AD Premium, EMS 또는 MFA 구독에 포함 됨).

### <a name="software"></a>소프트웨어

Windows Server 2008 R2 SP1 이상

### <a name="libraries"></a>라이브러리

이러한 라이브러리는 hello 확장명이 자동으로 설치 됩니다.
-   [Visual Studio 2013(X64)용 Visual C++ 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=40784)
-   [Windows PowerShell용 Microsoft Azure Active Directory 모듈 버전 1.1.166.0](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)

### <a name="azure-active-directory"></a>Azure Active Directory

Active Directory 동기화 된 tooAzure hello NPS 확장을 사용 하 여 모든 사용자 해야 Azure AD Connect를 사용 하 고 MFA를 등록 해야 합니다.

Hello 확장을 설치 하면 Azure AD 테 넌 트에 대 한 hello 디렉터리 ID 및 관리자 자격 증명이 필요 합니다. Hello에 디렉터리 ID를 찾을 수 [Azure 포털](https://portal.azure.com)합니다. 선택 hello 관리자 권한으로 로그인 **Azure Active Directory** hello 왼쪽에서 아이콘을 선택 합니다 **속성**합니다. Hello에 대 한 GUID 복사 hello **디렉터리 ID** 상자 하 고 저장 합니다. Hello NPS 확장을 설치할 때 hello 테 넌 트 ID로이 GUID를 사용 합니다.

![Azure Active Directory 속성에서 디렉터리 ID 찾기](./media/multi-factor-authentication-nps-extension/find-directory-id.png)

## <a name="prepare-your-environment"></a>환경 준비

원하는 tooprepare hello NPS 확장을 설치 하기 전에 사용자 환경 toohandle hello 인증 트래픽을 합니다.

### <a name="enable-hello-nps-role-on-a-domain-joined-server"></a>도메인에 가입 된 서버에 hello NPS 역할을 사용 하도록 설정

NPS 서버 hello tooAzure Active Directory를 연결 하 고 hello MFA 요청을 인증 합니다. 이 역할에 대한 서버를 한 개 선택하세요. RADIUS를 하지 않은 모든 요청에 대 한 오류를 throw 하는 hello NPS 확장 때문에 다른 서비스의 요청을 처리 하지 않는 하는 서버를 선택 하는 것이 좋습니다.

1. 서버에서 열고 hello **추가 역할 및 기능 마법사** hello 퀵 스타트 서버 관리자 메뉴에서에서 합니다.
2. 설치 유형에 대한 **역할 기반 또는 기능 기반 설치**를 선택합니다.
3. 선택 hello **네트워크 정책 및 액세스 서비스** 서버 역할입니다. 창이 팝업 되도록 tooinform 필수 기능 toorun 하는 경우이 역할입니다.
4. Hello 확인 페이지까지 hello 마법사를 계속 합니다. **설치**를 선택합니다.

또한이 서버 toohandle를 구성 해야 NPS에 대 한 지정 된 서버를가지고 hello VPN 솔루션에서에서 RADIUS 요청을 수신 합니다.

### <a name="configure-your-vpn-solution-toocommunicate-with-hello-nps-server"></a>VPN 솔루션 toocommunicate hello NPS 서버를 사용 하 여 구성

VPN 솔루션에 따라 사용, RADIUS 인증 정책 변경 단계 tooconfigure hello. 이 정책 toopoint tooyour RADIUS NPS 서버를 구성 합니다.

### <a name="sync-domain-users-toohello-cloud"></a>도메인 사용자 toohello 클라우드 동기화

이 단계에서 테 넌 트에 이미 있을 이지만 Azure AD Connect 데이터베이스 최근에 동기화가 좋은 toodouble 확인 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 관리자 권한으로 합니다.
2. **Azure Active Directory** > **Azure AD Connect** 선택
3. 동기화 상태가 **사용**이고 마지막 동기화가 1시간 미만인지 확인합니다.

지침을 hello us tookick 동기화의 새로운 라운드 해제 해야 할 경우 [Azure AD Connect 동기화: 스케줄러](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler)합니다.

### <a name="determine-which-authentication-methods-your-users-can-use"></a>사용자가 사용할 수 있는 인증 방법을 결정합니다.

어떤 인증 방법을 NPS 확장 배포와 함께 사용할 수 있는지에 영향을 미치는 두 가지 요소가 있습니다.

1. hello RADIUS 클라이언트 간에 사용 되는 hello 암호화 알고리즘이 (VPN, Netscaler 서버 또는 기타) 및 NPS 서버 hello 합니다.
   - **PAP** hello 클라우드에서 Azure MFA의 모든 hello 인증 방법을 지원: 전화 통화, 단방향 문자 메시지, 모바일 앱 알림 및 모바일 앱 확인 코드입니다.
   - **CHAPV2** 및 **EAP**는 전화 통화 및 모바일 앱 알림을 지원합니다.
2. hello 입력 클라이언트 응용 프로그램 hello 메서드 (VPN, Netscaler 서버 또는 기타)를 처리할 수 있습니다. 예를 들어 hello VPN 클라이언트에는 다른 방법 텍스트 또는 모바일 앱의 인증 코드에 tooallow hello 사용자 tootype?

Hello NPS 확장을 배포 하는 경우에 사용자를 위해 사용할 수 있는 어떤 방법이 이러한 요인 tooevaluate를 사용 합니다. RADIUS 클라이언트 PAP를 지 원하는 hello 클라이언트 UX에 확인 코드에 대 한 입력된 필드가 없는 경우 다음 전화 통화 및 모바일 앱 알림을 hello 방법은 두 가지가 지원 합니다.

Azure에서 [지원되지 않는 인증 방법을 사용하지 않도록 설정](multi-factor-authentication-whats-next.md#selectable-verification-methods)할 수 있습니다.

### <a name="enable-users-for-mfa"></a>MFA에 대한 사용자 설정

Hello 전체 NPS 확장을 배포 하기 전에 MFA tooenable tooperform 2 단계 인증을 사용 하지 않겠다고 hello 사용자가 필요 합니다. 바로 사용 가능한 추가 때 tootest hello 확장 배포, 완벽 하 게 Multi-factor Authentication에 등록 된 하나 이상의 테스트에서 계정이 필요 합니다.

이러한 단계 tooget 테스트 계정을 시작을 사용 합니다.
1. 역시 로그인[https://aka.ms/mfasetup](https://aka.ms/mfasetup) 테스트 계정을 사용 합니다. 
2. Hello 프롬프트 tooset을 확인 방법을를 따릅니다.
3. 조건부 액세스 정책을 만들거나 또는 [hello 사용자 상태를 변경](multi-factor-authentication-get-started-user-states.md) hello 테스트 계정에 대 한 toorequire 2 단계 인증 합니다. 

사용자가 또한 있어야만 toofollow 이러한 단계 tooenroll hello NPS 확장명이 인증할 수 있습니다.

## <a name="install-hello-nps-extension"></a>Hello NPS 확장 설치

> [!IMPORTANT]
> Hello NPS 확장 hello VPN 액세스 포인트와 다른 서버에 설치 합니다.

### <a name="download-and-install-hello-nps-extension-for-azure-mfa"></a>다운로드 하 고 Azure MFA에 대 한 hello NPS 확장을 설치 합니다.

1.  [Hello NPS 확장 다운로드](https://aka.ms/npsmfa) hello Microsoft 다운로드 센터에서에서.
2.  Hello 이진 toohello tooconfigure 원하는 네트워크 정책 서버에 복사 합니다.
3.  실행 *setup.exe* hello 설치 지침을 따릅니다. 오류가 발생 하면 해당 hello hello 필수 구성 요소 섹션에서 두 개의 라이브러리 성공적으로 설치를 다시 확인 하십시오.

### <a name="run-hello-powershell-script"></a>Hello PowerShell 스크립트 실행

이 위치에는 PowerShell 스크립트를 작성 하는 hello 설치 관리자: `C:\Program Files\Microsoft\AzureMfa\Config` (C:\는 설치 드라이브). 이 PowerShell 스크립트 hello 다음 작업을 수행 합니다.

-   자체 서명된 인증서를 만듭니다.
-   Hello hello 인증서 toohello 서비스에서 Azure AD 사용자의 공개 키를 연결 합니다.
-   Hello cert hello 로컬 컴퓨터 인증서 저장소에 저장 합니다.
-   권한 부여 액세스 toohello 인증서의 개인 키 tooNetwork 사용자입니다.
-   NPS hello를 다시 시작 합니다.

사용 하려는 경우가 아니면 toouse 사용자 고유의 인증서 (hello 자체 서명 된 인증서 대신 hello PowerShell 스크립트를 생성 하는) hello PowerShell 스크립트 toocomplete hello 설치를 실행 합니다. 여러 서버에 hello 확장을 설치 하는 경우 각 자체 인증서를 있어야 합니다.

1. 관리자 권한으로 Windows PowerShell을 실행합니다.
2. 디렉터리를 변경합니다.

   `cd "C:\Program Files\Microsoft\AzureMfa\Config"`

3. Hello 설치 프로그램에서 만든 hello PowerShell 스크립트를 실행 합니다.

   `.\AzureMfaNpsExtnConfigSetup.ps1`

4. PowerShell이 테넌트 ID에 대해 메시지를 표시합니다. Hello hello hello 전제 조건 섹션에서 Azure 포털에서에서 복사한 디렉터리 ID GUID를 사용 합니다.
5. 관리자 권한으로 tooAzure AD에에서 로그인 합니다.
6. PowerShell은 hello 스크립트가 완료 되 면 성공 메시지를 표시 합니다.  

부하 분산에 대해 tooset 되도록 추가 NPS 서버에서 다음이 단계를 반복 합니다.

>[!NOTE]
>Hello PowerShell 스크립트를 사용 하 여 인증서를 생성 하는 대신 자체 인증서를 사용 하는 경우 toohello NPS 명명 규칙을 정렬 됩니다 있는지 확인 합니다. 주체 이름 hello **CN =\<TenantID\>, OU = Microsoft NPS 확장**합니다. 

## <a name="configure-your-nps-extension"></a>NPS 확장 구성

이 섹션에는 성공적인 NPS 확장 배포를 위한 디자인 고려 사항 및 제안 사항이 포함되어 있습니다.

### <a name="configuration-limitations"></a>구성 제한 사항

- Azure MFA에 대 한 NPS 확장 hello 도구 toomigrate 사용자와 MFA 서버 toohello 클라우드에서 설정을 포함 되지 않습니다. 이러한 이유로 기존 배포 하지 않고 새 배포에 대 한 hello 확장을 사용 하는 것이 좋습니다. Tooperform 증명 접속 사용자에 게 기존 배포에서 hello 확장을 사용 하는 경우 다시 toopopulate가 MFA에 자세히 설명 hello 클라우드에서 합니다.  
- NPS 확장 hello hello UPN hello에서 온-프레미스 Active directory tooidentify hello Azure MFA에 hello 보조 인증 hello 확장을 수행 하기 위한 일 수 있습니다 구성된 toouse 대체 로그인 ID 또는 사용자 지정 Active Directory와 같은 다른 식별자를 사용 하 여 UPN 이외의 필드입니다. 참조 [고급 Multi-factor Authentication에 대 한 hello NPS 확장에 대 한 구성 옵션](multi-factor-authentication-advanced-vpn-configurations.md) 자세한 정보에 대 한 합니다.
- 모든 암호화 프로토콜이 모든 확인 메서드를 지원하는 것은 아닙니다.
   - **PAP**는 전화 통화, 단방향 문자 메시지, 모바일 앱 알림 및 모바일 앱 확인 코드를 지원합니다.
   - **CHAPV2** 및 **EAP**는 전화 통화 및 모바일 앱 알림을 지원합니다.

### <a name="control-radius-clients-that-require-mfa"></a>MFA가 필요한 RADIUS 클라이언트 제어

NPS 확장 hello를 사용 하 여 RADIUS 클라이언트에 대해 MFA를 사용 하면이 클라이언트에 대 한 모든 인증 필요 tooperform MFA 됩니다. 일부 RADIUS 클라이언트에 MFA tooenable 하려는 경우 두 명의 NPS 서버를 구성 하 고 그 중 하나에 hello 확장을 설치할 수 있습니다. Hello 확장으로 구성 toorequire MFA toosend 요청 toohello NPS 서버와 다른 RADIUS 클라이언트 toohello NPS 서버가 구성 되지 않음 hello 확장명이 원하는 RADIUS 클라이언트를 구성 합니다.

### <a name="prepare-for-users-that-arent-enrolled-for-mfa"></a>MFA에 등록되지 않은 사용자를 위한 준비

MFA에 대해 등록 되지 않은 사용자를 설정한 경우 tooauthenticate 하려고 할 때 수행 되는 작업을 확인할 수 있습니다. Hello 레지스트리 설정을 사용 하 여 *REQUIRE_USER_MATCH* hello 레지스트리 경로에 *HKLM\Software\Microsoft\AzureMFA* toocontrol hello 기능 동작입니다. 이 설정에는 다음과 같은 단일 구성 옵션이 있습니다.

| 키 | 값 | 기본값 |
| --- | ----- | ------- |
| REQUIRE_USER_MATCH | TRUE/FALSE | (해당 하는 tooTRUE)을 설정 하지 |

이 설정은 hello MFA에 대해 사용자 등록 되지 않은 경우 어떤 toodo toodetermine 됩니다. 때 hello 키 존재 하지 않거나을 설정 하지 않으면 tooTRUE, 설정 및 hello 사용자를 등록 하지 않은 hello 확장 실패 합니다 hello MFA 챌린지입니다. Hello 키가 설정 되어 tooFALSE hello 사용자가 등록 되지 않은 경우 MFA를 수행 하지 않고 인증이 진행 됩니다.

Toocreate이이 키를 선택 하 고 모두를 등록할 수 있음 Azure MFA에 대해 아직 하 고 사용자는 온 보 딩을 tooFALSE을 설정할 수 있습니다. 그러나 설정 hello 키 허용 하는 사용자에 MFA toosign에 대 한 등록 되지 않은 경우 이후 tooproduction 진행 하기 전에이 키를 제거 해야 합니다.

## <a name="troubleshooting"></a>문제 해결

### <a name="how-do-i-verify-that-hello-client-cert-is-installed-as-expected"></a>예상 대로 해당 hello 클라이언트 인증서가 설치 되어 확인 하려면 어떻게 해야 하나요?

Hello 인증서 저장소에 개인 키를 hello 검사 hello 설치 관리자에서 만든 자체 서명 된 인증서를 hello 부여 된 사용 권한이 toouser 찾아봅니다 **네트워크 서비스**합니다. hello 인증서의 주체 이름이 **CN \<tenantid\>, OU = Microsoft NPS 확장**

-------------------------------------------------------------

### <a name="how-can-i-verify-that-my-client-cert-is-associated-toomy-tenant-in-azure-active-directory"></a>Azure Active Directory에서 테 넌 트 관련된 toomy 내 클라이언트 인증서 인지 확인 하려면 어떻게 해야 합니까?

PowerShell 명령 프롬프트를 열고 다음 명령이 실행된 hello:

```
import-module MSOnline
Connect-MsolService
Get-MsolServicePrincipalCredential -AppPrincipalId "981f26a1-7f43-403b-a875-f8b09b8cd720" -ReturnKeyValues 1 
```

이 명령은 PowerShell 세션에서 테 넌 트 hello NPS 확장의 인스턴스와 연결 하는 모든 hello 인증서를 인쇄 합니다. 인증서에 대 한 클라이언트 인증서 hello 개인 키가 없는 "e-64로 인코딩된 X.509(.cer)" 파일로 내보내와 PowerShell에서 hello 목록과 비교 하십시오.

유효한-및 유효한-사람이 읽을 수 있는 형식에 있는 타임 스탬프 hello 명령 둘 이상의 인증서를 반환 하는 경우 사용 되는 toofilter 명백한 misfits 아웃 될 수 있습니다 때까지 합니다.

-------------------------------------------------------------

### <a name="why-are-my-requests-failing-with-adal-token-error"></a>내 요청이 ADAL 토큰 오류로 인해 실패하는 이유는 무엇입니까?

이 오류 때문일 수 있습니다 일부의 이유로 tooone 합니다. Toohelp 문제를 해결 하는 다음이 단계를 사용 합니다.

1. NPS 서버를 다시 시작합니다.
2. 클라이언트 인증서가 예상대로 설치되었는지 확인합니다.
3. 해당 hello 인증서가 Azure ad 테 넌 트와 연결을 확인 합니다.
4. Hello 확장을 실행 하는 hello 서버에서 액세스할 수 있는 해당 https://login.microsoftonline.com/를 확인 합니다.

-------------------------------------------------------------

### <a name="why-does-authentication-fail-with-an-error-in-http-logs-stating-that-hello-user-is-not-found"></a>알리는 hello 사용자를 찾을 수 없습니다는 HTTP 로그에 오류와 함께 인증이 실패 하는 이유

AD Connect를 실행 하 고 해당 hello 사용자는 Windows Active Directory 및 Azure Active Directory에 있는지 확인 합니다.

------------------------------------------------------------

### <a name="why-do-i-see-http-connect-errors-in-logs-with-all-my-authentications-failing"></a>내 모든 인증이 실패한 상태의 로그에 HTTP 연결 오류가 표시되는 이유는 무엇입니까?

Hello NPS 확장을 실행 하는 hello 서버에서 연결할 수 있는 해당 https://adnotifications.windowsazure.com를 확인 합니다.


## <a name="next-steps"></a>다음 단계

- 로그인에 대 한 대체 Id를 구성 하거나에 2 단계 인증을 수행 하지 않아야 하는 Ip에 대 한 예외 목록을 설정 [고급 Multi-factor Authentication에 대 한 hello NPS 확장에 대 한 구성 옵션](nps-extension-advanced-configuration.md)

- [Azure Multi-factor Authentication에 대 한 hello NPS 확장에서에서 오류 메시지를 해결 합니다.](multi-factor-authentication-nps-errors.md)
