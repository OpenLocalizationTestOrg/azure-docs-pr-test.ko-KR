---
title: "Azure AD Connect: 사용자 로그인 | Microsoft Docs"
description: "사용자 지정 설정을 위한 Azure AD Connect 사용자 로그인."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 547b118e-7282-4c7f-be87-c035561001df
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 7848b419f3855b25cfa074a46779d258bd534bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-user-sign-in-options"></a>Azure AD Connect 사용자 로그인 옵션
Azure Active Directory (Azure AD) 연결을 사용 하면 프로그램 사용자 toosign tooboth 클라우드 및 온-프레미스 리소스를 사용 하 여 hello 동일한 암호입니다. 이 문서 toouse tooAzure AD에에서 로그인 하는 것에 대 한 원하는 hello id를 선택 하면 각 identity 모델 toohelp에 대 한 주요 개념을 설명 합니다.

이미 익숙한 hello Azure AD id 모델 특정 메서드에 대 한 자세한 toolearn 원하는 hello 적절 한 링크를 참조 하십시오.

* [SSO(Single Sign-On)](active-directory-aadconnect-sso.md)를 사용하여 [암호 동기화](#password-synchronization)
* [통과 인증](active-directory-aadconnect-pass-through-authentication.md)
* [Federated SSO(Active Directory Federation Services(AD FS) 지원)](#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)

## <a name="choosing-hello-user-sign-in-method-for-your-organization"></a>조직에 대 한 hello 사용자 로그인-방법 선택
대부분의 조직 하 려 tooenable 사용자 로그인 tooOffice 비교 365, SaaS 응용 프로그램 및 기타 Azure AD 기반 리소스에 대 한 hello 기본 암호 동기화 옵션을 것이 좋습니다. 그러나 일부 조직에는 아닐 수 toouse 특별 한 이유가 없는이 옵션입니다. AD FS 등의 페더레이션된 로그인 옵션 또는 통과 인증 중에서 선택할 수 있습니다. 다음 테이블 toohelp hello 올바른 선택을 확인 hello를 사용할 수 있습니다.

너무 필요| SSO를 사용하는 PS| SSO를 사용하는 PA| AD FS |
 --- | --- | --- | --- |
새 사용자, 연락처 및 그룹 계정을 온-프레미스 Active Directory toohello 클라우드에서 자동으로 동기화 합니다.|x|x|x|
Office 365 하이브리드 시나리오에 대한 테넌트를 설정합니다.|x|x|x|
온-프레미스 암호를 사용 하 여 내에서 사용자가 toosign 및 클라우드 서비스 액세스를 사용 합니다.|x|x|x|
회사 자격 증명을 사용하여 Single Sign-On을 구현합니다.|x|x|x|
확인 암호가 hello 클라우드에 저장 됩니다.||x*|x|
온-프레미스 Multi-Factor Authentication 솔루션을 사용합니다.|||x|

*경량 커넥터를 통해

>[!NOTE]
> 통과 인증은 현재 리치 클라이언트에 몇 가지 제한 사항이 있습니다. 자세한 내용은 [통과 인증](active-directory-aadconnect-pass-through-authentication.md)을 참조하세요.

### <a name="password-synchronization"></a>암호 동기화
암호 동기화와 함께 온-프레미스 Active Directory tooAzure AD에서에서 사용자 암호 해시 동기화 됩니다. 사용 하 여 hello 동일한 사용자가 항상 수행할 수 있도록 하는 즉시 hello 새 암호 동기화 된 tooAzure AD는 암호 변경 되거나 온-프레미스를 재설정 하는 경우 클라우드 리소스와 온-프레미스 리소스에 대 한 암호입니다. hello 암호가 tooAzure AD 전송 또는 일반 텍스트로 Azure AD에 저장 되지 않습니다. 암호 쓰기 저장 tooenable 셀프 서비스 암호 재설정 Azure ad에서와 함께 암호 동기화를 사용할 수 있습니다.

또한 사용할 수 있습니다 [SSO](active-directory-aadconnect-sso.md) hello 회사 네트워크에 있는 도메인에 가입 된 컴퓨터에 있는 사용자에 대 한 합니다. 클라우드 리소스에 안전 하 게 액세스 하는 사용자 이름 toohelp tooenter single sign on, 활성화 된 사용자만 필요 합니다.

![암호 동기화](./media/active-directory-aadconnect-user-signin/passwordhash.png)

자세한 내용은 참조 hello [암호 동기화](active-directory-aadconnectsync-implement-password-synchronization.md) 문서.

### <a name="pass-through-authentication"></a>통과 인증
통과 인증을 사용 하면 hello 사용자의 암호는 hello 온-프레미스 Active Directory 컨트롤러에 대해 유효성이 검사 됩니다. hello 암호 toobe 부분도 Azure AD에 필요 하지 않습니다. 따라서 로그인 시간 제한 등의 온-프레미스 정책을 toobe 인증 toocloud 서비스 중에 평가 합니다.

통과 인증 hello 온-프레미스 환경에서 Windows Server 2012 R2 도메인에 가입 된 컴퓨터에서 간단한 에이전트를 사용합니다. 이 에이전트는 암호 유효성 검사 요청을 수신합니다. 모든 인바운드 포트가 toobe 열기 toohello 인터넷 필요 하지 않습니다.

또한 single sign on 사용자 hello 회사 네트워크에 있는 도메인에 가입 된 컴퓨터에 대해 사용할 수 있습니다. 클라우드 리소스에 안전 하 게 액세스 하는 사용자 이름 toohelp tooenter single sign on, 활성화 된 사용자만 필요 합니다.
![통과 인증](./media/active-directory-aadconnect-user-signin/pta.png)

자세한 내용은 다음을 참조하세요.
- [통과 인증](active-directory-aadconnect-pass-through-authentication.md)
- [Single Sign-On](active-directory-aadconnect-sso.md)

### <a name="federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2의 AD FS에 새 또는 기존 팜을 사용하는 페더레이션
페더레이션 로그인, 사용자가 로그인 할 수 tooAzure 온-프레미스 암호와 함께 AD 기반 서비스입니다. Hello 회사 네트워크에 있는 동안도 없는 경우 tooenter 암호입니다. AD FS와 함께 hello 페더레이션 옵션을 사용 하면 Windows Server 2012 r 2에서 AD FS와 함께 새 팜이나 기존 팜에서 배포할 수 있습니다. 기존 팜에 toospecify를 선택 하면 사용자가 로그인 할 수 있도록 Azure AD Connect 팜 및 Azure AD 간의 hello 트러스트를 구성 합니다.

<center>![Windows Server 2012 R2의 AD FS와 페더레이션](./media/active-directory-aadconnect-user-signin/federatedsignin.png)</center>

#### <a name="deploy-federation-with-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2의 AD FS로 페더레이션 배포

새 팜을 배포하는 경우 필수 요건은 다음과 같습니다.

* 페더레이션 서버 hello에 대 한 Windows Server 2012 R2 서버입니다.
* 웹 응용 프로그램 프록시 hello에 대 한 Windows Server 2012 R2 서버입니다.
* 원하는 페더레이션 서비스 이름에 대한 하나의 SSL 인증서가 있는 .pfx 파일 예: fs.contoso.com

새 팜을 배포 하거나 기존 팜을 사용하는 경우 필수 요건은 다음과 같습니다.

* 페더레이션 서버에 대한 로컬 관리자 자격 증명.
* 로컬 관리자 자격 증명 (도메인에 가입 되지)는 모든 작업 그룹 서버에 toodeploy를 만들려는 경우에 웹 응용 프로그램 프록시 역할을 hello 합니다.
* hello 컴퓨터에서 실행 하는 hello 마법사 toobe 수 tooconnect tooany Windows 원격 관리를 사용 하 여 AD FS 또는 웹 응용 프로그램 프록시에 tooinstall 되도록 다른 컴퓨터입니다.

자세한 내용은 참조 [AD FS로 SSO 구성](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs)을 참조하세요.

#### <a name="sign-in-by-using-an-earlier-version-of-ad-fs-or-a-third-party-solution"></a>이전 버전의 AD FS 또는 타사 솔루션을 사용하여 로그인
이미 구성한 경우 클라우드 로그인 이전 버전의 AD FS (예: AD FS 2.0) 또는 제 3 자 페더레이션 공급자를 사용 하 여, tooskip 사용자 로그인 구성 Azure AD Connect 통해 선택할 수 있습니다. 이렇게 하면 tooget hello 최신 동기화 및 Azure AD Connect의 다른 기능 동안 계속 기존 솔루션을 사용 하 여 로그인 합니다.

자세한 내용은 참조 hello [Azure AD에서 타사 페더레이션 호환성 목록](active-directory-aadconnect-federation-compatibility.md)합니다.


## <a name="user-sign-in-and-user-principal-name"></a>사용자 로그인 및 사용자 계정 이름
### <a name="understanding-user-principal-name"></a>사용자 계정 이름 이해
Active Directory에서 hello 기본 사용자 계정 이름 (UPN) 접미사는 hello 사용자 계정을 만든 위치 hello 도메인 hello DNS 이름입니다. 대부분의 경우에서 hello 인터넷에서 엔터프라이즈 도메인 hello로 등록 된 hello 도메인 이름입니다. 그러나 Active Directory 도메인 및 트러스트를 사용하여 더 많은 UPN 접미사를 추가할 수 있습니다.

hello hello 사용자의 UPN에 hello 형식이 username@domain합니다. 예를 들어 "contoso.com" 이라는 Active Directory 도메인, John 라는 사용자를 할 수 hello UPN "john@contoso.com"입니다. hello hello 사용자의 UPN RFC 822를 기반으로 합니다. UPN hello 및 전자 메일 공유 hello 같은 형식, 있지만 hello 값의 사용자에 대 한 UPN hello 존재 하거나 hello 사용자의 hello 전자 메일 주소와 동일한 hello 되지 않을 수 있습니다.

### <a name="user-principal-name-in-azure-ad"></a>Azure AD의 사용자 계정 이름
hello userPrincipalName 특성을 사용 하 여 hello Azure AD Connect 마법사 또는 온-프레미스에서 Azure AD에서 hello 사용자 계정 이름으로 사용 하는 특성 (에 사용자 지정 설치) toobe를 hello 지정할 수 있습니다. AD tooAzure 로그인에 사용 되는 hello 값입니다. Azure AD는 기본적으로 대체 한 후 tooa의 Azure AD에서 도메인 확인 hello userPrincipalName 특성의 값을 hello와 일치 하지 않으면. onmicrosoft.com 값입니다.

Azure Active Directory에 모든 디렉터리와 hello 형식 contoso.onmicrosoft.com 하도록 Azure 또는 다른 Microsoft 서비스를 사용 하 여 시작 하는 기본 제공 도메인 이름을 함께 제공 됩니다. 향상 되 고 hello 로그인 환경을 사용자 지정 도메인을 사용 하 여 간소화할 수 있습니다. 에 대 한 내용은 사용자 지정 도메인 이름 Azure AD에서 tooverify 도메인을 확인 하는 방법 및 [추가 사용자 지정 도메인 이름을 tooAzure Active Directory](../add-custom-domain.md#add-your-custom-domain)합니다.

## <a name="azure-ad-sign-in-configuration"></a>Azure AD 로그인 구성
### <a name="azure-ad-sign-in-configuration-with-azure-ad-connect"></a>Azure AD connect을 사용하여 Azure AD 로그인 구성
hello Azure AD 로그인 환경을 Azure AD hello hello Azure AD 디렉터리에서 확인 하는 사용자 지정 도메인의 동기화 된 tooone 되는 사용자의 사용자 계정 이름 접미사 hello 일치 시킬 수 있는지 여부에 따라 달라 집니다. Azure AD Connect 도움말을 제공 Azure AD 로그인 설정을 구성 하는 동안 hello 로그인에서 사용자 환경을 hello 클라우드 비슷한 toohello 온-프레미스 환경이 되도록 합니다.

Azure AD Connect 목록 hello 도메인 및 시도 toomatch에 대해 정의 된 UPN 접미사 hello Azure AD에서 사용자 지정 도메인을 사용 하 여 합니다. 그런 다음 쉽습니다 toobe 수행 해야 하는 hello 적절 한 작업으로.
hello Azure AD 로그인 페이지는 온-프레미스 Active Directory에 대해 정의 된 hello UPN 접미사를 나열 하 고 각 접미사에 대해 hello 해당 상태를 표시 합니다. hello 상태 값 hello 다음 중 하나일 수 있습니다.

| 시스템 상태 | 설명 | 작업 필요 |
|:--- |:--- |:--- |
| Verified |Azure AD Connect가 Azure AD에서 확인된 일치하는 도메인을 찾았습니다. 이 도메인에 대한 모든 사용자는 온-프레미스 자격 증명을 사용하여 로그인할 수 있습니다. |어떤 조치가 필요하지 않습니다. |
| 확인되지 않음 |Azure AD Connect는 Azure AD에서 사용자 지정 도메인을 찾을 수 있지만 확인되지 않습니다. 이 도메인의 hello 사용자의 UPN 접미사 hello 됩니다 변경할 toohello 기본. hello 도메인은 확인 되지 경우 동기화 후 onmicrosoft.com 접미사가 있습니다. | [Azure AD에서 hello 사용자 지정 도메인을 확인 합니다.](../add-custom-domain.md#verify-the-domain-name-with-azure-ad) |
| 추가되지 않음 |Azure AD Connect 사용자 지정 도메인 그 속하는지를 toohello UPN 접미사를 찾지 못했습니다. 이 도메인의 hello 사용자의 UPN 접미사 hello 됩니다 변경할 toohello 기본. onmicrosoft.com 접미사가 hello 도메인 추가 Azure에서 확인할 수 없는 경우. | [추가 하 고 해당 toohello UPN 접미사는 사용자 지정 도메인을 확인 합니다.](../add-custom-domain.md) |

hello Azure AD 로그인 페이지는 온-프레미스 Active Directory에 대해 정의 되 고 해당 사용자 지정 도메인 확인 상태를 현재 hello로 Azure AD에 hello 하는 hello UPN 접미사를 나열 합니다. 에서는 사용자 지정 설치를 선택할 수 있습니다 hello에 hello 사용자 계정 이름에 대 한 hello 특성 **Azure AD 로그인** 페이지.

![Azure AD 로그인 페이지](./media/active-directory-aadconnect-user-signin/custom_azure_sign_in.png)

Hello 새로 고침 단추 toore 인출 hello의 최신 상태 hello Azure AD에서 사용자 지정 도메인을 클릭할 수 있습니다.

### <a name="selecting-hello-attribute-for-hello-user-principal-name-in-azure-ad"></a>Azure AD에서 hello 사용자 계정 이름에 대 한 hello 특성을 선택 하면
hello 특성 userPrincipalName에는 사용자가 tooAzure AD 및 Office 365에 로그인 할 때 사용 하는 hello 특성입니다. Hello 사용자가 동기화 하기 전에 Azure AD에 사용 되는 hello 도메인 (UPN 접미사 라고도 함)를 확인 해야 합니다.

Hello 기본 특성 userPrincipalName을 유지 하는 것이 좋습니다. 다른 특성 (예: 전자 메일)을 포함 하는 hello 특성으로 hello 로그인 id입니다.가이 특성 nonroutable 고 가능한 tooselect는 확인할 수 없습니다. 대체 id. hello로도 알려져 hello 대체 ID 특성 값을 표준 RFC 822 hello를 따라야 합니다. 암호 SSO 및 hello 로그인 솔루션으로 페더레이션 SSO 모두 갖춘 대체 ID를 사용할 수 있습니다.

> [!NOTE]
> 대체 ID를 사용하면 일부 Office 365 워크로드와 호환되지 않습니다. 자세한 내용은 [대체 로그인 ID 구성](https://technet.microsoft.com/library/dn659436.aspx)을 참조하세요.
>
>

#### <a name="different-custom-domain-states-and-their-effect-on-hello-azure-sign-in-experience"></a>다른 사용자 지정 도메인 상태 및 hello Azure 로그인 경험에 미치는 영향
Azure AD 디렉터리의 사용자 지정 도메인 상태 hello 간 매우 중요 한 toounderstand hello 관계 이며 hello 된 UPN 접미사 정의 온-프레미스입니다. Azure AD Connect를 사용 하 여 동기화를 설정할 때 hello 다른 가능한 Azure 로그인 환경을 통해 해 보겠습니다.

다음 정보는 hello에 대 한 가정 예를 들어 UPN-의 일환으로 hello 온-프레미스 디렉터리에 사용 되는 hello UPN 접미사가 contoso.com 신경 한다는 것 user@contoso.com합니다.

###### <a name="express-settingspassword-synchronization"></a>Express 설정/암호 동기화
| 시스템 상태 | Azure 로그인 사용자 경험에 미치는 영향 |
|:---:|:--- |
| 추가되지 않음 |이 경우 contoso.com에 대 한 사용자 지정 도메인이 없습니다 hello Azure AD 디렉터리에 추가 된 되었습니다. 사용자에 게 UPN 온-프레미스 hello 접미사와 함께 @contoso.com 수 toouse tooAzure에서 자신의 온-프레미스 UPN toosign 수 없습니다. 대신 해야 toouse 새 UPN hello 기본 Azure AD 디렉터리에 대 한 hello 접미사를 추가 하 여 Azure AD를 통해 toothem 제공 합니다. 예를 들어 사용자가 Azure AD toohello 디렉터리 azurecontoso.onmicrosoft.com를 동기화 하는 경우 다음 hello 온-프레미스 사용자 user@contoso.com 의 UPN이 주어 집니다 user@azurecontoso.onmicrosoft.com합니다. |
| 확인되지 않음 |이 경우 hello Azure AD 디렉터리에 추가 된 사용자 지정 도메인 contoso.com을 해야 합니다. 아직 확인되지 않습니다. 와 hello 도메인을 확인 하지 않고 사용자가 동기화 하는 중입니다. 계속 진행 하는 경우에 다음 hello 사용자 Azure AD에 의해 새 UPN 할당 될, hello "추가 되지 않습니다" 시나리오에에서 동일 하 게 합니다. |
| Verified |이 경우 이미 추가 하 고 UPN 접미사 hello에 대 한 Azure AD에서 확인 하는 사용자 지정 도메인 contoso.com을 해야 합니다. 사용자가 될 수 toouse 자신의 온-프레미스 사용자 계정 이름 예를 들어 user@contoso.com, tooAzure 동기화 하는 후에 toosign tooAzure AD 합니다. |

###### <a name="ad-fs-federation"></a>AD FS 페더레이션
기본값은 hello 페더레이션을 만들 수 없습니다. Azure AD에서 onmicrosoft.com 도메인 또는 Azure AD에서 확인 되지 않은 사용자 지정 도메인입니다. 실행할 때는 hello Azure AD Connect 마법사는 확인 되지 않은 도메인 toocreate를 선택 하는 경우와 페더레이션을 다음 Azure AD Connect 프롬프트 hello 도메인에 대 한 DNS 호스팅되 만든 toobe 기록 필요한 hello로 있습니다. 자세한 내용은 참조 [페더레이션에 대해 선택한 hello Azure AD 도메인을 확인](active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation)합니다.

Hello 사용자 로그인 옵션을 선택한 경우 **AD FS와의 페더레이션을**, Azure AD에 페더레이션을 만들 사용자 지정 도메인 toocontinue 있어야 합니다. 를 설명 하겠습니다 hello Azure AD 디렉터리에 추가 된 사용자 지정 도메인 contoso.com 있어야 한다는 의미 합니다.

| 시스템 상태 | Hello Azure 로그인 사용자 경험에 미치는 영향 |
|:---:|:--- |
| 추가되지 않음 |이 경우 Azure AD Connect hello Azure AD 디렉터리의 hello UPN 접미사가 contoso.com에 대 한 일치 하는 사용자 지정 도메인을 찾지 못했습니다. 사용자가 toosign 해당 온-프레미스 UPN 함께 AD FS를 사용 하 여 필요한 경우 사용자 지정 도메인 contoso.com tooadd 필요 (같은 user@contoso.com). |
| 확인되지 않음 |이 경우에 Azure AD Connect는 이후 단계에서 도메인을 확인하는 방법에 대한 적절한 정보를 메시지로 표시합니다. |
| Verified |이 경우에 이동할 수 있습니다 계속 추가 작업 없이 hello 구성. |

## <a name="changing-hello-user-sign-in-method"></a>Hello 사용자 로그인 방법 변경
Hello 마법사와 Azure AD Connect의 hello 초기 구성 후에 Azure AD Connect에서 사용할 수 있는 hello 작업을 사용 하 여 페더레이션, 암호 동기화 또는 통과 인증에서 hello 사용자 로그인 방법을 변경할 수 있습니다. Hello Azure AD Connect 마법사를 다시 실행 하 고 수행할 수 있는 작업 목록이 표시 됩니다. 선택 **사용자 로그인 변경** hello 작업 목록에서 합니다.

![사용자 로그인 변경](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Hello 다음 페이지에서 묻는 tooprovide hello 자격 증명이 Azure AD에 대 한 합니다.

![TooAzure AD 연결](./media/active-directory-aadconnect-user-signin/changeusersignin2.png)

Hello에 **사용자 로그인** 페이지에서 원하는 hello 사용자 로그인을 선택 합니다.

![TooAzure AD 연결](./media/active-directory-aadconnect-user-signin/changeusersignin2a.png)

> [!NOTE]
> 임시 스위치 toopassword 동기화를 만들고만 있는 경우 다음 hello 선택 **사용자 계정을 변환 하지 않는** 확인란 합니다. 각 사용자 toofederated 변환 hello 옵션을 선택 하 고 몇 시간이 걸릴 수 있습니다.
>
>

## <a name="next-steps"></a>다음 단계
- [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
- [Azure AD Connect 설계 개념](active-directory-aadconnect-design-concepts.md)에 대해 자세히 알아봅니다.
