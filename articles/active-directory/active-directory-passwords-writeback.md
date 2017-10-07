---
title: "비밀번호 쓰기 저장을 사용하는 Azure AD SSPR | Microsoft Docs"
description: "Azure AD와 Azure AD를 사용 하 여 연결 toowriteback 암호 tooon 온-프레미스 디렉터리"
services: active-directory
keywords: "Active Directory 암호 관리, 암호 관리, Azure AD 셀프 서비스 암호 재설정"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 6a1dd964a51b4f3b5b0be303b722ab6deb4a6110
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="password-writeback-overview"></a>암호 쓰기 저장 개요

암호 쓰기 저장은 Azure AD tooconfigure toowrite 암호 백업 tooyou 온-프레미스 Active Directory 허용 합니다. Hello 필요 tooset를 제거 하 고 복잡 한 온-프레미스 셀프 서비스 암호 재설정 솔루션을 관리 하 고는 편리한 클라우드 기반 방법을 제공 사용자 tooreset에 대 한 온-프레미스 암호는 어디서 나 합니다. 비밀번호 쓰기 저장은 [Azure Active Directory 버전](active-directory-editions.md)의 현재 구독자가 설정하여 사용할 수 있는 [Azure Active Directory Connect](./connect/active-directory-aadconnect.md) 구성 요소입니다.

Hello 같은 기능을 제공 하는 암호 쓰기 저장

* **지연 피드백 없음** - 비밀번호 쓰기 저장은 동기식 작업입니다. 사용자가 자신의 암호 정책을 만족 하지 않습니다 또는 없는 상태 toobe 다시 설정 하거나 어떤 이유로 든 변경할 경우 즉시 알림이 표시 됩니다.
* **AD FS 또는 기타 페더레이션 기술 사용자를 위한 암호 재설정 지원** -암호 쓰기 저장으로 hello 페더레이션된 사용자 계정이 동기화 Azure AD 테 넌 트로 된 수 toomanage 자신의 온-프레미스 AD hello 클라우드에서 암호입니다.
* **사용 하 여 사용자에 대 한 암호 재설정 지원 [암호 해시 동기화](./connect/active-directory-aadconnectsync-implement-password-synchronization.md)**  -hello 암호 재설정 서비스에서 발견 된 암호 해시 동기화에 대 한 동기화 된 사용자 계정이 사용 됨 모두이 계정의 다시 설정 하는 경우 온-프레미스 및 암호를 동시에 클라우드입니다.
* **액세스 패널 및 Office 365를 hello에서의 암호 변경 지원** -이 페더레이션 또는 해당 암호가 백 tooyour 로컬 AD 환경 작성 암호는 사용자 돌아와 toochange 만료 되거나 만료 되지 않은 암호를 동기화 합니다.
* **관리자를 다시 설정 하는 경우 암호 쓰기 저장에서는 Azure 포털 hello** hello에 대 한 사용자의 암호를 재설정 하는 관리자 때마다- [Azure 포털](https://portal.azure.com)해당 사용자가 페더레이션 또는 암호 동기화를 바로잡을 수 hello 경우, admin 님 안녕하세요 암호도 로컬 AD에서 선택합니다. 이 현재 지원 되지 않습니다 hello Office 관리 포털에서에서 합니다.
* **적용 온-프레미스 AD 암호 정책** -사용자가 암호를 재설정 하는 경우 온-프레미스에 맞는지 확인 toothat 디렉터리 커밋하기 전에 AD 정책입니다. 여기에는 기록, 복잡성, 나이, 암호 필터 및 로컬 AD에서 사용자가 정의한 기타 암호 제한 사항이 포함됩니다.
* **인바운드 방화벽 규칙이 필요 하지 않은** -암호 쓰기 저장 Azure 서비스 버스 릴레이 기본 통신 채널로 하지 않았는지 tooopen 인바운드 포트가 기능 toowork이에 대 한 방화벽에서 사용 합니다.
* **온-프레미스 Active Directory에서 보호된 그룹이 내에 존재하지 않는 사용자 계정에 대해 지원되지 않습니다** - 보호된 그룹에 대한 자세한 내용은 [Active Directory의 보호된 계정 및 그룹](https://technet.microsoft.com/library/dn535499.aspx)을 참조하세요.

## <a name="how-password-writeback-works"></a>암호 쓰기 저장의 작동 원리

페더레이션 또는 암호 해시 동기화 사용자 tooreset 가져오거나 hello 다음과 같은 결과가 발생 hello 클라우드에서 암호를 변경 합니다.

1. 어떤 유형의 암호 hello 사용자가 toosee 확인 합니다.
    * Hello 암호가 온-프레미스에서 관리 하는 표시 하는 경우
        * 쓰기 저장 서비스가 실행 중인지와 hello 사용자 진행 하도록 실행,이 경우 경우 hello 확인
        * Hello 쓰기 저장 서비스를 없으면 위치도 제공 hello 사용자가 암호를 지금 재설정할 수 없습니다.
2. 다음으로 hello 사용자 hello 적절 한 인증 게이트를 전달 하 고 암호 다시 설정 hello 화면에 도달 합니다.
3. 새 암호를 선택 하 고이 확인 하는 hello 사용자.
4. 제출을 클릭 하면 hello 쓰기 저장 설정 프로세스 중에 생성 된 대칭 키로 hello 일반 텍스트 암호를 암호화 합니다.
5. Hello 암호를 암호화 한 후 포함 된 HTTPS 채널 tooyour 테 넌 트 관련 서비스 버스 릴레이 (도를 설정 하면에 대 한 hello 쓰기 저장 설정 프로세스 중)로 전송 되는 페이로드입니다. 이 릴레이는 온-프레미스 설치만 알고 있는 임의로 생성된 암호에 의해 보호됩니다.
6. Hello 메시지가 서비스 버스에 도달 하면 hello 암호 다시 설정 끝점이 자동으로 다시 시작 및 다시 설정 요청이 보류 중 중임을 알게 합니다.
7. hello 서비스 다음 찾습니다 hello 사용자에 대 한 문제의 hello 클라우드 앵커 특성을 사용 하 여 합니다. 이 조회 toosucceed에 대 한:

    * hello 사용자 개체 hello AD 커넥터 공간에에서 있어야 합니다.
    * hello 사용자 개체에 연결 된 toohello 해당 MV 개체 여야 합니다.
    * hello 사용자 개체에 연결 된 toohello 해당 AAD 커넥터 개체 여야 합니다.
    * hello AD 커넥터 개체 tooMV에서 링크 hello 동기화 규칙이 있어야 `Microsoft.InfromADUserAccountEnabled.xxx` hello 링크 합니다. <br> <br>
    Hello 클라우드에서 hello 호출이 들어오면 때 hello 동기화 엔진이 사용 하는 hello AAD 커넥터 공간 개체를 cloudAnchor 특성 toolook hello 하 hello 링크 백 toohello MV 개체 뒤에 오는 다음 hello 링크 백 toohello AD 개체를 따릅니다. 동일한 사용자 hello 동기화 엔진이 hello에 의존 하는 hello에 대 한 하는 여러 AD 개체 (다중 포리스트) 있을 수 있으므로 `Microsoft.InfromADUserAccountEnabled.xxx` 링크 toopick hello 하나를 수정 합니다.

    > [!Note]
    > 이 논리의 결과 수 toocommunicate 암호 쓰기 저장 toowork에 대 한 PDC 에뮬레이터 hello로 Azure AD Connect에 있어야 합니다. Tooenable를 수동으로 수행 해야 할 경우 hello를 마우스 오른쪽 단추로 클릭 하 여 Azure AD Connect toohello PDC 에뮬레이터를 연결할 수 있습니다 **속성** hello Active Directory 동기화 커넥터를 선택 하면 다음의 **구성 디렉터리 파티션**합니다. 여기에서 hello에 대 한 확인 **도메인 컨트롤러 연결 설정을** 섹션 및 hello 확인란 라는 **만 선호 도메인 컨트롤러를 사용 하 여**합니다. Hello DC가 PDC 에뮬레이터에서 앱을 원하는 경우에 Azure AD Connect tooconnect toohello PDC 암호 쓰기 저장을 시도 합니다.

8. 회원님께 hello 사용자 계정이 발견 되 면 적절 한 AD 포리스트 hello에 직접 tooreset hello 암호입니다.
9. Hello 암호 설정 작업이 성공 하면 알립니다 hello 사용자의 암호가 변경 되었습니다.
    > [!NOTE]
    > Hello 경우 hello 사용자 암호가 동기화 된 tooAzure AD 암호 동기화를 사용 하는 수 있으므로 hello 온-프레미스 암호 정책이 hello 클라우드 암호 정책 보다 약한 합니다. 이 경우에서는 어떤 hello 온-프레미스 정책 이며 해당 암호 해시 동기화 toosynchronize hello 해시 암호를 대신 허용에 여전히 적용 합니다. 이렇게 하면 온-프레미스 정책에는 적용 되도록 hello 클라우드에서 관계 없이 암호 동기화 또는 페더레이션 tooprovide를 사용 하는 경우 단일 로그온 합니다.

10. Hello 암호 설정 작업이 실패 하는 경우 hello toohello 사용자가 오류를 반환 했습니다 및 다시 시도 수 있도록 합니다.
    * hello 작업이 hello 다음으로 인해 실패할 수 있습니다.
        * hello 서비스가 가동 중단 되었거나
        * 선택한 hello 암호가 조직 정책을 충족 하지 않는
        * 찾을 수 없는 hello 사용자 hello 로컬 AD에서

    이러한 많은 경우에 대 한 메시지 보내기 및 수행할 수 있는 작업 hello 사용자에 게 알림 특정 한 tooresolve hello 문제입니다.

## <a name="configuring-password-writeback"></a>비밀번호 쓰기 저장 구성

hello 자동 업데이트 기능을 사용 하는 것이 좋습니다 [Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md) toouse 암호 쓰기 저장 하려는 경우.

디렉터리 동기화 및 Azure AD Sync는 더 이상 암호 쓰기 저장 hello 문서를 사용 하면 지원 되는 방법을 [디렉터리 동기화 및 Azure AD Sync에서 업그레이드](connect/active-directory-aadconnect-dirsync-deprecated.md) 전환와 자세한 정보 toohelp 했습니다.

hello 단계 아래 가정 hello를 사용 하 여 사용자 환경에서 Azure AD Connect를 이미 구성한 [Express](./connect/active-directory-aadconnect-get-started-express.md) 또는 [사용자 지정](./connect/active-directory-aadconnect-get-started-custom.md) 설정 합니다.

1. 암호 쓰기 저장 사용 및 tooconfigure tooyour Azure AD Connect 서버 로그인 및 hello 시작 **Azure AD Connect** 구성 마법사.
2. Hello 시작 화면에 클릭 **구성**합니다.
3. hello 추가 작업 화면 클릭 **동기화 옵션을 사용자 지정** 선택한 후 **다음**합니다.
4. Hello 연결 tooAzure AD 화면에 전역 관리자 자격 증명을 입력 하 고 선택 **다음**합니다.
5. Hello 디렉터리 및 도메인을 연결 하 고 선택할 수 있습니다 화면을 필터링 하는 OU **다음**합니다.
6. Hello 선택적 기능 화면 확인란 hello 다음 너무**암호 쓰기 저장** 클릭 **다음**합니다.
   ![Azure AD Connect에서 비밀번호 쓰기 저장 사용][Writeback]
7. Hello 준비 tooconfigure 화면 클릭 **구성** hello 프로세스 toocomplete 될 때까지 기다립니다.
8. [구성 완료]가 표시되면 **종료**를 클릭하면 됩니다.

## <a name="licensing-requirements-for-password-writeback"></a>비밀번호 쓰기 저장에 대한 라이선스 요구 사항

라이선스, 참조에 대 한 정보에 대 한 hello 항목 [암호 쓰기 저장에 필요한 라이선스](active-directory-passwords-licensing.md#licenses-required-for-password-writeback) hello 다음 사이트 또는

* [Azure Active Directory 가격 책정 사이트](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Secure Productive Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

### <a name="on-premises-authentication-modes-supported-for-password-writeback"></a>비밀번호 쓰기 저장에 지원되는 온-프레미스 인증 모드

사용자 암호 유형만 hello에 대 한 암호 쓰기 저장이 작동 합니다.

* **클라우드 전용 사용자**: 온-프레미스 암호가 없기 때문에 비밀번호 쓰기 저장은 이 상황에서 적용되지 않음
* **암호 동기화된 사용자**: 비밀번호 쓰기 저장이 지원됨
* **페더레이션된 사용자**: 비밀번호 쓰기 저장이 지원됨
* **통과 인증 사용자**: 비밀번호 쓰기 저장이 지원됨

### <a name="user-and-admin-operations-supported-for-password-writeback"></a>비밀번호 쓰기 저장에 지원되는 사용자 및 관리자 작업

암호는 상황에 따라 모든 hello에 다시 기록 됩니다.

* **지원되는 최종 사용자 작업**
  * 모든 최종 사용자 셀프 서비스 자발적 변경 암호 작업
  * 모든 최종 사용자 셀프 서비스 적용 변경 암호 작업(예: 암호 만료)
  * 모든 최종 사용자 셀프 서비스 암호 재설정 hello에서 시작 된 [암호 재설정 포털](https://passwordreset.microsoftonline.com)
* **지원되는 관리자 작업**
  * 모든 관리자 셀프 서비스 자발적 변경 암호 작업
  * 모든 관리자 셀프 서비스 적용 변경 암호 작업(예: 암호 만료)
  * 모든 관리자가 셀프 서비스 암호 재설정 hello에서 시작 된 [암호 재설정 포털](https://passwordreset.microsoftonline.com)
  * 모든 최종 사용자 관리자 시작한 암호 hello를 다시 설정 [Azure 클래식 포털](https://manage.windowsazure.com)
  * 모든 최종 사용자 관리자 시작한 암호 hello를 다시 설정 [Azure 포털](https://portal.azure.com)

### <a name="user-and-admin-operations-not-supported-for-password-writeback"></a>비밀번호 쓰기 저장에 지원되지 않는 사용자 및 관리자 작업

암호는 **하지** hello 다음 상황 중 하나에 다시 작성 합니다.

* **지원되지 않는 최종 사용자 작업**
  * PowerShell v1, v2, 또는 hello Azure AD Graph API 사용 하 여 자신의 암호를 재설정 하는 모든 최종 사용자
* **지원되지 않는 관리자 작업**
  * 모든 최종 사용자 관리자 시작한 암호 hello를 다시 설정 [Office 관리 포털](https://portal.office.com)
  * 모든 최종 사용자 관리자 시작한 암호 PowerShell v1, v2, 또는 hello Azure AD Graph API 다시 설정

이러한 제한은 tooremove 작업 하는, 특정 timeline 아직 공유할 수 있습니다 갖지 않습니다 했습니다.

## <a name="password-writeback-security-model"></a>암호 쓰기 저장 보안 모델

비밀번호 쓰기 저장은 매우 안전한 서비스입니다.  사용자 정보를 보호 tooensure, 아래에 설명 되어 있는 4 계층 보안 모델을 설정 합니다.

* **테넌트별 Service Bus Relay**
  * Hello 서비스를 설정 하는 경우 임의로 생성 된 강력한 암호를 Microsoft에 대 한 액세스에 의해 보호 되는 테 넌 트 관련 서비스 버스 릴레이를 설정 합니다.
* **잠겨 있는 강력한 암호 암호화 키**
  * Hello 서비스 버스 릴레이 만든 후 hello 유선을 통해 도착을 tooencrypt hello 암호 사용 강력한 대칭 키를 만듭니다. 이 키는 hello 클라우드의 과도 하 게 잠기고 hello 디렉터리에 암호와 마찬가지로 감사는 회사의 보안 저장소에만 실행 됩니다.
* **업계 표준 TLS**
  1. 암호 다시 설정 하거나 변경 하는 경우 작업이 발생 hello 클라우드에서 hello 일반 텍스트 암호를 사용 하 고 공개 키로 암호화 합니다.
  2. 에서는 다음 배치 하는 Microsoft의 SSL 인증서 tooyour 서비스 버스 릴레이 사용 하 여 암호화 된 채널을 통해 전송 되는 HTTPS 메시지로 합니다.
  3. Hello 메시지에 도착 하면 서비스 버스, 온-프레미스 에이전트 절전 모드 해제를 인증 후 이전에 생성 된 강력한 암호를 hello tooService 버스를 사용 하 여 합니다.
  4. 온-프레미스 에이전트 hello 암호화 된 메시지를 선택, 생성 된 hello 개인 키를 사용 하 여 암호를 해독 합니다.
  5. 온-프레미스 에이전트 hello AD DS SetPassword API를 통해 tooset hello 암호를 시도합니다.
     * 이 단계는 tooenforce 수 있습니다 AD 온-프레미스 암호 정책 (복잡성, 사용 기간, 기록, 필터, 등) hello 클라우드에서 합니다.
* **메시지 만료 정책** 
  * Hello 메시지 온-프레미스 서비스가 다운 된 때문에 서비스 버스에 위치, 시간 초과 됩니다 하 고 몇 분 tooincrease 보안 후에 제거 됩니다.

### <a name="password-writeback-encryption-details"></a>비밀번호 쓰기 저장 암호화 세부 정보

사용자가 전송한 후, 온-프레미스 환경, tooensure 최대 서비스 안정성 및 보안에 도착 하기 전에 암호 재설정 요청을 통해 이동 하는 hello 암호화 단계에 대 한 설명은 다음과 같습니다.

* **1 단계-2048 비트 RSA 키로 암호 암호화** -사용자가 온-프레미스 tooon, 첫 번째, hello 제출 된 암호 자체 다시 기록 암호 toobe 2048 비트 RSA 키로 암호화 되어 전송 하 고 나면 합니다.
* **2 단계-AES GCM과 함께 패키지 수준 암호화** -다음 hello 전체 패키지 (암호 + 필요한 메타 데이터) AES GCM을 사용 하 여 암호화 됩니다. 이렇게 하면 직접 액세스 toohello 기본 ServiceBus 채널 가진 사람이 면 누구나 hello 내용으로 보기/변조 되지 않도록 수 없습니다.
* **3 단계-모든 통신이 이루어지는 tls / SSL** -SSL/TLS 채널에서 발생 하는 서비스 버스와 모든 hello 통신 합니다. 이 인증 되지 않은 타사에서 hello 내용을 보호합니다.
* **자동 키 롤오버 이후 6 개월 마다** -자동으로 6 개월 마다 암호 쓰기 저장은 비활성화 / Azure AD Connect에 다시 설정 될 때마다 또는 우리 롤오버 모든 키 tooensure 최대 서비스 보안 및 안전 합니다.

### <a name="password-writeback-bandwidth-usage"></a>비밀번호 쓰기 저장 대역폭 사용

암호 쓰기 저장은 저대역폭을 보내는 서비스를 다시 toohello 온-프레미스 에이전트의 경우 다음 hello 인 경우에 요청:

1. 두 개의 메시지를 사용 하도록 설정 하거나 Azure AD Connect 통해 hello 기능을 사용 하지 않도록 설정 하면 전송 합니다.
2. 하나의 메시지 hello 서비스가 실행 되 고으로 분 마다 한 번씩 5에 대 한 서비스 하트 비트가로 보내집니다.
3. 두 개의 메시지는 새 암호를 전송할 때 각각 전송됩니다.
    * 요청 tooperform hello 작업으로 첫 번째 메시지
    * 두 번째 메시지를 hello 연산의 hello 결과 포함 하 고 상황에 따라 hello에 전송 됩니다.
        * 사용자 셀프 서비스 비밀번호 다시 설정 중에 새 비밀번호가 제출될 때마다
        * 사용자 비밀번호 변경 작업 중에 새 비밀번호가 제출될 때마다
        * 될 때마다 새 암호는 관리자가 시작한 사용자 암호 ("hello Azure 관리 포털에만 해당)에서 재설정 하는 동안 전송 됩니다.

#### <a name="message-size-and-bandwidth-considerations"></a>메시지 크기 및 대역폭 고려 사항

일반적으로 위에서 설명한 hello 메시지의 각 hello 크기는 아래에서 1kb 극단적인 로드가, 대역폭의 몇 가지 k b / 초를 소비 하는 hello 암호 쓰기 저장 서비스 자체는 합니다. 암호 업데이트 작업에 필요한 경우에 각 메시지를 실시간으로 보낸이 고 되므로 hello 메시지 크기는 매우 작으므로 hello 대역폭 사용량 hello 쓰기 저장 기능을 효과적으로 너무 작은 toohave 모든 실제 크게 영향을 합니다.

## <a name="next-steps"></a>다음 단계

링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.

* [**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작 
* [**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성
* [**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법
* [**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자
* [**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.
* [**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정
* [**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색
* [**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법
* [**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로? 그 이유는 무엇을? 어디서? 누가? 언제? -Tooask 항상 필요한 tooquestions 답변
* [**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다

[Writeback]: ./media/active-directory-passwords-writeback/enablepasswordwriteback.png "Azure AD Connect에서 비밀번호 쓰기 저장 사용"
