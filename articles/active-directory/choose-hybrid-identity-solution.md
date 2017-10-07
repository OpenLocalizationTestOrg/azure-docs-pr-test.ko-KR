---
title: "Azure 하이브리드 id 솔루션 aaaChoose | Microsoft Docs"
description: "Hello 사용 가능한 하이브리드 id 솔루션 및 결정에 대 한 있습니다 toomake hello 최상의 identity 거 버 넌 스 조직에 대 한 권장 사항에 대 한 기본적인 이해를 가져옵니다."
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4ab8aff314f6308ab32f77e81cf0f07e1f5d7b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-hybrid-identity-solutions"></a>Microsoft 하이브리드 ID 솔루션
[Microsoft Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) 하이브리드 id 솔루션 toosynchronize Azure AD 사용자가 온-프레미스를 관리 하는 동안 사용 하 여 온-프레미스 디렉터리 개체를 사용 합니다. Azure AD와 온-프레미스 Windows Server Active Directory는 toouse identity 동기화 또는 페더레이션 identity 삭제할지 toosynchronize 계획할 때는 첫 번째 의사 결정 toomake를 hello 합니다. 동기화 된 id 및 선택적으로 암호 해시를 설정 하면 사용자가 toouse hello 동일한 암호 tooaccess 온-프레미스와 클라우드 기반 조직 리소스입니다. Single sign-on (SSO) 또는 온-프레미스 MFA 같은 더 고급 시나리오 요구 사항에 대 한 Active Directory Federation Services (AD FS) toofederate identities toodeploy 해야합니다. 

하이브리드 ID를 구성하는 데 사용할 수 있는 옵션은 몇 가지가 있습니다. 이 문서에서는 정보 toohelp 간편한 배포에 따라 조직에 가장 적합 한 hello 및 특정 사용자 id 및 액세스 관리 요구를 선택 합니다. 조직의 요구에 맞는 가장 하는 id 모델을 고려할 때 시간, 기존 인프라, 복잡성 및 비용에 대 한 toothink을 해야 합니다. 이러한 요소는 조직마다 다르며 시간이 흐름에 따라 변경될 수 있습니다. 그러나 요구 사항, 변경 있습니다 hello 유연성 tooswitch tooa 다른 id 모델.

> [!TIP]
> 이러한 솔루션은 모두 [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)에서 제공됩니다.

## <a name="synchronized-identity"></a>동기화된 ID 
동기화 된 id는 Azure AD와 hello 가장 간단한 방법은 toosynchronize 온-프레미스 디렉터리 개체 (사용자 및 그룹)입니다. 

![동기화된 하이브리드 ID](./media/choose-hybrid-identity-solution/synchronized-identity.png)

동기화 된 identity hello 쉽고 빠른 방법 이지만, 사용자가 클라우드 기반 리소스에 대 한 별도 암호 toomaintain 여전히 필요 합니다. tooavoid이 수도 있습니다 (선택 사항) [사용자 암호 해시 동기화](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-implement-password-synchronization#what-is-password-synchronization) tooyour Azure AD 디렉터리입니다. 동일한 사용자 이름 및 암호를 온-프레미스를 사용 하는 hello와 toocloud 기반 조직 리소스에 암호 해시 사용 하면 사용자가 toolog 동기화 합니다. Azure AD Connect는 온-프레미스 디렉터리에 변경 내용이 있는지 주기적으로 확인하고 Azure AD 디렉터리를 동기화된 상태로 유지합니다. 온-프레미스 Active Directory에서 사용자 특성 또는 암호가 변경되면 Azure AD에서 자동으로 업데이트됩니다. 

대부분의 조직에 게만 tooenable 365 tooOffice, SaaS 응용 프로그램 및 기타 Azure AD 기반 리소스에 해당 사용자가 toosign hello 기본 암호 동기화 옵션을 사용 하는 것이 좋습니다. 드립니다 문제가 해결 되지 통과 인증 및 AD FS 간의 toodecide를 해야 합니다.

> [!TIP]
> 사용자 암호는 hello 실제 사용자 암호를 나타내는 해시 값의 hello 형태로 온-프레미스 Windows Server Active Directory에 저장 됩니다. 해시 값은 단방향 수학적 함수 (해시 알고리즘 hello)의 결과입니다. 결과 없으며 메서드 toorevert hello 암호의 단방향 함수 toohello 일반 텍스트 버전입니다. 암호 해시 toosign tooyour 온-프레미스 네트워크를 사용할 수 없습니다. Toosynchronize 암호를 선택 하는 경우 Azure AD Connect 추출 암호 해시 hello에서 온-프레미스 Active Directory와 동기화 된 tooAzure AD 되기 전에 toohello 암호 해시를 처리 하는 추가 보안을 적용 합니다. 암호 동기화는 암호 쓰기 저장 tooenable 셀프 서비스 암호 재설정 Azure ad에서와 함께 사용할 수도 있습니다. 또한 사용자가 도메인에 가입 된 컴퓨터에 연결 된 toohello 회사 네트워크에 대 한 single sign on (SSO) 사용할 수 있습니다. Single sign-on으로 사용 되는 사용자 하기만 tooenter는 username toosecurely 클라우드 리소스에 액세스 합니다. 

## <a name="pass-through-authentication"></a>통과 인증
[Azure AD 통과 인증](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication)은 온-프레미스 Active Directory를 사용하여 Azure AD 기반 서비스에 대한 간단한 암호 유효성 검사 솔루션을 제공합니다. 조직에 대 한 보안 및 규정 준수 정책에 해시 된 폼에도 사용자의 암호를 보내지 허용 하지 않는 경우 하기만 하면 toosupport 데스크톱 SSO 도메인 가입 장치에 대 한 통과 인증을 사용 하 여 평가 하는 것이 좋습니다. 통과 인증 AD FS와 비교 했을 때 hello 배포 인프라를 간소화 하는 DMZ hello에서 모든 배포 하지 않아도 됩니다. 사용자가 Azure AD를 사용하여 로그인할 때 이 인증 방법은 온-프레미스 Active Directory에 대해 직접 사용자 암호의 유효성을 검사합니다.

![통과 인증](./media/choose-hybrid-identity-solution/pass-through-authentication.png)

통과 인증을 위한 복잡 한 네트워크 인프라가 필요 하지 않으며 hello 클라우드에서 온-프레미스 암호 toostore 필요 하지 않습니다. Single sign-on으로 결합 tooAzure AD 또는 기타 클라우드 서비스에 로그인 할 때 통과 인증에 완전히 통합된 환경을 제공 합니다.

통과 인증은 암호 유효성 검사 요청을 수신 대기하는 간단한 온-프레미스 에이전트를 사용하는 Azure AD Connect를 통해 구성됩니다. hello 에이전트 쉽게 배포 toomultiple 컴퓨터 tooprovide 고가용성을 수 있으며 부하 분산 됩니다. 모든 통신은 아웃 바운드만, 이므로 hello 커넥터 toobe DMZ에서 설치에 대 한 요구 사항 없음. hello 커넥터에 대 한 hello 서버 컴퓨터 요구 사항은 다음과 같습니다.

- Windows Server 2012 R2 이상
- 사용자를 확인 하는 hello 포리스트에 tooa 도메인에 가입

> [!NOTE]
> Azure AD 통과 인증은 현재 미리 보기 상태이며 최신 인증을 지원하는 웹 브라우저 기반 클라이언트 및 Office 클라이언트에 대해 지원됩니다. 지원 되지 않는 클라이언트에 레거시 Office 클라이언트 및 Exchange ActiveSync (모바일 장치에서 네이티브 메일 클라이언트 포함)와 같은 것이 권장된 toouse hello 최신 인증 동일 합니다. 최신 인증 통과 인증을 사용 하면 뿐만 아니라 조건부 액세스 정책 toobe 등 multi-factor authentication이 적용에 대 한 수도 있습니다. 

통과 인증 tooAzure AD에 가입 된 Windows 10 장치를 사용할 경우 현재 지원 되지 않습니다. 그러나 자동 대체 toosupport Windows 10으로 암호 해시 동기화를 사용할 수 있습니다 및 기존 클라이언트 hello 앞에서 언급 한 합니다. Hello 미리 보기 기간 동안 암호 해시 동기화 Azure AD Connect에서 hello 로그인 옵션으로 통과 인증을 선택한 경우 기본적으로 사용 됩니다.


## <a name="federated-identity-ad-fs"></a>페더레이션 ID(AD FS)
사용자가 Office 365 및 다른 클라우드 서비스에 액세스하는 방식을 더 세밀하게 제어하려면 [AD FS(Active Directory Federation Services)](https://docs.microsoft.com/windows-server/identity/ad-fs/overview/whats-new-active-directory-federation-services-windows-server-2016)를 사용하여 SSO(Single Sign-On)와의 디렉터리 동기화를 설정하면 됩니다. 페더레이션 사용자의 로그인을 AD FS 대리자 인증 tooan 온-프레미스 사용자 자격 증명의 유효성을 검사 하는 서버. 이 모델에서는 온-프레미스 Active Directory 자격 증명은 tooAzure AD 전달 되지 합니다.

![페더레이션 ID](./media/choose-hybrid-identity-solution/federated-identity.png)

Id 페더레이션이 라고도 함,이 로그인 메서드를 사용 하면 모든 사용자 인증 제어 온-프레미스 관리자는 tooimplement 좀 더 엄격한 수준의 액세스 제어 합니다. Id 페더레이션이 AD FS와 함께 가장 복잡 한 hello 옵션 고 온-프레미스 환경에 추가 서버를 배포할 필요 합니다. Id 페더레이션이 Active Directory 및 AD FS 인프라에 대 한 tooproviding 연중 무휴 지원을 커밋합니다. 이 높은 수준의 지원과 필요한 이므로 온-프레미스 인터넷에 액세스 하는 경우 도메인 컨트롤러 또는 AD FS 서버를 사용할 수 없는 사용자가 toocloud 서비스에 로그인 할 수 없습니다.

> [!TIP]
> Active Directory Federation Services (AD FS)와 페더레이션을 toouse 결정 한 경우 설정할 수 있습니다 필요에 따라 백업으로 암호 동기화를 AD FS 인프라 실패 하는 경우.


## <a name="common-scenarios-and-recommendations"></a>일반적인 시나리오 및 권장 사항
다음은 몇 가지 일반적인 하이브리드 id 및 액세스 관리 시나리오 권장 toowhich 하이브리드 id 옵션 (또는 옵션)로 각각에 대해 수행할 수 있습니다.

|수행 작업:|PWS 및 SSO<sup>1</sup>| PTA 및 SSO<sup>2</sup> | AD FS<sup>3</sup>|
|-----|-----|-----|-----|
|새 사용자, 연락처 및 그룹 계정을 자동으로 내 온-프레미스 Active Directory toohello 클라우드에서 생성을 동기화 합니다.|![권장](./media/choose-hybrid-identity-solution/ic195031.png)| ![권장](./media/choose-hybrid-identity-solution/ic195031.png) |![권장](./media/choose-hybrid-identity-solution/ic195031.png)|
|Office 365 하이브리드 시나리오에 대한 테넌트 설정|![권장](./media/choose-hybrid-identity-solution/ic195031.png)| ![권장](./media/choose-hybrid-identity-solution/ic195031.png) |![권장](./media/choose-hybrid-identity-solution/ic195031.png)|
|내 사용자 toosign 사용 및 온-프레미스 암호를 사용 하 여 클라우드 서비스에 액세스|![권장](./media/choose-hybrid-identity-solution/ic195031.png)| ![권장](./media/choose-hybrid-identity-solution/ic195031.png) |![권장](./media/choose-hybrid-identity-solution/ic195031.png)|
|회사 자격 증명을 사용하여 Single Sign-On 구현|![권장](./media/choose-hybrid-identity-solution/ic195031.png)| ![권장](./media/choose-hybrid-identity-solution/ic195031.png) |![권장](./media/choose-hybrid-identity-solution/ic195031.png)|
|없는 암호 해시는 hello 클라우드에 저장 해두어야| |![권장](./media/choose-hybrid-identity-solution/ic195031.png)|![권장](./media/choose-hybrid-identity-solution/ic195031.png)|
|온-프레미스 다단계 인증 솔루션 사용| | |![권장](./media/choose-hybrid-identity-solution/ic195031.png)|
|사용자에 대한 스마트 카드 인증 지원<sup>4</sup>| | |![권장](./media/choose-hybrid-identity-solution/ic195031.png)|
|Hello Windows 10 desktop 및 hello Office 포털에서에서 암호 만료 알림 표시| | |![권장](./media/choose-hybrid-identity-solution/ic195031.png)|

> <sup>1</sup> Single Sign-On을 사용하여 암호 동기화 

> <sup>2</sup> 통과 인증 및 Single Sign-On 

> <sup>3</sup> AD FS를 통해 페더레이션된 Single Sign-On

> <sup>4</sup> AD FS는 엔터프라이즈 PKI tooallow와 통합할 수 있습니다 인증서를 사용 합니다. 이러한 인증서는 MDM 또는 GPO와 같은 신뢰할 수 있는 프로비전 채널이나 스마트 카드 인증서(PIV/CAC 카드 포함) 또는 비즈니스용 Hello(cert-trust)를 통해 배포되는 소프트 인증서일 수 있습니다. 스마트 카드 인증 지원에 대한 자세한 내용은 [이 블로그](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/)를 참조하세요.


## <a name="next-steps"></a>다음 단계
[개념 환경의 Azure 증명에 대한 자세한 정보](https://aka.ms/aad-poc)

[Azure AD Connect 설치](http://go.microsoft.com/fwlink/?LinkId=615771)

[하이브리드 ID 동기화 모니터링](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health)

