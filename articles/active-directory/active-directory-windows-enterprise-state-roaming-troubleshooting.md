---
title: "Azure Active Directory에서 엔터프라이즈 상태 로밍 설정 문제 해결 | Microsoft Docs"
description: "설정 및 앱 데이터 동기화에 대 한 답변 toosome 질문 IT 관리자가 있을 수를 제공 합니다."
services: active-directory
keywords: "엔터프라이즈 상태 로밍 설정, windows 클라우드, 엔터프라이즈 상태 로밍에 대한 질문과 대답"
documentationcenter: 
author: tanning
manager: swadhwa
editor: 
ms.assetid: f45d0515-99f7-42ad-94d8-307bc0d07be5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4636d016983426e30d696459f54167b8ad2babcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
#<a name="troubleshooting-enterprise-state-roaming-settings-in-azure-active-directory"></a>Azure Active Directory에서 엔터프라이즈 상태 로밍 설정 문제 해결

이 항목에서는 방법을 설명 tootroubleshoot 및 엔터프라이즈 상태 로밍와 문제를 진단 하 고 알려진된 문제 목록을 제공 합니다.

## <a name="preliminary-steps-for-troubleshooting"></a>문제 해결을 위한 준비 단계 
문제 해결을 시작 하기 전에 hello 사용자 및 장치 올바로 구성 되었는지, 및 hello 장치와 hello 사용자가 엔터프라이즈 상태 로밍 모든 hello 요구 사항이 충족 되었는지 확인 합니다. 

1. Hello 최신 업데이트와 Windows 10 및 최소 버전 1511 (OS 빌드 10586 이상) hello 장치에 설치 됩니다. 
2. hello 장치는 Azure AD에 가입 된 경우 또는 도메인에 연결 및 Azure AD에 등록 합니다.
3. Hello Azure Active Directory 포털에서 **엔터프라이즈 상태 로밍** hello 디렉터리 아래에 대해 활성화 되어 **구성** > **장치**  >  **사용자 설정 및 엔터프라이즈 앱 데이터 동기화가**합니다. 모든 사용자가 선택 되어 있거나 hello 사용자 hello 선택 옵션을 통해 동기화 하는 옵션과 사용 되 고 hello 보안 그룹에 포함 합니다.
4. hello 사용자에 게는 Azure Active Directory Premium 구독 toothem 할당 합니다.  
5. hello 장치 다시 시작 하 고 엔터프라이즈 상태 로밍 활성화 된 후 hello 사용자가 로그인 합니다.

## <a name="information-tooinclude-when-you-need-help"></a>정보 tooinclude 도움이 필요한 경우
아래 hello 지침으로 문제를 해결할 수 없는 경우에 지원 엔지니어가 문의할 수 있습니다. 문의할 때 다음 정보는 tooinclude hello를 좋습니다.

- **Hello 오류에 대 한 일반적인 설명** – hello 사용자에 게 표시 되는 오류 메시지가 있습니까? 오류 메시지가 없는 경우 설명 hello 자세히 자신이 예기치 않은 동작이 있습니다. 동기화에 대 한 어떤 기능을 사용할 수 및 toosync 예상 hello 사용자 인가요? 동기화 하는 여러 기능 하지 중 아니면 it 격리 tooone 있습니까?
- **영향을 받는 사용자** – 동기화가 한 사용자 또는 여러 사용자에 대 해 성공/실패합니까? 사용자당 몇 개의 장치가 관련됩니까? 모두 동기화되지 않거나 일부만 동기화되고 일부는 동기화되지 않습니까?
- **Hello 사용자에 대 한 내용은** – 어떤 id는 toolog toohello 장치에서 사용 하 여 hello 사용자? Hello 사용자는 toohello 장치 로그인? Toosync 허용 선택한 보안 그룹의 일부 인가요? 
- **Hello 장치에 대 한 내용은** –이 장치가 Azure AD 조인 또는 도메인에 가입 된? 어떤 빌드에 hello 장치는 있습니까? 가장 최근 업데이트 hello 무엇입니까?
- **날짜 / 시간 / 표준 시간대** – hello 정확한 날짜 및 시간 언급 했 듯이 hello 오류 였습니까 (hello 표준 시간대 포함)?
- 이 정보를 포함하면 최대한 빨리 문제를 해결하는데 도움이 됩니다.

## <a name="troubleshooting-and-diagnosing-issues"></a>문제 해결 및 문제 진단
이 섹션에서는 방법에 제안을 제공 tootroubleshoot 상태 로밍 하는 문제 관련된 tooEnterprise를 진단 하 고 있습니다.

## <a name="verify-sync-and-hello-sync-your-settings-settings-page"></a>동기화를 확인 하 고 hello "설정을 동기화 하 고" 설정 페이지 

1. Windows 10 PC tooa에 연결한 후 도메인에 tooallow 엔터프라이즈 상태 로밍, 회사 계정으로 로그온을 구성 합니다. 너무 이동**설정** > **계정** > **동기화 Your 설정** 하 고, 동기화 및 hello 개별 설정이 되어 있는지 확인 하 고 해당 hello 맨 회사 계정으로 동기화 하는 중 hello 설정 페이지를 나타냅니다. 동일한 계정에서 자신의 로그인 계정으로도 사용 됩니다 하는 hello 확인 **설정** > **계정** > **Your 정보**합니다. 
2. 동기화 hello 작업 표시줄 toohello 오른쪽 또는 맨 위 hello 화면의 측면을 이동 하는 등 hello 원래 컴퓨터에서 약간 변경 하 여 여러 컴퓨터에서 작동 하는지 확인 합니다. Hello 변경 toohello 두 번째 컴퓨터에서 5 분 전파를 감시 합니다. 
 - 잠금 및 잠금 해제 hello 화면 (Win + L) 동기화를 트리거할 수 있습니다.
 - 사용 해야 동률된 toohello 사용자 계정과 컴퓨터 계정이 아니라 hello은 엔터프라이즈 상태 로밍 동기화 toowork –에 대 한 두 Pc에서 동일한 로그온 계정을 hello 합니다.

**잠재적인 문제**: hello 설정 페이지에 hello 설정/해제 회색으로 나타나고 계정의 보는 대신 hello 텍스트 "일부 Windows 기능의 사용할 수 있는 Microsoft 계정 또는 회사 계정을 사용 하는 경우". 이 문제는 hello 장치 tooAzure AD를 성공적으로 인증 되지 않은 toobe 설정 된 도메인에 가입 된 장치와 tooAzure 광고를 등록 하지만 발생할 수 있습니다. 가능한 원인은 hello 장치 정책을 적용 해야, 하지만이 응용 프로그램 비동기적으로 발생 하 고 몇 시간으로 지연 될 수 있습니다. 이 문제를 다음 단계에서 수행 hello 확인 tooverify hello 좋다고 장치 등록 상태 toocheck을 hello 합니다.

### <a name="verify-hello-device-registration-status"></a>Hello 장치 등록 상태 확인
엔터프라이즈 상태 로밍 Azure AD에 등록 된 hello 장치 toobe가 필요 합니다. Windows 10 클라이언트를 등록 하는 hello를 확인 하 고 URL 설정 하는 Azure AD, 지문을 NGC 상태를 확인 하 여 특정 하지 않은 tooEnterprise 상태 로밍 아래 hello 지침 데 유용할 수 있지만 및 기타 정보입니다.

1.  열기 hello 명령 프롬프트를 승격 해제 됨된입니다. windows에서이 열 toodo 실행 시작 관리자 (Win + R) hello 및 tooopen "cmd"를 입력 합니다.
2.  Hello 명령 프롬프트를 연 후 입력 "*dsregcmd.exe /status*"입니다.
3.  예상된 출력에 대 한 hello **AzureAdJoined** 필드 값은 "YES" 여야 합니다 **WamDefaultSet** 필드 값 "YES" 하 고 해야 hello **WamDefaultGUID** 필드 값 이어야 합니다는 Hello 끝에 "(azure Ad)"으로 GUID입니다.

**잠재적인 문제**: **WamDefaultSet** 및 **AzureAdJoined** 모두 hello 필드 값에 "아니요"를 포함, hello 장치를 도메인에 가입 하 고 Azure AD에 등록 및 hello 장치 동기화 하지는 않습니다. 이 표시 되 면 hello 장치 toowait 정책 toobe 적용에 필요한 수도 tooAzure AD 연결에 실패 했습니다 hello 장치에 대 한 인증 hello 있습니다. hello 사용자 hello 정책 toobe 적용에 대 한 몇 시간 toowait이 있을 수 있습니다. 다른 문제 해결 단계는 작업 스케줄러에서에 다시 및 서명 또는 시작 hello 태스크에 의해 자동 등록을 다시 시도 포함 될 수 있습니다. 경우에 따라 관리자 권한 명령 프롬프트 창에서 "*dsregcmd.exe /leave*"를 실행하고 다시 부팅하여 등록을 다시 시도하면 이 문제 해결에 도움이 될 수 있습니다.


**잠재적인 문제**: hello 필드에 대 한 **AzureAdSettingsUrl** 빈 데이터 요소 및 hello 장치가 하지 않습니다 동기화.는 hello 사용자 수 있는 마지막 로그인 toohello 장치 hello 활성 Azure에서에서 엔터프라이즈 상태 로밍 사용 하기 전에 디렉터리 포털입니다. Hello 장치를 다시 시작 하 고 hello 사용자 로그인을가지고 있습니다. 필요에 따라 hello 포털의 IT 관리자는 사용 하지 않도록 설정 하 고 사용자 수 동기화 설정 및 엔터프라이즈 앱 데이터를 다시 설정 하는 hello 필요를 보십시오. 다시 활성화 hello 장치 다시 시작 하 고 hello 사용자 로그인을가지고 있습니다. Hello 문제가 해결 되지 않을 경우 **AzureAdSettingsUrl** 손상 된 장치 인증서의 hello 경우에서 비어 있을 수 있습니다. 이 경우 관리자 권한 명령 프롬프트 창에서 "*dsregcmd.exe /leave*"를 실행하고 다시 부팅하여 등록을 다시 시도하면 이 문제 해결에 도움이 될 수 있습니다.

## <a name="enterprise-state-roaming-and-multi-factor-authentication"></a>엔터프라이즈 상태 로밍 및 Multi-Factor Authentication 
특정 조건에서 엔터프라이즈 상태 로밍 실패할 수 있습니다 toosync 데이터 Azure Multi-factor Authentication 구성 된 경우. 대 한 자세한 내용은 이러한 증상을 hello 지원 문서를 참조 하십시오. [KB3193683](https://support.microsoft.com/kb/3193683)합니다. 

**잠재적인 문제**: 암호를 사용 하 여 tooa Windows 10 장치에 로그인 하는 동안 toosync 설정을 hello Azure Active Directory 포털에서 구성 된 toorequire Multi-factor Authentication 사용자 장치가 사용 하는 경우 실패할 수 있습니다. 이 Multi-factor Authentication 구성 유형은 의도 한 tooprotect Azure 관리자 계정입니다. 관리자가 사용자가 수 toosync tootheir Windows 10 장치를 해당 Microsoft Passport for Work PIN에 로그인 하거나 Office 365와 같은 다른 Azure 서비스에 액세스 하는 동안 Multi-factor Authentication을 완료 하 여 수 있습니다.

**잠재적인 문제**: 동기화 admin 님 안녕하세요 hello Active Directory Federation Services Multi-factor Authentication 조건부 액세스 정책을 구성 하 고 hello 장치에서 hello 액세스 토큰이 만료 되는 경우 실패할 수 있습니다. 에 로그인 하 고 로그 아웃 hello Microsoft Passport for Work PIN에 사용 하 여 또는 Office 365와 같은 다른 Azure 서비스에 액세스 하는 동안 Multi-factor Authentication을 완료 합니다.

###<a name="event-viewer"></a>이벤트 뷰어
고급 문제 해결에 대 한 이벤트 뷰어 사용된 toofind 특정 오류 될 수 있습니다. 이러한 hello 테이블 아래에 설명 되어 있습니다. 이벤트 뷰어 hello 이벤트를 확인할 수 있습니다 > 응용 프로그램 및 서비스 로그 > **Microsoft** > **Windows** > **SettingSync** 및 동기화와 함께 id 관련 문제에 대 한 **Microsoft** > **Windows** > **Azure AD**합니다.


## <a name="known-issues"></a>알려진 문제

### <a name="sync-does-not-work-on-devices-that-have-apps-side-loaded-using-mdm-software"></a>MDM 소프트웨어를 사용하여 앱이 로드된 장치에서는 동기화가 작동하지 않음

Windows 10 Anniversary 업데이트 (버전 1607) hello 하는 실행 하는 장치에 영향을 줍니다. Hello SettingSync Azure 로그에서 이벤트 뷰어에서 이벤트 ID 6013 hello 80070259 오류로 자주 발생 합니다.

**권장 작업**  
Windows 10 hello v1607 클라이언트 hello를 2016 년 8 월 23 일에 있는지 확인 누적 업데이트 ([KB3176934](https://support.microsoft.com/kb/3176934) OS 빌드 14393.82). 

---

### <a name="internet-explorer-favorites-do-not-sync"></a>Internet Explorer 즐겨찾기가 동기화되지 않음

Windows 10 11 월 업데이트 (버전 1511) hello 하는 실행 하는 장치에 영향을 줍니다.

**권장 작업**  
Windows 10 hello v1511 클라이언트 hello를 2016 년 7 월에 있는지 확인 누적 업데이트 ([KB3172985](https://support.microsoft.com/kb/3172985) OS 빌드 10586.494).

---

### <a name="theme-is-not-syncing-as-well-as-data-protected-with-windows-information-protection"></a>Windows 정보 보호로 보호된 데이터뿐만 아니라 테마가 동기화되지 않음 

로 보호 되는 데이터, tooprevent 데이터 유출 [Windows 정보 보호](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip) 장치를 사용 하 여 Windows 10 Anniversary 업데이트 hello에 대 한 엔터프라이즈 상태 로밍를 통해 동기화 되지 것입니다.



**권장 작업**  
없음. 향후 업데이트 tooWindows이이 문제를 해결할 수 있습니다.

---

### <a name="date-time-and-region-settings-do-not-sync-on-domain-joined-device"></a>날짜, 시간 및 지역 설정이 도메인 가입 장치에서 동기화되지 않음 
  
도메인에 가입 하는 장치 hello 날짜, 시간 및 지역 설정에 대 한 동기화 발생 하지 것입니다: 자동 시간입니다. 자동으로 사용 하 여 수 있습니다 override 다른 날짜, 시간 및 지역 설정을 hello 및 설정이 toosync 되지 않습니다. 

**권장 작업**  
없음. 

---

### <a name="uac-prompts-when-syncing-passwords"></a>암호 동기화 시 UAC 프롬프트

Hello를 실행 하는 영향을 줌 장치를 무선 NIC와 Windows 10 11 월 업데이트 (버전 1511) toosync 암호를 구성 합니다.

**권장 작업**  
Windows 10 hello v1511 클라이언트 hello 누적 업데이트에 있는지 확인 ([KB3140743](https://support.microsoft.com/kb/3140743) OS 빌드 10586.494).

---

### <a name="sync-does-not-work-on-devices-that-use-smart-card-for-login"></a>동기화는 로그인 시 스마트 카드를 사용하는 장치에서 작동하지 않음
스마트 카드 또는 가상 스마트 카드를 사용 하 여 tooyour Windows 장치에서 toosign 시도 하면 설정 동기화 작동이 중지 됩니다.     

**권장 작업**  
없음. 향후 업데이트 tooWindows이이 문제를 해결할 수 있습니다.

---

### <a name="domain-joined-device-is-not-syncing-after-leaving-corporate-network"></a>도메인에 가입된 장치가 회사 네트워크에서 벗어난 후 동기화되지 않음     
도메인에 가입 된 장치 등록 tooAzure 오랜 시간에 대 한 hello 장치는 오프 사이트 및 도메인 인증 완료할 수 없는 경우 AD 동기화 오류가 발생할 수 있습니다.

**권장 작업**  
동기화를 다시 시작할 수 있도록 hello 장치 tooa 회사 네트워크를 연결 합니다.

---

 ### <a name="azure-ad-joined-device-is-not-syncing-and-hello-user-has-a-mixed-case-user-principal-name"></a>Azure AD 조인 장치는 동기화 되지 하 고 hello 사용자에 게 혼합된 사례 사용자 계정 이름입니다.
 Hello 사용자에 게는 혼합 된 경우 UPN (예: 사용자 이름 대신 사용자 이름) 및 Windows 10 빌드 10586 too14393에서 업그레이드에 Azure AD 조인 장치의 hello 사용자가을 toosync hello 사용자의 장치에 실패할 수 있습니다. 

**권장 작업**  
hello 사용자 toounjoin 필요 하 고 hello 장치 toohello 클라우드를 다시 조인 합니다. toodo hello 로컬 관리자 사용자로이 로그인이, 너무 이동 하 여 hello 장치를 가입 해제 하 고**설정** > **시스템** > **에 대 한** 선택 " 관리 또는 연결 끊기 회사 또는 학교 "입니다. 아래의 hello 파일로 내보내고 Azure AD Join hello 다시에서 장치를 정리 **설정** > **시스템** > **에 대 한** "연결을 선택 하 고 tooWork 또는 학교 "입니다. Toojoin hello 장치 tooAzure Active Directory 및 전체 hello 흐름을 계속 합니다.

Hello 정리 단계에서는 다음 파일이 정리 hello:
- Settings.dat in `C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\Settings\`
- Hello 폴더에서 모든 hello 파일`C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\AC\TokenBroker\Account`

---

### <a name="event-id-6065-80070533-this-user-cant-sign-in-because-this-account-is-currently-disabled"></a>이벤트 ID 6065: 80070533 이 사용자는 현재 이 계정을 사용할 수 없기 때문에 로그인 할 수 없음  
Hello SettingSync/디버그 로그에서 이벤트 뷰어에서 hello 사용자의 자격 증명이 만료 되는 경우이 오류를 볼 수 있습니다. 또한 테 넌 트 hello 자동으로 프로 비전 AzureRMS 없는 경우 발생할 수 있습니다. 

**권장 작업**  
Hello 첫 번째 경우에서에 자격 증명 및 로그인 toohello 장치 hello 새 자격 증명으로 업데이트 하는 hello 사용자. toosolve hello AzureRMS 문제에 나열 된 hello 단계를 진행할 [KB3193791](https://support.microsoft.com/kb/3193791)합니다. 

---

### <a name="event-id-1098-error-0xcaa5001c-token-broker-operation-failed"></a>이벤트 ID 1098: 오류: 0xCAA5001C 토큰 브로커 작업 실패  
Hello AAD/Operational 로그에서 이벤트 뷰어에서이 오류가 나타날 수 이벤트 1104를: AAD 클라우드 AP 플러그 인 호출 토큰 가져오기 오류를 반환 했습니다: 0xC000005F 합니다. 이 문제는 권한 또는 소유권 특성이 없는 경우 발생합니다.    

**권장 작업**  
나열 된 hello 단계를 진행할 [KB3196528](https://support.microsoft.com/kb/3196528)합니다.  



## <a name="next-steps"></a>다음 단계

- 사용 하 여 hello [사용자 음성 포럼](https://feedback.azure.com/forums/169401-azure-active-directory/category/158658-enterprise-state-roaming) 어떻게 tooimprove 엔터프라이즈 상태 로밍 tooprovide 피드백과 확인 제안 합니다.

- 자세한 내용은 참조 hello [엔터프라이즈 상태 로밍 개요](active-directory-windows-enterprise-state-roaming-overview.md)합니다. 

## <a name="related-topics"></a>관련된 항목
* [엔터프라이즈 상태 로밍 개요](active-directory-windows-enterprise-state-roaming-overview.md)
* [Azure Active Directory에서 엔터프라이즈 상태 로밍 활성화](active-directory-windows-enterprise-state-roaming-enable.md)
* [설정 및 데이터 로밍 FAQ](active-directory-windows-enterprise-state-roaming-faqs.md)
* [설정 동기화에 대한 그룹 정책 및 MDM 설정](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Windows 10 로밍 설정 참조](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
