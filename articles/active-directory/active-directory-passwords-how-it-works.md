---
title: "자세히 알아보기: Azure AD SSPR | Microsoft Docs"
description: "Azure AD 셀프 서비스 암호 재설정 자세히 알아보기"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 618c5908-5bf6-4f0d-bf88-5168dfb28a88
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: c177192bbe69d179a25d174b06a0813ec28e2615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-password-reset-in-azure-ad-deep-dive"></a>Azure AD에서 셀프 서비스 암호 재설정 자세히 알아보기

SSPR는 어떻게 작동하나요? Hello 인터페이스에서 해당 옵션 의미 Azure AD 셀프 서비스 암호에 대 한 자세한 내용을 toofind 계속 다시 설정 합니다.

## <a name="how-does-hello-password-reset-portal-work"></a>Hello 암호 포털 작업을 재설정 하는 방법

사용자가 암호 재설정 포털 toohello, toodetermine 워크플로 시작 됩니다.

   * Hello 페이지 지역화 어떻게?
   * Hello 사용자 계정이 유효
   * 어떤 조직 hello 사용자에 속하지?
   * 여기서 hello 사용자의 암호 관리 되는지 여부
   * hello 사용자 사용이 허가 된 toouse hello 기능이입니다.


Hello 암호 재설정 페이지 뒤에 있는 hello 논리에 대 한 toolearn 아래 hello 단계를 자세히 읽습니다.

1. 사용자가 클릭 hello 계정 링크에 액세스할 수 없거나 너무 라인 직접[https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com)합니다.
2. 기반 hello 브라우저 로캘 hello 경험 hello 적절 한 언어로 렌더링 됩니다. hello 암호 재설정 환경 언어로 지역화 하는 Office 365에서 지 원하는 동일한 언어를 hello 합니다.
3. 사용자 ID를 입력하고 captcha를 전달합니다.
4. Azure AD hello 사용자 수 toouse 되는지 확인 hello 다음을 수행 하 여이 기능:
   * hello이 사용자는이 기능은 설정 되 고 할당 된 Azure AD 라이선스를 확인 합니다.
     * Hello 사용자가 없으면이 기능 사용 또는 라이선스가 할당 하는 경우 hello 사용자는 자신의 관리자 tooreset toocontact 요청 암호입니다.
   * 해당 hello 사용자에 게 관리자 정책에 따라 자신의 계정에 정의 된 hello 오른쪽 인증 데이터를 확인 합니다.
     * 정책에 하나의 인증만 필요한 경우 확인는 hello이 사용자는 hello 관리자 정책에서 사용 하는 hello 과제 중 하나 이상에 대해 정의 된 hello 적절 한 데이터입니다.
       * Hello 사용자가 구성 되지 않은 사용자 hello 없으면이 권장된 toocontact 자신의 관리자 tooreset를는 암호입니다.
     * Hello 정책 두 개의 인증이 필요한 경우 확인는 hello이 사용자는 hello 관리자 정책에서 사용 하는 hello 과제 중 적어도 두 개에 대해 정의 된 hello 적절 한 데이터입니다.
       * Hello 사용자 구성 되지 않은 경우 사용자 hello 것이 권장된 toocontact 자신의 관리자 tooreset가 자신의 암호입니다.
   * Hello 사용자 암호가 온-프레미스 (페더레이션 또는 암호 해시 동기화)에서 관리 하는 경우를 확인 합니다.
     * 쓰기 저장이 배포 된 hello 사용자 암호가 온-프레미스에서 관리 되는 경우 hello 사용자 tooproceed tooauthenticate ï ´ ù 및 암호를 재설정 합니다.
     * 쓰기 저장이 배포 되지 않은 및 hello 사용자 암호가 온-프레미스로 관리 되는 경우 hello 사용자는 자신의 관리자 tooreset toocontact 요청 암호입니다.
5. 해당 hello 사용자 수는 확인 되는 경우 toosuccessfully 암호를 재설정 한 후 hello 사용자 hello 재설정 프로세스가 안내 됩니다.

## <a name="authentication-methods"></a>인증 방법

셀프 서비스 암호 재설정 (SSPR)를 사용 하는 hello 다음 인증 방법에 대 한 옵션 중 하나 이상을 선택 해야 합니다. 사용자가 더 유연하게 사용할 수 있도록 두 개 이상의 인증 방법을 선택하는 것이 좋습니다.

* Email
* 휴대폰
* 사무실 전화
* Security Questions(보안 질문)

### <a name="what-fields-are-used-in-hello-directory-for-authentication-data"></a>인증 데이터에 대 한 hello 디렉터리 어떤 필드가 사용

* 사무실 전화에 전화 tooOffice 해당
    * 사용자가이 필드는 관리자가 정의 되어야 자체 수 없습니다 tooset
* 휴대폰 해당 tooeither 인증 전화 (공개적으로 볼 수 없음) 또는 휴대폰 (공개적으로 표시 됨)
    * hello 서비스 인증 전화를 먼저 찾습니다, 그리고 다음 대체 전화 tooMobile 없는 경우
* Tooeither 인증 전자 메일 (공개적으로 볼 수 없음) 또는 대체 전자 메일을 해당 하는 대체 전자 메일 주소
    * hello 서비스 인증 전자 메일을 먼저, 찾습니다 백 tooAlternate 전자 메일은 실패 합니다.

기본적으로만 hello 클라우드 특성 사무실 전화 및 이동 전화 인증 데이터에 대 한 온-프레미스 디렉터리에서 tooyour 클라우드 디렉터리를 동기화 합니다.

사용자가 암호 관리자에 게 해당 인증 방법의 hello 있는 데이터가 있는 경우 사용 하도록 설정한만 재설정 수 및 필요 합니다.

사용자가 원하지 않는 자신의 휴대폰 번호 toobe hello 디렉터리에 표시 되지만 여전히 toouse 같은 것 암호 재설정을 위해 관리자 해야 하지 hello 디렉터리에 고 채우고 hello 사용자 채워야 다음 자신의 **인증 전화**  hello 통해 특성 [암호 재설정 등록 포털](http://aka.ms/ssprsetup)합니다. 관리자 hello 사용자의 프로필에이 정보를 볼 수 있지만 다른 곳에서 게시 되지 않습니다. Azure 관리자 계정 인증 전화 번호를 등록 하면 hello 휴대폰 필드에 입력 하 고 표시 됩니다.

### <a name="number-of-authentication-methods-required"></a>필수 인증 방법의 수

이 옵션 hello 최소 사용자 tooreset 거쳐야 hello 사용할 수 있는 인증 방법 수를 결정 합니다. 자신의 암호를 잠금 해제 하 고 tooeither 1 또는 2를 설정할 수 있습니다.

Hello 관리자가 설정 된 경우 사용자가 인증 방법을 더 toosupply 선택할 수 있습니다.

관리자 tooreset toorequest 안내 하는 오류 페이지를 참조 하 고 사용자에 필요한 최소 hello 메서드를 등록 하는 경우 암호입니다.

### <a name="how-secure-are-my-security-questions"></a>보안 질문은 얼마나 안전한가요?

보안 질문을 사용 하는 경우 것이 좋습니다을 사용 중인 다른 메서드로 대로 어떤 사람들 hello 답변 tooanother 사용자 질문 알 수 있습니다 다른 방법 보다 보안 수준이 낮을 수 있습니다.

> [!NOTE] 
> 보안 질문 hello 디렉터리에 사용자 개체에 비공개적으로 안전 하 게 저장 되 고 등록 하는 동안 사용자가 대답만 수 있습니다. 관리자 tooread에 대 한 방법이 있으면는 사용자가 수정 하거나 질문 또는 대답 합니다.
>

### <a name="security-question-localization"></a>보안 질문 지역화

다음에 나오는 모든 미리 정의 된 질문 hello 사용자의 브라우저 로캘을 기반으로 하는 Office 365 언어 중 일부만 hello로 지역화 됩니다.

* 배우자/파트너를 처음 만난 도시는 어디인가요?
* 부모님이 처음 만난 도시는 어디인가요?
* 가장 가까운 형제 자매가 사는 도시는 어디인가요?
* 아버지가 출생하신 도시는 어디인가요?
* 첫 직장이 있는 도시는 어디인가요?
* 어머니가 출생하신 도시는 어디인가요?
* 2000년에 새해를 맞은 도시는 어디인가요?
* Hello 높은에서 가장 좋아하는 선생님의 성은 무엇입니까 * 학교?
* Hello 적용 대학의 이름은 무엇입니까 toobut स ा?
* hello 검사가 있는 사용자 첫 번째 결혼 피로연 hello 이름은 무엇입니까?
* 아버지의 중간 이름은 무엇인가요?
* 가장 좋아하는 음식은 무엇인가요?
* 외할머니의 성함은 무엇인가요?
* 어머니의 중간 이름은 무엇인가요?
* 가장 손위인 형제 자매의 생년월일은 언제인가요? (예: 1985년 11월)
* 가장 손위인 형제 자매의 중간 이름은 무엇인가요?
* 친할아버지의 성함은 무엇인가요?
* 가장 손아래인 형제 자매의 중간 이름은 무엇인가요?
* 6학년 때 다닌 학교는 어디인가요?
* 어떤 처음 hello च े 어린 시절 가장 친한 친구의 ं?
* 어떤 처음 hello च े 첫 번째 배우자의 ं?
* hello 가장 좋아하는 초등학교 선생님의 성은 무엇 이었습니까?
* 첫 번째 자동차 또는 오토바이의 hello 제조업체 및 모델 무엇 이었습니까?
* Hello 처음 다닌 학교의의 hello 이름은 무엇 이었습니까?
* 태어난 hello 병원의 hello 이름은 무엇 이었습니까?
* त ल ् ल े ं घ hello 이름을 hello?
* 어린 시절 영웅의 hello 이름은 무엇 이었습니까?
* 가장 좋아하는 봉 제 동물 인형의 hello 이름은 무엇 이었습니까?
* 첫 번째 애완 동물의 hello 이름은 무엇 이었습니까?
* 어린 시절 별명은 무엇인가요?
* 고등학교 때 가장 좋아한 스포츠는 무엇인가요?
* 첫 번째 직업은 무엇인가요?
* 어린 시절 전화 번호의 마지막 4 자리 hello 된 무엇입니까?
* त न ा, 무엇이 고 싶 었 toobe ज ा त?
* 누구 hello ळ ् य ा가 입니까?

### <a name="custom-security-questions"></a>사용자 지정 보안 질문

사용자 지정 보안 질문은 여러 로캘로 지역화되지 않습니다. 모든 사용자 지정 질문 hello에 표시 되는 hello 관리 사용자 인터페이스에 입력 된 hello 사용자의 브라우저 로캘 차이가 있는 경우에 동일한 언어입니다. 지역화 된 질문 해야 할 경우 미리 정의 된 hello 질문을 사용 하십시오.

사용자 지정 보안 질문의 hello 최대 길이 200 자입니다.

### <a name="security-question-requirements"></a>보안 질문 요구 사항

* 최소 질문 문자 수 제한은 3자입니다.
* 최대 질문 문자 수 제한은 40자입니다.
* 사용자가 여러 번의 문을 제기 동일 hello 응답 하지 않을 수 있습니다.
* 사용자가 hello를 제공 하지 않을 수 있습니다 하나 질문 보다 toomore 대답 동일
* 사용 되는 toodefine 질문 및 답변 유니코드 문자를 포함 하 여 모든 문자 집합 수 있습니다.
* hello 정의 하는 질문 수보다 크거나 같아야 합니다 보다 큰 질문 필요한 tooregister toohello 수

## <a name="registration"></a>등록

### <a name="require-users-tooregister-when-signing-in"></a>에 로그인 할 때 사용자가 tooregister 필요

이 옵션을 사용 하면 사용자 암호를 사용할 수는 재설정 toocomplete hello 암호 재설정 등록에서 수행 하는 것과 같은 Azure AD toosign를 사용 하 여 tooapplications를 로그인 하는 경우 필요 합니다.

* Office 365
* Azure 포털
* 액세스 패널
* 페더레이션된 응용 프로그램
* Azure AD를 사용하여 응용 프로그램 사용자 지정

이 기능을 해제 하면 계속 사용자 toomanually 레지스터 그들의 연락처 정보 방문 하 여 [http://aka.ms/ssprsetup](http://aka.ms/ssprsetup) hello를 클릭 하 여 **암호 재설정에 등록할** hello 링크 hello 액세스 패널의 프로필 탭입니다.

> [!NOTE]
> 사용자가 hello 창을 닫기 또는 취소를 클릭 하 여 hello 암호 재설정 등록 포털을 해제할 수 있지만 될 때마다 등록을 완료할 때까지 사용자가 로그인 하 라는 메시지가 표시 됩니다.
>

### <a name="number-of-days-before-users-are-asked-tooreconfirm-their-authentication-information"></a>수 일 전에 사용자가 요청 tooreconfirm 해당 인증 정보

이 옵션을 설정 하 고 인증 정보 reconfirming 사이의 hello 기간 결정 되며 hello를 사용 하는 경우 사용할 수만 **에 로그인 할 때 사용자가 tooregister 필요** 옵션입니다.

유효한 값은 0-730 일 0 사용자 tooreconfirm 해당 인증 정보 묻지 않음

## <a name="notifications"></a>알림

### <a name="notify-users-on-password-resets"></a>사용자에게 암호 재설정에 대해 알림

이 옵션은 tooyes 설정, 그런 다음 hello 사용자가 암호를 재설정 하는 hello SSPR 포털 tootheir 주를 통해 해당 암호가 변경 되었습니다 및 대체 전자 메일을 파일에 Azure AD에서 해결 됨을 알리는 전자 메일을 받습니다. 누구도 이 재설정 이벤트의 알림을 받지 않습니다.

### <a name="notify-all-admins-when-other-admins-reset-their-passwords"></a>다른 관리자가 암호를 재설정하면 모든 관리자에게 알림

이 옵션 설정 경우 tooyes, 다음 **모든 관리자** 다른 관리자가 SSPR을 사용 하 여 자신의 암호를 변경 된 것을 알리는 Azure AD에서 파일에 대해 전자 메일 tootheir 기본 전자 메일 주소를 수신 합니다.

예제: 환경에 4명의 관리자가 있습니다. 관리자 "A"는 SSPR을 사용하여 해당 암호를 재설정합니다. 관리자 B, C 및 D는 이를 알리는 전자 메일을 수신합니다.

## <a name="on-premises-integration"></a>온-프레미스 통합

Azure AD Connect를 설치, 구성 및 사용하도록 설정하는 경우 온-프레미스 통합에 추가 옵션이 생성됩니다.

### <a name="write-back-passwords-tooyour-on-premises-directory"></a>암호 tooyour 온-프레미스 디렉터리 쓰기 저장

이 디렉터리에 대해 암호 쓰기 저장을 활성화 하는 지 여부를 제어 하 고 쓰기 저장에 있으면 hello 온-프레미스 쓰기 저장 서비스의 hello 상태를 나타냅니다. Azure AD Connect를 다시 구성 하지 않고 tootemporarily 사용 안 함 hello 암호 쓰기 저장을 원하는 경우에 유용 합니다.

* Hello 전환에 있으면 집합 tooyes 쓰기 저장 사용 하도록 설정 되며 페더레이션 및 암호 해시 동기화 사용자 수 tooreset 됩니다 암호.
* Hello 전환에 있으면 집합 toono 비활성화 되 고 페더레이션 쓰기 저장 및 암호 해시 동기화 사용자 수 tooreset 됩니다 암호.

### <a name="allow-users-toounlock-accounts-without-resetting-their-password"></a>사용자가 자신의 암호를 재설정 하지 않고 toounlock 계정 허용

Hello 암호 재설정 포털을 방문 하는 사용자가 암호를 재설정 하지 않고 자신의 온-프레미스 Active Directory 계정 지정된 hello 옵션 toounlock 해야 하는지 여부를 지정 합니다. 기본적으로 Azure AD는 항상 계정 잠금 해제 암호 재설정을 수행할 때,이 설정을 통해 tooseparate 작업 합니다. 

* 경우 "yes" 사용자 지정된 hello 옵션 tooreset 암호 수를 hello 계정 또는 toounlock hello 암호를 재설정 하지 않고 잠금을 해제 한 후 너무 설정 합니다.
* 경우 설정 너무 "no" 인 사용자만 수 tooperform 됩니다 결합 된 암호 재설정 및 계정 잠금 해제 작업입니다.

## <a name="network-requirements"></a>네트워크 요구 사항

### <a name="firewall-rules"></a>방화벽 규칙

[Microsoft Office URL 및 IP 주소 목록](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)

이상에서는 및 Azure AD Connect 1.1.443.0 버전에 대 한 아웃 바운드 HTTPS 액세스 toohello 다음 필요 하며
* passwordreset.microsoftonline.com
* servicebus.windows.net

보다 세부적인 액세스에 대 한 Microsoft Azure 데이터 센터 IP 범위 수요일 마다 업데이트 되어 효과 hello 다음에 배치 하는 hello 업데이트 목록을 찾을 수 있습니다 월요일 [여기](https://www.microsoft.com/download/details.aspx?id=41653)합니다.

### <a name="idle-connection-timeouts"></a>유휴 연결 시간 제한

hello Azure AD Connect 도구 주기적 ping/keepalives tooServiceBus 끝점 tooensure를 hello 연결 유지를 보냅니다. 너무 많은 연결이 중지 되 고 됩니다 hello 도구 검색 해야, 것 ping toohello 끝점의 hello 주파수를 자동으로 증가 합니다. 그러나 hello 가장 낮은 '간격으로 ping' 삭제 toois 1 ping 60 초 마다 것이 좋습니다 프록시/방화벽 2-3 분 이상 유휴 연결 toopersist를 허용 합니다. *오래된 버전의 경우 4분 이상이 좋습니다.

## <a name="active-directory-permissions"></a>Active Directory 사용 권한

hello hello Azure AD Connect 유틸리티에 지정 된 계정이 있어야 암호 재설정 "," 암호 변경 "," lockoutTime에 대 한 쓰기 권한을 "및" pwdLastSet의 hello 루트 개체 중 하나에 대 한 권한 확장에 대 한 쓰기 권한을 **각 도메인** 해당 포리스트의 **또는** 원하는 범위 SSPR에 toobe hello 사용자 Ou에 있습니다.

확실 하지 않은 경우 위의 어떤 계정 hello hello Azure Active Directory Connect 구성 UI 열고 hello 현재 구성 옵션 보기를 클릭 합니다. 참조 합니다. tooadd 권한 toois "디렉터리 동기화" 아래에 나열 해야 하는 hello 계정

사용자 계정 대신 하 여 hello MA 서비스 계정이 각 포리스트에 toomanage 암호에 대 한 해당 포리스트 내 허용 이러한 사용 권한을 설정 합니다. **것을 잊은 경우 tooassign 이러한 사용 권한을 다음, 쓰기 저장 toobe 올바르게 구성 되어 나타나는 경우에, 사용자가 toomanage hello 클라우드에서 온-프레미스 암호를 시도할 때 오류가 발생 합니다.**

> [!NOTE]
> 디렉터리의 이러한 사용 권한 tooreplicate tooall 개체에 대 한 tooan 시간 이상 걸릴 수 있습니다.
>

암호 쓰기 저장 toooccur에 대 한 적절 한 권한을 hello tooset

1. Hello 적절 한 도메인 관리 권한이 있는 계정으로 Active Directory 사용자 및 컴퓨터를 열려면
2. Hello 보기 메뉴에서 고급 기능 설정 되어 있는지 확인
3. Hello 왼쪽된 패널에서 hello 도메인의 hello 루트를 나타내는 hello 개체를 마우스 오른쪽 단추로 클릭 하 고 속성 선택
    * Hello 보안 탭을 클릭 합니다.
    * [고급]을 클릭합니다.
4. Hello 사용 권한 탭에서 추가 클릭 합니다.
5. 사용 권한이 너무 (Azure AD Connect 설치 프로그램에서) 적용 되는 hello 계정 선택
6. Hello 적용 toodrop 상자에서 하위 사용자 개체를 선택 합니다.
7. 사용 권한 아래에서 확인란 hello hello 다음에 대 한
    * 암호 만료 안 됨
    * 암호 재설정
    * 암호 변경
    * lockoutTime 쓰기
    * pwdLastSet 쓰기
8. Tooapply를 통해 적용/확인을 클릭 하 고 열려 있는 대화 상자를 종료 합니다.

## <a name="how-does-password-reset-work-for-b2b-users"></a>B2B 사용자에 대한 암호 재설정은 어떻게 작동하나요?
암호 재설정 및 변경은 모든 B2B 구성에서 완전히 지원됩니다.  Hello 세 명시적 B2B 경우 암호 재설정에서 지 원하는 아래를 읽습니다.

1. **기존 Azure AD 테 넌 트와 파트너 조직에서 사용자가** -와 협력 하는 hello 조직에 기존 Azure AD 테 넌 트에서는 **암호 재설정 정책을 해당 테 넌 트에 설정 된 존중**합니다. 단계를 hello 암호 재설정 toowork, 파트너 조직 정당한 요구 toomake Azure AD SSPR를 사용할 수 있는지는 O365 고객에 대 한 추가 비용 없이 hello 및 수행 하 여 사용 하도록 설정할 수 있습니다에 대 한 우리의 [암호 관리 시작 ](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords) 가이드입니다.
2. **사용 하 여 등록 한 사용자 [셀프 서비스 등록](active-directory-self-service-signup.md)**  -와 협력 하는 hello 조직 hello를 사용 하는 경우 [셀프 서비스 등록](active-directory-self-service-signup.md) 테 넌 트에 기능 tooget, 우리 수 있도록 기본 설정으로 복원을 hello 등록 됩니까 전자 메일입니다.
3. **B2B 사용자** -새 hello를 사용 하 여 만든 모든 새 B2B 사용자 [Azure AD B2B 기능](active-directory-b2b-what-is-azure-ad-b2b.md) 됩니다 수 tooreset hello 초대 프로세스 중에 등록 됩니까 hello 전자 메일을 가진 암호입니다.

tootest 이동이, toohttp://passwordreset.microsoftonline.com 이러한 파트너 사용자 중 하나를 사용 합니다. 대체 전자 메일 또는 인증 전자 메일이 정의되어 있으면 암호 재설정이 예상대로 작동됩니다.

## <a name="next-steps"></a>다음 단계

링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.

* [**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작 
* [**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성
* [**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법
* [**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자
* [**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정
* [**비밀번호 쓰기 저장**](active-directory-passwords-writeback.md) - 비밀번호 쓰기 저장이 온-프레미스 디렉터리와 함께 작동 하는 원리
* [**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.
* [**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색
* [**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로? 그 이유는 무엇을? 어디서? 누가? 언제? -Tooask 항상 필요한 tooquestions 답변
* [**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다

