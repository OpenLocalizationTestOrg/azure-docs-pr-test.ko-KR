---
title: "단일 로그온 aaaProblems tooa 갤러리 비 페더레이션에 대해 구성 된 응용 프로그램에 서명 | Microsoft Docs"
description: "SAML 기반 페더레이션 single sign on Azure ad에 대해 구성 된 tooan 응용 프로그램에 로그인 할 때 직면할 수 있는 hello 특정 문제에 대 한 지침"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 1243456695c097f404a66fc89893efa2afdaaf22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-non-gallery-application-configured-for-federated-single-sign-on"></a>페더레이션된 single sign-on에 대해 구성 된 tooa 갤러리가 아닌 응용 프로그램에 로그인 하는 문제

tootroubleshoot 문제를 다음과 같이 Azure AD에서 tooverify hello 응용 프로그램 구성 해야 합니다.

-   Hello Azure AD 갤러리 응용 프로그램에 대 한 모든 hello 구성 단계를 따랐는지 합니다.

-   hello 식별자 및 AAD에서 구성 된 회신 URL은 hello 응용 프로그램의 예상 값 일치

-   사용자가 toohello 응용 프로그램 할당

## <a name="application-not-found-in-directory"></a>응용 프로그램을 디렉터리에서 찾을 수 없습니다

*오류 AADSTS70001: 응용 프로그램 식별자 'https://contoso.com' hello 디렉터리에 없습니다.*합니다.

**가능한 원인**

hello 발급자 특성 hello SAML 요청에는 AD hello Azure AD 응용 프로그램에 구성 된 hello 식별자 값과 일치 하지 않습니다 hello 응용 프로그램 tooAzure에서 보냅니다.

**해결 방법**

Azure AD에서 구성 된 식별자 값 hello를 일치 하는 hello SAML 요청에서 해당 hello 발급자 특성을 확인 합니다.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

   * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  <span id="_Hlk477190042" class="anchor"></span>너무 이동**도메인 및 Url** 섹션. Hello 텍스트 상자에는 hello 오류가 표시 되는 hello 식별자 값에 대 한 hello 값과 일치 하는 식별자에에서 hello 값을 확인 합니다.

Azure AD의 hello 식별자 값을 업데이트 한 후 해당 일치 하는 hello 값 hello SAML 요청에서 hello 응용 프로그램으로 전송 수 toosign toohello 응용 프로그램에 있어야 합니다.

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a>hello 회신 주소 hello 응용 프로그램으로 구성 된 hello 회신 주소를 일치 하지 않습니다. 

*오류 AADSTS50011: hello 회신 주소 'https://contoso.com' hello 응용 프로그램으로 구성 된 hello 회신 주소를 일치 하지 않습니다.* 

**가능한 원인** 

hello hello SAML 요청에 AssertionConsumerServiceURL 값 hello 회신 URL 값 또는 Azure AD에 구성 된 패턴과 일치 하지 않습니다. hello AssertionConsumerServiceURL hello SAML 요청에는 값은 hello 오류에서 참조 하는 hello URL입니다. 

**해결 방법** 

Azure AD에서의 일치 하는 hello 회신 URL 값 구성 hello SAML 요청에 hello AssertionConsumerServiceURL 값을 확인 합니다. 
 
1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자** 

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다. 

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다. 

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다. 

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다. 

  * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**
  
6.  Hello 응용 프로그램 선택 tooconfigure single sign on

7.  Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  너무 이동**도메인 및 Url** 섹션. 확인 하거나 hello 회신 URL 텍스트 상자에 붙여넣습니다 toomatch hello hello SAML 요청에 AssertionConsumerServiceURL 값 hello 값을 업데이트 합니다.

  * Hello 회신 URL 텍스트 상자에 표시 되지 않으면, 선택 hello **고급 URL 설정 표시** 확인란을 선택 합니다. 

Azure AD에서 hello 회신 URL 값을 업데이트 하 고 있으며 후 hello 값과 일치 하 hello 응용 프로그램에 의해 hello에서 SAML 요청을 보냅니다 수 toosign toohello 응용 프로그램에 있어야 합니다.

## <a name="user-not-assigned-a-role"></a>역할이 지정되지 않은 사용자

*오류 AADSTS50105: 사용자에서 로그인 되었습니다. hello 'brian@contoso.com' hello 응용 프로그램에 대 한 tooa 역할 할당 되지 않은*

**가능한 원인**

hello 사용자는 액세스 toohello 응용 프로그램이 Azure AD에서 허가 되지 않았습니다.

**해결 방법**

tooassign 아래의 hello 단계를 직접 수행 하는 하나 이상의 사용자가 tooan 응용 프로그램:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

  * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  원하는 사용자 toofrom hello 목록 tooassign hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 **사용자 및 그룹** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  Hello 클릭 **추가** hello 위로 단추 **사용자 및 그룹** 목록 tooopen hello **할당 추가** 블레이드입니다.

9.  hello 클릭 **사용자 및 그룹** hello에서 선택기 **할당 추가** 블레이드입니다.

10. Hello 입력 **전체 이름** 또는 **전자 메일 주소** hello에 할당 하려는 hello 사용자의 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자입니다.

11. Hello 위로 마우스를 가져가고 **사용자** hello 목록 tooreveal에는 **확인란**합니다. Hello 확인란 다음 toohello 사용자의 프로필 사진 또는 로고 tooadd 사용자 toohello 클릭 **선택한** 목록입니다.

12. **선택 사항:** 너무 원하는 경우**둘 이상의 사용자를 추가**, 다른 유형 **전체 이름** 또는 **전자 메일 주소** hello에 **이름으로 검색 전자 메일 주소 또는** 상자에서 검색 하 고이 사용자 toohello hello 확인란 tooadd 클릭 **선택한** 목록입니다.

13. 사용자 선택을 완료 했으면 클릭 hello **선택** 단추 tooadd 해당 사용자 및 그룹 toobe toohello 목록이 toohello 응용 프로그램을 할당 합니다.

14. **선택 사항:** hello 클릭 **역할 선택** hello에 선택 기가 **할당 추가** 블레이드 tooselect 역할 tooassign toohello 사용자가 선택한 합니다.

15. Hello 클릭 **할당** 단추 tooassign hello 응용 프로그램 toohello 사용자를 선택 합니다.

시간의 짧은 기간 이후에 hello 사용자가 선택한 이러한 응용 프로그램을 사용 하 여 hello hello 솔루션 설명 섹션에 설명 된 방법 수 toolaunch 수 있습니다.

## <a name="not-a-valid-saml-request"></a>유효한 SAML 요청이 아님

*오류 AADSTS75005: hello 요청을 유효한 토큰이 Saml2 프로토콜 메시지가 아닙니다.*

**가능한 원인**

Azure AD SAML Single Sign on에 대 한 hello 응용 프로그램에서 보낸 요청 hello를 지원 하지 않습니다. 일반적인 문제는 다음과 같습니다.

-   Hello SAML 요청에 필수 필드가 누락

-   SAML 요청 인코딩 방법

**해결 방법**

1.  SAML 요청을 캡처합니다. hello 자습서 따라 [어떻게 toodebug SAML 기반 single sign on tooapplications Azure AD에서](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toocapture hello SAML 요청 하는 방법을 toolearn 합니다.

2.  Hello 응용 프로그램 공급 업체와 공유 문의:

    -   SAML 요청

    -   [Azure AD Single Sign-On SAML 프로토콜 요구 사항](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

유효성을 검사 해야 Single Sign on에 대 한 hello Azure AD SAML 구현을 지원 합니다.

## <a name="no-resource-in-requiredresourceaccess-list"></a>requiredResourceAccess 목록에 리소스 없음

*오류 AADSTS65005: hello 클라이언트 응용 프로그램에서 요청 액세스 tooresource ' 00000002-0000-0000-c000-000000000000'. 이 요청이 실패 했습니다 hello 클라이언트가 requiredResourceAccess 목록에이 리소스를 지정 하지 않은*합니다.

**가능한 원인**

hello application 개체 손상 되었습니다.

**해결 방법**

hello 디렉터리에서 제거 hello 응용 프로그램 toosolve hello 문제입니다. 그런 다음 추가 하 고 hello 응용 프로그램을 다시 구성 다음 hello 단계를 수행 하십시오.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

  * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.

7.  클릭 **삭제** hello의 왼쪽 위에 hello 응용 프로그램에서 **개요** 블레이드입니다.

8.  Azure AD 새로 고치고 hello Azure AD 갤러리에서 hello 응용 프로그램을 추가 합니다. 그런 다음 hello 응용 프로그램을 다시 구성 합니다.

Hello 응용 프로그램을 다시 구성한 후 수 toosign toohello 응용 프로그램에 있어야 합니다.

## <a name="certificate-or-key-not-configured"></a>인증서 또는 키가 구성되지 않음

오류 AADSTS50003: 서명 키가 구성되지 않았습니다.

**가능한 원인**

hello application 개체 손상 및 Azure AD는 hello 응용 프로그램에 대해 구성 된 hello 인증서를 인식 하지 못하는 합니다.

**해결 방법**

toodelete 새 인증서를 만들 다음 hello 단계를 수행 하십시오.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

  * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  클릭 **새 인증서 만들기** hello에서 **SAML 서명 인증서** 섹션.

9.  [만료 날짜]를 선택합니다. 그런 다음 **저장**을 클릭합니다.

10. 확인 **새 인증서를 활성화할** toooverride hello 활성 인증서입니다. 클릭 **저장** hello hello 블레이드 위쪽에 tooactivate hello 롤오버 인증서를 수락 하 고 있습니다.

11. Hello에서 **SAML 서명 인증서** 섹션에서 클릭 **제거** tooremove hello **사용 안 함** 인증서입니다.

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a>문제 hello SAML 클레임을 사용자 지정할 때 전송 tooan 응용 프로그램

toolearn toocustomize hello SAML 특성 클레임 전송 tooyour 응용 프로그램 참조 [Azure Active Directory에서 매핑을 클레임](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) 자세한 정보에 대 한 합니다.

## <a name="next-steps"></a>다음 단계
[Azure AD Single Sign-On SAML 프로토콜 요구 사항](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
