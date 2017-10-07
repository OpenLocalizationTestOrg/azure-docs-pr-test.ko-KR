---
title: "문제 해결: Azure AD SSPR | Microsoft Docs"
description: "Azure AD 셀프 서비스 암호 재설정 문제 해결"
services: active-directory
keywords: 
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
ms.date: 08/08/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 361ef5f37e4e9de83d3f9d5a8e5177d186fe86d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-self-service-password-reset"></a>Tootroubleshoot 셀프 서비스 암호 다시 설정 하는 방법

셀프 서비스 암호 재설정 문제가 있는 경우 신속 하 게 tooget 것 아래에 있는 hello 항목에 도움이 될 수 있습니다.

## <a name="troubleshoot-self-service-password-reset-errors-that-a-user-may-see"></a>사용자가 볼 수 있는 셀프 서비스 암호 재설정 오류 문제 해결

| 오류 | 세부 정보 | 기술 세부 정보 |
| --- | --- | --- |
| TenantSSPRFlagDisabled = 9 | 죄송합니다. <br> 관리자가 조직에 대해 암호 재설정을 비활성화했기 때문에 지금은 암호를 재설정할 수 없습니다. 이 경우 tooresolve 수행할 수 있는 추가 작업이 없으므로 있습니다. 관리자에 게 문의 하십시오 tooenable 달라고이 기능입니다. toolearn 더 읽기 [Azure AD 암호를 잊어 버린 도움말](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-update-your-own-password#common-problems-and-their-solutions)합니다. | SSPR_0009: 관리자에 의해 암호 재설정이 활성화되지 않은 것을 감지했습니다. 관리자에 게 문의 하 고 조직에 대 한 암호 재설정 tooenable 요청 하십시오. |
| WritebackNotEnabled = 10 |죄송합니다. <br> 관리자가 조직에 필요한 서비스를 활성화하지 않았기 때문에 지금은 암호를 재설정할 수 없습니다. 이 경우 tooresolve 수행할 수 있는 추가 작업이 없으므로 있습니다. 관리자에 게 문의 하십시오 toocheck 달라고 조직의 구성 합니다. 이 필요한 서비스에 대해 자세히 toolearn 읽을 [암호 쓰기 저장을 구성할](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-writeback#configuring-password-writeback)합니다. | SSPR_0010: 비밀번호 쓰기 저장이 활성화되지 않은 것을 감지했습니다. 관리자에 게 문의 하 고 tooenable 암호 쓰기 저장 하도록 요청 하십시오. |
| SsprNotEnabledInUserPolicy = 11 | 죄송합니다.  <br> 관리자가 조직에 대해 암호 재설정을 구성하지 않았기 때문에 지금은 암호를 재설정할 수 없습니다. 이 경우 tooresolve 수행할 수 있는 추가 작업이 없으므로 있습니다. 관리자에 게 문의 하 고 tooconfigure 암호 재설정 하도록 요청 하십시오. 암호에 대 한 toolearn 재설정 구성 읽기 hello 문서 [빠른 시작: Azure AD 셀프 서비스 암호 재설정](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-getting-started)합니다. | SSPR_0011: 조직에서 암호 재설정 정책을 정의하지 않았습니다. 관리자에 게 문의해 하 고 암호 재설정 정책을 toodefine 하도록 요청 하십시오. |
| UserNotLicensed = 12 | 죄송합니다. <br> 조직에서 필요한 라이선스가 누락되었기 때문에 지금은 암호를 재설정할 수 없습니다. 이 경우 tooresolve 수행할 수 있는 추가 작업이 없으므로 있습니다. 관리자에 게 문의 하 고 toocheck 라이선스 할당을 요청 하십시오. 라이선스에 대 한 더 toolearn hello 문서를 읽어 보세요. [라이선스 요구 사항에 대 한 Azure AD 셀프 서비스 암호 재설정](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-licensing)합니다. | SSPR_0012: 조직 내에 필요한 hello 라이선스 필요한 tooperform 암호 재설정을 있습니다. 관리자에 게 문의 하 고 tooreview 라이선스 할당을 요청 하십시오. |
| UserNotMemberOfScopedAccessGroup = 13 | 죄송합니다. <br> 관리자가 사용자 계정 toouse 암호 재설정을 구성 하기 때문에 지금은 암호를 재설정할 수 없습니다. 이 경우 tooresolve 수행할 수 있는 추가 작업이 없으므로 있습니다. 관리자에 게 문의 하십시오 tooconfigure 달라고 암호 재설정을 위한 계정입니다. hello 문서를 참조 하는 암호 재설정에 대 한 계정 구성에 대 한 자세한 toolearn [사용자 암호 재설정 롤아웃하기](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-best-practices)합니다. | SSPR_0012: 암호를 재설정할 수 있는 그룹의 구성원이 아닙니다. 관리 및 요청 toobe 추가 toohello 부서를 문의 하십시오. |
| UserNotProperlyConfigured = 14 | 죄송합니다. <br> 계정에서 필요한 정보가 누락되었기 때문에 지금은 암호를 재설정할 수 없습니다. 이 경우 tooresolve 수행할 수 있는 추가 작업이 없으므로 있습니다. 관리자에 게 문의 하 고 tooreset 하도록 요청 하세요의 암호입니다. Tooyour 계정 액세스를 다시 구성한 후 hello에 따라 레지스터 hello 필요한 정보 hello 문서의 단계는 방법을 배울 수 있습니다 [셀프 서비스 암호 재설정을 위해 등록할](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-reset-register)합니다. | SSPR_0014: 추가 보안 정보는 필요한 tooreset 암호입니다. tooproceed, 관리자에 게 문의해 것을 요청 tooreset 암호입니다. 액세스 tooyour 계정을 만들었으면 https://aka.ms/ssprsetup에서 추가 보안 정보를 등록할 수 있습니다. 관리자의 hello 단계에 따라 추가 보안 정보 tooyour 계정을 추가할 수 [집합과 암호 재설정에 대 한 읽기 인증 데이터](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-data#set-and-read-authentication-data-using-powershell)합니다. |
| OnPremisesAdminActionRequired = 29 | 죄송합니다. <br> 조직의 암호 재설정 구성 문제 때문에 지금은 암호를 다시 설정할 수 없습니다. 이 경우 tooresolve 수행할 수 있는 추가 작업이 없으므로 있습니다. 관리자에 게 문의 하 고 tooinvestigate 하도록 요청 하십시오. hello 잠재적인 문제에 대해 자세히 toolearn hello 문서를 읽어 보세요. [암호 쓰기 저장 문제 해결](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-troubleshoot#troubleshoot-password-writeback)합니다. | SSPR_0029: 우리는 없습니다 tooreset 암호가 온-프레미스 구성에서 tooan 오류 때문입니다. 관리자에 게 문의 하 고 tooinvestigate 하도록 요청 하십시오. |
| OnPremisesConnectivityError = 30 | 죄송합니다. <br> 연결 문제 tooyour 조직으로 인해이 이번에 암호 다시 설정 수 없습니다. 지금은 없습니다 동작 tootake는 없지만 나중에 다시 시도 hello 문제 해결할 수 있습니다. Hello 문제가 계속 되 면 관리자에 게 문의해 tooinvestigate 하도록 요청 하십시오. 읽기 연결 문제에 대 한 자세한 toolearn [암호 쓰기 저장 문제 해결 연결](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-troubleshoot#troubleshoot-password-writeback-connectivity)합니다. | SSPR_0030: 온-프레미스 환경과 연결 상태가 안 tooa 인해 암호를 재설정할 수 없습니다. 관리자에 게 문의 하 고 tooinvestigate 하도록 요청 하십시오.|


## <a name="troubleshoot-password-reset-configuration-in-hello-azure-portal"></a>Hello Azure 포털에서에서 암호 재설정 구성 문제 해결

| **오류** | 해결 방법 |
| --- | --- |
| Hello 표시 되지 않는 **암호 재설정** hello Azure 포털에서에서 Azure AD 섹션 | Azure AD Premium 또는 Basic 라이선스가 할당 toohello 관리자 수행 hello 되는 작업 하지 않은 경우 발생할 수 있습니다. <br> 라이선스 toohello 관리자 계정에 hello 문서를 사용 하 여 할당 하 여이 해결할 수 있습니다 [할당, 확인 및 라이선스 문제 해결](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses) |
| 특정 구성 옵션이 보이지 않습니다. | Hello UI의 많은 요소는 필요할 때까지 숨겨집니다. Toosee 원하는 모든 hello 옵션을 사용 하도록 설정 하세요. |
| Hello 표시 되지 않는 **온-프레미스 통합** 탭 | Azure AD 연결을 다운로드하고 비밀번호 쓰기 저장을 구성하는 경우 이 옵션이 표시됩니다. 이 항목에 대 한 자세한 내용은 hello 문서 참조 [기본 설정을 사용 하는 Azure AD Connect 시작](./connect/active-directory-aadconnect-get-started-express.md)합니다. |

## <a name="troubleshoot-password-reset-reporting"></a>암호 재설정 보고 문제 해결

| **오류** | 해결 방법 |
| --- | --- |
| Hello에 표시 되는 모든 암호 관리 활동 유형 표시 되지 않는 **셀프 서비스 암호 관리** audit 이벤트 범주 | Azure AD Premium 또는 Basic 라이선스가 할당 toohello 관리자 수행 hello 되는 작업 하지 않은 경우 발생할 수 있습니다. <br> 라이선스 toohello 관리자 계정에 hello 문서를 사용 하 여 할당 하 여이 해결할 수 있습니다 [할당, 확인 및 라이선스 문제를 해결] |
| 사용자 등록이 여러 번 표시됩니다 | 현재 사용자가 등록할 때 별도 이벤트로 등록된 데이터의 각 개별 부분을 기록합니다. <br> Tooaggregate이이 데이터를 원하는 경우 hello 보고서를 다운로드할 수 있습니다 및 피벗 테이블에서와 열기 hello 데이터 excel toohave 보다 유연 합니다.

## <a name="troubleshoot-password-reset-registration-portal"></a>암호 재설정 등록 포털 문제 해결

| **오류** | 해결 방법 |
| --- | --- |
| 암호 재설정에 디렉터리를 사용할 수 없습니다 **관리자가 되지 설정한 toouse 하면이 기능** | 스위치 hello **셀프 서비스 암호 재설정 활성화** 너무 플래그**그룹** 또는 **모든 사람이** 클릭 **저장** |
| Azure AD Premium 또는 Basic 라이선스가 할당 된 사용자가 **관리자가 되지 설정한 toouse 하면이 기능** | Azure AD Premium 또는 Basic 라이선스가 할당 toohello 관리자 수행 hello 되는 작업 하지 않은 경우 발생할 수 있습니다. <br> 라이선스 toohello 관리자 계정에 hello 문서를 사용 하 여 할당 하 여이 해결할 수 있습니다 [할당, 확인 및 라이선스 문제 해결](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses) |
| 오류 처리 요청 | 많은 문제로 인해 발생할 수 있지만 일반적으로 서비스 중단 또는 구성 문제로 인해 이 오류가 발생합니다. 이 오류가 나타나고 비즈니스에 영향을 주는 경우 추가적인 도움이 필요하면 Microsoft 지원에 문의하세요. |

## <a name="troubleshoot-password-reset-portal"></a>암호 재설정 포털 문제 해결

| **오류** | 해결 방법 |
| --- | --- |
| 암호 재설정을 위해 디렉터리를 사용할 수 없습니다. | 스위치 hello **셀프 서비스 암호 재설정 활성화** 너무 플래그**그룹** 또는 **모든 사람이** 클릭 **저장** |
| Azure AD Premium 또는 Basic 라이선스가 할당되지 않은 사용자입니까? | Azure AD Premium 또는 Basic 라이선스가 할당 toohello 관리자 수행 hello 되는 작업 하지 않은 경우 발생할 수 있습니다. <br> 라이선스 toohello 관리자 계정에 hello 문서를 사용 하 여 할당 하 여이 해결할 수 있습니다 [할당, 확인 및 라이선스 문제 해결](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses) |
| 암호 재설정에 디렉터리를 사용할 수 있지만 사용자가 인증 정보를 누락했거나 형식이 잘못 되었습니다. | 해당 올바른 형식의 사용자 연락처 데이터가 계속 진행 하기 전에 hello 디렉터리에 파일을 확인 합니다. 이 항목에 대 한 자세한 내용은 hello 문서 참조 [Azure AD 셀프 서비스 암호 재설정 사용 되는 데이터](active-directory-passwords-data.md)합니다. |
| 암호 재설정에 디렉터리를 사용할 수 있지만 사용자에 대 한 연락처 데이터의 한 부분 파일 정책이 toorequire 두 개의 검증 단계가 설정 된 경우 | 계속하기 전에 해당 사용자에게 둘 이상의 제대로 구성된 연락 방법(예: 휴대폰 **및** 사무실 전화)이 있는지를 확인합니다. |
| 암호 재설정에 디렉터리를 사용할 수 및 사용자가 올바르게 구성 되어 있지만 사용자가 연결할 수 없습니다 toobe | 임시 서비스 오류 또는 잘못 된 연락처 데이터를 올바르게 검색 하지 못했습니다 hello 때문일 수 있습니다. <br> <br> Hello 사용자 10 초, 다시 시도 대기 하 고 "관리자에 게 문의" 링크가 나타납니다. 다시 시도 클릭 하면 암호 재설정 해당 사용자 계정에 대해 수행 하는 toobe 요청 양식 전자 메일 tooadministrators "관리자에 게 문의"을 클릭 하면 전송 하는 반면 hello 호출을 다시 시도 합니다. |
| 사용자가 받지 hello 암호 다시 설정 SMS 또는 전화 통화 | Hello 디렉터리에 형식이 잘못 됨 전화 번호의 hello 결과 수 있습니다. Hello 형식 hello 전화 번호 인지 확인 하십시오 "+ ccc xxxyyyzzzzXeeee"입니다. <br> <br> (이러한는 하이픈이 제거 되어 hello 호출 디스패치 되기 전에) hello 디렉터리에 하나를 지정 하는 경우에 암호 재설정 확장을 지원 하지 않습니다. 확장을 사용 하지 않고 숫자를 사용 하 여 시도 또는 hello 확장 hello 여 PBX의 전화번호에 통합 합니다. |
| 사용자는 암호 재설정 전자 메일을 수신하지 못합니다. | 이 문제에 대 한 hello 가장 일반적인 원인은 스팸 필터에서 해당 hello 메시지는 거부입니다. 스팸, 정크 또는 지운 편지함 폴더 hello 전자 메일을 확인 합니다. <br> 또한 hello hello 메시지에 대 한 올바른 전자 메일을 확인 해야 합니다. |
| 필자는 암호 재설정 정책을 설정했지만 관리자 계정이 암호 재설정을 사용하는 경우 해당 정책이 적용되지 않습니다. | Microsoft에서 관리 하 고 컨트롤 hello 관리자 암호 재설정 정책 tooensure hello 가장 높은 수준의 보안. |
| 사용자는 하루에 너무 많이 암호를 재설정하려 할 수 없습니다. | 짧은 기간에 너무 여러 번 tooreset 현상이 메커니즘 tooblock 사용자가 자신의 암호를 제한 하는 자동을 구현 합니다. 다음과 같은 때 이것이 일어납니다. <br> 1. 사용자는 전화 번호를 toovalidate 1 시간 동안에서 5 번 시도합니다. <br> 2. 사용자가 한 시간에 5 번 toouse hello 보안 질문 게이트를 시도 합니다. <br> 3. 사용자가 tooreset hello에 대 한 암호를 5 번 1 시간에에서 동일한 사용자 계정입니다. <br> toofix이 hello 사용자 toowait hello 마지막 시도 후 24 시간 동안 지시 하 고 사용자가 hello 다음 수 tooreset 암호 수 있습니다. |
| 사용자가 자신의 전화번호의 유효성을 검사하는 경우 오류가 보입니다. | 이 오류는 hello 전화 번호를 입력 한 파일에 hello 전화 번호가 일치 하지 않을 때 발생 합니다. Hello 사용자 암호 재설정에 대 한 전화 기반 방법을 toouse 동안 영역 및 국가 코드를 포함 하 여 hello 전체 전화 번호를 시작 하는 있는지 확인 합니다. |
| 오류 처리 요청 | 많은 문제로 인해 발생할 수 있지만 일반적으로 서비스 중단 또는 구성 문제로 인해 이 오류가 발생합니다. 이 오류가 나타나고 비즈니스에 영향을 주는 경우 추가적인 도움이 필요하면 Microsoft 지원에 문의하세요. |

## <a name="troubleshoot-password-writeback"></a>비밀번호 쓰기 저장 문제 해결

| **오류** | 해결 방법 |
| --- | --- |
| 암호 재설정 서비스 시작 하지 않습니다 오류와 함께 온-프레미스에서 6800 hello Azure AD Connect 컴퓨터의 응용 프로그램 이벤트 로그. <br> <br> 온보딩 후에 페더레이션되거나 암호 해시 동기화된 사용자는 자신의 암호를 재설정할 수 없습니다. | 암호 쓰기 저장을 사용 하는 hello 동기화 엔진 toohello 클라우드 등록 서비스와 통신 하 여 hello 쓰기 저장 라이브러리 tooperform hello 구성 (등록)를 호출 합니다. 온 보 딩 중 또는 Azure AD Connect 컴퓨터의 이벤트 로그에 hello 이벤트 로그에서 오류에 암호 쓰기 저장 결과 대 한 hello WCF 끝점을 시작 하는 동안 발생 한 모든 오류. <br> <br> ADSync 서비스의 다시 시작 하는 동안 쓰기 저장이 구성 된 경우 hello WCF 끝점이 시작 됩니다. 그러나 hello 끝점의 hello 시작에 실패 하면 म을 이벤트 6800 기록 되며 hello 동기화 서비스를 시작 합니다. 이 이벤트의 현재 상태 해당 hello 암호 쓰기 저장 끝점이 시작 되지 않은 것을 의미 합니다. 이 이벤트 로그 항목이 이벤트 (6800)에 대 한 이벤트 로그 세부 PasswordResetService hello 끝점을 시작 하지 못했습니다 이유를 나타내는 구성 요소에서 생성 합니다. 이러한 이벤트 로그 오류를 검토 하 고 암호 쓰기 저장 여전히 작동 하지 않는 경우 toorestart hello Azure AD Connect를 시도 하십시오. Hello 문제가 계속 되 면 toodisable를 시도 하 고 암호 쓰기 저장을 다시 사용 하도록 설정 합니다.
| 사용자 암호 tooreset 시도 하거나 암호 쓰기 저장을 사용 하도록 설정 된 계정을 잠금 해제, hello 작업이 실패 합니다. <br> <br> 또한 hello Azure AD Connect 이벤트 로그를 포함 하는 이벤트를 볼: "동기화 엔진 오류 시간을 반환 했습니다. = 800700CE, 메시지 = filename hello 또는 확장 너무 깁니다." hello 잠금 해제 작업 후에 발생 합니다. | Hello Active Directory 계정을 Azure AD Connect에 대 한 찾아 hello 암호 toocontain 최대 127 자 다시 설정 합니다. 그런 다음 hello 시작 메뉴에서 동기화 서비스를 엽니다. TooConnectors 이동한 hello Active Directory Connector를 찾습니다. 이를 선택하고 [속성]을 클릭합니다. Toohello 탐색 페이지에 자격 증명 및 hello 새 암호를 입력 합니다. 확인 tooclose hello 페이지를 선택 합니다. |
| Hello Azure AD Connect 설치 과정의 마지막 단계 hello에서 암호 쓰기 저장을 구성할 수 없습니다 나타내는 오류 표시 합니다. <br> <br> hello Azure AD 연결 응용 프로그램 이벤트 로그 "가져오는 동안 오류 발생 인증 토큰" 텍스트 함께 오류 32009가 포함 되어 있습니다. | 이 오류는 hello 다음 두 가지 경우에에서 발생 합니다.<br> <br> a. Hello hello Azure AD Connect 설치 프로세스를 시작할 때 지정한 hello 전역 관리자 계정에 대 한 잘못 된 암호를 지정 했습니다.<br> b. Toouse hello hello Azure AD Connect 설치 프로세스 시작 시 hello 전역 관리자 계정에 대 한 페더레이션된 사용자를 지정 하려고 했습니다.<br> <br> toofix이이 오류를 hello hello Azure AD Connect 설치 프로세스를 시작할 때 지정한 전역 관리자에 게에 대 한 페더레이션된 계정을 사용 하지 않는 지정 된 해당 hello 암호가 올바른지 확인 합니다. |
| hello Azure AD Connect 컴퓨터 이벤트 로그 오류 hello PasswordResetService에서 throw 된 32002가 포함 되어 있습니다. <br> <br> hello이 오류 메시지: "tooServiceBus 연결 오류, hello 토큰 공급자가 없습니다 tooprovide 보안 토큰..." | 온-프레미스 환경 hello 클라우드에서 수 tooconnect toohello 서비스 버스 끝점 않습니다. 이 오류는 일반적으로 아웃 바운드 연결 tooa 특정 포트 또는 웹 주소를 차단 방화벽 규칙에 의해 발생 합니다. 자세한 정보는 [네트워크 요구 사항](active-directory-passwords-how-it-works.md#network-requirements)을 참조하세요. 이러한 규칙을 업데이트 한 후 hello Azure AD Connect 컴퓨터를 다시 시작 하 고 암호 쓰기 저장 작업을 다시 시작 해야 합니다. |
| 시간이 지난 후에 페더레이션되거나 암호 해시 동기화된 사용자는 자신의 암호를 재설정할 수 없습니다. | 일부 드문 경우에서 Azure AD Connect가 다시 시작 하는 경우 암호 쓰기 저장 서비스 hello toorestart를 실패할 수 있습니다. 이 경우 먼저 암호 쓰기 저장에 나타나는지 확인 toobe-에서 사용 하도록 설정 이렇게 hello Azure AD Connect 마법사 또는 powershell (위의 방법 섹션 참조). Hello 기능 toobe 사용으로 표시 되 면 활성화 / 비활성화 hello 기능을 다시 hello UI 또는 PowerShell을 통해 해 보십시오. 작동하지 않으면 Azure AD Connect를 완전히 제거하고 다시 설치해보세요. |
| 페더레이션 또는 암호 해시 동기화 사용자가 서비스 문제가 발생 했습니다 hello 암호 나타내는 전송 후 암호에 오류가 표시 tooreset 려 합니다. <br ><br> 또한 toothis, 하는 동안 암호 재설정 작업, 관리 에이전트에 대 한 오류에는 온-프레미스 이벤트 로그의 액세스가 거부 되었다는 표시 될 수 있습니다. | 이벤트 로그에서 이러한 오류를 표시 하는 경우에 해당 hello AD MA (지정 된 계정이 hello 마법사에서 구성의 hello 시)에 hello 암호 쓰기 저장에 필요한 권한을 확인 합니다. <br> <br> **이 권한이 부여 되 면까지 걸릴 수 있으므로 사용 권한 tootrickle hello에 대 한 too1 시간 hello DC의 sdprop 백그라운드 작업을 통해.** <br> <br> 암호 재설정 toowork, hello 권한 toobe 해당 암호를 다시 설정 하는 hello 사용자 개체의 보안 설명자 hello에 자동 삽입 해야 합니다. 이 사용 권한을 hello 사용자 개체에 표시 될 때까지 암호 재설정 액세스 거부 toofail이 계속 됩니다. |
| 페더레이션 또는 암호 해시 동기화 사용자가 서비스 문제가 발생 했습니다 hello 암호 나타내는 전송 후 암호에 오류가 표시 tooreset 려 합니다. <br> <br> 또한 toothis, 하는 동안 암호 재설정 작업, hello "개체를 찾을 수 없습니다." 오류를 나타내는 Azure AD Connect 서비스에서에서 이벤트 로그에 오류가 표시 될 수 있습니다. | 이 오류는 일반적으로 hello 동기화 엔진이 해당 의미는 없습니다 toofind hello AAD 커넥터 공간이의 사용자 개체에 hello 또는 hello 연결 된 MV 또는 AD 커넥터 공간 개체입니다. <br> <br> tootroubleshoot이를 해당 hello 사용자 실제로 Azure AD Connect의 현재 인스턴스 hello 통해 온-프레미스 tooAAD에서 동기화 되었는지 확인 하 고 hello 커넥터 공간 및 MV의 hello 개체 hello 상태 검사 합니다. Hello AD CS 개체에 hello "Microsoft.InfromADUserAccountEnabled.xxx" 규칙을 통해 커넥터 toohello MV 개체를 확인 합니다.|
| 페더레이션 또는 암호 해시 동기화 사용자가 서비스 문제가 발생 했습니다 hello 암호 나타내는 전송 후 암호에 오류가 표시 tooreset 려 합니다. <br> <br> 또한 toothis, 하는 동안 암호 재설정 작업, "여러 명의 일치 항목 발견" 오류를 나타내는 hello Azure AD Connect 서비스에서 이벤트 로그에 오류가 표시 될 수 있습니다. | 이 해당 hello 동기화 엔진이 해당 hello MV 개체가 "Microsoft.InfromADUserAccountEnabled.xxx" hello 통해 한 AD CS 개체와 연결 된 toomore 검색을 나타냅니다. 즉 해당 hello 사용자 둘 이상의 포리스트에 있는 활성화 된 계정이 있습니다. **이 시나리오는 비밀번호 쓰기 저장을 지원하지 않습니다.** |
| 구성 오류가 있으면 암호 작업은 실패합니다. hello 응용 프로그램 이벤트 로그에 포함 <br> <br> 텍스트와 azure AD Connect 오류 6329가 있습니다: 0x8023061f (hello 작업이이 관리 에이전트에서 암호 동기화를 사용할 수 없으므로 실패 했습니다.) | 이 새 AD 포리스트 (또는 tooremove 및 기존 포리스트를 다시 추가) 후 암호 쓰기 저장 기능이 이미 설정 된 hello hello Azure AD Connect 구성이 변경 된 tooadd 경우 발생 합니다. 이렇게 새로 추가된 포리스트에서 사용자를 위한 암호 작업은 실패합니다. toofix hello 문제를 사용 하지 않도록 설정 하 고 hello 포리스트 구성 변경을 완료 된 후 hello 암호 쓰기 저장 기능을 다시 사용 하도록 설정 합니다. |

## <a name="password-writeback-event-log-error-codes"></a>비밀번호 쓰기 저장 이벤트 로그 오류 코드

암호 쓰기 저장 문제를 해결할 때 가장 좋은 방법은 응용 프로그램 이벤트 로그에 Azure AD Connect 컴퓨터 tooinspect 됩니다. 이 이벤트 로그는 비밀번호 쓰기 저장에 관심을 둔 두 개의 소스에서 비롯된 이벤트를 포함합니다. hello PasswordResetService 원본은 암호 쓰기 저장 문제 관련된 toohello 작업 및 작업을 설명 합니다. hello ADSync 원본은 AD 환경에서 문제 관련된 toosetting 암호 및 작업을 설명 합니다.

### <a name="source-of-event-is-adsync"></a>이벤트의 소스는 ADSync입니다.

| 코드 | 이름/메시지 | 설명 |
| --- | --- | --- |
| 6329 | BAIL: MMS(4924) 0x80230619 – "제한 hello 방지 되는 암호가 변경 toohello 현재 하나를 지정 합니다." | 이 이벤트는 암호 쓰기 저장 서비스 hello tooset hello 암호 사용 기간, 기록, 복잡성 또는 필터링 hello 도메인 요구 사항을 충족 하지 않는 로컬 디렉터리에서 암호를 시도할 때 발생 합니다. <br> <br> 최소 암호 사용 기간, 및 hello 시간 내에 암호를 최근에 변경가 없는 경우 수 toochange hello 암호 다시 지정 하는 hello에 도달할 때까지 도메인의 사용 기간입니다. 테스트를 위해 최소 보존 기간 too0을 설정 되어야 합니다. <br> <br> 암호 기록 요구 사항을 설정 하 고, 있는 경우 사용 되지 않은 hello에 마지막 N 개, 여기서 N은 hello 암호 기록 하는 암호를 선택 해야 설정 합니다. 이 경우 오류가 표시에 사용 된 hello 최근 N 회 동안 암호 선택 않으면 합니다. 테스트를 위해 기록 too0을 설정 되어야 합니다. <br> <br> 암호 복잡성 요구 사항이 있는 경우 hello 사용자가 toochange 시도할 때 적용 모두 또는 암호 다시 설정 합니다. <br> <br> 암호 필터가 사용 하도록 설정, 사용자 hello 필터링 조건을 만족 하지 않는 암호를 선택 하는 경우 재설정 hello 또는 변경 작업이 실패 합니다. |
| HR 8023042 | 동기화 엔진 반환 된 오류: hr = 80230402, 메시지 개체 hello로 중복 된 항목이 있기 때문에 실패 한 시도 tooget = 같은 앵커 | 이 이벤트 발생 hello 동일한 사용자 id가 여러 도메인에 사용 하도록 설정 합니다. 예를 들어 계정/리소스 포리스트를 동기화 하는 중 hello가 있는 경우 동일한 사용자 id 있고 활성화 각에서는이 오류가 발생할 수 있습니다. <br> <br> 사용자가 고유하지 않은 앵커 특성(예: 별칭 또는 UPN)을 사용하고 두 명의 사용자가 해당하는 동일한 앵커 특성을 공유하는 경우 이 오류가 발생할 수 있습니다. <br> <br> tooresolve이 문제를 하지 않았는지 중복 된 사용자 도메인 내에서 각 사용자에 대 한 고유한 앵커 특성을 사용 하 고 있는지 확인 합니다. |

### <a name="source-of-event-is-passwordresetservice"></a>이벤트의 소스는 PasswordResetService입니다.

| 코드 | 이름/메시지 | 설명 |
| --- | --- | --- |
| 31001 | PasswordResetStart | 이 이벤트는 hello 온-프레미스 서비스 검색 한 암호 재설정 hello 클라우드에서 시작 된 페더레이션 또는 암호 해시 동기화 사용자에 대 한 요청을 나타냅니다. 이 이벤트는 모든 암호에 첫 번째 이벤트 hello 쓰기 저장 작업을 다시 설정 합니다. |
| 31002 | PasswordResetSuccess | 이 이벤트는 사용자 암호 다시 설정 작업 동안 새 암호를 선택, 한 것으로 확인이 암호가 회사 암호 요구 사항을 충족 하 고 해당 암호에 다시 기록 되었습니다 toohello 로컬 AD 환경 나타냅니다. |
| 31003 | PasswordResetFail | 이 이벤트는 사용자는 암호를 선택 하 고 암호 toohello 온-프레미스 환경 성공적으로 도착 하지만 오류가 발생 했습니다. hello 로컬 AD 환경에서 tooset hello 암호를 시도 하는 것을 나타냅니다. 이 옵션은 다음과 같은 이유로 발생할 수 있습니다. <br> <br> hello 사용자의 암호 hello 사용 기간, 기록, 복잡성을 충족 하지 않거나 hello 도메인에 대 한 요구 사항을 필터링 합니다. 이 완전히 새로운 암호 tooresolve 하려고 시도 합니다. <br> <br> hello 사용자 계정에에 hello MA 서비스 계정이 hello 적절 한 사용 권한을 tooset hello 새 암호를 않아도 됩니다. <br> <br> hello 사용자의 계정이 암호 설정 작업을 허용 하지 않는 도메인 또는 enterprise admins와 같은 보호 된 그룹입니다. |
| 31004 | OnboardingEventStart | 이 이벤트는 Azure AD Connect와 암호 쓰기 저장을 사용 하는 경우에 발생 하 고 시작 했음을 온 보 딩 사용자 조직 toohello 암호 쓰기 저장 웹 서비스를 나타냅니다. |
| 31005 | OnboardingEventSuccess | 이 이벤트는 hello 등록 프로세스가 완료 되었으며 암호 쓰기 저장 기능이 준비 toouse 임을 나타냅니다. |
| 31006 | ChangePasswordStart | 이 이벤트 hello 온-프레미스 서비스 검색 hello 클라우드에서 시작 된 페더레이션 또는 암호 해시 동기화 사용자에 대 한 암호 변경 요청을 나타냅니다. 이 이벤트는 모든 암호 변경 쓰기 저장 작업의 hello 첫 번째 이벤트입니다. |
| 31007 | ChangePasswordSuccess | 이 이벤트는 사용자가 암호 변경 작업 동안 새 암호를 선택, 한 것으로 확인이 암호가 회사 암호 요구 사항을 충족 하 고 해당 암호에 다시 기록 되었습니다 toohello 로컬 AD 환경 나타냅니다. |
| 31008 | ChangePasswordFail | 이 이벤트는 사용자는 암호를 선택 하 고 암호 toohello 온-프레미스 환경 성공적으로 도착 하지만 오류가 발생 했습니다. hello 로컬 AD 환경에서 tooset hello 암호를 시도 하는 것을 나타냅니다. 이 옵션은 다음과 같은 이유로 발생할 수 있습니다. <br> <br> hello 사용자의 암호 hello 사용 기간, 기록, 복잡성을 충족 하지 않거나 hello 도메인에 대 한 요구 사항을 필터링 합니다. 이 완전히 새로운 암호 tooresolve 하려고 시도 합니다. <br> <br> hello 사용자 계정에에 hello MA 서비스 계정이 hello 적절 한 사용 권한을 tooset hello 새 암호를 않아도 됩니다. <br> <br> hello 사용자의 계정이 암호 설정 작업을 허용 하지 않는 도메인 또는 enterprise admins와 같은 보호 된 그룹입니다. |
| 31009 | ResetUserPasswordByAdminStart | hello 온-프레미스 서비스에서 검색 한 암호 재설정 사용자 대신 관리자에 게에서 시작 된 페더레이션 또는 암호 해시 동기화 사용자에 대 한 요청. 이 이벤트는 hello 모든 시작한 암호 재설정 쓰기 저장 작업의 첫 번째 이벤트입니다. |
| 31010 | ResetUserPasswordByAdminSuccess | admin 님 안녕하세요 시작한 암호 다시 설정 작업 동안 새 암호를 선택,이 암호가 회사 암호 요구 사항을 충족 하 고 해당 암호에 다시 기록 되었습니다 toohello 로컬 AD 환경 것으로 확인 합니다. |
| 31011 | ResetUserPasswordByAdminFail | admin 님 안녕하세요가 사용자 대신 암호를 선택 하 고 암호를 성공적으로 도착 toohello 온-프레미스 환경 있지만 오류가 발생 했습니다. hello 로컬 AD 환경에서 tooset hello 암호를 시도 했습니다. 이 옵션은 다음과 같은 이유로 발생할 수 있습니다. <br> <br> hello 사용자의 암호 hello 사용 기간, 기록, 복잡성을 충족 하지 않거나 hello 도메인에 대 한 요구 사항을 필터링 합니다. 이 완전히 새로운 암호 tooresolve 하려고 시도 합니다. <br> <br> hello 사용자 계정에에 hello MA 서비스 계정이 hello 적절 한 사용 권한을 tooset hello 새 암호를 않아도 됩니다. <br> <br> hello 사용자의 계정이 암호 설정 작업을 허용 하지 않는 도메인 또는 enterprise admins와 같은 보호 된 그룹입니다. |
| 31012 | OffboardingEventStart | 이 이벤트는 Azure AD Connect와 암호 쓰기 저장을 사용 하지 않도록 설정 하는 경우에 발생 하 고 시작 했음을 등록 취소 하면 조직 toohello 암호 쓰기 저장 웹 서비스를 나타냅니다. |
| 31013| OffboardingEventSuccess| 이 이벤트는 hello 등록 취소 프로세스가 완료 되었으며 암호 쓰기 저장 기능 비활성화 했습니다 나타냅니다. |
| 31014| OffboardingEventFail| 이 이벤트는 hello 등록 취소 프로세스가 실패 했습니다. 나타냅니다. Tooa 권한 오류 hello 클라우드 또는 온-프레미스 관리자 계정 구성 하는 동안 지정 된 것 같습니다 없거나 넣을 toouse 페더레이션된 클라우드 전역 관리자 암호 쓰기 저장을 사용 하지 않도록 설정 합니다. toofix 관리 권한을 해당 사용자가 하지이, 검사 hello 암호 쓰기 저장 기능을 구성 하는 동안 페더레이션 계정을 사용 합니다.|
| 31015| WriteBackServiceStarted| 이 이벤트는 해당 hello 암호 쓰기 저장 서비스가 성공적으로 시작 되었고 hello 클라우드에서 준비 tooaccept 암호 관리 요청을 나타냅니다.|
| 31016| WriteBackServiceStopped| 이 이벤트는 hello 암호 쓰기 저장 서비스가 중지 되었습니다. hello 클라우드에서 모든 암호 관리 요청이 성공 수 없음을 나타냅니다.|
| 31017| AuthTokenSuccess| 이 이벤트는 Azure AD Connect는 설치 toostart hello 등록 취소 또는 등록 프로세스 중에 지정한 전역 admin 님 안녕하세요에 대 한 권한 부여 토큰을 성공적으로 검색에서는 나타냅니다.|
| 31018| KeyPairCreationSuccess| 이 이벤트는 hello 암호 암호화 키 hello 클라우드 전송 toobe tooyour 온-프레미스 환경에서 사용 되는 tooencrypt 암호를 만들었음을 나타냅니다.|
| 32000| UnknownError| 이 이벤트는 암호 관리 작업을 하는 동안 알 수 없는 오류를 나타냅니다. 자세한 내용은 hello 이벤트의 hello 예외 텍스트를 확인 합니다. 문제가 발생하는 경우 암호 쓰기 저장 기능을 비활성화하고 재활성화하여 시도하십시오. 도움이 되지 않고 하는 경우 추적 id 지정된 내부자 tooyour 지원 엔지니어는 hello와 함께 이벤트 로그의 복사본을 포함 합니다.|
| 32001| ServiceError| 이 이벤트 다시 설정 서비스를 toohello 클라우드 암호를 연결에 오류가 발생 한 것 및 hello 온-프레미스 서비스에서 없습니다 tooconnect toohello 암호 다시 설정 웹 서비스 하는 경우 발생 합니다.|
| 32002| ServiceBusError| 이 이벤트가 나타냅니다 tooyour 테 넌 트의 서비스 버스 인스턴스에 연결 하는 오류가 발생 했습니다. 이는 온-프레미스 환경에서 아웃 바운드 연결을 차단하기 때문에 발생할 수 있습니다. TCP 443 및 toohttps://ssprsbprodncu-sb.accesscontrol.windows.net/를 통해 연결을 허용 하 고 다시 시도 하 여 방화벽 tooensure를 확인 합니다. 여전히 문제가 발생하는 경우 암호 쓰기 저장 기능을 비활성화하고 재활성화하여 시도하십시오.|
| 32003| InPutValidationError| 이 이벤트는 tooour 웹 서비스 API를 전달 된 hello 입력이 잘못 되었음을 나타냅니다. Hello 작업을 다시 시도 하십시오.|
| 32004| DecryptionError| 이 이벤트는 hello 클라우드에서 도착 하는 hello 암호 해독 오류가 발생 했음을 나타냅니다. Hello 클라우드 서비스와 온-프레미스 환경 사이의 암호 해독 키 불일치 때문일 수 있습니다. tooresolve이를 사용 하지 않도록 설정 하 고 다시 온-프레미스 환경에서 암호 쓰기 저장을 사용 합니다.|
| 32005| ConfigurationError| 온보딩하는 동안 온-프레미스 환경의 구성 파일에서 테넌트 관련 정보를 저장합니다. 이 이벤트가 나타냅니다 hello 서비스를 시작 하는 경우이 파일 또는 저장 중 오류 발생 된 hello 파일을 읽는 동안 오류가 발생 했습니다. toofix이이 문제를 사용 하지 않도록 설정 하 고 다시 tooforce 암호 쓰기 저장이 구성 파일의 다시 쓰기를 사용 하도록 설정 해 보십시오.|
| 32007| OnBoardingConfigUpdateError| 등록 하는 동안 데이터 hello 클라우드 toohello에서 온-프레미스 암호 다시 설정 서비스 보냅니다. 그런 다음 해당 데이터는 tooan 메모리에 파일이 있을 때까지 전송 toohello 동기화 서비스 toostore이이 정보를 디스크에 안전 하 게 기록 됩니다. 이 이벤트는 메모리에서 해당 데이터를 작성하거나 업데이트하는 데 문제가 있음을 나타냅니다. toofix이이 문제를 사용 하지 않도록 설정 하 고 다시 tooforce 암호 쓰기 저장이이 구성의 다시 쓰기를 사용 하도록 설정 해 보십시오.|
| 32008| ValidationError| 이 이벤트는 hello 암호 다시 설정 웹 서비스에서 잘못 된 응답을 수신 했습니다 나타냅니다. toofix이이 문제를 사용 하지 않도록 설정 하 고 암호 쓰기 저장을 다시 사용 하도록 설정 해 보십시오.|
| 32009| AuthTokenError| 이 이벤트는 가져올 수 없음을 권한 부여 토큰 Azure AD Connect 설치 중에 지정한 hello 전역 관리자 계정에 대 한 것을 나타냅니다. 이 오류는 잘못 된 사용자 이름으로 발생할 수 있습니다 또는 hello 전역 관리자 계정에 지정 된 암호나 hello 전역 관리자 계정을 지정 하기 때문에 페더레이션 됩니다. toofix hello 사용 하 여 다시 실행된 구성이이 문제를 사용자 이름 및 암호를 수정 하 고 관리 되는 (클라우드 전용 또는 암호 동기화) 계정 관리자에 게 확인 합니다.|
| 32010| CryptoError| 이 이벤트는 암호의 암호화 키 또는 hello 클라우드 서비스에서 도착 하는 암호를 해독할 hello 생성 오류가 발생 했습니다. 나타냅니다. 이 오류가 환경에 문제가 있음을 나타낼 수 있습니다. 자세한 이벤트 로그 toolearn 프로그램의 세부 정보 hello와이 문제를 해결 하십시오. 수도이 작업을 수행할 hello 암호 쓰기 저장 서비스 tooresolve 사용 하지 않도록 설정 했다가 다시 사용 하도록 설정 합니다.|
| 32011| OnBoardingServiceError| 이 이벤트는 온-프레미스 서비스 hello hello 암호 다시 설정 웹 서비스 tooinitiate hello 온 보 딩 프로세스와 올바르게 통신 하지 못했습니다 나타냅니다. 이는 테넌트에 대한 인증 토큰을 가져오는 방화벽 규칙 또는 문제 때문일 수 있습니다. toofix이 TCP 443 및 TCP 9350 9354 또는 toohttps://ssprsbprodncu-sb.accesscontrol.windows.net/을 통한 아웃 바운드 연결을 차단 하지는 해당 hello tooonboard를 사용 하는 AAD 관리자 계정이 페더레이션 계정이 아닌지 확인 합니다.|
| 32013| OffBoardingError| 이 이벤트는 온-프레미스 서비스 hello hello 암호 다시 설정 웹 서비스 tooinitiate hello 등록 취소 프로세스와 올바르게 통신 하지 못했습니다 나타냅니다. 이는 테넌트에 대한 인증 토큰을 가져오는 방화벽 규칙 또는 문제 때문일 수 있습니다. toofix이 toohttps://ssprsbprodncu-sb.accesscontrol.windows.net/, 또는 443을 통해 아웃 바운드 연결을 차단 하지는 해당 hello toooffboard를 사용 하는 AAD 관리자 계정이 페더레이션 계정이 아닌지 확인 합니다.|
| 32014| ServiceBusWarning| 이 이벤트는 tooretry tooconnect tooyour 테 넌 트의 서비스 버스 인스턴스에 놓았습니다 나타냅니다. 정상 조건에서이 해야 되지에 문제가 되지 않지만이 이벤트가 여러 번 표시 하는 경우 대기 시간이 길거나 낮은 대역폭 연결 경우 특히 네트워크 연결 tooservice 버스를 확인 하십시오.|
| 32015| ReportServiceHealthError| 암호 쓰기 저장 서비스의 순서 toomonitor hello 상태에서 하트 비트 데이터 tooour 암호 다시 설정 웹 서비스 5 분 마다 보냅니다. 이 이벤트는이 상태 정보 백 toohello 클라우드 웹 서비스를 보낼 때 오류가 발생 했음을 나타냅니다. 이 상태 정보는 OII 또는 PII 데이터가 포함 되지 않은 않으며 순수 하 게 하트 비트 및 기본 서비스 통계를 hello 클라우드의 서비스 상태 정보를 제공할 수 있습니다.|
| 33001| ADUnKnownError| 이 이벤트 AD에서 반환 된 알 수 없는 오류가 있었음을 나타냅니다.이 오류에 대 한 자세한 정보에 대 한 hello ADSync 원본의 이벤트에 대 한 hello 서버 이벤트 로그를 Azure AD Connect를 확인 하세요.|
| 33002| ADUserNotFoundError| 이 이벤트는 해당 hello 사용자에 게 tooreset 또는 암호 hello 온-프레미스 디렉터리에 없습니다. 변경을 나타냅니다. Hello 사용자가 삭제 된 온-프레미스 되는 경우에 있지만 hello 클라우드가 발생할 수 또는 동기화에 문제가 있는 경우. 동기화 로그를 확인 하 고 hello 마지막 자세한 정보에 대 한 몇 가지 동기화 실행 세부 정보.|
| 33003| ADMutliMatchError| Azure AD Connect toodetermine의 hello 설치 과정에서 방법을 지정 하는 hello 클라우드 앵커 암호 다시 설정 하거나 변경 요청이 hello 클라우드에서 시작을 사용 하 여 온-프레미스 환경에서 백 tooa 사용자 요청 toolink 합니다. 이 이벤트 hello로 온-프레미스 디렉터리에 두 명의 사용자가 있음을 나타냅니다. 동일한 클라우드 앵커 특성입니다. 동기화 로그를 확인 하 고 hello 마지막 자세한 정보에 대 한 몇 가지 동기화 실행 세부 정보.|
| 33004| ADPermissionsError| 이 이벤트는 관리 에이전트 서비스 계정이 해당 hello hello 적절 한 권한이 없을 hello에 계정에 tooset 새 암호를 나타냅니다. 해당 hello hello 사용자 포리스트의 MA 계정 재설정 및 변경 암호에 대 한 권한이 hello 포리스트의 모든 개체에에서 확인 합니다. Toothis 하는 방법에 대 한 자세한 내용은 4 단계를 참조: hello 적절 한 Active Directory 사용 권한을 설정 합니다.|
| 33005| ADUserAccountDisabled| 이 이벤트는 tooreset 시도 우리 또는 온-프레미스에서 사용할 수 없는 계정에 대 한 암호를 변경 하는 나타냅니다. Hello 계정을 사용 하도록 설정 하 고 hello 작업을 다시 시도 하십시오.|
| 33006| ADUserAccountLockedOut| 이벤트는 tooreset 시도 우리 또는 온-프레미스에서 잠긴 계정의 암호를 변경 하는 나타냅니다. 사용자가 짧은 기간 동안 너무 여러 번 암호 작업을 변경 또는 재설정하려는 경우 잠겨질 수 있습니다. Hello 계정의 잠금을 해제 하 고 hello 작업을 다시 시도 하십시오.|
| 33007| ADUserIncorrectPassword| 이 이벤트는 해당 hello 사용자 변경 작업을 수행 하는 암호 때 현재 암호를 잘못 지정을 나타냅니다. 현재 암호를 올바르게 hello를 지정 하 고 다시 시도 하십시오.|
| 33008| ADPasswordPolicyError| 이 이벤트는 암호 쓰기 저장 서비스 hello tooset hello 암호 사용 기간, 기록, 복잡성 또는 필터링 hello 도메인 요구 사항을 충족 하지 않는 로컬 디렉터리에서 암호를 시도할 때 발생 합니다. <br> <br> 최소 암호 사용 기간, 및 hello 시간 내에 암호를 최근에 변경가 없는 경우 수 toochange hello 암호 다시 지정 하는 hello에 도달할 때까지 도메인의 사용 기간입니다. 테스트를 위해 최소 보존 기간 too0을 설정 되어야 합니다. <br> <br> 암호 기록 요구 사항을 설정 하 고, 있는 경우 사용 되지 않은 hello에 마지막 N 개, 여기서 N은 hello 암호 기록 하는 암호를 선택 해야 설정 합니다. 이 경우 오류가 표시에 사용 된 hello 최근 N 회 동안 암호 선택 않으면 합니다. 테스트를 위해 기록 too0을 설정 되어야 합니다. <br> <br> 암호 복잡성 요구 사항이 있는 경우 hello 사용자가 toochange 시도할 때 적용 모두 또는 암호 다시 설정 합니다. <br> <br> 암호 필터가 사용 하도록 설정, 사용자 hello 필터링 조건을 만족 하지 않는 암호를 선택 하는 경우 재설정 hello 또는 변경 작업이 실패 합니다.|
| 33009| ADConfigurationError| 이 이벤트는 암호 백 tooyour 온-프레미스 Active Directory와 tooa 구성 문제로 인해 디렉터리를 작성 하는 문제가 발생 했습니다. 나타냅니다. 발생 한 오류에 대 한 자세한 내용은 hello ADSync 서비스의 메시지에 대 한 hello Azure AD Connect 컴퓨터의 응용 프로그램 이벤트 로그를 확인 합니다.|


## <a name="troubleshoot-password-writeback-connectivity"></a>암호 쓰기 저장 연결 문제 해결

Azure AD Connect의 hello 암호 쓰기 저장 구성 요소에 서비스 중단이 발생 하는 경우이 tooresolve를 수행할 수 있는 일부 빠른 단계 다음과 같습니다.

* [다시 시작 해야 Azure AD Connect Sync 서비스가 hello](#restart-the-azure-ad-connect-sync-service)
* [사용 하지 않도록 설정 하 고 다시 hello 암호 쓰기 저장 기능을 사용 하도록 설정](#disable-and-re-enable-the-password-writeback-feature)
* [Hello 최신 Azure AD Connect 릴리스 설치](#install-the-latest-azure-ad-connect-release)
* [비밀번호 쓰기 저장 문제 해결](#troubleshoot-password-writeback)

일반적으로 다음이 단계를 실행 toorecover 위에 hello 순서로 서비스 hello 가장 빠른 방법으로 하는 것이 좋습니다.

### <a name="restart-hello-azure-ad-connect-sync-service"></a>다시 시작 해야 Azure AD Connect Sync 서비스가 hello

Hello를 다시 시작 하면 tooresolve 연결 문제 또는 다른 일시적인 문제 hello 서비스를 Azure AD Connect Sync 서비스가 수 도움이 됩니다.

1. 관리자로 서 클릭 **시작** 실행 하는 hello 서버의 **Azure AD Connect**합니다.
2. 형식 **"services.msc"** hello 검색 상자 및 키를 눌러 **Enter**합니다.
3. Hello에 대 한 확인 **Microsoft Azure AD Sync** 항목입니다.
4. hello 서비스 항목을 마우스 오른쪽 단추로 클릭 **다시 시작**, hello 작업 toocomplete 될 때까지 기다립니다.

   ![Hello Azure AD Sync 서비스를 다시 시작][Service Restart]

이러한 단계는 hello 클라우드 서비스와 연결 다시 설정 하 고 발생할 수 있습니다 중단 문제를 해결 합니다. Hello 동기화 서비스를 다시 시작 해도 문제가 해결 되지 경우 toodisable 시도 다시 다음 단계로 hello 암호 쓰기 저장 기능을 사용 하도록 설정 하는 것이 좋습니다.

### <a name="disable-and-re-enable-hello-password-writeback-feature"></a>사용 하지 않도록 설정 하 고 다시 hello 암호 쓰기 저장 기능을 사용 하도록 설정

해제 및 다시 설정 hello 암호 쓰기 저장 기능을 사용 하 tooresolve 연결에 문제가 발생 합니다.

1. 관리자 권한으로 열고 hello **Azure AD Connect 구성 마법사**합니다.
2. Hello에 **tooAzure AD 연결** 대화 상자에서를 입력 하면 **Azure AD 전역 관리자 자격 증명**
3. Hello에 **tooAD DS 연결** 대화 상자에서를 입력 하면 **AD 도메인 서비스 관리자 자격 증명**합니다.
4. Hello에 **사용자가 고유 하 게 식별** 대화 상자에서 hello 클릭 **다음** 단추입니다.
5. Hello에 **선택적 기능** 대화 상자에서 hello의 선택을 취소 **암호 쓰기 저장** 확인란을 선택 합니다.
6. 클릭 **다음** hello 남은 toohello에 도달할 때까지 아무 것도 변경 하지 않고 대화 상자 페이지를 통해 **준비 tooconfigure** 페이지.
7. 구성 하 여 해당 hello 페이지 표시 hello **암호 쓰기 저장 옵션을 사용 하지 않도록** 녹색 hello를 클릭 한 다음 **구성** toocommit 변경 내용을 단추 합니다.
8. Hello에 **마침** 대화 상자에서 hello 선택 취소 **지금 동기화** 옵션을 선택한 다음 클릭 **마침** tooclose hello 마법사.
9. Hello를 다시 열고 **Azure AD Connect 구성 마법사**합니다.
10. **2-8 단계를 반복**를 제외 하 고 있습니다, **hello 암호 쓰기 저장 옵션을 선택** hello에 **선택적 기능** toore 사용 hello 서비스 화면입니다.

이러한 단계를 실행하여 클라우드 서비스를 사용하여 연결을 재설정하고 발생할 수 있는 중단이 해결될 수 있습니다.

비활성화 및 다시 hello 암호 쓰기 저장 기능을 사용 하면 문제가 해결 되지 않으면, tooreinstall 다음 단계로 Azure AD Connect를 시도 하는 것이 좋습니다.

### <a name="install-hello-latest-azure-ad-connect-release"></a>Hello 최신 Azure AD Connect 릴리스 설치

Azure AD Connect를 다시 설치하면 클라우드 서비스와 로컬 AD 환경 간의 구성 및 연결 문제를 해결할 수 있습니다.

위에서 설명한 hello 처음 두 단계를 시도한 후에이 단계를 수행할 것이 좋습니다.

> [!WARNING]
> Hello 상자 동기화 규칙에서 사용자 지정한 경우 **수동으로 완료 한 후 다시 배포 하 고 업그레이드를 계속 하기 전에 이러한 백업**합니다.

1. Hello에서 hello 최신 버전의 Azure AD Connect 다운로드 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=615771)합니다.
2. Azure AD Connect를 이미 설치한 이후 Azure AD Connect 설치 toohello 최신 버전이 tooperform 내부 업그레이드 tooupdate 있어야 합니다.
3. Hello 다운로드 한 패키지를 실행 하 고 지침 tooupdate hello 화면에 나타나는 따릅니다 Azure AD Connect 컴퓨터입니다.

이러한 단계를 실행하여 클라우드 서비스를 사용하여 연결을 재설정하면 사용자에게 발생할 수 있는 중단을 해결할 수 있습니다.

설치 hello 최신 버전의 hello Azure AD Connect 서버 문제를 해결 되지 않으면, hello 최신 릴리스를 설치한 후 마지막 단계로 암호 쓰기 저장을 사용 하지 않도록 설정 했다가 다시 사용 하도록 설정를 시도 하는 것이 좋습니다.

## <a name="verify-whether-azure-ad-connect-has-hello-required-permission-for-password-writeback"></a>Azure AD Connect에 암호 쓰기 저장에 대 한 hello 필요한 권한이 있는지 확인 하십시오. 
Azure AD Connect 필요 AD **암호 재설정** 권한 tooperform 암호 쓰기 저장 합니다. 했는지 toofind Azure AD Connect 권한이 hello에 대 한는 지정한 온-프레미스 AD 사용자 계정을 hello 유효 사용 권한을 Windows 기능을 사용할 수 있습니다.

1. TooAzure AD 연결 서버에 로그인 하 고 hello 시작 **동기화 서비스 관리자** (→ 시작 동기화 서비스).
2. Hello에서 **커넥터** 탭을 선택 hello 온-프레미스 **AD 커넥터** 클릭 **속성**합니다.  
![유효 권한 - 2단계](./media/active-directory-passwords-troubleshoot/checkpermission01.png)  
3. Hello 팝업 대화 상자에서 선택한 hello **tooActive Directory 포리스트에 연결** 탭과 hello 기록해 **사용자 이름** 속성입니다. Azure AD Connect tooperform 디렉터리 동기화에서 사용 하는 hello AD DS 계정입니다. Azure AD Connect tooperform 암호 쓰기 저장에 대 한 hello AD DS 계정에 암호 재설정 권한이 있어야 합니다.  
![유효 권한 - 3단계](./media/active-directory-passwords-troubleshoot/checkpermission02.png)  
4. 로그 tooan에 온-프레미스 도메인 컨트롤러와 시작 hello **Active Directory 사용자 및 컴퓨터** 응용 프로그램입니다.
5. **보기**를 클릭하고 **고급 기능** 옵션이 사용하도록 설정되어 있는지 확인합니다.  
![유효 권한 - 5단계](./media/active-directory-passwords-troubleshoot/checkpermission03.png)  
6. Hello tooverify AD 사용자 계정 찾습니다. Hello 계정을 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.  
![유효 권한 - 6단계](./media/active-directory-passwords-troubleshoot/checkpermission04.png)  
7. Hello 팝업 대화 상자에서 이동 toohello **보안** 탭을 클릭 **고급**합니다.  
![유효 권한 - 7단계](./media/active-directory-passwords-troubleshoot/checkpermission05.png)  
8. Hello 고급 보안 설정 팝업 대화 상자에서 이동 toohello **유효한 액세스** 탭 합니다.
9. 클릭 **사용자 선택** 하 고 Azure AD Connect에서 사용 하는 hello AD DS 계정 선택 (3 단계 참조). 그다음에 **유효한 액세스 보기**를 클릭합니다.  
![유효 권한 - 9단계](./media/active-directory-passwords-troubleshoot/checkpermission06.png)  
10. 아래로 스크롤하여 **암호 재설정**을 검색합니다. Hello 항목을 선택 하면 hello AD DS 계정에 권한이 있는지 의미의 hello tooreset hello 암호에는 AD 사용자 계정을 선택 합니다.  
![유효 권한 - 10단계](./media/active-directory-passwords-troubleshoot/checkpermission07.png)  

## <a name="azure-ad-forums"></a>Azure AD 포럼

Azure AD에 대 한 일반적인 질문이 있는 경우 셀프 서비스 암호 재설정 있습니다 수 hello 커뮤니티에 지원을 요청 hello 및 [Azure AD 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD)합니다. Hello 커뮤니티 구성원 엔지니어, 제품 관리자, Mvp 및 친구 IT 전문가 포함합니다.

## <a name="contact-microsoft-support"></a>Microsoft 지원에 문의

Hello 응답 tooan 문제를 찾을 수 없는 경우 지원 팀은 항상 사용 가능한 tooassist 수익과입니다.

tooproperly 지원, 포함 된 사례를 열 때 가능한 세부 정보를 제공 하 게 합니다.

* **Hello 오류에 대 한 일반적인 설명** -hello 오류 란? 발견 된 hello 동작은 무엇 이었습니까? Hello 오류를 어떻게 재현할 수 우리? 최대한 많은 세부 정보를 제공해주세요.
* **페이지** -hello 오류를 발견 하는 경우에 된? 수 tooand 스크린 샷을 있다면 hello URL을 포함 하십시오.
* **코드 지원** -hello 수준과 hello 오류를 표시 하는 경우에 생성 하는 hello 지원 코드 무엇 이었습니까? 
    * toofind이 재현 hello 오류 클릭 hello hello hello 화면 맨 아래에 지원 코드 링크 및 송신 hello 지원 엔지니어 hello 결과 GUID 합니다.
    ![Hello hello 화면 맨 아래에 hello 지원 코드 찾기][Support Code]
    * 인 경우 hello 맨 아래에 지원 코드가 없으면 페이지에서 f12 키를 누르고 SID 및 CID 검색 보내고 이러한 두 가지 결과 toohello 지원 엔지니어입니다.
* **날짜, 시간 및 표준 시간대** -hello 정확한 날짜 및 시간을 포함 하십시오 **hello 표준 시간대와** hello 오류가 발생 했습니다.
* **사용자 ID** -hello 오류 보여 준다는 사실을 알았습니다 hello 사용자를 게? (user@contoso.com)
    * 페더레이션된 사용자입니까?
    * 암호 해시 동기화 사용자입니까?
    * 클라우드 전용 사용자입니까?
* **라이선스** -hello 사용자는 Azure AD Premium 또는 Azure AD Basic 라이선스가 할당 있습니까?
* **응용 프로그램 이벤트 로그** hello 오류 하면 온-프레미스 인프라에는 암호 쓰기 저장을 사용 하는 경우-지원 서비스에 문의할 때 hello Azure AD Connect 서버에서 응용 프로그램 이벤트 로그의 압축 된 복사본을 포함 합니다.

    

[Service Restart]: ./media/active-directory-passwords-troubleshoot/servicerestart.png "Hello Azure AD Sync 서비스를 다시 시작"
[Support Code]: ./media/active-directory-passwords-troubleshoot/supportcode.png "지원 코드 hello 창의 오른쪽 hello 아래에 위치한"

## <a name="next-steps"></a>다음 단계

링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.

* [**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작 
* [**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성
* [**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법
* [**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자
* [**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.
* [**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정
* [**비밀번호 쓰기 저장**](active-directory-passwords-writeback.md) - 비밀번호 쓰기 저장이 온-프레미스 디렉터리와 함께 작동 하는 원리
* [**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색
* [**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법
* [**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로? 그 이유는 무엇을? 어디서? 누가? 언제? -Tooask 항상 필요한 tooquestions 답변
