---
title: "Azure id 및 액세스 제어를 사용 하 여 개인 데이터 aaaProtect | Microsoft Docs"
description: "개인 데이터를 보호 Azure id 및 액세스 제어 toohelp를 사용 하 여"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a>Azure Active Directory 및 Multi-Factor Authentication: ID 및 액세스 제어를 사용하여 개인 데이터 보호

이 문서 정보 및 Azure Active Directory 및 다단계 인증 보안 기능 및 서비스를 사용 하 여 tooprotect 개인 데이터를 사용할 수 있는 절차를 제공 합니다.

## <a name="scenario"></a>시나리오

Hello 미국에서 본사는 큰 크루즈 회사 hello 지중해, Adriatic, 발트어 바다 뿐 아니라 hello 영국 제도에서 해당 작업 toooffer 여정이 확장 합니다. toosupport 이탈리아를 더 작은 여러 크루즈 줄 획득 이러한 노력 독일, 덴마크 및 hello 영국 

hello 회사 hello 클라우드에서 Microsoft Azure toostore 회사 데이터를 사용합니다. 여기에는 전 세계 고객 기반의 이름, 주소, 전화 번호 및 신용 카드 정보와 같이 식별 가능한 개인 정보가 포함됩니다. 또한 모든 위치에 주소, 전화 번호, 세금 id 번호, 회사 직원에 대 한 의료 보험 정보 등 기존의 인적 자원 정보를 포함 합니다. hello 크루즈 줄에는 현재 및 과거 고객과 개인 정보 tootrack 관계를 포함 하는 보상 및 충성도 프로그램 멤버의 큰 데이터베이스 유지 관리 합니다.

회사 직원 hello 네트워크 hello 회사의 원격 사무실 및 여행사에서 액세스 하는 hello world 주변에 있는 toosome 회사 리소스에 액세스 했습니다.

## <a name="problem-statement"></a>문제 설명

hello 회사 손상 toouse 대 id toogain의 액세스는 침입자에서 고객의 및 직원의 개인 데이터의 hello 개인 정보를 보호 해야 합니다. 또한 확인 해야 합니다 합법적인 사용자가 데이터 toodo 해야 하는 사용자만 제한 되는 액세스 toopersonal 작업 합니다.

## <a name="company-goal"></a>회사 목표

hello 회사의 목표는 tooensure toopersonal 데이터에 액세스 하는 엄격 하 게 제어 합니다. Access toopersonal 데이터를 사용자의 신원을 강력한 인증에서 보호할 수 있다는 반드시 합니다. [최소 권한]에 대 한 정책을 합법적인 사용자가 필요로 하는 액세스 하는 유일한 hello 수준을 갖도록 (https://en.wikipedia.org/wiki/Principle_of_least_privilege)을 적용 해야 합니다.

## <a name="solutions"></a>솔루션

Microsoft Azure 액세스 tooresources 개인 데이터를 포함 하는 사람을 toohelp 회사 제어 id 및 액세스 관리 도구를 제공 합니다.

### <a name="azure-active-directory"></a>Azure Active Directory

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) id를 관리 하 고 다른 온-프레미스 및 다른 클라우드 리소스, 데이터 및 응용 프로그램 tooAzure의 액세스를 제어 합니다. [Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) 개인 데이터와 같은 toocertain 정보에 액세스할 권한이 있는 사용자의 다단계 인증 toominimize hello 수는 데 도움이 됩니다. Toodiscover 수 있기를 제한 하 고 권한 있는 id 및 액세스 tooresources, 및 tooassign 일시적 이며 jit (JUST-IN-TIME) 관리 권한 tooeligible 사용자를 모니터링 합니다. 또한 AAD 관리 권한을 가진 사용자에 대한 정보도 제공합니다.

AAD PIM를 사용 하 여 관련 된 전체 hello 활동은 다음과 같습니다.

- 디렉터리에 대한 Privileged Identity Management 활성화

- 한 눈에 Privileged Identity Management 관리 대시보드 toosee 중요 한 정보를 사용 하 여

- 추가 하거나 영구 또는 적격 관리자 tooeach 역할을 제거 하 여 hello 권한 있는 id (관리자)를 관리 합니다.

- Hello 역할 활성화 설정을 구성합니다.

- 역할 활성화

- 역할 활동 검토

#### <a name="how-do-i-enable-aad-pim"></a>AAD PIM을 사용하도록 설정하려면 어떻게 할까요?

PIM을 사용 하 여 디렉터리에 대 한 toostart 다음 hello지 않습니다:

1. 디렉터리의 전역 관리자로 Azure 포털 toohello에 로그인 합니다.

2. 조직에서 둘 이상의 디렉터리를 경우 hello hello Azure 포털의 상단 오른쪽 모서리에서 사용자 이름을 선택 합니다. Azure AD Privileged Identity Management ´ hello 디렉터리를 선택 합니다.

3. 선택 **더 많은 서비스** hello를 사용 하 여 **필터** Azure AD Privileged Identity Management에 대 한 toosearch 텍스트 상자에 붙여넣습니다.

4. 확인 **Pin toodashboard** 클릭 하 고 **만들기**합니다. hello Privileged Identity Management 응용 프로그램을 엽니다.

Azure AD Privileged Identity Management 설정 되 고 나면 hello 응용 프로그램을 열 때마다 hello 탐색 블레이드를 표시 합니다.

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

AAD PIM 시작에 대한 자세한 내용과 지침은 [Azure AD Privileged Identity Management 시작](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)을 참조하세요.

### <a name="azure-role-based-access-control"></a>Azure 역할 기반 액세스 제어

[Azure 역할 기반 액세스 제어](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) 다단계 인증 hello hello 사용자의 할당 된 역할에 따라 액세스 권한을 부여 함으로써 tooAzure 리소스에 액세스를 관리 하는 (RBAC)는 데 도움이 됩니다. 팀에서 의무를 분리 수 있으며 hello 양의 데이터만 액세스 toousers, 그룹 및 필요 하다는 tooperform 업무 응용 프로그램 권한을 부여할 수 있습니다.

Toousers hello Azure 포털, Azure 명령줄 도구 또는 Azure 관리 Api를 사용 하 여 역할 기반 액세스를 부여할 수 있습니다.

Azure RBAC 기본 사항에 대 한 자세한 내용은 참조 하세요. [hello Azure 포털에서에서 역할 기반 액세스 제어를 시작 합니다.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a>PowerShell을 사용하여 Azure RBAC를 관리하려면 어떻게 할까요?

PowerShell cmdlet toomanage hello 다음 관리 작업을 포함 하 여 Azure RBAC를 사용할 수 있습니다.

- 역할 나열

- 액세스 권한이 있는 사용자 확인

- 액세스 권한 부여

- 액세스 권한 제거

- 사용자 지정 역할 만들기

- 리소스 공급자에 대한 작업 가져오기

- 사용자 지정 역할 수정

- 사용자 지정 역할 삭제

- 사용자 지정 역할 나열

Toomanage PowerShell과 함께 Azure RBAC를 확인 하려면 어떻게에 대 한 지침은 [Azure powershell 관리 역할 기반 액세스](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell)합니다.

### <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication

[Azure Multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA)은 간단한 로그인 프로세스에 대 한 사용자 요구를 충족 하면서 보호 액세스 toodata 및 응용 프로그램을 사용 하는 2 단계 확인 솔루션입니다. 전화 통화, 문자 메시지 또는 모바일 앱 확인과 같은 다양한 확인 방법을 통해 강력한 인증을 전달합니다.

toofirst 해야 toodeploy MFA에서 Azure 클라우드 hello 사용 하도록 설정 하 고 다음 사용자에 대 한 2 단계 인증을 켭니다.

#### <a name="how-do-i-enable-azure-toouse-mfa"></a>Azure toouse MFA를 어떻게 사용 합니까?

사용자에 게 Azure Multi-factor Authentication을 포함 하는 라이선스 있으면 Azure MFA에 toodo tooturn 해야 하는 일은 없습니다. 그렇지 않으면 디렉터리에 toocreate Multi-factor Auth 공급자를 사용 해야 합니다. toodo이를 다음이 단계를 수행 합니다.

1. 선택 **Active Directory** hello Azure 클래식 포털 (관리자 권한으로 로그온)에서.

2. **Multi-Factor Authentication 공급자**를 선택합니다.

3. **새로 만들기**를 선택한 다음 **App Services** 아래에서 **Multi-Factor Auth 공급자**를 선택합니다.

4. **빠른 생성**을 선택합니다.

5. Hello 이름 필드에서 작성 (인증 단위 또는 활성화 된 사용자별) 사용 모델을 선택 하십시오.

6. MFA 공급자는 hello와 연관 된 디렉터리를 지정 합니다.

7. Hello 클릭 **만들기** 단추입니다.

![](media/protect-personal-data-identity-access-controls/quick-create.png)

자세한 방법에 대 한 toomanage Multi-factor Auth 공급자를 사용 하 여 참조 [Azure Multi-factor Auth 공급자 시작 합니다.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a>사용자에 대한 2단계 인증을 설정하려면 어떻게 할까요?

모든 기호 기능에 대 한 2 단계 인증을 적용할 수 있습니다 또는 특정 조건을 만족할 경우에 조건부 액세스 정책을 toorequire 2 단계 인증을 만들 수 있습니다.

Azure MFA 사용자 상태를 변경 하 여 hello에 대 한 2 단계 인증을 요구 한 기존의 접근 방식은입니다. 사용 하도록 설정 하면 모든 hello 사용자가 로그인 할 때마다 동일한 요구 사항을 tooperform 2 단계 인증을 hello 합니다. 사용자가 사용하도록 설정되면 해당 사용자에게 영향을 줄 수 있는 모든 조건부 액세스 정책이 무시됩니다.

조건부 액세스 정책을 사용하여 Azure MFA를 사용하도록 설정하는 것은 2단계 인증을 요구하는 것보다 더 유연한 방법입니다. Toogroups 뿐만 아니라 개별 사용자에 게 적용 되는 조건부 액세스 정책을 만들 수 있습니다. 위험 수준이 높은 그룹에는 위험 수준이 낮은 그룹보다 더 많은 제한이 제공되거나 위험 수준이 높은 클라우드 앱에만 2단계 인증이 요구되고 위험 수준이 낮은 그룹에는 건너뛸 수 있습니다. 그러나 조건부 액세스는 Azure Active Directory의 유료 기능입니다.

사용자 상태를 변경 하 여 MFA tooenable 다음 hello지 않습니다.

1. 관리자 권한으로 Azure 포털 toohello에 로그인 합니다.
2. 너무 이동**Azure Active Directory \> 사용자 및 그룹 \> 모든 사용자에 게**합니다.
3. **Multi-Factor Authentication**을 선택합니다.
4. Azure MFA에 대 한 tooenable 되도록 찾기 hello 사용자입니다. Toochange 할 수 있습니다 hello hello 위쪽에는 보기입니다.
5. Hello 상자 다음 toohello 사용자의 이름을 확인 하십시오.
6. 오른쪽의 빠른 단계에서 사용 되는 hello, 선택 **사용**합니다.

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. Hello 팝업 창이 열리면 선택한 내용을 확인 합니다.  사용자가 MFA 활성화 된 사람 묻습니다 tooregister hello 다음 번에 로그인 합니다.

조건부 액세스 정책 사용 하 여 Azure MFA tooenable 다음 hello지 않습니다.

1. 관리자 권한으로 Azure 포털 toohello에 로그인 합니다.

2. 너무 이동**Azure Active Directory \> 조건부 액세스**합니다.

3. **새 정책**을 선택합니다.

4. **할당** 아래에서 **사용자 및 그룹**을 선택합니다. 사용 하 여 hello **Include** 및 **제외** 탭 toospecify 있는 사용자 및 그룹 hello 정책에 의해 관리 됩니다.

5. **할당** 아래에서 **클라우드 앱**을 선택합니다. 너무 선택**모든 클라우드 앱이 포함**합니다.
6.  **액세스 제어** 아래에서 **허용**을 선택합니다. **다단계 인증 필요**를 선택합니다.
7.  설정 **정책 사용** 너무**에** 선택한 후 **저장**합니다.

에 대 한 내용은 사기 행위 경고를 tooconfigure Azure MFA 설정 tooset 일회성 바이패스를 만든 사용자 지정 음성 메시지를 사용 하 여, 캐싱을 구성 하 여, 신뢰할 수 있는 Ip를 지정, 앱 암호를 만들, 선택 및 사용자가 신뢰 하는 장치에 대 한 MFA를 기억 하는 것을 사용 하도록 설정 참조 확인 방법을 [Azure Multi-factor Authentication 설정 구성 합니다.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)

## <a name="next-steps"></a>다음 단계

- [Azure AD에서 권한 있는 액세스 보안](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [Azure Multi-Factor Authentication에 대한 질문과 대답](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [역할 기반 액세스 제어 문제 해결](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [Azure Active Directory ID 보호](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
