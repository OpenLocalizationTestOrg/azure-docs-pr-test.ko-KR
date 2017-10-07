---
title: "SaaS 앱에 대 한 조건부 액세스 aaaAzure | Microsoft Docs"
description: "Azure AD에서 조건부 액세스는 신뢰할 수 있는 네트워크에 없는 사용자에 대 한 있습니다 tooconfigure 응용 프로그램별 다단계 인증 액세스 규칙 및 hello 기능 tooblock 액세스를 허용 합니다. "
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 69748014c0c8e266ba66562980c784aba4c68d80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-conditional-access"></a>Azure Active Directory 조건부 액세스 시작
[SaaS](https://azure.microsoft.com/overview/what-is-saas/) 앱과 Azure AD 연결 앱에 대한 Azure Active Directory 조건부 액세스는 그룹, 위치 및 응용 프로그램 민감도에 따라 조건부 액세스를 구성할 수 있습니다. 

응용 프로그램 민감도를 기반으로 하는 조건부 액세스를 통해 응용 프로그램당 Multi-Factor Authentication(MFA) 액세스 규칙을 설정할 수 있습니다. 응용 프로그램당 MFA 신뢰할 수 있는 네트워크에 없는 사용자에 대 한 hello 기능 tooblock 액세스를 제공 합니다. MFA 규칙 tooall toohello 응용 프로그램에 할당 된 사용자 또는 사용자가 지정 된 보안 그룹 내에서 사용자에 대해서만 적용할 수 있습니다.  Hello 조직의 네트워크 내에 있는 IP 주소에서 hello 응용 프로그램에 액세스 하는 경우 hello MFA 요구 사항에서 사용자가 제외할 수 있습니다.

이러한 기능은 Azure Active Directory Premium 라이선스를 구입한 사용할 수 있는 toocustomers 됩니다.

## <a name="scenario-prerequisites"></a>시나리오 필수 조건
* Azure Active Directory Premium에 대한 라이선스
* 페더레이션 또는 관리되는 Azure Active Directory 테넌트
* 페더레이션된 테넌트가 해당 다단계 인증의 사용 요구

## <a name="configure-per-application-access-rules"></a>응용 프로그램별 액세스 규칙 구성
이 섹션에서는 tooconfigure 응용 프로그램별 액세스 하는 방법을 설명 규칙입니다.

1. Azure AD에 대 한 전역 관리자는 해당 하는 계정을 사용 하 여 Azure 클래식 포털 toohello에 로그인 합니다.
2. Hello 왼쪽된 창에서 선택 **Active Directory**합니다.
3. Hello 디렉터리 탭에서 디렉터리를 선택 합니다.
4. 선택 hello **응용 프로그램** 탭 합니다.
5. 규칙 hello 하 선택 hello 응용 프로그램에 대 한 설정 됩니다.
6. 선택 hello **구성** 탭 합니다.
7. 액세스 규칙 섹션 toohello 아래로 스크롤하십시오. Hello 원하는 액세스 규칙을 선택 합니다.
8. Hello 규칙을 적용할 hello 사용자 지정 합니다.
9. 선택 하 여 hello 정책 설정 **toobe에서 활성화**합니다.

## <a name="understanding-access-rules"></a>액세스 규칙 이해
이 섹션에서는 hello Azure 조건부 응용 프로그램 액세스에서에서 지원 되는 hello 액세스 규칙에 대 한 자세한 설명을 제공 합니다.

### <a name="specifying-hello-users-hello-access-rules-apply-to"></a>지정 하 여 hello 사용자 hello 액세스 규칙에 적용
기본적으로 hello 정책 tooall 사용자 액세스 toohello 응용 프로그램에 적용 됩니다. 그러나 제한할 수도 있습니다 hello 정책 toousers 지정 hello의 구성원 인 보안 그룹입니다. hello **그룹 추가** 단추를 사용 하는 tooselect 하나 또는 액세스 규칙 hello hello 그룹 선택 대화 상자에서 더 많은 그룹에 적용 됩니다. 이 대화 상자에 사용 되는 tooremove 선택 그룹 될 수도 있습니다. Hello 규칙을 선택한 tooapply tooGroups hello 액세스 규칙은만 적용의 지정 된 hello tooone 속한 사용자에 대 한 보안 그룹입니다.

보안 그룹도 명시적으로에서 제외할 수 hello 정책 hello를 선택 하 여 **제외한** 옵션 및 하나 이상의 그룹을 지정 합니다. Hello에 그룹의 구성원 인 사용자 **제외한** 목록 제목 toohello 다단계 인증 요구 사항 됩니다, 해당 hello 액세스 규칙을 적용할 그룹의 멤버인 경우에 합니다.
아래에 표시 된 hello 액세스 규칙 hello 응용 프로그램에 액세스할 때 hello 관리자 그룹 toouse multi-factor authentication에서 모든 사용자가 필요 합니다.

![MFA를 사용하는 조건부 액세스 규칙 설정](./media/active-directory-conditional-access-azuread-connected-apps/conditionalaccess-saas-apps.png)

## <a name="conditional-access-rules-with-mfa"></a>MFA를 사용하는 조건부 액세스 규칙
사용자가를 구성한 경우 hello 사용자별 다단계 인증 기능을 사용 하 여 hello 사용자에 대해이 설정을 hello 응용 프로그램의 다단계 인증 규칙 hello와 결합 합니다. 즉, 사용자별으로 multi-factor authentication에 대해 구성 된 사용자 hello 응용 프로그램 다단계 인증 규칙에서 제외 된 경우에 필요한 tooperform 다단계 인증 됩니다. 다단계 인증 및 사용자별 설정에 대해 자세히 알아보세요.

### <a name="access-rule-options"></a>액세스 규칙 옵션
다음 옵션 hello 지원 됩니다.

* **Multi-factor authentication 필요**: toowhom hello 액세스 규칙 적용 하는 hello 사용자에 적용 정책 hello 하는 hello 응용 프로그램에 액세스 하기 전에 필요한 toocomplete 다단계 인증을 수 있습니다.
* **Multi-factor authentication이 아닐 때 작업 요구**: 사용자는 신뢰할 수 있는 IP 주소에서 오는 필요한 tooperform 다단계 인증 되지 것입니다. hello 신뢰 hello 다단계 인증 설정 페이지에서 IP 주소 범위를 구성할 수 있습니다.
* **회사에 있지 않을 때 액세스 차단**: 신뢰할 수 있는 IP 주소에서 액세스하는 사용자가 차단됩니다. hello 신뢰 hello 다단계 인증 설정 페이지에서 IP 주소 범위를 구성할 수 있습니다.

### <a name="setting-rule-status"></a>규칙 상태 설정
액세스 규칙 상태 hello 규칙을 설정 또는 해제를 허용 합니다. Hello 액세스 규칙이 해제 되어, hello 다단계 인증 요구 사항이 적용 되지 않습니다.

### <a name="access-rule-evaluation"></a>액세스 규칙 평가
사용자가 OAuth 2.0, OpenID Connect, SAML 또는 WS-Federation을 사용하는 페더레이션된 응용 프로그램에 액세스할 때 액세스 규칙이 평가됩니다. 또한 hello OAuth 2.0 및 OpenID Connect 사용 액세스 토큰 새로 고침 토큰 tooacquire 액세스 규칙이 평가 됩니다. 새로 고침 토큰이 사용 될 때 정책 평가가 실패 하면 오류 hello **invalid_grant** 반환 됩니다 hello 사용자에 게 필요한 toore 나타냅니다-toohello 클라이언트를 인증 합니다.

### <a name="configure-federation-services-tooprovide-multi-factor-authentication"></a>페더레이션 서비스 tooprovide multi-factor authentication 구성
페더레이션된 테 넌 트에 대 한 MFA 수행할 수 있습니다 hello 또는 Azure Active Directory에서 온-프레미스 AD FS 서버입니다.

기본적으로 MFA는 Azure Active Directory에서 호스트되는 모든 페이지에 발생합니다. tooconfigure MFA 온-프레미스, hello **– SupportsMFA** 너무 속성을 설정 해야**true** Windows PowerShell 용 hello Azure AD 모듈을 사용 하 여 Azure Active Directory에 있습니다.

hello 다음 예제에서는 어떻게 tooenable 온-프레미스 MFA hello를 사용 하 여 [Set-msoldomainfederationsettings cmdlet](https://msdn.microsoft.com/library/azure/dn194088.aspx) hello contoso.com 테 넌 트에:

    Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true

또한 toosetting이이 플래그를 hello 페더레이션된 테 넌 트 AD FS 인스턴스 해야 tooperform 다단계 인증을 구성 합니다. 에 대 한 hello 지침 [Azure Multi-factor Authentication 온-프레미스 배포](../multi-factor-authentication/multi-factor-authentication-get-started-server.md)합니다.

## <a name="related-articles"></a>관련 문서
* [연결 된 Active Directory tooAzure tooOffice 365 및 기타 응용 프로그램 액세스 보안](active-directory-conditional-access.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)

