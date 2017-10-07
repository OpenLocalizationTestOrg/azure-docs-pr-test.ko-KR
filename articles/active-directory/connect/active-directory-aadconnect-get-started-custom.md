---
title: "Azure AD Connect: 사용자 지정 설치 | Microsoft Docs"
description: "이 문서에는 Azure AD Connect에 대 한 사용자 지정 설치 옵션 hello 자세히 설명합니다. 이러한 지침은 tooinstall Azure AD Connect 통해 Active Directory를 사용 합니다."
services: active-directory
keywords: "Azure AD Connect의 정의, Active Directory 설치, Azure AD에 대한 필수 구성 요소"
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 6d42fb79-d9cf-48da-8445-f482c4c536af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: c49724fab78c5a1688662043f69506fff6f82104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-installation-of-azure-ad-connect"></a>Azure AD Connect의 사용자 지정 설치
Azure AD Connect **사용자 지정 설정** hello 설치에 대 한 추가 옵션을 원할 때 사용 됩니다. 여러 포리스트에 있는 경우 또는 hello 빠른 설치에 포함 하지 않는 tooconfigure 선택적 기능이 필요한 경우 사용 됩니다. 여기서 hello 모든 경우에 사용 [ **express 설치** ](active-directory-aadconnect-get-started-express.md) 또는 배포 토폴로지 옵션 충족 하지 않습니다.

Azure AD Connect 설치를 시작 하기 전에 있어야 너무[Azure AD Connect 다운로드](http://go.microsoft.com/fwlink/?LinkId=615771) 및 전체 hello 필수 단계를 [Azure AD Connect: 하드웨어 및 필수 구성 요소](active-directory-aadconnect-prerequisites.md)합니다. 또한 [Azure AD Connect 계정 및 사용 권한](active-directory-aadconnect-accounts-permissions.md)에 설명된 대로 사용할 수 있는 계정이 있어야 합니다.

사용자 지정된 설정이 토폴로지에 일치 하지 않는 경우 예를 들어 tooupgrade DirSync 참조 [관련 설명서](#related-documentation) 다른 시나리오에 대 한 합니다.

## <a name="custom-settings-installation-of-azure-ad-connect"></a>Azure AD Connect의 사용자 지정 설정 설치
### <a name="express-settings"></a>Express 설정
이 페이지에서 클릭 **사용자 지정** toostart 사용자 지정된 설정 설치 합니다.

### <a name="install-required-components"></a>필요한 구성 요소 설치
Hello 동기화 서비스를 설치에 hello 옵션 구성 섹션을 선택 취소 된 채로 두고 Azure AD Connect 모든 항목을 자동으로 설정 합니다. 한 SQL Server 2012 Express LocalDB 인스턴스를 설정 하 고 hello 적절 한 그룹을 만들고 사용 권한을 할당 합니다. Toochange hello 기본값을 원할 경우 hello 다음 사용할 수 있는 테이블 toounderstand hello 옵션 구성 옵션을 사용할 수 있습니다.

![필수 구성 요소](./media/active-directory-aadconnect-get-started-custom/requiredcomponents.png)

| 선택적 구성 | 설명 |
| --- | --- |
| 기존 SQL Server 사용 |Toospecify hello SQL Server 이름과 인스턴스 이름을 hello 있습니다. 싶다는 의사를 toouse 데이터베이스 서버에 이미 있는 경우이 옵션을 선택 합니다. Hello 인스턴스 이름 뒤에 쉼표 및 포트 번호를 입력 **인스턴스 이름을** SQL Server에 없는 경우 브라우저를 사용 합니다. |
| 기존 서비스 계정 사용 |기본적으로 Azure AD Connect 동기화 서비스 toouse hello에 대 한 가상 서비스 계정을 사용합니다. Toouse 필요를 원격 SQL server를 사용 하거나 인증을 요구 하는 프록시를 사용 하는 경우는 **관리 서비스 계정** hello 도메인의 서비스 계정을 사용 하 고 hello 암호를 알고 있습니다. 이 경우 hello 계정 toouse를 입력 합니다. Hello 설치를 실행 하는 hello 사용자 이므로 sql에서 SA hello 서비스 계정에 대 한 로그인을 만들 수 있는지 확인 합니다. [Azure AD Connect 계정 및 사용 권한](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) |
| 사용자 지정 동기화 그룹 지정 |기본적으로 Azure AD Connect hello 동기화 서비스를 설치 하는 경우 4 명의 그룹 toohello 로컬 서버를 만듭니다. 이러한 그룹은: 관리자 그룹, Operators 그룹, 찾아보기 그룹 및 hello 암호 다시 설정 그룹입니다. 여기서 사용자의 고유한 그룹을 지정할 수 있습니다. hello 그룹 hello 서버에서 로컬 이어야 하며 hello 도메인에서 찾을 수 없습니다. |

### <a name="user-sign-in"></a>사용자 로그인
Tooselect 묻는 hello 필수 구성 요소를 설치한 후 사용자 로그온 방법 단일. 다음 표에서 hello hello 사용 가능한 옵션에 대 한 간단한 설명을 제공 합니다. 참조에 대 한 전체 설명은 hello 로그인 방법이, [사용자 로그인](active-directory-aadconnect-user-signin.md)합니다.

![사용자 로그인](./media/active-directory-aadconnect-get-started-custom/usersignin2.png)

| SSO(Single Sign-On) 옵션 | 설명 |
| --- | --- |
| 암호 동기화 |사용자가 수 toosign hello의 온-프레미스 네트워크를 사용 하는 동일한 암호를 사용 하 여 Office 365와 같은 tooMicrosoft 클라우드 서비스에 있습니다. hello 사용자 암호는 암호 해시로 동기화 된 tooAzure AD 고 hello 클라우드에서 인증이 됩니다. 자세한 내용은 [암호 동기화](active-directory-aadconnectsync-implement-password-synchronization.md)를 참조하세요. |
|통과 인증(미리 보기)|사용자가 수 toosign hello의 온-프레미스 네트워크를 사용 하는 동일한 암호를 사용 하 여 Office 365와 같은 tooMicrosoft 클라우드 서비스에 있습니다.  hello 사용자 암호 toohello 온-프레미스 Active Directory 컨트롤러 toobe 유효성을 검사를 통해 전달 됩니다.
| AD FS로 페더레이션 |사용자가 수 toosign hello의 온-프레미스 네트워크를 사용 하는 동일한 암호를 사용 하 여 Office 365와 같은 tooMicrosoft 클라우드 서비스에 있습니다.  hello 사용자 리디렉션됩니다 tootheir 온-프레미스에서 AD FS 인스턴스 toosign 및 인증 온-프레미스에 발생 합니다. |
| 구성하지 않음 |기능이 설치 및 구성되지 않았습니다. 이미 타사 페더레이션 서버 또는 다른 기존 솔루션이 있는 경우 이 옵션을 선택합니다. |
|Single Sign-On을 사용하도록 설정|이 옵션을 암호 동기화와 통과 인증을 사용할 수 하며 hello 회사 네트워크에서 데스크톱 사용자에 대 한 단일 로그인 환경을 제공 합니다.  자세한 내용은 [Single sign-on](active-directory-aadconnect-sso.md)을 참조하세요. </br>참고 AD FS 고객에 대 한이 옵션이 제공 되지 않습니다 AD FS 이미 제공 hello 동일한 수준의 single sign에 때문에 있습니다.</br>(hello에 설명 해제 되지 않으면 같은 시간)
|로그인 옵션|이 옵션을 암호 동기화 고객에 대 한 ´ ï ´ 하며 hello 회사 네트워크에서 데스크톱 사용자에 대 한 단일 로그인 환경을 제공 합니다.  </br>자세한 내용은 [Single sign-on](active-directory-aadconnect-sso.md)을 참조하세요. </br>참고 AD FS 고객에 대 한이 옵션이 제공 되지 않습니다 AD FS 이미 제공 hello 동일한 수준의 single sign에 때문에 있습니다.


### <a name="connect-tooazure-ad"></a>TooAzure AD 연결
Hello 연결 tooAzure AD 화면에 전역 관리자 계정 및 암호를 입력 합니다. 선택한 경우 **AD FS와의 페더레이션을** hello 이전 페이지에서 서명을 하지 않는 tooenable 페더레이션에 대 한 도메인 계정을 사용 하 여 계획 합니다. toouse hello 기본 계정을 권장 사항은 **onmicrosoft.com** Azure AD 디렉터리와 함께 제공 되는 도메인입니다.

이 계정은 toocreate에만 사용 되는 서비스 계정을 Azure AD에서 형식이 hello 마법사가 완료 된 후에 사용 되지 않습니다.  
![사용자 로그인](./media/active-directory-aadconnect-get-started-custom/connectaad.png)

전역 관리자 계정을 사용 하도록 설정 하는 MFA가 tooprovide hello에 암호를 다시 hello 로그인 팝업 및 전체 hello MFA 챌린지 할 수 있습니다. 확인 코드 또는 전화 통화를 제공 하는 hello 챌린지 될 수 있습니다.  
![사용자 로그인 MFA](./media/active-directory-aadconnect-get-started-custom/connectaadmfa.png)

hello 전역 관리자 계정에가 수 [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md) 사용 하도록 설정 합니다.

오류가 발생하고 연결에 문제가 있는 경우 [연결 문제 해결](active-directory-aadconnect-troubleshoot-connectivity.md)을 참조하세요.

## <a name="pages-under-hello-section-sync"></a>동기화 hello 섹션 아래에 있는 페이지

### <a name="connect-your-directories"></a>디렉터리에 연결
tooconnect tooyour Active Directory 도메인 서비스, Azure AD Connect hello 포리스트 이름과 충분 한 권한이 있는 계정의 자격 증명이 필요합니다.

![연결 디렉터리](./media/active-directory-aadconnect-get-started-custom/connectdir01.png)

Hello 포리스트 이름을 입력 하 고 클릭 한 후 **디렉터리 추가**, 팝업 대화 상자에 표시 되 고 hello 다음 옵션을 표시 합니다.

| 옵션 | 설명 |
| --- | --- |
| 기존 계정 사용 | 기존 AD DS tooprovide 계정이 toobe toohello AD 포리스트 디렉터리 동기화 중에 연결 하기 위한 Azure AD Connect를 사용 하려면이 옵션을 선택 합니다. Hello 도메인 부분, 즉 FABRIKAM\syncuser 또는 fabrikam.com\syncuser NetBios 또는 FQDN 형식으로 입력할 수 있습니다. 이 계정은 hello 기본 읽기 권한만 필요 하므로 일반 사용자 계정 수 있습니다. 그러나 시나리오에 따라 더 많은 사용 권한이 할 수 있습니다. 자세한 내용은 [Azure AD Connect 계정 및 권한](active-directory-aadconnect-accounts-permissions.md#create-the-ad-ds-account)을 참조하세요. |
| 새 계정 만들기 | Azure AD Connect 마법사 toocreate hello AD DS 계정 Azure AD connect 디렉터리 동기화 동안 toohello AD 포리스트를 연결 하기 위해 필요한 경우이 옵션을 선택 합니다. 이 옵션을 선택 하는 엔터프라이즈 관리자 계정에 대 한 hello 사용자 이름 및 암호를 입력 합니다. hello 엔터프라이즈 관리자 계정을 제공 사용 하 여 Azure AD Connect 마법사 toocreate hello 요구 하므로 AD DS 계정. Hello 도메인 부분, 즉 FABRIKAM\administrator 또는 fabrikam.com\administrator NetBios 또는 FQDN 형식으로 입력할 수 있습니다. |

![연결 디렉터리](./media/active-directory-aadconnect-get-started-custom/connectdir02.png)


### <a name="azure-ad-sign-in-configuration"></a>Azure AD 로그인 구성
이 페이지에서는 tooreview hello UPN 도메인에 온-프레미스 AD DS와 Azure AD에서 확인 되었습니다. 이 페이지에 대 한 hello userPrincipalName tooconfigure hello 특성 toouse에서는.

![확인되지 않은 도메인](./media/active-directory-aadconnect-get-started-custom/aadsigninconfig.png)  
**추가되지 않음** 및 **확인되지 않음**으로 표시된 모든 도메인을 검토합니다. 사용한 해당 도메인을 Azure AD에서 확인하도록 합니다. 도메인을 확인 한 경우 hello 새로 고침 기호를 클릭 합니다. 자세한 내용은 참조 [추가 하 고 hello 도메인 확인](../active-directory-add-domain.md)

**UserPrincipalName** -hello 특성 userPrincipalName hello 특성 사용자가 tooAzure AD 및 Office 365에 로그인 할 때 사용 됩니다. hello 도메인으로 알려진 hello UPN 접미사를 사용, hello 사용자가 동기화 하기 전에 Azure AD에서 확인 해야 합니다. Tookeep hello 기본 특성 userPrincipalName를 사용 하는 것이 좋습니다. 이 특성이 라우팅할 수 없는 않으며를 확인할 수 없어서 경우 가능한 tooselect를은 다른 특성입니다. Hello 로그인 id입니다. 보유 하는 hello 특성으로 예를 들어 전자 메일을 선택할 수 있습니다. userPrincipalName 이외의 다른 특성을 사용하는 것을 **대체 ID**라고 합니다. hello 대체 ID 특성 값을 표준 RFC822 hello를 따라야 합니다. 대체 ID는 암호 동기화 및 페더레이션과 함께 사용할 수 있습니다.

>[!NOTE]
> 통과 인증을 사용 하도록 설정 하면 순서 toocontinue hello 마법사를 통해 확인 된 도메인을 하나 이상 있어야 합니다.

> [!WARNING]
> 대체 ID를 사용하면 모든 Office 365 워크로드 부하와 호환되지 않습니다. 자세한 내용은 참조 너무[대체 로그인 ID 구성](https://technet.microsoft.com/library/dn659436.aspx)합니다.
>
>

### <a name="domain-and-ou-filtering"></a>도메인 및 OU 필터링
기본적으로 모든 도메인 및 OU가 동기화됩니다. 일부 도메인 또는 Ou toosynchronize tooAzure AD 하지 않을 경우 이러한 도메인 및 Ou를 선택 취소할 수 있습니다.  
![DomainOU 필터링](./media/active-directory-aadconnect-get-started-custom/domainoufiltering.png)  
Hello 마법사의이 페이지는 도메인 및 OU 기반 필터링 구성입니다. Toomake 변경 하려는 경우 다음 참조 [도메인 기반 필터링](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) 및 [ou 기반 필터링](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) 이러한 변경을 수행 하기 전에 합니다. 일부 Ou hello 기능에 필수적인 선택 되지 않은 아니어야 합니다.

Azure AD Connect 버전 1.1.524.0 미만에서 OU 기반 필터링을 사용하면 기본적으로 나중에 추가되는 새 OU가 동기화됩니다. 새 hello 동작을 원하는 경우 Ou 일치 하지 않아 해야 다음 hello 마법사 완료 된 후에 구성할 수 [ou 기반 필터링](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering)합니다. Azure AD Connect 버전 1.1.524.0 또는 후에 새 Ou toobe를 동기화 하려는 지 여부를 나타낼 수 있습니다.

Toouse 하려는 경우 [그룹 기반 필터링](#sync-filtering-based-on-groups), 다음 hello 그룹과 hello OU가 포함 되어 있고 OU 필터링 된 필터링 되지 있는지를 확인 합니다. OU 필터링은 그룹 기반 필터링 전에 평가됩니다.

일부 도메인 toofirewall 제한 인해 연결할 수 없는 가능한 이기도 합니다. 이러한 도메인은 기본적으로 선택 취소되며 경고가 표시됩니다.  
![연결할 수 없는 도메인](./media/active-directory-aadconnect-get-started-custom/unreachable.png)  
이 경고를 표시 하는 경우 이러한 도메인에 실제로 연결할 수 없는 hello 경고 예상 되 고 있는지 확인 합니다.

### <a name="uniquely-identifying-your-users"></a>사용자를 고유하게 식별

#### <a name="select-how-users-should-be-identified-in-your-on-premises-directories"></a>온-프레미스 디렉터리에서 사용자를 식별하는 방법 선택
hello 포리스트 기능 간에 일치 하면 AD DS 포리스트의 사용자가 Azure AD에 표시 되는 방법을 toodefine. 사용자는 포리스트 전반에 걸쳐 한번만 표시할 수 있거나 활성화된 계정과 비활성화된 계정의 조합으로 이루어집니다. hello 사용자 연락처 일부 포리스트에도 표시 될 수 있습니다.

![고유한](./media/active-directory-aadconnect-get-started-custom/unique.png)

| 설정 | 설명 |
| --- | --- |
| [사용자는 모든 포리스트에 걸쳐 한번만 표시됩니다](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |모든 사용자가 Azure AD에 개별 개체로 만들어집니다. hello 개체는 hello 메타 버스에 조인 되지 않습니다. |
| [Mail 특성](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |이 옵션 같은 서로 다른 포리스트에 값 hello hello 메일 특성에 있는 경우 사용자 및 연락처를 조인 합니다. 연락처가 GALSync를 사용하여 생성 된 경우 이 옵션을 사용합니다. 이 옵션을 선택 하면 해당 메일 특성 채워집니다 되지 사용자 개체는 동기화 된 tooAzure AD 되지 않습니다. |
| [ObjectSID 및 msExchangeMasterAccountSID/ msRTCSIP-OriginatorSid](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |이 옵션은 계정 포리스트에서 활성화된 사용자를 리소스 포리스트에서 비활성화된 사용자와 조인합니다. Exchange의 경우 이 구성을 연결된 된 사서함이라고 합니다. Lync만 사용 하 고 Exchange 리소스 포리스트의 hello에 없으면이 옵션을 사용할 수도 있습니다. |
| sAMAccountName 및 MailNickName |이 옵션은가 예상된 hello 로그인 ID hello 사용자를 찾을 수에 대 한 특성에 조인 합니다. |
| 특정 특성 |이 옵션 tooselect을 사용 하면 사용자 고유의 특성입니다. 이 옵션을 선택 하면 사용자 개체 (선택된) 속성을 가진 입력 되지 않습니다는 동기화 된 tooAzure AD 되지 않습니다. **제한 사항:** 있는지 toopick 이미 hello 메타 버스에서 찾을 수 있는 특성을 확인 합니다. (Hello 메타 버스)에 없는 사용자 지정 특성을 선택 하면 hello를 완료할 수 없습니다. |

#### <a name="select-how-users-should-be-identified-with-azure-ad---source-anchor"></a>Azure AD로 사용자를 식별하는 방법 선택 - 원본 앵커
hello sourceAnchor 특성은 사용자 개체의 hello 수명 동안 변경할 수 없는 특성. 것 hello 기본 키를 Azure AD에서 hello 사용자와 hello 온-프레미스 사용자를 연결 합니다.

| 설정 | 설명 |
| --- | --- |
| Azure 내 hello 원본 앵커를 관리할 수 있도록 | Azure AD toopick hello 특성을 원하는 경우이 옵션을 선택 합니다. 이 옵션을 선택 하는 경우 Azure AD Connect 마법사 문서 섹션에서 설명 하는 hello sourceAnchor 특성 선택 논리를 적용 하는 [Azure AD Connect: 개념-게스트가 ConsistencyGuid sourceAnchor로 사용 하 여 디자인](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor)합니다. hello 마법사는 사용자 지정 설치 완료 후 hello 원본 앵커 특성으로 사용할 특성 선택 않은 알려 줍니다. |
| 특정 특성 | Toospecify hello sourceAnchor 특성으로 기존 AD 특성을 원하는 경우이 옵션을 선택 합니다. |

Hello 특성을 변경할 수 없으므로, 좋은 특성 toouse 계획 해야 합니다. 좋은 후보는 objectGUID입니다. 이 특성 hello 사용자 계정 포리스트/도메인 간에 이동 하지 않는 한 변경 되지 않습니다. 계정 포리스트 간에 이동 하는 위치는 다중 포리스트 환경에서 다른 특성 해야 사용할 hello employeeID 사용 하 여 특성 등. 결혼을 하거나 할당이 변경될 때 바뀔 수 있는 특성을 피하십시오. @-sign와 함께 특성을 사용할 수 없으므로 email 및 userPrincipalName을 사용할 수 없습니다. hello 특성은 대/소문자 구분도 만들어지므로 포리스트 간에 개체를 이동 하면 확인 되었는지 toopreserve hello 위/소문자로 변환 합니다. 이진 특성은 Base64로 인코딩되지만 다른 특성 유형은 인코딩되지 않은 상태로 남아 있습니다. 페더레이션 시나리오 및 일부 Azure AD 인터페이스에서는 이 특성을 immutableID라고도 합니다. Hello에 hello 원본 앵커에 대 한 자세한 내용은 있습니다 [디자인 개념](active-directory-aadconnect-design-concepts.md#sourceanchor)합니다.

### <a name="sync-filtering-based-on-groups"></a>그룹에 따라 동기화 필터링
그룹 기능을 필터링 하는 hello 파일럿에 대 한 개체의 작은 하위 집합만 toosync를 허용 합니다. 이 기능 toouse, 온-프레미스 Active Directory에이 목적을 위해 그룹을 만듭니다. 사용자와 직접 구성원으로 동기화 된 tooAzure AD 되어야 하는 그룹을 추가 합니다. 나중에 추가 하 고 Azure AD에 존재 해야 하는 개체의 사용자가 toothis 그룹 toomaintain hello 목록을 제거할 수 있습니다. Toosynchronize 원하는 모든 개체에 hello 그룹의 직접 구성원 여야 합니다. 사용자, 그룹, 연락처 및 컴퓨터/장치는 모두 직접 구성원이어야 합니다. 중첩된 그룹 구성원은 확인되지 않습니다. 자체 전용 hello 그룹 멤버 추가 됨에 따라 그룹을 추가할 때 및 멤버가 아닌 합니다.

![동기화 필터링](./media/active-directory-aadconnect-get-started-custom/filter2.png)

> [!WARNING]
> 이 기능은 원하는 toosupport 파일럿 배포에 설명 합니다. 본격적인 프로덕션 배포에 사용하지 마십시오.
>
>

완전 한 프로덕션 배포에서는 모든 개체 toosynchronize와 단일 그룹 toobe 하드 toomaintain을 것입니다. 에 hello 메서드 중 하나를 사용 해야 대신 [구성 필터링](active-directory-aadconnectsync-configure-filtering.md)합니다.

### <a name="optional-features"></a>선택적 기능
이 화면에서는 tooselect hello 선택적 기능을 대 한 특정 시나리오에 있습니다.

![선택적 기능](./media/active-directory-aadconnect-get-started-custom/optional.png)

> [!WARNING]
> DirSync 또는 Azure AD Sync 활성 현재 있는 경우 Azure AD Connect의 hello 쓰기 저장 기능을 활성화 하지 마십시오.
>
>

| 선택적 기능 | 설명 |
| --- | --- |
| Exchange 하이브리드 배포 |hello Exchange 하이브리드 배포 기능을 사용 하면 Exchange 사서함의 공존 hello에 대 한 온-프레미스와 Office 365에서 합니다. Azure AD Connect에서는 [특성](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) 의 특정 집합을 Azure AD에서 온-프레미스 디렉터리로 다시 동기화합니다. |
| Exchange 메일 공용 폴더 | hello Exchange 메일에 대 한 공용 폴더 기능은 온-프레미스 Active Directory tooAzure AD에서에서 toosynchronize 메일 사용이 가능한 공용 폴더 개체입니다. |
| Azure AD 앱 및 특성 필터링 |Azure AD 앱 및 특성 필터링을 사용 하면 hello 동기화 된 특성 집합을 맞출 수 있습니다. 이 옵션을 두 개 더 많은 구성 페이지 toohello 마법사를 추가 합니다. 자세한 내용은 [Azure AD 앱 및 특성 필터링](#azure-ad-app-and-attribute-filtering)을 참조하세요. |
| 암호 동기화 |Hello 로그인 솔루션으로 페더레이션을 선택한 경우이 옵션을 사용할 수 있습니다. 암호 동기화는 백업 옵션으로 사용할 수 있습니다. 자세한 내용은 [암호 동기화](active-directory-aadconnectsync-implement-password-synchronization.md)를 참조하세요. </br></br>통과 인증을 선택한 경우이 옵션이 기본 tooensure 지원 하기 때문에 레거시 클라이언트 백업 옵션으로으로 사용 됩니다. 자세한 내용은 [암호 동기화](active-directory-aadconnectsync-implement-password-synchronization.md)를 참조하세요.|
| 비밀번호 쓰기 저장 |암호 쓰기 저장을 사용 하면 Azure AD에서 발생 된 암호 변경이 다시 쓰여집니다 tooyour 온-프레미스 디렉터리. 자세한 내용은 [암호 관리 시작](../active-directory-passwords-getting-started.md)을 참조하세요. |
| 그룹 쓰기 저장 |Hello를 사용 하는 경우 **Office 365 그룹** 기능, 다음 이러한 그룹을 나타내는 온-프레미스 Active Directory에서 사용할 수 있습니다. 이 옵션은 Exchange가 온-프레미스 Active Directory에 있는 경우 사용할 수 있습니다. 자세한 내용은 [그룹 쓰기 저장](active-directory-aadconnect-feature-preview.md#group-writeback)을 참조하세요. |
| 장치 쓰기 저장 |있습니다 toowriteback 장치 개체가 Azure AD tooyour 온-프레미스에 조건부 액세스 시나리오에 대 한 Active Directory. 자세한 내용은 [Azure AD Connect에서 장치 쓰기 저장 사용](active-directory-aadconnect-feature-device-writeback.md)을 참조하세요. |
| 디렉터리 확장 특성 동기화 |디렉터리 확장 특성 동기화를 활성화 하 여 지정 된 특성에 동기화 된 tooAzure AD 됩니다. 자세한 내용은 [디렉터리 확장](active-directory-aadconnectsync-feature-directory-extensions.md)을 참조하세요. |

### <a name="azure-ad-app-and-attribute-filtering"></a>Azure AD 앱 및 특성 필터링
하려는 경우 toolimit 어떤 특성 toosynchronize tooAzure AD를 사용 하는 서비스를 선택 하 여 다음 시작 합니다. 이 페이지에서 구성을 변경 하는 경우 새 서비스는 hello 설치 마법사를 다시 실행 하 여 명시적으로 선택한 toobe에 있습니다.

![앱의 선택적 기능](./media/active-directory-aadconnect-get-started-custom/azureadapps2.png)

Hello 이전 단계에서 선택한 hello 서비스에 따라,이 페이지는 동기화 되는 모든 특성이 표시 됩니다. 이 목록은 동기화된 모든 개체 형식의 조합입니다. 가 없을 경우 toonot 필요한 몇 가지 특정 특성 동기화 특성을 선택 취소할 수 있습니다.

![특성의 선택적 기능](./media/active-directory-aadconnect-get-started-custom/azureadattributes2.png)

> [!WARNING]
> 특성을 제거하면 기능에 영향을 줄 수 있습니다. 모범 사례 및 권장 사항은 [동기화된 특성](active-directory-aadconnectsync-attributes-synchronized.md#attributes-to-synchronize)을 참조하세요.
>
>

### <a name="directory-extension-attribute-sync"></a>디렉터리 확장 특성 동기화
Azure AD의 조직 또는 Active Directory의 다른 특성으로 추가 하는 사용자 지정 특성으로 hello 스키마를 확장할 수 있습니다. toouse이이 기능을 선택 **디렉터리 확장 특성 동기화** hello에 **선택적 기능** 페이지. 이 페이지에 더 많은 특성 toosync를 선택할 수 있습니다.

![디렉터리 확장](./media/active-directory-aadconnect-get-started-custom/extension2.png)

자세한 내용은 [디렉터리 확장](active-directory-aadconnectsync-feature-directory-extensions.md)을 참조하세요.

### <a name="enabling-single-sign-on-sso"></a>SSO(Single Sign-On) 사용하도록 설정
암호 동기화 또는 통과 인증을 사용 하 여 single sign on 사용 하기 위해 구성 하는 것은 하나만 필요 toocomplete 한 번 동기화 된 tooAzure AD 되는 각 포리스트에 대 한 간단 합니다. 구성은 다음과 같이 두 단계로 이루어집니다.

1.  온-프레미스 Active Directory에서 hello 필요한 컴퓨터 계정을 만듭니다.
2.  단일 toosupport 로그온 hello 클라이언트 컴퓨터의 hello 인트라넷 영역을 구성 합니다.

#### <a name="create-hello-computer-account-in-active-directory"></a>Active Directory에 hello 컴퓨터 계정 만들기
Azure AD Connect에 추가 된 각 포리스트에 대 한 각 포리스트에 hello 컴퓨터 계정을 만들 수 있도록 toosupply 도메인 관리자 자격 증명이 필요 합니다. hello 자격 증명이 사용 되는 toocreate hello 계정만 및 저장 되거나 다른 작업에 사용 됩니다. Hello에 hello 자격 증명을 추가 하면 **단일 사용 로그온** 페이지와 같이 hello Azure AD Connect 마법사:

![Single Sign-On을 사용하도록 설정](./media/active-directory-aadconnect-get-started-custom/enablesso.png)

>[!NOTE]
>Toouse Single sign-on 해당 포리스트의 사용 하지 않을 경우 특정 포리스트에 건너뛸 수 있습니다.

#### <a name="configure-hello-intranet-zone-for-client-machines"></a>클라이언트 컴퓨터에 대 한 hello 인트라넷 영역 구성
tooensure hello 클라이언트 로그인 hello 인트라넷에 자동으로 영역 하는 두 개의 Url hello 인트라넷 영역에 포함 되어 있는지 tooensure가 필요 합니다. 이렇게 하면 해당 hello 도메인에 가입 된 컴퓨터에 자동으로 회사 네트워크에 연결 된 toohello 때 AD는 Kerberos 티켓 tooAzure 보냅니다.
에 컴퓨터에 hello 그룹 정책 관리 도구입니다.

1.  Hello open 그룹 정책 관리 도구
2.  사용자가 적용 된 tooall 될 hello 그룹 정책을 편집 합니다. 예를 들어 hello 기본 도메인 정책입니다.
3.  너무 이동**사용자 구성 \ 관리 템플릿 \ Components\Internet 보게 제어 Panel\Security 페이지** 선택 **사이트 할당 목록 tooZone** hello 이미지당 아래 합니다.
4.  Hello 정책을 사용 하도록 설정 하 고 hello 다음 hello 대화 상자에서 두 개의 항목을 입력 합니다.

        Value: `https://autologon.microsoftazuread-sso.com`  
        Data: 1  
        Value: `https://aadg.windows.net.nsatc.net`  
        Data: 1

5.  비슷한 toohello 다음과 같아야 합니다.  
![인트라넷 영역](./media/active-directory-aadconnect-get-started-custom/sitezone.png)

6.  **확인**을 두 번 클릭합니다.

## <a name="configuring-federation-with-ad-fs"></a>AD FS로 페더레이션 구성
Azure AD Connect를 사용하여 AD FS를 구성하는 것은 단 몇 번의 클릭으로 간단합니다. hello 다음 hello 구성 하기 전에 필요 합니다.

* 원격 관리를 사용 하도록 설정 된 페더레이션 서버 hello에 대 한 Windows Server 2012 R2 서버
* 원격 관리를 사용 하도록 설정 된 웹 응용 프로그램 프록시 서버 hello에 대 한 Windows Server 2012 R2 서버
* Hello 페더레이션에 대 한 SSL 인증서 서비스 (예: sts.contoso.com) toouse • 이름

### <a name="ad-fs-configuration-pre-requisites"></a>AD FS 구성 필수 조건
tooconfigure AD FS를 Azure AD Connect를 사용 하 여 팜, WinRM hello 원격 서버에서 활성화 되었는지 확인 합니다. 또한 hello 포트에 나열 된 요구 사항을 통과 [표 3-Azure AD Connect 및 페더레이션 서버/WAP](active-directory-aadconnect-ports.md#table-3---azure-ad-connect-and-ad-fs-federation-serverswap)합니다.

### <a name="create-a-new-ad-fs-farm-or-use-an-existing-ad-fs-farm"></a>새 AD FS 팜을 만들거나 기존 AD FS 팜 사용
기존 AD FS 팜 사용 하거나 새 AD FS 팜을 toocreate를 선택할 수 있습니다. 새 toocreate를 선택 하면 필요한 tooprovide hello SSL 인증서 됩니다. Hello SSL 인증서는 암호로 보호 되 면 hello 암호를 묻는 메시지가 나타납니다.

![AD FS 팜](./media/active-directory-aadconnect-get-started-custom/adfs1.png)

기존 AD FS 팜에 toouse를 선택 하면 이동 직접 toohello 화면 AD FS와 Azure AD 간의 트러스트 관계 hello를 구성 합니다.

### <a name="specify-hello-ad-fs-servers"></a>Hello AD FS 서버를 지정 합니다.
AD FS tooinstall 원하는 hello 서버를 입력 합니다. 용량 계획 요구 사항에 따라 하나 이상의 서버를 추가할 수 있습니다. 이 구성을 수행 하기 전에 모든 서버 tooActive 디렉터리를 조인 합니다. Microsoft에서는 테스트 및 파일럿 배포를 위해 단일 AD FS 서버를 설치하는 것이 좋습니다. 그런 다음 추가 하 고 초기 구성 후에 다시 Azure AD Connect를 실행 하 여 더 많은 서버 toomeet 크기 조정 요구 사항를 배포 합니다.

> [!NOTE]
> 이 구성을 수행 하기 전에 모든 서버는 조인 된 tooan AD 도메인을 확인 합니다.
>
>

![AD FS 서버](./media/active-directory-aadconnect-get-started-custom/adfs2.png)

### <a name="specify-hello-web-application-proxy-servers"></a>Hello 웹 응용 프로그램 프록시 서버 지정
원하는 웹 응용 프로그램 프록시 서버 hello 서버를 입력 합니다. 웹 응용 프로그램 프록시 서버 hello DMZ (엑스트라넷 연결)에 배포 되 고 hello 엑스트라넷의 요청을 인증 지원. 용량 계획 요구 사항에 따라 하나 이상의 서버를 추가할 수 있습니다. Microsoft에서는 테스트 및 파일럿 배포를 위해 단일 웹 응용 프로그램 프록시 서버를 설치하는 것이 좋습니다. 그런 다음 추가 하 고 초기 구성 후에 다시 Azure AD Connect를 실행 하 여 더 많은 서버 toomeet 크기 조정 요구 사항를 배포 합니다. Hello 인트라넷에서 프록시 서버 toosatisfy 인증 수가 해당 하는 것이 좋습니다.

> [!NOTE]
> <li> Hello AD FS 서버의 로컬 관리자 계정을 사용 하 든 hello 없는 경우에 관리자 자격 증명에 대 한 메시지가 됩니다.</li>
> <li> 이 단계를 실행 하기 전에 hello Azure AD Connect 서버와 웹 응용 프로그램 프록시 서버 hello HTTP/HTTPS 연결 되는지 확인 합니다.</li>
> <li> 웹 응용 프로그램 서버 hello와 hello AD FS 서버 tooallow 인증 요청 tooflow 통해 HTTP/HTTPS 연결 인지 확인 합니다.</li>
>

![웹앱](./media/active-directory-aadconnect-get-started-custom/adfs3.png)

Hello 웹 응용 프로그램 서버 설정할 수는 보안 연결 toohello AD FS 서버 되도록 증명된 tooenter 자격 증명을 됩니다. 이러한 자격 증명 toobe AD FS 서버 hello에 대 한 로컬 관리자 필요합니다.

![Proxy](./media/active-directory-aadconnect-get-started-custom/adfs4.png)

### <a name="specify-hello-service-account-for-hello-ad-fs-service"></a>AD FS 서비스 hello에 대 한 hello 서비스 계정 지정
hello AD FS 서비스 도메인에 필요한 서비스 계정 tooauthenticate 사용자 및 Active Directory에서 사용자 정보를 조회 합니다. 두 종류의 서비스 계정을 지원할 수 있습니다.

* **그룹 관리 서비스 계정** -Windows Server 2012에서 Active Directory Domain Services에 도입되었습니다. 이 계정 유형은 AD FS, tooupdate hello 계정 암호를 정기적으로 필요 없이 단일 계정 등의 서비스를 제공 합니다. AD FS 서버에 속해 있는 hello 도메인의 Windows Server 2012 도메인 컨트롤러를 이미 있는 경우이 옵션을 사용 합니다.
* **도메인 사용자 계정** -이러한 유형의 계정 해야 tooprovide 암호를 정기적으로 암호 업데이트 hello hello 암호 변경 또는 만료 된 경우. AD FS 서버에 속해 있는 hello 도메인에 Windows Server 2012 도메인 컨트롤러 수 없는 경우에이 옵션을 사용 합니다.

그룹 관리 서비스 계정 선택했는데 Active Directory에서 이 기능을 사용한 적이 없는 경우 엔터프라이즈 관리자 자격 증명에 대한 메시지가 표시됩니다. 이러한 자격 증명의 사용 되는 tooinitiate hello에 대 한 키 저장소 및 Active Directory의 hello 기능을 활성화 합니다.

> [!NOTE]
> Azure AD Connect hello AD FS 서비스는 hello 도메인의 SPN으로 이미 등록 되어 있으면 검사 toodetect를 수행 합니다.  AD DS에는 한 번에 등록 하는 중복 된 SPN toobe를 허용 하지 않습니다.  중복 된 SPN이 없으면 됩니다 수 tooproceed 추가로 hello SPN 제거 될 때까지 합니다.

![AD FS 서비스 계정](./media/active-directory-aadconnect-get-started-custom/adfs5.png)

### <a name="select-hello-azure-ad-domain-that-you-wish-toofederate"></a>원하는 toofederate hello Azure AD 도메인을 선택 합니다.
이 구성은 AD FS와 Azure AD 간에 사용 되는 toosetup hello 페더레이션 관계에 설명 합니다. AD FS tooissue 보안 토큰 tooAzure AD를 구성 하 고이 특정 AD FS 인스턴스에서 tootrust hello 토큰을 Azure AD를 구성 합니다. 만이 페이지는 tooconfigure hello 초기 설치에서 단일 도메인 허용 합니다. 나중에 Azure AD Connect를 다시 실행하여 더 많은 도메인을 구성할 수 있습니다.

![Azure AD 도메인](./media/active-directory-aadconnect-get-started-custom/adfs6.png)

### <a name="verify-hello-azure-ad-domain-selected-for-federation"></a>페더레이션에 대해 선택한 hello Azure AD 도메인 확인
페더레이션 hello 도메인 toobe을 선택 하면 Azure AD Connect 사용 하면 필요한 정보 tooverify 확인 되지 않은 도메인 있습니다. 참조 [추가 hello 도메인 및 확인](../active-directory-add-domain.md) 방법에 대 한 toouse이이 정보입니다.

![Azure AD 도메인](./media/active-directory-aadconnect-get-started-custom/verifyfeddomain.png)

> [!NOTE]
> Hello 하는 동안 AD 연결 시도 tooverify hello 도메인 단계를 구성 합니다. Tooconfigure hello 필요한 DNS 레코드를 추가 하지 않고 계속 하면 hello 마법사 수 toocomplete hello 구성 되지 않습니다.
>
>

## <a name="configure-and-verify-pages"></a>페이지 구성 및 확인
hello 구성은이 페이지에서 수행 됩니다.

> [!NOTE]
> 설치를 계속하기 전에 페더레이션을 구성한 경우 [페더레이션 서버에 대 한 이름 확인](active-directory-aadconnect-prerequisites.md#name-resolution-for-federation-servers)을 구성했는지 확인합니다.
>
>

![준비 tooconfigure](./media/active-directory-aadconnect-get-started-custom/readytoconfigure2.png)

### <a name="staging-mode"></a>스테이징 모드
가능한 toosetup 준비 모드와 병렬로 새 동기화 서버는 것만 지원 되는 toohave 한 동기화 서버 hello 클라우드에서 tooone 디렉터리 내보내기 합니다. 하지만 예를 들어 하나의 실행 중인 디렉터리 동기화, 다른 서버에서 toomove 하려는 경우 준비 모드에서 Azure AD Connect를 활성화할 수 있습니다. 아무것도 내보내지 것 않습니다 하지만 사용 하도록 설정 하면 hello 동기화 엔진에서는 가져오기 및이 정상적으로 데이터를 동기화 하는 광고 또는 광고 tooAzure 합니다. hello 기능 암호 동기화 및 암호 쓰기 저장은 준비 모드에서 사용할 수 없습니다.

![스테이징 모드](./media/active-directory-aadconnect-get-started-custom/stagingmode.png)

준비 모드에서 가능한 toomake 필요한 변경을 toohello 동기화 엔진이 이며 내보낸 toobe에 대 한 기능을 검토 합니다. Hello 구성 좋은 모양, hello 설치 마법사를 다시 실행 하 고 준비 모드를 사용 하지 않도록 설정 합니다. 데이터는 이제이 서버에서 내보낸된 tooAzure AD입니다. 다른 서버에서 동일한 시간 하나만 있으므로 서버에서 적극적으로 내보내는 hello hello 있는지 toodisable를 확인 합니다.

자세한 내용은 [준비 모드](active-directory-aadconnectsync-operations.md#staging-mode)를 참조하세요.

### <a name="verify-your-federation-configuration"></a>페더레이션 구성 확인
Azure AD Connect hello 확인 단추를 클릭할 때 사용자에 대 한 hello DNS 설정을 확인 합니다.

**인트라넷 연결 확인**

* 해결 FQDN 페더레이션: Azure AD Connect 확인 hello 페더레이션 FQDN DNS tooensure 연결 해결할 수 있습니다. Azure AD Connect hello FQDN을 확인할 수 없는 경우 hello 확인 실패 합니다. Hello toosuccessfully 완료 hello 확인 순서에 페더레이션 서비스 FQDN에 대 한 DNS 레코드가 있는지 확인 합니다.
* DNS A 레코드: Azure AD Connect는 페더레이션 서비스에 대한 A 레코드가 있는지 확인합니다. A 레코드 hello 없는 경우, hello 확인이 실패 합니다. 만들기는 A 레코드가 아니라 레코드를 CNAME 순서 toosuccessfully에 페더레이션 FQDN에 대 한 hello 확인을 완료 합니다.

**엑스트라넷 연결 확인**

* 해결 FQDN 페더레이션: Azure AD Connect 확인 hello 페더레이션 FQDN DNS tooensure 연결 해결할 수 있습니다.

![완료](./media/active-directory-aadconnect-get-started-custom/completed.png)

![Verify](./media/active-directory-aadconnect-get-started-custom/adfs7.png)

또한 hello 확인 단계를 수행 합니다.

* Hello 인트라넷의 도메인에 가입 된 컴퓨터에서 브라우저에서 로그인 할 수 있는지 확인: toohttps://myapps.microsoft.com 연결 고 hello 로그인 로그인된 계정을 사용 하 여 확인 합니다. hello 기본 제공 AD DS 관리자 계정 동기화 되지 않은 및 확인에 사용 될 수 없습니다.
* Hello 엑스트라넷에서 장치에서 로그인 할 수 있는지 확인 합니다. 홈 컴퓨터 또는 모바일 장치에서 toohttps://myapps.microsoft.com 연결 및 자격 증명을 제공 합니다.
* 리치 클라이언트 로그인 유효성을 검사합니다. Toohttps://testconnectivity.microsoft.com 연결, hello 선택 **Office 365** 탭 및 선택 hello **Office 365 Single Sign-on 테스트**합니다.

## <a name="next-steps"></a>다음 단계
Hello 설치가 완료 되 면 로그 아웃 하 고 동기화 서비스 관리자 또는 동기화 규칙 편집기를 사용 하기 전에 다시 tooWindows에 로그인 합니다.

Azure AD Connect를 설치 했으므로 다음을 할 수 있습니다 [hello 설치 되었는지 확인 하 고 라이선스를 할당](active-directory-aadconnect-whats-next.md)합니다.

Hello 설치를 사용 하도록 설정 된 이러한 기능에 대 한 자세한 정보: [실수로 삭제 금지](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) 및 [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md)합니다.

이러한 공통 항목에 대 한 자세한 정보: [스케줄러와 tootrigger 동기화 방법을](active-directory-aadconnectsync-feature-scheduler.md)합니다.

[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
